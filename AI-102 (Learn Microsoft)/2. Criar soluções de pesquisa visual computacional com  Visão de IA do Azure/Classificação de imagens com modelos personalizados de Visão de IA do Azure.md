# Introdução
- Com os modelos personalizados na Visão de IA do Azure, você pode treinar um modelo de IA para classificar imagens ou detectar objetos nelas.

- A _Classificação de imagem_ é um problema comum da pesquisa visual computacional que exige que o software analise uma imagem para categorizá-la (ou _classificá-la_). Nesse módulo, você aprenderá como o serviço **Visão de IA do Azure** permite a criação de seus próprios modelos de visão personalizados para classificação de imagens.

- A _detecção de objetos_ é outro problema comum de pesquisa visual computacional que exige que o software identifique a localização de classes específicas de objetos em uma imagem. O processo de criação de um projeto de detecção de objetos é semelhante ao de um projeto de classificação de imagens, envolvendo etapas que vão desde a criação até a rotulagem e treinamento. Este módulo trata dos conceitos e das questões relacionadas à detecção de objetos, mas o exercício prático será focado em classificação.
# Entenda os tipos de modelos personalizados
- Os modelos personalizados da Visão de IA do Azure têm funcionalidades diferentes com base no tipo. Os tipos de modelos personalizados incluem **Classificação de imagem, Detecção de objeto e Reconhecimento de produto**
### Classificação de imagens
- A classificação de imagem é um recurso de pesquisa visual computacional em que um modelo é treinado para prever um rótulo para uma imagem com base no conteúdo de toda a imagem. Normalmente, o rótulo de classe está relacionado ao _assunto_ principal da imagem. No entanto, cada caso de uso pode variar.
- Por exemplo, as imagens a seguir são classificadas com base no tipo de frutas que contêm.

![Diagram with three labeled photographs of fruit, classified as Apple, Banana, and Orange.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/custom-model-ai-vision-image-classification/media/classified-fruit.png)

- Os modelos podem ser treinados para classificação multiclasse (em que há várias classes, mas cada imagem pode pertencer a apenas uma classe) ou classificação multirrótulo (em que uma imagem pode ser associada a vários rótulos).
## Detecção de objetos
- A detecção de objetos é uma forma de pesquisa visual computacional em que um modelo é treinado para detectar a presença e a localização de uma ou mais classes de objetos em uma imagem. Por exemplo, um sistema de finalização de compra habilitado para IA em uma loja de supermercado pode precisar identificar o tipo e a localização dos itens que estão sendo comprados.

![A photograph of fruit with the location and type of fruits detected.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/custom-model-ai-vision-image-classification/media/object-detection.png)

- Há dois componentes na detecção de objeto:
	- O rótulo de classe de cada objeto detectado na imagem. Por exemplo, você pode prever se uma imagem contém uma maçã e duas laranjas.
	- A localização de cada objeto dentro da imagem, indicada como coordenadas de uma caixa delimitadora que inclui o objeto.
## Reconhecimento de produto
- O reconhecimento de produto funciona da mesma forma que a detecção de objeto, mas com maior precisão para rótulos e nomes de marcas. As previsões do reconhecimento de produto têm o rótulo de classe e a localização, permitindo que você saiba onde o produto está na imagem.
# Criar um projeto personalizado
- Para criar um modelo personalizado na Visão de IA do Azure, primeiro é necessário ter um recurso do Serviços de IA do Azure (ou um recurso de Visão de IA do Azure). Depois que o recurso estiver implantado na sua assinatura, você vai precisar montar seu projeto personalizado.
## Componentes de um projeto de Visão personalizada
- O primeiro componente de um projeto personalizado é o _conjunto de dados_. Esse conjunto é a sua coleção de imagens para treinar o modelo, junto com o _arquivo COCO_ que define as informações dos rótulos dessas imagens. Seu conjunto de dados fica armazenado em um contêiner de armazenamento de blobs do Azure, e vamos falar mais sobre o arquivo COCO nesta unidade.

- Depois de definir suas imagens e rótulos de classe, você poderá treinar seu modelo personalizado. Durante o treinamento, você escolhe o tipo de modelo a treinar, qual conjunto de dados usar e seu orçamento para o treinamento (em quantidade de tempo). Quando o treinamento do modelo terminar, você poderá verificar o desempenho e usar o modelo para fazer previsões.

