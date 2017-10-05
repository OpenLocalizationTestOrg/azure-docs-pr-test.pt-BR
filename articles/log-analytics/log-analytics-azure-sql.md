---
title: "Solução de Análise do Azure SQL no Log Analytics | Microsoft Docs"
description: "A solução de Análise do Azure SQL ajuda a gerenciar os bancos de dados do Azure SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="64835-103">Monitorar o Banco de Dados SQL do Azure usando a Análise do Azure SQL (Visualização) no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="64835-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Símbolo da Análise de SQL do Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="64835-105">A solução Análise de SQL do Azure do Azure Log Analytics coleta e visualiza métricas de desempenho importantes do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="64835-106">Usando as métricas que coleta com a solução, você pode criar alertas e regras de monitoramentos personalizadas.</span><span class="sxs-lookup"><span data-stu-id="64835-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="64835-107">E você pode monitorar o Banco de Dados SQL e métricas de pool elástico em várias assinaturas do Azure e pools elásticos e visualizá-los.</span><span class="sxs-lookup"><span data-stu-id="64835-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="64835-108">A solução também ajuda a identificar problemas em cada camada da pilha do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64835-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="64835-109">Ele usa [métricas de Diagnóstico do Azure](log-analytics-azure-storage.md) junto com modos de exibição de Log Analytics para apresentar dados sobre todos os bancos de dados do Azure SQL e pools elásticos em um único espaço de trabalho de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="64835-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="64835-110">Atualmente, essa solução de visualização dá suporte a até 5.000 Bancos de Dados do Azure SQL e 150.000 Pools Elásticos por espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="64835-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="64835-111">A solução Análise de SQL do Azure, assim como outras disponíveis para o Log Analytics, ajuda você a monitorar e receber notificações sobre a integridade dos recursos do Azure – neste caso, o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="64835-112">O Banco de Dados SQL do Microsoft Azure é um serviço de banco de dados relacional escalonável que fornece recursos semelhantes aos recursos familiares do SQL Server para aplicativos em execução na nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="64835-113">O Log Analytics ajuda a coletar, correlacionar e visualizar dados estruturados e não estruturados.</span><span class="sxs-lookup"><span data-stu-id="64835-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="64835-114">Fontes conectadas</span><span class="sxs-lookup"><span data-stu-id="64835-114">Connected sources</span></span>

<span data-ttu-id="64835-115">A solução Análise de SQL do Azure não usa agentes para se conectar ao serviço Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="64835-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="64835-116">A tabela a seguir descreve as fontes conectadas que têm suporte dessa solução.</span><span class="sxs-lookup"><span data-stu-id="64835-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="64835-117">Fonte Conectada</span><span class="sxs-lookup"><span data-stu-id="64835-117">Connected Source</span></span> | <span data-ttu-id="64835-118">Suporte</span><span class="sxs-lookup"><span data-stu-id="64835-118">Support</span></span> | <span data-ttu-id="64835-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="64835-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="64835-120">Agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="64835-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="64835-121">Não</span><span class="sxs-lookup"><span data-stu-id="64835-121">No</span></span> | <span data-ttu-id="64835-122">Agentes diretos do Windows não são usados pela solução.</span><span class="sxs-lookup"><span data-stu-id="64835-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="64835-123">Agentes do Linux</span><span class="sxs-lookup"><span data-stu-id="64835-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="64835-124">Não</span><span class="sxs-lookup"><span data-stu-id="64835-124">No</span></span> | <span data-ttu-id="64835-125">Agentes do Linux diretos não são usados pela solução.</span><span class="sxs-lookup"><span data-stu-id="64835-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="64835-126">Grupo de gerenciamento do SCOM</span><span class="sxs-lookup"><span data-stu-id="64835-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="64835-127">Não</span><span class="sxs-lookup"><span data-stu-id="64835-127">No</span></span> | <span data-ttu-id="64835-128">Uma conexão direta do agente do SCOM ao Log Analytics não é usada pela solução.</span><span class="sxs-lookup"><span data-stu-id="64835-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="64835-129">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="64835-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="64835-130">Não</span><span class="sxs-lookup"><span data-stu-id="64835-130">No</span></span> | <span data-ttu-id="64835-131">O Log Analytics não lê os dados pré-existentes de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="64835-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="64835-132">Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="64835-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="64835-133">Sim</span><span class="sxs-lookup"><span data-stu-id="64835-133">Yes</span></span> | <span data-ttu-id="64835-134">Os dados de métricas do Azure são enviados para o Log Analytics diretamente pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="64835-135">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="64835-135">Prerequisites</span></span>

