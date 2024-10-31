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

