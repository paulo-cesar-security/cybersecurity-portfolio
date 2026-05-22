# Investigando conexão suspeita na rede (Splunk)

**Cenário:**

Sou um analista SOC Nível 1 em turno e recebi um alerta indicando uma conexão de rede suspeita usando a porta 5678 no host WIN-105. Minha tarefa é conduzir uma investigação e determinar se essa atividade é suspeita.

**1 \- Com qual endereço IP a conexão foi estabelecida?**

Para iniciar usei a consulta: index=task4 EventCode=3 ComputerName=WIN-105 destinationport: 5678

E o resultado foi: IP 10.10.114.80

![](images/image2.png)

**2 \- Qual processo iniciou essa conexão suspeita?**

**Resposta: SharePoInt.exe**

![](images/image3.png)

**3 \- O que é o hash MD5 do processo malicioso da pergunta anterior?**

Como eu já sabia o processo que iniciou a conexão suspeita usei a consulta: index=task4 SharePoInt.exe

Apareceu vários eventos, então cliquei em hashs no menu a esquerda e apareceu essas informações:

![](images/image4.png)

Correlacionando os logs encontro a resposta: [770D14FFA142F09730B415506249E7D1](https://10-64-150-21.reverse-proxy.cell-prod-us-east-1a.vm.tryhackme.com/en-US/app/search/search?q=search%20index%3Dtask4%20SharePoInt.exe&display.page.search.mode=smart&dispatch.sample_ratio=1&workload_pool=&earliest=0&latest=&sid=1779454955.11#)

**4 \- Qual é o nome da tarefa programada que foi criada no sistema?**

Usei essa consulta para investigar tarefas programadas:

index=task4 schtasks.exe

![](images/image5.png)

Descobri que a tarefa programada é essa: Office365 Install

**Conclusão**

Através a análise dos logs no Splunk foi possível identificar um ataque na rede onde o atacante tinha o objetivo de executar malware automaticamente toda vez que o computador inicia-se ou em horários específicos, iria manter acesso persistente, mesmo após reinicialização, queria esconder a atividade maliciosa usando um nome corporativo comum e possivelmente manter comunicação C2.

Autor: Paulo Cesar  
Formado em Segurança da informação  
linkedin.com/in/paulo-cesar-security

![](images/image1.png)


