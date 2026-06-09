# Laboratório SOC Analyst N1 — Investigação de PowerShell Suspeito

**Cenário**

Sou analista SOC Nível 1 da empresa fictícia BlueFinance.<br>
Durante meu turno, o SIEM gerou um alerta relacionado à execução suspeita de PowerShell em uma máquina de usuário.

O alerta chamou atenção porque o comando estava:

codificado em Base64<br>
usando parâmetro -EncodedCommand<br>
executado via PowerShell oculto<br>

**Meu objetivo era descobrir:**

se era atividade legítima<br>
o que o comando fazia<br>
se houve comprometimento<br>
quais IOC precisavam ser escalados

O resultado completo do laboratório pode ser acessado na pasta /anexos acima.
