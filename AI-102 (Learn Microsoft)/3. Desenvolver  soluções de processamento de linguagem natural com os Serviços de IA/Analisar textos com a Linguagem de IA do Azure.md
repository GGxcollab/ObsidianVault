# Introdução
- Todos os dias, o mundo gera uma enorme quantidade de dados; grande parte dele baseada em texto na forma de emails, postagens de mídias sociais, revisões online, documentos de negócios e muito mais. Técnicas de inteligência artificial que aplicam modelos estatísticos e semânticos permitem que você crie aplicativos que extraem significado e insights dos dados baseados em texto.

- A Linguagem de IA do Azure fornece uma API para técnicas comuns de análise de texto que você pode integrar facilmente ao código do seu próprio aplicativo.

- Neste módulo, você aprenderá como utilizar a Linguagem de IA do Azure para:
	- Detecção de idioma a partir do texto.
	- Analisar o sentimento do texto.
	- Extrair frases-chave, entidades e entidades vinculadas.

# Provisionar um recurso de Linguagem de IA do Azure
- A Linguagem de IA do Azure foi projetada para ajudar você a extrair informações do texto. Ele fornece funcionalidade que você pode usar para:
	- _Detecção de idioma_ – determinar o idioma no qual o texto está escrito.
	- _Extração de frases-chave_ – identificar palavras e frases importantes no texto que indicam os pontos principais.
	- _Análise de sentimento_ – quantificar o quanto o texto é positivo ou negativo.
	- _Reconhecimento de entidade nomeada_ – detectar referências a entidades, incluindo pessoas, locais, períodos, organizações e muito mais.
	- _Vinculação de entidade_ – identificar entidades específicas fornecendo links de referência para artigos da Wikipédia.
    
    ![Diagram showing an Azure AI Language resource performing language detection, key phrase extraction, sentiment analysis, named entity recognition, and entity linking.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/analyze-text-ai-language/media/text-analytics-resource.png)
    

## Recursos do Azure para análise de texto
Para utilizar a Linguagem de IA do Azure para analisar texto, você deve provisionar um recurso para ela na sua assinatura do Azure.

Após o provisionamento de um recurso adequado na sua assinatura do Azure, você pode utilizar seu **ponto de extremidade** e uma de suas **chaves** para chamar as APIs da Linguagem de IA do Azure a partir do seu código. Você pode chamar as APIs de Linguagem de IA do Azure enviando solicitações no formato JSON para a interface REST ou usando qualquer um dos SDKs de programação específicos por linguagem.

>[!NOTE] Observação
>Os exemplos de código nas unidades subsequentes neste módulo mostram as solicitações JSON e as respostas trocadas com a interface REST. Ao usar um SDK, as solicitações JSON são abstraídas por objetos e métodos apropriados que encapsulam os mesmos valores de dados. Você terá a oportunidade de experimentar o SDK para C# ou Python por conta própria no exercício posterior do módulo.

# Detectar o idioma
- A API de detecção de idioma da IA do Azure avalia a entrada de texto e, para cada documento enviado, retorna identificadores de idioma com uma pontuação que indica a força da análise.
- Esse recurso é útil para conteúdo armazena esse texto arbitrário de coleção, onde o idioma é desconhecido. Outro cenário poderia envolver um bot de chat. Se um usuário iniciar uma sessão com o bot de chat, a detecção de idioma poderá ser usada para determinar qual idioma ele está usando e permitirá que você configure suas respostas de bot no idioma apropriado.
- Você pode analisar os resultados dessa análise para determinar qual idioma é usado no documento de entrada. A resposta também retorna uma pontuação que reflete a confiança do modelo (um valor entre 0 e 1).
- A detecção de idioma pode funcionar com documentos ou frases únicas. É importante observar que o tamanho do documento deve ter menos de 5.120 caracteres. O limite de tamanho é por documento e cada coleção é restrita a 1.000 itens (IDs). Uma amostra de um conteúdo JSON formatado corretamente que você pode enviar para o serviço no corpo da solicitação é exibida aqui, incluindo uma coleção de **documentos**, cada um contendo uma **ID** exclusiva e o **texto**a ser analisado. Opcionalmente, você pode fornecer uma **countryHint** para melhorar o desempenho da previsão.

**JSON**
```
{
    "kind": "LanguageDetection",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
              {
                "id": "1",
                "text": "Hello world",
                "countryHint": "US"
              },
              {
                "id": "2",
                "text": "Bonjour tout le monde"
              }
        ]
    }
}
```

- O serviço retornará uma resposta JSON que contém um resultado para cada **documento** no corpo da solicitação, incluindo o idioma previsto e um valor que indica o nível de confiança da previsão. O nível de confiança é um valor que varia de 0 a 1 com valores mais próximos de 1 sendo um nível de confiança mais alto. Aqui está um exemplo de resposta JSON padrão que mapeia para o JSON da solicitação acima.

