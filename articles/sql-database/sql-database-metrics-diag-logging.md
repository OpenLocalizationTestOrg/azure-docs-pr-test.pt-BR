---
title: "aaaAzure SQL de banco de dados métricas & log de diagnóstico | Microsoft Docs"
description: "Saiba mais sobre como configurar o uso de recursos do banco de dados do Azure SQL recursos toostore, conectividade e as estatísticas de execução de consulta."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="e7d4e-103">Métricas de banco de dados SQL do Azure e o log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e7d4e-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="e7d4e-104">O Banco de Dados SQL do Azure pode emitir métrica e logs de diagnóstico para facilitar o monitoramento.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="e7d4e-105">Você pode configurar o uso de recursos do banco de dados do Azure SQL toostore, trabalhadores e sessões e conectividade em um desses recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-105">You can configure Azure SQL Database toostore resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="e7d4e-106">**Armazenamento do Azure**: para o arquivamento de grandes quantidades de telemetria por um pequeno baixo</span><span class="sxs-lookup"><span data-stu-id="e7d4e-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="e7d4e-107">**Hub de Eventos do Azure**: para a integração de telemetria de Banco de Dados SQL do Azure com a sua solução de monitoramento personalizada ou pipelines ativos</span><span class="sxs-lookup"><span data-stu-id="e7d4e-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="e7d4e-108">**Análise de logs do Azure**: para fora da caixa Olá solução com relatórios, alertas e redução de recursos de monitoramento</span><span class="sxs-lookup"><span data-stu-id="e7d4e-108">**Azure Log Analytics**: For out of hello box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![Arquitetura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="e7d4e-110">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="e7d4e-110">Enable logging</span></span>

<span data-ttu-id="e7d4e-111">Métricas e log de diagnóstico não está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="e7d4e-112">Você pode habilitar e gerenciar o log de diagnóstico usando um dos métodos a seguir de saudação e métricas:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-112">You can enable and manage metrics and diagnostics logging using one of hello following methods:</span></span>
- <span data-ttu-id="e7d4e-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-113">Azure portal</span></span>
- <span data-ttu-id="e7d4e-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d4e-114">PowerShell</span></span>
- <span data-ttu-id="e7d4e-115">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-115">Azure CLI</span></span>
- <span data-ttu-id="e7d4e-116">API REST</span><span class="sxs-lookup"><span data-stu-id="e7d4e-116">REST API</span></span> 
- <span data-ttu-id="e7d4e-117">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e7d4e-117">Resource Manager template</span></span>

<span data-ttu-id="e7d4e-118">Quando você habilitar o log de diagnóstico e métricas, você precisa toospecify Olá recursos do Azure, onde os dados selecionados são coletados.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-118">When you enable metrics and diagnostics logging, you need toospecify hello Azure resource where selected data is collected.</span></span> <span data-ttu-id="e7d4e-119">Opções disponíveis:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-119">Options available:</span></span>
- <span data-ttu-id="e7d4e-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e7d4e-120">Log analytics</span></span>
- <span data-ttu-id="e7d4e-121">Hub de evento</span><span class="sxs-lookup"><span data-stu-id="e7d4e-121">Event Hub</span></span>
- <span data-ttu-id="e7d4e-122">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-122">Azure Storage</span></span> 

<span data-ttu-id="e7d4e-123">Você pode provisionar um novo recurso do Azure ou selecionar um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="e7d4e-124">Depois de selecionar o recurso de armazenamento Olá, é necessário toospecify toocollect os dados.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-124">After selecting hello storage resource, you need toospecify which data toocollect.</span></span> <span data-ttu-id="e7d4e-125">As opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-125">Options available include:</span></span>

