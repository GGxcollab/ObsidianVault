# Introdução
- Os **serviços de IA do Azure** são serviços baseados em nuvem que encapsulam recursos de IA. Em vez de um único produto, você deve pensar nos serviços de IA do Azure como um conjunto de serviços individuais que você pode usar como componentes básicos para compor aplicativos sofisticados e inteligentes.
- Os serviços de IA incluem uma ampla gama de serviços individuais em linguagem, fala, visão, IA generativa e muito mais. Você pode usar os serviços de IA para criar suas próprias soluções de IA e fornecer soluções prontas para uso nos cenários mais comuns de IA. Alguns exemplos de serviços individuais de IA do Azure incluem:
	- **Visão de IA do Azure** – Analise conteúdo em imagens e vídeos.
	- **Linguagem de IA do Azure** – Crie aplicativos com recursos de compreensão de linguagem natural líderes do setor.
	- **Fala de IA do Azure** – Conversão de fala em texto, conversão de texto em fala, tradução e reconhecimento de locutor.
	- **IA do Azure para Informação de Documentos**: uma solução de reconhecimento óptico de caracteres (OCR) que pode extrair um significado semântico de formulários, como faturas, recibos e outros.
	- **Pesquisa de IA do Azure** – Uma solução de pesquisa em escala de nuvem que usa serviços de IA para extrair insights de dados e documentos.
	- **OpenAI do Azure** – Um serviço de IA do Azure que fornece acesso aos recursos do OpenAI GPT-4.
