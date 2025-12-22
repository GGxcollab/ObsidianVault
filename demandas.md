- O **Plataforma DevSecOps** - minha ultima demanda foi a aplicação do fluxo deploy do arquivo azure-pipeline no repositorio do usuário a partir da escolha do usuário pela plataforma web

- **R3vense** - Criação e refinamento do chatbot R3vense que é um chatbot inteligente projetado para auxiliar e executar ações relacionadas à nossa área de Cyber. O sistema tambem utiliza inteligência artificial (Azure OpenAI) com orquestração automática de ferramentas via MCP (Model Context Protocol que é Um protocolo que padroniza a comunicação entre modelos de IA e serviços externos (ferramentas, bancos de dados, etc.).) para fornecer respostas contextuais e executar ações em sistemas de segurança.
	- Entregue o MVP do projeto 

- **Integração do fluxo do Sentinel e ServiceNow,** afim de fechar os incidentes criando as classificações dos mesmos baseados nos comentários de resolução escrito pelo analista e no tipo de incidente

- **Automação JusBR** - (ATUALMENTE PARADA POR NÃO TER UMA SOLUÇÃO PARA O CAPTCHA)
	- **Objetivo Principal:** Automatizar a captura e entrega de petições iniciais de processos judiciais através de integração com o portal JusBr.

	**Como funciona:**
	
	1. Sistema recebe requisição API com número CNJ do processo
	2. Solução acessa automaticamente o portal JusBr
	3. Localiza e captura o documento "Petição Inicial"
	4. Retorna o documento via API para o solicitante
	
	**Em outras palavras:** É uma ponte automatizada entre sistemas externos e o JusBr - você envia o número do processo, a solução busca a petição inicial no portal e devolve o documento, tudo via API.

### a fazer

- Acrescentar mais funcionalidades ao Revense, viabilizando a possibilidade de integração por área que temos dentro da cyber, para ajudar a centralizar so conhecimentos dentro do chatbot e ajudar os times a tomarem decisoes e fazerem suas demandas 
- Correção da Classificação dos Owners no Sentinel a apartir do momento em que o incidente for tratado e solucionado pelo N2, tudo isso no nosso ambiente da BBTS
- **Plataforma Teamie** - Projeto desenvolvido pela necessidade de outras gerências, em terem os próprios bots com base no Cybernotify.