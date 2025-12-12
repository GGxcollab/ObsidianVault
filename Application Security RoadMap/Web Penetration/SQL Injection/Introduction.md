# What is SQL injection (SQLi)?

- A injeção de SQL (SQLi) é uma vulnerabilidade de segurança web que permite a um atacante interferir nas consultas que uma aplicação faz ao seu banco de dados. Isso pode permitir que um atacante visualize dados que normalmente não conseguiria recuperar. Esses dados podem incluir informações pertencentes a outros usuários ou quaisquer outros dados aos quais a aplicação tenha acesso. Em muitos casos, um atacante pode modificar ou excluir esses dados, causando alterações permanentes no conteúdo ou comportamento da aplicação.
- Em algumas situações, um atacante pode escalar um ataque de injeção de SQL para comprometer o servidor subjacente ou outra infraestrutura de back-end. Isso também pode permitir a realização de ataques de negação de serviço (DoS).

## Qual o impacto de um ataque de injeção de SQL bem-sucedido?

Um ataque de injeção de SQL bem-sucedido pode resultar em acesso não autorizado a dados confidenciais, tais como:

- Senhas.
- Dados do cartão de crédito.
- Informações pessoais do usuário.

Ataques de injeção de SQL têm sido usados ​​em muitas violações de dados de alto perfil ao longo dos anos. Esses ataques causaram danos à reputação e multas regulatórias. Em alguns casos, um invasor pode obter uma porta dos fundos persistente nos sistemas de uma organização, levando a uma violação de segurança de longo prazo que pode passar despercebida por um longo período.

## SQL injection in different parts of the query

Most SQL injection vulnerabilities occur within the `WHERE` clause of a `SELECT` query. Most experienced testers are familiar with this type of SQL injection.

However, SQL injection vulnerabilities can occur at any location within the query, and within different query types. Some other common locations where SQL injection arises are:

- In `UPDATE` statements, within the updated values or the `WHERE` clause.
- In `INSERT` statements, within the inserted values.
- In `SELECT` statements, within the table or column name.
- In `SELECT` statements, within the `ORDER BY` clause.

## Como detectar vulnerabilidades de injeção de SQL: 

Você pode detectar injeções de SQL manualmente usando um conjunto sistemático de testes em cada ponto de entrada do aplicativo. Para isso, você normalmente submeteria:

- o caractere de aspas simples `'` e procuraria por erros ou outras anomalias;
- Alguma sintaxe específica de SQL que avalia o valor base (original) do ponto de entrada e um valor diferente, procurando por diferenças sistemáticas nas respostas do aplicativo;
- Condições booleanas como `OR 1=1` e `OR 1=2`, procurando por diferenças nas respostas do aplicativo;
- Payloads projetados para acionar atrasos quando executados em uma consulta SQL, procurando por diferenças no tempo de resposta;
- Payloads OAST projetados para acionar uma interação de rede fora da banda quando executados em uma consulta SQL, monitorando quaisquer interações resultantes.

## Injeção de SQL em diferentes partes da consulta

A maioria das vulnerabilidades de injeção de SQL ocorre dentro da `WHERE`cláusula de uma `SELECT`consulta. A maioria dos testadores experientes está familiarizada com esse tipo de injeção de SQL.

No entanto, vulnerabilidades de injeção de SQL podem ocorrer em qualquer local da consulta e em diferentes tipos de consulta. Alguns outros locais comuns onde a injeção de SQL surge são:

- Nas `UPDATE`declarações, dentro dos valores atualizados ou da `WHERE`cláusula.
- Nas `INSERT`declarações, dentro dos valores inseridos.
- Nas `SELECT`declarações, dentro do nome da tabela ou da coluna.
- Nas `SELECT`declarações, dentro da `ORDER BY`cláusula.

## exemplos de injeção de SQL

Existem diversas vulnerabilidades, ataques e técnicas de injeção de SQL que ocorrem em diferentes situações. Alguns exemplos comuns de injeção de SQL incluem:

- [Recuperação de dados ocultos](https://portswigger.net/web-security/sql-injection#retrieving-hidden-data) , onde você pode modificar uma consulta SQL para retornar resultados adicionais.
- [Subverter a lógica da aplicação](https://portswigger.net/web-security/sql-injection#subverting-application-logic) , onde você pode alterar uma consulta para interferir na lógica da aplicação.
- [Ataques UNION](https://portswigger.net/web-security/sql-injection/union-attacks) , nos quais é possível recuperar dados de diferentes tabelas do banco de dados.
- [Injeção SQL cega](https://portswigger.net/web-security/sql-injection/blind) , onde os resultados de uma consulta que você controla não são retornados nas respostas do aplicativo.

## Recuperando dados ocultos

Imagine um aplicativo de compras que exibe produtos em diferentes categorias. Quando o usuário clica na categoria **Presentes** , o navegador solicita a seguinte URL:

`https://insecure-website.com/products?category=Gifts`

Isso faz com que o aplicativo execute uma consulta SQL para recuperar detalhes dos produtos relevantes do banco de dados:

`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

Esta consulta SQL solicita ao banco de dados que retorne:

- todos os detalhes ( `*`)
- da `products`tabela
- onde `category`é`Gifts`
- e `released`é `1`.

A restrição `released = 1`está sendo usada para ocultar produtos que ainda não foram lançados. Podemos presumir que, para produtos não lançados, `released = 0`...

O aplicativo não implementa nenhuma defesa contra ataques de injeção de SQL. Isso significa que um invasor pode construir o seguinte ataque, por exemplo:

`https://insecure-website.com/products?category=Gifts'--`

Isso resulta na seguinte consulta SQL:

`SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1`

É importante notar que `&&` `--`é um indicador de comentário em SQL. Isso significa que o restante da consulta é interpretado como um comentário, removendo-o efetivamente. Neste exemplo, isso significa que a consulta não inclui mais `&&` `AND released = 1`. Como resultado, todos os produtos são exibidos, incluindo aqueles que ainda não foram lançados.

Você pode usar um ataque semelhante para fazer com que o aplicativo exiba todos os produtos de qualquer categoria, incluindo categorias que ele desconhece:

`https://insecure-website.com/products?category=Gifts'+OR+1=1--`

Isso resulta na seguinte consulta SQL:

`SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1`

A consulta modificada retorna todos os itens onde `is` é ` `category`true` `Gifts`, ou ` `1`is` é igual a `true` `1`. Como ` `1=1`is` é sempre verdadeiro, a consulta retorna todos os itens.

#### Aviso

Tenha cuidado ao inserir a condição `OR 1=1`em uma consulta SQL. Mesmo que pareça inofensiva no contexto em que está sendo inserida, é comum que aplicativos usem dados de uma única solicitação em várias consultas diferentes. Se a sua condição atingir uma instrução `UPDATE`OR `DELETE`, por exemplo, isso pode resultar em perda acidental de dados.

