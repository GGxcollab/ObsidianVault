# Introdução
- Um padrão comum para os aplicativos "inteligentes" é permitir que os usuários façam perguntas usando uma linguagem natural e recebam as respostas adequadas. Na verdade, esse tipo de solução faz com que as publicações tradicionais de perguntas frequentes tenham uma inteligência conversacional. Neste módulo, você aprenderá como utilizar a Linguagem de IA do Azure para criar uma base de conhecimento de pares de perguntas e respostas que podem dar suporte a um aplicativo ou bot.
- Depois de concluir este módulo, você poderá:
	- Compreenda as respostas às perguntas e como elas se comparam à compreensão da linguagem.
	- Criar, testar, publicar e consumir uma base de conhecimento.
	- Implemente conversa com várias rodadas e aprendizado ativo.
	- Crie um bot de resposta às perguntas para interagir utilizando linguagem natural.
# Entender respostas às perguntas
- A **Linguagem de IA do Azure** inclui um recurso de _resposta às perguntas_, que permite definir uma _base de conhecimento_ de pares de perguntas e respostas que podem ser utilizadas usando entrada de linguagem natural. A base de dados de conhecimento pode ser publicada em um ponto de extremidade REST e consumida por aplicativos cliente, normalmente _bots_.

![A diagram showing how a conversational app uses a knowledge base of questions and answers.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/diagram.png)

- A base de dados de conhecimento pode ser criada a partir de fontes existentes, incluindo:
	- Sites que contêm a documentação de FAQ (perguntas frequentes).
	- Arquivos que contêm texto estruturado, como folhetos ou guias de usuário.
	- Pares de perguntas e respostas de _bate-papo_ integrados que encapsulam trocas de conversação comuns.

>[!NOTE] Observação
>A capacidade de resposta às perguntas da Linguagem de IA do Azure é uma versão mais recente do **Serviço QnA**, que ainda existe como um serviço autônomo. Para saber como migrar uma base de dados de conheciment o do QnA Maker para a Linguagem de IA do Azure, consulte o [guia de instruções de migração](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/question-answering/how-to/migrate-qnamaker).

# Comparar as respostas às perguntas com a compreensão da Linguagem de IA do Azure
- Uma base de conhecimento de resposta às perguntas é uma forma de modelo de linguagem, o que levanta a questão de quando usar a resposta às perguntas e quando utilizar as capacidades de _compreensão de linguagem coloquial_ da Linguagem de IA do Azure.
- Os dois são semelhantes, já que ambos permitem que você defina um modelo de linguagem que pode ser consultado usando expressões de linguagem natural. No entanto, há algumas diferenças nos casos de uso que eles foram projetados para resolver, conforme mostrado na seguinte tabela:

