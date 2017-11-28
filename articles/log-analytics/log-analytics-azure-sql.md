---
title: "aaaAzure solução de análise do SQL na análise de Log | Microsoft Docs"
description: "Olá solução de análise do SQL Azure ajuda a gerenciar seus bancos de dados do SQL Azure."
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
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="76c12-103">Monitorar o Banco de Dados SQL do Azure usando a Análise do Azure SQL (Visualização) no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="76c12-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Símbolo da Análise de SQL do Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="76c12-105">Olá solução de análise do SQL Azure no Azure Log Analytics coleta e visualiza as métricas importantes de desempenho do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="76c12-106">Usando métricas Olá coletados com solução hello, você pode criar regras personalizadas de monitoramentos e alertas.</span><span class="sxs-lookup"><span data-stu-id="76c12-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="76c12-107">E você pode monitorar o Banco de Dados SQL e métricas de pool elástico em várias assinaturas do Azure e pools elásticos e visualizá-los.</span><span class="sxs-lookup"><span data-stu-id="76c12-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="76c12-108">Olá solução também ajuda a tooidentify problemas em cada camada da pilha de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="76c12-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="76c12-109">Ele usa [métricas de diagnóstico do Azure](log-analytics-azure-storage.md) junto com a análise de Log exibições toopresent dados sobre todos os bancos de dados SQL do Azure e pools Elásticos em um único espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="76c12-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="76c12-110">No momento, esta solução visualização dá suporte para até too150, 000 bancos de dados do SQL do Azure e 5.000 Pools Elásticos de SQL por espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="76c12-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="76c12-111">Olá solução de análise do SQL Azure, como outros disponíveis para análise de Log ajuda a monitorar e receber notificações sobre integridade de saudação de seus recursos do Azure – nesse caso, o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="76c12-112">Banco de dados SQL do Microsoft Azure é um serviço de banco de dados relacional escalonável que fornece familiar tooapplications de recursos de tipo de SQL Server em execução no hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="76c12-113">Análise de log ajuda a toocollect, correlacionar e visualizar dados estruturados e não estruturados.</span><span class="sxs-lookup"><span data-stu-id="76c12-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="76c12-114">Fontes conectadas</span><span class="sxs-lookup"><span data-stu-id="76c12-114">Connected sources</span></span>

<span data-ttu-id="76c12-115">Olá solução de análise do SQL Azure não usa agentes tooconnect toohello serviço de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="76c12-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="76c12-116">Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução.</span><span class="sxs-lookup"><span data-stu-id="76c12-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="76c12-117">Fonte Conectada</span><span class="sxs-lookup"><span data-stu-id="76c12-117">Connected Source</span></span> | <span data-ttu-id="76c12-118">Suporte</span><span class="sxs-lookup"><span data-stu-id="76c12-118">Support</span></span> | <span data-ttu-id="76c12-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="76c12-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="76c12-120">Agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="76c12-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="76c12-121">Não</span><span class="sxs-lookup"><span data-stu-id="76c12-121">No</span></span> | <span data-ttu-id="76c12-122">Direcione os agentes não são usados pela solução de saudação do Windows.</span><span class="sxs-lookup"><span data-stu-id="76c12-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="76c12-123">Agentes do Linux</span><span class="sxs-lookup"><span data-stu-id="76c12-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="76c12-124">Não</span><span class="sxs-lookup"><span data-stu-id="76c12-124">No</span></span> | <span data-ttu-id="76c12-125">Direcione os agentes não são usados pela solução de saudação do Linux.</span><span class="sxs-lookup"><span data-stu-id="76c12-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="76c12-126">Grupo de gerenciamento do SCOM</span><span class="sxs-lookup"><span data-stu-id="76c12-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="76c12-127">Não</span><span class="sxs-lookup"><span data-stu-id="76c12-127">No</span></span> | <span data-ttu-id="76c12-128">Uma conexão direta de saudação SCOM agente tooLog Analytics não é usada pela solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c12-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="76c12-129">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="76c12-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="76c12-130">Não</span><span class="sxs-lookup"><span data-stu-id="76c12-130">No</span></span> | <span data-ttu-id="76c12-131">Análise de log não lê dados saudação de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76c12-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="76c12-132">Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="76c12-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="76c12-133">Sim</span><span class="sxs-lookup"><span data-stu-id="76c12-133">Yes</span></span> | <span data-ttu-id="76c12-134">Dados de métrica do Azure são enviados tooLog análise diretamente pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="76c12-135">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76c12-135">Prerequisites</span></span>

