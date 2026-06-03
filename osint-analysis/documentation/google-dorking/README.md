# Google Dorking para OSINT — Principais Operadores e Técnicas

**Importante:** Google Dorking é uma técnica utilizada para refinar pesquisas e localizar informações publicamente indexadas pelos mecanismos de busca. Em OSINT, deve ser utilizada apenas para identificar dados expostos publicamente e apoiar investigações legítimas.

## Operadores fundamentais

| Operador      | Função                                       | Exemplo                                 |
| ------------- | -------------------------------------------- | --------------------------------------- |
| `site:`       | Pesquisa dentro de um domínio específico     | `site:empresa.com.br`                   |
| `filetype:`   | Procura tipos específicos de arquivos        | `filetype:pdf`                          |
| `intitle:`    | Busca palavras no título da página           | `intitle:"relatório"`                   |
| `allintitle:` | Todas as palavras devem estar no título      | `allintitle:investigação relatório`     |
| `inurl:`      | Busca palavras na URL                        | `inurl:admin`                           |
| `allinurl:`   | Todas as palavras devem estar na URL         | `allinurl:login painel`                 |
| `intext:`     | Busca palavras no conteúdo da página         | `intext:"confidencial"`                 |
| `allintext:`  | Todas as palavras devem aparecer no conteúdo | `allintext:empresa fornecedor contrato` |
| `cache:`      | Exibe versão armazenada pelo Google          | `cache:empresa.com.br`                  |
| `related:`    | Sites semelhantes ao domínio pesquisado      | `related:empresa.com.br`                |

## Operadores de Exclusão

| Operador | Função                              | Exemplo                    |
| -------- | ----------------------------------- | -------------------------- |
| `-`      | Exclui um termo da pesquisa         | `amazon -aws`              |
| `""`     | Pesquisa frase exata                | `"joão da silva"`          |
| `OR`     | Pesquisa uma opção ou outra         | `"empresa" OR "companhia"` |
| `AND`    | Combina termos                      | `osint AND investigação`   |
| `*`      | Coringa para palavras desconhecidas | `"João * Silva"`           |

## Busca por Documentos

**PDFs**<br>
site:empresa.com.br filetype:pdf

**Planilhas**<br>
site:empresa.com.br filetype:xls<br>
site:empresa.com.br filetype:xlsx

**Documentos Word**<br>
site:empresa.com.br filetype:doc<br>
site:empresa.com.br filetype:docx

**Apresentações**<br>
site:empresa.com.br filetype:ppt<br>
site:empresa.com.br filetype:pptx

**Arquivos de texto**
site:empresa.com.br filetype:txt

## Busca de Infraestrutura
**Subdomínios**<br>
site:*.empresa.com.br

**Portais internos expostos**
site:empresa.com.br inurl:portal

**Painéis administrativos**
site:empresa.com.br inurl:admin

**Diretórios específicos**
site:empresa.com.br inurl:uploads

## Busca de Pessoas
**Nome completo**<br>
"João da Silva"

**Nome + Empresa**<br>
"João da Silva" "Empresa XYZ"

**Nome + Cargo**<br>
"João da Silva" "Diretor"

**Nome + Cidade**<br>
"João da Silva" "São Paulo"

## Busca de E-mails<br>
**E-mails de um domínio**<br>
"@empresa.com.br"

**E-mails em documentos**<br>
site:empresa.com.br filetype:pdf "@empresa.com.br"

## Busca em Redes Sociais<br>
**LinkedIn**<br>
site:linkedin.com/in "Empresa XYZ"

**GitHub**<br>
site:github.com "Empresa XYZ"

**X (Twitter)**<br>
site:x.com "Empresa XYZ"

**Facebook**<br>
site:facebook.com "Empresa XYZ"

**Instagram**<br>
site:instagram.com "Empresa XYZ"

## Busca por Vazamentos e Exposição de Dados<br>
**Relatórios públicos**<br>
site:empresa.com.br filetype:pdf "relatório"

**Contratos**<br>
site:empresa.com.br filetype:pdf contrato

**Licitações**<br>
site:gov.br licitação

**Editais**<br>
site:gov.br edital

## Busca em Sites Governamentais<br>
**Apenas domínio GOV.BR**<br>
site:gov.br

**Empresas em documentos públicos**<br>
site:gov.br "Empresa XYZ"

**CPF ou CNPJ em documentos**<br>
site:gov.br filetype:pdf "12.345.678/0001-99"

## Combinações Poderosas para OSINT**<br>
**Empresa + PDFs**<br>
"Empresa XYZ" filetype:pdf

**Empresa + Planilhas**<br>
"Empresa XYZ" filetype:xlsx

**Empresa + Contratos**<br>
"Empresa XYZ" contrato

**Empresa + Endereço**<br>
"Empresa XYZ" endereço

**Empresa + Telefone**<br>
"Empresa XYZ" telefone

**Empresa + E-mail**<br>
"Empresa XYZ" "@"

**Empresa + Sócios**<br>
"Empresa XYZ" sócio

## Dicas para Investigações OSINT
- Utilize aspas ("") sempre que pesquisar nomes completos.
- Combine múltiplos operadores para reduzir falsos positivos.
- Pesquise em diferentes idiomas quando houver indícios de atuação internacional.
- Analise documentos PDF, DOCX e XLSX encontrados.
- Verifique versões antigas dos sites utilizando a ferramenta Wayback Machine.
- Correlacione resultados obtidos no Google com outras fontes OSINT.
- Documente todas as consultas realizadas para manter a rastreabilidade da investigação
- Estrutura básica de uma consulta OSINT eficiente
- "ALVO" site:DOMÍNIO filetype:TIPO palavra-chave

**Exemplo:**

"Empresa XYZ" site:empresa.com.br filetype:pdf relatório

Essa combinação permite localizar documentos específicos relacionados ao alvo utilizando apenas informações publicamente indexadas pelos mecanismos de busca.

---
**Autor:** Paulo Cesar<br>
**Linkedin:** linkedin.com/in/paulo-cesar-security

