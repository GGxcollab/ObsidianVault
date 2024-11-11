# Introdução
_Processamento da linguagem natural_ (NLP) é um problema comum de IA no qual o software deve ser capaz de trabalhar com texto ou fala na forma de linguagem natural que um usuário humano escreveria ou falaria. Dentro do NLP, existe a _Compreensão da linguagem natural_ (NLU), que lida com o problema de determinar o significado semântico da linguagem natural, geralmente usando um modelo de linguagem treinado.

Um padrão de design comum para uma solução de reconhecimento de linguagem natural é semelhante ao seguinte:

![Diagram showing an app accepts natural language input, and uses a model to determine semantic meaning before taking the appropriate action.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/build-language-understanding-model/media/language-understanding-app.png)

Neste padrão de design:

1. Um aplicativo aceita a entrada de linguagem natural de um usuário.
2. Um modelo de linguagem é usado para determinar o significado semântico (_intenção_ do usuário).
3. O aplicativo realiza uma ação apropriada.

A **Linguagem de IA do Azure** permite que os desenvolvedores criem aplicativos com base em modelos de linguagem que podem ser treinados com um número relativamente pequeno de amostras para distinguir o significado pretendido de um usuário.

Neste módulo, você aprenderá a usar o serviço para criar um aplicativo de reconhecimento de linguagem natural usando a Linguagem de IA do Azure.

Depois de concluir este módulo, você poderá:

- Provisionar um recurso de Linguagem de IA do Azure.
- Definir intenções, entidades e enunciados.
- Usar padrões para diferenciar enunciados semelhantes.
- Usar componentes de entidade predefinidos.
- Treinar, testar, publicar e revisar um modelo.