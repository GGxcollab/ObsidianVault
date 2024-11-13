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

Os recursos do Serviço de Linguagem de IA do Azure se enquadram em duas categorias: recursos pré-configurados e recursos aprendidos. Os recursos aprendidos exigem a criação e o treinamento de um modelo para prever corretamente os rótulos apropriados, o que é abordado nas próximas unidades deste módulo.

Esta unidade aborda a maioria dos recursos do serviço de Linguagem de IA do Azure, mas você pode consultar a [documentação do serviço de Linguagem de IA do Azure](https://learn.microsoft.com/pt-br/azure/cognitive-services/language-service/overview) para obter uma lista completa, incluindo inícios rápidos e uma explicação completa de tudo o que está disponível.

O uso desses recursos em seu aplicativo requer o envio da consulta para o ponto de extremidade apropriado. O ponto de extremidade usado para consultar um recurso específico varia, mas todos eles são prefixados com o recurso de Linguagem de IA do Azure criado em sua conta do Azure, ao criar a sua solicitação REST ou ao definir o seu cliente utilizando um SDK. Exemplos dessas ferramentas podem ser encontrados na próxima unidade.

## Recursos pré-configurados

O serviço de Linguagem de IA do Azure fornece determinados recursos sem qualquer rotulagem ou treinamento de modelo. Depois de criar seu recurso, você pode enviar seus dados e usar os resultados retornados em seu aplicativo.

Todos os recursos a seguir estão pré-configurados.

### Resumo

O resumo está disponível para documentos e conversas e resumirá o texto em frases-chave previstas para encapsular o significado da entrada.

### Reconhecimento de entidade nomeada

O reconhecimento de entidade nomeada pode extrair e identificar entidades, como pessoas, locais ou empresas, permitindo que seu aplicativo reconheça diferentes tipos de entidades para respostas de linguagem natural aprimoradas. Por exemplo, no texto "O píer à beira-mar é minha atração favorita de Seattle", _Seattle_ seria identificada e categorizada como um local.

### Detecção de PIIs (informações de identificação pessoal)

A detecção de PII permite identificar, categorizar e redigir informações que podem ser consideradas confidenciais, como endereços de email, endereços residenciais, endereços IP, nomes e informações de integridade protegidas. Por exemplo, se o texto "email@contoso.com" foi incluído na consulta, todo o endereço de email poderá ser identificado e redigido.

### Extração de frases-chave

A extração de frase-chave é um recurso que extrai rapidamente os principais conceitos do texto fornecido. Por exemplo, no texto "Análise de Texto é um dos recursos nos Serviços de IA do Azure.", o serviço extrairia _"Serviços de IA do Azure"_ e _"Análise de Texto"_.

### Análise de sentimento

A análise de sentimento identifica o quão positiva ou negativa é uma cadeia de caracteres ou um documento. Por exemplo, no texto "Ótimo hotel. Perto de muitos restaurantes e atrações para ir a pé", o serviço identificaria isso como _positivo_ com uma pontuação de confiança relativamente alta.

### Detecção de idioma

A detecção de idioma usa um ou mais documentos e identifica o idioma para cada um deles. Por exemplo, se o texto de um dos documentos fosse "Bonjour", o serviço o identificaria como _francês_.

## Recursos aprendidos

Os recursos aprendidos exigem que você rotule dados, treine e implante seu modelo para disponibilizá-los para uso em seu aplicativo. Esses recursos permitem personalizar quais informações são previstas ou extraídas.

 Observação

A qualidade dos dados afeta muito a precisão do modelo. Seja objetivo sobre quais dados são usados, quão bem eles são marcados ou rotulados e quão variados são os dados de treinamento. Para obter detalhes, consulte as [recomendações para rotular dados](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/conversational-language-understanding/how-to/tag-utterances), que inclui diretrizes importantes para marcação de dados. Veja também as [métricas de avaliação](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/custom-text-classification/concepts/evaluation-metrics) que podem ajudar a identificar onde seu modelo precisa de melhorias.

### Compreensão da linguagem coloquial (CLU)

A CLU é um dos principais recursos personalizados oferecidos pela Linguagem de IA do Azure. A CLU ajuda os usuários a compilar modelos de reconhecimento de linguagem natural personalizados para prever a intenção geral e extrair informações importantes de enunciados de entrada. A CLU exige que os dados sejam marcados pelo usuário para ensiná-los a prever intenções e entidades com precisão.

O exercício neste módulo será criar um modelo de CLU e usá-lo em seu aplicativo.

### Reconhecimento de Entidade Nomeada personalizado

O reconhecimento de entidade personalizada usa dados rotulados personalizados e extrai entidades especificadas de texto não estruturado. Por exemplo, se tiver vários documentos de contrato dos quais deseja extrair as partes envolvidas, você poderá treinar um modelo para reconhecer como prevê-los.

### Classificação personalizada de textos

A classificação de textos personalizada permite que os usuários classifiquem texto ou documentos como grupos definidos personalizados. Por exemplo, você pode treinar um modelo para examinar artigos de notícias e identificar a categoria em que eles devem se enquadrar, como _Notícias_ ou _Entretenimento_.

### Respostas às perguntas

As respostas às perguntas é sobretudo um recurso pré-configurado que fornece respostas para perguntas fornecidas como entrada. Os dados para responder a essas perguntas são provenientes de documentos como perguntas frequentes ou manuais.

Por exemplo, digamos que você queira criar um assistente de chat virtual no site da sua empresa para responder a perguntas comuns. Você pode usar as perguntas frequentes de uma empresa como o documento de entrada para criar os pares de perguntas e respostas. Depois de implantado, o assistente de chat pode passar perguntas de entrada para o serviço e obter as respostas como resultado.

Para obter uma lista completa de recursos e como usá-los, confira a [documentação](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/overview) da Linguagem de IA do Azure.