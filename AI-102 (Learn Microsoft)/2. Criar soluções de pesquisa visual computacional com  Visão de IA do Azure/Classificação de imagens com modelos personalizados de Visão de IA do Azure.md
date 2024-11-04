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
# Criar um projeto pe