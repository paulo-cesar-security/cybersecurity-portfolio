## Investigação utilizando o Shodan
Cenário

A equipe de TI informou ao SOC que um servidor da empresa pode estar exposto diretamente na internet sem necessidade.

Sua tarefa como analista SOC é validar a exposição utilizando apenas o Shodan.

# Objetivo da Investigação

# Descobrir:

- Se o servidor está acessível pela internet
- Qual serviço está exposto
- Qual porta está aberta
- Qual o possível risco da exposição
- Informações Recebidas
- Campo	Valor
- IP suspeito	189.10.10.25
- Nome do ativo	SRV-REMOTE
- Solicitação	Validar exposição externa
- Investigação no Shodan

# Acessei o Shodan e pesquisei:

189.10.10.25

# Resultado Encontrado

O Shodan retorna:

Porta aberta	3389
Serviço	Microsoft RDP
Status	Online
Sistema operacional	Windows

# Com base nas informações encontradas no Shodan, foi possível identificar que:

- O servidor está acessível publicamente
- O serviço RDP está exposto na internet
- A porta 3389 encontra-se aberta
- O ativo pode estar sujeito a tentativas de brute force
- Evidência Coletada
- IP: 189.10.10.25
- Porta: 3389
- Serviço: Microsoft RDP
- Origem da evidência: Shodan
  
# Conclusão

A investigação utilizando o Shodan permitiu identificar rapidamente um serviço remoto exposto publicamente na internet.

Essa visibilidade me ajudou a:

- Detectar exposições indevidas
- Identificar superfícies de ataque
- Priorizar correções
- Alertar equipes responsáveis
- Demonstração de Competências SOC
