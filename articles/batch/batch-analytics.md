---
title: "Análise de lote do Azure | Documentos do Microsoft"
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
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="70173-103">Análise de lote</span><span class="sxs-lookup"><span data-stu-id="70173-103">Batch Analytics</span></span>
<span data-ttu-id="70173-104">Os tópicos na Análise de lote contêm informações de referência para os eventos e alertas disponíveis para recursos de serviço em lotes.</span><span class="sxs-lookup"><span data-stu-id="70173-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="70173-105">Consulte [Registro em log de diagnóstico de Lote do Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) para obter mais informações sobre como habilitar e consumir logs de diagnóstico de lote.</span><span class="sxs-lookup"><span data-stu-id="70173-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="70173-106">Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="70173-106">Diagnostic logs</span></span>

<span data-ttu-id="70173-107">O serviço Lote do Azure emite os eventos de log de diagnóstico a seguir durante o tempo de vida de determinados recursos do lote.</span><span class="sxs-lookup"><span data-stu-id="70173-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="70173-108">**Eventos do Log de Serviço**</span><span class="sxs-lookup"><span data-stu-id="70173-108">**Service Log events**</span></span>
* [<span data-ttu-id="70173-109">Criação de pool</span><span class="sxs-lookup"><span data-stu-id="70173-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="70173-110">Início de exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="70173-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="70173-111">Conclusão da exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="70173-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="70173-112">Início de redimensionamento de pool</span><span class="sxs-lookup"><span data-stu-id="70173-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="70173-113">Conclusão de redimensionamento de pool</span><span class="sxs-lookup"><span data-stu-id="70173-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="70173-114">Início da tarefa</span><span class="sxs-lookup"><span data-stu-id="70173-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="70173-115">Conclusão da tarefa</span><span class="sxs-lookup"><span data-stu-id="70173-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="70173-116">Falha da tarefa</span><span class="sxs-lookup"><span data-stu-id="70173-116">Task fail</span></span>](batch-task-fail-event.md)