# Introdução
- SQL Injection é onde um atacante insere código SQL malicioso em campos de entrada.

## Como detectar vulnerabilidades de injeção de SQL: 

Você pode detectar injeções de SQL manualmente usando um conjunto sistemático de testes em cada ponto de entrada do aplicativo. Para isso, você normalmente submeteria:

- o caractere de aspas simples `'` e procuraria por erros ou outras anomalias;
- Alguma sintaxe específica de SQL que avalia o valor base (original) do ponto de entrada e um valor diferente, procurando por diferenças sistemáticas nas respostas do aplicativo;
- Condições booleanas como `OR 1=1` e `OR 1=2`, procurando por diferenças nas respostas do aplicativo;
- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
- OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions. 