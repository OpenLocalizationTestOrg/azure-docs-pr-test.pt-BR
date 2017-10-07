---
title: "aaaAzure análise de lote | Microsoft Docs"
description: "Referência para análise de lote do Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="d454d-103">Análise de lote</span><span class="sxs-lookup"><span data-stu-id="d454d-103">Batch Analytics</span></span>
<span data-ttu-id="d454d-104">tópicos de saudação na análise do lote contêm informações de referência para eventos de saudação e alertas disponíveis para os recursos de serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="d454d-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="d454d-105">Consulte [Registro em log de diagnóstico de Lote do Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) para obter mais informações sobre como habilitar e consumir logs de diagnóstico de lote.</span><span class="sxs-lookup"><span data-stu-id="d454d-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="d454d-106">Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="d454d-106">Diagnostic logs</span></span>

<span data-ttu-id="d454d-107">Olá serviço de lote do Azure emite Olá eventos de log de diagnóstico a seguir durante a vida útil de saudação de determinados recursos de lote.</span><span class="sxs-lookup"><span data-stu-id="d454d-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="d454d-108">**Eventos do Log de Serviço**</span><span class="sxs-lookup"><span data-stu-id="d454d-108">**Service Log events**</span></span>
* [<span data-ttu-id="d454d-109">Criação de pool</span><span class="sxs-lookup"><span data-stu-id="d454d-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="d454d-110">Início de exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="d454d-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="d454d-111">Conclusão da exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="d454d-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="d454d-112">Início de redimensionamento de pool</span><span class="sxs-lookup"><span data-stu-id="d454d-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="d454d-113">Conclusão de redimensionamento de pool</span><span class="sxs-lookup"><span data-stu-id="d454d-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="d454d-114">Início da tarefa</span><span class="sxs-lookup"><span data-stu-id="d454d-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="d454d-115">Conclusão da tarefa</span><span class="sxs-lookup"><span data-stu-id="d454d-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="d454d-116">Falha da tarefa</span><span class="sxs-lookup"><span data-stu-id="d454d-116">Task fail</span></span>](batch-task-fail-event.md)