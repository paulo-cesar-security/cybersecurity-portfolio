# Comandos Linux para Cibersegurança

Comandos Linux úteis para análise de logs, investigação, monitoramento e threat hunting.

---

# Navegação e Arquivos

## Listar arquivos detalhadamente

```bash id="a1p6nk"
ls -la
```

### Objetivo

Visualizar permissões, usuários e arquivos ocultos.

---

## Buscar arquivos

```bash id="m7fp30"
find / -name "arquivo.txt"
```

### Objetivo

Localizar arquivos suspeitos ou indicadores.

---

## Buscar arquivos modificados recentemente

```bash id="yv1dny"
find / -mtime -1
```

### Objetivo

Identificar alterações recentes no sistema.

---

# Análise de Logs

## Visualizar logs em tempo real

```bash id="x0brdr"
tail -f /var/log/auth.log
```

### Objetivo

Monitorar autenticações em tempo real.

---

## Buscar falhas de login

```bash id="6rbx5r"
grep "Failed password" /var/log/auth.log
```

### Objetivo

Detectar brute force SSH.

---

## Buscar IPs em logs

```bash id="b8c8su"
grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}'
```

### Objetivo

Extrair endereços IP.

---

## Filtrar eventos específicos

```bash id="t7lx9z"
journalctl | grep ssh
```

### Objetivo

Investigar eventos SSH.

---

# Rede e Conexões

## Ver conexões ativas

```bash id="ckmg1o"
ss -tunap
```

### Objetivo

Monitorar conexões suspeitas.

---

## Ver portas abertas

```bash id="5j9u7i"
netstat -tulnp
```

### Objetivo

Identificar serviços expostos.

---

## Testar conectividade

```bash id="r7z6an"
ping 8.8.8.8
```

### Objetivo

Verificar comunicação de rede.

---

## Consultar DNS

```bash id="btqoyv"
dig google.com
```

### Objetivo

Análise DNS.

---

## Capturar tráfego

```bash id="0o6nza"
tcpdump -i eth0
```

### Objetivo

Analisar pacotes de rede.

---

# Processos e Execução

## Ver processos ativos

```bash id="5f0w0t"
ps aux
```

### Objetivo

Identificar processos suspeitos.

---

## Monitoramento interativo

```bash id="8l4h0k"
top
```

### Objetivo

Monitorar CPU e memória.

---

## Encerrar processo

```bash id="v4x9v8"
kill -9 PID
```

### Objetivo

Finalizar processo malicioso.

---

## Ver árvore de processos

```bash id="ic79w0"
pstree
```

### Objetivo

Investigar relação entre processos.

---

# Usuários e Permissões

## Ver usuários logados

```bash id="ydf7ec"
who
```

### Objetivo

Monitorar sessões ativas.

---

## Histórico de logins

```bash id="e4r7is"
last
```

### Objetivo

Investigar acessos.

---

## Ver privilégios sudo

```bash id="frt1t2"
sudo -l
```

### Objetivo

Verificar permissões elevadas.

---

## Ver permissões de arquivos

```bash id="ln0j9g"
stat arquivo.txt
```

### Objetivo

Analisar permissões e timestamps.

---

# Threat Hunting

## Buscar PowerShell em Linux

```bash id="dbr8lp"
ps aux | grep powershell
```

### Objetivo

Detectar PowerShell Core.

---

## Buscar conexões suspeitas

```bash id="5yfqpx"
lsof -i
```

### Objetivo

Identificar comunicação suspeita.

---

## Buscar arquivos SUID

```bash id="1c5p4f"
find / -perm -4000 2>/dev/null
```

### Objetivo

Detectar possíveis vetores de privilege escalation.

---

## Buscar arquivos ocultos

```bash id="u40g7f"
find / -name ".*"
```

### Objetivo

Identificar arquivos escondidos.

---

# Compressão e Hashes

## Gerar hash SHA256

```bash id="7gjp5e"
sha256sum arquivo
```

### Objetivo

Verificar integridade de arquivos.

---

## Compactar arquivos

```bash id="yq5q3w"
tar -czvf backup.tar.gz pasta/
```

### Objetivo

Criar backups e evidências.

---

# Serviços e Persistência

## Ver serviços ativos

```bash id="n0px3u"
systemctl list-units --type=service
```

### Objetivo

Identificar serviços suspeitos.

---

## Ver tarefas agendadas

```bash id="6kq94o"
crontab -l
```

### Objetivo

Detectar persistência.

---

# Comandos Mais Importantes para SOC

## Alta Prioridade

* grep
* find
* journalctl
* tail
* ss
* netstat
* ps
* tcpdump
* lsof
* sha256sum

---

# Diretórios Importantes

| Diretório       | Objetivo             |
| --------------- | -------------------- |
| /var/log        | Logs do sistema      |
| /etc            | Configurações        |
| /tmp            | Arquivos temporários |
| /home           | Usuários             |
| /var/spool/cron | Cron jobs            |
| /root           | Usuário root         |

---

# Indicadores Suspeitos

## Possíveis sinais de comprometimento

* processos desconhecidos
* conexões externas incomuns
* arquivos SUID suspeitos
* tarefas cron desconhecidas
* serviços não reconhecidos
* consumo elevado de CPU

---

# Referências

* Linux Man Pages
* MITRE ATT&CK
* GTFOBins
* Elastic Security
* Wazuh Documentation
