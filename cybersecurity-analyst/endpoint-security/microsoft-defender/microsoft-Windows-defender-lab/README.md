# Microsoft Applied Skills: proteja-se contra ameaças cibernéticas com o Microsoft Defender XDR

**Cenário**

Eu fui contratado(a) recentemente pela Contoso, Ltd. para ajudar a equipe de TI da empresa a se defender contra ameaças usando o Microsoft Defender (XDR).

Os executivos da empresa estão muito preocupados em garantir que todas as diretrizes sejam seguidas e que todos os requisitos sejam atendidos durante a execução das atividades no ambiente.

As diretrizes e requisitos estão detalhados em uma série de e-mails. Eu devo ler essas mensagens e concluir as atividades de acordo com os requisitos fornecidos.

Eu posso executar as atividades no portal do Microsoft Defender ou em qualquer outra ferramenta da Microsoft disponível na máquina virtual.

**Passo 1**

Eu faço login na máquina virtual:

Nome de usuário: Admin
Senha: Pa55w.rd

**Tarefas**

**E-mail 1 — Ambiente existente**

Recebo credenciais para gerenciar recursos no Microsoft 365:

Usuário: admin@WWLx401041.onmicrosoft.com
Senha: pDr81D+26)(0tV]HXy40=S+A3Fi(xv~y

Meu ambiente de laboratório contém duas VMs: Client1 e Client2 (Windows 11).

Eu devo executar as tarefas no cliente correto conforme indicado.

Preparação do Microsoft Defender XDR

**Eu devo:**
![]()

- Fazer login no Client2
- Abrir Edge e acessar https://security.microsoft.com
- Ir em Investigation and response → Incidents and alerts → Incidents
- Aguardar mensagem de provisionamento
- Fechar o Edge após conclusão
- Reabrir o Edge e acessar novamente o portal
- Execução no Client2

**Faço login no Client2**
- Abro Edge
- Acesso Microsoft Defender XDR
- Navego até Incidents
- Aguardo a inicialização do ambiente
- Reinicio o navegador e acesso novamente
- E-mail 3 — Integrar endpoint ao Microsoft Defender XDR

**Agora eu devo:**

**Parte 1 — Criar grupo de dispositivos**

No portal Defender:

- Crio grupo: Group1
- Dispositivos: Windows 10 e Windows 11
- Remediação: automática (Full)
  
**Parte 2 — Onboarding**
  
- Vou em Settings → Endpoints → Onboarding
- Escolho Windows 10 e 11
 
**Método: Local Script**
  
- Escolho conectividade simplificada (*.endpoint.security.microsoft.com)
- Baixo o pacote e salvo em Downloads do Client2
  
**Parte 3 — Executar onboarding**

- Extraio ZIP
- Executo .cmd como administrador
- Aguardo conclusão
- Parte 4 — Verificação
- Verifico Client2 em Assets → Devices

**Parte 5 — Ataque**

- No Client2 executo script PowerShell em C:\Files
  
**E-mail 4 — Política de segurança de endpoint**

No Client1:

Eu crio uma política chamada:

- EndpointPolicy1

**Configuro:**

- Windows 11
- Attack surface reduction rules
- Regra: bloquear JavaScript/VBScript de executar downloads
- Atribuo ao grupo sg-Executive
  
**E-mail 5 — Incidente**

- Investigo incidente no Client2
- Analiso timeline
- Identifico IP malicioso e target

**Exemplo encontrado:**

- IP: 160.20.85.173
- Target: Notepad.exe

**Crio:**

- Indicator1 (bloqueio de IP)
- Regra KQL no Advanced Hunting
- Execução de coleta e marcação de usuário comprometido
- E-mail 6 — Investigação forense

- Abro Live Response no Client2
- Visualizo conexões
- Coleto pacote de investigação
- Extraio CSV
- Isolo o dispositivo
  
**Email final — Conclusão**

Concluo o laboratório de defesa contra ameaças usando Microsoft Defender XDR.
