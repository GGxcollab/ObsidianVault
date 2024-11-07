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

# Detectar o idioma
- A API de detecção de idioma da IA do Azure avalia a entrada de texto e, para cada documento enviado, retorna identificadores de idioma com uma pontuação que indica a força da análise.
- Esse recurso é útil para conteúdo armazena esse texto arbitrário de coleção, onde o idioma é desconhecido. Outro cenário poderia envolver um bot de chat. Se um usuário iniciar uma sessão com o bot de chat, a detecção de idioma poderá ser usada para determinar qual idioma ele está usando e permitirá que você configure suas respostas de bot no idioma apropriado.
- Você pode analisar os resultados dessa análise para determinar qual idioma é usado no documento de entrada. A resposta também retorna uma pontuação que reflete a confiança do modelo (um valor entre 0 e 1).
- A detecção de idioma pode funcionar com documentos ou frases únicas. É importante observar que o tamanho do documento deve ter menos de 5.120 caracteres. O limite de tamanho é por documento e cada coleção é restrita a 1.000 itens (IDs). Uma amostra de um conteúdo JSON formatado corretamente que você pode enviar para o serviço no corpo da solicitação é exibida aqui, incluindo uma coleção de **documentos**, cada um contendo uma **ID** exclusiva e o **texto**a ser analisado. Opcionalmente, você pode fornecer uma **countryHint** para melhorar o desempenho da previsão.