**JSON**
```
{   "kind": "LanguageDetectionResults",
    "results": {
        "documents": [
          {
            "detectedLanguage": {
              "confidenceScore": 1,
              "iso6391Name": "en",
              "name": "English"
            },
            "id": "1",
            "warnings": []
          },
          {
            "detectedLanguage": {
              "confidenceScore": 1,
              "iso6391Name": "fr",
              "name": "French"
            },
            "id": "2",
            "warnings": []
          }
        ],
        "errors": [],
        "modelVersion": "2022-10-01"
    }
}

```

- Em nosso exemplo, todos os idiomas mostram uma confiança de 1, principalmente porque o texto é relativamente simples e fácil de identificar a linguagem.

- Se você apresentar um documento com conteúdo multilíngue, o serviço se comportará de um modo um pouco diferente. O conteúdo de idioma misto dentro do mesmo documento retorna o idioma com a representação maior no conteúdo, mas com uma classificação positiva inferior, refletindo a intensidade marginal dessa avaliação. No exemplo a seguir, a entrada é uma mistura de inglês, espanhol e francês. O analisador usa a análise estatística do texto para determinar o idioma _predominante_.

**JSON**
```
{
  "documents": [
    {
      "id": "1",
      "text": "Hello, I would like to take a class at your University. ¿Se ofrecen clases en español? Es mi primera lengua y más fácil para escribir. Que diriez-vous des cours en français?"
    }
  ]
}
```

O exemplo a seguir mostra uma resposta para esse exemplo de vários idiomas.

**JSON**
```
{
    "documents": [
        {
            "id": "1",
            "detectedLanguage": {
                "name": "Spanish",
                "iso6391Name": "es",
                "confidenceScore": 0.9375
            },
            "warnings": []
        }
    ],
    "errors": [],
    "modelVersion": "2022-10-01"
}
```

- A última condição a considerar é quando há ambiguidade no conteúdo do idioma. O cenário poderá acontecer se você enviar um conteúdo textual que o analisador não é capaz de analisar, por exemplo, devido a problemas de codificação de caractere ao converter o texto em uma variável de cadeia de caracteres. Como resultado, a resposta para o nome do idioma e o código ISO indicará (desconhecido) e o valor da pontuação será retornado como `0`. O exemplo de código a seguir mostra o aspecto da resposta.

**JSON**
```
{
    "documents": [
        {
            "id": "1",
            "detectedLanguage": {
                "name": "(Unknown)",
                "iso6391Name": "(Unknown)",
                "confidenceScore": 0.0
            },
            "warnings": []
        }
    ],
    "errors": [],
    "modelVersion": "2022-10-01"
}
```

# Extrair frases-chave
- A extração de frases-chave é o processo de avaliar o texto de documentos e identificar os principais pontos relacionados ao contexto dos documentos.
- A extração de frases-chave funciona melhor para documentos maiores (o tamanho máximo que pode ser analisado é de 5.120 caracteres).
- Assim como na detecção de idioma, a interface REST permite que você envie um ou mais documentos para análise.

**JSON**
```
{
    "kind": "KeyPhraseExtraction",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
            {
              "id": "1",
              "language": "en",
              "text": "You must be the change you wish 
                       to see in the world."
            },
            {
              "id": "2",
              "language": "en",
              "text": "The journey of a thousand miles 
                       begins with a single step."
            }
        ]
    }
}
```

- A resposta contém uma lista de frases-chave detectadas em cada documentação:

**JSON**
```

{
    "kind": "KeyPhraseExtractionResults",
    "results": {
    "documents": [   
        {
         "id": "1",
         "keyPhrases": [
           "change",
           "world"
         ],
         "warnings": []
       },
       {
         "id": "2",
         "keyPhrases": [
           "miles",
           "single step",
           "journey"
         ],
         "warnings": []
       }
],
    "errors": [],
    "modelVersion": "2021-06-01"
    }
}
```

# Analisar sentimento
- A análise de sentimento é usada para avaliar o quanto um documento de texto é positivo ou negativo, o que pode ser útil em várias cargas de trabalho, como:
	- Avaliar um filme, um livro ou um produto ao quantificar o sentimento com base em opiniões.
	- Priorizar respostas do serviço de atendimento ao consumidor para a correspondência recebida por email ou mensagens de mídias sociais.

- Ao utilizar a Linguagem de IA do Azure para avaliar o sentimento, a resposta inclui o sentimento da documentação de modo geral e o sentimento da sentença individual para cada documento enviado para o serviço.

- Por exemplo, você pode enviar um único documento para uma análise de sentimento como esta:

**JSON**
```
{
  "kind": "SentimentAnalysis",
  "parameters": {
    "modelVersion": "latest"
  },
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "Good morning!"
      }
    ]
  }
}

```

- A resposta do servidor pode se parecer com o seguinte:

