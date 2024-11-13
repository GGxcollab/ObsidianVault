# Introdução
- _Processamento da linguagem natural_ (NLP) é um problema comum de IA no qual o software deve ser capaz de trabalhar com texto ou fala na forma de linguagem natural que um usuário humano escreveria ou falaria. Dentro do NLP, existe a _Compreensão da linguagem natural_ (NLU), que lida com o problema de determinar o significado semântico da linguagem natural, geralmente usando um modelo de linguagem treinado.

- Um padrão de design comum para uma solução de reconhecimento de linguagem natural é semelhante ao seguinte:

![Diagram showing an app accepts natural language input, and uses a model to determine semantic meaning before taking the appropriate action.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/build-language-understanding-model/media/language-understanding-app.png)

- Neste padrão de design:
	1. Um aplicativo aceita a entrada de linguagem natural de um usuário.
	2. Um modelo de linguagem é usado para determinar o significado semântico (_intenção_ do usuário).
	3. O aplicativo realiza uma ação apropriada.

- A **Linguagem de IA do Azure** permite que os desenvolvedores criem aplicativos com base em modelos de linguagem que podem ser treinados com um número relativamente pequeno de amostras para distinguir o significado pretendido de um usuário.

- Neste módulo, você aprenderá a usar o serviço para criar um aplicativo de reconhecimento de linguagem natural usando a Linguagem de IA do Azure.

- Depois de concluir este módulo, você poderá:
	- Provisionar um recurso de Linguagem de IA do Azure.
	- Definir intenções, entidades e enunciados.
	- Usar padrões para diferenciar enunciados semelhantes.
	- Usar componentes de entidade predefinidos.
	- Treinar, testar, publicar e revisar um modelo.
