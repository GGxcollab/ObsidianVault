# Introdução
- Protocolo que padroniza como sistemas podem prover contexto para as LLMs.
- Padroniza como as LLMs podem se conectar em diferentes data sources e ferramentas.
		![[Pasted image 20250604151911.png]]
##### Exemplo de chamada:
- Quais são os containers docker que estão sendo executados?
- Verifique no postgres registros que tenho na tabela de logs
- Qual produto que possui com o id 1 de acordo com minha "Tool"
 **Em determinadas situações você precisará ser mais expressivo ao solicitar**:

# Componentes
![[Pasted image 20250604152810.png]]

- Exemplos de Aplicações que implementam MCP Clients:
	- GitHub Copilot
	- Cursor
	- Claude Desktop
	- Claude Code
- Exemplos de MCP Servers
	- Postgres
	- Google Drive
	- Github
	- Slack
	- Filesystem
	- Docker
	- Kubernetes
# Arquitetura de um MCP Server
### Tools
- São ferramentas que realizam ações. Elas são controladas pelo modelo, ou seja, a ==própria LLM decide quando chamar==.
- **Autodiscovery**: LLM possui formas de entender quais tools estão disponíveis.
### Resources
- Permitem que os servidores disponibilizem dados que podem ser lidos pelos clients e usado como contexto pelo LLM.
- Resources são controlados pelo client