**JSON*
```
{
  "kind": "SentimentAnalysisResults",
  "results": {
    "documents": [
      {
        "id": "1",
        "sentiment": "positive",
        "confidenceScores": {
          "positive": 0.89,
          "neutral": 0.1,
          "negative": 0.01
        },
        "sentences": [
          {
            "sentiment": "positive",
            "confidenceScores": {
              "positive": 0.89,
              "neutral": 0.1,
              "negative": 0.01
            },
            "offset": 0,
            "length": 13,
            "text": "Good morning!"
          }
        ],
        "warnings": []
      }
    ],
    "errors": [],
    "modelVersion": "2022-11-01"
  }
}
```

- O sentimento da frase baseia-se em pontuações de confiança para valores de classificação **positivos**, **negativos** e **neutros** entre zero e um.

- O sentimento geral do documento baseia-se em frases:
	- Se todas as frases forem neutras, o sentimento geral será neutro.
	- Se as classificações de sentenças incluírem apenas as positivas e neutras, o sentimento geral será positivo.
	- Se as classificações de frase incluírem apenas as negativas e neutras, o sentimento geral será negativo.
	- Se as classificações de frase incluírem as positivas e negativas, o sentimento geral será misto.
# Extrair entidades
- O Reconhecimento de Entidade Nomeada identifica as entidades mencionadas no texto. As entidades são agrupadas em categorias e subcategorias, por exemplo:
	- Pessoa
	- Localização
	- Datetime
	- Organização
	- Endereço
	- Email
	- URL

>[!NOTE] Observação
>Para obter uma lista completa de categorias, consulte a [documentação](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/named-entity-recognition/concepts/named-entity-categories?tabs=ga-api).

- A entrada para o reconhecimento de entidade é semelhante à entrada para as outras funções de API de Linguagem de IA do Azure:

**JSON**
```
{
  "kind": "EntityRecognition",
  "parameters": {
    "modelVersion": "latest"
  },
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "Joe went to London on Saturday"
      }
    ]
  }
}
```

- A resposta inclui uma lista de entidades categorizadas encontradas em cada documento:

**JSON**
```
{
    "kind": "EntityRecognitionResults",
     "results": {
          "documents":[
              {
                  "entities":[
                  {
                    "text":"Joe",
                    "category":"Person",
                    "offset":0,
                    "length":3,
                    "confidenceScore":0.62
                  },
                  {
                    "text":"London",
                    "category":"Location",
                    "subcategory":"GPE",
                    "offset":12,
                    "length":6,
                    "confidenceScore":0.88
                  },
                  {
                    "text":"Saturday",
                    "category":"DateTime",
                    "subcategory":"Date",
                    "offset":22,
                    "length":8,
                    "confidenceScore":0.8
                  }
                ],
                "id":"1",
                "warnings":[]
              }
          ],
          "errors":[],
          "modelVersion":"2021-01-15"
    }
}
```

- Para obter mais informações sobre entidades, consulte o módulo [Criação de um modelo de compreensão da linguagem coloquial](https://learn.microsoft.com/pt-br/training/modules/build-language-understanding-model/).
# Extrair entidades vinculadas
- Em alguns casos, o mesmo nome pode ser aplicável a mais de uma entidade. Por exemplo, uma instância da palavra "Vênus" refere-se ao planeta ou à deusa da mitologia?

- A vinculação de entidades pode ser usada para desambiguar entidades de mesmo nome ao referenciar um artigo em uma base de dados de conhecimento. A Wikipédia fornece a base de dados de conhecimento para o serviço de Análise de Texto. Os links de artigo específicos são determinados com base no contexto da entidade dentro do texto.

- Por exemplo, "Eu vi Vênus iluminado no céu" está associado ao link [https://en.wikipedia.org/wiki/Venus](https://en.wikipedia.org/wiki/Venus); enquanto "Vênus, a Deusa da beleza" está associado a [https://en.wikipedia.org/wiki/Venus_(mythology)](https://en.wikipedia.org/wiki/Venus_(mythology)).

- Assim como acontece com todas as funções de Linguagem de IA do Azure, você pode enviar um ou mais documentos para análise:

**JSON**
```

{
  "kind": "EntityLinking",
  "parameters": {
    "modelVersion": "latest"
  },
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "I saw Venus shining in the sky"
      }
    ]
  }
}
```

- A resposta inclui as entidades identificadas no texto juntamente com links para os artigos associados:

**JSON**
```
{
  "kind": "EntityLinkingResults",
  "results": {
    "documents": [
      {
        "id": "1",
        "entities": [
          {
            "bingId": "89253af3-5b63-e620-9227-f839138139f6",
            "name": "Venus",
            "matches": [
              {
                "text": "Venus",
                "offset": 6,
                "length": 5,
                "confidenceScore": 0.01
              }
            ],
            "language": "en",
            "id": "Venus",
            "url": "https://en.wikipedia.org/wiki/Venus",
            "dataSource": "Wikipedia"
          }
        ],
        "warnings": []
      }
    ],
    "errors": [],
    "modelVersion": "2021-06-01"
  }
}
```

![[Pasted image 20241107151552.png]]