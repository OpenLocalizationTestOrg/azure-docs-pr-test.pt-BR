---
title: "Métricas de banco de dados SQL do Azure e o log de diagnóstico | Microsoft Docs"
description: "Saiba mais sobre como configurar recursos de banco de dados SQL do Azure para armazenar as estatísticas de execução de consulta, conectividade e uso de recursos."
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
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="2627f-103">Métricas de banco de dados SQL do Azure e o log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="2627f-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="2627f-104">O Banco de Dados SQL do Azure pode emitir métrica e logs de diagnóstico para facilitar o monitoramento.</span><span class="sxs-lookup"><span data-stu-id="2627f-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="2627f-105">Você pode configurar o Banco de Dados SQL do Azure para armazenar o uso de recursos, trabalhos, sessões e conectividade em um destes recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="2627f-105">You can configure Azure SQL Database to store resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="2627f-106">**Armazenamento do Azure**: para o arquivamento de grandes quantidades de telemetria por um pequeno baixo</span><span class="sxs-lookup"><span data-stu-id="2627f-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="2627f-107">**Hub de Eventos do Azure**: para a integração de telemetria de Banco de Dados SQL do Azure com a sua solução de monitoramento personalizada ou pipelines ativos</span><span class="sxs-lookup"><span data-stu-id="2627f-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="2627f-108">**Análise de logs do Azure**: Para solução de monitoramento fora da caixa com relatórios, alertas e recursos de mitigação</span><span class="sxs-lookup"><span data-stu-id="2627f-108">**Azure Log Analytics**: For out of the box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![Arquitetura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="2627f-110">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="2627f-110">Enable logging</span></span>

<span data-ttu-id="2627f-111">Métricas e log de diagnóstico não está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="2627f-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="2627f-112">Você pode habilitar e gerenciar as métricas e diagnóstico de log usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="2627f-112">You can enable and manage metrics and diagnostics logging using one of the following methods:</span></span>
- <span data-ttu-id="2627f-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-113">Azure portal</span></span>
- <span data-ttu-id="2627f-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2627f-114">PowerShell</span></span>
- <span data-ttu-id="2627f-115">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-115">Azure CLI</span></span>
- <span data-ttu-id="2627f-116">API REST</span><span class="sxs-lookup"><span data-stu-id="2627f-116">REST API</span></span> 
- <span data-ttu-id="2627f-117">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2627f-117">Resource Manager template</span></span>

<span data-ttu-id="2627f-118">Quando você habilitar o log de diagnóstico e métricas, você precisa especificar os recursos do Azure, onde os dados selecionados são coletados.</span><span class="sxs-lookup"><span data-stu-id="2627f-118">When you enable metrics and diagnostics logging, you need to specify the Azure resource where selected data is collected.</span></span> <span data-ttu-id="2627f-119">Opções disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2627f-119">Options available:</span></span>
- <span data-ttu-id="2627f-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2627f-120">Log analytics</span></span>
- <span data-ttu-id="2627f-121">Hub de evento</span><span class="sxs-lookup"><span data-stu-id="2627f-121">Event Hub</span></span>
- <span data-ttu-id="2627f-122">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-122">Azure Storage</span></span> 

<span data-ttu-id="2627f-123">Você pode provisionar um novo recurso do Azure ou selecionar um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="2627f-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="2627f-124">Depois de selecionar o recurso de armazenamento, você precisa especificar quais dados coletar.</span><span class="sxs-lookup"><span data-stu-id="2627f-124">After selecting the storage resource, you need to specify which data to collect.</span></span> <span data-ttu-id="2627f-125">As opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="2627f-125">Options available include:</span></span>

- <span data-ttu-id="2627f-126">**[métricas de 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**  - contém o percentual DTU, o limite DTU, o percentual de CPU, porcentagem de leitura de dados físicos, porcentagem de gravação de log, êxito/falha/bloqueados por conexões de firewall, porcentagem de sessões, porcentagem de funcionários, armazenamento, porcentagem de armazenamento, porcentagem de armazenamento XTP</span><span class="sxs-lookup"><span data-stu-id="2627f-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="2627f-127">Se você especificar uma conta de AzureStorage ou Hub de eventos, você pode especificar uma política de retenção para especificar que os dados mais antigos do que um período de tempo selecionado é excluído.</span><span class="sxs-lookup"><span data-stu-id="2627f-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy to specify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="2627f-128">Se você especificar a análise de Log, a política de retenção depende do tipo de preço selecionado.</span><span class="sxs-lookup"><span data-stu-id="2627f-128">If you specify Log Analytics, the retention policy depends on the selected pricing tier.</span></span> <span data-ttu-id="2627f-129">Saiba mais sobre [Preço do Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="2627f-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="2627f-130">Recomendamos que você leia os artigos [Visão geral de métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Visão geral dos Logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para entender não apenas como habilitar o registro em log, mas também as métricas e categorias de log com suporte dos vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-130">We recommend that you read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="2627f-131">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-131">Azure portal</span></span>

<span data-ttu-id="2627f-132">Para habilitar as métricas e coleta de logs de diagnóstico no portal do Azure, navegue até o banco de dados SQL Azure ou página de pool elástico e, em seguida, clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="2627f-132">To enable metrics and diagnostic logs collection in the Azure portal, navigate to your Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![habilitar no portal do Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="2627f-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2627f-134">PowerShell</span></span>

<span data-ttu-id="2627f-135">Para habilitar as métricas e o log de diagnóstico usando o PowerShell, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2627f-135">To enable metrics and diagnostics logging using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="2627f-136">Para habilitar o armazenamento dos Logs de Diagnóstico em uma Conta de Armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-136">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="2627f-137">A ID da Conta de Armazenamento é a ID de recurso da conta de armazenamento para a qual você deseja enviar os logs.</span><span class="sxs-lookup"><span data-stu-id="2627f-137">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="2627f-138">Para habilitar o streaming dos Logs de Diagnóstico para um Hub de Eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-138">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="2627f-139">A ID da Regra do Barramento de Serviço é uma cadeia de caracteres com este formato:</span><span class="sxs-lookup"><span data-stu-id="2627f-139">The Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="2627f-140">Para habilitar o envio dos Logs de Diagnóstico para um espaço de trabalho do Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-140">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="2627f-141">É possível obter a ID de recurso do seu espaço de trabalho do Log Analytics usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-141">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="2627f-142">Você pode combinar esses parâmetros para permitir várias opções de saída.</span><span class="sxs-lookup"><span data-stu-id="2627f-142">You can combine these parameters to enable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="2627f-143">CLI</span><span class="sxs-lookup"><span data-stu-id="2627f-143">CLI</span></span>

<span data-ttu-id="2627f-144">Para habilitar as métricas e o log de diagnóstico usando o CLI do Azure, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2627f-144">To enable metrics and diagnostics logging using the Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="2627f-145">Para habilitar o armazenamento dos Logs de Diagnóstico em uma Conta de Armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-145">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="2627f-146">A ID da Conta de Armazenamento é a ID de recurso da conta de armazenamento para a qual você deseja enviar os logs.</span><span class="sxs-lookup"><span data-stu-id="2627f-146">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="2627f-147">Para habilitar o streaming dos Logs de Diagnóstico para um Hub de Eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-147">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="2627f-148">A ID da Regra do Barramento de Serviço é uma cadeia de caracteres com este formato:</span><span class="sxs-lookup"><span data-stu-id="2627f-148">The Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="2627f-149">Para habilitar o envio dos Logs de Diagnóstico para um espaço de trabalho do Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="2627f-149">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="2627f-150">Você pode combinar esses parâmetros para permitir várias opções de saída.</span><span class="sxs-lookup"><span data-stu-id="2627f-150">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="2627f-151">API REST</span><span class="sxs-lookup"><span data-stu-id="2627f-151">REST API</span></span>

<span data-ttu-id="2627f-152">Saiba sobre como [alterar as Configurações de Diagnóstico usando a API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="2627f-152">Read about how to [change Diagnostic settings using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="2627f-153">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2627f-153">Resource Manager template</span></span>

<span data-ttu-id="2627f-154">Leia sobre como [habilitar as Configurações de Diagnóstico na criação do recurso usando o modelo do Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="2627f-154">Read about how to [enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="2627f-155">Fluxo em Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2627f-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="2627f-156">Métricas de banco de dados SQL do Azure e logs de diagnóstico podem ser transmitidos em Log Analytics usando a opção "Enviar para análise de Log" incorporada no portal ou, habilitando o Log Analytics em uma configuração de diagnóstico por meio de cmdlets do PowerShell do Azure, CLI do Azure ou API REST do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2627f-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using the built-in “Send to Log Analytics” option in the portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="2627f-157">Visão geral da instalação</span><span class="sxs-lookup"><span data-stu-id="2627f-157">Installation overview</span></span>

<span data-ttu-id="2627f-158">Monitorar fleet de banco de dados SQL do Azure é simples com Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2627f-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="2627f-159">Três etapas são necessárias:</span><span class="sxs-lookup"><span data-stu-id="2627f-159">Three steps are required:</span></span>

1.  <span data-ttu-id="2627f-160">Criar recursos de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2627f-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="2627f-161">Configurar bancos de dados para gravar logs de diagnóstico e métricas para o Log Analytics criado</span><span class="sxs-lookup"><span data-stu-id="2627f-161">Configure databases to record metrics and diagnostic logs into the created Log Analytics</span></span>
3.  <span data-ttu-id="2627f-162">Instalar a solução de **Análise de SQL do Azure** na galeria do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2627f-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="2627f-163">Criar recursos de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2627f-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="2627f-164">Clique em **Novo** no menu da esquerda.</span><span class="sxs-lookup"><span data-stu-id="2627f-164">Click **New** in the left-hand menu.</span></span>
2. <span data-ttu-id="2627f-165">Clique em **Monitoramento + Gerenciamento**</span><span class="sxs-lookup"><span data-stu-id="2627f-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="2627f-166">Clique em **Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="2627f-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="2627f-167">Preencha o formulário de Log Analytics com as informações adicionais necessárias: nome do espaço de trabalho, assinatura, grupo de recursos, local e tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="2627f-167">Fill in the Log Analytics form with the additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![log analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a><span data-ttu-id="2627f-169">Configurar bancos de dados para gravar logs de diagnóstico e métricas</span><span class="sxs-lookup"><span data-stu-id="2627f-169">Configure databases to record metrics and diagnostic logs</span></span>

<span data-ttu-id="2627f-170">A maneira mais fácil de configurar onde os bancos de dados registram suas métricas é por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-170">The easiest way to configure where databases record their metrics is through the Azure portal.</span></span> <span data-ttu-id="2627f-171">No portal do Azure, navegue até o recurso de banco de dados SQL do Azure e clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="2627f-171">In the Azure portal, navigate to your Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="2627f-172">Instalar a solução de Análise de SQL do Azure na galeria</span><span class="sxs-lookup"><span data-stu-id="2627f-172">Install the Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="2627f-173">Depois que o recurso de Log Analytics é criado e seus dados estão fluindo nele, instale a solução de análise de SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-173">Once the Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="2627f-174">Isso pode ser feito por meio da **Galeria de soluções** que você pode encontrar na home page do OMS e no menu lateral.</span><span class="sxs-lookup"><span data-stu-id="2627f-174">This can be done through the **Solutions Gallery** that you can find on the OMS homepage and in the side menu.</span></span> <span data-ttu-id="2627f-175">Na galeria, localize e clique em solução de **Análise de SQL do Azure** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2627f-175">In the gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![solução de monitoramento](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="2627f-177">Na home page do seu OMS, um novo bloco chamado **Análise de SQL do Azure** é exibido.</span><span class="sxs-lookup"><span data-stu-id="2627f-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="2627f-178">Selecionar este bloco abre o painel de Análise de SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-178">Selecting this tile opens the Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="2627f-179">Usando a solução de Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="2627f-180">Análise de SQL do Azure é um painel hierárquico que permite navegar pela hierarquia de recursos de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-180">Azure SQL Analytics is a hierarchical dashboard that allows you to navigate through the hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="2627f-181">Esse recurso permite que você faça o monitoramento de alto nível, mas ele também permite definir o escopo de seu monitoramento para o conjunto correto de recursos.</span><span class="sxs-lookup"><span data-stu-id="2627f-181">This capability enables you to do high-level monitoring but it also enables you to scope your monitoring to just the right set of resources.</span></span>
<span data-ttu-id="2627f-182">O painel contém a lista de recursos diferentes sob o recurso selecionado.</span><span class="sxs-lookup"><span data-stu-id="2627f-182">Dashboard contains the lists of different resources under the selected resource.</span></span> <span data-ttu-id="2627f-183">Por exemplo, para uma assinatura selecionada, você pode ver todos os servidores, pools elásticos e bancos de dados que pertencem à assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="2627f-183">For example, for a selected subscription you can see the all servers, elastic pools and databases that belong to the selected subscription.</span></span> <span data-ttu-id="2627f-184">Além disso, para Pools Elásticos e bancos de dados, você pode ver as métricas de uso de recursos daquele recurso.</span><span class="sxs-lookup"><span data-stu-id="2627f-184">Additionally, for Elastic Pools and databases, you can see the resource usage metrics of that resource.</span></span> <span data-ttu-id="2627f-185">Isso inclui gráficos para DTU, CPU, IO, LOG, sessões, operadores, conexões e armazenamento em GB.</span><span class="sxs-lookup"><span data-stu-id="2627f-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="2627f-186">Fluxo no Hub de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="2627f-187">Métricas de banco de dados SQL do Azure e logs de diagnóstico podem ser transmitidos em Hub de eventos usando a opção "Enviar para um hub de eventos" incorporada no portal ou, habilitando a Regra de Barramento de Serviço em uma configuração de diagnóstico por meio de Cmdlets do PowerShell do Azure, CLI do Azure ou API REST do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2627f-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using the built-in “Stream to an event hub” option in the portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="2627f-188">O que fazer com as métricas e os logs de diagnóstico no Hub de eventos?</span><span class="sxs-lookup"><span data-stu-id="2627f-188">What to do with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="2627f-189">Depois que os dados selecionados são transmitidos para o Hub de eventos, você está mais próximo de habilitar cenários de monitoramento avançado.</span><span class="sxs-lookup"><span data-stu-id="2627f-189">Once the selected data is streamed into Event Hub, you are one step closer to enabling advanced monitoring scenarios.</span></span> <span data-ttu-id="2627f-190">Os Hub de Eventos agem como a "porta de entrada” para um pipeline de eventos e depois que os dados são coletados em um Hub de Eventos, eles podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2627f-190">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="2627f-191">Hub de Eventos separa a produção de um fluxo de eventos do consumo desses eventos, para que os consumidores de eventos possam acessar os eventos em seu próprio cronograma.</span><span class="sxs-lookup"><span data-stu-id="2627f-191">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span> <span data-ttu-id="2627f-192">Para obter mais informações sobre o Hub de eventos, consulte:</span><span class="sxs-lookup"><span data-stu-id="2627f-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="2627f-193">[O que são Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="2627f-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="2627f-194">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="2627f-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="2627f-195">Veja algumas maneiras de usar o recurso de streaming:</span><span class="sxs-lookup"><span data-stu-id="2627f-195">Here are just a few ways you might use the streaming capability:</span></span>

-   <span data-ttu-id="2627f-196">Exibir a integridade do serviço transmitindo dados de "afunilamento" para o Power BI - Usando os Hubs de Eventos, Stream Analytics e o Power BI, é fácil transformar suas métricas e dados de diagnóstico em informações quase em tempo real nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-196">View service health by streaming “hot path” data to PowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="2627f-197">Para uma visão geral de como configurar um Hubs de Eventos, processar dados com o Stream Analytics e usar o Power BI como uma saída, consulte [Stream Analytics e Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="2627f-197">For an overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="2627f-198">Logs de fluxo para fluxos de log e telemetria de terceiros – Usando a transmissão de Hubs de eventos, você pode obter suas métricas e logs de diagnóstico para soluções de log analytics e monitoramento de terceiros diferentes.</span><span class="sxs-lookup"><span data-stu-id="2627f-198">Stream logs to third-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in to different third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="2627f-199">Criar uma plataforma de registro em log e telemetria personalizada – Se você já tiver uma plataforma de telemetria personalizada ou estiver pensando em criar uma, a natureza altamente escalonável de publicação-assinatura dos Hubs de Eventos permite a flexibilidade de ingestão de logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2627f-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="2627f-200">Consulte [o guia de Dan Rosanova sobre como usar os Hubs de Eventos em uma plataforma de telemetria de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="2627f-200">See [Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="2627f-201">Fluxo no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-201">Stream into Azure Storage</span></span>

<span data-ttu-id="2627f-202">Métricas de banco de dados SQL do Azure e logs de diagnóstico podem ser armazenados no Armazenamento do Azure usando a opção "Arquivar para uma conta de armazenamento" incorporada no portal do Azure, ou habilitando o Armazenamento do Azure em uma configuração de diagnóstico por meio de Cmdlets do PowerShell do Azure, CLI do Azure ou API REST do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2627f-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using the built-in "Archive to a storage account” option in the Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="2627f-203">Esquema de métricas e logs de diagnóstico na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2627f-203">Schema of metrics and diagnostic logs in the storage account</span></span>

<span data-ttu-id="2627f-204">Depois que você configurar as métricas e coleta de logs de diagnóstico, um contêiner de armazenamento é criado na conta de armazenamento que você selecionou quando as primeiras linhas de dados estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2627f-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in the storage account you selected when the first rows of data are available.</span></span> <span data-ttu-id="2627f-205">A estrutura desses blobs é:</span><span class="sxs-lookup"><span data-stu-id="2627f-205">The structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="2627f-206">Ou, simplesmente:</span><span class="sxs-lookup"><span data-stu-id="2627f-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="2627f-207">Por exemplo, um nome de blob para métricas de 1 minuto pode ser:</span><span class="sxs-lookup"><span data-stu-id="2627f-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="2627f-208">No caso de você desejar registrar os dados do Pool Elástico, o nome do blob é um pouco diferente:</span><span class="sxs-lookup"><span data-stu-id="2627f-208">In case you want to record the data from the Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="2627f-209">Baixar logs e métricas do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2627f-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="2627f-210">Consulte [Baixar métricas e logs de diagnósticos do Armazenamento do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="2627f-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="2627f-211">métricas de 1 minuto</span><span class="sxs-lookup"><span data-stu-id="2627f-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="2627f-212">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="2627f-212">**Resource**</span></span>|<span data-ttu-id="2627f-213">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="2627f-213">**Metrics**</span></span>|
|<span data-ttu-id="2627f-214">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="2627f-214">Database</span></span>|<span data-ttu-id="2627f-215">porcentagem de DTU, DTU usado, o limite DTU, o porcentagem de CPU, porcentagem de leitura de dados físicos, porcentagem de gravação de log, êxito/falha/bloqueados por conexões de firewall, porcentagem de sessões, porcentagem de funcionários, armazenamento, porcentagem de armazenamento, porcentagem de armazenamento XTP, deadlocks</span><span class="sxs-lookup"><span data-stu-id="2627f-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="2627f-216">Pool elástico</span><span class="sxs-lookup"><span data-stu-id="2627f-216">Elastic pool</span></span>|<span data-ttu-id="2627f-217">porcentagem de eDTU, eDTU usado, o limite eDTU, porcentagem de CPU, porcentagem de leitura de dados físicos, porcentagem de gravação de log, porcentagem de sessões, porcentagem de funcionários, armazenamento, porcentagem de armazenamento, limite de armazenamento, porcentagem de armazenamento XTP</span><span class="sxs-lookup"><span data-stu-id="2627f-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2627f-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2627f-218">Next steps</span></span>

- <span data-ttu-id="2627f-219">Leia os artigos [Visão geral de métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Visão geral dos Logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para entender não apenas como habilitar o registro em log, mas também as métricas e categorias de log com suporte dos vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="2627f-219">Read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>
- <span data-ttu-id="2627f-220">Leia estes artigos para saber mais sobre os hubs de eventos:</span><span class="sxs-lookup"><span data-stu-id="2627f-220">Read these articles to learn about event hubs:</span></span>
   - <span data-ttu-id="2627f-221">[O que são Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="2627f-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="2627f-222">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="2627f-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="2627f-223">Consulte [Baixar métricas e logs de diagnósticos do Armazenamento do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="2627f-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
