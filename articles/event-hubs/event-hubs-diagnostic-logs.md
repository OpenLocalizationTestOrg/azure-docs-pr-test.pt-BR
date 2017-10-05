---
title: "Logs de diagnóstico dos Hubs de Eventos do Azure | Microsoft Docs"
description: "Saiba como configurar logs de diagnóstico para hub de eventos no Azure."
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
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="cf756-103">Logs de diagnóstico dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cf756-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="cf756-104">É possível exibir dois tipos de logs para os Hubs de Eventos do Azure:</span><span class="sxs-lookup"><span data-stu-id="cf756-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="cf756-105">**[Logs de atividades](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="cf756-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="cf756-106">Esses logs contém informações sobre as operações executadas em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="cf756-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="cf756-107">Os logs estão sempre habilitados.</span><span class="sxs-lookup"><span data-stu-id="cf756-107">The logs are always enabled.</span></span>
* <span data-ttu-id="cf756-108">**[Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="cf756-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="cf756-109">É possível configurar logs de diagnóstico para ter uma visão mais detalhada de tudo o que acontece com um trabalho.</span><span class="sxs-lookup"><span data-stu-id="cf756-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="cf756-110">Os logs de diagnóstico abrangem atividades desde o momento em que o trabalho é criado até sua exclusão, incluindo atualizações e atividades que ocorrem durante a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="cf756-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="cf756-111">Ativar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="cf756-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="cf756-112">Os logs de diagnóstico estão desabilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="cf756-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="cf756-113">Para habilitar logs de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="cf756-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="cf756-114">No [Portal do Azure](https://portal.azure.com), em **Monitoramento + Gerenciamento**, clique em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="cf756-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Navegação de folha para os logs de diagnóstico](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="cf756-116">Clique no recurso que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="cf756-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="cf756-117">Clique em **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="cf756-117">Click **Turn on diagnostics**.</span></span>

    ![Ativar logs de diagnóstico](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="cf756-119">Para **Status**, clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="cf756-119">For **Status**, click **On**.</span></span>

    ![Alterar o status dos logs de diagnóstico](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="cf756-121">Defina o destino de arquivamento desejado, por exemplo, uma conta de armazenamento, um hub de eventos ou o Log Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf756-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="cf756-122">Salve as novas configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="cf756-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="cf756-123">As novas configurações terão efeito em aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="cf756-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="cf756-124">Depois disso, os logs aparecerão no destino de arquivamento configurado, na folha **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="cf756-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="cf756-125">Para saber mais sobre como configurar um diagnóstico, confira a [visão geral dos logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="cf756-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="cf756-126">Categorias dos logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="cf756-126">Diagnostic logs categories</span></span>
<span data-ttu-id="cf756-127">Os Hubs de Eventos capturam os logs de diagnóstico de duas categorias:</span><span class="sxs-lookup"><span data-stu-id="cf756-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="cf756-128">**ArchiveLogs**: logs relacionados aos arquivos mortos dos Hubs de Eventos, especificamente os logs relacionados a erros de arquivo morto.</span><span class="sxs-lookup"><span data-stu-id="cf756-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="cf756-129">**OperationalLogs**: informações sobre o que está acontecendo durante a operação dos Hubs de Eventos, especificamente o tipo de operação, incluindo a criação do hub de eventos, os recursos usados e o status da operação.</span><span class="sxs-lookup"><span data-stu-id="cf756-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="cf756-130">Esquema de logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="cf756-130">Diagnostic logs schema</span></span>
<span data-ttu-id="cf756-131">Todos os logs são armazenados no formato JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="cf756-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="cf756-132">Cada entrada tem campos de cadeia de caracteres que usam o formato descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="cf756-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="cf756-133">Esquema dos logs de arquivo morto</span><span class="sxs-lookup"><span data-stu-id="cf756-133">Archive logs schema</span></span>

<span data-ttu-id="cf756-134">As cadeias de caracteres JSON do log de arquivo morto incluem os elementos listados na seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="cf756-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="cf756-135">Nome</span><span class="sxs-lookup"><span data-stu-id="cf756-135">Name</span></span> | <span data-ttu-id="cf756-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="cf756-136">Description</span></span>
------- | -------
<span data-ttu-id="cf756-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="cf756-137">TaskName</span></span> | <span data-ttu-id="cf756-138">Descrição da tarefa que falhou.</span><span class="sxs-lookup"><span data-stu-id="cf756-138">Description of the task that failed.</span></span>
<span data-ttu-id="cf756-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="cf756-139">ActivityId</span></span> | <span data-ttu-id="cf756-140">ID interna, usada para acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="cf756-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="cf756-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="cf756-141">trackingId</span></span> | <span data-ttu-id="cf756-142">ID interna, usada para acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="cf756-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="cf756-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="cf756-143">resourceId</span></span> | <span data-ttu-id="cf756-144">ID do Recurso do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf756-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="cf756-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="cf756-145">eventHub</span></span> | <span data-ttu-id="cf756-146">Nome completo do hub de eventos (inclui o nome do namespace).</span><span class="sxs-lookup"><span data-stu-id="cf756-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="cf756-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="cf756-147">partitionId</span></span> | <span data-ttu-id="cf756-148">Partição do Hub de Eventos usada para gravação.</span><span class="sxs-lookup"><span data-stu-id="cf756-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="cf756-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="cf756-149">archiveStep</span></span> | <span data-ttu-id="cf756-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="cf756-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="cf756-151">startTime</span><span class="sxs-lookup"><span data-stu-id="cf756-151">startTime</span></span> | <span data-ttu-id="cf756-152">Hora de início da falha.</span><span class="sxs-lookup"><span data-stu-id="cf756-152">Failure start time.</span></span>
<span data-ttu-id="cf756-153">failures</span><span class="sxs-lookup"><span data-stu-id="cf756-153">failures</span></span> | <span data-ttu-id="cf756-154">Número de vezes que a falha ocorreu.</span><span class="sxs-lookup"><span data-stu-id="cf756-154">Number of times failure occurred.</span></span>
<span data-ttu-id="cf756-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="cf756-155">durationInSeconds</span></span> | <span data-ttu-id="cf756-156">Duração da falha.</span><span class="sxs-lookup"><span data-stu-id="cf756-156">Duration of failure.</span></span>
<span data-ttu-id="cf756-157">Message</span><span class="sxs-lookup"><span data-stu-id="cf756-157">message</span></span> | <span data-ttu-id="cf756-158">Mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="cf756-158">Error message.</span></span>
<span data-ttu-id="cf756-159">categoria</span><span class="sxs-lookup"><span data-stu-id="cf756-159">category</span></span> | <span data-ttu-id="cf756-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="cf756-160">ArchiveLogs</span></span>

<span data-ttu-id="cf756-161">O código a seguir é um exemplo de uma cadeia de caracteres JSON do log de arquivo morto:</span><span class="sxs-lookup"><span data-stu-id="cf756-161">The following code is an example of an archive log JSON string:</span></span>

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
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="cf756-162">Esquema de logs operacionais</span><span class="sxs-lookup"><span data-stu-id="cf756-162">Operational logs schema</span></span>

<span data-ttu-id="cf756-163">As cadeias de caracteres JSON do log operacional incluem os elementos listados na seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="cf756-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="cf756-164">Nome</span><span class="sxs-lookup"><span data-stu-id="cf756-164">Name</span></span> | <span data-ttu-id="cf756-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="cf756-165">Description</span></span>
------- | -------
<span data-ttu-id="cf756-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="cf756-166">ActivityId</span></span> | <span data-ttu-id="cf756-167">ID interna, usada para fins de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="cf756-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="cf756-168">EventName</span><span class="sxs-lookup"><span data-stu-id="cf756-168">EventName</span></span> | <span data-ttu-id="cf756-169">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="cf756-169">Operation name.</span></span>  
<span data-ttu-id="cf756-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="cf756-170">resourceId</span></span> | <span data-ttu-id="cf756-171">ID do Recurso do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf756-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="cf756-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="cf756-172">SubscriptionId</span></span> | <span data-ttu-id="cf756-173">ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="cf756-173">Subscription ID.</span></span>
<span data-ttu-id="cf756-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="cf756-174">EventTimeString</span></span> | <span data-ttu-id="cf756-175">Tempo da operação.</span><span class="sxs-lookup"><span data-stu-id="cf756-175">Operation time.</span></span>
<span data-ttu-id="cf756-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="cf756-176">EventProperties</span></span> | <span data-ttu-id="cf756-177">Propriedades da operação.</span><span class="sxs-lookup"><span data-stu-id="cf756-177">Operation properties.</span></span>
<span data-ttu-id="cf756-178">Status</span><span class="sxs-lookup"><span data-stu-id="cf756-178">Status</span></span> | <span data-ttu-id="cf756-179">Status da operação.</span><span class="sxs-lookup"><span data-stu-id="cf756-179">Operation status.</span></span>
<span data-ttu-id="cf756-180">Chamador</span><span class="sxs-lookup"><span data-stu-id="cf756-180">Caller</span></span> | <span data-ttu-id="cf756-181">Chamador da operação (Portal do Azure ou cliente de gerenciamento).</span><span class="sxs-lookup"><span data-stu-id="cf756-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="cf756-182">categoria</span><span class="sxs-lookup"><span data-stu-id="cf756-182">category</span></span> | <span data-ttu-id="cf756-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="cf756-183">OperationalLogs</span></span>

<span data-ttu-id="cf756-184">O código a seguir é um exemplo de uma cadeia de caracteres JSON do log operacional:</span><span class="sxs-lookup"><span data-stu-id="cf756-184">The following code is an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cf756-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf756-185">Next steps</span></span>
* [<span data-ttu-id="cf756-186">Introdução aos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cf756-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="cf756-187">Visão geral de API de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cf756-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="cf756-188">Introdução aos Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="cf756-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
