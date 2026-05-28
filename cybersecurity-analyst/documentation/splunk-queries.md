# Splunk Queries para Cibersegurança

Consultas SPL (Search Processing Language) utilizadas para investigação, threat hunting e monitoramento em ambientes Splunk.

---

# Falhas de Login (Brute Force)

## Detectar múltiplas falhas de autenticação

```spl id="e8x3fa"
index=wineventlog EventCode=4625
| stats count by src_ip, Account_Name
| sort - count
```

### Objetivo

Detectar brute force ou password spraying.

---

# Logons Administrativos

```spl id="q4v7km"
index=wineventlog EventCode=4672
| table _time, host, Account_Name
```

### Objetivo

Monitorar logons administrativos.

---

# Logons RDP

```spl id="p6r1fd"
index=wineventlog EventCode=4624 Logon_Type=10
| table _time, Account_Name, src_ip, host
```

### Objetivo

Detectar acessos remotos via RDP.

---

# Contas Bloqueadas

```spl id="0w5f6i"
index=wineventlog EventCode=4740
| table _time, Target_Account, host
```

### Objetivo

Identificar possíveis ataques de senha.

---

# Criação de Processos

```spl id="n5r4fz"
index=wineventlog EventCode=4688
| table _time, host, New_Process_Name, CommandLine
```

### Objetivo

Threat Hunting e investigação.

---

# PowerShell Codificado

```spl id="w4v6xa"
index=wineventlog EventCode=4688 CommandLine="*-enc*"
```

### Objetivo

Detectar PowerShell Base64.

---

# Download via PowerShell

```spl id="j8d9cm"
index=wineventlog EventCode=4688 CommandLine="*DownloadString*"
```

### Objetivo

Detectar download remoto de scripts.

---

# LOLBins

## Certutil

```spl id="v6u2qe"
index=wineventlog EventCode=4688 New_Process_Name="*certutil.exe"
```

---

## Mshta

```spl id="v9m0kt"
index=wineventlog EventCode=4688 New_Process_Name="*mshta.exe"
```

---

## Rundll32

```spl id="6q7h5i"
index=wineventlog EventCode=4688 New_Process_Name="*rundll32.exe"
```

---

## Regsvr32

```spl id="n4u9hf"
index=wineventlog EventCode=4688 New_Process_Name="*regsvr32.exe"
```

---

# Criação de Usuário

```spl id="q9n7x5"
index=wineventlog EventCode=4720
| table _time, Subject_Account_Name, Target_Account_Name
```

### Objetivo

Monitorar criação de contas.

---

# Adição a Grupo Administrativo

```spl id="d7r3xa"
index=wineventlog EventCode=4732
| table _time, Member_Name, Group_Name
```

### Objetivo

Detectar escalada de privilégios.

---

# Tarefas Agendadas

```spl id="t7u0ah"
index=wineventlog EventCode=4698
```

### Objetivo

Detectar persistência.

---

# Serviços Instalados

```spl id="h5m1w8"
index=wineventlog EventCode=7045
```

### Objetivo

Monitorar persistência via serviços.

---

# Compartilhamentos SMB

```spl id="q7r4kw"
index=wineventlog EventCode=5140
| table _time, Share_Name, Account_Name, src_ip
```

### Objetivo

Monitorar acessos SMB.

---

# Sysmon - Conexões de Rede

```spl id="6f5r1m"
index=sysmon EventCode=3
| table _time, Image, DestinationIp, DestinationPort
```

### Objetivo

Detectar conexões suspeitas.

---

# Sysmon - DNS Query

```spl id="m3v4qh"
index=sysmon EventCode=22
| stats count by QueryName
| sort - count
```

### Objetivo

Detectar beaconing e DNS tunneling.

---

# IOC Hunting por IP

```spl id="n6f8ri"
index=* src_ip="8.8.8.8"
```

### Objetivo

Investigar IOC de IP.

---

# IOC Hunting por Hash

```spl id="q5h2vo"
index=* SHA256="HASH_AQUI"
```

### Objetivo

Investigar malware conhecido.

---

# Processos Filhos do Office

```spl id="y4w7bz"
index=wineventlog EventCode=4688
Parent_Process_Name IN ("*WINWORD.EXE","*EXCEL.EXE","*OUTLOOK.EXE")
```

### Objetivo

Detectar macros e execução maliciosa.

---

# Conexões para Portas Incomuns

```spl id="f5n9jv"
index=sysmon EventCode=3
NOT DestinationPort IN (80,443,53)
```

### Objetivo

Identificar possível C2.

---

# Defender Desativado

```spl id="0q9xpk"
index=wineventlog EventCode IN (5001,5007)
```

### Objetivo

Detectar evasão de defesa.

---

# Top Event IDs

```spl id="r8y2af"
index=wineventlog
| stats count by EventCode
| sort - count
```

### Objetivo

Visualizar eventos mais frequentes.

---

# Técnicas MITRE ATT&CK Relacionadas

| Técnica | Nome                              |
| ------- | --------------------------------- |
| T1059   | Command and Scripting Interpreter |
| T1003   | Credential Dumping                |
| T1021   | Remote Services                   |
| T1110   | Brute Force                       |
| T1547   | Persistência                      |
| T1562   | Defense Evasion                   |

---

# Event IDs Mais Importantes

## Alta Prioridade

* 4625
* 4688
* 4698
* 4720
* 4732
* 4769
* 7045
* Sysmon 1
* Sysmon 3
* Sysmon 10

---

# Indicadores Suspeitos

## Possíveis sinais de ataque

* PowerShell Base64
* LOLBins
* brute force
* tarefas agendadas
* serviços suspeitos
* conexões externas
* desativação do Defender

---

# Referências

* [Splunk Documentation](https://docs.splunk.com/Documentation/Splunk
* MITRE ATT&CK
* SigmaHQ
* Microsoft Learn
* Sysmon Documentation
