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
