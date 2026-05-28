# É fundamental conhecer as portas, serviços e protocolos para entender rapidamente o que está acontecendo na hora de um alerta de incidente.

# Administração remota

| Porta | Serviço    | Protocolo | Importância                        |
| ----- | ---------- | --------- | ---------------------------------- |
| 20/21 | FTP        | TCP       | Transferência de arquivos insegura |
| 22    | SSH        | TCP       | Administração Linux                |
| 23    | Telnet     | TCP       | Inseguro, legado                   |
| 69    | TFTP       | UDP       | Transferência simples/insegura     |
| 3389  | RDP        | TCP       | Acesso remoto Windows              |
| 5900  | VNC        | TCP       | Desktop remoto                     |
| 5938  | TeamViewer | TCP       | Suporte remoto                     |
| 22    | SCP/SFTP   | TCP       | Transferência segura               |

# Web e aplicações

| Porta | Serviço                 |
| ----- | ----------------------- |
| 80    | HTTP                    |
| 443   | HTTPS                   |
| 8080  | HTTP Alternate / Proxy  |
| 8443  | HTTPS Alternate         |
| 8000  | Aplicações web          |
| 8888  | Jupyter / serviços web  |
| 81    | Painéis administrativos |
| 3000  | Node.js / React         |
| 5000  | Flask                   |
| 5601  | Kibana                  |
| 9200  | Elasticsearch           |
| 9443  | Painéis seguros         |

# DNS e infraestrutura

| Porta   | Serviço            |
| ------- | ------------------ |
| 53      | DNS                |
| 67/68   | DHCP               |
| 123     | NTP                |
| 161/162 | SNMP               |
| 389     | LDAP               |
| 636     | LDAPS              |
| 88      | Kerberos           |
| 464     | Kerberos Password  |
| 3268    | Global Catalog     |
| 3269    | Global Catalog SSL |

# Windows / Active Directory

| Porta | Serviço          |
| ----- | ---------------- |
| 135   | RPC              |
| 137   | NetBIOS Name     |
| 138   | NetBIOS Datagram |
| 139   | NetBIOS Session  |
| 445   | SMB              |
| 5985  | WinRM HTTP       |
| 5986  | WinRM HTTPS      |
| 9389  | AD Web Services  |

# E-mail

| Porta | Serviço         |
| ----- | --------------- |
| 25    | SMTP            |
| 465   | SMTPS           |
| 587   | SMTP Submission |
| 110   | POP3            |
| 995   | POP3S           |
| 143   | IMAP            |
| 993   | IMAPS           |

# Banco de dados

| Porta | Serviço              |
| ----- | -------------------- |
| 1433  | Microsoft SQL Server |
| 1521  | Oracle DB            |
| 3306  | MySQL                |
| 5432  | PostgreSQL           |
| 6379  | Redis                |
| 27017 | MongoDB              |
| 9042  | Cassandra            |

# VPN e tunelamento

| Porta | Serviço     |
| ----- | ----------- |
| 500   | IPSec       |
| 4500  | IPSec NAT-T |
| 1194  | OpenVPN     |
| 1701  | L2TP        |
| 1723  | PPTP        |
| 51820 | WireGuard   |

# Containers, cloud e DevOps

| Porta | Serviço             |
| ----- | ------------------- |
| 2375  | Docker API insegura |
| 2376  | Docker TLS          |
| 6443  | Kubernetes API      |
| 10250 | Kubelet             |
| 9090  | Prometheus          |
| 9100  | Node Exporter       |
| 9092  | Kafka               |

# SIEM, monitoramento e segurança

| Porta | Serviço            |
| ----- | ------------------ |
| 1514  | Wazuh Agent        |
| 1515  | Wazuh Registration |
| 514   | Syslog             |
| 2055  | NetFlow            |
| 4739  | IPFIX              |
| 9000  | SonarQube / apps   |
| 5140  | Syslog alternativo |

# Serviços frequentemente explorados

| Porta | Serviço       | Observação         |
| ----- | ------------- | ------------------ |
| 445   | SMB           | Ransomware         |
| 3389  | RDP           | Brute force        |
| 22    | SSH           | Credential attacks |
| 21    | FTP           | Credenciais fracas |
| 23    | Telnet        | Inseguro           |
| 5900  | VNC           | Exposição remota   |
| 9200  | Elasticsearch | Exposição pública  |
| 2375  | Docker API    | Execução remota    |
| 3306  | MySQL         | Banco exposto      |
| 5432  | PostgreSQL    | Banco exposto      |

# Portas MUITO importantes para SOC Analyst

Top prioridade:

- 22
- 53
- 80
- 88
- 123
- 135
- 139
- 389
- 443
- 445
- 514
- 636
- 3389
- 5985
- 5986
- 9200
- 5601

**Exemplo prático**

**Porta 445 - SMB**

**Uso**
Compartilhamento de arquivos Windows.

**Riscos**
- EternalBlue
- lateral movement
- ransomware
- pass-the-hash

**Monitoramento**
- conexões SMB incomuns
- múltiplas autenticações
- acesso administrativo remoto

**Ferramentas relacionadas**
- PsExec
- smbclient
- CrackMapExec