- Na maioria dos casos, você vai seguir estas etapas:

	1. Criar seu contêiner de armazenamento de blobs e carregar apenas as imagens de treinamento.
	2. Criar o conjunto de dados para seu projeto e conectá-lo ao contêiner de armazenamento de blobs. Ao criar seu conjunto de dados, você define o tipo de projeto: classificação de imagem, detecção de objetos ou reconhecimento de produto.
	3. Rotular os dados em seu Projeto de Rotulagem de Dados do Azure Machine Learning, o que gera o arquivo COCO no contêiner de armazenamento de blobs.
	4. Conectar o arquivo COCO concluído das imagens rotuladas ao seu conjunto de dados.
	5. Treinar seu modelo personalizado no conjunto de dados e rótulos criados.
	6. Verificar o desempenho e iterar caso o desempenho treinado não atenda às expectativas.

- Uma vez que o desempenho atender às expectativas, o modelo pode ser utilizado no Vision Studio ou em seu próprio aplicativo.

### Arquivos COCO
- Um arquivo COCO é um arquivo JSON com um formato específico que define:
	- **imagens**: define o local da imagem no armazenamento de blobs, nome, largura, altura e ID.
	- **anotações**: define as classificações (ou objetos), incluindo em qual categoria a imagem está classificada, a área e a caixa delimitadora (se estiver rotulando para detecção de objetos).
	- **categorias**: define a ID da classe de rótulo nomeada.