- <span data-ttu-id="e7d4e-126">**[métricas de 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**  - contém o percentual DTU, o limite DTU, o percentual de CPU, porcentagem de leitura de dados físicos, porcentagem de gravação de log, êxito/falha/bloqueados por conexões de firewall, porcentagem de sessões, porcentagem de funcionários, armazenamento, porcentagem de armazenamento, porcentagem de armazenamento XTP</span><span class="sxs-lookup"><span data-stu-id="e7d4e-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="e7d4e-127">Se você especificar uma conta de AzureStorage ou Hub de eventos, você pode especificar um toospecify de política de retenção que os dados mais antigos do que um período de tempo é excluído.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy toospecify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="e7d4e-128">Se você especificar a análise de Log, política de retenção Olá depende de camada de preços selecionada hello.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-128">If you specify Log Analytics, hello retention policy depends on hello selected pricing tier.</span></span> <span data-ttu-id="e7d4e-129">Saiba mais sobre [Preço do Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="e7d4e-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="e7d4e-130">É recomendável que você leia os dois Olá [visão geral das métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigos toogain entender não apenas como tooenable registro em log, mas Olá categorias de log e métricas suporte Olá vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-130">We recommend that you read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e7d4e-131">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-131">Azure portal</span></span>

<span data-ttu-id="e7d4e-132">métricas de tooenable e coleta de logs de diagnóstico Olá portal do Azure, navegue tooyour banco de dados do SQL Azure ou página de pool Elástico e, em seguida, clique em **configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-132">tooenable metrics and diagnostic logs collection in hello Azure portal, navigate tooyour Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![Habilitar a saudação portal do Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="e7d4e-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d4e-134">PowerShell</span></span>

<span data-ttu-id="e7d4e-135">métricas de tooenable e o log de diagnóstico usando o PowerShell, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-135">tooenable metrics and diagnostics logging using PowerShell, use hello following commands:</span></span>

- <span data-ttu-id="e7d4e-136">armazenamento de tooenable dos Logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-136">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="e7d4e-137">Olá ID da conta de armazenamento é a id de recurso de saudação para Olá toowhich de conta de armazenamento você deseja toosend Olá logs.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-137">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="e7d4e-138">tooenable streaming de Logs de diagnóstico tooan Hub de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-138">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="e7d4e-139">Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-139">hello Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="e7d4e-140">Enviar tooenable do espaço de trabalho de análise de Log de tooa Logs de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-140">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="e7d4e-141">Você pode obter a id de recurso de saudação do seu espaço de trabalho de análise de Log usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-141">You can obtain hello resource id of your Log Analytics workspace using hello following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="e7d4e-142">Você pode combinar várias opções de saída para tooenable esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-142">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="e7d4e-143">CLI</span><span class="sxs-lookup"><span data-stu-id="e7d4e-143">CLI</span></span>

<span data-ttu-id="e7d4e-144">métricas de tooenable e logs de diagnóstico usando Olá CLI do Azure, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-144">tooenable metrics and diagnostics logging using hello Azure CLI, use hello following commands:</span></span>

- <span data-ttu-id="e7d4e-145">armazenamento de tooenable dos Logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-145">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="e7d4e-146">Olá ID da conta de armazenamento é a id de recurso de saudação para Olá toowhich de conta de armazenamento você deseja toosend Olá logs.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-146">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="e7d4e-147">tooenable streaming de Logs de diagnóstico tooan Hub de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-147">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="e7d4e-148">Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-148">hello Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="e7d4e-149">Enviar tooenable do espaço de trabalho de análise de Log de tooa Logs de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-149">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

<span data-ttu-id="e7d4e-150">Você pode combinar várias opções de saída para tooenable esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-150">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="e7d4e-151">API REST</span><span class="sxs-lookup"><span data-stu-id="e7d4e-151">REST API</span></span>

<span data-ttu-id="e7d4e-152">Leia mais sobre como muito[alterar configurações de diagnóstico usando Olá API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7d4e-152">Read about how too[change Diagnostic settings using hello Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="e7d4e-153">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e7d4e-153">Resource Manager template</span></span>

<span data-ttu-id="e7d4e-154">Leia mais sobre como muito[Habilitar configurações de diagnóstico na criação de recursos usando o modelo do Gerenciador de recursos](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="e7d4e-154">Read about how too[enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="e7d4e-155">Fluxo em Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e7d4e-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="e7d4e-156">Métricas de banco de dados SQL do Azure e logs de diagnóstico podem ser transmitidos em análise de Log usando a opção de internos "enviar tooLog análise" de saudação no portal de hello, ou habilitar análise de Log em uma configuração de diagnóstica por meio de cmdlets do PowerShell do Azure, CLI do Azure ou Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using hello built-in “Send tooLog Analytics” option in hello portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="e7d4e-157">Visão geral da instalação</span><span class="sxs-lookup"><span data-stu-id="e7d4e-157">Installation overview</span></span>

<span data-ttu-id="e7d4e-158">Monitorar fleet de banco de dados SQL do Azure é simples com Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="e7d4e-159">Três etapas são necessárias:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-159">Three steps are required:</span></span>

1.  <span data-ttu-id="e7d4e-160">Criar recursos de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e7d4e-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="e7d4e-161">Configurar métricas de toorecord de bancos de dados e logs de diagnóstico em Olá criado análise de Log</span><span class="sxs-lookup"><span data-stu-id="e7d4e-161">Configure databases toorecord metrics and diagnostic logs into hello created Log Analytics</span></span>
3.  <span data-ttu-id="e7d4e-162">Instalar a solução de **Análise de SQL do Azure** na galeria do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e7d4e-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="e7d4e-163">Criar recursos de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e7d4e-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="e7d4e-164">Clique em **novo** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-164">Click **New** in hello left-hand menu.</span></span>
2. <span data-ttu-id="e7d4e-165">Clique em **Monitoramento + Gerenciamento**</span><span class="sxs-lookup"><span data-stu-id="e7d4e-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="e7d4e-166">Clique em **Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="e7d4e-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="e7d4e-167">Preencha o formulário de análise de Log de saudação com informações adicionais de saudação necessárias: nome do espaço de trabalho, assinatura, grupo de recursos, local e preço.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-167">Fill in hello Log Analytics form with hello additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![log analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a><span data-ttu-id="e7d4e-169">Configurar métricas de toorecord de bancos de dados e logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e7d4e-169">Configure databases toorecord metrics and diagnostic logs</span></span>

<span data-ttu-id="e7d4e-170">Olá tooconfigure de maneira mais fácil onde os bancos de dados registram suas métricas é por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-170">hello easiest way tooconfigure where databases record their metrics is through hello Azure portal.</span></span> <span data-ttu-id="e7d4e-171">Olá portal do Azure, navegue tooyour recursos de banco de dados SQL em e clique em **as configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-171">In hello Azure portal, navigate tooyour Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="e7d4e-172">Instale a solução de análise do SQL Azure de saudação da Galeria</span><span class="sxs-lookup"><span data-stu-id="e7d4e-172">Install hello Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="e7d4e-173">Depois Olá recursos de análise de Log é criado e seus dados estão fluindo nele, instale a solução de análise do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-173">Once hello Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="e7d4e-174">Isso pode ser feito por meio de saudação **Galeria de soluções** que você pode encontrar na home page do OMS hello e no menu do lado de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-174">This can be done through hello **Solutions Gallery** that you can find on hello OMS homepage and in hello side menu.</span></span> <span data-ttu-id="e7d4e-175">Na Galeria de hello, localize e clique em **análise do SQL Azure** solução e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-175">In hello gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![solução de monitoramento](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="e7d4e-177">Na home page do seu OMS, um novo bloco chamado **Análise de SQL do Azure** é exibido.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="e7d4e-178">Selecionar este bloco abre o painel de análise do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-178">Selecting this tile opens hello Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="e7d4e-179">Usando a solução de Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="e7d4e-180">Análise do SQL Azure é um painel hierárquico que permite que você toonavigate pela hierarquia de saudação de recursos de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-180">Azure SQL Analytics is a hierarchical dashboard that allows you toonavigate through hello hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="e7d4e-181">Isso permite que o recurso você toodo alto nível de monitoramento mas ele também permite que você tooscope seu monitoramento Olá toojust certo conjunto de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-181">This capability enables you toodo high-level monitoring but it also enables you tooscope your monitoring toojust hello right set of resources.</span></span>
<span data-ttu-id="e7d4e-182">Painel contém listas de saudação de recursos diferentes em recursos da saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-182">Dashboard contains hello lists of different resources under hello selected resource.</span></span> <span data-ttu-id="e7d4e-183">Por exemplo, para uma assinatura selecionada consulte Olá todos os servidores, pools Elásticos e bancos de dados que pertencem a toohello selecionados a assinatura.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-183">For example, for a selected subscription you can see hello all servers, elastic pools and databases that belong toohello selected subscription.</span></span> <span data-ttu-id="e7d4e-184">Além disso, para Pools Elásticos e bancos de dados, você pode ver métricas de uso de recursos de saudação do recurso.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-184">Additionally, for Elastic Pools and databases, you can see hello resource usage metrics of that resource.</span></span> <span data-ttu-id="e7d4e-185">Isso inclui gráficos para DTU, CPU, IO, LOG, sessões, operadores, conexões e armazenamento em GB.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="e7d4e-186">Fluxo no Hub de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="e7d4e-187">Métricas de banco de dados SQL do Azure e logs de diagnóstico podem ser transmitidos para o Hub de eventos usando a opção de internos "fluxo tooan hub de eventos" hello no portal de hello, ou habilitando o Id de regra de barramento de serviço em uma configuração de diagnóstica por meio de Cmdlets do PowerShell do Azure, CLI do Azure ou Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using hello built-in “Stream tooan event hub” option in hello portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="e7d4e-188">Quais toodo com métricas e logs de diagnóstico no Hub de eventos?</span><span class="sxs-lookup"><span data-stu-id="e7d4e-188">What toodo with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="e7d4e-189">Quando dados saudação selecionado são transmitidos para o Hub de eventos, você estará um tooenabling mais próxima etapa cenários de monitoramentos avançados.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-189">Once hello selected data is streamed into Event Hub, you are one step closer tooenabling advanced monitoring scenarios.</span></span> <span data-ttu-id="e7d4e-190">Hubs de eventos age como hello "porta da frente" para um pipeline de eventos, e depois que os dados são coletados em um Hub de eventos que pode ser transformado e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-190">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="e7d4e-191">Hubs de eventos separa a produção de hello de um fluxo de eventos do consumo Olá desses eventos, para que os consumidores de evento possam acessar eventos de saudação em suas próprias agendas.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-191">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span> <span data-ttu-id="e7d4e-192">Para obter mais informações sobre o Hub de eventos, consulte:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="e7d4e-193">[O que são Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="e7d4e-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="e7d4e-194">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="e7d4e-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="e7d4e-195">Aqui estão algumas maneiras que você pode usar o hello capacidade para streaming:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-195">Here are just a few ways you might use hello streaming capability:</span></span>

-   <span data-ttu-id="e7d4e-196">Exibir a integridade do serviço facilmente por streaming "afunilamento" dados tooPowerBI - usando Hubs de eventos, análise de fluxo e Power BI, você pode transformar seus dados de métricas e diagnóstico para perto de informações em tempo real em seus serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-196">View service health by streaming “hot path” data tooPowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="e7d4e-197">Para uma visão geral de como tooset a dos Hubs de eventos, processar dados com a análise de fluxo e usar o Power BI como uma saída, consulte [do Stream Analytics e o Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="e7d4e-197">For an overview of how tooset up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="e7d4e-198">Fluxo logs toothird terceiros registro em log e telemetria fluxos – usando os Hubs de eventos streaming, você podem obter seus logs de diagnóstico e métricas toodifferent soluções de análise de log e de monitoramento de terceiros.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-198">Stream logs toothird-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in toodifferent third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="e7d4e-199">Crie uma telemetria personalizada e a plataforma de log – se você já tem uma plataforma de telemetria personalizada ou estão pensando sobre como criar um, Olá altamente escalonável de publicação / assinatura natureza dos Hubs de eventos permite que você tooflexibly ingestão logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="e7d4e-200">Consulte [toousing de guia de Dan Rosanova Hubs de eventos em uma plataforma de telemetria de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="e7d4e-200">See [Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="e7d4e-201">Fluxo no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-201">Stream into Azure Storage</span></span>

<span data-ttu-id="e7d4e-202">Métricas de banco de dados SQL do Azure e logs de diagnóstico podem ser armazenados no armazenamento do Azure usando a opção Olá interna "Arquivar a conta de armazenamento tooa" em Olá portal do Azure, ou habilitando o armazenamento do Azure em uma configuração de diagnóstica por meio de Cmdlets do PowerShell do Azure, CLI do Azure ou do Azure API de REST do monitor.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using hello built-in "Archive tooa storage account” option in hello Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="e7d4e-203">Esquema de métricas e logs de diagnóstico na conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="e7d4e-203">Schema of metrics and diagnostic logs in hello storage account</span></span>

<span data-ttu-id="e7d4e-204">Depois que você configurar as métricas e coleta de logs de diagnóstico, um contêiner de armazenamento é criado na conta de armazenamento Olá selecionada durante as primeiras linhas de saudação de dados estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in hello storage account you selected when hello first rows of data are available.</span></span> <span data-ttu-id="e7d4e-205">estrutura Olá esses blobs é:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-205">hello structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="e7d4e-206">Ou, simplesmente:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="e7d4e-207">Por exemplo, um nome de blob para métricas de 1 minuto pode ser:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="e7d4e-208">Caso você deseje toorecord dados Olá Olá Pool Elástico, nome do blob é um pouco diferente:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-208">In case you want toorecord hello data from hello Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="e7d4e-209">Baixar logs e métricas do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e7d4e-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="e7d4e-210">Consulte [Baixar métricas e logs de diagnósticos do Armazenamento do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="e7d4e-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="e7d4e-211">métricas de 1 minuto</span><span class="sxs-lookup"><span data-stu-id="e7d4e-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="e7d4e-212">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="e7d4e-212">**Resource**</span></span>|<span data-ttu-id="e7d4e-213">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="e7d4e-213">**Metrics**</span></span>|
|<span data-ttu-id="e7d4e-214">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="e7d4e-214">Database</span></span>|<span data-ttu-id="e7d4e-215">porcentagem de DTU, DTU usado, o limite DTU, o porcentagem de CPU, porcentagem de leitura de dados físicos, porcentagem de gravação de log, êxito/falha/bloqueados por conexões de firewall, porcentagem de sessões, porcentagem de funcionários, armazenamento, porcentagem de armazenamento, porcentagem de armazenamento XTP, deadlocks</span><span class="sxs-lookup"><span data-stu-id="e7d4e-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="e7d4e-216">Pool elástico</span><span class="sxs-lookup"><span data-stu-id="e7d4e-216">Elastic pool</span></span>|<span data-ttu-id="e7d4e-217">porcentagem de eDTU, eDTU usado, o limite eDTU, porcentagem de CPU, porcentagem de leitura de dados físicos, porcentagem de gravação de log, porcentagem de sessões, porcentagem de funcionários, armazenamento, porcentagem de armazenamento, limite de armazenamento, porcentagem de armazenamento XTP</span><span class="sxs-lookup"><span data-stu-id="e7d4e-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="e7d4e-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7d4e-218">Next steps</span></span>

- <span data-ttu-id="e7d4e-219">Ler os dois Olá [visão geral das métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigos toogain entender não apenas como tooenable log, mas Olá métricas e categorias de log suporte Olá vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d4e-219">Read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>
- <span data-ttu-id="e7d4e-220">Leia essas toolearn artigos sobre hubs de eventos:</span><span class="sxs-lookup"><span data-stu-id="e7d4e-220">Read these articles toolearn about event hubs:</span></span>
   - <span data-ttu-id="e7d4e-221">[O que são Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="e7d4e-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="e7d4e-222">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="e7d4e-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="e7d4e-223">Consulte [Baixar métricas e logs de diagnósticos do Armazenamento do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="e7d4e-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
