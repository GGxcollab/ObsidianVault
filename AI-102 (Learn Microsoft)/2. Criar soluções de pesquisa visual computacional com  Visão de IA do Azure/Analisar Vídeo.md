# Introdução
- É cada vez mais comum que organizações e indivíduos gerem conteúdo em formato de vídeo. Por exemplo, você pode usar um celular para capturar um evento ao vivo ou pode gravar uma teleconferência que combina filmagens de webcam e apresentação de slides ou documentos. Como resultado, uma grande quantidade de informações é encapsulada em arquivos de vídeo, e você pode precisar extrair essas informações para análise ou para dar suporte à indexação para capacidade de pesquisa.
- Neste módulo, você aprenderá a usar o serviço **Azure Video Indexer** para analisar vídeos.
- Após concluir este módulo, você será capaz de:
	- Descreva os recursos do Azure Video Indexer.
	- Extraia insights personalizados.
	- Use widgets e APIs do Azure Video Indexer.
# Entenda os recursos do Azure Video Indexer
- O serviço **Azure Video Indexer** foi projetado para ajudar você a extrair informações de vídeos. Ele fornece funcionalidade que você pode usar para:

	- _Reconhecimento facial_ - detectando a presença de pessoas individuais na imagem. Isso requer aprovação [de Acesso Limitado](https://aka.ms/cog-services-limited-access) .
	- _Reconhecimento óptico de caracteres_ - leitura de texto no vídeo.
	- _Transcrição de fala_ - criação de uma transcrição de texto do diálogo falado no vídeo.
	- _Tópicos_ - identificação dos principais tópicos discutidos no vídeo.
	- _Sentimento_ - análise de quão positivos ou negativos são os segmentos dentro do vídeo.
	- _Rótulos_ - tags de rótulo que identificam objetos ou temas principais ao longo do vídeo.
	- _Moderação de conteúdo_ - detecção de temas adultos ou violentos no vídeo.
	- _Segmentação de cena_ - uma divisão do vídeo em suas cenas constituintes.

 - O serviço Video Analyzer fornece um portal que você pode usar para carregar, visualizar e analisar vídeos interativamente.

![O portal do Analisador de Vídeo](https://learn.microsoft.com/en-us/training/wwl-data-ai/analyze-video/media/video-indexer-portal.png)

# Extrair insights personalizados
- O Azure Video Indexer inclui modelos predefinidos que podem reconhecer celebridades famosas, fazer OCR e transcrever frases faladas em texto. Você pode estender os recursos de reconhecimento do Video Analyzer criando modelos personalizados para:
	- **Pessoas** . Adicione imagens dos rostos das pessoas que você quer reconhecer em vídeos e treine um modelo. O Video Indexer reconhecerá essas pessoas em todos os seus vídeos.
		- *Observação*:
			- Isso só funciona após a aprovação [do Acesso Limitado](https://aka.ms/cog-services-limited-access) , aderindo ao nosso padrão de IA Responsável.
	- **Idioma** . Se sua organização usa terminologia específica que pode não ser de uso comum, você pode treinar um modelo personalizado para detectá-la e transcrevê-la.
	- **Marcas** . Você pode treinar um modelo para reconhecer nomes específicos como marcas, por exemplo, para identificar produtos, projetos ou empresas que sejam relevantes para o seu negócio.Os widgets usados no portal do Azure Video Indexer para reproduzir, analisar e editar vídeos podem ser incorporados em suas próprias interfaces HTML personalizadas. Você pode usar essa técnica para compartilhar insights de vídeos específicos com outras pessoas sem dar a elas acesso total à sua conta no portal do Azure Video Indexer.

# Use widgets e APIs do Video Analyzer

Embora você possa executar todas as tarefas de análise de vídeo no portal do Azure Video Indexer, você pode querer incorporar o serviço em aplicativos personalizados. Há duas maneiras de fazer isso.

## Widgets do Indexador de Vídeo do Azure

Os widgets usados no portal do Azure Video Indexer para reproduzir, analisar e editar vídeos podem ser incorporados em suas próprias interfaces HTML personalizadas. Você pode usar essa técnica para compartilhar insights de vídeos específicos com outras pessoas sem dar a elas acesso total à sua conta no portal do Azure Video Indexer.
<<<<<<< HEAD
![[Pasted image 20241106150712 1.png]]
=======
![[Pasted image 20241106150712.png]]
>>>>>>> origin/master

# API do Indexador de Vídeo do Azure
- O Azure Video Indexer fornece uma API REST que você pode usar para obter informações sobre sua conta, incluindo um token de acesso.

**HTTP**
```
https://api.videoindexer.ai/Auth/<location>/Accounts/<accountId>/AccessToken
```

- Você pode então usar seu token para consumir a API REST e automatizar tarefas de indexação de vídeo, criando projetos, recuperando insights e criando ou excluindo modelos personalizados.

- Por exemplo, uma chamada GET para `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Customization/CustomLogos/Logos/<logoId>?<accessToken>`o endpoint REST retorna o logotipo especificado. Em outro exemplo, você pode enviar uma solicitação GET para `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos?<accessToken>`, que retorna detalhes de vídeos em sua conta, semelhante ao seguinte exemplo JSON:

**JSON**
```
{ 
	"accountId": "SampleAccountId", 
	"id": "30e66ec1b1", 
	"partition": null, 
	"externalId": null, 
	"metadata": null, 
	"name": "test3", 
	"description": null, 
	"created": "2018-04-25T16=50=00.967+00=00", 
	"lastModified": "2018-04-25T16=58=13.409+00=00", 
	"lastIndexed": "2018-04-25T16=50=12.991+00=00", 
	"privacyMode": "Private", 
	"userName": "SampleUserName", 
	"isOwned": true, 
	"isBase": true, 
	"state": "Processing", 
	"processingProgress": "", 
	"durationInSeconds": 13, 
	"thumbnailVideoId": "30e66ec1b1", 
	"thumbnailId": "55848b7b-8be7-4285-893e-cdc366e09133", 
	"social": { 
		"likedByUser": false, 
		"likes": 0, 
		"views": 0 
		}, 
	"searchMatches": [], 
	"indexingPreset": "Default", 
	"streamingPreset": "Default", 
	"sourceLanguage": "en-US" }
```

## Implantar com modelo ARM
Os modelos do Azure Resource Manager (ARM) estão disponíveis para criar o recurso Azure AI Video Indexer na sua assinatura, com base nos parâmetros especificados no arquivo de modelo.

Para obter uma lista completa de APIs disponíveis, consulte o [Portal do desenvolvedor do Video Indexer](https://api-portal.videoindexer.ai/) .
<<<<<<< HEAD
![[Pasted image 20241106152304 1.png]]
=======
![[Pasted image 20241106152304.png]]
>>>>>>> origin/master
