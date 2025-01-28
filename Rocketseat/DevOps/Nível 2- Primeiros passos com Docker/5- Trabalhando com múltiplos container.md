# Um breve Overview

[Commit: Um breve Overview](https://github.com/rocketseat-education/devops-docker-containers/commit/f09438a1e6dfa9cd2f669c86fa511ffa45e1cd2d)

- Nesta aula, abordamos a orquestração de containers, explicando como executar múltiplos containers localmente e conectar uma aplicação a um banco de dados MySQL. Demonstramos como buscar e rodar uma imagem MySQL específica, passando variáveis de ambiente essenciais. Também discutimos a complexidade de gerenciar vários containers e a importância de definir nomes para eles. Por fim, testamos a conexão da aplicação com o banco de dados dentro e fora do container.
- Como criar o container do MySQL:
- ![[Pasted image 20250128171441.png]]

# Rodando múltiplos containers

[Commit: Rodando múltiplos containers](https://github.com/rocketseat-education/devops-docker-containers/commit/e8c4800d6656d2a8a976a25299882886377517f4)

- Nesta aula, abordamos a conexão entre containers, destacando a importância de definir nomes para facilitar a comunicação entre eles. Foi discutido um erro de conexão com o banco de dados MySQL e a necessidade de ajustar a configuração da aplicação para se conectar corretamente. Também foi mencionada a importância de garantir que o MySQL esteja rodando antes da aplicação para evitar problemas de inicialização. Por fim, foi mencionada a complexidade de gerenciar múltiplos containers e a promessa de explorar um componente para facilitar a escalabilidade na próxima aula.

# Declarando múltiplos containers

[Commit: Declarando múltiplos containers](https://github.com/rocketseat-education/devops-docker-containers/commit/6529311b0ec28cddbd2bda8314df5796a144fac5)

- Nesta aula, abordamos a orquestração de containers com Docker Compose. Exploramos a estrutura básica do Docker Compose, como definir serviços, imagens e portas. A importância de redes e volumes, além da identação correta no arquivo .yml. Demonstramos como executar o Docker Compose e resolver problemas com variáveis de ambiente. Finalizamos com a execução e gerenciamento de containers. Na próxima aula, continuaremos a configurar serviços, redes e volumes.
- ![[Pasted image 20250128173802.png]]

# Comunicação entre containers

[Commit: Comunicação entre containers](https://github.com/rocketseat-education/devops-docker-containers/commit/a284ab8b9564f034123c746531bee345c95fac97)

- Nesta aula, aprendemos a configurar uma API para rodar com Docker Compose. Exploramos como definir o serviço da API, utilizando o build em vez de apenas a imagem, e configurar as portas. Também vimos como lidar com dependências entre serviços, como o MySQL, para evitar problemas de inicialização. Além disso, abordamos a criação de redes personalizadas e a importância de nomear os containers adequadamente. Ao final, destacamos a utilidade do comando `docker-compose logs` e a preparação para trabalhar com volumes.
- ![[Pasted image 20250128175317.png]]

# Armazenamento de volumes

[Commit: Armazenamento de volumes](https://github.com/rocketseat-education/devops-docker-containers/commit/f54e788185f356092e5caf785c03728cbf8bed0c)

- Nesta aula, expliquei como os volumes funcionam no contexto de containers Docker. Destaquei a importância de usar volumes para persistir dados, especialmente em bancos de dados como o MySQL. Mostrei como declarar um volume no Docker Compose e como verificar sua configuração com comandos como docker ps e docker container inspect. Encerrei ressaltando a importância de fixar conceitos básicos de containers para avançar para tópicos como CI/CD e orquestração com Kubernetes.
- ![[Pasted image 20250128181331.png]]

## Quiz
![[Pasted image 20250128181140.png]]
![[Pasted image 20250128181209.png]]