# Laboratório 02 — Investigação de Credential Dumping com Mimikatz

**Conceito**

Credential Dumping é uma técnica utilizada por atacantes para roubar credenciais armazenadas em memória.

**O alvo mais comum é o processo:**

lsass.exe

( Local Security Authority Subsystem Service )

É nele que o Windows mantém informações relacionadas à autenticação.

**Ferramentas como:**

- Mimikatz
- LaZagne
- Nanodump
- ProcDump

são frequentemente utilizadas para extrair credenciais.

**No framework MITRE ATT&CK, essa técnica está associada a:**

- Credential Access
- T1003
  
**Cenário**

Sou analista SOC Nível 1 da empresa fictícia SecureBank.

Durante meu turno, recebi um alerta do EDR indicando possível acesso ao processo LSASS.

**Alerta recebido**

Alert Name:<br>
Possible Credential Dumping

Severity: <br>
High

Host: <br>
FIN-PC-023

User: <br>
j.santos

Detection:<br>
Suspicious LSASS Access

Time:<br>
2026-06-18 10:21:44

**Primeira análise**

Assim que recebi o alerta pensei:

O que preciso descobrir? <br>
Quem acessou o LSASS? <br>
Qual processo realizou o acesso? <br>
Foi uma ferramenta legítima? <br>
Houve roubo de credenciais? <br>
Existe movimentação lateral posterior? <br>
Investigação Inicial

Comecei pesquisando os eventos relacionados ao host.

**Splunk** <br>
index=windows <br>
host="FIN-PC-023" <br>
lsass.exe

**Resultado:**

Target Process: <br>
lsass.exe

Source Process: <br>
mimikatz.exe

User: <br>
j.santos

**Primeira conclusão**

O alerta ficou muito mais sério.

Eu não estava mais investigando apenas um acesso suspeito.

Agora eu tinha evidência direta de:

mimikatz.exe<br>
Investigando Criação do Processo

**Queria descobrir:**

- quem executou
- de onde veio
- qual foi o processo pai
  
**Splunk** <br>
index=windows <br>
host="FIN-PC-023" <br>
mimikatz.exe

**Resultado:**

EventCode: 4688

Process: <br>
mimikatz.exe

Path: <br>
C:\Users\j.santos\Downloads\mimikatz.exe

Parent Process: <br>
cmd.exe 

**Análise**

Nesse momento observei:

executado manualmente <br>
veio da pasta Downloads <br>
iniciado através do CMD

Comportamento bastante suspeito.

**Investigando Linha de Comando**

Agora queria saber exatamente o que foi executado.

**KQL**<br>
DeviceProcessEvents <br>
| where DeviceName == "FIN-PC-023" <br>
| where FileName == "mimikatz.exe" <br>
| project Timestamp, <br>
ProcessCommandLine

**Resultado:**

mimikatz.exe <br>
privilege::debug <br>
sekurlsa::logonpasswords <br>
exit

**Minha análise**

O comando:

sekurlsa::logonpasswords

é um dos comandos mais conhecidos do Mimikatz.

**Seu objetivo:**

- Extrair credenciais
- Extrair hashes NTLM
- Extrair tickets Kerberos
  
**Verificando Resultado da Extração**

Procurei eventos posteriores.

**Splunk**<br>
index=windows <br>
host="FIN-PC-023" <br>
("NTLM" OR "Kerberos")

**Resultado:**

Account: <br>
backup.service

NTLM Hash: <br>
aad3b435b51404eeaad3...<br>
Mudança de Severidade

**Agora eu tinha:**

✅ Execução do Mimikatz

✅ Acesso ao LSASS

✅ Extração de credenciais

O comprometimento estava praticamente confirmado.

Investigando Movimentação Posterior

Ataques raramente param após o Credential Dumping.

O próximo passo normalmente é:

Lateral Movement

Investigando Logins Após o Dump

**KQL**<br>
DeviceLogonEvents <br>
| where AccountName == "backup.service" <br>
| project Timestamp, <br>
DeviceName, <br>
LogonType

**Resultado:**

10:24 <br>
SERVER-FILE01

10:26 <br>
SERVER-BACKUP01

10:29 <br>
SERVER-DB01

**Nova descoberta**

A conta extraída começou a aparecer em outros servidores.

**Isso indicava:**

Possível uso das credenciais roubadas

Investigando Origem do Mimikatz

**Agora queria descobrir:**

Como o arquivo chegou na máquina?

**Splunk**<br>
index=proxy <br>
host="FIN-PC-023" <br>
mimikatz.exe

**Resultado:**

URL:

hxxps://fileshare-upload[.]com/tools/mimikatz.exe <br>
Investigando Outros Hosts

Uma pergunta importante:

O atacante executou Mimikatz apenas nesta máquina?

**Splunk** <br>
index=windows <br>
mimikatz.exe

Resultado:

FIN-PC-023

Somente um host afetado.

Investigando Persistência

Procurei sinais de persistência após o roubo de credenciais.

**KQL** <br>
DeviceRegistryEvents <br>
| where DeviceName == "FIN-PC-023" <br>
| where RegistryKey contains "Run"

**Resultado:**

Nenhum resultado encontrado <br>
Conclusão da Investigação

**Eu já possuía evidências suficientes:**

Cadeia do Ataque <br>
Download do Mimikatz <br>
↓ <br>
Execução local <br>
↓ <br>
Acesso ao LSASS <br>
↓ <br>
Extração de credenciais <br>
↓ <br>
Uso da conta backup.service <br>
↓ <br>
Acesso a múltiplos servidores 

**IOC Identificados**

**Arquivo** <br>
mimikatz.exe

**URL** <br>
fileshare-upload.com

**Conta comprometida** <br>
backup.service

**Host inicial** <br>
FIN-PC-023

**Timeline do Ataque** <br>
10:18 Download do Mimikatz

10:20 Execução do arquivo

10:21 Acesso ao LSASS

10:22 Extração de credenciais

10:24 Login SERVER-FILE01

10:26 Login SERVER-BACKUP01

10:29 Login SERVER-DB01

10:31 Alerta gerado

**Ações Como SOC N1** <br>
Contenção <br>
Escalar imediatamente para N2 <br>
Solicitar isolamento de FIN-PC-023 <br>
Solicitar bloqueio da conta backup.service <br>
Solicitar reset de credenciais <br>

**Hunting**

**Pesquisar:**
**SPL**<br>
index=windows <br>
backup.service

e

**SPL** <br>
index=windows <br>
lsass.exe

para identificar outros acessos suspeitos.

**Relatório Final SOC N1**

Foi identificado possível Credential Dumping
na estação FIN-PC-023.

Durante a investigação foi observada a execução
da ferramenta mimikatz.exe com uso do comando
sekurlsa::logonpasswords.

Foi confirmado acesso ao processo lsass.exe
e extração de credenciais da conta backup.service.

Posteriormente foram identificadas autenticações
da conta comprometida em múltiplos servidores.

**IOC identificados:**

- mimikatz.exe
- fileshare-upload.com
- backup.service
- FIN-PC-023

Incidente escalado para equipe N2
devido ao risco de comprometimento lateral.