|                           | Respostas às perguntas                                                                                                                               | Reconhecimento vocal                                                                                                                       |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Padrão de uso**             | O usuário envia uma pergunta, esperando uma resposta                                                                                                 | O usuário envia um enunciado, esperando uma resposta ou uma ação apropriada                                                                |
| **Processamento de consulta** | O serviço usa o reconhecimento de linguagem natural para fazer a correspondência de a uma pergunta com uma resposta na base de dados de conhecimento | O serviço usa o reconhecimento de linguagem natural para interpretar o enunciado, correspondê-lo a uma intenção e identificar as entidades |
| **Resposta**                  | A resposta é uma resposta estática a uma pergunta conhecida                                                                                          | A resposta indica a intenção mais provável e entidades referenciadas                                                                       |
| **Lógica do cliente**         | O aplicativo cliente normalmente apresenta a resposta para o usuário                                                                                 | O aplicativo cliente é responsável por executar a ação apropriada com base na intenção detectada                                           |
- Os dois serviços são, na verdade, complementares. Você pode criar soluções abrangentes de linguagem natural que combinem modelos de reconhecimento de linguagem e bases de conhecimento de resposta às perguntas.
# Como criar uma base de dados de conhecimento
- Para criar uma solução de resposta às perguntas, você pode usar a API REST ou SDK para escrever um código que defina, treine e publique a base de conhecimento. Entretanto, é mais comum utilizar a interface da Web do [Estúdio de Linguagem](https://language.azure.com/) para definir e gerenciar uma base de conhecimentos.

- Para criar uma base de dados de conhecimento, você deve:
	1. Entre no portal do Azure.
	    
	2. Pesquise **Azure AI Services**usando o campo de pesquisa na parte superior do portal.
	    
	3. Selecione **Criar** no recurso **Language Service**.
	    
	4. Criar um recurso na sua assinatura do Azure:
	    - Habilite o recurso de _Resposta às perguntas_.
	    - Criar ou selecionar um recurso **Azure AI Search** para hospedar o índice da base de dados de conhecimento.
	    
	5. No Estúdio de Linguagem, selecione seu recurso de Linguagem de IA do Azure e crie um projeto de **Resposta às perguntas personalizado** (**custom Question Answering**).
	    
	6. Adicione uma ou mais fontes de dados para preencher a base de conhecimento:
	    - URLs para páginas da web contendo perguntas frequentes.
	    - Arquivos contendo texto estruturado a partir do qual perguntas e respostas podem ser derivadas.
	    - Conjuntos de dados de _bate-papo_ predefinidos que incluem perguntas e respostas comuns de conversas em um estilo específico.

	7. Editar os pares de perguntas e respostas no portal.
# Implementar conversa com várias rodadas
- Embora muitas vezes você possa criar uma base de dados de conhecimento eficaz que consiste em pares individuais de perguntas e respostas, às vezes talvez seja necessário fazer perguntas de acompanhamento para gerar mais informações de um usuário antes de apresentar uma resposta definitiva. Esse tipo de interação é conhecido como uma _conversa com várias rodadas_ (_multi-round conversation_).

![A diagram showing a multi-turn conversation.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/multi-turn-conversation.png)

- Você pode habilitar respostas multi-turn ao importar perguntas e respostas de uma página da web existente ou documento com base em sua estrutura, ou você pode definir explicitamente prompts de acompanhamento e respostas para perguntas e pares de respostas existentes.

- Por exemplo, suponha que uma pergunta inicial para uma base de dados de conhecimento de reserva de viagem seja "Como posso cancelar uma reserva?". Uma reserva pode se referir a um hotel ou voo, portanto, um prompt de acompanhamento é necessário para esclarecer esse detalhe. A resposta pode consistir em um texto como "As políticas de cancelamento dependem do tipo de reserva" e incluir prompts de acompanhamento com links para respostas sobre como cancelar voos e hotéis.

- Ao definir um prompt de acompanhamento para a conversa com várias rodadas, você pode vincular a uma resposta existente na base de dados de conhecimento ou definir uma nova resposta especificamente para o acompanhamento. Você também pode restringir a resposta vinculada para que ela seja exibida apenas no contexto da conversa com várias rodadas iniciada pela pergunta original.
# Testar e publicar uma base de conhecimento
- Depois de definir uma base de dados de conhecimento, você pode treinar seu modelo de linguagem natural e testá-lo antes de publicá-lo para uso em um aplicativo ou bot.
### Testar uma base de dados de conhecimento
- Você pode testar sua base de conhecimento interativamente no Language Studio, enviando perguntas e revisando as respostas que são retornadas. Você pode inspecionar os resultados para exibir suas pontuações de confiança, bem como outras respostas potenciais.

[![Screenshot of the test pane of the custom question answering project in the Language studio.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/test-new-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/test-new.png#lightbox)
### Implantar uma base de conhecimento
- Quando estiver satisfeito com o desempenho de sua base de conhecimento, você pode implementá-la em um terminal REST que os aplicativos cliente podem usar para enviar perguntas e receber respostas. Você deve implantar diretamente do Estúdio de Linguagem.

# Usar uma base de dados de conhecimento
- Para consumir a base de conhecimento publicada, você pode usar a interface REST.
- O corpo da solicitação mínima para a função contém uma pergunta, como esta:

**JSON**
```
{
  "question": "What do I need to do to cancel a reservation?",
  "top": 2,
  "scoreThreshold": 20,
  "strictFilters": [
    {
      "name": "category",
      "value": "api"
    }
  ]
}
```

| Propriedade    | Descrição                                                         |
| -------------- | ----------------------------------------------------------------- |
| pergunta       | Pergunta a ser enviada à base de dados de conhecimento.           |
| top            | Número máximo de respostas que serão retornadas.                  |
| scoreThreshold | Limite de pontuação para as respostas retornadas.                 |
| strictFilters  | Limite apenas às respostas que contêm os metadados especificados. |

- A resposta inclui a pergunta correspondente mais próxima que foi encontrada na base de conhecimento, juntamente com a resposta associada, a pontuação de confiança e outros metadados sobre o par de pergunta e resposta:

**JSON**
```

{
  "answers": [
    {
      "score": 27.74823341616769,
      "id": 20,
      "answer": "Call us on 555 123 4567 to cancel a reservation.",
      "questions": [
        "How can I cancel a reservation?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    }
  ]
}
```
# Aprimorar o desempenho de respostar às perguntas
- Depois de criar e testar uma base de conhecimento, você pode melhorar seu desempenho com _aprendizado ativo_ e definindo _sinônimos_.

## Usar o aprendizado ativo
- A aprendizagem ativa pode ajudar você a fazer aprimoramentos contínuos para melhorar a resposta correta às perguntas dos usuários ao longo do tempo. As pessoas geralmente fazem perguntas que são formuladas de forma diferente, mas que, no final das contas, têm o mesmo significado. O aprendizado ativo pode ajudar em situações como essa, pois habilita você a considerar perguntas alternativas para cada par de perguntas e respostas. O aprendizado ativo está habilitado por padrão.

 Para utilizar o aprendizado ativo, você pode fazer o seguinte: 
### Crie seus pares de perguntas e respostas
Você deve criar pares de perguntas e respostas no Estúdio de Linguagem para o seu projeto. Você também pode importar um arquivo que contenha pares de perguntas e respostas para fazer upload em massa.

[![A screenshot showing how to import a file with question and answer pairs.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/import-file-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/import-file.png#lightbox)

### Analisar sugestões

O aprendizado ativo começa então a oferecer perguntas alternativas para cada pergunta em seus pares de perguntas e respostas. Você deve acessar essa opção no painel de sugestões de revisão:

[![A screenshot of the Review suggestions pane.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/review-suggestions-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/review-suggestions.png#lightbox)

Você deve analisar e, em seguida, aceitar ou rejeitar essas frases alternativas sugeridas para cada pergunta, selecionando a marca de seleção ou o símbolo de exclusão ao lado da frase alternativa. Você pode aceitar ou rejeitar sugestões em massa usando a opção **Aceitar todas as sugestões** ou **Rejeitar todas as sugestões** na parte superior.

Você também pode adicionar manualmente perguntas alternativas ao selecionar **Adicionar pergunta alternativa** para um par no painel Editar base de conhecimento:

[![A screenshot showing the Add alternate question option on the Edit knowledge base pane.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/add-alternate-questions-manual-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-question-answer-solution-ai-language/media/add-alternate-questions-manual.png#lightbox)

 Observação

Para obter mais informações sobre aprendizado ativo, consulte [Enriqueça seu projeto com aprendizado ativo](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/question-answering/tutorials/active-learning).

## Definir sinônimos

Os sinônimos são úteis quando as perguntas enviadas pelos usuários podem incluir várias palavras diferentes para significar a mesma coisa. Por exemplo, um cliente de uma Agência de viagens pode se referir a uma "reserva" ou a "agendamento". Ao defini-los como sinônimos, o serviço de resposta a perguntas pode encontrar uma resposta apropriada, independentemente de qual termo um cliente individual usa.

Para definir sinônimos, você deve usar a API REST para enviar sinônimos no seguinte formato JSON:

JSONCopiar

```
{
    "synonyms": [
        {
            "alterations": [
                "reservation",
                "booking"
                ]
        }
    ]
}
```

>[!NOTE] Observação
>Para saber mais sobre sinônimos, confira [Melhorar a qualidade de resposta com sinônimos](https://learn.microsoft.com/pt-br/azure/ai-services/language-service/question-answering/tutorials/adding-synonyms).

![[Pasted image 20241111135736.png]]