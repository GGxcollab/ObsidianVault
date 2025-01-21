
# Containers, Docker e LXC -  Aula 01
## O que é um Container?
- **Ambiente isolado**
	- você tem a sua aplicação, imaginando aqui bem por alto, e a sua aplicação, ela precisa de alguns recursos para conseguir funcionar. Ela vai precisar, por exemplo, de um recurso computacional, CPU e memória RAM, e ela também vai precisar de recursos, digamos que tecnológicos. Então, por exemplo, a sua aplicação ela roda em Node, por exemplo. Então você precisaria ter um ambiente com o Node configurado, mais ou menos como você vai rodar na sua máquina. Você não precisa instalar ali o Node, instalar o npm e tudo mais, para fazer a gestão de nips e tudo mais.
	- Container, a ideia é que eu vou criar um ambiente que é isolado do seu sistema operacional, e dentro desse ambiente você tem todos os recursos que a sua aplicação precisa para funcionar.
- **Compartilha um host de controle**
	- Cada aplicação que voce tiver, necessariamente falando é um Container
	- Exemplo famoso navio cargueiro. O navio cargueiro, ele carrega ali vários containers, então vamos imaginar o navio cargueiro como um host, certo? Um host de controle. Ele está lá com os vários containers, em alto mar, ambiente de produção, tendo problemas, tendo ondas e tudo mais, aí um container caiu. Caiu ali do nosso host de controle. Isso não afetou o navio cargueiro, ele continuou indo com os containers restantes, digamos assim.
- **Contém todos os elementos necessários para rodar uma aplicação**
- **LXC**
	- "Linux Containers": é um recurso nativo de containers para conseguir rodar container nativos no Linux
	- Segue os mesmos principios a plataforma de container, ou seja, é opensource, fornece um conjunto de modelos, ferramentas, libs, e tudo mais para conseguir isolar as aplicações.
## E as Máquinas Virtuais?
- **Tudo roda na mesma maquina**
	- ou seja, se o servidor parar de funcionar, todas as minhas operações são paralisadas
	- O container ja não é a ideias, pois tem ambientes isolados, cada um com seu próprio ambiente de execução de forma isolada do SO (Sistema Operacional)
	- MV é medida em gigabytes, ja o container é em megabytes
	- ![[Pasted image 20250120231508.png]]
- Possui seu próprio SO.
## Docker
- **Surgiu há cerca de 15 anos.**
- **Interface para lidar com containers**
- **Utiliza o kernel do Linux**
- **Baseado em imagem**
	- Facilita a portabilidade
	- é basicamente voce tem sua aplicação la com os recursos que ela precisa, e voce cria um arquivo declarativo com aqueles recursos que a aplicação necessita. E, a partir dai, voce vai buildar, isso gera uma imagem, e essa imagem que você vai, de fato, executar
- **Facilita o ciclo de entrega**


# Princípios de Isolamento - Aula 02
## Isolamento
- **Como funciona?**
	- CGroup
		- é uma funcionalidade que possibilita o controle e a limitação de recursos de um processo. Ele fica no kernel do Linux. E basicamente, ele é utilizado aqui pra impor limites de CPU, memória, input, output e alguns outros recursos ali também do container.
	- Namespace
		- basicamente é isolamento de recurso
		- sistema de arquivos, processos e até mesmo rede.
		- Então, basicamente falando, um container, ele só enxerga os seus próprios processos, os seus próprios sistemas de arquivos e também as suas próprias interfaces de rede
	- Unshare
		- basicamente ele visa criar um novo namespace para um processo já existente, digamos assim, e a ideia é possibilitar a execução de processos em um ambiente isolado, sem a necessidade de uma interface de container. 
		- Então caso você não esteja trabalhando, por exemplo, com o Docker, o UnShare permite que você faça essa criação na mão. Então você conseguiria criar esse namespace com o próprio UnShare

# Open Container Initiative (OCI) - Aula 03
## O que é a OCI?
- Estrutura de governança
- Visa facilitar a interoperabilidade
- Garante padrões mantendo a flexibilidade
	- Então, o grande ponto aqui é que você consiga ter os containers trabalhando de forma que todos sigam as mesmas interfaces para os formatos, principalmente falando sobre imagem e container