---
title: "AAA \"evento de início da tarefa de lote do Azure | Microsoft Docs\""
description: "Referência de evento de início de tarefa de lote."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="a50f8-103">Evento de início da tarefa</span><span class="sxs-lookup"><span data-stu-id="a50f8-103">Task start event</span></span>

 <span data-ttu-id="a50f8-104">Esse evento é emitido quando uma tarefa tiver sido agendada toostart em um nó de computação pelo Agendador hello.</span><span class="sxs-lookup"><span data-stu-id="a50f8-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="a50f8-105">Observe que se a tarefa Olá é repetida ou retirada da fila esse evento será emitido novamente para hello mesma tarefa, mas Olá contagem de repetição e a versão da tarefa de sistema será atualizado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="a50f8-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="a50f8-106">Olá, exemplo a seguir mostra o corpo de saudação de um evento de início da tarefa.</span><span class="sxs-lookup"><span data-stu-id="a50f8-106">hello following example shows hello body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="a50f8-107">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a50f8-107">Element name</span></span>|<span data-ttu-id="a50f8-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="a50f8-108">Type</span></span>|<span data-ttu-id="a50f8-109">Observações</span><span class="sxs-lookup"><span data-stu-id="a50f8-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="a50f8-110">jobId</span><span class="sxs-lookup"><span data-stu-id="a50f8-110">jobId</span></span>|<span data-ttu-id="a50f8-111">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a50f8-111">String</span></span>|<span data-ttu-id="a50f8-112">id de saudação do trabalho de saudação que contém a tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="a50f8-113">ID</span><span class="sxs-lookup"><span data-stu-id="a50f8-113">id</span></span>|<span data-ttu-id="a50f8-114">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a50f8-114">String</span></span>|<span data-ttu-id="a50f8-115">id de saudação da tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-115">hello id of hello task.</span></span>|
