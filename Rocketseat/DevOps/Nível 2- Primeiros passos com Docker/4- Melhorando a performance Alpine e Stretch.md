# Alpine e Stretch

- Nesta aula, abordamos a otimização de containers, destacando a importância de reduzir o tamanho das imagens para melhorar a performance. Introduzimos o Alpine, uma distribuição Linux enxuta e otimizada para containers. Comparamos diferentes versões do Node, mostrando a redução significativa de tamanho e vulnerabilidades ao utilizar o Alpine em vez do Debian. Exploramos também outras versões do Debian, como Stretch, Buster e Jessie. Na próxima aula, faremos a transição para o Alpine para otimizar ainda mais nossos containers.

# Adicionando o Alpine na nossa imagem

[Commit: Adicionando o Alpine na nossa imagem](https://github.com/rocketseat-education/devops-docker-containers/commit/f54fb9b11c870f8120dd70c29e420c727ed08201)

- Nesta aula, foi abordado o processo de configuração de uma aplicação com Alpine, uma imagem leve do Docker. Foi destacada a importância de seguir a lógica de nomenclatura ao trabalhar com diferentes tecnologias. Foi demonstrado como realizar o build da imagem Docker, aproveitando o mecanismo de cache para economizar tempo. Ao trocar a base image para Alpine, houve uma redução significativa no tamanho da imagem, mostrando a eficiência dessa prática. O próximo passo será abordar estágios múltiplos para otimização.
- ![[Pasted image 20250128153526.png]]
- ![[Pasted image 20250128153612.png]]
- ![[Pasted image 20250128153721.png]]

# Criando múltiplos estágios

[Commit: Criando múltiplos estágios](https://github.com/rocketseat-education/devops-docker-containers/commit/2e1bf92194fe5e19c10fd7b979303d52b91f2091)

- Nesta aula, abordo o conceito de multi-stage building para otimização de containers. Explico como dividir o processo de build em diferentes estágios, evitando incluir itens desnecessários na imagem final. Demonstro na prática como utilizar aliases e copiar arquivos entre estágios, resultando em uma imagem mais leve e otimizada. Ao final, realizo um docker build para mostrar a redução do tamanho da imagem com o multi-stage build.
-  os primeiros "COPY" é da interface para o container, o ultimo é de um estagio para o outro
- ![[Pasted image 20250128155213.png]]

# Comparando imagens

[Commit: Comparando imagens](https://github.com/rocketseat-education/devops-docker-containers/commit/6e3c5569760019e86b1d605ca59cf37c34e31840)

- Nesta aula, otimizamos uma imagem Docker, reduzindo seu tamanho de 1GB para 210MB. Realizamos ajustes, removendo bibliotecas desnecessárias e executando comandos como `workspaces focus --production` e `yarn-cache-clean`. Enfrentamos um erro ao rodar o `yarn run-bind` devido à dependência dev. Corrigimos isso executando o `yarn` antes do build. Testamos a imagem Docker e verificamos os arquivos dentro do container. Encerramos a otimização e nos preparamos para falar sobre orquestração de containers em ambiente local.

# Ultimas correções no Dockerfile

[Commit: Ultimas correções no Dockerfile](https://github.com/rocketseat-education/devops-docker-containers/commit/da8347aa2e46f5592b498ba42688d18af7fd8bd8)

- Nesta aula, são feitas alterações no Dockerfile, como copiar o package.json e ajustar o comando start para uso em produção. Após as modificações, é feita a build e execução do container, sem associar um volume. O instrutor destaca que na próxima aula será abordado o uso de volumes, indicando a importância para bancos de dados. Por fim, menciona que a aplicação deve estar rodando corretamente e convida para a próxima aula sobre orquestração.
- ![[Pasted image 20250128160042.png]]
- agora rebuilda

## Quiz
![[Pasted image 20250128160715.png]]
![[Pasted image 20250128160733.png]]