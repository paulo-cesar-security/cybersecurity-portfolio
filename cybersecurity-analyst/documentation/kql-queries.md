# KQL Queries para Cibersegurança

Consultas KQL utilizadas para investigação, threat hunting e monitoramento em SIEMs como Microsoft Sentinel e Defender XDR.

---

# Falhas de Login (Brute Force)

## Múltiplas falhas de autenticação

```kql
SecurityEvent
| where EventID == 4625
| summarize Tentativas=count() by IpAddress, Account
| order by Tentativas desc
```

### Objetivo

Detectar brute force ou password spraying.

---

# Logins Administrativos

```kql
SecurityEvent
| where EventID == 4672
| project TimeGenerated, Account, Computer
```

### Objetivo

Monitorar logons administrativos.

---

# Logins RDP

```kql
SecurityEvent
| where EventID == 4624
| where LogonType == 10
| project TimeGenerated, Account, IpAddress, Computer
```

### Objetivo

Identificar acessos remotos via RDP.

---

# Contas Bloqueadas

```kql
SecurityEvent
| where EventID == 4740
| project TimeGenerated, TargetAccount, Computer
```

### Objetivo

Detectar contas bloqueadas por múltiplas falhas.

---

# Criação de Processos Suspeitos

```kql
SecurityEvent
| where EventID == 4688
| where Process has_any ("powershell.exe","cmd.exe","rundll32.exe","certutil.exe")
| project TimeGenerated, Account, Process, CommandLine
```

### Objetivo

Identificar ferramentas frequentemente utilizadas em ataques.

---

# PowerShell Codificado

```kql
SecurityEvent
| where EventID == 4688
| where CommandLine contains "-enc"
| project TimeGenerated, Account, CommandLine
```

### Objetivo

Detectar PowerShell codificado em Base64.

---

# Downloads Suspeitos PowerShell

```kql
SecurityEvent
| where EventID == 4688
| where CommandLine contains "DownloadString"
```

### Objetivo

Detectar download remoto de scripts.

---

# Criação de Usuários

```kql
SecurityEvent
| where EventID == 4720
| project TimeGenerated, TargetAccount, SubjectAccount
```

### Objetivo

Monitorar criação de contas.

---

# Adição a Grupo Administrativo

```kql
SecurityEvent
| where EventID == 4732
| project TimeGenerated, MemberName, GroupName
```

### Objetivo

Detectar escalada de privilégios.

---

# Serviços Instalados

```kql
SecurityEvent
| where EventID == 7045
| project TimeGenerated, ServiceName, Account
```

### Objetivo

Detectar persistência por serviços.

---

# Tarefas Agendadas

```kql
SecurityEvent
| where EventID == 4698
| project TimeGenerated, TaskName, SubjectAccount
```

### Objetivo

Detectar persistência por Scheduled Tasks.

---

# Compartilhamentos SMB

```kql
SecurityEvent
| where EventID == 5140
| project TimeGenerated, Account, ShareName, IpAddress
```

### Objetivo

Monitorar acessos SMB.

---

# Conexões de Rede Sysmon

```kql
Event
| where EventID == 3
| project TimeGenerated, Computer, DestinationIp, DestinationPort, Image
```

### Objetivo

Detectar conexões suspeitas e possíveis C2.

---

# DNS Suspeito (Sysmon)

```kql
Event
| where EventID == 22
| summarize Consultas=count() by QueryName
| order by Consultas desc
```

### Objetivo

Detectar DNS tunneling ou beaconing.

---

# Execução de LOLBins

```kql
SecurityEvent
| where EventID == 4688
| where Process has_any (
    "certutil.exe",
    "mshta.exe",
    "regsvr32.exe",
    "rundll32.exe",
    "wmic.exe"
)
```

### Objetivo

Detectar Living Off The Land Binaries.

---

# Processos Filhos do Office

```kql
SecurityEvent
| where EventID == 4688
| where ParentProcessName has_any ("WINWORD.EXE","EXCEL.EXE","OUTLOOK.EXE")
```

### Objetivo

Detectar possível execução maliciosa via Office.

---

# Conexões Externas para Portas Incomuns

```kql
DeviceNetworkEvents
| where RemotePort !in (80,443,53,25)
| summarize Conexoes=count() by RemoteIP, RemotePort
| order by Conexoes desc
```

### Objetivo

Detectar comunicação suspeita.

---

# Alterações no Microsoft Defender

```kql
Event
| where EventID in (5001,5007)
| project TimeGenerated, Computer, RenderedDescription
```

### Objetivo

Detectar tentativa de desativar proteções.

---

# IOC Hunting por IP

```kql
DeviceNetworkEvents
| where RemoteIP == "8.8.8.8"
```

### Objetivo

Investigar IOC de IP.

---

# IOC Hunting por Hash

```kql
DeviceFileEvents
| where SHA256 == "HASH_AQUI"
```

### Objetivo

Investigar malware conhecido.

---

# Top Event IDs

```kql
SecurityEvent
| summarize Total=count() by EventID
| order by Total desc
```

### Objetivo

Identificar eventos mais frequentes.

---

# Eventos Mais Importantes para SOC

## Alta Prioridade

* 4624
* 4625
* 4688
* 4698
* 4720
* 4732
* 4740
* 4768
* 4769
* 7045

---

# Referências

* Microsoft Learn
* Microsoft Sentinel Documentation
* Defender XDR Documentation
* MITRE ATT&CK
* Sigma Rules
