# PowerShell para Cibersegurança

Comandos PowerShell úteis para monitoramento, investigação, threat hunting e resposta a incidentes.

---

# Informações do Sistema

## Informações do computador

```powershell id="p49h1e"
systeminfo
```

### Objetivo

Obter informações do sistema operacional e patches.

---

## Versão do PowerShell

```powershell id="9e5h4f"
$PSVersionTable
```

### Objetivo

Verificar versão do PowerShell.

---

# Processos

## Listar processos

```powershell id="cvk2vv"
Get-Process
```

### Objetivo

Visualizar processos ativos.

---

## Buscar PowerShell em execução

```powershell id="6o1r1m"
Get-Process powershell
```

### Objetivo

Monitorar sessões PowerShell.

---

## Encerrar processo

```powershell id="h3aj4t"
Stop-Process -Id PID -Force
```

### Objetivo

Finalizar processo suspeito.

---

# Rede e Conexões

## Ver conexões TCP

```powershell id="f34j8v"
Get-NetTCPConnection
```

### Objetivo

Monitorar conexões de rede.

---

## Ver portas abertas

```powershell id="yw13v7"
netstat -ano
```

### Objetivo

Identificar serviços expostos.

---

## Resolver DNS

```powershell id="x6b8z7"
Resolve-DnsName google.com
```

### Objetivo

Investigar DNS.

---

## Testar conectividade

```powershell id="cv5h3r"
Test-NetConnection google.com
```

### Objetivo

Verificar comunicação de rede.

---

# Usuários e Autenticação

## Usuário atual

```powershell id="5rq1b9"
whoami
```

### Objetivo

Verificar contexto do usuário.

---

## Ver grupos do usuário

```powershell id="m8s0w6"
whoami /groups
```

### Objetivo

Investigar privilégios.

---

## Ver usuários locais

```powershell id="h7oc2i"
Get-LocalUser
```

### Objetivo

Auditoria de contas locais.

---

## Ver grupos locais

```powershell id="j9u7u0"
Get-LocalGroup
```

### Objetivo

Auditoria de grupos.

---

# Logs e Eventos

## Buscar falhas de logon

```powershell id="tr6tkn"
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625}
```

### Objetivo

Detectar brute force.

---

## Buscar criação de processos

```powershell id="a91r1n"
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688}
```

### Objetivo

Threat Hunting.

---

## Buscar PowerShell Script Block Logging

```powershell id="6qj4dn"
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational"
```

### Objetivo

Monitorar scripts PowerShell.

---

# Arquivos e Integridade

## Gerar hash SHA256

```powershell id="e9l4qf"
Get-FileHash arquivo.exe -Algorithm SHA256
```

### Objetivo

Verificar integridade de arquivos.

---

## Buscar arquivos recentes

```powershell id="8l5o7g"
Get-ChildItem C:\ -Recurse | Sort-Object LastWriteTime -Descending
```

### Objetivo

Identificar arquivos recentes.

---

# Serviços e Persistência

## Listar serviços

```powershell id="6n7m9l"
Get-Service
```

### Objetivo

Auditoria de serviços.

---

## Buscar serviços suspeitos

```powershell id="2e7x7o"
Get-Service | Where-Object {$_.Status -eq "Running"}
```

### Objetivo

Investigar persistência.

---

## Ver tarefas agendadas

```powershell id="6j8m0q"
Get-ScheduledTask
```

### Objetivo

Detectar persistência.

---

# Segurança e Defender

## Status do Microsoft Defender

```powershell id="h6j1k0"
Get-MpComputerStatus
```

### Objetivo

Verificar proteção do Defender.

---

## Histórico de ameaças

```powershell id="s7g5q9"
Get-MpThreat
```

### Objetivo

Investigar malware detectado.

---

## Atualizações do Defender

```powershell id="2z3d6k"
Update-MpSignature
```

### Objetivo

Atualizar assinaturas.

---

# Threat Hunting

## Buscar comandos codificados

```powershell id="8f2q0q"
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688} | Where-Object {$_.Message -match "-enc"}
```

### Objetivo

Detectar PowerShell Base64.

---

## Buscar LOLBins

```powershell id="w2m5o8"
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688} | Where-Object {
$_.Message -match "certutil|mshta|rundll32|regsvr32"
}
```

### Objetivo

Detectar Living Off The Land Binaries.

---

## Buscar conexões externas suspeitas

```powershell id="6q4m9p"
Get-NetTCPConnection | Where-Object {$_.RemotePort -notin 80,443,53}
```

### Objetivo

Identificar tráfego suspeito.

---

# Comandos Mais Importantes para SOC

## Alta Prioridade

* Get-WinEvent
* Get-Process
* Get-Service
* Get-NetTCPConnection
* Get-FileHash
* Get-ScheduledTask
* whoami
* systeminfo

---

# Indicadores Suspeitos

## Possíveis sinais de comprometimento

* PowerShell codificado
* execução de certutil
* execução de mshta
* conexões externas incomuns
* tarefas agendadas suspeitas
* serviços desconhecidos

---

# LOLBins Mais Monitorados

## Alta Prioridade

* powershell.exe
* certutil.exe
* mshta.exe
* rundll32.exe
* regsvr32.exe
* wmic.exe
* bitsadmin.exe

---

# Referências

* Microsoft Learn
* PowerShell Documentation
* MITRE ATT&CK
* LOLBAS Project
* Elastic Detection Rules
