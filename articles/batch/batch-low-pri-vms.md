---
title: "Executar cargas de trabalho do Lote do Azure em VMs econômicas de baixa prioridade (versão prévia) | Microsoft Docs"
description: Saiba como provisionar VMs de baixa prioridade para reduzir o custo das cargas de trabalho do Lote do Azure.
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="1d7ac-103">Usar VMs de baixa prioridade com o Lote (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="1d7ac-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="1d7ac-104">O Lote do Azure oferece VMs (máquinas virtuais) de baixa prioridade para reduzir o custo das cargas de trabalho no Lote.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="1d7ac-105">VMs de baixa prioridade possibilitam novos tipos de cargas de trabalho do Lote, fornecendo uma grande capacidade de computação que também é mais econômica.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="1d7ac-106">VMs de baixa prioridade tiram proveito da capacidade excedente do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="1d7ac-107">Quando você especifica VMs de baixa prioridade em seus pools, o Lote do Azure pode usar automaticamente esse excedente quando ele estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="1d7ac-108">A desvantagem de usar VMs de baixa prioridade é que essas VMs podem ser sofrer preempção quando não houver capacidade excedente disponível no Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="1d7ac-109">Por esse motivo, as VMs de baixa prioridade são mais adequadas para determinados tipos de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="1d7ac-110">Use VMs de baixa prioridade para cargas de trabalho de processamento assíncronas e em lote, em que o tempo para conclusão do trabalho é flexível e o trabalho é distribuído entre várias VMs.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="1d7ac-111">VMs de baixa prioridade são significativamente mais baratas que VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="1d7ac-112">Para ver detalhes dos preços, consulte [Preços do Lote](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="1d7ac-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="1d7ac-113">Para obter uma discussão adicional sobre VMs de baixa prioridade, consulte o comunicado de postagem de blog: [Computação em lote por uma fração do preço](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="1d7ac-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d7ac-114">Atualmente, as VMs de baixa prioridade estão na fase de versão prévia e estão disponíveis apenas para cargas de trabalho em execução no Lote.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="1d7ac-115">Casos de uso para VMs de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="1d7ac-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="1d7ac-116">Dadas as características das VMs de baixa prioridade, quais cargas de trabalho podem e não podem usá-las?</span><span class="sxs-lookup"><span data-stu-id="1d7ac-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="1d7ac-117">De modo geral, cargas de trabalho de processamento em lote são uma boa opção, uma vez que os trabalhos são divididos em várias tarefas paralelas ou há muitos trabalhos que são expandidos e distribuídos entre várias VMs.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="1d7ac-118">Para maximizar o uso da capacidade excedente no Azure, trabalhos adequados podem ser escalados horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="1d7ac-119">Ocasionalmente, as VMs podem não estar disponíveis ou podem sofrer preempção, o que levará a uma redução de capacidade para os trabalhos e pode levar a repetições e interrupções de tarefas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="1d7ac-120">Portanto, os trabalhos devem ser flexíveis quanto ao tempo necessário para executá-los.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="1d7ac-121">Trabalhos com tarefas mais longas podem ser mais afetados se forem interrompidos.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="1d7ac-122">Se tarefas de longa duração implementarem o uso de pontos de verificação para salvar o andamento conforme forem executadas, o impacto das interrupções será muito menor.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="1d7ac-123">Tarefas com tempos de execução menores tendem a funcionar melhor com VMs de baixa prioridade, pois o impacto da interrupção é muito menor.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="1d7ac-124">Trabalhos de MPI de longa duração que utilizam várias VMs não são adequados para o uso de VMs de baixa prioridade, pois uma VM que sofresse preempção provavelmente faria com que todo o trabalho precisasse ser executado novamente.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="1d7ac-125">Alguns exemplos de casos de uso de processamento em lote adequados ao uso de VMs de baixa prioridade são:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="1d7ac-126">**Desenvolvimento e teste**: em particular, se soluções de grande escala estiverem sendo desenvolvidas, economias significativas podem ser obtidas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="1d7ac-127">Todos os tipos de testes podem ser beneficiados, mas testes de carga de larga escala e testes de regressão são ótimas opções.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="1d7ac-128">**Complementação de capacidade sob demanda**: VMs de baixa prioridade podem ser usadas para complementar VMs dedicadas regulares – quando disponíveis, os trabalhos podem ser dimensionados e, portanto, concluídos mais rapidamente para reduzir o custo; quando não estiverem disponíveis, a linha de base de VMs dedicadas estará disponível.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="1d7ac-129">**Tempo de execução de trabalho flexível**: se houver flexibilidade quanto ao tempo necessário para concluir os trabalhos, quedas potencias na capacidade poderão ser toleradas. No entanto, com a adição de VMs de baixa prioridade, frequentemente os trabalhos serão executados mais rapidamente e por um custo mais baixo.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="1d7ac-130">Pools do Lote podem ser configurados para usar as VMs de baixa prioridade de algumas maneiras, dependendo da flexibilidade no tempo de execução do trabalho:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="1d7ac-131">VMs de baixa prioridade podem ser usadas somente em um pool e o Lote simplesmente recuperará qualquer capacidade ignorada quando disponível.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="1d7ac-132">Essa é a maneira mais econômica de executar trabalhos, pois somente VMs de baixa prioridade são usadas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="1d7ac-133">VMs de baixa prioridade podem ser usadas em conjunto com uma linha de base fixa de VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="1d7ac-134">O número fixo de VMs dedicadas garante que sempre haja alguma capacidade para manter um trabalho em andamento.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="1d7ac-135">Pode haver uma combinação dinâmica de VMs dedicadas e de baixa prioridade, para que as VMs de baixa prioridade, mais econômicas, sejam usadas somente quando disponíveis e as VMs dedicadas, com preço total, sejam expandidas quando necessário, de modo a manter uma quantidade mínima de capacidade disponível e manter os trabalhos em andamento.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="1d7ac-136">Suporte do Lote para VMs de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="1d7ac-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="1d7ac-137">O Lote do Azure fornece vários recursos que tornam mais fácil consumir e se beneficiar de VMs de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="1d7ac-138">Pools do Lote podem conter VMs dedicadas e VMs de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="1d7ac-139">O número de cada tipo de VM pode ser especificado quando o pool é criado e pode ser alterado a qualquer momento para um pool existente usando a operação de redimensionamento explícito ou o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="1d7ac-140">O envio de trabalhos e tarefas pode permanecer inalterado e não precisa se preocupar com os tipos de VM no pool.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="1d7ac-141">Também é possível fazer com que um pool use apenas VMs de baixa prioridade para executar trabalhos da forma mais econômica possível, mas use VMs dedicadas se a capacidade cair para baixo do limite mínimo, a fim de manter os trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="1d7ac-142">Pools do Lote buscam automaticamente usar o número alvo de VMs de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="1d7ac-143">Se as VMs sofrerem preempção, o Lote tentará substituir a capacidade perdida e retornar ao valor alvo.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="1d7ac-144">Caso as tarefas sejam interrompidas, o Lote detectará e, automaticamente, colocará em fila essas tarefas para que elas sejam executadas novamente.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="1d7ac-145">VMs de baixa prioridade têm uma cota de núcleos que difere das VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="1d7ac-146">A cotação para VMs de baixa prioridade é maior do que a das VMs dedicadas, porque as VMs de baixa prioridade custam menos.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="1d7ac-147">Consulte [Limites e cotas do serviço de Lote](batch-quota-limit.md#resource-quotas) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="1d7ac-148">Atualmente, VMs de baixa prioridade não têm suporte para contas do Lote em que o modo de alocação do pool é definido como [Assinatura de usuário](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="1d7ac-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="1d7ac-149">Criar e atualizar pools</span><span class="sxs-lookup"><span data-stu-id="1d7ac-149">Create and update pools</span></span>

<span data-ttu-id="1d7ac-150">Um pool do Lote pode conter VMs dedicadas e de baixa prioridade (também conhecidas como nós de computação).</span><span class="sxs-lookup"><span data-stu-id="1d7ac-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="1d7ac-151">É possível definir o número alvo de nós de computação para VMs dedicadas e de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="1d7ac-152">O número alvo de nós especifica o número de VMs que você deseja ter no pool.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="1d7ac-153">Por exemplo, para criar um pool usando VMs do serviço de nuvem do Azure tendo como valor alvo 5 VMs dedicadas e 20 VMs de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="1d7ac-154">Para criar um pool usando máquinas virtuais do Azure (neste caso, VMs Linux) tendo como valor alvo 5 VMs dedicadas e 20 VMs de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="1d7ac-155">É possível obter o número atual de nós para VMs dedicadas e de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="1d7ac-156">Os nós do pool têm uma propriedade para indicar se o nó é uma VM dedicada ou de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="1d7ac-157">Quando um ou mais nós de um pool sofrerem preempção, uma operação de listar nós no pool ainda retornará esses nós, o número atual de nós de baixa prioridade permanecerá inalterado, mas esses nós terão seu estado definido como **Admitiu Preempção**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="1d7ac-158">O Lote tentará localizar VMs substitutas e, se for bem-sucedido, os nós passarão pelos estados **Criando** e **Iniciando** antes de ficarem disponíveis para a execução da tarefa, assim como ocorreria com novos nós.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="1d7ac-159">Dimensionar um pool que contém VMs de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="1d7ac-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="1d7ac-160">Assim como acontece com pools que consistem somente em VMs dedicadas, é possível dimensionar um pool que contém VMs de baixa prioridade chamando o método Redimensionar ou usando o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="1d7ac-161">A operação de redimensionamento do pool usa um segundo parâmetro opcional que atualiza o valor de **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="1d7ac-162">A fórmula de dimensionamento automático do pool dá suporte a VMs de baixa prioridade, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="1d7ac-163">Você pode obter ou definir o valor da variável definida pelo serviço **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="1d7ac-164">Você pode obter o valor da variável definida pelo serviço **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="1d7ac-165">Você pode obter o valor da variável definida pelo serviço **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="1d7ac-166">Essa variável retorna o número de nós com estado "admitiu preempção" e permite que você expanda ou reduza o número de nós dedicados, dependendo do número de nós que admitiram preempção e que estão indisponíveis.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="1d7ac-167">Trabalhos e tarefas</span><span class="sxs-lookup"><span data-stu-id="1d7ac-167">Jobs and tasks</span></span>

<span data-ttu-id="1d7ac-168">Trabalhos e tarefas exigem muito pouco suporte para nós de baixa prioridade; o único suporte é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="1d7ac-169">A propriedade JobManagerTask de um trabalho tem uma nova propriedade, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="1d7ac-170">Quando essa propriedade tiver o valor "true", a tarefa do gerenciador de trabalho poderá ser agendada em um nó dedicado ou de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="1d7ac-171">Se essa propriedade tiver o valor "false", a tarefa do gerenciador de trabalho será agendada apenas para um nó dedicado.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="1d7ac-172">Um [variável de ambiente](batch-compute-node-environment-variables.md) está disponível para um aplicativo de tarefas para que ele possa determinar se ela está em execução em um nó de baixa prioridade ou dedicado.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="1d7ac-173">A variável de ambiente é AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="1d7ac-174">Tratamento de preempções</span><span class="sxs-lookup"><span data-stu-id="1d7ac-174">Handling preemption</span></span>

<span data-ttu-id="1d7ac-175">Ocasionalmente, as VMs podem sofrer preempção. Quando isso acontece, o lote faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="1d7ac-176">As VMs que sofreram preempção têm seu estado atualizado para **Admitiu Preempção**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="1d7ac-177">Caso tarefas estivessem sendo executadas nas VMs do nó que sofreu preempção, essas tarefas serão recolocadas em fila e serão executadas novamente.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="1d7ac-178">A VM será excluída efetivamente, o que fará com que todos os dados armazenados localmente na VM sejam perdidos.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="1d7ac-179">O pool tentará continuamente alcançar o número alvo de nós de baixa prioridade disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="1d7ac-180">Quando a capacidade de substituição for encontrada, os nós manterão suas IDs, mas serão reinicializados, passando pelos estados **Criando** e **Inicial** antes que fiquem disponíveis para o agendamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="1d7ac-181">Contagens de preempção estão disponíveis como uma métrica no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="1d7ac-182">Métricas</span><span class="sxs-lookup"><span data-stu-id="1d7ac-182">Metrics</span></span>

<span data-ttu-id="1d7ac-183">Novas métricas estão disponíveis no [Portal do Azure](https://portal.azure.com) para nós de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="1d7ac-184">Essas métricas são:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-184">These metrics are:</span></span>

- <span data-ttu-id="1d7ac-185">Contagem de nós de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="1d7ac-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="1d7ac-186">Contagem de núcleos de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="1d7ac-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="1d7ac-187">Contagem de nós com preempção</span><span class="sxs-lookup"><span data-stu-id="1d7ac-187">Preempted Node Count</span></span>

<span data-ttu-id="1d7ac-188">Para exibir as métricas no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="1d7ac-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="1d7ac-189">Navegue até sua conta do Lote no portal e exiba as configurações de sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="1d7ac-190">Selecione **Métricas** na seção **Monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="1d7ac-191">Selecione as métricas desejadas na lista **Métricas Disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Métricas para nós de baixa prioridade](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="1d7ac-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d7ac-193">Next steps</span></span>

* <span data-ttu-id="1d7ac-194">Leia ae [Visão geral de recursos do Lote para desenvolvedores](batch-api-basics.md), informações essenciais para qualquer pessoa que está se preparando para usar o Lote.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="1d7ac-195">O artigo contém informações mais detalhadas sobre os recursos de serviço do Lote, como pools, nós, trabalhos e tarefas, e os muitos recursos da API que você pode usar ao criar o aplicativo do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="1d7ac-196">Saiba mais sobre as [Ferramentas e APIs do Lote](batch-apis-tools.md) disponíveis para a criação de soluções do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d7ac-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
