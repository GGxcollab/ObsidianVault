# Desenvolver soluções de processamento de linguagem natural
### Analisar Texto
- **Serviço de Linguagem de AI do Azure**
	- Recursos pré-configurados:
		- Detecção de idioma
			- ![[Pasted image 20241002170957.png]]
		- Extração de frases-chave
			- ![[Pasted image 20241002171130.png]]
		- Análise de sentimento
			- ![[Pasted image 20241002171143.png]]
		- Reconhecimento de entidade nomeada
			- ![[Pasted image 20241002171200.png]]
		- Vinculação de entidade
			- ![[Pasted image 20241002171225.png]]
		- Resumo 
			- ![[Pasted image 20241002171611.png]]
		- Detecção de PII
			- ![[Pasted image 20241002171855.png]]
	- Os recursos personalizáveis são abordados em outro seção
	- ![[Pasted image 20241002170711.png]]
### Traduzir texto
- **O Serviço Tradutor**
	- API REST de tradução de texto multilíngue
		- *Detecção* de idioma
		- A *tradução* de um para muitos
		- Transliteração de *script*
		- ![[Pasted image 20241002172136.png]]
		- ![[Pasted image 20241002172334.png]]
		- ![[Pasted image 20241002172352.png]]
-   **Tradução Personalizada**
	- Cria um modelo de tradução personalizado
		1. Usar o portal do Tradutor Personalizado
		2. Criar um espaço de trabalho vinculado ao seu recurso Tradutor de IA do Azure
		3. Criar um projeto
		4. Carregar os arquivos de dados de treinamento
		5. Treinar um modelo
	- Chame seu modelo por meio da API do Tradutor
		- Especificar um parâmetro de **categoria** com o ID da categoria do projeto
	- ![[Pasted image 20241003111331.png]]
### Criar uma solução de respostas às perguntas
- **Introdução a Respostas às perguntas**
	- Base de dados de conhecimento de pares de perguntas e respostas com reconhecimento de linguagem natural
	- Publicado como um ponto de extremidade REST para aplicativos a serem consumidos
	- Disponível por meio de SDKs específicos de linguagem
	- ![[Pasted image 20241003112144.png]]
- **Respostas às perguntas versus Reconhecimento de linguagem**
	- Respostas às perguntas
		- O usuário envia uma pergunta, esperando uma resposta
		- O serviço usa o reconhecimento de linguagem natural para fazer a correspondência de a uma pergunta com uma resposta na base de dados de conhecimento
		- A resposta é uma resposta estática a uma pergunta conhecida
		- O aplicativo cliente apresenta a resposta para o usuário
	- Reconhecimento Vocal
		- O usuário envia um enunciado, esperando uma resposta ou uma ação apropriada
		- O serviço usa o reconhecimento de linguagem natural para interpretar o enunciado, correspondê-lo a uma intenção e identificar as entidades
		- A resposta indica a intenção mais provável e entidades referenciadas
		- O aplicativo cliente é responsável por executar a ação apropriada com base na intenção detectada
- **Criação de uma base de dados de conhecimento**
	- Usar o portal do Language Studio
		1. Crie um recurso de **Linguagem de IA do Azure** em sua assinatura do Azure
		2. No Estúdio de Linguagem, selecione seu recurso de Linguagem de IA do Azure e crie um projeto de **Resposta às perguntas personalizado.**
		3. Preencha a base de dados de conhecimento:
			- Importar da página da Web de perguntas frequentes existente
			- Carregar arquivos de documento
			- Adicionar pares "bate-papo" predefinidos
		4. Criar a base de dados de conhecimento e editar pares de perguntas e respostas
- **Conversa com várias rodadas**
	- Adicionar prompts de acompanhamento para definir trocas de várias rodadas
		- Pode fazer referência a pares de perguntas e respostas existentes
		- Pode ser restrito apenas a repostas de acompanhamento
		- ![[Pasted image 20241003143628.png]]
- **Testar e publicar uma base de dados de conhecimento**
	- Testar interativamente a Language Studio
		- Inspecionar os resultados para ver as pontuações de confiança
		- Adicione frases alternativas para melhorar as pontuações confirme necessário
	- Publicar a base de dados de conhecimento treinada
		- Criar um ponto de extremidade baseado em HTTP REST para aplicativos cliente consumirem
		- A base de dados de conhecimento publicada pode ser usada com SDKs em seu aplicativo
		- 
