# Desenvolver soluções de processamento de linguagem natural
### Analisar Texto (Language Studio)
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
- **Criação de aplicativos cliente**
	- ![[Pasted image 20241003145852.png]]
- **Aprimorar o desempenho de respostas às perguntas**
	- Habilitar o *Aprendizado Ativo* para sugerir alternativas quanto várias perguntas tiverem pontuação semelhantes para a entrada de usuários
		- **Implícito**: o serviço identifica possíveis frases alternativas para perguntas e apresenta sugestões no Language Studio. Revisar periodicamente e aceitar/rejeitar as sugestões.
		- **Explícito:** o serviço retorna várias correspondências de perguntas possíveis para o usuário e o usuário identifica a correta. Em seguida, o aplicativo cliente usa a API para enviar itens de feedback, identificando a resposta correta.
	- Criar sinônimos para termos com o mesmo significado
		- Adicione sinônimos à base de dados de conhecimento por meio da interface da API ou do Language Studio.
		- ![[Pasted image 20241003150643.png]]
### Criar um aplicativo de compreensão da linguagem coloquial 
- (Language Studio) -> identificar texto
- **Introdução ao conhecimento de linguagem**
	1. Um aplicativo aceita a entrada de linguagem natural de um usuário
	2. Um modelo de linguagem é usado para determinar o significado semântico (intenção do usuário)
	3. O aplicativo realiza uma ação apropriada
	 ![[Pasted image 20241003151919.png]]
	- **O NPL (Processamento de Linguagem Natural) requer um modelo de linguagem para interpretar a entrada do usuário**
		- Muitas vezes, essa atividade é chamada de NLU (reconhecimento de linguagem natural)
		- A CLU (Compreensão da Linguagem Coloquial) é um serviço do Azure para permitir que você crie um componente de compreensão de linguagem natural a ser usado em um aplicativo de conversação de ponta a ponta.
- **Intenções e enunciados**
	- Para treinar um modelo de reconhecimento de linguagem:
		- Especificar  *enunciados* que representam a entrada de linguagem natural esperada
		- Mapear enunciados para *intenções* que atribuem significados semântico
		- ![[Pasted image 20241003165338.png]]
- **Entities**
	- Defina entidades para adicionar contexto específico a intenções
		- ![[Pasted image 20241003165528.png]]
	- Tipos de entidade:
		- ![[Pasted image 20241003165551.png]]
- **Componentes de entidade predefinida**
	- Os componentes predefinidos preveem automaticamente tipos comuns de enunciados:
		- ![[Pasted image 20241003170340.png]]
- **Funcionalidades do serviço de Linguagem de IA do Azure**
	- Os recursos se enquadram em duas categorias:
		- **Recursos pré-configurados** - podem ser usados sem rotulagem ou treinamento:
			- Resumo
			- Reconhecimento de entidade nomeada
			- Detecção de PII
			- Detecção de frases principais
			- Análise de sentimento
			- Detecção de idioma
		- **Recursos aprendidos** - Exigem rotulagem, treinamento e implantação para utilização
			- Compreensão do idioma da conversa
			- Reconhecimento de Entidade Nomeada personalizado
			- Classificação personalizada de textos
			- Respostas às perguntas
- **Processar precisões**
	- Envie uma solicitação para um slot publicado, especificando:
		- **Variante** - indica qual recurso de linguagem está sendo solicitado. Por exemplo, a **variante** é definida como Conversa para a compreensão da linguagem coloquial ou *EntityRecognition* para detectar entidades.
		- **Parâmetros** - indica os valores para vários parâmetros de entrada. Esses parâmetros variam, dependendo do recurso.
		- **Entrada de análise** - especifica os documentos de entrada ou cadeias de caracteres de texto a serem analisados pelo serviço de Linguagem de IA do Azure.
		- ![[Pasted image 20241003171544.png]]
- **Treinamento, Teste, Publicação e Revisão**
	1. Treine um modelo para conhecer intenções e entidades a partir de exemplos de enunciado
	2. Testar o modelo interativamente ou usando um conjunto de dados de teste com rótulos conhecidos
	3. Implantar um modelo treinado em um ponto de extremidade público para que os aplicativos cliente possam usá-lo
	4. Revisar previsões e iterar em enunciados para treinar seu modelo
	 ![[Pasted image 20241003171935.png]]
### Classificação personalizada e extração de entidade nomeada
- **Classificação personalizada de textos**
	- Atribuir etiquetas personalizadas a documentos
		1. Conectar-se a documentos no Azure
		2. Definir rótulos de classes para atribuir aos seus documentos
		3. Documentos de rótulos 
		4. Treinar  seu modelo
	- Chame seu modelo por meio da API de linguagem
		- Especificar o nome do projeto e da implantação
	- Podem ser projetos de rótulos únicos ou de vários rótulos
		- ![[Pasted image 20241017152910.png]]
- **Reconhecimento de Entidade Nomeada personalizado**
	- Atribuir etiquetas personalizadas a entidades no seus documentos
		1. Conectar-se a documentos no Azure
		2. Definir rótulos de classes para atribuir aos seus documentos
		3. Rotular documentos de forma completa e consistente
		4. Treinar seu modelo
	- Chame seu modelo por meio de API de linguagem
		- Especificar o nome do projeto e da implantação
		- ![[Pasted image 20241017153308.png]]
- **Revisar e melhorar um modelo**
	1. Treinar um modelo para ensinar rótulos ou entidades
	2. Revisar o desempenho do modelo para determinar como melhorar o desempenho, incluindo a matriz de confusão
	3. Determinar quais casos precisam ser adicionados aos seus dados de treinamento
	4. Retreine o seu modelo com novos dados incluídos e repita conforme necessário
		![[Pasted image 20241017153909.png]]
