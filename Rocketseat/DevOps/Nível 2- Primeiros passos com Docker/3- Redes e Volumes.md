# Camada de abstração

- Nesta aula, abordamos a importância da comunicação e redes em containers Docker. Exploramos os conceitos de redes, como o driver bridge, null e roast, e a criação de redes personalizadas. Destacamos a organização de redes por projetos e a utilização de redes específicas para diferentes aplicações. Além disso, discutimos a criação de redes com o comando `docker network create` e a importância das boas práticas, como a utilização de tags para otimização. Na próxima aula, vamos aprofundar o conhecimento em redes e realizar algumas práticas.
- se na criação de um container nao associar a nenhuma rede, será **brigde**, que é basicamente um driver, uma rede padrao para qualquer container e ela vai fornecer uma interface que vai fazer o bridge com o docker zero, lá do roast. Então, basicamente, você vai ter ali um endereço já associado ao seu container e você também vai conseguir fazer comunicação via TCP e IP por default.
-  O grande ponto, a boa prática, na verdade, é que quando você vai trabalhar com containers, principalmente localmente, tem uma questão organizacional, em produção também, vai seguir essa lógica, mas localmente, é legal que você tenha as suas redes de acordo com os seus projetos.
-  **None**, na verdade, que é o NULL, basicamente, até pelo nome, ele vai isolar o nosso container, ok? Caso você tenha em use case um caso de uso de container que não vai ter comunicação externa, por uma questão de segurança, por exemplo, você pode associar uma rede NULL para esse container, beleza? E aí, dentro do container, a única interface de rede disponível vai ser a própria localhost. Qualquer coisa além disso, o seu container não vai enxergar
- **Host** tem ali como objetivo entregar todas as interfaces existentes. Então, quando você coloca Host, o nome Host é por conta do docker host, então todas as interfaces disponíveis no docker host também ficarão ali disponibilizadas, como eu estava dizendo, para o container
- Comando para criar a rede:
	- **docker network create (nome da rede)**
- Comando para listar as redes:
	- **docker network ls**


# Gerenciando redes
- Nesta aula, foi abordado como associar uma rede a um container Docker. Foram apresentadas duas formas de fazer essa associação: utilizando o comando `docker network connect (id network) (id container)` para containers já em execução e definindo a rede no momento da criação do container com o parâmetro `--network`. Foi explicado como verificar a associação da rede ao container utilizando os comandos `docker network inspect` e `docker container inspect`. Também foi mencionado que um container pode estar associado a várias redes.
- Caso voce nao tenha o container, mas ja tenha a network o comando é o seguinte:
	- **docker run --network (nome da rede)**
- ![[Pasted image 20250127162630.png]]
	- ja roda o container com a network, a porta e a tag


# Arquivos e Containers

- Esta aula, aborda a importância dos volumes em containers Docker para manter dados persistentes. Mostra como os arquivos são armazenados no container e como são perdidos ao reconstruir o container. Destaca a necessidade de separar responsabilidades e exemplifica a criação de arquivos dentro do container. Demonstra como os arquivos são perdidos sem volumes persistentes. O instrutor encerra indicando que o próximo vídeo abordará como manter arquivos persistentes em volumes específicos.


# Entendendo sobre volumes

- Nesta aula, abordamos o conceito de volumes no Docker. Volumes são diretórios externos que permitem persistência de dados, essenciais para salvar arquivos e manter dados em containers. A criação e associação de volumes são fundamentais para garantir a persistência de dados entre reinicializações de containers. O comando `docker volume` é utilizado para gerenciar volumes, permitindo a criação, inspeção e remoção de volumes. A associação de volumes com containers é feita através do comando `docker run -v`, garantindo a persistência dos dados.
- ![[Pasted image 20250127174325.png]]
- ![[Pasted image 20250127174337.png]]

# Persistindo informações nos volumes

Nesta aula, abordo a criação de arquivos em containers Docker e a persistência desses arquivos em volumes. Demonstrando como criar, verificar e manter arquivos em containers com volumes associados. Destaco a importância de apontar para o volume ao executar um container para evitar a perda de arquivos. Exploro a continuidade da existência dos volumes mesmo após a exclusão dos arquivos e a possibilidade de restaurar arquivos ao associar um volume novamente. Esses conceitos serão aprofundados nos módulos futuros.

## Quiz
![[Pasted image 20250128151303.png]]
![[Pasted image 20250128151323.png]]