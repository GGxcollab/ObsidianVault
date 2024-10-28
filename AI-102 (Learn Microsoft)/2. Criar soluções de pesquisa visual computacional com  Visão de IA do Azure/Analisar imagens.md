# Introdução
- A Visão de IA do Azure é uma ramificação da inteligência artificial (IA) em que o software interpreta a entrada visual, geralmente de imagens ou feeds de vídeo.
- Neste módulo, você aprendeu como usar o serviço de **Visão de IA do Azure** para extrair informações de imagens.
- Depois de concluir este módulo, você poderá:
	- Provisionar um recurso da Visão de IA do Azure.
	- Analise uma imagem.
	- Gere uma miniatura recortada inteligente.
# Provisionar um recurso da Visão de IA do Azure
- A **Visão de IA do Azure** é projetada para ajudá-lo a extrair informações de imagens. Ele fornece a funcionalidade que você pode usar para:
	- _Geração de marca e descrição_ – determinando uma legenda apropriada para uma imagem e identificando “marcas” relevantes que podem ser usadas como palavras-chave para indicar seu assunto.
	- _Detecção de objetos_ – detectando a presença e o local de objetos específicos dentro da imagem.
	- _Detecção facial_ – detectando a presença, a localização e os recursos de rostos humanos na imagem.
	- _Metadados de imagem, cor e análise de tipo_ – determinando o formato e o tamanho de uma imagem, sua paleta de cores dominante e se ela contém clip art.
	- _Identificação de categoria_ – identificando uma categorização apropriada para a imagem e se ela contém pontos de referência conhecidos.
	- _Remoção de segundo plano_ – detecta o segundo plano em uma imagem e produz a imagem com o segundo plano transparente ou uma imagem alfa fosca em escala de cinza.
	- _Classificação de moderação_ – determine se a imagem inclui qualquer conteúdo adulto ou violento.
	- _Reconhecimento óptico de caracteres_ – leitura de texto na imagem.
	- _Geração de miniatura inteligente_ – identificando a região principal de interesse na imagem para criar uma versão menor de “miniatura”.
	- ![[Pasted image 20241028155921.png]]
- Você pode provisionar a **Visão de IA do Azure** como um recurso de serviço único ou usar a API de Visão de IA do Azure em um recurso dos **Serviços de IA do Azure** de vários serviços.
# Analisar uma imagem
- Para analisar uma imagem, você pode usar o método REST **Analisar Imagem** ou o método equivalente no SDK para sua linguagem de programação preferida, especificando os recursos visuais que você deseja incluir na análise (e se você selecionar categorias, incluir ou não detalhes de celebridades ou pontos de referência). Esse método retorna um documento JSON que contém as informações solicitadas.
- Observação:
	- A detecção de celebridades exigirá que seja aprovada por meio de uma [política de Acesso Limitado](https://aka.ms/cog-services-limited-access). Leia mais sobre a [adição de dessa política](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/) ao nosso padrão de IA Responsável. O reconhecimento de celebridades é visto em algumas capturas de tela, no entanto, não está incluído no laboratório.
- Python

```
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential

client = ImageAnalysisClient(
    endpoint=os.environ["ENDPOINT"],
    credential=AzureKeyCredential(os.environ["KEY"])
)

result = client.analyze(
    image_url="<url>",
    visual_features=[VisualFeatures.CAPTION, VisualFeatures.READ],
    gender_neutral_caption=True,
    language="en",
)
```

- Os recursos visuais disponíveis estão contidos na enumeração `VisualFeatures`:

	- VisualFeatures.TAGS: Identifica marcas sobre a imagem, incluindo objetos, cenário, configuração e ações
	- VisualFeatures.OBJECTS: Retorna a caixa delimitadora para cada objeto detectado
	- VisualFeatures.CAPTION: Gera uma legenda da imagem em linguagem natural
	- VisualFeatures.DENSE_CAPTIONS: Gera legendas mais detalhadas para os objetos detectados
	- VisualFeatures.PEOPLE: Retorna a caixa delimitadora para pessoas detectadas
	- VisualFeatures.SMART_CROPS: Retorna a caixa delimitadora da taxa de proporção especificada para a área de interesse
	- VisualFeatures.READ: Extrai texto legível

- Especificar os recursos visuais que você deseja analisar na imagem determina quais informações a resposta conterá. A maioria das respostas conterá uma caixa delimitadora (se um local na imagem for razoável) ou uma pontuação de confiança (para recursos como marcas ou legendas).

- A resposta JSON para análise de imagem é semelhante a este exemplo, dependendo dos recursos solicitados:

- JSON

```
{
  "apim-request-id": "abcde-1234-5678-9012-f1g2h3i4j5k6",
  "modelVersion": "<version>",
  "denseCaptionsResult": {
    "values": [
      {
        "text": "a house in the woods",
        "confidence": 0.7055229544639587,
        "boundingBox": {
          "x": 0,
          "y": 0,
          "w": 640,
          "h": 640
        }
      },
      {
        "text": "a trailer with a door and windows",
        "confidence": 0.6675070524215698,
        "boundingBox": {
          "x": 214,
          "y": 434,
          "w": 154,
          "h": 108
        }
      }
    ]
  },
  "metadata": {
    "width": 640,
    "height": 640
  }
}
```