- <span data-ttu-id="76c12-136">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-136">An Azure Subscription.</span></span> <span data-ttu-id="76c12-137">Se não tiver uma, você poderá criá-la [grátis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="76c12-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="76c12-138">Um espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="76c12-138">A Log Analytics workspace.</span></span> <span data-ttu-id="76c12-139">Você pode usar um existente ou pode [criar um novo](log-analytics-get-started.md) para começar a usar essa solução.</span><span class="sxs-lookup"><span data-stu-id="76c12-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="76c12-140">Habilitar o diagnóstico do Azure para seus bancos de dados SQL do Azure e pools Elásticos e [configurá-las toosend tooLog seus dados análise](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="76c12-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="76c12-141">Configuração</span><span class="sxs-lookup"><span data-stu-id="76c12-141">Configuration</span></span>

<span data-ttu-id="76c12-142">Execute Olá etapas tooadd Olá análise do SQL Azure solução tooyour espaço de trabalho a seguir.</span><span class="sxs-lookup"><span data-stu-id="76c12-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="76c12-143">Adicionar espaço de trabalho do hello análise do SQL Azure solução tooyour em [do Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="76c12-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="76c12-144">No portal do Azure de Olá, clique em **novo** (Olá símbolo de +), na lista de saudação de recursos, selecione **monitoramento + gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="76c12-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="76c12-145">![Monitoramento + Gerenciamento](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="76c12-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="76c12-146">Em Olá **monitoramento + gerenciamento** lista, clique em **ver todos os**.</span><span class="sxs-lookup"><span data-stu-id="76c12-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="76c12-147">Em Olá **recomendado** lista, clique em **mais** e, em seguida, na lista de novos hello, localize **análise do SQL Azure (visualização)** e, em seguida, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="76c12-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="76c12-148">![Solução de Análise do Azure SQL](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="76c12-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="76c12-149">Em Olá **análise do SQL Azure (visualização)** folha, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="76c12-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="76c12-150">![Criar](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="76c12-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="76c12-151">Em Olá **criar nova solução** folha, no espaço de trabalho Olá selecione que você deseja tooadd Olá solução tooand e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="76c12-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="76c12-152">![Adicionar tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="76c12-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="76c12-153">tooconfigure várias assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="76c12-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="76c12-154">toosupport várias assinaturas, use o script do PowerShell de saudação do [log de métricas de recursos de habilitar o Azure usando o PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="76c12-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="76c12-155">Fornece Olá ID de recurso de espaço de trabalho como um parâmetro ao executar dados de diagnóstico Olá script toosend de recursos no espaço de trabalho de tooa de uma assinatura do Azure em outra assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="76c12-156">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="76c12-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="76c12-157">Usando a solução de saudação</span><span class="sxs-lookup"><span data-stu-id="76c12-157">Using hello solution</span></span>

<span data-ttu-id="76c12-158">Quando você adiciona o espaço de trabalho do hello solução tooyour, Olá bloco de análise do SQL Azure é adicionado tooyour espaço de trabalho, e ele aparece na visão geral.</span><span class="sxs-lookup"><span data-stu-id="76c12-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="76c12-159">bloco Olá mostra o número de saudação de bancos de dados SQL do Azure e pools Elásticos do SQL Azure conectado à solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c12-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Bloco de Análise do SQL Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="76c12-161">Exibindo dados da Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="76c12-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="76c12-162">Clique em Olá **análise do SQL Azure** o painel de controle do bloco tooopen Olá análise do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="76c12-163">Painel de saudação inclui folhas Olá definidas abaixo.</span><span class="sxs-lookup"><span data-stu-id="76c12-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="76c12-164">Cada folha lista os recursos de too15 (assinatura, server, pool Elástico e banco de dados).</span><span class="sxs-lookup"><span data-stu-id="76c12-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="76c12-165">Clique em qualquer painel da saudação tooopen Olá recursos para o recurso específico.</span><span class="sxs-lookup"><span data-stu-id="76c12-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="76c12-166">Banco de dados ou Pool Elástico contém gráficos-Olá com métricas para um recurso selecionado.</span><span class="sxs-lookup"><span data-stu-id="76c12-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="76c12-167">Clique em uma caixa de diálogo de pesquisa de Log de saudação do tooopen de gráfico.</span><span class="sxs-lookup"><span data-stu-id="76c12-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="76c12-168">Folha</span><span class="sxs-lookup"><span data-stu-id="76c12-168">Blade</span></span> | <span data-ttu-id="76c12-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="76c12-169">Description</span></span> |
|---|---|
| <span data-ttu-id="76c12-170">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="76c12-170">Subscriptions</span></span> | <span data-ttu-id="76c12-171">Lista de assinaturas com o número de servidores, pools e bancos de dados conectados.</span><span class="sxs-lookup"><span data-stu-id="76c12-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="76c12-172">Servidores</span><span class="sxs-lookup"><span data-stu-id="76c12-172">Servers</span></span> | <span data-ttu-id="76c12-173">Lista de servidores com o número de pools e bancos de dados conectados.</span><span class="sxs-lookup"><span data-stu-id="76c12-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="76c12-174">Pools elásticos</span><span class="sxs-lookup"><span data-stu-id="76c12-174">Elastic Pools</span></span> | <span data-ttu-id="76c12-175">Lista de pools Elásticos conectados com máximo GB e eDTU em Olá observado período.</span><span class="sxs-lookup"><span data-stu-id="76c12-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="76c12-176">Bancos de dados</span><span class="sxs-lookup"><span data-stu-id="76c12-176">Databases</span></span> | <span data-ttu-id="76c12-177">Lista de bancos de dados conectados com GB e DTU máximo em Olá observado período.</span><span class="sxs-lookup"><span data-stu-id="76c12-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="76c12-178">Analisar dados e criar alertas</span><span class="sxs-lookup"><span data-stu-id="76c12-178">Analyze data and create alerts</span></span>

<span data-ttu-id="76c12-179">Facilmente, você pode criar alertas com dados Olá provenientes de recursos do Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="76c12-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="76c12-180">Aqui estão algumas das consultas de [pesquisa de logs](log-analytics-log-searches.md) úteis que você pode usar para alertas:</span><span class="sxs-lookup"><span data-stu-id="76c12-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="76c12-181">*DTU alta no Banco de Dados SQL do Azure*</span><span class="sxs-lookup"><span data-stu-id="76c12-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="76c12-182">*Alta DTU no pool elástico do Banco de Dados SQL do Azure*</span><span class="sxs-lookup"><span data-stu-id="76c12-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="76c12-183">Você pode usar essas consultas com base no alerta tooalert em limites específicos para o banco de dados do SQL Azure e pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="76c12-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="76c12-184">tooconfigure um alerta para seu espaço de trabalho do OMS:</span><span class="sxs-lookup"><span data-stu-id="76c12-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="76c12-185">tooconfigure um alerta para seu espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="76c12-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="76c12-186">Vá toohello [portal do OMS](http://mms.microsoft.com/) e entrar.</span><span class="sxs-lookup"><span data-stu-id="76c12-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="76c12-187">Abra o espaço de trabalho de saudação que você configurou para solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c12-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="76c12-188">Na página de visão geral de saudação, clique em Olá **análise do SQL Azure (visualização)** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="76c12-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="76c12-189">Execute uma das consultas de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="76c12-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="76c12-190">Na Pesquisa de Log, clique em **Alerta**.</span><span class="sxs-lookup"><span data-stu-id="76c12-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="76c12-191">![criar alerta na pesquisa](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="76c12-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="76c12-192">Em Olá **Adicionar regra de alerta** página, defina propriedades adequadas hello e Olá limites específicos que você deseja e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="76c12-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="76c12-193">![adicionar regra de alerta](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="76c12-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="76c12-194">Tomar decisões com base em dados da Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="76c12-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="76c12-195">Por exemplo, uma das consultas de hello mais úteis que você pode executar é toocompare utilização de DTU Olá para todos os Pools de Elástico do SQL Azure em todas as suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="76c12-196">Unidade de taxa de transferência de banco de dados (DTU) fornece uma maneira toodescribe Olá a capacidade relativa de um nível de desempenho de pools e os bancos de dados Basic, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="76c12-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="76c12-197">DTUs são baseadas em uma medida combinada de CPU, memória, leituras e gravações.</span><span class="sxs-lookup"><span data-stu-id="76c12-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="76c12-198">Quando as DTUs aumentam, Olá capacidade oferecida pelo aumento de nível de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c12-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="76c12-199">Por exemplo, um nível de desempenho com cinco DTUs tem cinco vezes mais energia do que um nível de desempenho com uma DTU.</span><span class="sxs-lookup"><span data-stu-id="76c12-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="76c12-200">Uma cota DTU máxima aplica-se o pool de servidor e elástica tooeach.</span><span class="sxs-lookup"><span data-stu-id="76c12-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="76c12-201">Executando Olá consulta de pesquisa de Log a seguir, você pode dizer facilmente se você subutilização ou mais utilizar os pools Elásticos do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="76c12-202">Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá acima consulta alteraria toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="76c12-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="76c12-203">Saudação de exemplo a seguir, você pode ver um pool Elástico tem um alto uso quase 100% enquanto outros têm muito pouca utilização DTU.</span><span class="sxs-lookup"><span data-stu-id="76c12-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="76c12-204">Você pode investigar mais tootroubleshoot recentes alterações em potencial em seu ambiente usando logs de atividades do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Resultados de pesquisa de log - alta utilização](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="76c12-206">Consulte também</span><span class="sxs-lookup"><span data-stu-id="76c12-206">See also</span></span>

- <span data-ttu-id="76c12-207">Use [pesquisas de Log](log-analytics-log-searches.md) no tooview de análise de Log detalhado de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="76c12-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="76c12-208">[Criar seus próprios painéis](log-analytics-dashboards.md) mostrando os dados do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="76c12-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="76c12-209">[Criar alertas](log-analytics-alerts.md) quando ocorrerem eventos específicos do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="76c12-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