# Entender os recursos predefinidos do serviços de Linguagem de IA do Azure
- O serviço de Linguagem de IA do Azure fornece vários recursos para entender a linguagem humana. Você pode usar cada recurso para se comunicar melhor com os usuários, entender melhor a comunicação recebida ou usá-los juntos para fornecer mais insights sobre o que o usuário está dizendo, pretendendo e perguntando.
- Os recursos do Serviço de Linguagem de IA do Azure se enquadram em duas categorias: recursos pré-configurados e recursos aprendidos. Os recursos aprendidos exigem a criação e o treinamento de um modelo para prever corretamente os rótulos apropriados, o que é abordado nas próximas unidades deste módulo.
- Esta unidade aborda a maioria dos recursos do serviço de Linguagem de IA do Azure, mas você pode consultar a [documentação do serviço de Linguagem de IA do Azure](https://learn.microsoft.com/pt-br/azure/cognitive-services/language-service/overview) para obter uma lista completa, incluindo inícios rápidos e uma explicação completa de tudo o que está disponível.
- O uso desses recursos em seu aplicativo requer o envio da consulta para o ponto de extremidade apropriado. O ponto de extremidade usado para consultar um recurso específico varia, mas todos eles são prefixados com o recurso de Linguagem de IA do Azure criado em sua conta do Azure, ao criar a sua solicitação REST ou ao definir o seu cliente utilizando um SDK. Exemplos dessas ferramentas podem ser encontrados na próxima unidade.

## Recursos pré-configurados
- O serviço de Linguagem de IA do Azure fornece determinados recursos sem qualquer rotulagem ou treinamento de modelo. Depois de criar seu recurso, você pode enviar seus dados e usar os resultados retornados em seu aplicativo.

Todos os recursos a seguir estão pré-configurados.

### Resumo
- O resumo está disponível para documentos e conversas e resumirá o texto em frases-chave previstas para encapsular o significado da entrada.

### Reconhecimento de entidade nomeada
- O reconhecimento de entidade nomeada pode extrair e identificar entidades, como pessoas, locais ou empresas, permitindo que seu aplicativo reconheça diferentes tipos de entidades para respostas de linguagem natural aprimoradas. Por exemplo, no texto "O píer à beira-mar é minha atração favorita de Seattle", _Seattle_ seria identificada e categorizada como um local.

### Detecção de PIIs (informações de identificação pessoal)
- A detecção de PII permite identificar, categorizar e redigir informações que podem ser consideradas confidenciais, como endereços de email, endereços residenciais, endereços IP, nomes e informações de integridade protegidas. Por exemplo, se o texto "email@contoso.com" foi incluído na consulta, todo o endereço de email poderá ser identificado e redigido.

### Extração de frases-chave
- A extração de frase-chave é um recurso que extrai rapidamente os principais conceitos do texto fornecido. Por exemplo, no texto "Análise de Texto é um dos recursos nos Serviços de IA do Azure.", o serviço extrairia _"Serviços de IA do Azure"_ e _"Análise de Texto"_.

### Análise de sentimento
- A análise de sentimento identifica o quão positiva ou negativa é uma cadeia de caracteres ou um documento. Por exemplo, no texto "Ótimo hotel. Perto de muitos restaurantes e atrações para ir a pé", o serviço identificaria isso como _positivo_ com uma pontuação de confiança relativamente alta.

### Detecção de idioma
- A detecção de idioma usa um ou mais documentos e identifica o idioma para cada um deles. Por exemplo, se o texto de um dos documentos fosse "Bonjour", o serviço o identificaria como _francês_.

## Recursos aprendidos
- Os recursos aprendidos exigem que você rotule dados, treine e implante seu modelo para disponibilizá-los para uso em seu aplicativo. Esses recursos permitem personalizar quais informações são previstas ou extraídas.

>[!NOTE] Observação
>A qualidade dos dados afeta muito a precisão do modelo. Seja objetivo sobre quais dados são usados, quão bem eles são marcados ou rotulados e quão variados são os dados de treinamento. Para obter detalhes, consulte as [recomendações para rotular dados](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/conversational-language-understanding/how-to/tag-utterances), que inclui diretrizes importantes para marcação de dados. Veja também as [métricas de avaliação](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/custom-text-classification/concepts/evaluation-metrics) que podem ajudar a identificar onde seu modelo precisa de melhorias.

### Compreensão da linguagem coloquial (CLU)
- A CLU é um dos principais recursos personalizados oferecidos pela Linguagem de IA do Azure. A CLU ajuda os usuários a compilar modelos de reconhecimento de linguagem natural personalizados para prever a intenção geral e extrair informações importantes de enunciados de entrada. A CLU exige que os dados sejam marcados pelo usuário para ensiná-los a prever intenções e entidades com precisão.
- O exercício neste módulo será criar um modelo de CLU e usá-lo em seu aplicativo.

### Reconhecimento de Entidade Nomeada personalizado
- O reconhecimento de entidade personalizada usa dados rotulados personalizados e extrai entidades especificadas de texto não estruturado. Por exemplo, se tiver vários documentos de contrato dos quais deseja extrair as partes envolvidas, você poderá treinar um modelo para reconhecer como prevê-los.

### Classificação personalizada de textos
- A classificação de textos personalizada permite que os usuários classifiquem texto ou documentos como grupos definidos personalizados. Por exemplo, você pode treinar um modelo para examinar artigos de notícias e identificar a categoria em que eles devem se enquadrar, como _Notícias_ ou _Entretenimento_.

### Respostas às perguntas
- As respostas às perguntas é sobretudo um recurso pré-configurado que fornece respostas para perguntas fornecidas como entrada. Os dados para responder a essas perguntas são provenientes de documentos como perguntas frequentes ou manuais.
- Por exemplo, digamos que você queira criar um assistente de chat virtual no site da sua empresa para responder a perguntas comuns. Você pode usar as perguntas frequentes de uma empresa como o documento de entrada para criar os pares de perguntas e respostas. Depois de implantado, o assistente de chat pode passar perguntas de entrada para o serviço e obter as respostas como resultado.
- Para obter uma lista completa de recursos e como usá-los, confira a [documentação](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/overview) da Linguagem de IA do Azure.
# Entender os recursos para compilar um modelo de compreensão da linguagem coloquial
- Para usar o serviço de reconhecimento vocal para desenvolver uma solução NLP, você precisará criar um recurso de linguagem no Azure. Esse recurso será usado para criar seu modelo e processar solicitações de previsão de aplicativos cliente.

>[!NOTE] Dica
>O laboratório deste módulo aborda a compilação de um modelo para a compreensão da linguagem coloquial. Para obter módulos mais focados na classificação de texto personalizado e no reconhecimento personalizado de entidade nomeada, confira os módulos de solução personalizados no roteiro de aprendizagem [Desenvolver soluções de linguagem natural](https://learn.microsoft.com/pt-br/training/paths/develop-language-solutions-azure-ai).

## Criar seu modelo
- Para recursos que exigem um modelo para previsão, você precisará compilar, treinar e implantar esse modelo antes de usá-lo para fazer uma previsão. Esta construção e treinamento ensinarão ao serviço de Linguagem de IA do Azure o que procurar.

- Primeiro, você precisará criar seu recurso de Linguagem de IA do Azure no [portal do Azure](https://portal.azure.com/). Em seguida:
	1. Pesquise **serviços de IA do Azure**.
	2. Localize e selecione o **serviço de linguagem**.
	3. Selecione **Criar** no **Serviço de Linguagem**.
	4. Preencha os detalhes necessários, escolhendo a região mais próxima geograficamente (para melhor desempenho) e dando a ela um nome exclusivo.

- Depois que esse recurso tiver sido criado, você precisará de uma chave e do ponto de extremidade. Eles podem ser encontrados no lado esquerdo em **Chaves e Ponto de Extremidade** da página de visão geral do recurso.

### Usar o Language Studio
- Para obter um método mais visual de compilação, treinamento e implantação do modelo, você pode usar o [Language Studio](https://aka.ms/languageStudio) para obter cada uma dessas etapas. Na página principal, você pode optar por criar um projeto de **compreensão da linguagem coloquial**. Depois que o projeto for criado, passe pelo mesmo processo que o mostrado acima para compilar, treinar e implantar seu modelo.

[![Screenshot of the Language Studio home page.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/build-language-understanding-model/media/language-studio-conversational-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/build-language-understanding-model/media/language-studio-conversational.png#lightbox)
- O laboratório neste módulo usará o Language Studio para compilar seu modelo. Para saber mais, confira o [início rápido do Language Studio](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/language-studio)

### Usar a API REST
- Uma forma de compilar seu modelo é por meio da API REST. O padrão seria criar seu projeto, importar dados, treinar, implantar e, em seguida, usar seu modelo.
- Essas tarefas são executadas de maneira assíncrona; você precisará enviar uma solicitação para o URI apropriado para cada etapa e, em seguida, enviar outra solicitação para obter o status desse trabalho.
- Por exemplo, se você quiser implantar um modelo para um projeto de compreensão da linguagem coloquial, envie o trabalho de implantação e verifique o status do trabalho de implantação.
#### Autenticação
- Para cada chamada para seu recurso de Linguagem de IA do Azure, você autentica a solicitação fornecendo o cabeçalho a seguir.

|Key|Valor|
|---|---|
|`Ocp-Apim-Subscription-Key`|A chave para o recurso|

#### Solicitar implantação
- Envie uma solicitação **POST** para o ponto de extremidade a seguir.

**rest**

```
{ENDPOINT}/language/authoring/analyze-conversations/projects/{PROJECT-NAME}/deployments/{DEPLOYMENT-NAME}?api-version={API-VERSION}
```

|Espaço reservado|Valor|Exemplo|
|---|---|---|
|`{ENDPOINT}`|O ponto de extremidade do recurso de Linguagem de IA do Azure|`https://<your-subdomain>.cognitiveservices.azure.com`|
|`{PROJECT-NAME}`|O nome do seu projeto. Esse valor diferencia maiúsculas de minúsculas|`myProject`|
|`{DEPLOYMENT-NAME}`|O nome da implantação. Esse valor diferencia maiúsculas de minúsculas|`staging`|
|`{API-VERSION}`|A versão da API que você está chamando|`2022-05-01`|

Inclua o seguinte `body` na solicitação.

**JSON**
```
{
  "trainedModelLabel": "{MODEL-NAME}",
}
```

| Espaço reservado | Valor                                                                                              |
| ---------------- | -------------------------------------------------------------------------------------------------- |
| `{MODEL-NAME}`   | O nome do modelo que será atribuído à implantação. Esse valor diferencia maiúsculas de minúsculas. |

- O envio bem-sucedido da solicitação receberá uma resposta `202` com um cabeçalho de resposta de `operation-location`. Esse cabeçalho terá uma URL com a qual solicitar o status, formatado da seguinte maneira:

**rest**

```
{ENDPOINT}/language/authoring/analyze-conversations/projects/{PROJECT-NAME}/deployments/{DEPLOYMENT-NAME}/jobs/{JOB-ID}?api-version={API-VERSION}
```

#### Obter status da implantação

- Envie uma solicitação **GET** para a URL do cabeçalho de resposta acima. Os valores já estarão preenchidos com base na solicitação de implantação inicial.

**rest**
```
{ENDPOINT}/language/authoring/analyze-conversations/projects/{PROJECT-NAME}/deployments/{DEPLOYMENT-NAME}/jobs/{JOB-ID}?api-version={API-VERSION}
```

|Espaço reservado|Valor|
|---|---|
|`{ENDPOINT}`|O ponto de extremidade para autenticação de sua solicitação de API|
|`{PROJECT-NAME}`|O nome do projeto (com diferenciação de maiúsculas de minúsculas)|
|`{DEPLOYMENT-NAME}`|O nome da implantação (com diferenciação de maiúsculas de minúsculas)|
|`{JOB-ID}`|A ID para localizar o status de treinamento do modelo, encontrada no valor de cabeçalho detalhado acima na solicitação de implantação|
|`{API-VERSION}`|A versão da API que você está chamando|

- O corpo da resposta fornecerá os detalhes do status da implantação. O campo `status` terá o valor de _êxito_ quando a implantação for concluída.

**JSON**
```
{
    "jobId":"{JOB-ID}",
    "createdDateTime":"String",
    "lastUpdatedDateTime":"String",
    "expirationDateTime":"String",
    "status":"running"
}
```

- Para obter um passo a passo completo de cada etapa com solicitações de exemplo, consulte o [início rápido de reconhecimento de conversa](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/conversational-language-understanding/quickstart?pivots=rest-api#create-a-clu-project).

## Consultar seu modelo
- Para consultar seu modelo para uma previsão, você pode usar SDKs em C# ou Python ou usar a API REST.
### Consultar usando SDKs
- Para consultar seu modelo usando um SDK, primeiro você precisa criar seu cliente. Depois de ter seu cliente, você o usará para chamar o ponto de extremidade apropriado.

**C#**
```
var languageClient = new TextAnalyticsClient(endpoint, credentials);
var response = languageClient.ExtractKeyPhrases(document);
```

**Python**
```
language_client = TextAnalyticsClient(
            endpoint=endpoint, 
            credential=credentials)
response = language_client.extract_key_phrases(documents = documents)[0]
```

- Outros recursos de linguagem, como compreensão da linguagem coloquial, exigem que a solicitação seja criada e enviada de forma diferente.

**C#**
```
var data = new
{
    analysisInput = new
    {
        conversationItem = new
        {
            text = userText,
            id = "1",
            participantId = "1",
        }
    },
    parameters = new
    {
        projectName,
        deploymentName,
        // Use Utf16CodeUnit for strings in .NET.
        stringIndexType = "Utf16CodeUnit",
    },
    kind = "Conversation",
};
Response response = await client.AnalyzeConversationAsync(RequestContent.Create(data));
```

**Python**
```
result = client.analyze_conversation(
    task={
        "kind": "Conversation",
        "analysisInput": {
            "conversationItem": {
                "participantId": "1",
                "id": "1",
                "modality": "text",
                "language": "en",
                "text": query
            },
            "isLoggingEnabled": False
        },
        "parameters": {
            "projectName": cls_project,
            "deploymentName": deployment_slot,
            "verbose": True
        }
    }
)
```

### Consultar usando a API REST
- Para consultar seu modelo usando REST, crie uma solicitação **POST** para a URL apropriada com o corpo apropriado especificado. Para recursos internos, como detecção de idioma ou análise de sentimento, você consultará o ponto de extremidade `analyze-text`.

 Dica

Lembre-se de que cada pedido precisa de ser autenticado com a sua chave de recurso da Linguagem de IA do Azure no cabeçalho `Ocp-Apim-Subscription-Key`

restCopiar

```
{ENDPOINT}/language/:analyze-text?api-version={API-VERSION}
```

Expandir a tabela

|Espaço reservado|Valor|
|---|---|
|`{ENDPOINT}`|O ponto de extremidade para autenticação de sua solicitação de API|
|`{API-VERSION}`|A versão da API que você está chamando|

- Dentro do corpo dessa solicitação, você deve especificar o parâmetro `kind`, que informa ao serviço qual tipo de reconhecimento vocal você está solicitando.

Se você quiser detectar o idioma, por exemplo, o corpo JSON seria semelhante ao seguinte.

JSONCopiar

```
{
    "kind": "LanguageDetection",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
            {
                "id":"1",
                "text": "This is a document written in English."
            }
        ]
    }
}
```

- Outros recursos de linguagem, como compreensão da linguagem coloquial, exigem que a solicitação seja roteada para um ponto de extremidade diferente. Por exemplo, a solicitação de compreensão da linguagem coloquial seria enviada para o seguinte.

restCopiar

```
{ENDPOINT}/language/:analyze-conversations?api-version={API-VERSION}
```

Expandir a tabela

|Espaço reservado|Valor|
|---|---|
|`{ENDPOINT}`|O ponto de extremidade para autenticação de sua solicitação de API|
|`{API-VERSION}`|A versão da API que você está chamando|

Essa solicitação incluiria um corpo JSON semelhante ao seguinte.

JSONCopiar

```
{
  "kind": "Conversation",
  "analysisInput": {
    "conversationItem": {
      "id": "1",
      "participantId": "1",
      "text": "Sample text"
    }
  },
  "parameters": {
    "projectName": "{PROJECT-NAME}",
    "deploymentName": "{DEPLOYMENT-NAME}",
    "stringIndexType": "TextElement_V8"
  }
}
```

Expandir a tabela

|Espaço reservado|Valor|
|---|---|
|`{PROJECT-NAME}`|O nome do projeto no qual você compilou seu modelo|
|`{DEPLOYMENT-NAME}`|O nome da sua implantação|

### Resposta de amostra

- A resposta de consulta de um SDK será retornada no objeto, que varia dependendo do recurso (como em `response.key_phrases` ou `response.Value`). A API REST retornará JSON que seria semelhante ao seguinte.

JSONCopiar

```
{
    "kind": "KeyPhraseExtractionResults",
    "results": {
        "documents": [{
            "id": "1",
            "keyPhrases": ["modern medical office", "Dr. Smith", "great staff"],
            "warnings": []
        }],
        "errors": [],
        "modelVersion": "{VERSION}"
    }
}
```

- Para outros modelos, como compreensão da linguagem coloquial, uma resposta de exemplo à consulta seria semelhante à seguinte.

JSONCopiar

```
{
  "kind": "ConversationResult",
  "result": {
    "query": "String",
    "prediction": {
      "topIntent": "intent1",
      "projectKind": "Conversation",
      "intents": [
        {
          "category": "intent1",
          "confidenceScore": 1
        },
        {
          "category": "intent2",
          "confidenceScore": 0
        }
      ],
      "entities": [
        {
          "category": "entity1",
          "text": "text",
          "offset": 7,
          "length": 4,
          "confidenceScore": 1
        }
      ]
    }
  }
}
```

- Os SDKs para Python e C# retornam JSON que é muito semelhante à resposta REST.

- Para obter documentação completa sobre recursos, incluindo exemplos e guias de instruções, confira as páginas de [documentação da Linguagem de IA do Azure](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/).