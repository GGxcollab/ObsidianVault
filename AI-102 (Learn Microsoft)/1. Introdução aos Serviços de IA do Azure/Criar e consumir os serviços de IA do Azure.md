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