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
	- Base de dados de conheci
