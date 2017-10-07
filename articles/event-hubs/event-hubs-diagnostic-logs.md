---
title: "logs de diagnóstico de Hubs de eventos aaaAzure | Microsoft Docs"
description: "Saiba como tooset backup de logs de diagnósticos para os hubs de eventos no Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="e6730-103">Logs de diagnóstico dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="e6730-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="e6730-104">É possível exibir dois tipos de logs para os Hubs de Eventos do Azure:</span><span class="sxs-lookup"><span data-stu-id="e6730-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="e6730-105">**[Logs de atividades](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e6730-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="e6730-106">Esses logs contém informações sobre as operações executadas em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="e6730-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="e6730-107">Olá logs são sempre habilitados.</span><span class="sxs-lookup"><span data-stu-id="e6730-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="e6730-108">**[Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e6730-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="e6730-109">É possível configurar logs de diagnóstico para ter uma visão mais detalhada de tudo o que acontece com um trabalho.</span><span class="sxs-lookup"><span data-stu-id="e6730-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="e6730-110">Atividades de cobertura de logs de diagnóstico de tempo de saudação trabalho Olá é criado até que o trabalho de saudação é excluído, incluindo atualizações e as atividades que ocorrem durante a saudação trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="e6730-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="e6730-111">Ativar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e6730-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="e6730-112">Os logs de diagnóstico estão desabilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="e6730-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="e6730-113">logs de diagnóstico tooenable:</span><span class="sxs-lookup"><span data-stu-id="e6730-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="e6730-114">Em Olá [portal do Azure](https://portal.azure.com), em **monitoramento + gerenciamento**, clique em **logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e6730-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Logs de toodiagnostic de navegação de folha](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="e6730-116">Clique em recurso Olá desejado toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e6730-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="e6730-117">Clique em **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e6730-117">Click **Turn on diagnostics**.</span></span>

    ![Ativar logs de diagnóstico](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="e6730-119">Para **Status**, clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="e6730-119">For **Status**, click **On**.</span></span>

    ![Alterar o status de saudação de logs de diagnóstico](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="e6730-121">Destino de arquivo do hello conjunto desejado. Por exemplo, uma conta de armazenamento, um hub de eventos ou análise de logs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6730-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="e6730-122">Salve Olá novas configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e6730-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="e6730-123">As novas configurações terão efeito em aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="e6730-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="e6730-124">Depois disso, os logs são exibidos no destino de arquivamento Olá configurado, no hello **logs de diagnóstico** folha.</span><span class="sxs-lookup"><span data-stu-id="e6730-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="e6730-125">Para obter mais informações sobre como configurar o diagnóstico, consulte Olá [visão geral dos logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e6730-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="e6730-126">Categorias dos logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e6730-126">Diagnostic logs categories</span></span>
<span data-ttu-id="e6730-127">Os Hubs de Eventos capturam os logs de diagnóstico de duas categorias:</span><span class="sxs-lookup"><span data-stu-id="e6730-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="e6730-128">**ArchiveLogs**: logs relacionados a arquivos de Hubs tooEvent, especificamente, registra erros de tooarchive relacionados.</span><span class="sxs-lookup"><span data-stu-id="e6730-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="e6730-129">**OperationalLogs**: informações sobre o que está acontecendo durante as operações de Hubs de eventos, especificamente, Olá o tipo de operação, incluindo a criação do hub de eventos, os recursos usados e Olá status da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6730-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="e6730-130">Esquema de logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e6730-130">Diagnostic logs schema</span></span>
<span data-ttu-id="e6730-131">Todos os logs são armazenados no formato JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="e6730-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="e6730-132">Cada entrada tem campos de cadeia de caracteres que usam o formato de saudação descrito nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6730-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="e6730-133">Esquema dos logs de arquivo morto</span><span class="sxs-lookup"><span data-stu-id="e6730-133">Archive logs schema</span></span>

<span data-ttu-id="e6730-134">Cadeias de caracteres JSON do arquivo log incluem elementos listados na Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6730-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="e6730-135">Nome</span><span class="sxs-lookup"><span data-stu-id="e6730-135">Name</span></span> | <span data-ttu-id="e6730-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="e6730-136">Description</span></span>
------- | -------
<span data-ttu-id="e6730-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="e6730-137">TaskName</span></span> | <span data-ttu-id="e6730-138">Descrição da tarefa de saudação que falhou.</span><span class="sxs-lookup"><span data-stu-id="e6730-138">Description of hello task that failed.</span></span>
<span data-ttu-id="e6730-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="e6730-139">ActivityId</span></span> | <span data-ttu-id="e6730-140">ID interna, usada para acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="e6730-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="e6730-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="e6730-141">trackingId</span></span> | <span data-ttu-id="e6730-142">ID interna, usada para acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="e6730-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="e6730-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="e6730-143">resourceId</span></span> | <span data-ttu-id="e6730-144">ID do Recurso do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6730-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="e6730-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="e6730-145">eventHub</span></span> | <span data-ttu-id="e6730-146">Nome completo do hub de eventos (inclui o nome do namespace).</span><span class="sxs-lookup"><span data-stu-id="e6730-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="e6730-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="e6730-147">partitionId</span></span> | <span data-ttu-id="e6730-148">Partição do Hub de Eventos usada para gravação.</span><span class="sxs-lookup"><span data-stu-id="e6730-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="e6730-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="e6730-149">archiveStep</span></span> | <span data-ttu-id="e6730-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="e6730-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="e6730-151">startTime</span><span class="sxs-lookup"><span data-stu-id="e6730-151">startTime</span></span> | <span data-ttu-id="e6730-152">Hora de início da falha.</span><span class="sxs-lookup"><span data-stu-id="e6730-152">Failure start time.</span></span>
<span data-ttu-id="e6730-153">failures</span><span class="sxs-lookup"><span data-stu-id="e6730-153">failures</span></span> | <span data-ttu-id="e6730-154">Número de vezes que a falha ocorreu.</span><span class="sxs-lookup"><span data-stu-id="e6730-154">Number of times failure occurred.</span></span>
<span data-ttu-id="e6730-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="e6730-155">durationInSeconds</span></span> | <span data-ttu-id="e6730-156">Duração da falha.</span><span class="sxs-lookup"><span data-stu-id="e6730-156">Duration of failure.</span></span>
<span data-ttu-id="e6730-157">Message</span><span class="sxs-lookup"><span data-stu-id="e6730-157">message</span></span> | <span data-ttu-id="e6730-158">Mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="e6730-158">Error message.</span></span>
<span data-ttu-id="e6730-159">categoria</span><span class="sxs-lookup"><span data-stu-id="e6730-159">category</span></span> | <span data-ttu-id="e6730-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="e6730-160">ArchiveLogs</span></span>

<span data-ttu-id="e6730-161">Olá código a seguir é um exemplo de um cadeia de caracteres JSON do log de arquivo:</span><span class="sxs-lookup"><span data-stu-id="e6730-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="e6730-162">Esquema de logs operacionais</span><span class="sxs-lookup"><span data-stu-id="e6730-162">Operational logs schema</span></span>

<span data-ttu-id="e6730-163">Cadeias de caracteres do log operacional JSON incluem elementos listados na Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6730-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="e6730-164">Nome</span><span class="sxs-lookup"><span data-stu-id="e6730-164">Name</span></span> | <span data-ttu-id="e6730-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="e6730-165">Description</span></span>
------- | -------
<span data-ttu-id="e6730-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="e6730-166">ActivityId</span></span> | <span data-ttu-id="e6730-167">ID interna, usadas tootrack finalidade.</span><span class="sxs-lookup"><span data-stu-id="e6730-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="e6730-168">EventName</span><span class="sxs-lookup"><span data-stu-id="e6730-168">EventName</span></span> | <span data-ttu-id="e6730-169">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="e6730-169">Operation name.</span></span>  
<span data-ttu-id="e6730-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="e6730-170">resourceId</span></span> | <span data-ttu-id="e6730-171">ID do Recurso do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6730-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="e6730-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="e6730-172">SubscriptionId</span></span> | <span data-ttu-id="e6730-173">ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="e6730-173">Subscription ID.</span></span>
<span data-ttu-id="e6730-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="e6730-174">EventTimeString</span></span> | <span data-ttu-id="e6730-175">Tempo da operação.</span><span class="sxs-lookup"><span data-stu-id="e6730-175">Operation time.</span></span>
<span data-ttu-id="e6730-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="e6730-176">EventProperties</span></span> | <span data-ttu-id="e6730-177">Propriedades da operação.</span><span class="sxs-lookup"><span data-stu-id="e6730-177">Operation properties.</span></span>
<span data-ttu-id="e6730-178">Status</span><span class="sxs-lookup"><span data-stu-id="e6730-178">Status</span></span> | <span data-ttu-id="e6730-179">Status da operação.</span><span class="sxs-lookup"><span data-stu-id="e6730-179">Operation status.</span></span>
<span data-ttu-id="e6730-180">Chamador</span><span class="sxs-lookup"><span data-stu-id="e6730-180">Caller</span></span> | <span data-ttu-id="e6730-181">Chamador da operação (Portal do Azure ou cliente de gerenciamento).</span><span class="sxs-lookup"><span data-stu-id="e6730-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="e6730-182">categoria</span><span class="sxs-lookup"><span data-stu-id="e6730-182">category</span></span> | <span data-ttu-id="e6730-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="e6730-183">OperationalLogs</span></span>

<span data-ttu-id="e6730-184">Olá código a seguir é um exemplo de uma cadeia de caracteres do log operacional JSON:</span><span class="sxs-lookup"><span data-stu-id="e6730-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="e6730-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6730-185">Next steps</span></span>
* [<span data-ttu-id="e6730-186">Introdução tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="e6730-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e6730-187">Visão geral de API de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="e6730-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="e6730-188">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="e6730-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
