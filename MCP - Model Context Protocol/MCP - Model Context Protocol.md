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
- São ferramentas que realizam ações. Elas são controladas pelo modelo, ou seja, a **própria LLM decide quando chamar**.
- **Autodiscovery**: LLM possui formas de entender quais tools estão disponíveis.
### Resources
- Permitem que os servidores disponibilizem dados que podem ser lidos pelos clients e usado como contexto pelo LLM.
- Resources são controlados pelo client (Application-controlled), ou seja, **o client decide quando usar e não o modelo**.
- Diferentes tipos de dados: Arquivos, Banco de dados, respostas de API, imagens, arquivos de log
- Prove a fonte de dados e quem utiliza a chamada dessa fonte de dados é o client não necessariamente o modelo que vai decidir
- Cada resource possui seu próprio URI
- Exemplos:
	- screen: //host/image1
	- file: //caminho/file/pdf
	- postges: /database/customers/schema
### Prompts
- Permitem que o server defina templates de prompt para que os clients possam usar.
- Prompts são "**User-Controlled**", ou seja, os prompts ficam disponíveis, mas o usuário precisa "selecionar".
- Podem ser templates estáticos, dinâmicos passando parâmetros, inclusive pegando contexto de um resource.
- Dependendo da ferramenta, pode ser utilizado com o "/"
# Formato de comunicação
### Stdio
- O client MCP executa o servidor MCP como um subprocesso
- O servidor recebe mensagens JSON-RPC em usa entrada padrão (stdin) e escreve para sua saída padrão (stdout)
- Comunicação local, onde o cliente e o servidor estão na mesma máquina.
- Simples e o mais comum de se ver no dia a dia
### SSE (Server Sent Events)
- O client abre uma conexão SSE com o servidor, e o servidor envia mensagens como eventos SSE usando HTTP.
- Forma utilizada para acessar um Servidor MCP de forma remota (ex.: Copilot Studio)
- Bem mais complexo de se desenvolver pelo fato de haver diversos fatores envolvidos, como segurança, controle de acesso, re