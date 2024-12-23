# O que é e pra que ele é utilizado?
## Flask
- é um framework leve e poderoso para construir aplicações web em Python.
## Framework
- é um conjunto de ferramentas, bibliotecas e convenções que fornecem uma estrutura para desenvolver aplicações.
## Vantagens:
- **Simplicidade**
- **Escalabilidade**
- **Flexibilidade**
## Usos reais
- Pinterest
- Linkedin
- Netflix 
- Uber
## Conceitos básicos API e API Rest
- Nesta aula, vamos falar sobre APIs (Application Programming Interfaces). Vou te mostrar um exemplo simples de comunicação entre duas pessoas para ilustrar o conceito de API. Assim como as pessoas se comunicam, os sistemas também precisam se comunicar. 
- Uma API é uma interface que permite que um sistema se conecte a outro sistema. Por exemplo, um cliente (como um aplicativo) pode enviar uma requisição para uma API, que por sua vez passa essa requisição para o servidor. O servidor processa a requisição e envia uma resposta de volta para a API, que então envia a resposta de volta para o cliente. 
- A API é como uma ponte que permite que diferentes softwares troquem informações e funcionem juntos. Para estabelecer essa comunicação, é necessário seguir um conjunto de regras, como o protocolo HTTP e os métodos GET, POST, PUT, DELETE e PATCH. O REST (Representational State Transfer) é um estilo de arquitetura para o desenvolvimento de APIs que se baseia nos princípios do protocolo HTTP. 
- Quando uma API segue todos os princípios do REST, ela é considerada RESTful. É importante entender esses conceitos para construir APIs eficientes.
- ![[Pasted image 20241220161410.png]]
- ![[Pasted image 20241220161449.png]]
- ![[Pasted image 20241220161722.png]]
## Métodos de Requisição
- **Método de requisição HTTP**
	- O protocolo HTTP define um conjunto de métodos para realizar as requisições 
	- O protocolo HTTP define diferentes métodos para realizar requisições, cada um com uma finalidade específica. Vamos começar com o método GET, que é utilizado para recuperar dados de um recurso específico. Em seguida, temos o método POST, que é usado para inserir informações em um recurso. O método PUT é utilizado para atualizar informações de um recurso, substituindo todas as informações existentes. Já o método PATCH é usado para fazer atual
- **Código de Resposta HTTP** ("developer.mozilla.org")
	- Os códigos de resposta informam o que aconteceu com a requisição. Temos diferentes faixas de números para classificar esses códigos. 
	- Por exemplo, os códigos entre 100 e 199 são informativos, enquanto os códigos entre 200 e 299 indicam que a requisição foi bem-sucedida. Já os códigos entre 300 e 399 são para redirecionamento, e os códigos entre 400 e 499 são para erros do cliente. Os códigos entre 500 e 599 são para erros do servidor. É importante entender esses códigos para interpretar corretamente as respostas das requisições.