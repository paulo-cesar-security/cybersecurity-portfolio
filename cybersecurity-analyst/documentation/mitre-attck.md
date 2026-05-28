# MITRE ATT&CK para Cibersegurança

Resumo de técnicas MITRE ATT&CK importantes para SOC, Threat Hunting, SIEM e Resposta a Incidentes.

---

# O que é MITRE ATT&CK?

MITRE ATT&CK é um framework utilizado para mapear:

* comportamento de atacantes
* técnicas de invasão
* persistência
* movimentação lateral
* exfiltração

Muito utilizado em:

* SOC
* SIEM
* Threat Hunting
* Red Team
* Blue Team

---

# Initial Access

## T1190 - Exploit Public-Facing Application

### Descrição

Exploração de aplicações expostas na internet.

### Exemplos

* vulnerabilidades web
* RCE
* SQL Injection

### Indicadores

* acessos incomuns
* spikes HTTP 500
* execução remota

---

## T1566 - Phishing

### Descrição

Ataques via e-mail malicioso.

### Exemplos

* anexos maliciosos
* links maliciosos
* macros Office

### Indicadores

* Office criando PowerShell
* downloads suspeitos
* mshta.exe

---

# Execution

## T1059 - Command and Scripting Interpreter

### Descrição

Execução de comandos/scripts.

### Ferramentas comuns

* PowerShell
* cmd.exe
* bash
* python

### Indicadores

* comandos codificados
* scripts remotos
* execução suspeita

---

## T1204 - User Execution

### Descrição

Usuário executa arquivo malicioso.

### Exemplos

* arquivos ISO
* executáveis
* macros

---

# Persistence

## T1547 - Boot or Logon Autostart Execution

### Descrição

Persistência automática após reinicialização.

### Exemplos

* Run Keys
* Startup Folder
* Serviços

### Indicadores

* alterações no registro
* novos serviços
* tarefas agendadas

---

## T1053 - Scheduled Task

### Descrição

Persistência via tarefas agendadas.

### Indicadores

* Event ID 4698
* tarefas incomuns

---

# Privilege Escalation

## T1068 - Exploitation for Privilege Escalation

### Descrição

Exploração para ganho de privilégios.

### Exemplos

* vulnerabilidades locais
* drivers vulneráveis

---

## T1134 - Access Token Manipulation

### Descrição

Abuso de tokens de acesso.

### Indicadores

* processos suspeitos
* impersonation

---

# Defense Evasion

## T1027 - Obfuscated Files or Information

### Descrição

Ofuscação de scripts/comandos.

### Exemplos

* Base64
* PowerShell encoded

### Indicadores

* "-enc"
* strings grandes codificadas

---

## T1562 - Impair Defenses

### Descrição

Tentativa de desativar mecanismos de defesa.

### Exemplos

* desativar Defender
* parar antivírus

### Indicadores

* Event ID 5001
* Event ID 5007

---

# Credential Access

## T1003 - OS Credential Dumping

### Descrição

Roubo de credenciais.

### Ferramentas comuns

* Mimikatz
* LSASS dumping

### Indicadores

* acesso ao LSASS
* Sysmon Event ID 10

---

## T1110 - Brute Force

### Descrição

Ataques de senha.

### Indicadores

* múltiplos 4625
* lockouts
* várias tentativas

---

# Discovery

## T1082 - System Information Discovery

### Descrição

Coleta de informações do sistema.

### Comandos comuns

* systeminfo
* hostname
* whoami

---

## T1018 - Remote System Discovery

### Descrição

Descoberta de hosts remotos.

### Exemplos

* ping sweep
* net view
* arp

---

# Lateral Movement

## T1021 - Remote Services

### Descrição

Movimento lateral usando serviços remotos.

### Exemplos

* RDP
* SMB
* PsExec
* WinRM

### Indicadores

* 4624 Tipo 3
* 4624 Tipo 10
* 5140

---

# Collection

## T1113 - Screen Capture

### Descrição

Captura de tela.

### Indicadores

* ferramentas de screenshot
* processos suspeitos

---

## T1005 - Data from Local System

### Descrição

Coleta de arquivos locais.

### Indicadores

* compressão de arquivos
* acessos incomuns

---

# Command and Control

## T1071 - Application Layer Protocol

### Descrição

Comunicação C2 usando protocolos comuns.

### Exemplos

* HTTP
* HTTPS
* DNS

### Indicadores

* beaconing
* conexões externas incomuns

---

## T1095 - Non-Application Layer Protocol

### Descrição

Uso de protocolos incomuns.

### Indicadores

* portas estranhas
* tráfego anômalo

---

# Exfiltration

## T1041 - Exfiltration Over C2 Channel

### Descrição

Exfiltração via canal C2.

### Indicadores

* upload incomum
* tráfego criptografado suspeito

---

# Impact

## T1486 - Data Encrypted for Impact

### Descrição

Ransomware.

### Indicadores

* criptografia massiva
* criação de extensões
* deleção de backups

---

# Técnicas Mais Importantes para SOC

## Alta Prioridade

* T1059
* T1003
* T1110
* T1027
* T1547
* T1053
* T1021
* T1562
* T1071
* T1486

---

# Ferramentas Frequentemente Associadas

| Ferramenta | Técnicas |
| ---------- | -------- |
| PowerShell | T1059    |
| Mimikatz   | T1003    |
| PsExec     | T1021    |
| certutil   | T1105    |
| mshta      | T1218    |
| rundll32   | T1218    |

---

# Indicadores Mais Comuns

## Alta Prioridade

* PowerShell codificado
* criação de serviços
* tarefas agendadas
* brute force
* conexões SMB
* desativação do Defender
* criação de usuários

---

# Referências

* MITRE ATT&CK
* Microsoft Learn
* SigmaHQ
* Elastic Security
* Wazuh Documentation
