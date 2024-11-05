# Introdução
Detecção, análise e reconhecimento faciais são desafios comuns da visão computacional para sistemas de inteligência artificial. A capacidade de detectar quando uma pessoa está presente, identificar a localização facial de uma pessoa ou reconhecer um indivíduo com base em suas características faciais é uma forma importante dos sistemas de inteligência artificial demonstrarem um comportamento parecido com o humano e criar empatia com os usuários.

Neste módulo, você aprenderá a detectar, analisar e reconhecer rostos usando os Serviços de IA do Azure.

Depois de concluir este módulo, você poderá:

- Identificar as opções de análise de detecção facial.
- Descrever as considerações de análise facial.
- Detectar rostos com o serviço de Visão de IA do Azure.
- Descrever os recursos do serviço de Detecção Facial.
- Saiba mais sobre o reconhecimento do rosto.
# Identificar opções de detecção, análise e identificação faciais
- Há dois serviços de IA do Azure que você pode usar para criar soluções que detectam rostos ou pessoas em imagens.

![The Azure AI Vision and Face services offer facial analysis capabilities](https://learn.microsoft.com/pt-br/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-options.png)

## O serviço de Visão de IA do Azure
- O serviço **Visão de IA do Azure** permite que você detecte pessoas em uma imagem, além de retornar uma caixa delimitadora para a localização delas.

## O serviço de Detecção Facial
- O serviço de **Detecção Facial** oferece recursos de análise facial mais abrangentes do que o serviço de Visão de IA do Azure, incluindo:
	- Detecção facial (com a caixa delimitadora).
	- Análise de recursos faciais abrangente (incluindo pose de cabeça, presença de óculos, manchas, marcas faciais, oclusão e outros).
	- Comparação e verificação faciais.
	- Reconhecimento facial.

>[!NOTE] Importante
>O uso de reconhecimento do rosto, identificação, comparação e verificação exigirá a aprovação por meio de uma [Política de acesso limitado](https://aka.ms/cog-services-limited-access). Leia mais sobre a [adição de dessa política](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/) ao nosso padrão de IA Responsável. O reconhecimento do rosto será abordado no restante deste módulo, mas não estará disponível sem a inscrição para o Acesso Limitado.

# Entender as considerações de análise facial
- Embora todos os aplicativos de inteligência artificial exijam considerações sobre o uso responsável e ético, sistemas que usam dados faciais podem ser particularmente problemáticos.
 - Ao criar uma solução que usa dados faciais, as considerações incluem (mas não se limitam a):
	- **Dados, privacidade e segurança**. Os dados faciais são de identificação pessoal e devem ser considerados confidenciais e particulares. Você deve garantir que dispõe de proteção adequada para dados faciais usados para treinamento e inferência de modelos.
	- **Transparência**. Garanta que os usuários sejam informados sobre como seus dados faciais são usados e quem terá acesso a eles.
	- **Imparcialidade e inclusividade**. Garanta que o seu sistema baseado em reconhecimento facial não possa ser usado de maneira prejudicial às pessoas com base na sua aparência ou para atingi-las injustamente.
# Detectar rostos com o serviço de Visão de IA no Azure
- Para detectar e analisar rostos com o serviço de Visão de IA do Azure, chame a função REST de **Análise de Imagem** (SDK ou o método REST equivalente), especificando **Pessoas** como uma dos recursos visuais a serem retornados.
- Em imagens que contêm uma ou mais pessoas, a resposta inclui detalhes da localização delas na imagem e os atributos da pessoa detectada, desta forma:

JSON
```
{ 
  "modelVersion": "2023-10-01",
  "metadata": {
    "width": 400,
    "height": 600
  },
  "peopleResult": {
    "values": [
      {
        "boundingBox": {
          "x": 0,
          "y": 56,
          "w": 101,
          "h": 189
        },
        "confidence": 0.9474349617958069
      },
      {
        "boundingBox": {
          "x": 402,
          "y": 96,
          "w": 124,
          "h": 156
        },
        "confidence": 0.9310565276194865
      },
    ...
    ]
  }
}
```

Para obter mais informações sobre a detecção facial da Visão de IA do Azure, confira a [Página de conceito de detecção facial](https://learn.microsoft.com/pt-br/azure/ai-services/computer-vision/concept-people-detection)

>[!NOTE] Observação
>A Visão de IA do Azure anteriormente incluía previsão de idade e sexo, no entanto, isso foi removido como uma proteção para uso responsável. Você pode ler mais sobre nossos [Investimentos de IA Responsável aqui](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/).

# Entender os recursos do serviço de Detecção Facial
- O serviço de **Detecção Facial** fornece recursos abrangentes de detecção, análise e reconhecimento faciais.

![The Face service provides a wide range of facial analysis capabilities](https://learn.microsoft.com/pt-br/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-service.png)

- O serviço de Detecção Facial fornece funcionalidade que você pode usar para:
	- _Detecção facial_ – Para cada rosto detectado, os resultados incluem uma ID que identifica o rosto e as coordenadas da caixa delimitadora indicando a localização na imagem.
	- _Análise de atributo facial_ – Você pode retornar uma grande variedade de atributos faciais, entre eles:
	    - Posição da cabeça (orientação de _inclinação_, _rotação_ e _guinada_ no espaço 3D)
	    - Óculos (_sem óculos_, _óculos de leitura_, _óculos de sol_ ou _óculos de natação_)
	    - Desfoque (_baixo_, _médio_ ou _alto_)
	    - Exposição (_subexposição_, _boa exposição_ ou _superexposição_)
	    - Ruído (ruído visual na imagem)
	    - Oclusão (objetos que obscurecem o rosto)
	    - Acessórios (óculos, chapéu, máscara)
	    - QualityForRecognition (_baixo_, _médio_ou _alto_)
	- _Localização do ponto de referência facial_ – Coordenadas para os principais pontos de referência em relação às características faciais (por exemplo, cantos de olho, pupilas, ponta do nariz e assim por diante)
	- _Comparação facial_ – Você pode comparar os rostos em várias imagens em busca de semelhanças (para encontrar indivíduos com características faciais semelhantes) e para verificação (a fim de determinar que um rosto em uma imagem é a mesma pessoa que um rosto em outra imagem)
	- _Reconhecimento do rosto_ – Você pode treinar um modelo com uma coleção de rostos que pertencem a indivíduos específicos e usar o modelo para identificar essas pessoas em novas imagens.
	- _Vivacidade facial_: a vivacidade pode ser usada para determinar se o vídeo de entrada é um fluxo real ou falso para impedir que indivíduos mal intencionados falsifiquem o sistema de reconhecimento.

- Você pode provisionar a **Detecção Facial** como um recurso de serviço único ou pode usar a API de detecção facial em um recurso de **Serviços de IA do Azure** de vários serviços.

- Se desejar usar os recursos de identificação, reconhecimento e verificação da **Detecção Facial**, você precisará se inscrever na [política de Acesso Limitado](https://aka.ms/cog-services-limited-access) e obter aprovação para que esses recursos sejam disponbilizados.
# Comparar rostos detectados e fazer a correspondência deles
- Quando um rosto é detectado pelo serviço de Detecção Facial, uma ID exclusiva é atribuída a ele e retida no recurso do serviço por 24 horas. A ID é um GUID, sem indicação da identidade do indivíduo além das características faciais.

>[!NOTE] Importante
>O uso de reconhecimento do rosto, comparação e verificação exigirá a aprovação por meio de uma [Política de acesso limitado](https://aka.ms/cog-services-limited-access). Leia mais sobre a [adição de dessa política](https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/) ao nosso padrão de IA Responsável. O reconhecimento do rosto não estará disponível para novos clientes até que lhes seja concedida a política de Acesso Limitado.

- Embora a ID facial detectada seja armazenada em cache, as imagens subsequentes podem ser usadas para comparar os novos rostos com a identidade armazenada em cache e determinar se são _semelhantes_ (em outras palavras, compartilham recursos faciais semelhantes) ou para _verificar_ se a mesma pessoa aparece em duas imagens.

![Um rosto detectado em duas imagens](https://learn.microsoft.com/pt-br/training/wwl-data-ai/detect-analyze-recognize-faces/media/face-matching.png)

- Essa capacidade de comparar rostos anonimamente pode ser útil em sistemas em que é importante confirmar que a mesma pessoa está presente em duas ocasiões, sem a necessidade de saber a identidade real da pessoa. Por exemplo, ao capturar imagens de pessoas conforme elas entram e saem de um espaço protegido para verificar se todos que entraram já saíram.

# Implementar o reconhecimento do rosto