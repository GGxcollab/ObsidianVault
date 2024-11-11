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

# Comparar as respostas às perguntas com a comprrensão