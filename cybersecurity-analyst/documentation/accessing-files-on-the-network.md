# Acessando arquivos na rede pelo Windows e pelo Linux
Como geralmente funciona numa empresa:

- “o arquivo está na pasta da equipe”
- “está no servidor financeiro”
- “está no compartilhamento do RH”
- “está no drive Z:”

**Ou seja, a empresa normalmente usa:**

Servidores centrais, pastas compartilhadas organizadas, permissões por setor.

**O cenário mais comum**

Existe um servidor chamado: **SRV-ARQUIVOS**

Ele guarda:

Documentos, planilhas, backups , arquivos da equipe.

# Exemplo realista
A Ana fala:

“Deixei o relatório na pasta Financeiro.”

O Carlos já sabe que a pasta fica em:

\\SRV-ARQUIVOS\Financeiro

Então ele:

Abre o Explorer, acessa o caminho, abre o arquivo.

# Acessando pelo Linux
o acesso desse mesmo exemplo seria: smb://SRV-ARQUIVOS/Financeiro
Pelo terminal seria: smbclient //SRV-ARQUIVOS/Financeiro -U carlos

