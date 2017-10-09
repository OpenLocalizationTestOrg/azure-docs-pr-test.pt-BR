---
title: "logs de diagnóstico de barramento de serviço aaaAzure | Microsoft Docs"
description: "Saiba como tooset backup de logs de diagnósticos para o barramento de serviço no Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="2d376-103">Logs de diagnóstico do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="2d376-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="2d376-104">É possível exibir dois tipos de logs para o Barramento de Serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="2d376-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="2d376-105">**[Logs de atividades](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="2d376-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="2d376-106">Esses logs contém informações sobre as operações executadas em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="2d376-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="2d376-107">Olá logs são sempre habilitados.</span><span class="sxs-lookup"><span data-stu-id="2d376-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="2d376-108">**[Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="2d376-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="2d376-109">É possível configurar logs de diagnóstico para obter informações mais detalhadas sobre tudo o que acontece em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="2d376-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="2d376-110">Atividades de cobertura de logs de diagnóstico de tempo de saudação trabalho Olá é criado até que o trabalho de saudação é excluído, incluindo atualizações e as atividades que ocorrem durante a saudação trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="2d376-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="2d376-111">Ativar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="2d376-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="2d376-112">Os logs de diagnóstico estão desabilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="2d376-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="2d376-113">logs de diagnóstico tooenable, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d376-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="2d376-114">Em Olá [portal do Azure](https://portal.azure.com), em **monitoramento + gerenciamento**, clique em **logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="2d376-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Logs de toodiagnostic de navegação de folha](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="2d376-116">Clique em recurso Olá desejado toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2d376-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="2d376-117">Clique em **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="2d376-117">Click **Turn on diagnostics**.</span></span>

    ![ativar logs de diagnóstico](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="2d376-119">Para **Status**, clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="2d376-119">For **Status**, click **On**.</span></span>

    ![alterar logs de diagnóstico de status](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="2d376-121">Destino de arquivo do hello conjunto desejado. Por exemplo, uma conta de armazenamento, um Hub de eventos ou análise de logs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d376-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="2d376-122">Salve Olá novas configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2d376-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="2d376-123">As novas configurações terão efeito em aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="2d376-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="2d376-124">Depois disso, os logs são exibidos no destino de arquivamento Olá configurado, no hello **logs de diagnóstico** folha.</span><span class="sxs-lookup"><span data-stu-id="2d376-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="2d376-125">Para obter mais informações sobre como configurar o diagnóstico, consulte Olá [visão geral dos logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2d376-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="2d376-126">Esquema de logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="2d376-126">Diagnostic logs schema</span></span>

<span data-ttu-id="2d376-127">Todos os logs são armazenados no formato JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="2d376-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="2d376-128">Cada entrada tem campos de cadeia de caracteres que usam o formato de saudação descrito na Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="2d376-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="2d376-129">Esquema de logs operacionais</span><span class="sxs-lookup"><span data-stu-id="2d376-129">Operational logs schema</span></span>

<span data-ttu-id="2d376-130">Registra no hello **OperationalLogs** categoria captura o que acontece durante as operações de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="2d376-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="2d376-131">Especificamente, esses logs capturar o tipo de operação hello, incluindo a criação da fila, os recursos usados e Olá status da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d376-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="2d376-132">Cadeias de caracteres do log operacional JSON incluem elementos listados na Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d376-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="2d376-133">Nome</span><span class="sxs-lookup"><span data-stu-id="2d376-133">Name</span></span> | <span data-ttu-id="2d376-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="2d376-134">Description</span></span>
------- | -------
<span data-ttu-id="2d376-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="2d376-135">ActivityId</span></span> | <span data-ttu-id="2d376-136">ID interna, usada para acompanhamento</span><span class="sxs-lookup"><span data-stu-id="2d376-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="2d376-137">EventName</span><span class="sxs-lookup"><span data-stu-id="2d376-137">EventName</span></span> | <span data-ttu-id="2d376-138">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="2d376-138">Operation name</span></span>           
<span data-ttu-id="2d376-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="2d376-139">resourceId</span></span> | <span data-ttu-id="2d376-140">ID de recurso do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d376-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="2d376-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="2d376-141">SubscriptionId</span></span> | <span data-ttu-id="2d376-142">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="2d376-142">Subscription ID</span></span>
<span data-ttu-id="2d376-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="2d376-143">EventTimeString</span></span> | <span data-ttu-id="2d376-144">Tempo de operação</span><span class="sxs-lookup"><span data-stu-id="2d376-144">Operation time</span></span>
<span data-ttu-id="2d376-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="2d376-145">EventProperties</span></span> | <span data-ttu-id="2d376-146">Propriedades da operação</span><span class="sxs-lookup"><span data-stu-id="2d376-146">Operation properties</span></span>
<span data-ttu-id="2d376-147">Status</span><span class="sxs-lookup"><span data-stu-id="2d376-147">Status</span></span> | <span data-ttu-id="2d376-148">Status da operação</span><span class="sxs-lookup"><span data-stu-id="2d376-148">Operation status</span></span>
<span data-ttu-id="2d376-149">Chamador</span><span class="sxs-lookup"><span data-stu-id="2d376-149">Caller</span></span> | <span data-ttu-id="2d376-150">Chamador da operação (portal do Azure ou cliente de gerenciamento)</span><span class="sxs-lookup"><span data-stu-id="2d376-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="2d376-151">categoria</span><span class="sxs-lookup"><span data-stu-id="2d376-151">category</span></span> | <span data-ttu-id="2d376-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="2d376-152">OperationalLogs</span></span>

<span data-ttu-id="2d376-153">Este é um exemplo de uma cadeia de caracteres JSON do log operacional:</span><span class="sxs-lookup"><span data-stu-id="2d376-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="2d376-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d376-154">Next steps</span></span>

<span data-ttu-id="2d376-155">Visite Olá links toolearn mais sobre o barramento de serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d376-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="2d376-156">Introdução tooService barramento</span><span class="sxs-lookup"><span data-stu-id="2d376-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="2d376-157">Introdução ao Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="2d376-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
