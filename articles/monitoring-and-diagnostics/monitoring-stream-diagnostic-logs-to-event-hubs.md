---
title: "Logs de diagnóstico do Azure de aaaStream tooan Namespace de Hubs de evento | Microsoft Docs"
description: "Saiba como toostream diagnóstico do Azure registra tooan namespace de Hubs de eventos."
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
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="9874b-103">Fluxo de Logs de diagnóstico do Azure tooan Namespace de Hubs de evento</span><span class="sxs-lookup"><span data-stu-id="9874b-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="9874b-104">**[Logs de diagnósticos do Azure](monitoring-overview-of-diagnostic-logs.md)**  pode ser transmitida em quase em tempo real tooany aplicativo usando a opção hello "Exportar tooEvent Hubs" incorporada no Portal de saudação ou habilitando Olá ID de regra de barramento de serviço em uma configuração de diagnóstica por meio de saudação do PowerShell do Azure CLI cmdlets ou do Azure.</span><span class="sxs-lookup"><span data-stu-id="9874b-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="9874b-105">O que você pode fazer com os logs de diagnóstico e os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="9874b-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="9874b-106">Aqui estão algumas maneiras que você pode usar o hello capacidade para streaming para Logs de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="9874b-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="9874b-107">**Fluxo de logs de sistemas de registro em log e telemetria de too3rd** – ao longo do tempo, streaming de Hubs de eventos se tornará Olá mecanismo toopipe os logs de diagnóstico na parte toothird SIEMs e soluções de análise de log.</span><span class="sxs-lookup"><span data-stu-id="9874b-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="9874b-108">**Exibir a integridade do serviço por streaming "afunilamento" dados tooPowerBI** – usando Hubs de eventos, análise de fluxo e Power BI, você pode facilmente transformar os dados de diagnóstico em informações em tempo real toonear em seus serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="9874b-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="9874b-109">[Este artigo de documentação fornece uma visão de geral grande como tooset a Hubs de eventos, processar dados com a análise de fluxo e usar o Power BI como uma saída](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="9874b-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="9874b-110">Aqui estão algumas dicas para configurá-lo com os logs de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="9874b-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="9874b-111">Um hub de eventos para uma categoria de logs de diagnóstico é criado automaticamente quando você marca a opção Olá no portal de saudação ou habilitá-lo por meio do PowerShell, para que você deseja que o hub de eventos tooselect Olá Olá namespace com o nome da saudação que começa com **insights**.</span><span class="sxs-lookup"><span data-stu-id="9874b-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="9874b-112">Olá código SQL a seguir está um exemplo de análise de fluxo de consulta que você pode usar tooparse todos os dados de log Olá na tabela do Power BI tooa:</span><span class="sxs-lookup"><span data-stu-id="9874b-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="9874b-113">**Criar uma plataforma de registro em log e telemetria personalizada** – se você já tem uma plataforma de telemetria personalizada ou estão pensando sobre como criar um, Olá altamente escalonável de publicação / assinatura natureza dos Hubs de eventos permite que você tooflexibly ingestão diagnóstico logs.</span><span class="sxs-lookup"><span data-stu-id="9874b-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="9874b-114">[Consulte toousing de guia de Dan Rosanova Hubs de eventos em uma plataforma de telemetria de escala global aqui](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="9874b-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="9874b-115">Habilitar o streaming de logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="9874b-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="9874b-116">Você pode habilitar o streaming de logs de diagnóstico programaticamente, por meio do portal hello, ou usando Olá [APIs de REST do Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="9874b-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="9874b-117">De qualquer forma, você cria uma configuração de diagnóstica que você especifica um namespace de Hubs de eventos e categorias de log hello e métricas que você deseja toosend no namespace toohello.</span><span class="sxs-lookup"><span data-stu-id="9874b-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="9874b-118">Um hub de eventos é criado no namespace Olá para cada categoria de log que você habilitar.</span><span class="sxs-lookup"><span data-stu-id="9874b-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="9874b-119">Uma **categoria de log** de diagnóstico é um tipo de log que um recurso pode coletar.</span><span class="sxs-lookup"><span data-stu-id="9874b-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="9874b-120">A habilitação e streaming de logs de diagnóstico dos recursos de computação (por exemplo, VMs ou Service Fabric) [exige um conjunto diferente de etapas](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="9874b-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="9874b-121">Olá barramento de serviço ou Hubs de evento namespace não tem toobe em Olá mesma assinatura que o recurso Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.</span><span class="sxs-lookup"><span data-stu-id="9874b-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="9874b-122">Logs de diagnóstico de fluxo usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="9874b-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="9874b-123">No portal de hello, navegar tooAzure Monitor e clique em **configurações de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="9874b-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Seção de monitoramento do Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="9874b-125">Se desejar filtrar lista Olá por tipo de recurso ou grupo de recursos, clique no recurso Olá para o qual você gostaria que tooset uma configuração de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="9874b-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="9874b-126">Se nenhuma configuração existir no recurso de saudação selecionado, você está toocreate solicitada uma configuração.</span><span class="sxs-lookup"><span data-stu-id="9874b-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="9874b-127">Clique em “Ativar diagnóstico”.</span><span class="sxs-lookup"><span data-stu-id="9874b-127">Click "Turn on diagnostics."</span></span>

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="9874b-129">Se houver configurações existentes no recurso hello, você verá uma lista de configurações já configurado nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="9874b-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="9874b-130">Clique em "Adicionar configuração de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="9874b-130">Click "Add diagnostic setting."</span></span>

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="9874b-132">Dê sua configuração para um nome e marque a caixa de saudação para **hub de eventos do fluxo tooan**, em seguida, selecione um namespace de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="9874b-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="9874b-134">Olá namespace selecionado será onde o hub de eventos de saudação é criado (se esta for a primeira vez em que os logs de diagnósticos de streaming) ou transmitido muito (se já houver recursos que são de streaming log categoria toothis namespace), e política de saudação define Olá permissões de mecanismo de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9874b-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="9874b-135">Atualmente, o hub de eventos streaming tooan requer permissões de escuta, envio e gerenciar.</span><span class="sxs-lookup"><span data-stu-id="9874b-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="9874b-136">Você pode criar ou modificar políticas de acesso compartilhado de namespace Hubs de eventos no portal de saudação na guia Configurar de saudação para seu namespace.</span><span class="sxs-lookup"><span data-stu-id="9874b-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="9874b-137">tooupdate uma destas configurações de diagnósticas, o cliente Olá deve ter permissão de ListKey de Olá na regra de autorização de Hubs de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9874b-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="9874b-138">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9874b-138">Click **Save**.</span></span>

<span data-ttu-id="9874b-139">Após alguns instantes, nova configuração de saudação aparece na lista de configurações para esse recurso e logs de diagnóstico são transmitidos a conta de armazenamento toothat assim que novos dados de evento são gerados.</span><span class="sxs-lookup"><span data-stu-id="9874b-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="9874b-140">Via Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9874b-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="9874b-141">tooenable streaming por meio do hello [Cmdlets do PowerShell do Azure](insights-powershell-samples.md), você pode usar o hello `Set-AzureRmDiagnosticSetting` cmdlet com estes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9874b-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="9874b-142">Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`, por exemplo, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="9874b-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="9874b-143">Via CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9874b-143">Via Azure CLI</span></span>
<span data-ttu-id="9874b-144">tooenable streaming por meio do hello [CLI do Azure](insights-cli-samples.md), você pode usar o hello `insights diagnostic set` comando como este:</span><span class="sxs-lookup"><span data-stu-id="9874b-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="9874b-145">Use Olá mesmo formato para ID de regra de barramento de serviço, conforme explicado para Olá Cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9874b-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="9874b-146">Como consomem a dados de log de saudação dos Hubs de eventos?</span><span class="sxs-lookup"><span data-stu-id="9874b-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="9874b-147">Aqui está um exemplo de dados de saída dos Hubs de Eventos:</span><span class="sxs-lookup"><span data-stu-id="9874b-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="9874b-148">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9874b-148">Element Name</span></span> | <span data-ttu-id="9874b-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="9874b-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9874b-150">records</span><span class="sxs-lookup"><span data-stu-id="9874b-150">records</span></span> |<span data-ttu-id="9874b-151">Uma matriz de todos os eventos de log nessa carga.</span><span class="sxs-lookup"><span data-stu-id="9874b-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="9874b-152">tempo real</span><span class="sxs-lookup"><span data-stu-id="9874b-152">time</span></span> |<span data-ttu-id="9874b-153">Hora em que hello evento ocorreu.</span><span class="sxs-lookup"><span data-stu-id="9874b-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="9874b-154">categoria</span><span class="sxs-lookup"><span data-stu-id="9874b-154">category</span></span> |<span data-ttu-id="9874b-155">Categoria do log desse evento.</span><span class="sxs-lookup"><span data-stu-id="9874b-155">Log category for this event.</span></span> |
| <span data-ttu-id="9874b-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="9874b-156">resourceId</span></span> |<span data-ttu-id="9874b-157">ID de recurso do recurso de saudação que gerou este evento.</span><span class="sxs-lookup"><span data-stu-id="9874b-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="9874b-158">operationName</span><span class="sxs-lookup"><span data-stu-id="9874b-158">operationName</span></span> |<span data-ttu-id="9874b-159">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9874b-159">Name of hello operation.</span></span> |
| <span data-ttu-id="9874b-160">level</span><span class="sxs-lookup"><span data-stu-id="9874b-160">level</span></span> |<span data-ttu-id="9874b-161">Opcional.</span><span class="sxs-lookup"><span data-stu-id="9874b-161">Optional.</span></span> <span data-ttu-id="9874b-162">Indica o nível de log de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9874b-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="9874b-163">propriedades</span><span class="sxs-lookup"><span data-stu-id="9874b-163">properties</span></span> |<span data-ttu-id="9874b-164">Propriedades de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9874b-164">Properties of hello event.</span></span> |

<span data-ttu-id="9874b-165">Você pode exibir uma lista de todos os provedores de recursos que oferecem suporte a streaming Hubs tooEvent [aqui](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9874b-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="9874b-166">Transmitir dados de recursos de Computação</span><span class="sxs-lookup"><span data-stu-id="9874b-166">Stream data from Compute resources</span></span>
<span data-ttu-id="9874b-167">Você também pode transmitir os logs de diagnóstico dos recursos de computação usando o agente de diagnóstico do Windows Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9874b-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="9874b-168">[Consulte este artigo](../event-hubs/event-hubs-streaming-azure-diags-data.md) como tooset esse backup.</span><span class="sxs-lookup"><span data-stu-id="9874b-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9874b-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9874b-169">Next steps</span></span>
* [<span data-ttu-id="9874b-170">Saiba mais sobre os Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="9874b-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="9874b-171">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="9874b-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

