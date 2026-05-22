# Investigando conexão suspeita na rede (Splunk)

## Cenário:

Sou um analista SOC Nível 1 em turno e recebi um alerta indicando uma conexão de rede suspeita usando a porta 5678 no host WIN-105. Minha tarefa é conduzir uma investigação e determinar se essa atividade é suspeita.

**1 - Com qual endereço IP a conexão foi estabelecida?**
Para iniciar usei a consulta: **index=task4 EventCode=3 ComputerName=WIN-105 destinationport: 5678**
E o resultado foi: IP 10.10.114.80

**2 - Qual processo iniciou essa conexão suspeita?**
Resposta: SharePoInt.exe

**3 - O que é o hash MD5 do processo malicioso da pergunta anterior?**
Como eu já sabia o processo que iniciou a conexão suspeita usei a consulta: **index=task4 SharePoInt.exe**
Apareceu vários eventos, então cliquei em hashs no menu a esquerda e apareceu essas informações:

Correlacionando os logs encontro a resposta: 770D14FFA142F09730B415506249E7D1

**4 - Qual é o nome da tarefa programada que foi criada no sistema?**
Usei essa consulta para investigar tarefas programadas:
**index=task4 schtasks.exe**

Descobri que a tarefa programada é essa: Office365 Install

**Conclusão**
Através a análise dos logs no Splunk foi possível identificar um ataque na rede onde o atacante tinha o objetivo de executar malware automaticamente toda vez que o computador inicia-se ou em horários específicos, iria manter acesso persistente, mesmo após reinicialização, queria esconder a atividade maliciosa usando um nome corporativo comum e possivelmente manter comunicação C2.

Autor: Paulo Cesar
Formado em Segurança da informação
linkedin.com/in/paulo-cesar-security