- Normalmente, os arquivos COCO são criados ao rotular suas imagens de treinamento em um Projeto de Rotulagem de Dados do Azure Machine Learning. Se você está migrando de um projeto antigo de [Visão Personalizada](https://learn.microsoft.com/pt-br/azure/ai-services/computer-vision/how-to/migrate-from-custom-vision), pode usar o script de migração para criar seu arquivo COCO.

- Um arquivo COCO de exemplo é semelhante a:
JSON

```
{
  "images": [
    {
      "id": 1,
      "width": 1024,
      "height": 768,
      "file_name": "abc.jpg",
      "coco_url": "AmlDatastore://fruit/abc.jpg",
      "absolute_url": "https://myBlobStorage.blob.core.windows.net/fruit/abc.jpg",
      "date_captured": "<date>"
    },
    {
      "id": 2,
      "width": 1024,
      "height": 768,
      "file_name": "xyz.jpg",
      "coco_url": "AmlDatastore://fruit/xyz.jpg",
      "absolute_url": "https://myBlobStorage.blob.core.windows.net/fruit/xyz.jpg",
      "date_captured": "<date>"
    },
    <...>
  ],
  "annotations": [
    {
      "id": 1,
      "category_id": 1,
      "image_id": 1,
      "area": 0.0
    },
    {
      "id": 2,
      "category_id": 1,
      "image_id": 2,
      "area": 0.0
    },
    <...>
  ],
  "categories": [
    {
      "id": 1,
      "name": "apple"
    },
    {
      "id": 2,
      "name": "orange"
    },
    {
      "id": 3,
      "name": "banana"
    }
  ]
}
```

- Se você estiver rotulando um conjunto de dados de detecção de objetos, cada anotação no arquivo COCO também contém uma matriz de caixa delimitadora com os valores na matriz sendo _Esquerda_, _Topo_, _Largura_e _Altura_.

JSON 

```
"bbox": [
    0.11803319477782331,
    0.41586723392402375,
    0.7765206955096307,
    0.3483334397217212
]
```

## Criando seu conjunto de dados
- Depois de ter imagens no contêiner de armazenamento de blobs, você poderá criar seu conjunto de dados para treinamento usando a API REST ou usando o Vision Studio. A solicitação REST seria semelhante à chamada REST a seguir:

rest
```
curl -X PUT https://<endpoint>/computervision/datasets/<dataset-name>?api-version=<version>\
  -H "Content-Type: application/json" \
  -H "Ocp-Apim-Subscription-Key: <subscription-key>" \
  --data-ascii "
  {
    'annotationKind':'imageClassification',
    'annotationFileUris':['<URI>']
  }"
```

- Se estiver usando o [Vision Studio](https://portal.vision.cognitive.azure.com/), você navegará até o bloco do modelo personalizado, selecionará seu recurso e criar seu conjunto de dados. A partir daí, você pode abrir ou criar um Projeto de Rotulagem de Dados do Azure Machine Learning ou carregar um arquivo COCO existente. O exercício neste módulo explica como criar seu conjunto de dados dessa forma.

- Usar o Vision Studio permite que você se conecte ao projeto de rotulagem no Azure Machine Learning em vez de especificar o arquivo COCO na solicitação REST. Os demais exemplos desta unidade usam o Vision Studio, mas se preferir o método REST, os exemplos estarão disponíveis nas páginas de documentação.
# Rotular e treinar um modelo personalizado
- Depois de carregar suas imagens para o armazenamento de blob e criar seu conjunto de dados, a próxima etapa é rotular suas imagens e conectar o arquivo COCO resultante. Se você já tiver um arquivo COCO para suas imagens de treinamento, poderá ignorar a etapa de rotulagem.
## Rotulando suas imagens de treinamento
- A rotulagem de suas imagens de treinamento é feita no Estúdio do Azure Machine Learning, usando o Projeto de Rotulagem de Dados. Ter etiquetas completas e precisas para suas imagens de treinamento melhora muito o desempenho do seu modelo treinado. Ao rotular suas imagens, certifique-se de atribuir rótulos com precisão e rotular completamente todas as instâncias de cada classe.

- Em seu conjunto de dados no Vision Studio, crie um novo projeto de Rotulagem de Dados do Azure Machine Learning ou conecte-se a um projeto existente se você tiver criado um no Estúdio do Azure Machine Learning.

![Screenshot of a new dataset in Vision Studio custom model project.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/custom-model-ai-vision-image-classification/media/new-dataset.png)

- Depois que seu projeto for criado, selecionar esse botão o levará ao Azure Machine Learning Studio e abrirá o projeto de rotulagem. Na Rotulagem de Dados do Azure Machine Learning, você pode adicionar categorias para suas imagens ou objetos (como maçã, laranja, banana). Depois de ter categorias, inicie o projeto e vá para a guia de rotulagem. Você precisa rotular 3 a 5 imagens por categoria.

![Screenshot of a labeling fruit in Azure Machine Learning Studio.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/custom-model-ai-vision-image-classification/media/aml-studio-data-labeling-apply-labels.png)

- Há ferramentas com o Azure Machine Learning para ajudar na rotulagem, como a _rotulagem assistida por ML_, que pega alguns rótulos que você fornece para um subconjunto das imagens e tenta rotular as imagens restantes para você. Se estiver usando esses recursos, é importante revisar os rótulos para garantir que eles sejam precisos. Se não forem precisos, o desempenho do modelo treinado diminui.

- Quando a rotulagem for concluída e todas as imagens de treinamento forem classificadas ou rotuladas corretamente, você poderá adicionar seu arquivo COCO ao conjunto de dados diretamente do workspace do Azure Machine Learning.

## Treinar seu modelo
- Com todas as imagens de treinamento rotuladas, o próximo passo é treinar seu modelo. Ao treinar um modelo, selecione o tipo de modelo, especifique o conjunto de dados que deseja usar como dados de treinamento e indique o orçamento de treinamento. O orçamento de treinamento é um limite superior de tempo para execução do treinamento. O tempo real utilizado para o treinamento geralmente é menor do que o orçamento especificado.

- Quando o modelo for treinado, selecioná-lo permite que você visualize o desempenho da execução da avaliação. Se um conjunto de dados de avaliação não for fornecido durante o treinamento do modelo, ele usará a execução de avaliação padrão. A execução de avaliação padrão retira um pequeno conjunto das imagens rotuladas do conjunto de treinamento, usa o modelo treinado para previsões nesse subconjunto e compara as previsões com os rótulos fornecidos.

- Na página do modelo treinado, você pode disparar novas execuções de avaliação em um conjunto diferente de imagens ou experimentar seus próprios testes no Vision Studio selecionando a guia na parte superior da página.