---
title: "Eventos de início de tarefa em lote do Azure | Microsoft Docs"
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="33ab6-103">Evento de início da tarefa</span><span class="sxs-lookup"><span data-stu-id="33ab6-103">Task start event</span></span>

 <span data-ttu-id="33ab6-104">Esse evento é emitido quando uma tarefa é agendada para iniciar em um nó de computação pelo agendador.</span><span class="sxs-lookup"><span data-stu-id="33ab6-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="33ab6-105">Observe que, se a tarefa for repetida ou colocada novamente na fila, esse evento será emitido novamente para a mesma tarefa, mas a contagem de repetição e versão de tarefa do sistema serão atualizadas adequadamente.</span><span class="sxs-lookup"><span data-stu-id="33ab6-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="33ab6-106">O exemplo a seguir mostra o corpo de um evento de início da tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-106">The following example shows the body of a task start event.</span></span>

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

|<span data-ttu-id="33ab6-107">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="33ab6-107">Element name</span></span>|<span data-ttu-id="33ab6-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="33ab6-108">Type</span></span>|<span data-ttu-id="33ab6-109">Observações</span><span class="sxs-lookup"><span data-stu-id="33ab6-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="33ab6-110">jobId</span><span class="sxs-lookup"><span data-stu-id="33ab6-110">jobId</span></span>|<span data-ttu-id="33ab6-111">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="33ab6-111">String</span></span>|<span data-ttu-id="33ab6-112">A ID do trabalho que contém a tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="33ab6-113">ID</span><span class="sxs-lookup"><span data-stu-id="33ab6-113">id</span></span>|<span data-ttu-id="33ab6-114">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="33ab6-114">String</span></span>|<span data-ttu-id="33ab6-115">A ID da tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-115">The id of the task.</span></span>|
|<span data-ttu-id="33ab6-116">taskType</span><span class="sxs-lookup"><span data-stu-id="33ab6-116">taskType</span></span>|<span data-ttu-id="33ab6-117">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="33ab6-117">String</span></span>|<span data-ttu-id="33ab6-118">O tipo de tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-118">The type of the task.</span></span> <span data-ttu-id="33ab6-119">Pode ser “JobManager” indicando que é uma tarefa do gerenciador de trabalhos ou “Usuário”, indicando que não é uma tarefa do gerenciador de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="33ab6-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="33ab6-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="33ab6-120">systemTaskVersion</span></span>|<span data-ttu-id="33ab6-121">Int32</span><span class="sxs-lookup"><span data-stu-id="33ab6-121">Int32</span></span>|<span data-ttu-id="33ab6-122">Esse é o contador interno de repetição de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="33ab6-123">Internamente, o serviço em lotes pode repetir uma tarefa para contabilizar problemas transitórios.</span><span class="sxs-lookup"><span data-stu-id="33ab6-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="33ab6-124">Esses problemas podem incluir erros internos de agendamento ou tentativa de recuperar nós de computação em estado inválido.</span><span class="sxs-lookup"><span data-stu-id="33ab6-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="33ab6-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="33ab6-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="33ab6-126">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="33ab6-126">Complex Type</span></span>|<span data-ttu-id="33ab6-127">Contém informações sobre o nó de computação em que a tarefa é executada.</span><span class="sxs-lookup"><span data-stu-id="33ab6-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="33ab6-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="33ab6-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="33ab6-129">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="33ab6-129">Complex Type</span></span>|<span data-ttu-id="33ab6-130">Especifica que a tarefa é uma tarefa com várias instâncias que precisa de vários nós de computação.</span><span class="sxs-lookup"><span data-stu-id="33ab6-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="33ab6-131">Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="33ab6-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="33ab6-132">restrições</span><span class="sxs-lookup"><span data-stu-id="33ab6-132">constraints</span></span>](#constraints)|<span data-ttu-id="33ab6-133">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="33ab6-133">Complex Type</span></span>|<span data-ttu-id="33ab6-134">As restrições de execução aplicáveis a essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="33ab6-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="33ab6-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="33ab6-136">Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="33ab6-136">Complex Type</span></span>|<span data-ttu-id="33ab6-137">Contém informações sobre a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="33ab6-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="33ab6-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="33ab6-139">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="33ab6-139">Element name</span></span>|<span data-ttu-id="33ab6-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="33ab6-140">Type</span></span>|<span data-ttu-id="33ab6-141">Observações</span><span class="sxs-lookup"><span data-stu-id="33ab6-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="33ab6-142">poolId</span><span class="sxs-lookup"><span data-stu-id="33ab6-142">poolId</span></span>|<span data-ttu-id="33ab6-143">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="33ab6-143">String</span></span>|<span data-ttu-id="33ab6-144">A ID do pool em que a tarefa foi executada.</span><span class="sxs-lookup"><span data-stu-id="33ab6-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="33ab6-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="33ab6-145">nodeId</span></span>|<span data-ttu-id="33ab6-146">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="33ab6-146">String</span></span>|<span data-ttu-id="33ab6-147">A ID do nó em que a tarefa foi executada.</span><span class="sxs-lookup"><span data-stu-id="33ab6-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="33ab6-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="33ab6-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="33ab6-149">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="33ab6-149">Element name</span></span>|<span data-ttu-id="33ab6-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="33ab6-150">Type</span></span>|<span data-ttu-id="33ab6-151">Observações</span><span class="sxs-lookup"><span data-stu-id="33ab6-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="33ab6-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="33ab6-152">numberOfInstances</span></span>|<span data-ttu-id="33ab6-153">int</span><span class="sxs-lookup"><span data-stu-id="33ab6-153">Int</span></span>|<span data-ttu-id="33ab6-154">O número de nós de computação que a tarefa precisa.</span><span class="sxs-lookup"><span data-stu-id="33ab6-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="33ab6-155"><a name="constraints"></a> restrições</span><span class="sxs-lookup"><span data-stu-id="33ab6-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="33ab6-156">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="33ab6-156">Element name</span></span>|<span data-ttu-id="33ab6-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="33ab6-157">Type</span></span>|<span data-ttu-id="33ab6-158">Observações</span><span class="sxs-lookup"><span data-stu-id="33ab6-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="33ab6-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="33ab6-159">maxTaskRetryCount</span></span>|<span data-ttu-id="33ab6-160">Int32</span><span class="sxs-lookup"><span data-stu-id="33ab6-160">Int32</span></span>|<span data-ttu-id="33ab6-161">O número máximo de vezes que a tarefa pode ser repetida.</span><span class="sxs-lookup"><span data-stu-id="33ab6-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="33ab6-162">O serviço em lotes repetirá uma tarefa se seu código de saída for diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="33ab6-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="33ab6-163">Observe que esse valor controla especificamente o número de tentativas.</span><span class="sxs-lookup"><span data-stu-id="33ab6-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="33ab6-164">O serviço em lotes tentará a tarefa uma vez e, em seguida, pode tentar novamente até esse limite.</span><span class="sxs-lookup"><span data-stu-id="33ab6-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="33ab6-165">Por exemplo, se a contagem máxima de repetição for 3, o lote tentará uma tarefa até 4 vezes (uma tentativa inicial e 3 repetições).</span><span class="sxs-lookup"><span data-stu-id="33ab6-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="33ab6-166">Se a contagem máxima de repetição for 0, o serviço em lote não tentará repetir a tarefas.</span><span class="sxs-lookup"><span data-stu-id="33ab6-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="33ab6-167">Se a contagem máxima de repetição for -1, o serviço em lotes repetirá as tarefas ilimitadamente.</span><span class="sxs-lookup"><span data-stu-id="33ab6-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="33ab6-168">O valor padrão é 0 (sem novas tentativas).</span><span class="sxs-lookup"><span data-stu-id="33ab6-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="33ab6-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="33ab6-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="33ab6-170">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="33ab6-170">Element name</span></span>|<span data-ttu-id="33ab6-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="33ab6-171">Type</span></span>|<span data-ttu-id="33ab6-172">Observações</span><span class="sxs-lookup"><span data-stu-id="33ab6-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="33ab6-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="33ab6-173">retryCount</span></span>|<span data-ttu-id="33ab6-174">Int32</span><span class="sxs-lookup"><span data-stu-id="33ab6-174">Int32</span></span>|<span data-ttu-id="33ab6-175">O número de vezes que a tarefa foi repetida pelo serviço em lotes.</span><span class="sxs-lookup"><span data-stu-id="33ab6-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="33ab6-176">A tarefa será repetida se a saída tiver um código de saída diferente de zero, até a MaxTaskRetryCount especificada</span><span class="sxs-lookup"><span data-stu-id="33ab6-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
