---
title: "Habilitar o log de diagnóstico para Eventos em lote - Azure | Microsoft Docs"
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
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="3ad8e-103">Eventos de log para avaliação de diagnóstico e monitoramento de soluções do Lote</span><span class="sxs-lookup"><span data-stu-id="3ad8e-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="3ad8e-104">Assim como acontece com muitos serviços do Azure, o serviço de Lote emite eventos de log para certos recursos durante a vida útil do recurso.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="3ad8e-105">Você pode habilitar logs de diagnóstico do Lote do Azure para registrar eventos de recursos, como pools e tarefas, e usar os logs para a avaliação e monitoramento de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="3ad8e-106">Eventos como criação de pool, exclusão de pool, início da tarefa, conclusão de tarefa e outros são incluídos nos logs de diagnóstico do Lote.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad8e-107">Este artigo descreve os eventos de registro em log para os próprios recursos de conta do Lote, e não para os dados de saída de trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="3ad8e-108">Para obter detalhes sobre como armazenar os dados de saída de seus trabalhos e tarefas, confira [Persistir a saída de trabalhos e tarefas do Lote do Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="3ad8e-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3ad8e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ad8e-109">Prerequisites</span></span>
* [<span data-ttu-id="3ad8e-110">Conta do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="3ad8e-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="3ad8e-111">Conta do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3ad8e-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="3ad8e-112">Para persistir os logs de diagnóstico do Lote, você deve criar uma conta de Armazenamento do Azure na qual o Azure armazenará os logs.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="3ad8e-113">Especifique a conta de Armazenamento quando você [Habilitar o registro em log de diagnóstico](#enable-diagnostic-logging) para sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="3ad8e-114">A conta de Armazenamento especificada quando você habilita a coleta de log não é a mesma que uma conta de armazenamento vinculada citada nos artigos [pacotes de aplicativos](batch-application-packages.md) e [persistência de saída da tarefa](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="3ad8e-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="3ad8e-115">Você é **cobrado** pelos dados armazenados em sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="3ad8e-116">Isso inclui os logs de diagnóstico discutidos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="3ad8e-117">Lembre-se disso ao projetar sua [política de retenção de log](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="3ad8e-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="3ad8e-118">Habilitar registro em log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="3ad8e-118">Enable diagnostic logging</span></span>
<span data-ttu-id="3ad8e-119">O registro em log de diagnóstico não está habilitado por padrão para sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="3ad8e-120">Você deve habilitar explicitamente o registro em log de diagnóstico para cada conta do Lote que você deseja monitorar:</span><span class="sxs-lookup"><span data-stu-id="3ad8e-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="3ad8e-121">Como habilitar a coleção de Logs de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="3ad8e-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="3ad8e-122">Recomendamos que você leia todo o artigo [Visão geral dos Logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para entender não apenas como habilitar o registro em log, mas também as categorias de log com suporte dos vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="3ad8e-123">Por exemplo, atualmente o Lote do Azure oferece suporte a uma categoria de log: **Logs de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="3ad8e-124">Logs de serviço</span><span class="sxs-lookup"><span data-stu-id="3ad8e-124">Service Logs</span></span>
<span data-ttu-id="3ad8e-125">Os Logs de serviço do Lote do Azure contêm os eventos emitidos pelo serviço de Lote do Azure durante o tempo de vida de um recurso do Lote como uma tarefa ou um pool.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="3ad8e-126">Cada evento emitido pelo Lote é armazenado na conta de Armazenamento especificada no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="3ad8e-127">Por exemplo, este é o corpo de um exemplo de **evento de criação de pool**:</span><span class="sxs-lookup"><span data-stu-id="3ad8e-127">For example, this is the body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="3ad8e-128">Cada corpo de evento reside em um arquivo .json na conta especificada do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="3ad8e-129">Se você quiser acessar os logs diretamente, talvez você queira examinar o [esquema de Logs de Diagnóstico na conta de armazenamento](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3ad8e-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="3ad8e-130">Eventos do Log de Serviço</span><span class="sxs-lookup"><span data-stu-id="3ad8e-130">Service Log events</span></span>
<span data-ttu-id="3ad8e-131">O serviço do Lote emite atualmente os seguintes eventos do Log de Serviço.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="3ad8e-132">Essa lista pode não ser completa, pois outros eventos podem ter sido adicionados desde a última atualização deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="3ad8e-133">**Eventos do Log de Serviço**</span><span class="sxs-lookup"><span data-stu-id="3ad8e-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="3ad8e-134">[Criação de pool][pool_create]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="3ad8e-135">[Início de exclusão de pool][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="3ad8e-136">[Conclusão de exclusão de pool][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="3ad8e-137">[Início de redimensionamento de pool][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="3ad8e-138">[Conclusão de redimensionamento de pool][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="3ad8e-139">[Início de tarefa][task_start]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="3ad8e-140">[Conclusão de tarefa][task_complete]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="3ad8e-141">[Falha de tarefa][task_fail]</span><span class="sxs-lookup"><span data-stu-id="3ad8e-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ad8e-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ad8e-142">Next steps</span></span>
<span data-ttu-id="3ad8e-143">Além de armazenar os eventos do log de diagnóstico em uma conta de Armazenamento do Azure, você também pode transmitir eventos do Log de Serviço do Lote para um [Hub de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md), e enviá-los para o [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ad8e-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="3ad8e-144">Transmitir Logs de Diagnóstico do Azure para os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3ad8e-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="3ad8e-145">Transmita os eventos de diagnóstico do Lote para o serviço de entrada de dados altamente dimensionável, Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="3ad8e-146">Os Hubs de Eventos podem incluir milhões de eventos por segundo, os quais você pode transformar e armazenar usando qualquer provedor de análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="3ad8e-147">Analisar logs de diagnóstico do Azure usando o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3ad8e-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="3ad8e-148">Envie seus logs de diagnóstico para o Log Analytics, onde você pode analisá-los no portal do OMS (Operations Management Suite) ou exportá-los para análise no Power BI ou Excel.</span><span class="sxs-lookup"><span data-stu-id="3ad8e-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