### Reconhecimento de fala, tradução e síntese (Speech Studio)
- **O serviço de fala**
	- APIs de Fala
		- API de reconhecimento de fala (reconhecimento de fala)
			- ![[Pasted image 20241021120528.png]]
		- API de conversão de texto em fala (síntese de fala)
			- ![[Pasted image 20241021140122.png]]
		- API de tradução de fala
		- API de Reconhecimento de Locutor
		- Reconhecimento de intenção (usa compreensão de linguagem coloquial)
			- ![[Pasted image 20241017155419.png]]
	- Formato de Áudio e Vozes
		- Áudio
			- Selecione um formato de áudio para especificar:
				- Tipo de arquivo de áudio
				- Taxa de amostragem
				- Profundidade de bits
		- Vozes
			- Vozes padrão: vozes sintéticas criadas com base em amostras de áudio
			- Vozes neurais: vozes de som mais natural criadas usando redes neurais profundas
		- ![[Pasted image 20241021141801.png]]
	- Linguagem de marcação de síntese de fala (SSML)
		- ![[Pasted image 20241021141944.png]]
	- Síntese de traduções como fala
		- **Síntese baseada em evento**
			- Compatível apenas com tradução 1:1 (idioma destino único)
			- Especifique a voz desejada no **TranslationConfig**
			- Use o evento **Sintetização** para recuperar o fluxo de áudio
			- Criar um manipulador de eventos
			- Use Result.GetAudio() para recuperar o fluxo de bytes
		- **Síntese manual**
			- Uso para vários idiomas de destino
			- Traduzir para texto e usar a API de Conversão de Texto em Fala para sintetizar cada tradução nos resultados
-----------------------------

# Desenvolver soluções de IA generativa com Serviço OpenAI do Azure
### Introdução ao Serviço OpenAI do Azure
- **O que é uma IA generativa?**
	- ![[Pasted image 20241021143947.png]]
- **Provisionar um recurso do OpenAI do Azure no Azure**
	- Implantar um modelo no estúdio do OpenAI do Azure para úsa-lo
		1. Solicite acesso ao serviço OpenAI do Azure
		2. Crie um recurso do **OpenAI do Azure** no portal do Azure
	- Como alternativa, use a CLI do Azure
		- ![[Pasted image 20241021144407.png]]
	- ![[Pasted image 20241021144419.png]]
- **Estúdio do OpenAI do Azure**
	- Portal da Web para trabalhar com modelos do OpenAI do Azure: "https:// oai.azure.com/"
	- Exibir e implantar modelos base
	- Conectar suas próprias fontes de dados
	- Gerenciar arquivos de dados e ajuste para modelos personalizados
	- Testar modelos em playgrounds visuais:
		- **Chat** (GPT-3.5-Turbo e modelos anteriores)
		- **Preenchimentos** (GPT-3 e modelos anteriores)
		- **DALL-E** (gerações de imagens)
		- **Assistentes** (experiências personalizadas e semelhantes ao Copilot)
	- ![[Pasted image 20241021145019.png]]
- **Tipos de modelos de IA generativa**
	- ![[Pasted image 20241021150325.png]]
	- ![[Pasted image 20241021150336.png]]
- **Como testar modelos no playground do Estúdio do OpenAI**
	- ![[Pasted image 20241021163832.png]]
### Desenvolver aplicativos com o Serviço OpenAI do Azure
- **Como integrar o OpenAI do Azure ao seu aplicativo**
	- Os aplicativos enviam os prompts aos modelos implantados. As respostas são conclusões.
	- Três pontos de extremidade de API REST:
		- **Preenchimento** - o modelo usa um prompt de entrada e gera um ou mais preenchimentos previstos.
		- **Inserções** - o modelo usa a entrada e retorna uma representação de vetor dessa entrada.
		- **ChatCompletion** - o modelo recebe entrada na forma de uma conversa de chat (em que as funções são específicas com a mensagem enviada) e a próximo conclusão é gerada.
	- **ChatCompletion** será o ponto de extremidade em que nos concentramos para este curso
	- Use a **Conclusão** e **Inserções** com modelos baseados em GPT-3
	- Use o **ChatCompletion** com o GPT-35-Turbo e modelos posteriores
- **Usando API REST do OpenAI do Azure**
	- ![[Pasted image 20241021170448.png]]
	- ![[Pasted image 20241021170551.png]]
	- ![[Pasted image 20241021170913.png]]
- **Como usar os SDKs do OpenAI do Azure**
	- ![[Pasted image 20241021171108.png]]
### Aplicar engenharia de prompts com o Serviço de OpenAI do Azure
- **Construção de prompts para:**
	- Maximizara relevância e a precisão dos preenchimentos
	- Especificar a formatação e o estilo dos preenchimentos
	- Fornecer contexto de conversa
	- Reduzir o viés e aumentar a imparcialidade
### Implementar RAG (Geração Aumentada de Recuperação) com o Serviço OpenAI do Azure
- **Como o OpenAI do Azure pode usar seus dados**
	- Configurar as fontes de dados
		- Usar uma fonte de dados existente, como um recurso de pesquisa do Azure
		- Use o estúdio do OpenAI do Azure para criar essa fonte de dados, se voce ainda não tiver uma
		- Ao criar uma fonte de dados, é possível usar dados que já estão em sua conta, como armazenamento de blobs
	- Configurar o estúdio ou seu aplicativo para se conectar a essa fonte de dados
	- Use o Modelo do OpenAI do Azure, que agora usa seus dados para fundamentação 

