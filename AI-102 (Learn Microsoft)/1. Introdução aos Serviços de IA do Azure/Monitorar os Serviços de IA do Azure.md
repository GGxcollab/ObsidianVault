# Introdução
- Os serviços de IA do Azure fornecem uma plataforma baseada em nuvem para criar recursos de inteligência artificial em seus aplicativos. Como qualquer serviço de software, você deve monitorar os serviços de IA do Azure para acompanhar custos, identificar tendências de utilização e detectar possíveis problemas.
- Depois de concluir este módulo, você poderá:
	- Monitore os custos dos serviços de IA do Azure.
	- Criar alertas e exibir métricas para os serviços de IA do Azure.
	- Gerencie o log de diagnóstico dos serviços de IA do Azure.
# Monitorar o custo
-  Um dos principais benefícios de usar serviços de nuvem é que você pode obter eficiências de custo pagando pelos serviços apenas à medida que os utiliza. Alguns recursos dos serviços de IA do Azure oferecem um nível gratuito com restrições de uso, o que é útil para desenvolvimento e teste, e um ou mais níveis cobrados que geram encargos com base nas transações. A taxa de cobrança específica depende do tipo de recurso.
## Planejar custos para serviços de IA
- Antes de implantar uma solução que depende de serviços de IA, você pode estimar os custos usando a [Calculadora de Preços do Azure](https://azure.microsoft.com/pricing/calculator/).
- Para usar a calculadora de preços para estimar os custos dos serviços de IA, crie uma nova estimativa e selecione **Serviços de IA do Azure** na categoria **IA + Machine Learning**. Em seguida, selecione a API do serviço de IA específico que você planeja usar (por exemplo, _Análise de Texto de IA do Azure_), a região na qual planeja provisioná-la, o tipo de preço da instância que planeja usar e preencha as métricas de uso esperadas e a opção de suporte. Para criar uma estimativa que inclua várias APIs de serviços de IA, adicione outros produtos dos **Serviços de IA do Azure** à estimativa.
- Depois de criar uma estimativa, você pode salvá-la. Você também pode exportá-la no formato Microsoft Excel.
## Exibir custos para serviços de IA
- Em comum com outros recursos do Azure, você pode exibir detalhes de custos acumulados para recursos dos serviços de IA no portal do Azure.
- Para exibir os custos dos serviços de IA, entre no portal do Azure e selecione sua assinatura. Você poderá exibir os custos gerais da assinatura selecionando a guia **Análise de custo**. Para exibir apenas os custos dos serviços de IA, adicione um filtro que restrinja os dados para refletir recursos com um **nome de serviço** de **Serviços Cognitivos**.
>[!NOTE] Observação
> Para obter mais informações, confira [Planejar e gerenciar custos dos serviços de IA do Azure](https://learn.microsoft.com/pt-br/azure/ai-services/plan-manage-costs) na documentação dos serviços de IA.

# Criar alertas
- O Microsoft Azure dá suporte a alertas para recursos por meio da criação de _regras de alerta_. Use regras de alerta a fim de configurar notificações e alertas para seus recursos com base em eventos ou limites de métrica. Esses alertas garantem que a equipe correta seja informada quando surgir um problema.

![A screenshot of an alert in the Azure portal and an email.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/monitor-ai-services/media/alert.png)
## Regras de alerta
- Para criar uma regra de alerta para um recurso dos serviços de IA do Azure, selecione o recurso no portal do Azure e, na guia **Alertas**, adicione uma nova regra de alerta. Para definir a regra de alerta, você deve especificar:
	- O _escopo_ da regra de alerta – em outras palavras, o recurso que você deseja monitorar.
	- Uma _condição_ na qual o alerta é disparado. O gatilho específico para o alerta é baseado em um _tipo de sinal_, que pode ser _Log de Atividades_ (uma entrada no log de atividades criada por uma ação realizada no recurso, como regenerar suas chaves de assinatura) ou _Métrica_ (um limite de métrica como o número de erros superior a dez em uma hora).
	- _Ações_ opcionais, como enviar um email a um administrador notificando-o sobre o alerta ou executando um Aplicativo logico do Azure para resolver o problema automaticamente.
	- _Detalhes da regra de alerta_, como um nome para a regra de alerta e o grupo de recursos no qual ela deve ser definida.

> [!NOTE] Observação
> Para obter mais informações, confira [Visão geral de alertas no Microsoft Azure](https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/alerts-overview) na documentação do Azure.

# Métricas de exibição
- O Azure Monitor coleta métricas para recursos do Azure em intervalos regulares para que você possa rastrear indicadores de utilização, integridade e desempenho de recursos. As métricas específicas coletadas dependem do recurso do Azure. No caso dos Serviços de IA do Azure, o Azure Monitor coleta métricas relacionadas a solicitações de ponto de extremidade, dados enviados e retornados, erros e outras medições úteis.
## Exibir as métricas no portal do Azure
- Você pode exibir métricas para um recurso individual no portal do Azure selecionando o recurso e exibindo sua página **Métricas**. Nessa página, você pode adicionar métricas específicas de recursos a gráficos. Por padrão, um gráfico vazio é criado para você, e você pode adicionar mais gráficos conforme necessário.
- Por exemplo, a imagem a seguir mostra a página **Métricas** de um recurso de serviços de IA, mostrando o número total de chamadas para o serviço ao longo de um período de tempo.

![A screenshot showing metrics for an AI services resource.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/monitor-ai-services/media/metric.png)

- Você pode adicionar várias métricas a um gráfico e escolher agregações e tipos de gráfico apropriados. Quando estiver satisfeito com o gráfico, você pode _compartilhá-lo_ exportando-o para o Excel ou copiando um link para ele e pode _cloná-lo_ para criar um gráfico duplicado na página **Métricas** – potencialmente como um ponto de partida para um novo gráfico que mostra as mesmas métricas de uma maneira diferente.

## Adicionar métricas a um painel
- No portal do Azure, você pode criar _painéis_ que consistem em várias visualizações de diferentes recursos em seu ambiente do Azure para ajudar você a obter uma visão geral da integridade e do desempenho de seus recursos do Azure.
- Para criar um painel, selecione **Painel** no menu do portal do Azure (sua exibição padrão pode já estar definida para um painel em vez da home page do portal). Lá, você pode adicionar até 100 painéis nomeados para encapsular exibições de aspectos específicos de seus serviços do Azure que você deseja rastrear.
- Você pode adicionar uma variedade de blocos e outras visualizações a um painel e, ao exibir métricas para um recurso específico em um gráfico, conforme descrito anteriormente, você pode adicionar o gráfico a um painel novo ou existente. Na imagem a seguir, dois gráficos mostrando as métricas de um recurso de serviços de IA foram adicionados a um painel de controle.

![A screenshot showing metrics in a dashboard.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/monitor-ai-services/media/metric-dashboard.png)

>[!NOTE] Observação
>Para obter mais informações sobre painéis, confira [Criar um painel no portal do Azure](https://learn.microsoft.com/pt-br/azure/azure-portal/azure-portal-dashboards) na documentação do Azure.
 
# Gerenciar logs de diagnóstico
- O log de diagnósticos permite que você capture dados operacionais avançados para um recurso dos serviços de IA do Azure, que pode ser usado para analisar o uso do serviço e solucionar problemas.

## Criar recursos para o armazenamento de log de diagnóstico
- Para capturar logs de diagnóstico para um recurso dos serviços de IA do Azure, você precisa de um destino para os dados de log. Você pode usar os Hubs de Eventos do Azure como um destino para encaminhar os dados para uma solução de telemetria personalizada e pode se conectar diretamente a algumas soluções de terceiros; mas, na maioria dos casos, você usará um (ou ambos) dos seguintes tipos de recurso em sua assinatura do Azure:
	- **Azure Log Analytics** – Um serviço que permite consultar e visualizar dados de log no portal do Azure.
	- **Armazenamento do Azure** – um armazenamento de dados baseado em nuvem que você pode usar para armazenar arquivos de log (que podem ser exportados para análise em outras ferramentas, conforme necessário).

- Você deve criar esses recursos antes de configurar o log de diagnósticos para o recurso dos serviços de IA do Azure. Se você pretende arquivar dados de log no Armazenamento do Microsoft Azure, crie a conta do Armazenamento do Microsoft Azure na mesma região que seu recurso dos serviços de IA do Azure.

## Defina as configurações de diagnóstico
- Com seus destinos de log estabelecidos, você pode definir as configurações de diagnóstico para seu recurso dos serviços de IA do Azure. Defina as configurações de diagnóstico na página **Configurações de diagnóstico** do painel para seu recurso dos serviços de IA do Azure no portal do Azure. Ao adicionar configurações de diagnóstico, você deve especificar:
	- Um nome para suas configurações de diagnóstico.
	- As categorias de dados de eventos de log que você deseja capturar.
	- Detalhes dos destinos nos quais você deseja armazenar os dados de log.

- No exemplo a seguir, as configurações de diagnóstico armazenam todos os dados de log e métricas disponíveis no Azure Log Analytics e no Armazenamento do Azure.

![A screenshot of diagnostic settings for an Azure AI services resource.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/monitor-ai-services/media/diagnostic-settings.png)

## Exibir dados de log no Azure Log Analytics
- Pode levar uma hora ou mais antes que os dados de diagnóstico comecem a fluir para os destinos, mas quando os dados tiverem sido capturados, você poderá exibi-los em seu recurso do Azure Log Analytics executando consultas, conforme mostrado neste exemplo.

![A screenshot of an Azure log Analytics query returning diagnostic data logged for an Azure AI services resource.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/monitor-ai-services/media/azure-log-analytics.png)

>[!NOTE] Observação
>Para obter mais informações, confira [Habilitar log de diagnósticos para serviços de IA do Azure](https://learn.microsoft.com/pt-br/azure/ai-services/diagnostic-logging) na documentação dos serviços de IA do Azure.