- Embora os detalhes de cada serviço de IA do Azure possam variar, a abordagem para provisioná-los e consumi-los costuma ser a mesma.
 - **Observação**
	- Você pode encontrar uma lista completa dos serviços de IA do Azure na [documentação](https://learn.microsoft.com/pt-br/azure/ai-services/what-are-ai-services#available-azure-ai-services).
- Neste módulo, você vai aprender a:
	- Criar recursos dos serviços de IA do Azure em uma assinatura do Azure.
	- Identificar pontos de extremidade, chaves e locais necessários para consumir um recurso dos Serviços de IA do Azure.
	- Utilizar uma API REST para consumir um serviço de IA do Azure.
	- Utilizar um SDK para consumir um serviço de IA do Azure.
# Provisionar um recurso dos Serviços de IA do Azure
- Os serviços de IA do Azure incluem uma ampla gama de recursos de IA que você pode usar nos seus aplicativos. Para usar qualquer um dos serviços de IA, você precisa criar recursos apropriados em uma assinatura do Azure para definir um ponto de extremidade no qual o serviço possa ser consumido, fornecer chaves de acesso para acesso autenticado e gerenciar a cobrança para o uso do serviço pelo aplicativo.
### Opções para recursos do Azure
- Para muitos dos serviços de IA do Azure disponíveis, você pode escolher entre as seguintes opções de provisionamento:
### Recurso de vários serviços
- Você pode provisionar um recurso dos **serviços de IA** que dá suporte a vários serviços de IA diferentes. Por exemplo, você pode criar um único recurso que permita usar a **Linguagem de IA do Azure**, a **Visão de IA do Azure** e a **Fala de IA do Azure**, entre outros serviços.
- Essa abordagem permite que você gerencie um único conjunto de credenciais de acesso para consumir vários serviços em um único ponto de extremidade e com um único ponto de cobrança para uso de todos os serviços.
### Recurso de serviço único
- Cada serviço de IA pode ser provisionado individualmente, por exemplo, criando uma **Linguagem de IA** discreta e recursos de **Visão de IA** em sua assinatura do Azure.
- Essa abordagem permite que você use pontos de extremidade separados para cada serviço (por exemplo, para provisioná-los em diferentes regiões geográficas) e para gerenciar credenciais de acesso para cada serviço de forma independente. Ele também permite que você gerencie a cobrança separadamente para cada serviço.
- Os recursos de serviço único geralmente oferecem uma camada gratuita (com restrições de uso), tornando-os uma boa opção para experimentar um serviço antes de usá-lo em um aplicativo de produção.
### Recursos de treinamento e previsão
- Embora a maioria dos serviços de IA possam ser usados por meio de um único recurso do Azure, alguns oferecem (ou requerem) recursos separados para o _treinamento_ e a _previsão_ do modelo. Isso permite que você gerencie a cobrança do treinamento de modelos personalizados e o consumo do modelo por aplicativos separadamente e, na maioria dos casos, permite que você use um recurso dedicado específico para cada serviço para treinar um modelo, mas um recurso de **serviços de IA** genérico para disponibilizar o modelo para os aplicativos para fins de inferência
# Identificar pontos de extremidade e chaves
- Ao provisionar um recurso dos serviços de IA do Azure na sua assinatura do Azure, você estará definindo um ponto de extremidade por meio do qual o serviço poderá ser consumido por um aplicativo.
- Para consumir o serviço por meio do ponto de extremidade, os aplicativos exigem as seguintes informações:
	- **O URI do ponto de extremidade**. Esse é o endereço HTTP no qual a interface REST do serviço pode ser acessada. A maioria dos kits de desenvolvimento de software (SDKs) dos serviços de IA usam o URI do ponto de extremidade para iniciar uma conexão com o ponto de extremidade.
	- **Uma chave de assinatura**. O acesso ao ponto de extremidade é restrito com base em uma chave de assinatura. Os aplicativos cliente devem fornecer uma chave válida para consumir o serviço. Quando você provisiona um recurso de serviços de IA, são criadas duas chaves, e os aplicativos podem utilizar qualquer uma delas. Você também pode regenerar as chaves conforme necessário para controlar o acesso ao recurso.
	- **A localização do recurso**. Ao provisionar um recurso no Azure, você geralmente o atribui a um local, que determina o data center do Azure no qual o recurso é definido. Embora a maioria dos SDKs use o URI do ponto de extremidade para se conectar ao serviço, alguns exigem o local.
# Usar a API REST
- Os serviços de IA do Azure fornecem interfaces de programação de aplicativo (APIs) REST que os aplicativos de cliente podem usar para consumir serviços. Na maioria dos casos, as funções de serviço podem ser chamadas por meio do envio de dados no formato JSON em uma solicitação HTTP, que pode ser uma solicitação POST, PUT ou GET, dependendo da função específica que está sendo chamada. Os resultados da função são retornados ao cliente como uma resposta HTTP, geralmente com conteúdo JSON que encapsula os dados de saída da função.

![Diagram of an app submitting a JSON request to an Azure AI services REST API and receiving a JSON response.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-manage-ai-services/media/rest-api.png)

- O uso de interfaces REST com um ponto de extremidade HTTP significa que qualquer linguagem de programação ou ferramenta capaz de enviar e receber JSON sobre HTTP pode ser usada para consumir serviços de IA. Você pode usar linguagens de programação comuns, como Microsoft C#, Python e JavaScript, além de utilitários como Postman e cURL, que podem ser úteis para o teste.
# Usar um SDK
- Você pode desenvolver um aplicativo que utilize os serviços de IA do Azure usando interfaces REST, mas é mais fácil criar soluções mais complexas usando bibliotecas nativas para a linguagem de programação na qual você está desenvolvendo o aplicativo.

![A diagram of an app submitting a call to an Azure AI services resource through a language-specific SDK, which abstracts the JSON request and response.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/create-manage-ai-services/media/sdk.png)

- Os kits de desenvolvimento de software (SDKs) para linguagens de programação comuns abstraem as interfaces REST para a maioria dos serviços de IA do Azure. A disponibilidade do SDK varia com os serviços individuais de IA, mas, para a maioria dos serviços, existe um SDK para linguagens como:
	- Microsoft C# (.NET Core)
	- Python
	- JavaScript (Node.js)
	- Go
	- Java
- Cada SDK inclui pacotes que você pode instalar para usar bibliotecas específicas do serviço em seu código e documentação online para ajudá-lo a determinar as classes, métodos e parâmetros apropriados usados para trabalhar com o serviço.
![[Pasted image 20241030135255.png]]