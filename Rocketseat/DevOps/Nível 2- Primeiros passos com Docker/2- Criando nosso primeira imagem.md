# Estrutura de um Dockerfile

[Commit: Estrutura de um Dockerfile](https://github.com/rocketseat-education/devops-docker-containers/commit/0f8c46d5dcadcc8088a2f6a5262be3bc5a7d2557)

- Nesta aula, discutimos a continuação da construção do Dockerfile para executar nossa aplicação. Abordamos instruções como `workdir` para definir o diretório de trabalho, `copy` para copiar arquivos, `run` para executar comandos e `cmd` para iniciar a aplicação. Exploramos a importância de expor portas e a criação de imagens Docker. Também destacamos a necessidade de otimizar o tamanho das imagens geradas. Ao final, preparamos a imagem para rodar o container.
- ![[Pasted image 20250127174102.png]]

## Rodando Nosso Container

Nesta aula, abordei a criação e execução de um container Docker a partir de uma imagem. Expliquei sobre a importância de tags, Image ID, tamanho da imagem e utilização do comando `docker run`. Destaquei a instrução `-rm` para deletar o container ao final do ciclo de vida, mapeamento de portas com `-p`, e a visualização de containers em execução com `docker ps`. Também mencionei a execução em background com `-d` e a visualização de logs com `docker logs`. Finalizei ressaltando a importância das boas práticas na criação de containers.

# Melhorias e Otimizações na Nossa Imagem

[Commit: Melhorias e Otimizações na Nossa Imagem](https://github.com/rocketseat-education/devops-docker-containers/commit/7e635ed090972147fc5f0fa6c8663dbf052e89c7)

Nesta aula, vamos abordar boas práticas para melhorar a performance e economizar espaço em uma build Docker. Explico a importância de copiar o Yarn.loc, adicionar o yarnrc.yml e ignorar pastas como NodeModules e dist. Demonstro como utilizar o docker ignore e a tag correta ao construir imagens Docker. Ao final, destaco a necessidade de versionamento adequado. Essas práticas contribuem para otimizar builds e manter um histórico de versões eficiente.

## Quiz
![[Pasted image 20250122231618.png]]
![[Pasted image 20250122231637.png]]
![[Pasted image 20250122231653.png]]