- <span data-ttu-id="64835-136">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-136">An Azure Subscription.</span></span> <span data-ttu-id="64835-137">Se não tiver uma, você poderá criá-la [grátis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="64835-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="64835-138">Um espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="64835-138">A Log Analytics workspace.</span></span> <span data-ttu-id="64835-139">Você pode usar um existente ou pode [criar um novo](log-analytics-get-started.md) para começar a usar essa solução.</span><span class="sxs-lookup"><span data-stu-id="64835-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="64835-140">Habilite o Diagnóstico do Azure para os bancos de dados do Azure SQL e pools elásticos e [configure-os para enviar os dados para o Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="64835-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="64835-141">Configuração</span><span class="sxs-lookup"><span data-stu-id="64835-141">Configuration</span></span>

<span data-ttu-id="64835-142">Realize as etapas a seguir para adicionar a solução Análise de SQL do Azure ao seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="64835-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="64835-143">Adicione a solução de análise do SQL do Azure do [marketplace do Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) ou usando o processo descrito em [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="64835-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="64835-144">No portal do Azure, clique em **Novo** (o símbolo +) e, na lista de recursos, selecione **Monitoramento + Gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="64835-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="64835-145">![Monitoramento + Gerenciamento](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="64835-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="64835-146">Na lista **Monitoramento + Gerenciamento**, clique em **Ver todos**.</span><span class="sxs-lookup"><span data-stu-id="64835-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="64835-147">Na lista **Recomendado**, clique em **Mais** e, na nova lista, localize **Análise do Azure SQL (Visualização)** e selecione-a.</span><span class="sxs-lookup"><span data-stu-id="64835-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="64835-148">![Solução de Análise do Azure SQL](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="64835-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="64835-149">Na folha **Análise do Azure SQL (Visualização)**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="64835-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="64835-150">![Criar](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="64835-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="64835-151">Na folha **Criar nova solução**, selecione o espaço de trabalho ao qual você deseja adicionar a solução e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="64835-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="64835-152">![adicionar ao espaço de trabalho](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="64835-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="64835-153">Para configurar várias assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="64835-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="64835-154">Para dar suporte a várias assinaturas, use o script do PowerShell de [Habilitar log de métricas de recursos do Azure usando o PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="64835-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="64835-155">Forneça a ID de recurso do espaço de trabalho como um parâmetro ao executar o script para enviar dados de diagnóstico de recursos em uma assinatura do Azure a um espaço de trabalho em outra assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="64835-156">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="64835-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="64835-157">Usando a solução</span><span class="sxs-lookup"><span data-stu-id="64835-157">Using the solution</span></span>

<span data-ttu-id="64835-158">Quando você adiciona a solução ao espaço de trabalho, o bloco de Análise do Azure SQL é adicionado ao espaço de trabalho e aparece na Visão geral.</span><span class="sxs-lookup"><span data-stu-id="64835-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="64835-159">O bloco mostra o número de bancos de dados do Azure SQL e pools elásticos do Azure SQL aos quais a solução está conectada.</span><span class="sxs-lookup"><span data-stu-id="64835-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Bloco de Análise do SQL Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="64835-161">Exibindo dados da Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="64835-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="64835-162">Clique no bloco **Análise de SQL do Azure** para abrir o painel da Análise de SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="64835-163">O painel inclui as folhas definidas abaixo.</span><span class="sxs-lookup"><span data-stu-id="64835-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="64835-164">Cada folha lista até 15 recursos (assinatura, servidor, pool elástico e banco de dados).</span><span class="sxs-lookup"><span data-stu-id="64835-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="64835-165">Clique em um dos recursos para abrir o painel do recurso específico.</span><span class="sxs-lookup"><span data-stu-id="64835-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="64835-166">Pool elástico ou Banco de dados contém os gráficos com as métricas de um recurso selecionado.</span><span class="sxs-lookup"><span data-stu-id="64835-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="64835-167">Clique em um gráfico para abrir a caixa de diálogo Pesquisa de Logs.</span><span class="sxs-lookup"><span data-stu-id="64835-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="64835-168">Folha</span><span class="sxs-lookup"><span data-stu-id="64835-168">Blade</span></span> | <span data-ttu-id="64835-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="64835-169">Description</span></span> |
|---|---|
| <span data-ttu-id="64835-170">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="64835-170">Subscriptions</span></span> | <span data-ttu-id="64835-171">Lista de assinaturas com o número de servidores, pools e bancos de dados conectados.</span><span class="sxs-lookup"><span data-stu-id="64835-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="64835-172">Servidores</span><span class="sxs-lookup"><span data-stu-id="64835-172">Servers</span></span> | <span data-ttu-id="64835-173">Lista de servidores com o número de pools e bancos de dados conectados.</span><span class="sxs-lookup"><span data-stu-id="64835-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="64835-174">Pools elásticos</span><span class="sxs-lookup"><span data-stu-id="64835-174">Elastic Pools</span></span> | <span data-ttu-id="64835-175">Lista de pools elásticos conectados com GBs e eDTUs máximos no período observado.</span><span class="sxs-lookup"><span data-stu-id="64835-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="64835-176">Bancos de dados</span><span class="sxs-lookup"><span data-stu-id="64835-176">Databases</span></span> | <span data-ttu-id="64835-177">Lista de bancos de dados conectados com GBs e DTUs máximos no período observado.</span><span class="sxs-lookup"><span data-stu-id="64835-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="64835-178">Analisar dados e criar alertas</span><span class="sxs-lookup"><span data-stu-id="64835-178">Analyze data and create alerts</span></span>

<span data-ttu-id="64835-179">Você pode criar facilmente alertas com os dados provenientes de recursos de Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="64835-180">Aqui estão algumas das consultas de [pesquisa de logs](log-analytics-log-searches.md) úteis que você pode usar para alertas:</span><span class="sxs-lookup"><span data-stu-id="64835-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="64835-181">*DTU alta no Banco de Dados SQL do Azure*</span><span class="sxs-lookup"><span data-stu-id="64835-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="64835-182">*Alta DTU no pool elástico do Banco de Dados SQL do Azure*</span><span class="sxs-lookup"><span data-stu-id="64835-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="64835-183">Você pode usar essas consultas com base no alerta para alertar sobre limites específicos para o Banco de Dados SQL do Azure e pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="64835-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="64835-184">Para configurar um alerta para seu espaço de trabalho OMS:</span><span class="sxs-lookup"><span data-stu-id="64835-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="64835-185">Para configurar um alerta para seu espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="64835-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="64835-186">Acesse o [portal do OMS](http://mms.microsoft.com/) e entre.</span><span class="sxs-lookup"><span data-stu-id="64835-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="64835-187">Abra o espaço de trabalho que você configurou para a solução.</span><span class="sxs-lookup"><span data-stu-id="64835-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="64835-188">Na página Visão geral, clique no bloco **Análise do Azure SQL (Visualização)**.</span><span class="sxs-lookup"><span data-stu-id="64835-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="64835-189">Execute uma das consultas de exemplo.</span><span class="sxs-lookup"><span data-stu-id="64835-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="64835-190">Na Pesquisa de Log, clique em **Alerta**.</span><span class="sxs-lookup"><span data-stu-id="64835-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="64835-191">![criar alerta na pesquisa](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="64835-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="64835-192">Na página **Adicionar Regra de Alerta**, defina as propriedades adequadas e os limites específicos que você deseja e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="64835-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="64835-193">![adicionar regra de alerta](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="64835-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="64835-194">Tomar decisões com base em dados da Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="64835-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="64835-195">Por exemplo, uma das consultas mais úteis que você pode executar é comparar a utilização de DTU para todos os Pools Elásticos do Azure SQL em todas as suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="64835-196">A DTU (Unidade de Taxa de Transferência de Banco de Dados) fornece uma maneira de descrever a capacidade relativa de um nível de desempenho de pools e bancos de dados Basic, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="64835-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="64835-197">DTUs são baseadas em uma medida combinada de CPU, memória, leituras e gravações.</span><span class="sxs-lookup"><span data-stu-id="64835-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="64835-198">À medida que as DTUs aumentam, aumenta a capacidade oferecida pelo nível de desempenho.</span><span class="sxs-lookup"><span data-stu-id="64835-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="64835-199">Por exemplo, um nível de desempenho com cinco DTUs tem cinco vezes mais energia do que um nível de desempenho com uma DTU.</span><span class="sxs-lookup"><span data-stu-id="64835-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="64835-200">Uma cota de DTU máxima aplica-se a cada servidor e pool elástico.</span><span class="sxs-lookup"><span data-stu-id="64835-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="64835-201">Executando a consulta de Pesquisa de Log a seguir, você pode saber facilmente se está subutilizando ou sobreutilizando os pools elásticos do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="64835-202">Se o seu espaço de trabalho fosse atualizado para a [nova linguagem de consulta do Log Analytics](log-analytics-log-search-upgrade.md), a consulta acima seria alterada para o demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="64835-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="64835-203">No exemplo a seguir, você pode ver que um pool elástico tem alto uso de quase 100% de DTU, enquanto outros têm pouca utilização.</span><span class="sxs-lookup"><span data-stu-id="64835-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="64835-204">Você pode investigar mais para solucionar possíveis alterações recentes no ambiente usando os logs de atividade do Azure.</span><span class="sxs-lookup"><span data-stu-id="64835-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Resultados de pesquisa de log - alta utilização](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="64835-206">Consulte também</span><span class="sxs-lookup"><span data-stu-id="64835-206">See also</span></span>

- <span data-ttu-id="64835-207">Usar [Pesquisas de Log](log-analytics-log-searches.md) no Log Analytics para exibir dados detalhados do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="64835-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="64835-208">[Criar seus próprios painéis](log-analytics-dashboards.md) mostrando os dados do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="64835-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="64835-209">[Criar alertas](log-analytics-alerts.md) quando ocorrerem eventos específicos do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="64835-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
