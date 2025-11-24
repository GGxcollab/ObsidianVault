- O **projeto DevSecOps** tem como objetivo desenvolver uma plataforma web que facilite a aplicação automatizada de templates de CI/CD oriundos do projeto PASSC do Azure DevOps em projetos da organização

- Criação e refinamento do chatbot (R3vense)

- Integração do fluxo do Sentinel e ServiceNow, afim de fechar os incidentes criando as classificações dos mesmos baseados nos comentários de resolução escrito pelo analista e no tipo de incidente

- Automação JusBR - 
	- **Objetivo Principal:** Automatizar a captura e entrega de petições iniciais de processos judiciais através de integração com o portal JusBr.

	**Como funciona:**
	
	1. Sistema recebe requisição API com número CNJ do processo
	2. Solução acessa automaticamente o portal JusBr
	3. Localiza e captura o documento "Petição Inicial"
	4. Retorna o documento via API para o solicitante
	
	**Em outras palavras:** É uma ponte automatizada entre sistemas externos e o JusBr - você envia o número do processo, a solução busca a petição inicial no portal e devolve o documento, tudo via API.