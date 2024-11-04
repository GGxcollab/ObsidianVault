# Introdução
- Os contêineres possibilitam hospedar serviços de IA do Azure localmente ou no Azure. Por exemplo, se o seu aplicativo usa dados confidenciais em um SQL Server local para chamar um serviço dos serviços de IA do Azure, você pode implantar os serviços de IA do Azure em contêineres na mesma rede. Agora, seus dados podem permanecer em sua rede local, sem que sejam transmitidos para a nuvem. A implantação dos serviços de IA do Azure em um contêiner local também diminuirá a latência entre o serviço e os dados locais, o que pode aprimorar o desempenho.
- Neste módulo, você aprenderá a:
	- Crie contêineres para reutilização.
	- Implante em um contêiner e proteja um contêiner.
	- Consuma serviços de IA do Azure a partir de um contêiner.

# Entender contêineres
- Quando você implanta um serviço de software, ele deve ser hospedado em um ambiente que forneça o hardware, o sistema operacional e os componentes de runtime de suporte dos quais o serviço depende.
- Os serviços de IA do Azure são fornecidos como um serviço de nuvem, no qual o software do serviço é hospedado em um data center do Azure que fornece os serviços de runtime, sistema operacional e hardware subjacentes. No entanto, você também pode implantar alguns serviços de IA do Azure em um _contêiner_, que encapsula os componentes de runtime necessários e que, por sua vez, são implantados em um host de contêiner que fornece o sistema operacional e hardware subjacentes.

![Diagram of a container host with 4 containers](https://learn.microsoft.com/pt-br/training/wwl-data-ai/investigate-container-for-use-with-ai-services/media/containers.png)

## O que é um contêiner?
- Um contêiner consiste em um aplicativo ou serviço e nos componentes de runtime necessários para executá-lo, ao mesmo tempo que abstrai o sistema operacional subjacente e o hardware. Na prática, essa abstração resulta em dois benefícios significativos:

	- Os contêineres são portáveis entre hosts, que podem estar executando sistemas operacionais diferentes ou usar hardware diferente – tornando mais fácil mover um aplicativo e todas as suas dependências.
	- Um único host de contêiner pode dar suporte a vários contêineres isolados, cada um com sua própria configuração de runtime específica – facilitando a consolidação de vários aplicativos com diferentes requisitos de configuração.

- Um contêiner é encapsulado em uma _imagem de contêiner_ que define o software e a configuração a que ele deve dar suporte. As imagens podem ser armazenadas em um registro central, como o _Docker Hub_, ou você pode manter um conjunto de imagens em seu próprio registro.
## Implantação de contêiner
- Para usar um contêiner, você normalmente extrai a imagem de contêiner de um registro e a implanta em um host do contêiner, especificando quaisquer definições de configuração necessárias. O host do contêiner pode estar na nuvem, em uma rede privada ou em seu computador local. Por exemplo:
	- Um servidor do _Docker_*.
	- Uma ACI (Instância de Contêiner do Azure).
	- Um cluster do AKS (Serviço de Kubernetes do Azure).

*_Docker é uma solução de software livre para desenvolvimento e gerenciamento de contêineres que inclui um mecanismo de servidor que pode ser usado para hospedar contêineres. Há versões do servidor Docker para sistemas operacionais comuns, incluindo Microsoft Windows e Linux._

>[!NOTE]Dica
>Para saber mais sobre contêineres, confira o módulo [Introdução aos contêineres do Docker](https://learn.microsoft.com/pt-br/training/modules/intro-to-docker-containers/) no Microsoft Learn.