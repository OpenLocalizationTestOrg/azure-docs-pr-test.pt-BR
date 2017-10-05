---
title: "Transmitir Logs de Diagnóstico do Azure para um Namespace de Hubs de Eventos | Microsoft Docs"
description: "Saiba como transmitir logs de diagnóstico do Azure para um namespace de Hubs de Eventos."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 01ba8ddfcf90e1368ac147296fd180f99420d96f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hubs-namespace"></a><span data-ttu-id="bca6e-103">Transmitir Logs de Diagnóstico do Azure para um Namespace de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="bca6e-103">Stream Azure Diagnostic Logs to an Event Hubs Namespace</span></span>
<span data-ttu-id="bca6e-104">Os **[logs de diagnóstico do Azure](monitoring-overview-of-diagnostic-logs.md)** podem ser transmitidos em tempo real a qualquer aplicativo usando a opção interna "Exportar para Hubs de Eventos" no Portal, ou habilitando a ID da Regra de Barramento de Serviço em uma configuração de diagnóstico por meio de cmdlets do Azure PowerShell ou da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bca6e-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule ID in a diagnostic setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="bca6e-105">O que você pode fazer com os logs de diagnóstico e os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="bca6e-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="bca6e-106">Veja algumas maneiras de usar o recurso de streaming para os Logs de Diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="bca6e-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="bca6e-107">**Transmitir logs para sistemas de registro em log e telemetria de terceiros** – ao longo do tempo, a transmissão de Hubs de Eventos se tornará o mecanismo para direcionar seus logs de diagnóstico para SIEMs e soluções de análise de log de terceiros.</span><span class="sxs-lookup"><span data-stu-id="bca6e-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your diagnostic logs in to third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="bca6e-108">**Exibir a integridade do serviço transmitindo dados de "afunilamento" para o PowerBI** – com os Hubs de Eventos, Stream Analytics e o PowerBI, é fácil transformar seus dados de diagnóstico em informações quase em tempo real nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="bca6e-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in to near real-time insights on your Azure services.</span></span> <span data-ttu-id="bca6e-109">[Este artigo de documentação apresenta uma excelente visão geral de como configurar Hubs de Eventos, processar dados com o Stream Analytics e usar o PowerBI como saída](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="bca6e-109">[This documentation article gives a great overview of how to set up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="bca6e-110">Aqui estão algumas dicas para configurá-lo com os logs de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="bca6e-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="bca6e-111">Um hub de eventos de uma categoria de logs de diagnóstico é criado automaticamente quando você marca a opção no portal ou habilita-a por meio do PowerShell, de modo que você possa selecionar o hub de evento no namespace com o nome que começa com **insights-**.</span><span class="sxs-lookup"><span data-stu-id="bca6e-111">An event hub for a category of diagnostic logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the event hub in the namespace with the name that starts with **insights-**.</span></span>
  * <span data-ttu-id="bca6e-112">O código SQL a seguir é um exemplo de consulta do Stream Analytics que você pode usar para analisar todos os dados de log em uma tabela do PowerBI:</span><span class="sxs-lookup"><span data-stu-id="bca6e-112">The following SQL code is a sample Stream Analytics query that you can use to parse all the log data in to a PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="bca6e-113">**Compilar uma plataforma de registro em log e telemetria personalizada** – Se você já tiver uma plataforma de telemetria personalizada ou estiver pensando em criar uma, a natureza altamente escalonável de publicação-assinatura dos Hubs de Eventos permite a flexibilidade de ingestão de logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="bca6e-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="bca6e-114">[Confira o guia de Dan Rosanova sobre como usar os Hubs de Eventos em uma plataforma de telemetria de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="bca6e-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="bca6e-115">Habilitar o streaming de logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="bca6e-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="bca6e-116">Você pode habilitar programaticamente o streaming de logs de diagnóstico por meio do portal ou usando a [API REST do Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="bca6e-116">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="bca6e-117">De qualquer forma, você cria uma configuração de diagnóstico no qual especifica um namespace de Hubs de Eventos e as categorias de log e as métricas que deseja enviar para o namespace.</span><span class="sxs-lookup"><span data-stu-id="bca6e-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and the log categories and metrics you want to send in to the namespace.</span></span> <span data-ttu-id="bca6e-118">Um hub de eventos é criado no namespace para cada categoria de log que você habilitar.</span><span class="sxs-lookup"><span data-stu-id="bca6e-118">An event hub is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="bca6e-119">Uma **categoria de log** de diagnóstico é um tipo de log que um recurso pode coletar.</span><span class="sxs-lookup"><span data-stu-id="bca6e-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="bca6e-120">A habilitação e streaming de logs de diagnóstico dos recursos de computação (por exemplo, VMs ou Service Fabric) [exige um conjunto diferente de etapas](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="bca6e-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="bca6e-121">O namespace do Barramento de Serviço ou dos Hubs de Eventos não precisa estar na mesma assinatura que o recurso que emite os logs, desde que o usuário que define a configuração tenha acesso RBAC apropriado a ambas as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="bca6e-121">The Service Bus or Event Hubs namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="bca6e-122">Transmitir logs de diagnóstico usando o portal</span><span class="sxs-lookup"><span data-stu-id="bca6e-122">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="bca6e-123">No portal, navegue até o Azure Monitor e clique em **Configurações de Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="bca6e-123">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Seção de monitoramento do Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="bca6e-125">Se desejar filtrar a lista por tipo de recurso ou grupo de recursos, clique no recurso para o qual você deseja definir uma configuração de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="bca6e-125">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="bca6e-126">Se nenhuma configuração existir no recurso que você selecionou, será solicitada a criação de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="bca6e-126">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="bca6e-127">Clique em “Ativar diagnóstico”.</span><span class="sxs-lookup"><span data-stu-id="bca6e-127">Click "Turn on diagnostics."</span></span>

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="bca6e-129">Se houver configurações existentes no recurso, você verá uma lista de configurações já definidas nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="bca6e-129">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="bca6e-130">Clique em "Adicionar configuração de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="bca6e-130">Click "Add diagnostic setting."</span></span>

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="bca6e-132">Dê um nome à sua configuração e marque a caixa **Fluxo para um hub de eventos** e então selecione um namespace de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="bca6e-132">Give your setting a name and check the box for **Stream to an event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="bca6e-134">O namespace selecionado será o local em que o hub de evento é criado (se este for seu primeiro streaming de logs de diagnóstico) ou transmitido (se já houver recursos realizando o streaming dessa categoria log para esse namespace) e a política define as permissões do mecanismo de streaming.</span><span class="sxs-lookup"><span data-stu-id="bca6e-134">The namespace selected will be where the event hub is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="bca6e-135">Atualmente, o streaming para um hub de eventos exige as permissões para Gerenciar, Enviar e Escutar.</span><span class="sxs-lookup"><span data-stu-id="bca6e-135">Today, streaming to an event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="bca6e-136">Você pode criar ou modificar políticas de acesso compartilhado de namespace de Hubs de Eventos no portal na guia Configurar para seu namespace.</span><span class="sxs-lookup"><span data-stu-id="bca6e-136">You can create or modify Event Hubs namespace shared access policies in the portal under the Configure tab for your namespace.</span></span> <span data-ttu-id="bca6e-137">Para atualizar uma dessas configurações de diagnóstico, o cliente deve ter a permissão ListKey na regra de autorização de Hubs de Evento.</span><span class="sxs-lookup"><span data-stu-id="bca6e-137">To update one of these diagnostic settings, the client must have the ListKey permission on the Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="bca6e-138">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bca6e-138">Click **Save**.</span></span>

<span data-ttu-id="bca6e-139">Após alguns instantes, a nova configuração aparece na lista de configurações para esse recurso e os logs de diagnóstico são transmitidos para a conta de armazenamento assim que os novos dados de evento são gerados.</span><span class="sxs-lookup"><span data-stu-id="bca6e-139">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="bca6e-140">Via Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bca6e-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="bca6e-141">Para habilitar o streaming por meio de [Cmdlets do Azure PowerShell](insights-powershell-samples.md), use o cmdlet `Set-AzureRmDiagnosticSetting` com estes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="bca6e-141">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="bca6e-142">A ID da Regra do Barramento de Serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}` , `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="bca6e-142">The Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="bca6e-143">Via CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bca6e-143">Via Azure CLI</span></span>
<span data-ttu-id="bca6e-144">Para habilitar o streaming por meio da [CLI do Azure](insights-cli-samples.md), use o comando `insights diagnostic set` da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="bca6e-144">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="bca6e-145">Use o mesmo formato para ID de Regra do Barramento de Serviço, conforme explicado para o Cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bca6e-145">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="bca6e-146">Como eu consumo os dados de log dos Hubs de Eventos?</span><span class="sxs-lookup"><span data-stu-id="bca6e-146">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="bca6e-147">Aqui está um exemplo de dados de saída dos Hubs de Eventos:</span><span class="sxs-lookup"><span data-stu-id="bca6e-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="bca6e-148">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="bca6e-148">Element Name</span></span> | <span data-ttu-id="bca6e-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="bca6e-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bca6e-150">records</span><span class="sxs-lookup"><span data-stu-id="bca6e-150">records</span></span> |<span data-ttu-id="bca6e-151">Uma matriz de todos os eventos de log nessa carga.</span><span class="sxs-lookup"><span data-stu-id="bca6e-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="bca6e-152">tempo real</span><span class="sxs-lookup"><span data-stu-id="bca6e-152">time</span></span> |<span data-ttu-id="bca6e-153">A hora na qual o evento ocorreu.</span><span class="sxs-lookup"><span data-stu-id="bca6e-153">Time at which the event occurred.</span></span> |
| <span data-ttu-id="bca6e-154">categoria</span><span class="sxs-lookup"><span data-stu-id="bca6e-154">category</span></span> |<span data-ttu-id="bca6e-155">Categoria do log desse evento.</span><span class="sxs-lookup"><span data-stu-id="bca6e-155">Log category for this event.</span></span> |
| <span data-ttu-id="bca6e-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="bca6e-156">resourceId</span></span> |<span data-ttu-id="bca6e-157">ID de recurso do recurso que gerou esse evento.</span><span class="sxs-lookup"><span data-stu-id="bca6e-157">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="bca6e-158">operationName</span><span class="sxs-lookup"><span data-stu-id="bca6e-158">operationName</span></span> |<span data-ttu-id="bca6e-159">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="bca6e-159">Name of the operation.</span></span> |
| <span data-ttu-id="bca6e-160">level</span><span class="sxs-lookup"><span data-stu-id="bca6e-160">level</span></span> |<span data-ttu-id="bca6e-161">Opcional.</span><span class="sxs-lookup"><span data-stu-id="bca6e-161">Optional.</span></span> <span data-ttu-id="bca6e-162">Indica o nível do evento de log.</span><span class="sxs-lookup"><span data-stu-id="bca6e-162">Indicates the log event level.</span></span> |
| <span data-ttu-id="bca6e-163">propriedades</span><span class="sxs-lookup"><span data-stu-id="bca6e-163">properties</span></span> |<span data-ttu-id="bca6e-164">Propriedades do evento.</span><span class="sxs-lookup"><span data-stu-id="bca6e-164">Properties of the event.</span></span> |

<span data-ttu-id="bca6e-165">É possível exibir uma lista de todos os provedores de recursos que dão suporte a streaming para o Hub de Eventos [aqui](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bca6e-165">You can view a list of all resource providers that support streaming to Event Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="bca6e-166">Transmitir dados de recursos de Computação</span><span class="sxs-lookup"><span data-stu-id="bca6e-166">Stream data from Compute resources</span></span>
<span data-ttu-id="bca6e-167">Também é possível transmitir logs de diagnóstico de recursos de Computação usando o agente do Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="bca6e-167">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="bca6e-168">[Consulte este artigo](../event-hubs/event-hubs-streaming-azure-diags-data.md) para saber como configurar isso.</span><span class="sxs-lookup"><span data-stu-id="bca6e-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bca6e-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bca6e-169">Next steps</span></span>
* [<span data-ttu-id="bca6e-170">Saiba mais sobre os Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="bca6e-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="bca6e-171">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="bca6e-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