|<span data-ttu-id="a50f8-116">taskType</span><span class="sxs-lookup"><span data-stu-id="a50f8-116">taskType</span></span>|<span data-ttu-id="a50f8-117">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a50f8-117">String</span></span>|<span data-ttu-id="a50f8-118">tipo de saudação da tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-118">hello type of hello task.</span></span> <span data-ttu-id="a50f8-119">Pode ser “JobManager” indicando que é uma tarefa do gerenciador de trabalhos ou “Usuário”, indicando que não é uma tarefa do gerenciador de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a50f8-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="a50f8-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="a50f8-120">systemTaskVersion</span></span>|<span data-ttu-id="a50f8-121">Int32</span><span class="sxs-lookup"><span data-stu-id="a50f8-121">Int32</span></span>|<span data-ttu-id="a50f8-122">Este é o contador de repetições interno de saudação em uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a50f8-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="a50f8-123">Internamente, serviço de lote de saudação pode repetir tooaccount uma tarefa para problemas transitórios.</span><span class="sxs-lookup"><span data-stu-id="a50f8-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="a50f8-124">Esses problemas podem incluir interno toorecover agendamento erros ou tentativas de nós de computação em um estado inválido.</span><span class="sxs-lookup"><span data-stu-id="a50f8-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="a50f8-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="a50f8-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="a50f8-126">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="a50f8-126">Complex Type</span></span>|<span data-ttu-id="a50f8-127">Contém informações sobre o nó de computação Olá no qual Olá tarefa foi executada.</span><span class="sxs-lookup"><span data-stu-id="a50f8-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="a50f8-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="a50f8-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="a50f8-129">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="a50f8-129">Complex Type</span></span>|<span data-ttu-id="a50f8-130">Especifica que Olá é tarefa várias instâncias que exigem vários nós de computação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="a50f8-131">Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a50f8-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="a50f8-132">restrições</span><span class="sxs-lookup"><span data-stu-id="a50f8-132">constraints</span></span>](#constraints)|<span data-ttu-id="a50f8-133">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="a50f8-133">Complex Type</span></span>|<span data-ttu-id="a50f8-134">restrições de execução de saudação que se aplicam a tarefa toothis.</span><span class="sxs-lookup"><span data-stu-id="a50f8-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="a50f8-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="a50f8-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="a50f8-136">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="a50f8-136">Complex Type</span></span>|<span data-ttu-id="a50f8-137">Contém informações sobre a execução de saudação da tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="a50f8-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="a50f8-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="a50f8-139">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a50f8-139">Element name</span></span>|<span data-ttu-id="a50f8-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="a50f8-140">Type</span></span>|<span data-ttu-id="a50f8-141">Observações</span><span class="sxs-lookup"><span data-stu-id="a50f8-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="a50f8-142">poolId</span><span class="sxs-lookup"><span data-stu-id="a50f8-142">poolId</span></span>|<span data-ttu-id="a50f8-143">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a50f8-143">String</span></span>|<span data-ttu-id="a50f8-144">id de saudação do pool de saudação em qual Olá tarefa foi executada de.</span><span class="sxs-lookup"><span data-stu-id="a50f8-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="a50f8-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="a50f8-145">nodeId</span></span>|<span data-ttu-id="a50f8-146">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a50f8-146">String</span></span>|<span data-ttu-id="a50f8-147">Olá o id do nó de saudação em qual Olá tarefa foi executada.</span><span class="sxs-lookup"><span data-stu-id="a50f8-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="a50f8-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="a50f8-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="a50f8-149">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a50f8-149">Element name</span></span>|<span data-ttu-id="a50f8-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="a50f8-150">Type</span></span>|<span data-ttu-id="a50f8-151">Observações</span><span class="sxs-lookup"><span data-stu-id="a50f8-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="a50f8-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="a50f8-152">numberOfInstances</span></span>|<span data-ttu-id="a50f8-153">int</span><span class="sxs-lookup"><span data-stu-id="a50f8-153">Int</span></span>|<span data-ttu-id="a50f8-154">número de saudação de nós de computação necessários pela tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="a50f8-155"><a name="constraints"></a> restrições</span><span class="sxs-lookup"><span data-stu-id="a50f8-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="a50f8-156">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a50f8-156">Element name</span></span>|<span data-ttu-id="a50f8-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="a50f8-157">Type</span></span>|<span data-ttu-id="a50f8-158">Observações</span><span class="sxs-lookup"><span data-stu-id="a50f8-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="a50f8-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="a50f8-159">maxTaskRetryCount</span></span>|<span data-ttu-id="a50f8-160">Int32</span><span class="sxs-lookup"><span data-stu-id="a50f8-160">Int32</span></span>|<span data-ttu-id="a50f8-161">Olá número máximo de vezes Olá tarefa pode ser repetida.</span><span class="sxs-lookup"><span data-stu-id="a50f8-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="a50f8-162">Olá serviço de lote repete uma tarefa se seu código de saída é diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="a50f8-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="a50f8-163">Observe que esse valor controla especificamente o número de tentativas de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="a50f8-164">serviço de lote Olá tentará a tarefa Olá uma vez e pode, em seguida, repita o limite de toothis.</span><span class="sxs-lookup"><span data-stu-id="a50f8-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="a50f8-165">Por exemplo, se a contagem de repetição máxima Olá é 3, o lote tenta uma tarefa de backup too4 vezes (uma tentativa inicial e 3 tentativas).</span><span class="sxs-lookup"><span data-stu-id="a50f8-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="a50f8-166">Se a contagem de repetição máxima Olá for 0, Olá serviço de lote não tenta novamente a tarefas.</span><span class="sxs-lookup"><span data-stu-id="a50f8-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="a50f8-167">Se a contagem de repetição máxima Olá é -1, o serviço de lote Olá repete tarefas sem limite.</span><span class="sxs-lookup"><span data-stu-id="a50f8-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="a50f8-168">valor padrão de saudação é 0 (sem repetições).</span><span class="sxs-lookup"><span data-stu-id="a50f8-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="a50f8-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="a50f8-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="a50f8-170">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a50f8-170">Element name</span></span>|<span data-ttu-id="a50f8-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="a50f8-171">Type</span></span>|<span data-ttu-id="a50f8-172">Observações</span><span class="sxs-lookup"><span data-stu-id="a50f8-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="a50f8-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="a50f8-173">retryCount</span></span>|<span data-ttu-id="a50f8-174">Int32</span><span class="sxs-lookup"><span data-stu-id="a50f8-174">Int32</span></span>|<span data-ttu-id="a50f8-175">Olá o número de vezes Olá tarefa foi repetida pelo serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50f8-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="a50f8-176">tarefa de saudação será repetida se ele for encerrada com um código de saída diferente de zero, o toohello especificado MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="a50f8-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
