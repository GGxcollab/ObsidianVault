# Introdução
- SQL Injection é onde um atacante insere código SQL malicioso em campos de entrada.

## Como detectar vulnerabilidades de injeção de SQL: 

Você pode detectar injeções de SQL manualmente usando um conjunto sistemático de testes em cada ponto de entrada do aplicativo. Para isso, você normalmente submeteria:

- o caractere de aspas simples `'` e procuraria por erros ou outras anomalias;
- Alguma sintaxe específica de SQL que avalia o valor base (original) do ponto de entrada e um valor diferente, procurando por diferenças sistemáticas nas respostas do aplicativo;
- Condições booleanas como `OR 1=1` e `OR 1=2`, procurando por diferenças nas respostas do aplicativo;
- Payloads projetados para acionar atrasos quando executados em uma consulta SQL, procurando por diferenças no tempo de resposta;
- Payloads OAST projetados para acionar uma interação de rede fora da banda quando executados em uma consulta SQL, monitorando quaisquer interações resultantes.