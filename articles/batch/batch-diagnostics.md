---
title: "aaaEnable log de diagnóstico para eventos de lote - Azure | Microsoft Docs"
description: "Registre e analisar eventos de log de diagnóstico para recursos de conta do Lote do Azure, como pools e tarefas."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="21e9b-103">Eventos de log para avaliação de diagnóstico e monitoramento de soluções do Lote</span><span class="sxs-lookup"><span data-stu-id="21e9b-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="21e9b-104">Assim como acontece com muitos serviços do Azure, Olá serviço de lote emite eventos de log para certos recursos durante Olá tempo de vida do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="21e9b-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="21e9b-105">Você pode habilitar eventos de toorecord de logs de diagnóstico do Azure Batch para recursos, como tarefas e pools e, em seguida, usar os logs de saudação para avaliação de diagnóstica e monitoramento.</span><span class="sxs-lookup"><span data-stu-id="21e9b-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="21e9b-106">Eventos como criação de pool, exclusão de pool, início da tarefa, conclusão de tarefa e outros são incluídos nos logs de diagnóstico do Lote.</span><span class="sxs-lookup"><span data-stu-id="21e9b-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="21e9b-107">Este artigo descreve os eventos de registro em log para os próprios recursos de conta do Lote, e não para os dados de saída de trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="21e9b-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="21e9b-108">Para obter detalhes sobre como armazenar dados de saída de saudação de seus trabalhos e tarefas, consulte [saída de trabalhos e tarefas de lote do Azure persistem](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="21e9b-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="21e9b-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="21e9b-109">Prerequisites</span></span>
* [<span data-ttu-id="21e9b-110">Conta do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="21e9b-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="21e9b-111">Conta do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="21e9b-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="21e9b-112">logs de diagnóstico toopersist em lotes, você deve criar uma conta de armazenamento do Azure em que o Azure armazenará Olá logs.</span><span class="sxs-lookup"><span data-stu-id="21e9b-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="21e9b-113">Especifique a conta de Armazenamento quando você [Habilitar o registro em log de diagnóstico](#enable-diagnostic-logging) para sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="21e9b-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="21e9b-114">Olá conta de armazenamento especificada quando você habilita a coleta de log não é Olá mesmo como uma saudação do armazenamento vinculado conta referida tooin [pacotes de aplicativos](batch-application-packages.md) e [persistência de saída da tarefa](batch-task-output.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="21e9b-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="21e9b-115">Você está **cobrado** para dados de saudação armazenados em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="21e9b-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="21e9b-116">Isso inclui logs de diagnóstico Olá discutido neste artigo.</span><span class="sxs-lookup"><span data-stu-id="21e9b-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="21e9b-117">Lembre-se disso ao projetar sua [política de retenção de log](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="21e9b-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="21e9b-118">Habilitar registro em log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="21e9b-118">Enable diagnostic logging</span></span>
<span data-ttu-id="21e9b-119">O registro em log de diagnóstico não está habilitado por padrão para sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="21e9b-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="21e9b-120">Você deve habilitar explicitamente o log de diagnóstico para cada conta de lote que você deseja toomonitor:</span><span class="sxs-lookup"><span data-stu-id="21e9b-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="21e9b-121">Como tooenable coleta de Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="21e9b-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="21e9b-122">É recomendável que você leia Olá completo [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo toogain entender não apenas como tooenable log, mas Olá log categorias suportados pelo Olá vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="21e9b-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="21e9b-123">Por exemplo, atualmente o Lote do Azure oferece suporte a uma categoria de log: **Logs de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="21e9b-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="21e9b-124">Logs de serviço</span><span class="sxs-lookup"><span data-stu-id="21e9b-124">Service Logs</span></span>
<span data-ttu-id="21e9b-125">Logs de serviço de lote do Azure contêm os eventos emitidos pelo serviço de lote do Azure Olá durante o tempo de vida de saudação de um recurso de lote como uma tarefa ou um pool.</span><span class="sxs-lookup"><span data-stu-id="21e9b-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="21e9b-126">Cada evento emitido pelo lote é armazenado no hello especificado conta de armazenamento no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="21e9b-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="21e9b-127">Por exemplo, este é o corpo de saudação de uma amostra de **criação do pool de evento**:</span><span class="sxs-lookup"><span data-stu-id="21e9b-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="21e9b-128">Cada corpo de evento reside em um. JSON arquivo hello especificou a conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="21e9b-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="21e9b-129">Se você quiser tooaccess Olá logs diretamente, poderá Olá tooreview [esquema dos Logs de diagnóstico na conta de armazenamento Olá](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="21e9b-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="21e9b-130">Eventos do Log de Serviço</span><span class="sxs-lookup"><span data-stu-id="21e9b-130">Service Log events</span></span>
<span data-ttu-id="21e9b-131">Olá serviço em lotes atualmente emite Olá eventos de Log do serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="21e9b-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="21e9b-132">Essa lista pode não ser completa, pois outros eventos podem ter sido adicionados desde a última atualização deste artigo.</span><span class="sxs-lookup"><span data-stu-id="21e9b-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="21e9b-133">**Eventos do Log de Serviço**</span><span class="sxs-lookup"><span data-stu-id="21e9b-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="21e9b-134">[Criação de pool][pool_create]</span><span class="sxs-lookup"><span data-stu-id="21e9b-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="21e9b-135">[Início de exclusão de pool][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="21e9b-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="21e9b-136">[Conclusão de exclusão de pool][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="21e9b-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="21e9b-137">[Início de redimensionamento de pool][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="21e9b-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="21e9b-138">[Conclusão de redimensionamento de pool][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="21e9b-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="21e9b-139">[Início de tarefa][task_start]</span><span class="sxs-lookup"><span data-stu-id="21e9b-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="21e9b-140">[Conclusão de tarefa][task_complete]</span><span class="sxs-lookup"><span data-stu-id="21e9b-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="21e9b-141">[Falha de tarefa][task_fail]</span><span class="sxs-lookup"><span data-stu-id="21e9b-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21e9b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21e9b-142">Next steps</span></span>
<span data-ttu-id="21e9b-143">Eventos de log de diagnóstico de toostoring de adição em uma conta de armazenamento do Azure, você também pode transmitir tooan de eventos de Log do serviço de lote [Hub de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)e enviá-los muito[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="21e9b-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="21e9b-144">Fluxo de Logs de diagnóstico do Azure tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="21e9b-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="21e9b-145">Serviço de entrada de dados altamente escalonável do lote eventos de diagnóstico toohello, Hubs de eventos de fluxo.</span><span class="sxs-lookup"><span data-stu-id="21e9b-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="21e9b-146">Os Hubs de Eventos podem incluir milhões de eventos por segundo, os quais você pode transformar e armazenar usando qualquer provedor de análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="21e9b-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="21e9b-147">Analisar logs de diagnóstico do Azure usando o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="21e9b-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="21e9b-148">Envie seu tooLog logs de diagnóstico análise onde analisá-los no portal do Operations Management Suite (OMS) hello ou exportá-los para análise no Power BI ou Excel.</span><span class="sxs-lookup"><span data-stu-id="21e9b-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
