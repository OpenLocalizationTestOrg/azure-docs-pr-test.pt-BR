---
title: "aaaRun cargas de trabalho de lote do Azure em VMs de baixa prioridade econômicas (visualização) | Microsoft Docs"
description: "Saiba como saudação de tooreduce de VMs de baixa prioridade tooprovision custo de cargas de trabalho de lote do Azure."
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
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="33a94-103">Usar VMs de baixa prioridade com o Lote (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="33a94-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="33a94-104">Lote do Azure oferece o custo de saudação tooreduce baixa priorty máquinas de virtuais (VMs) de cargas de trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="33a94-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="33a94-105">VMs de baixa prioridade possibilitam novos tipos de cargas de trabalho do Lote, fornecendo uma grande capacidade de computação que também é mais econômica.</span><span class="sxs-lookup"><span data-stu-id="33a94-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="33a94-106">VMs de baixa prioridade tiram proveito da capacidade excedente do Azure.</span><span class="sxs-lookup"><span data-stu-id="33a94-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="33a94-107">Quando você especifica VMs de baixa prioridade em seus pools, o Lote do Azure pode usar automaticamente esse excedente quando ele estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="33a94-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="33a94-108">compensação Olá para o uso de máquinas virtuais de prioridade baixa é que essas VMs podem ser apropriadas quando não há capacidade excedente está disponível no Azure.</span><span class="sxs-lookup"><span data-stu-id="33a94-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="33a94-109">Por esse motivo, as VMs de baixa prioridade são mais adequadas para determinados tipos de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="33a94-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="33a94-110">Use máquinas virtuais de baixa prioridade para o lote e cargas de trabalho de processamento assíncrono em que o tempo de conclusão do trabalho de saudação é flexível e trabalho Olá é distribuído entre várias VMs.</span><span class="sxs-lookup"><span data-stu-id="33a94-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="33a94-111">VMs de baixa prioridade são significativamente mais baratas que VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="33a94-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="33a94-112">Para ver detalhes dos preços, consulte [Preços do Lote](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="33a94-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="33a94-113">Para uma discussão adicional de VMs de baixa prioridade, consulte o anúncio de postagem de blog Olá: [em lote de computação em uma fração do preço Olá](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="33a94-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33a94-114">Atualmente, as VMs de baixa prioridade estão na fase de versão prévia e estão disponíveis apenas para cargas de trabalho em execução no Lote.</span><span class="sxs-lookup"><span data-stu-id="33a94-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="33a94-115">Casos de uso para VMs de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="33a94-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="33a94-116">Dadas as características de saudação de VMs de baixa prioridade, quais cargas de trabalho podem e não podem usá-los?</span><span class="sxs-lookup"><span data-stu-id="33a94-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="33a94-117">De modo geral, cargas de trabalho de processamento em lote são uma boa opção, uma vez que os trabalhos são divididos em várias tarefas paralelas ou há muitos trabalhos que são expandidos e distribuídos entre várias VMs.</span><span class="sxs-lookup"><span data-stu-id="33a94-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="33a94-118">uso de toomaximize de capacidade excedente em trabalhos do Azure, adequados pode expandir.</span><span class="sxs-lookup"><span data-stu-id="33a94-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="33a94-119">Ocasionalmente, máquinas virtuais podem não estar disponíveis ou serão superados, que resultará na capacidade reduzida de trabalhos e pode causar a execução repetida e tootask interrupção.</span><span class="sxs-lookup"><span data-stu-id="33a94-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="33a94-120">Trabalhos, portanto, devem ser flexíveis em tempo de saudação que toorun podem ser tomadas.</span><span class="sxs-lookup"><span data-stu-id="33a94-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="33a94-121">Trabalhos com tarefas mais longas podem ser mais afetados se forem interrompidos.</span><span class="sxs-lookup"><span data-stu-id="33a94-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="33a94-122">Se demoradas tarefas implementam o andamento do ponto de verificação toosave conforme eles são executados, em seguida, o impacto de interrupção seria muito menor.</span><span class="sxs-lookup"><span data-stu-id="33a94-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="33a94-123">Tarefas com tempos de execução menores tendem toowork melhor com baixa prioridade VMs como Olá impacto de interrupção é muito menor.</span><span class="sxs-lookup"><span data-stu-id="33a94-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="33a94-124">Trabalhos MPI que utilizam várias VMs não são toouse adequado de longa execução VMs de baixa prioridade como uma VM admitiu preempção serão provavelmente lead toohello todo trabalho executará toobe novamente.</span><span class="sxs-lookup"><span data-stu-id="33a94-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="33a94-125">Alguns exemplos de processamento em lotes usam casos toouse adequado VMs de baixa prioridade são:</span><span class="sxs-lookup"><span data-stu-id="33a94-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="33a94-126">**Desenvolvimento e teste**: em particular, se soluções de grande escala estiverem sendo desenvolvidas, economias significativas podem ser obtidas.</span><span class="sxs-lookup"><span data-stu-id="33a94-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="33a94-127">Todos os tipos de testes podem ser beneficiados, mas testes de carga de larga escala e testes de regressão são ótimas opções.</span><span class="sxs-lookup"><span data-stu-id="33a94-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="33a94-128">**Complementando a capacidade sob demanda**: VMs de baixa prioridade podem ser usadas para complementar as VMs regular dedicadas - quando disponível, os trabalhos podem dimensionar e, portanto, conclua mais rápido para reduzir o custo; quando não está disponível, linha de base de saudação do dedicado VMs estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="33a94-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="33a94-129">**Tempo de execução de trabalho flexível**: se há flexibilidade em trabalhos de timer Olá ter toocomplete, e em seguida, descarta potencial na capacidade pode ser tolerada; no entanto, com hello adição dos trabalhos de VMs de baixa prioridade frequentemente será executado mais rapidamente e para reduzir o custo.</span><span class="sxs-lookup"><span data-stu-id="33a94-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="33a94-130">Pools de lote podem ser configurado toouse VMs de baixa prioridade de algumas maneiras, dependendo da flexibilidade de saudação em tempo de execução do trabalho:</span><span class="sxs-lookup"><span data-stu-id="33a94-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="33a94-131">VMs de baixa prioridade podem ser usadas somente em um pool e o Lote simplesmente recuperará qualquer capacidade ignorada quando disponível.</span><span class="sxs-lookup"><span data-stu-id="33a94-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="33a94-132">Isso é mais baratos trabalhos de tooexecute de maneira hello como VMs de baixa prioridade só são usadas.</span><span class="sxs-lookup"><span data-stu-id="33a94-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="33a94-133">VMs de baixa prioridade podem ser usadas em conjunto com uma linha de base fixa de VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="33a94-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="33a94-134">Olá número fixo de VMs dedicados garante que haja sempre alguns tookeep capacidade um trabalho em andamento.</span><span class="sxs-lookup"><span data-stu-id="33a94-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="33a94-135">Pode ser dinâmica mistura de VMs dedicadas e de baixa prioridade, para que as VMs de baixa prioridade mais baratas são usadas somente quando disponível, mas Olá preço completo dedicado VMs são expandidas quando necessário, tookeep uma quantidade mínima de trabalhos de saudação do capacidade tookeep disponíveis em andamento.</span><span class="sxs-lookup"><span data-stu-id="33a94-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="33a94-136">Suporte do Lote para VMs de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="33a94-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="33a94-137">Lote do Azure fornece vários recursos que o tornam fácil tooconsume e se beneficiar de VMs de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="33a94-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="33a94-138">Pools do Lote podem conter VMs dedicadas e VMs de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="33a94-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="33a94-139">número de saudação de cada tipo de VM pode ser especificado quando um pool é criado ou alterado a qualquer momento para um pool existente, usando a operação de redimensionamento explícita de saudação ou dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="33a94-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="33a94-140">Envio de trabalhos e tarefas pode permanecer inalterado e não precisa se preocupar com tipos VM Olá no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="33a94-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="33a94-141">Também é possível toohave um pool completamente usar baixa prioridade VMs toorun trabalhos barata possível, mas de aceleração dedicadas VMs se capacidade Olá cair abaixo do limite mínimo, para manter os trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="33a94-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="33a94-142">Pools de lote automaticamente buscam toohello número de destino de VMs de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="33a94-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="33a94-143">Se as VMs são capturadas, lote tentará Olá tooreplace perda a capacidade e o destino de retorno toohello.</span><span class="sxs-lookup"><span data-stu-id="33a94-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="33a94-144">No caso de saudação de tarefas que está sendo interrompida, lote detectará e automaticamente enfileiramento toobe tarefas execute novamente.</span><span class="sxs-lookup"><span data-stu-id="33a94-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="33a94-145">VMs de baixa prioridade têm uma cota de núcleos que difere das VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="33a94-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="33a94-146">Olá aspas para VMs de baixa prioridade é maior do que VMs dedicadas, porque as VMs de baixa prioridade menor custam.</span><span class="sxs-lookup"><span data-stu-id="33a94-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="33a94-147">Consulte [Limites e cotas do serviço de Lote](batch-quota-limit.md#resource-quotas) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="33a94-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="33a94-148">Máquinas virtuais de baixa prioridade atualmente não têm suporte para contas de lote em que o modo de alocação de pool hello está definido muito[assinatura de usuário](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="33a94-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="33a94-149">Criar e atualizar pools</span><span class="sxs-lookup"><span data-stu-id="33a94-149">Create and update pools</span></span>

<span data-ttu-id="33a94-150">Um pool de lote pode conter dedicados e de baixa prioridade máquinas virtuais (também chamados tooas nós de computação).</span><span class="sxs-lookup"><span data-stu-id="33a94-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="33a94-151">Você pode definir o número de destino de saudação de nós de computação para VMs dedicadas e de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="33a94-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="33a94-152">Olá, número de nós de destino Especifica Olá número de VMs que você deseja toohave no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="33a94-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="33a94-153">Por exemplo, toocreate um pool usando o serviço de nuvem do Azure VMs com um destino de 5 dedicado VMs e 20 VMs de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="33a94-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="33a94-154">toocreate um pool de máquinas virtuais do Azure (no caso VMs do Linux) com um destino de 5 dedicado VMs e 20 VMs de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="33a94-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="33a94-155">Você pode obter o número atual de saudação de nós para VMs dedicadas e de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="33a94-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="33a94-156">Nós de pool tem uma propriedade tooindicate se nó Olá é uma VM dedicada ou de baixa prioridade:</span><span class="sxs-lookup"><span data-stu-id="33a94-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="33a94-157">Quando um ou mais nós em um pool são capturadas, uma operação de lista de nós no pool ainda retornará os nós, Olá o número atual de nós de baixa prioridade permanece inalterado, mas esses nós terá seu estado definido toothe **admitiu preempção**estado.</span><span class="sxs-lookup"><span data-stu-id="33a94-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="33a94-158">Lote tentará toofind substituição VMs e, se for bem-sucedido, nós Olá passará por **criando** e **iniciando** estados antes de se tornar disponível para execução de tarefas, como novos nós.</span><span class="sxs-lookup"><span data-stu-id="33a94-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="33a94-159">Dimensionar um pool que contém VMs de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="33a94-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="33a94-160">Como ocorre com pools consiste exclusivamente em VMs dedicadas, é possível tooscale uma pool que contém baixa prioridade VMs chamando o método de redimensionamento hello, ou usando o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="33a94-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="33a94-161">operação de redimensionamento do pool Hello usa um parâmetro opcional segundo que atualiza o valor de **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="33a94-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="33a94-162">fórmula de dimensionamento automático do pool de saudação dá suporte a VMs de baixa prioridade da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="33a94-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="33a94-163">Você pode obter ou definir o valor de saudação da variável definida pelo serviço de saudação **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="33a94-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="33a94-164">Você pode obter o valor de saudação da variável definida pelo serviço de saudação **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="33a94-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="33a94-165">Você pode obter o valor de saudação da variável definida pelo serviço de saudação **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="33a94-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="33a94-166">Essa variável retorna o número de saudação de nós no hello preempção estado e permite que você expandir ou reduzir o número de saudação de nós dedicado, dependendo do número de saudação de admitiu preempção nós que não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="33a94-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="33a94-167">Trabalhos e tarefas</span><span class="sxs-lookup"><span data-stu-id="33a94-167">Jobs and tasks</span></span>

<span data-ttu-id="33a94-168">Trabalhos e tarefas exigem muito pouco suporte para nós de baixa prioridade. suporte apenas para Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="33a94-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="33a94-169">Olá JobManagerTask propriedade de um trabalho tem uma nova propriedade, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="33a94-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="33a94-170">Quando essa propriedade é true, a tarefa do Gerenciador de trabalho Olá pode ser agendada em um nó dedicado ou de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="33a94-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="33a94-171">Se essa propriedade for falsa, tarefa do Gerenciador de trabalho Olá será agendado tooa nó dedicado.</span><span class="sxs-lookup"><span data-stu-id="33a94-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="33a94-172">Um [variável de ambiente](batch-compute-node-environment-variables.md) é o aplicativo de tarefa tooa disponíveis para que ele possa determinar se ele está em execução em um nó de baixa prioridade ou dedicado.</span><span class="sxs-lookup"><span data-stu-id="33a94-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="33a94-173">variável de ambiente Olá é AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="33a94-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="33a94-174">Tratamento de preempções</span><span class="sxs-lookup"><span data-stu-id="33a94-174">Handling preemption</span></span>

<span data-ttu-id="33a94-175">Ocasionalmente, podem ser impedidas VMs; Quando isso acontece, o lote Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="33a94-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="33a94-176">VMs admitiu preempção Hello têm seu estado atualizado muito**admitiu preempção**.</span><span class="sxs-lookup"><span data-stu-id="33a94-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="33a94-177">Se estavam executando tarefas hello preempção VMs do nó, essas tarefas são retirada da fila e execute novamente.</span><span class="sxs-lookup"><span data-stu-id="33a94-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="33a94-178">Olá VM efetivamente é excluído, à esquerda tooany dados armazenados localmente no hello VM sejam perdido.</span><span class="sxs-lookup"><span data-stu-id="33a94-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="33a94-179">pool de saudação continuamente número de tentativas tooreach Olá destino de baixa prioridade nós disponíveis.</span><span class="sxs-lookup"><span data-stu-id="33a94-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="33a94-180">Quando a capacidade de substituição for encontrada, os nós manterão suas IDs, mas serão reinicializados, passando pelos estados **Criando** e **Inicial** antes que fiquem disponíveis para o agendamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="33a94-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="33a94-181">Contagens de preempção estão disponíveis como uma métrica de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="33a94-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="33a94-182">Métricas</span><span class="sxs-lookup"><span data-stu-id="33a94-182">Metrics</span></span>

<span data-ttu-id="33a94-183">Novas métricas estão disponíveis no hello [portal do Azure](https://portal.azure.com) para nós de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="33a94-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="33a94-184">Essas métricas são:</span><span class="sxs-lookup"><span data-stu-id="33a94-184">These metrics are:</span></span>

- <span data-ttu-id="33a94-185">Contagem de nós de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="33a94-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="33a94-186">Contagem de núcleos de baixa prioridade</span><span class="sxs-lookup"><span data-stu-id="33a94-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="33a94-187">Contagem de nós com preempção</span><span class="sxs-lookup"><span data-stu-id="33a94-187">Preempted Node Count</span></span>

<span data-ttu-id="33a94-188">métricas de tooview em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="33a94-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="33a94-189">Navegue tooyour conta de lote no portal de saudação e exibir configurações de saudação para sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="33a94-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="33a94-190">Selecione **métricas** de saudação **monitoramento** seção.</span><span class="sxs-lookup"><span data-stu-id="33a94-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="33a94-191">Selecione métricas Olá desejar Olá **métricas disponíveis** lista.</span><span class="sxs-lookup"><span data-stu-id="33a94-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Métricas para nós de baixa prioridade](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="33a94-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33a94-193">Next steps</span></span>

* <span data-ttu-id="33a94-194">Saudação de leitura [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md), informações essenciais para qualquer pessoa toouse lote de preparação.</span><span class="sxs-lookup"><span data-stu-id="33a94-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="33a94-195">artigo Olá contém informações mais detalhadas sobre os recursos de serviço de lote como pools, nós, trabalhos e tarefas e Olá muitos recursos da API que você pode usar ao criar seu aplicativo de lote.</span><span class="sxs-lookup"><span data-stu-id="33a94-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="33a94-196">Saiba mais sobre Olá [ferramentas e APIs de lote](batch-apis-tools.md) disponíveis para criar soluções de lote.</span><span class="sxs-lookup"><span data-stu-id="33a94-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
