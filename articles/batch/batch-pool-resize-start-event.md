---
title: Evento inicial de redimensionamento de pool de lote do Azure | Documentos do Microsoft
description: "Referência de redimensionamento do pool de lote evento inicial."
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="b16f4-103">Evento inicial de redimensionamento de pool</span><span class="sxs-lookup"><span data-stu-id="b16f4-103">Pool resize start event</span></span>

 <span data-ttu-id="b16f4-104">Esse evento é emitido quando um redimensionamento de pool é iniciado.</span><span class="sxs-lookup"><span data-stu-id="b16f4-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="b16f4-105">Como o redimensionamento do pool é um evento assíncrono, você pode esperar que um evento completo de redimensionamento de pool seja emitido quando a operação de redimensionamento é concluída.</span><span class="sxs-lookup"><span data-stu-id="b16f4-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="b16f4-106">O exemplo a seguir mostra o corpo de um evento inicial de redimensionamento de pool para um redimensionamento de 0 a 2 nós com redimensionamento manual.</span><span class="sxs-lookup"><span data-stu-id="b16f4-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="b16f4-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="b16f4-107">Element</span></span>|<span data-ttu-id="b16f4-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="b16f4-108">Type</span></span>|<span data-ttu-id="b16f4-109">Observações</span><span class="sxs-lookup"><span data-stu-id="b16f4-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b16f4-110">poolId</span><span class="sxs-lookup"><span data-stu-id="b16f4-110">poolId</span></span>|<span data-ttu-id="b16f4-111">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b16f4-111">String</span></span>|<span data-ttu-id="b16f4-112">A ID do pool.</span><span class="sxs-lookup"><span data-stu-id="b16f4-112">The id of the pool.</span></span>|
|<span data-ttu-id="b16f4-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="b16f4-113">nodeDeallocationOption</span></span>|<span data-ttu-id="b16f4-114">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b16f4-114">String</span></span>|<span data-ttu-id="b16f4-115">Especifica quando os nós poderão ser removidos do pool, se o tamanho do pool estiver diminuindo.</span><span class="sxs-lookup"><span data-stu-id="b16f4-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="b16f4-116">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="b16f4-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="b16f4-117">**colocar novamente na fila** – Finalize as tarefas em execução e coloque-as novamente na fila.</span><span class="sxs-lookup"><span data-stu-id="b16f4-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="b16f4-118">As tarefas serão executadas novamente quando o trabalho for habilitado.</span><span class="sxs-lookup"><span data-stu-id="b16f4-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="b16f4-119">Remova nós assim que tarefas forem terminadas.</span><span class="sxs-lookup"><span data-stu-id="b16f4-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b16f4-120">**terminar** – Termine as tarefas em execução.</span><span class="sxs-lookup"><span data-stu-id="b16f4-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="b16f4-121">As tarefas não serão executadas novamente.</span><span class="sxs-lookup"><span data-stu-id="b16f4-121">The tasks will not run again.</span></span> <span data-ttu-id="b16f4-122">Remova nós assim que tarefas forem terminadas.</span><span class="sxs-lookup"><span data-stu-id="b16f4-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b16f4-123">**taskcompletion** – Permita a conclusão das tarefas atualmente em execução.</span><span class="sxs-lookup"><span data-stu-id="b16f4-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="b16f4-124">Não agende novas tarefas enquanto aguarda.</span><span class="sxs-lookup"><span data-stu-id="b16f4-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b16f4-125">Remova nós quando todas as tarefas forem concluídas.</span><span class="sxs-lookup"><span data-stu-id="b16f4-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="b16f4-126">**Retaineddata** – Permita que as tarefas atualmente em execução sejam concluídas e aguarde que os todos os períodos de retenção de dados das tarefas expirem.</span><span class="sxs-lookup"><span data-stu-id="b16f4-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="b16f4-127">Não agende novas tarefas enquanto aguarda.</span><span class="sxs-lookup"><span data-stu-id="b16f4-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b16f4-128">Remova nós quando todos os períodos de retenção de tarefa expirem.</span><span class="sxs-lookup"><span data-stu-id="b16f4-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="b16f4-129">O valor padrão é colocar novamente na fila.</span><span class="sxs-lookup"><span data-stu-id="b16f4-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="b16f4-130">Se o tamanho do pool aumentar, o valor será definido como **inválido**.</span><span class="sxs-lookup"><span data-stu-id="b16f4-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="b16f4-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="b16f4-131">currentDedicated</span></span>|<span data-ttu-id="b16f4-132">Int32</span><span class="sxs-lookup"><span data-stu-id="b16f4-132">Int32</span></span>|<span data-ttu-id="b16f4-133">O número de nós de computação atualmente atribuídos ao pool.</span><span class="sxs-lookup"><span data-stu-id="b16f4-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="b16f4-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="b16f4-134">targetDedicated</span></span>|<span data-ttu-id="b16f4-135">Int32</span><span class="sxs-lookup"><span data-stu-id="b16f4-135">Int32</span></span>|<span data-ttu-id="b16f4-136">O número de nós de computação solicitados para o pool.</span><span class="sxs-lookup"><span data-stu-id="b16f4-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="b16f4-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="b16f4-137">enableAutoScale</span></span>|<span data-ttu-id="b16f4-138">Bool</span><span class="sxs-lookup"><span data-stu-id="b16f4-138">Bool</span></span>|<span data-ttu-id="b16f4-139">Especifica se o tamanho do pool é ajustado automaticamente com o tempo.</span><span class="sxs-lookup"><span data-stu-id="b16f4-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="b16f4-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="b16f4-140">isAutoPool</span></span>|<span data-ttu-id="b16f4-141">Bool</span><span class="sxs-lookup"><span data-stu-id="b16f4-141">Bool</span></span>|<span data-ttu-id="b16f4-142">Especifica se o pool foi criado por meio de um mecanismo de AutoPool do trabalho.</span><span class="sxs-lookup"><span data-stu-id="b16f4-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
