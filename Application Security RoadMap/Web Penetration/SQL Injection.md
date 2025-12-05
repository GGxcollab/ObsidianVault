# What is SQL injection (SQLi)?

- A injeção de SQL (SQLi) é uma vulnerabilidade de segurança web que permite a um atacante interferir nas consultas que uma aplicação faz ao seu banco de dados. Isso pode permitir que um atacante visualize dados que normalmente não conseguiria recuperar. Esses dados podem incluir informações pertencentes a outros usuários ou quaisquer outros dados aos quais a aplicação tenha acesso. Em muitos casos, um atacante pode modificar ou excluir esses dados, causando alterações permanentes no conteúdo ou comportamento da aplicação.
- Em algumas situações, um atacante pode escalar um ataque de injeção de SQL para comprometer o servidor subjacente ou outra infraestrutura de back-end. Isso também pode permitir a realização de ataques de negação de serviço (DoS).

## Como detectar vulnerabilidades de injeção de SQL: 

Você pode detectar injeções de SQL manualmente usando um conjunto sistemático de testes em cada ponto de entrada do aplicativo. Para isso, você normalmente submeteria:

- o caractere de aspas simples `'` e procuraria por erros ou outras anomalias;
- Alguma sintaxe específica de SQL que avalia o valor base (original) do ponto de entrada e um valor diferente, procurando por diferenças sistemáticas nas respostas do aplicativo;
- Condições booleanas como `OR 1=1` e `OR 1=2`, procurando por diferenças nas respostas do aplicativo;
- Payloads projetados para acionar atrasos quando executados em uma consulta SQL, procurando por diferenças no tempo de resposta;
- Payloads OAST projetados para acionar uma interação de rede fora da banda quando executados em uma consulta SQL, monitorando quaisquer interações resultantes.