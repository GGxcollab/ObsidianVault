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

>[!NOTE] Dica
>Para saber mais sobre contêineres, confira o módulo [Introdução aos contêineres do Docker](https://learn.microsoft.com/pt-br/training/modules/intro-to-docker-containers/) no Microsoft Learn.

# Usar contêineres dos serviços de IA do Azure
- Há imagens de contêiner para os serviços de IA do Azure no Registro de Contêiner da Microsoft que você pode usar para implantar um serviço em contêineres que encapsula uma API de serviço dos serviços de IA do Azure.
- Para implantar e usar um contêiner de serviços de IA do Azure, as três atividades a seguir devem ocorrer:
	1. A imagem de contêiner para a API dos serviços de IA do Azure específica que você deseja usar é baixada e implantada em um host de contêiner, como um servidor Docker local, uma ACI (Instância de Contêiner do Azure) ou AKS (Serviço de Kubernetes do Azure).
	2. Os aplicativos cliente enviam dados para o ponto de extremidade fornecido pelo serviço em contêineres e recuperam os resultados da mesma forma que fariam de um recurso de nuvem dos serviços de IA do Azure no Azure.
	3. Periodicamente, as métricas de uso do serviço em contêineres são enviadas para um recurso dos serviços de IA do Azure no Azure para calcular a cobrança do serviço.

![A diagram of an Azure AI services container deployed to a container host and consumed by a client application.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/investigate-container-for-use-with-ai-services/media/ai-services-container.png)

- Mesmo ao usar um contêiner, você deve provisionar um recurso dos serviços de IA do Azure no Azure para fins de cobrança. Os aplicativos cliente enviam suas solicitações ao serviço em contêineres, o que significa que dados potencialmente confidenciais não são enviados ao ponto de extremidade dos serviços de IA do Azure no Azure; mas o contêiner deve ser capaz de se conectar ao recurso dos serviços de IA do Azure no Azure periodicamente para enviar métricas de uso para cobrança.

## Imagens de contêiner dos serviços de IA do Azure
- Cada contêiner fornece um subconjunto de funcionalidades dos serviços de IA do Azure. Por exemplo, nem todos os recursos do serviço de Linguagem de IA do Azure estão em um único contêiner. Detecção de idioma, tradução e análise de sentimentos são imagens de contêiner separadas. No entanto, as etapas de configuração são semelhantes para cada contêiner.
### Contêineres de linguagem
- Para o serviço de Linguagem de IA, os principais recursos são mapeados para imagens separadas:

|Recurso|Imagem|
|---|---|
|Extração de Frases-Chave|mcr.microsoft.com/azure-cognitive-services/textanalytics/keyphrase|
|Detecção de Idioma|mcr.microsoft.com/azure-cognitive-services/textanalytics/language|
|Análise de Sentimento|mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment|
|Reconhecimento de entidade nomeada|mcr.microsoft.com/product/azure-cognitive-services/textanalytics/language/about|
|Análise de Texto para integridade|mcr.microsoft.com/product/azure-cognitive-services/textanalytics/healthcare/about|
|Tradutor|mcr.microsoft.com/product/azure-cognitive-services/translator/text-translation/about|
|Resumo|mcr.microsoft.com/azure-cognitive-services/textanalytics/summarization|

>[!NOTE] Observação
>A Análise de Sentimento dá suporte a outros idiomas, substituindo o _en_ na imagem pelo código de idioma correto
### Contêineres de fala

| Recurso                                  | Imagem                                                                                        |
| ---------------------------------------- | --------------------------------------------------------------------------------------------- |
| Conversão de fala em texto               | mcr.microsoft.com/product/azure-cognitive-services/speechservices/speech-to-text/about        |
| Conversão de fala em texto personalizada | mcr.microsoft.com/product/azure-cognitive-services/speechservices/custom-speech-to-text/about |
| Conversão de texto em fala neural        | mcr.microsoft.com/product/azure-cognitive-services/speechservices/neural-text-to-speech/about |
| Detecção de idioma de fala               | mcr.microsoft.com/product/azure-cognitive-services/speechservices/language-detection/about    |
|                                          |                                                                                               |
### Contêineres de visão

|Recurso|Imagem|
|---|---|
|Ler OCR|mcr.microsoft.com/product/azure-cognitive-services/vision/read/about|
|Análise espacial|mcr.microsoft.com/product/azure-cognitive-services/vision/spatial-analysis/about|

- Você pode usar o comando _pull_ do Docker para baixar imagens de contêiner e trabalhar com elas diretamente de seu computador. Alguns dos contêineres estão em um estado de visualização pública "restrita", e é preciso solicitar acesso explicitamente para usá-los. Fora isso, os contêineres estarão disponíveis para qualquer pessoa usar com a implantação dos serviços de IA do Azure.

- Para obter uma lista completa de imagens de contêiner dos serviços de IA do Azure disponíveis atualmente e anotações específicas para cada uma, confira [Marcas de imagem de contêiner dos serviços de IA do Azure e notas de versão](https://learn.microsoft.com/pt-br/azure/ai-services/cognitive-services-container-support#containers-in-azure-ai-services).

## Configuração de contêiner dos serviços de IA do Azure
- Ao implementar uma imagem de contêiner dos serviços de IA do Azure em um host, você deve especificar três configurações.

|Configuração|Descrição|
|---|---|
|ApiKey|Chave do serviço de IA do Azure implantado; usada para cobrança.|
|Cobrança|URI de Ponto de Extremidade do serviço de IA do Azure implantado; usado para cobrança.|
|Eula|Valor **Aceitar** para indicar que você aceita a licença para o contêiner.|
## Consumo dos serviços de IA do Azure a partir de um contêiner
- Depois que o contêiner dos serviços de IA do Azure for implantado, os aplicativos consumirão do ponto de extremidade dos serviços de IA do Azure em contêineres, em vez de consumirem do ponto de extremidade padrão do Azure. O aplicativo cliente deve ser configurado com o ponto de extremidade apropriado para seu contêiner, mas não precisa fornecer uma chave de assinatura para ser autenticado. Você pode implementar sua própria solução de autenticação e aplicar restrições de segurança de rede conforme apropriado para seu cenário de aplicativo específico.