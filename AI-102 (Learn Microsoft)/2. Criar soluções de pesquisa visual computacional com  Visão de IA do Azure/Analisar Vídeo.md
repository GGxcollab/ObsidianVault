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

# Ex