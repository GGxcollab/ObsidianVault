# Introdução
- Todos os dias, o mundo gera uma enorme quantidade de dados; grande parte dele baseada em texto na forma de emails, postagens de mídias sociais, revisões online, documentos de negócios e muito mais. Técnicas de inteligência artificial que aplicam modelos estatísticos e semânticos permitem que você crie aplicativos que extraem significado e insights dos dados baseados em texto.

- A Linguagem de IA do Azure fornece uma API para técnicas comuns de análise de texto que você pode integrar facilmente ao código do seu próprio aplicativo.

- Neste módulo, você aprenderá como utilizar a Linguagem de IA do Azure para:
	- Detecção de idioma a partir do texto.
	- Analisar o sentimento do texto.
	- Extrair frases-chave, entidades e entidades vinculadas.

# Provisionar um recurso de Linguagem de IA do Azure
-A Linguagem de IA do Azure foi projetada para ajudar você a extrair informações do texto. Ele fornece funcionalidade que você pode usar para:

- _Detecção de idioma_ – determinar o idioma no qual o texto está escrito.
    
- _Extração de frases-chave_ – identificar palavras e frases importantes no texto que indicam os pontos principais.
    
- _Análise de sentimento_ – quantificar o quanto o texto é positivo ou negativo.
    
- _Reconhecimento de entidade nomeada_ – detectar referências a entidades, incluindo pessoas, locais, períodos, organizações e muito mais.
    
- _Vinculação de entidade_ – identificar entidades específicas fornecendo links de referência para artigos da Wikipédia.
    
    ![Diagram showing an Azure AI Language resource performing language detection, key phrase extraction, sentiment analysis, named entity recognition, and entity linking.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/analyze-text-ai-language/media/text-analytics-resource.png)
    

## Recursos do Azure para análise de texto
Para utilizar a Linguagem de IA do Azure para analisar texto, você deve provisionar um recurso para ela na sua assinatura do Azure.

Após o provisionamento de um recurso adequado na sua assinatura do Azure, você pode utilizar seu **ponto de extremidade** e uma de suas **chaves** para chamar as APIs da Linguagem de IA do Azure a partir do seu código. Você pode chamar as APIs de Linguagem de IA do Azure enviando solicitações no formato JSON para a interface REST ou usando qualquer um dos SDKs de programação específicos por linguagem.

>[!NOTE] Observação
>Os exemplos de código nas unidades subsequentes neste módulo mostram as solicitações JSON e as respostas trocadas com a interface REST. Ao usar um SDK, as solicitações JSON são abstraídas por objetos e métodos apropriados que encapsulam os mesmos valores de dados. Você terá a oportunidade de experimentar o SDK para C# ou Python por conta própria no exercício posterior do módulo.

