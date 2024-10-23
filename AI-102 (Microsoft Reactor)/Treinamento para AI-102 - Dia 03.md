# Criar uma solução de mineração de conhecimento
### Implementar uma solução de pesquisa inteligente
- **IA do Azure Search**
	- É o motor principal que tem apara armazenamento e indexação do que for, seja documento, texto e etc
	- Mineração de conhecimento alimentada por IA
		- Indexe documentos e dados de uma variedade de fontes
		- Usar habilidades para enriquecer dados de índice
		- Armazenar insights extraídos em um repositório de conhecimento para análise e integração
	- Recurso do Azure:
		- **Pesquisa de IA do Azure** para indexação e consulta principais
		- **Serviços de IA do Azure** para enriquecimento de índice
		- **Conta de armazenamento** para persistência de repositório conhecimento
	- ![[Pasted image 20241022145523.png]]
- **Componentes principais de uma solução de pesquisa de IA**
	- **Fonte de dados**
		- O armazenamento de dados a ser pesquisado:
			- Contêiner do armazenamento de Blobs
			- Banco de Dados SQL
			- Cosmo DB
		- Você também pode enviar documentos JSON diretamente para um índice
	- **Skillset**
		- Pense que Storage account seria um grande deposito, o conteiner seria uma caixa dentro do deposito e o blobs seria os itens que tem dentro da caixa
		- Define um pipeline de enriquecimento de habilidades de IA para aprimorar os dados durante a indexação:
			- Habilidades internas de IA
			- Habilidades personalizadas
	- **Indexador**
		- Mapeia campos de fonte de dados e saídas de conjunto de habilidades para campos de índice
			- A execução do indexador cria o índice
		- Pode ser um API, LLM que se conectam e indexão
	- **índice**
		- Coleção pesquisável de documentos JSON contendo campos extraídos e enriquecidos
- **Como funciona um pipeline de enriquecimento**
	- ![[Pasted image 20241022154841.png]]
### Criar uma habilidade personalizada para a Pesquisa de IA no Azure
- **Introdução às habilidades personalizadas**
	- Quando as habilidades incorporadas não fornecem o que você precisa...
	- Crie uma habilidade personalizada:
		- Integrar a inteligÊncia de documentos
		- Consumir um modelo do Azure Machine Learning
		- Qualquer outra lógica personalizada
	- As habilidades personalizadas são implementadas como APIs da Web
		- Normalmente Azure Functions
	- ![[Pasted image 20241022155846.png]]
- **Interfaces de habilidades personalizadas**
	- ![[Pasted image 20241022160020.png]]
- **Adicionar uma habilidade personalizada a um conjunto de habilidades**
	- Adicionar "Custom.WebApiSkill" a um conjunto de habilidades
	- Especificar o URI para o ponto de extremidade da API Web
		- Opcionalmente, adicione parâmetros e cabeçalho
	- Definir o contexto para especificar em qual ponto da hierarquia de documentos a habilidade deve ser chamada
	- Atribuir valores de entrada
		- Geralmente de campos de documentos existentes
	- Armazenar saída em um novo cargo
		- Opcionalmente, especificar um nome do cmapo de destino (caso contrário, o nome de saída será usado)
	- ![[Pasted image 20241022160519.png]]
### Criar um repositório de conhecimento
- **O que é um repositório de conhecimento?**
	- Insights persistentes extraídos pelo processo de indexação
	- Armazenado como projeções no Armazenamento do Azure
		- **Tabela**: Tabelas relacionais com chaves para ingresso
		- **Objeto**: estruturas JSON de campos de documentos
		- **Arquivos**: imagens extraídas salvas no formato JPG
	- Usado para análise ou integração em fluxos de trabalho de processamento de dados
		- ![[Pasted image 20241022162951.png]]
- **Uso da habilidade do Shaper para projeções**
	- Reestruturar campos para simplificar projeções
		- Criar um objeto JSON com os campos que você deseja persistir
		- Usar sourceContext e entradas para mapear primitivos para objetos JSON bem formados
		- ![[Pasted image 20241022165104.png]]
- **Implementar um repositório de conhecimento**
	- ![[Pasted image 20241022165216.png]]
----------
# Desenvolver soluções com a IA do Azure para informação de Documentos
### Desenvolver uma solução de Informação de Documentos (Document Intelligence Studio)
- **O Serviço para Informação de Documentos**
	- Extração de dados de formulários e documentos:
		- Análise de documentos a partir de documentos gerais
			- Leia: OCR para texto impresso e escrito
			- Layout: extrair texto e estrutura
			- Documento geral: extrair texto, estrutura e pares chave-valor
		- Modelos pré-criados para tiposde formulário comuns
		- Treinar modelos personalizados para sesu próprios formulários
			- Modelo personalizado: extrair dados de layouts estáticos
			- Neural personalizado: extrair dados de documentos de tipo mistos
			- Composição personalizada: coleção de vários modelos atribuídos a um único modelo
	- Provisão como serviço único recurso de **Informação de Documentos** ou **Serviços de IA do Azure** multisserviços
		- ![[Pasted image 20241023114826.png]]
- **Modelos predefinidos**
	- ![[Pasted image 20241023115454.png]]
- **Chamando API**
	- Cada solicitação é configurada com seu ponto de extremidade de recurso e precisa de sua chave de recurso
	- Envie a solicitação, que quando bem-sucedida retorna um instrumento de sondagem para obter os resultados
		- REST o retorna no cabeçalho Operation-Location
		- SDKS retornam um objeto da solicitação
	- Consultar o instrumento de sondagem recebido para os dados extraídos
		- ![[Pasted image 20241023120912.png]]
- **Resposta da API**
	- A resposta foi dividida por página, linhas e palavras
	- Subconjunto de resposta REST incluído aqui
	- Os objetos de resposta do SDK tem estrutura semelhante, divididos de forma semelhante
	- Dados adicionais sobre marcas de seleção ou texto detectado, como caixa delimitadora e estilo manuscrito
	- ![[Pasted image 20241023141212.png]]
- **Tipos de modelos personalizados**
	- **Classificação personalizada**
		- Aplicar um rótulo a todo documento
		- Ideal para classificar um grande número de documentos recebidos em tipos
		- Requer duas classes diferentes e um mínimo de cinco documentos rotulados por classe
		- Um tipo de modelo treinamento
	- **Extração personalizada**
		- Aplica rótulo a texto específico 
		- Ideal para extrair etiquetas personalizadas de documentos
		- Requer cinco exemplos do mesmo tipo de documento
		- Dois métodos de treinamento:
			- **Modelo personalizado (formulário personalizado)**
				- Tempo de treinamento: 1-5 minutos
				- Estrutura do documento: formulários, modelos, outros documentos estruturados
			- **Neural personalizado (documento personalizado)**
				- Tempo de treinamento: 20-60 minutos
				- Estrutura do documento: documentos estruturados e não estruturado
	- 
- **Treinamento de modelos personalizados**
	1. Crie projetos e carregue arquivos de treinamento para seu projeto ou conecte-se ao armazenamento de blobs contendo arquivos
	2. adicionar tipo de dados (como campo ou assinatura) para começar a rotular seu conjunto de dados
	3. Selecione uma palavra no documento e atribua um dos campos para rotulá-la
	4. Repita para todos os campos e arquivos em seu conjunto de dados
	5. Layout e etiquetagem automática (usando um modelo predefinido) podem auxiliar nesse processo
	6. Treine o modelo, fornecendo um ID de modelo usada em solicitações de API
		![[Pasted image 20241023143414.png]]
- **Pontuações de precisão e con**