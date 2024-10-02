# O que é inteligência artificial?
- Software que exibe recursos semelhantes aos humanos, tais como:
	- Percepção Visual
	- Análise de texto 
	- Conversa
	- Tomada de decisão 
#### Ciência de dados, Aprendizado de máquina e IA
- IA: Aplicativos e agentes de software inteligente.
- Machine Learning: Uso de dados e algoritmos para treinar modelos preditivos.
- Ciência de Dados: Aplicação de técnicas matemáticas e estatísticas de análise de dados.
#### IA para engenheiros de software
- Habilidades de desenvolvimento de software
	- Código (C#, Python, Node.js, ...)
	- Consumo de APIs (REST ou SDKs)
	- DevOps (controle do código - fonte, CI/CD)
- Reconhecimento conceitual de IA
	- Treinamento de modelo e inferência
	- Pontuação de probabilidade e confiança
	- IA responsável e ética
#### Consideração para a IA responsável
- Imparcialidade
- Confiabilidade e Segurança
- Privacidade e Segurança
- Inclusão 
- Transparência
- Responsabilidade
#### Azure Machine Learning
- Plataforma de nuvem para criação e operação de soluções de aprendizado de máquina
- ![[Pasted image 20241001154247.png]]
#### Serviços de IA do Azure
- **Serviços de IA pré-empacotados que você pode integrar em soluções.**
	- Os recursos incluem:
		- Idiomas
			- Análise de texto 
			- Respostas ás perguntas
			- Reconhecimento vocal
			- Tradução
		- Fala
			- Reconhecimento de fala
			- Sintetização de voz
			- Tradução de fala
			- Reconhecimento de locutor
		- Visão
			- Análise de imagens e vídeos
			- Classificação de imagens
			- Detecção de objetos
			- Reconhecimento óptico de caracteres
		- Generativo
			- Gerar complementos de texto
			- Geração de imagem
- Serviços de IA do Azure
	- IA do Azuere para Informação de Documentos
	- Linguagem de IA do Azure
	- Visão de IA do Azure
	- OpenAI do Azure
	- IA do Azure Search
#### AI do Azure Search
- Indexação enriquecida com IA para pesquisa e mineração de conhecimento.
- É possivel dizer que é como se fosse sua pasta do seu computador so que na nuvem, com fotos, pdfs, documentos.
- Bom utilizar para organizar suas informações
- ![[Pasted image 20241001163142.png]]
- ----------------------------------------------------
### Provisionar recursos dos Serviços de IA do Azure
- **Crie em recurso em sua assinatura do Azure**
	- Você criará um recurso de serviço único ou um recurso de vários serviços:
	- Um recurso multiserviço **(Serviçode IA do Azure)**:
		- Acesse vários serviços de IA do Azure com uma única chave e ponto de extremidade.
		- Consolida a cobrança dos serviços que você usa.
	- Recurso de serviço único (por exemplo, **Idioma**):
		- Acesse um só serviço de IA do Azure com uma chave exclusiva e um ponto de extremidade para cada serviço criado.
		- Use a camada gratuita para experimentar o serviço.
	- ![[Pasted image 20241001165147.png]]
### Pontos de extremidade, chaves e locais
- **Informações  necessárias para se conectar**
- **Ponto de extremidade:**
	- URL na qual o serviço pode ser consumido
	- Exigido pela *maioria* dos clientes SDK
- **Chaves:**
	- Use *qualquer uma* das chaves para autenticar
- **Local**
	- Data center do Azure no qual o recurso é provisionado
	- Exigido por *alguns* clientes SDK
- ![[Pasted image 20241001165746.png]]
### APIs REST dos Serviços de IA do Azure
- **Os clientes enviam solicitações HTTP para o ponto de extremidade do recurso**
	- Chave especificada no cabeçalho da solicitação
	- Dados de entrada no formato JSON
	- O esquema específico varia de acordo com o serviço e o método
- **O serviço retorna a resposta em JSON**
- ![[Pasted image 20241001170243.png]]
### SDKs de serviços de IA do Azure
- **A biblioteca de runtime abstrai a interface REST**
- Vários SDKs para cada serviço:
	- .Net
	- Python
	- Node.js
	- Java 
	- Others
- ![[Pasted image 20241001170548.png]]
- ----------------------------------------------------
# Usar os Serviços de IA do Azure para aplicativos empresariais
### Considerações sobre segurança dos Serviços de IA do Azure
- **Regenerar chaves regularmente para proteger o acesso**
	- Para evitar a interrupção do serviço, altere os aplicativos para usar a chave 2 antes de regenerar a chave 1; e vice-versa.
- **Considere proteger chaves armazenando-as no Azure Key Vault**
	- Os aplicativos podem usar uma entidade de serviço como uma identidade gerenciada para recuperar chaves do Key Vault.
- ![[Pasted image 20241001171414.png]]
### Monitorar a atividade dos Serviços de IA do Azure
- **ALERTAS**
	- Esses alertas garantem que a equipe correta saiba quando surgir um problema.
	- Cada alerta ou notificação disponível no Azure Monitor é o produto de uma regra.
- **MÉTRICA**
	- Métricas são valores numéricos.
	- As métricas são coletadas em intervalos regulares e são úteis para alertas. 
	- As métricas são armazenadas em um banco de dados de série temporal.
- **CONFIGURAÇÃO DE DIAGNÓSTICO**
	- As configurações de diagnóstico servem para fornecer informações detalhadas para diagnósticos e auditoria.
	- Destinos de diagnóstico:
		- Workspace do Lof Analytics
		- Hub de Eventos
		- Armazenamento do Azure
- **LOGS**
	- Os Logs contêm informações com carimbo de data/hora sobre as alterações feitas nos recursos.
	- Os dados de log são organizados em registro.
	- Os logs podem incluir valores numéricos, mas a maioria inclui dados de texto.
	- O tipo mais comum de entrada de log registra um evento.
- ----------------------------------------------------
# Criar soluções de pesquisa computacional com a Visão de IA do Azure
### Visão de IA do Azure - Análise de Imagem
- **Análise de imagem**:
	- Geração de legendas e tags
	- Detecção de objetos
	- Detecção de pessoas
	- Reconhecimento óptico de caracteres
	- Miniaturas com recorte inteligente
	- Remoção de Plano de Fundo
	- Inserções multimodais
	- Reconhecimento de produto
- **Pode ser usado como:**
	- Recurso autônomo da **Visão de IA do Azure**
	- Recurso multisserviço dos **Serviços de IA do Azure**
	- *Alguns novos recursos são limitados a regiões especificas*
- ![[Pasted image 20241002112818.png]]
### APIs de Análise de Imagem
- Chamada única **de análise** para recuperar recursos específicos na enumeração **VisualFeatures**
	- VisualFeatures.Caption
	- VisualFeatures.DenseCaptions
	- VisualFeatures.Tags.
	- VisualFeatures.Objects
	- VisualFeatures.SmartCrops
	- VisualFeatures.People
	- VisualFeatures.Read
- Os SDKs definem o **cliente** e, em seguida, chamam a função **analyze()** a partir de:
	- Cliente define ponto de extremidade e chave de recurso
- **Analyze()** precisa de:
	- Dados de imagem do arquivo ou URL
	- Recursos visuais para analisar
	- (Opcional) Opções de análise: Quais recursos, idiomas e outras opções para a análise 
- ![[Pasted image 20241002114633.png]]
### Opções de análise de imagem
- Opções de análise
	- Taxas de proporção de corte 
	- Legendas neutras em relação a gênero
	- idioma
	- Versão do modelo
- ![[Pasted image 20241002115033.png]]
### Resultado de análise de imagem
- A análise de imagem bem-sucedida retorna JSON (REST) ou objeto (SDKs)
- Os resultados podem ter uma ou várias camadas de profundidade
	- Rótulos > valores[] > nome
	- Texto > linhas > palavras
- ![[Pasted image 20241002115612.png]]
### Visão de IA do Azure - OCR
- Usar **Análise de imagem** com o recurso LEITURA
- Visão OCR vs. Informação de Documentos:
	- OCR: imagens gerais, não documentadas, com quantidades menores de texto. API síncrona.
	- Informação de Documentos: ideal para documentos com muito texto: API assíncrona.
- Resultados em JSON (REST) ou objeto (SDK) de estrutura semelhante
- ![[Pasted image 20241002115941.png]]
- ----------------------------------------------------
# Detectar rostos com Visão de IA do Azure
### Opções para detecção, análise e reconhecimento facial
- **Análise de Imagens**
	- Detecção de pessoas
	- Apenas localização fornecida
- **Serviço de Detecção Facial**
	- Detecção facial
	- Análise abrangente de características faciais
	- Comparação e identificação Facial *
	- Reconhecimento Facial *
	- * *Exige aprovação de Acesso Limitado*
- ![[Pasted image 20241002134043.png]]
### Consideração para detecção facial e reconhecimento facial
- Os princípios de IA responsável se aplicam a todos os tipos de aplicativos, mas sistemas que dependem de dados faciais podem ser particularmente problemático. Como uma proteçãeo para o uso de IA responsável, o reconhecimento facial, identificação, verificação e comparação esta por trás de uma política de Acesso Limitado, exigindo que os usuários sejam aprovados pela Microsoft antes de habilitar esses recursos.
- **Segurança e privacidade de dados**
	- Sistemas baseados em dados faciais devem proteger a privacidade individual, garatindo que os dados pessoais identificáveis não sejam acessados de forma inadequada.
- **Transparência**
	- Garanta que os usuários estejam informados sobre como a imagem deles será