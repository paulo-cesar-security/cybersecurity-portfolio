# Laboratório SOC Analyst N1 — Investigação de Exfiltração de Dados via DNS

**Cenário**

Sou analista SOC Nível 1 da empresa fictícia HealthCore.
Durante meu turno, o SIEM gerou um alerta relacionado a tráfego DNS anômalo originado de uma estação do setor financeiro.

**O alerta chamou atenção porque:** <br>
houve milhares de consultas DNS em poucos minutos<br>
os domínios eram extremamente longos<br>
o padrão parecia automatizado<br>
o host nunca havia apresentado esse comportamento

**Meu objetivo era:** <br>
validar o alerta<br>
identificar possível exfiltração de dados<br>
investigar o host comprometido<br>
coletar IOC<br>
escalar corretamente o incidente

O resultado completo do laboratório pode ser acessado na pasta /anexos acima.
