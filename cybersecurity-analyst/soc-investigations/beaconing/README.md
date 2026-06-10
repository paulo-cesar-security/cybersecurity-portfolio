# Laboratório — Investigação de Beaconing (Command & Control)

**Conceito**

Beaconing ocorre quando um malware comprometido faz contato periódico com um servidor do atacante (C2 - Command & Control).

**O objetivo do atacante pode ser:**

- Receber comandos
- Baixar payloads
- Exfiltrar dados
- Manter persistência

Um dos principais sinais é a regularidade das conexões.

**Exemplo:**

09:00:00<br>
09:05:00<br>
09:10:00<br>
09:15:00<br>
09:20:00

Humanos não trabalham assim.

Malwares sim.

**Cenário**

Sou analista SOC Nível 1 da empresa fictícia TechSolutions.

Às 14:30, o SIEM gerou um alerta indicando possível comunicação periódica com um domínio malicioso.

**Alerta recebido**

**Alert Name:** <br>
Possible Beaconing Activity

**Severity:** <br>
High

**Host:** <br>
HR-PC-017

**User:** <br>
c.oliveira

**Destination:** <br>
api-cloudsync.net

**Time:** <br>
2026-06-15 14:30:11

**Primeira análise**

Antes de abrir qualquer log, pensei:

- O que preciso responder?
- O host realmente está se comunicando periodicamente?
- Qual processo está gerando a comunicação?
- Existe malware?
- O host está comprometido?
- Houve movimentação posterior?
- Investigação Inicial no Splunk

Primeiro procurei todas as conexões relacionadas ao domínio.

**</> Spl:**

index=proxy <br>
host="HR-PC-017" <br>
"api-cloudsync.net"

**Resultado:**

14:00:02 <br>
14:05:01 <br>
14:10:02 <br>
14:15:01 <br>
14:20:02 <br>
14:25:01 <br>
14:30:02

Minha primeira conclusão

Algo chamou atenção imediatamente.

As conexões aconteciam praticamente a cada 5 minutos.

Esse padrão é extremamente incomum para atividade humana.

Comecei a suspeitar de:

Command & Control (C2) <br>
Refinando a análise

Quis medir exatamente o intervalo entre eventos.

**Pesquisa:**

**</> Spl:**

index=proxy <br>
host="HR-PC-017" <br>
"api-cloudsync.net" <br>
| table _time host url

**Resultado:**

| Horário  | URL               |
| -------- | ----------------- |
| 14:00:02 | api-cloudsync.net |
| 14:05:01 | api-cloudsync.net |
| 14:10:02 | api-cloudsync.net |
| 14:15:01 | api-cloudsync.net |
| 14:20:02 | api-cloudsync.net |

**Investigação no Sentinel (KQL)**

Agora precisava descobrir qual processo gerava as conexões.

DeviceNetworkEvents <br>
| where DeviceName == "HR-PC-017" <br>
| where RemoteUrl contains "api-cloudsync.net" <br>
| project Timestamp, <br>
InitiatingProcessFileName, <br>
InitiatingProcessCommandLine, <br>
RemoteIP

**Resultado:**

Process: <br>
updater.exe

Path:<br>
C:\Users\c.oliveira\AppData\Roaming\updater.exe

RemoteIP: <br>
185.221.99.44

**Mudança de Severidade**

Nesse momento meu alerta mental aumentou.

Por quê?

O executável estava em:

C:\Users\c.oliveira\AppData\Roaming\

Local muito utilizado por malware.

**Investigando o Processo**

Agora queria saber:

Quando esse processo apareceu?

**Splunk**

index=windows <br>
host="HR-PC-017" <br>
updater.exe

**Resultado:**

EventCode=4688

Process: <br>
updater.exe

Parent: <br>
winword.exe <br>
Nova descoberta

O malware foi iniciado pelo:

WINWORD.EXE

Isso muda completamente a investigação.

**Agora existe forte suspeita de:**

Documento malicioso <br>
Investigando o Documento

Procurei eventos anteriores.

index=email <br>
recipient="c.oliveira@techsolutions.com"

**Resultado:**

Subject: <br>
Updated Benefits Policy

Attachment: <br>
Benefits_Update.docm

Sender: <br>
rh-beneficios@consulting-update.com <br>
Minha hipótese

**Sequência provável:**

Email recebido <br>
↓ <br>
Documento DOCM aberto <br>
↓ <br>
Macro executada <br>
↓ <br>
updater.exe instalado <br>
↓ <br>
Beaconing iniciado <br>
Confirmando Persistência

Malwares de C2 normalmente sobrevivem ao reboot.

Procurei persistência.

**KQL** <br>
DeviceRegistryEvents <br>
| where DeviceName == "HR-PC-017" <br>
| where RegistryKey contains "Run"

**Resultado:**

Registry Key:

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Value:

UpdaterAgent <br>
Agora o cenário ficou claro

Eu já tinha:

✅ Documento malicioso

✅ Execução de malware

✅ Persistência

✅ Comunicação periódica

Verificando Possível Download de Payload

Procurei downloads adicionais.

DeviceNetworkEvents <br>
| where DeviceName == "HR-PC-017" <br>
| where InitiatingProcessFileName == "updater.exe"

**Resultado:**

GET /payload.bin

Response: <br>
200 OK

Downloaded: <br>
523 KB <br>
Conclusão

Agora o incidente não era mais suspeita.

Era comprometimento confirmado.

IOC Identificados <br>
Domínio <br>
api-cloudsync.net <br>
IP <br>
185.221.99.44 <br>
Arquivo <br>
updater.exe <br>
Documento <br>
Benefits_Update.docm <br>
Remetente <br>
rh-beneficios@consulting-update.com

**Timeline do Ataque**

13:41 Email recebido

13:44 Documento aberto

13:44 Macro executada

13:45 updater.exe criado

14:00 Primeiro beacon

14:05 Segundo beacon

14:10 Terceiro beacon

14:15 Quarto beacon

14:20 Quinto beacon

14:25 Sexto beacon

14:30 Alerta gerado

Ações Como SOC N1

**Após confirmar o incidente:**

- Contenção
- Escalar para N2 imediatamente
- Solicitar isolamento do host
- Solicitar bloqueio do domínio
- Solicitar bloqueio do IP
- Documentação
- Registrar IOC
- Registrar timeline
- Registrar evidências
- Hunting

Pesquisar em outros hosts:

index=proxy <br>
"api-cloudsync.net"

e

index=windows <br>
updater.exe

para verificar se existem outras máquinas comprometidas.

**Relatório Final SOC N1**

Foi identificado comprometimento da estação <br>
HR-PC-017 através de documento malicioso recebido por e-mail.

A investigação revelou execução de macro <br>
presente no arquivo Benefits_Update.docm, <br>
resultando na criação do executável updater.exe.

O malware estabeleceu comunicação periódica <br>
(beaconing) com o domínio api-cloudsync.net <br>
em intervalos aproximados de 5 minutos.

Também foi identificada persistência através <br>
da chave HKCU\Software\Microsoft\Windows\CurrentVersion\Run.

**IOC coletados:**

- api-cloudsync.net
- 185.221.99.44
- updater.exe
- Benefits_Update.docm

Incidente escalado para equipe N2 para contenção.





