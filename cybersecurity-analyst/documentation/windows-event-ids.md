# Windows Event IDs para Cibersegurança

## Eventos de Autenticação

| Event ID | Descrição                                 | Importância                    |
| -------- | ----------------------------------------- | ------------------------------ |
| 4624     | Logon realizado com sucesso               | Monitoramento de autenticações |
| 4625     | Falha de logon                            | Detecção de brute force        |
| 4634     | Logoff realizado                          | Rastreamento de sessão         |
| 4647     | Usuário iniciou logoff                    | Atividade do usuário           |
| 4648     | Logon usando credenciais explícitas       | Possível abuso de credenciais  |
| 4672     | Privilégios especiais atribuídos          | Logon administrativo           |
| 4768     | Solicitação de TGT Kerberos               | Monitoramento Kerberos         |
| 4769     | Solicitação de ticket de serviço Kerberos | Detecção de Kerberoasting      |
| 4771     | Falha de pré-autenticação Kerberos        | Ataques de senha               |
| 4776     | Tentativa de autenticação NTLM            | Monitoramento NTLM             |

---

# Eventos de Criação e Execução de Processos

| Event ID | Descrição              | Importância               |
| -------- | ---------------------- | ------------------------- |
| 4688     | Processo criado        | Threat Hunting            |
| 4689     | Processo encerrado     | Rastreamento de processos |
| 4697     | Serviço instalado      | Persistência              |
| 7045     | Novo serviço instalado | Malware/Persistência      |
| 7036     | Serviço alterou estado | Monitoramento de serviços |

---

# Eventos de Contas de Usuário

| Event ID | Descrição                         | Importância                  |
| -------- | --------------------------------- | ---------------------------- |
| 4720     | Conta de usuário criada           | Criação suspeita de usuários |
| 4722     | Conta habilitada                  | Ativação indevida            |
| 4723     | Tentativa de alteração de senha   | Modificação de conta         |
| 4724     | Tentativa de redefinição de senha | Escalada de privilégio       |
| 4725     | Conta desabilitada                | Monitoramento administrativo |
| 4726     | Conta deletada                    | Exclusão de usuários         |
| 4732     | Usuário adicionado a grupo local  | Escalada de privilégio       |
| 4738     | Conta modificada                  | Alterações em usuários       |
| 4740     | Conta bloqueada                   | Indicador de brute force     |

---

# Eventos de Política e Permissões

| Event ID | Descrição                      | Importância               |
| -------- | ------------------------------ | ------------------------- |
| 4719     | Política de auditoria alterada | Tentativa de ocultar logs |
| 4739     | Política de domínio alterada   | Modificação de domínio    |
| 4670     | Permissões de objeto alteradas | Alteração suspeita        |

---

# Eventos de Acesso Remoto e Movimento Lateral

| Event ID     | Descrição                           | Importância           |
| ------------ | ----------------------------------- | --------------------- |
| 4624 Tipo 3  | Logon de rede                       | SMB e acessos remotos |
| 4624 Tipo 10 | Logon RDP                           | Acesso remoto via RDP |
| 4778         | Sessão RDP reconectada              | Rastreamento RDP      |
| 4779         | Sessão RDP desconectada             | Rastreamento RDP      |
| 5140         | Compartilhamento de rede acessado   | Monitoramento SMB     |
| 5145         | Acesso detalhado a compartilhamento | Movimento lateral     |

---

# Eventos PowerShell

| Event ID | Descrição                     | Importância                      |
| -------- | ----------------------------- | -------------------------------- |
| 4103     | Logging de módulos PowerShell | Atividade PowerShell             |
| 4104     | Script Block Logging          | Detecção de PowerShell malicioso |
| 4105     | Comando PowerShell iniciado   | Monitoramento                    |
| 4106     | Comando PowerShell finalizado | Rastreamento                     |

---

# Eventos do Microsoft Defender

| Event ID | Descrição                         | Importância              |
| -------- | --------------------------------- | ------------------------ |
| 1116     | Malware detectado                 | Detecção de ameaça       |
| 1117     | Remediação iniciada               | Atividade antivírus      |
| 5001     | Proteção em tempo real alterada   | Tentativa de desativação |
| 5007     | Configuração do Defender alterada | Alteração suspeita       |

---

# Eventos de Persistência

| Event ID | Descrição                | Importância        |
| -------- | ------------------------ | ------------------ |
| 4698     | Tarefa agendada criada   | Persistência       |
| 4699     | Tarefa agendada deletada | Limpeza de rastros |
| 4700     | Tarefa habilitada        | Persistência       |
| 4701     | Tarefa desabilitada      | Evasão de defesa   |

---

# Eventos Sysmon (Muito Importantes)

| Sysmon ID | Descrição                  | Importância          |
| --------- | -------------------------- | -------------------- |
| 1         | Criação de processo        | Threat Hunting       |
| 3         | Conexão de rede            | Detecção C2          |
| 7         | DLL carregada              | Monitoramento DLL    |
| 8         | CreateRemoteThread         | Injeção de código    |
| 10        | Acesso a processo          | Credential Dumping   |
| 11        | Arquivo criado             | Malware              |
| 12        | Registro criado/deletado   | Persistência         |
| 13        | Valor de registro alterado | Autoruns             |
| 22        | Consulta DNS               | DNS Tunneling        |
| 24        | Alteração de clipboard     | Possível exfiltração |

---

# Event IDs Mais Importantes para SOC

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
* 4104
* 7045
* Sysmon 1
* Sysmon 3
* Sysmon 10

---

# Exemplos de Detecção

## Brute Force

Monitorar:

* múltiplos eventos 4625
* mesmo IP
* vários usuários

## Abuso de PowerShell

Monitorar:

* 4104
* comandos codificados em Base64
* download de scripts

## Movimento Lateral

Monitorar:

* 4624 Tipo 3
* 5140
* 5145
* atividade PsExec

## Persistência

Monitorar:

* 4698
* 7045
* alterações de registro

---

# Referências

* Microsoft Learn
* Sysmon Documentation
* MITRE ATT&CK
* Elastic Detection Rules
* Sigma Rules
