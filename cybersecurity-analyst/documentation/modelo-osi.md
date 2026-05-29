# O Modelo OSI (Open Systems Interconnection)

É uma estrutura conceitual de **7 camadas** criada pela ISO para padronizar a comunicação entre diferentes sistemas computacionais.

Ele divide o processo de transmissão de dados em etapas hierárquicas e independentes, facilitando o diagnóstico de falhas e a interoperabilidade.

As 7 camadas são organizadas da seguinte forma (do topo para a base):

## Camadas Superiores (Orientadas ao Software)

- **7. Aplicação:** A camada que interage diretamente com o usuário e com os aplicativos (ex: navegadores, clientes de e-mail). **Protocolos: HTTP, FTP, DNS.** 
- **6. Apresentação:** Responsável pela tradução, compactação e criptografia dos dados, garantindo que o receptor consiga lê-los.
- **5. Sessão:** Controla e mantém a conexão ativa entre os dispositivos, gerenciando o início, a manutenção e o encerramento da troca de dados.

## Camada Central

- **4. Transporte:** Assegura que os dados sejam entregues por completo, de forma confiável e na ordem correta. Controla o fluxo de informações. **Protocolos: TCP e UDP.**

## Camadas Inferiores (Orientadas ao Hardware)

- **3. Rede:** Determina a melhor rota para os dados chegarem ao destino (roteamento). **Protocolos: IP.**
- **2. Enlace de Dados:** Agrupa os bits em quadros (frames) e gerencia a detecção de erros e o controle de acesso físico à rede (MAC).
- **1. Física:** Transforma e transmite os dados em sinais brutos (elétricos, luminosos ou ondas de rádio) através do meio físico (cabos, fibra óptica, ar).
