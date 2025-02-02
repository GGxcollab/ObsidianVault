# Introdução
- Suponhamos que você recebeu milhares de imagens e precisa transferir o texto das imagens para um banco de dados do computador. As imagens digitalizadas têm texto organizado em formatos diferentes e contêm vários idiomas. Quais são algumas maneiras de concluir o projeto em um período razoável e garantir que os dados sejam inseridos com um alto grau de precisão?
- Empresas em todo o mundo enfrentam cenários semelhantes todos os dias. Sem os serviços de IA (inteligência artificial), seria desafiador concluir o projeto, especialmente se a escala dele fosse alterada.
- Usando serviços de IA, podemos tratar esse projeto como um cenário de pesquisa visual computacional e aplicar o OCR (reconhecimento óptico de caracteres). O OCR permite extrair texto de imagens, como fotos de placas de rua e produtos, bem como de documentos — como manuscritos ou não estruturados.
- Para criar uma solução de IA automatizada, você precisa treinar modelos de machine learning para abranger muitos casos de uso. O serviço de Visão de IA do Azure fornece acesso a algoritmos avançados para processar imagens e retorna dados para armazenamento seguro.
- Neste módulo, você aprenderá a:
	- Identificar como o Serviço de Visão de IA do Azure permite que você leia texto de imagens
	- Usar o serviço de Visão de IA do Azure com SDKs e a API REST
	- Desenvolver um aplicativo que possa ler texto impresso e manuscrito
# Explorar as opções de Visão de IA do Azure para a leitura de textos
- A IA do Azure fornece dois recursos diferentes que leem texto de documentos e imagens, um no Serviço de Visão de IA do Azure e outro no IA do Azure para Informação de Documentos. Há sobreposição com relação ao que cada serviço fornece, no entanto cada um é otimizado para resultados dependendo da entrada.
	- **Análise de Imagem** OCR (reconhecimento óptico de caracteres):
	    - Use esse recurso para documentos gerais não estruturados com menor quantidade de texto ou imagens que contenham texto.
	    - Os resultados são retornados imediatamente (síncronos) de uma só chamada à API.
	    - Tem funcionalidade para analisar imagens além da extração de texto, incluindo a detecção de objetos, a descrição ou categorização de uma imagem, a geração de miniaturas recortadas inteligentes e muito mais.
	    - Os exemplos incluem: placas de rua, anotações manuscritas e placas de loja.
	- **Informação de Documentos**:
	    - Use esse serviço para ler grandes volumes de texto em imagens e documentos em PDF.
	    - Este serviço usa o contexto e a estrutura do documento para melhorar a precisão.
	    - A chamada de função inicial retorna uma ID de operação assíncrona, que deve ser usada em uma chamada subsequente para recuperar os resultados.
	    - Os exemplos incluem: recibos, artigos e faturas.
- Você pode acessar ambas as tecnologias por meio da API REST ou de uma biblioteca de clientes. Neste módulo, vamos nos concentrar no recurso OCR na **Análise de Imagem**. Se você quiser saber mais sobre **Informação de Documentos**, [a leitura deste módulo](https://learn.microsoft.com/pt-br/training/modules/use-prebuilt-form-recognizer-models/) fornecerá uma boa introdução.
# Usar a API de Leitura
- Para usar o recurso OCR de Leitura, chame a função **ImageAnalysis** (API REST ou método de SDK equivalente), passando a URL da imagem ou os dados binários e, opcionalmente, especificando uma legenda com neutralidade de gênero ou o idioma em que o texto está escrito (com um valor padrão de **en** para inglês).

- Para fazer uma solicitação de OCR para **ImageAnalysis**, especifique o recurso visual como `READ`.
**C#**
```
ImageAnalysisResult result = client.Analyze(
    <image-to-analyze>,
    VisualFeatures.Read);
```

**Python**
```
result = client.analyze(
    image_url=<image_to_analyze>,
    visual_features=[VisualFeatures.READ]
)
```

- Se estiver usando a API REST, especifique o recurso como `read`.

**rest**
```
https://<endpoint>/computervision/imageanalysis:analyze?features=read&...
```

- Os resultados da função OCR de Leitura são retornados de forma síncrona, como JSON ou o objeto específico da linguagem de uma estrutura semelhante. Esses resultados são divididos em _blocos_ (com o serviço atual usando apenas um bloco), _linhas_ e _palavras_. Além disso, os valores de texto são incluídos nos níveis de _linha_ e de _palavra_, facilitando a leitura de linhas inteiras de texto caso você não precise extrair texto no nível da _palavra_ individual.

**JSON**
```
{
    "metadata":
    {
        "width": 500,
        "height": 430
    },
    "readResult":
    {
        "blocks":
        [
            {
                "lines":
                [
                    {
                        "text": "Hello World!",
                        "boundingPolygon":
                        [
                            {"x":251,"y":265},
                            {"x":673,"y":260},
                            {"x":674,"y":308},
                            {"x":252,"y":318}
                        ],
                        "words":
                        [
                            {
                                "text":"Hello",
                                "boundingPolygon":
                                [
                                    {"x":252,"y":267},
                                    {"x":307,"y":265},
                                    {"x":307,"y":318},
                                    {"x":253,"y":318}
                                ],
                            "confidence":0.996
                            },
                            {
                                "text":"World!",
                                "boundingPolygon":
                                [
                                    {"x":318,"y":264},
                                    {"x":386,"y":263},
                                    {"x":387,"y":316},
                                    {"x":319,"y":318}
                                ],
                                "confidence":0.99
                            }
                        ]
                    },
                ]
            }
        ]
    }
}
```

![[Pasted image 20241106112740.png]]
