---
title: AAA "evento inicial de redimensionamento do pool de lote do Azure | Microsoft Docs"
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="40fb7-103">Evento inicial de redimensionamento de pool</span><span class="sxs-lookup"><span data-stu-id="40fb7-103">Pool resize start event</span></span>

 <span data-ttu-id="40fb7-104">Esse evento é emitido quando um redimensionamento de pool é iniciado.</span><span class="sxs-lookup"><span data-stu-id="40fb7-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="40fb7-105">Como o redimensionamento do pool de saudação é um evento assíncrono, você pode esperar um toobe de evento de conclusão de redimensionamento pool emitido depois que a operação de redimensionamento Olá for concluída.</span><span class="sxs-lookup"><span data-stu-id="40fb7-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="40fb7-106">redimensiona Olá mostra Olá corpo de um evento de início de redimensionamento do pool para um pool de redimensionamento de 0 nós too2 com um manual de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="40fb7-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="40fb7-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="40fb7-107">Element</span></span>|<span data-ttu-id="40fb7-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="40fb7-108">Type</span></span>|<span data-ttu-id="40fb7-109">Observações</span><span class="sxs-lookup"><span data-stu-id="40fb7-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="40fb7-110">poolId</span><span class="sxs-lookup"><span data-stu-id="40fb7-110">poolId</span></span>|<span data-ttu-id="40fb7-111">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="40fb7-111">String</span></span>|<span data-ttu-id="40fb7-112">id de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="40fb7-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="40fb7-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="40fb7-113">nodeDeallocationOption</span></span>|<span data-ttu-id="40fb7-114">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="40fb7-114">String</span></span>|<span data-ttu-id="40fb7-115">Especifica quando nós podem ser removidos do pool hello, se o tamanho do pool de saudação está diminuindo.</span><span class="sxs-lookup"><span data-stu-id="40fb7-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="40fb7-116">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="40fb7-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="40fb7-117">**colocar novamente na fila** – Finalize as tarefas em execução e coloque-as novamente na fila.</span><span class="sxs-lookup"><span data-stu-id="40fb7-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="40fb7-118">tarefas de saudação serão executadas novamente quando o trabalho de saudação está habilitado.</span><span class="sxs-lookup"><span data-stu-id="40fb7-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="40fb7-119">Remova nós assim que tarefas forem terminadas.</span><span class="sxs-lookup"><span data-stu-id="40fb7-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="40fb7-120">**terminar** – Termine as tarefas em execução.</span><span class="sxs-lookup"><span data-stu-id="40fb7-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="40fb7-121">tarefas de saudação não serão executado novamente.</span><span class="sxs-lookup"><span data-stu-id="40fb7-121">hello tasks will not run again.</span></span> <span data-ttu-id="40fb7-122">Remova nós assim que tarefas forem terminadas.</span><span class="sxs-lookup"><span data-stu-id="40fb7-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="40fb7-123">**taskcompletion** – permitir em toocomplete de tarefas em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="40fb7-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="40fb7-124">Não agende novas tarefas enquanto aguarda.</span><span class="sxs-lookup"><span data-stu-id="40fb7-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="40fb7-125">Remova nós quando todas as tarefas forem concluídas.</span><span class="sxs-lookup"><span data-stu-id="40fb7-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="40fb7-126">**Retaineddata** - permitir executando tarefas toocomplete e esperar até que todas as tarefas tooexpire de períodos de retenção de dados.</span><span class="sxs-lookup"><span data-stu-id="40fb7-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="40fb7-127">Não agende novas tarefas enquanto aguarda.</span><span class="sxs-lookup"><span data-stu-id="40fb7-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="40fb7-128">Remova nós quando todos os períodos de retenção de tarefa expirem.</span><span class="sxs-lookup"><span data-stu-id="40fb7-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="40fb7-129">valor padrão de saudação é enfileiramento.</span><span class="sxs-lookup"><span data-stu-id="40fb7-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="40fb7-130">Se tamanho de pool hello está aumentando, valor hello está definido muito**inválido**.</span><span class="sxs-lookup"><span data-stu-id="40fb7-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="40fb7-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="40fb7-131">currentDedicated</span></span>|<span data-ttu-id="40fb7-132">Int32</span><span class="sxs-lookup"><span data-stu-id="40fb7-132">Int32</span></span>|<span data-ttu-id="40fb7-133">número de saudação de nós de computação atualmente atribuído toohello pool.</span><span class="sxs-lookup"><span data-stu-id="40fb7-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="40fb7-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="40fb7-134">targetDedicated</span></span>|<span data-ttu-id="40fb7-135">Int32</span><span class="sxs-lookup"><span data-stu-id="40fb7-135">Int32</span></span>|<span data-ttu-id="40fb7-136">número de saudação de nós de computação que são solicitadas para o pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="40fb7-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="40fb7-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="40fb7-137">enableAutoScale</span></span>|<span data-ttu-id="40fb7-138">Bool</span><span class="sxs-lookup"><span data-stu-id="40fb7-138">Bool</span></span>|<span data-ttu-id="40fb7-139">Especifica se o tamanho do pool de saudação ajusta automaticamente ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="40fb7-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="40fb7-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="40fb7-140">isAutoPool</span></span>|<span data-ttu-id="40fb7-141">Bool</span><span class="sxs-lookup"><span data-stu-id="40fb7-141">Bool</span></span>|<span data-ttu-id="40fb7-142">Especifica se o pool de saudação foi criado por meio do mecanismo de pool automático de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="40fb7-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
