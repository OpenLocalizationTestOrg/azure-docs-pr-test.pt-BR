---
title: "várias instâncias de aaaUse tarefas aplicativos de MPI toorun - lote do Azure | Microsoft Docs"
description: "Saiba como tipo de aplicativos de Interface MPI (Message Passing) tooexecute usando a tarefa de várias instâncias de saudação em lote do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="55df4-103">Usar várias instâncias tarefas toorun passando Interface aplicativos MPI (Message) em lote</span><span class="sxs-lookup"><span data-stu-id="55df4-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="55df4-104">Várias instâncias tarefas permitem que você toorun uma tarefa de lote do Azure em vários nós de computação simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="55df4-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="55df4-105">Essas tarefas permitem cenários de computação de alto desempenho, como aplicativos MPI (Interface de Transmissão de Mensagens) no Lote.</span><span class="sxs-lookup"><span data-stu-id="55df4-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="55df4-106">Neste artigo, você aprenderá como tarefas de várias instâncias de tooexecute usando Olá [Batch .NET] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="55df4-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="55df4-107">Enquanto os exemplos neste artigo Olá se concentrar no .NET de lote, MS-MPI, e nós de computação do Windows, conceitos de tarefa de várias instâncias de Olá discutidos aqui são aplicáveis tooother plataformas e tecnologias (Python e Intel MPI em nós do Linux, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="55df4-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="55df4-108">Visão geral da tarefa de várias instâncias</span><span class="sxs-lookup"><span data-stu-id="55df4-108">Multi-instance task overview</span></span>
<span data-ttu-id="55df4-109">Em lote, cada tarefa é normalmente executada em um único nó de computação – enviar o trabalho de tooa várias tarefas e Olá serviço de lote agenda cada tarefa para execução em um nó.</span><span class="sxs-lookup"><span data-stu-id="55df4-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="55df4-110">No entanto, ao configurar uma tarefa **configurações com várias instâncias**, informe o lote tooinstead criar uma tarefa principal e várias subtarefas que são executadas em vários nós.</span><span class="sxs-lookup"><span data-stu-id="55df4-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="55df4-111">![Visão geral da tarefa de várias instâncias][1]</span><span class="sxs-lookup"><span data-stu-id="55df4-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="55df4-112">Quando você enviar uma tarefa com o trabalho de tooa de configurações de várias instâncias, o lote executa várias tarefas de instância exclusiva de toomulti etapas:</span><span class="sxs-lookup"><span data-stu-id="55df4-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="55df4-113">Olá serviço de lote cria um **primário** e várias **subtarefas** com base nas configurações de várias instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="55df4-114">número total de saudação de tarefas (primários além de todas as subtarefas) corresponde o número de saudação do **instâncias** (nós de computação) você especificar nas configurações de várias instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="55df4-115">Lote designa uma saudação nós de computação como Olá **mestre**, e agendamentos Olá tooexecute tarefa primária no mestre de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="55df4-116">Ele agenda Olá subtarefas tooexecute no restante da saudação da tarefa de várias instâncias do toohello alocado de nós de computação hello, uma subtarefa por nó.</span><span class="sxs-lookup"><span data-stu-id="55df4-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="55df4-117">Olá primária e todas as subtarefas baixar qualquer **arquivos comuns do recurso** você especificar nas configurações de várias instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="55df4-118">Depois que os arquivos de recursos comuns Olá tiverem sido baixados, hello primário e subtarefas executar Olá **comando coordenação** você especificar nas configurações de várias instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="55df4-119">comando de coordenação de saudação é nós tooprepare geralmente usados para executar tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="55df4-120">Isso pode incluir serviços em segundo plano (como [Microsoft MPI][msmpi_msdn]do `smpd.exe`) e verificar se nós de saudação são mensagens do nó entre tooprocess pronto.</span><span class="sxs-lookup"><span data-stu-id="55df4-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="55df4-121">tarefa principal de saudação executa Olá **comando aplicativo** no nó mestre Olá *depois* Olá coordenação comando foi concluído com êxito pelo hello primária e todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="55df4-122">comando do aplicativo Hello Olá de linha de comando da tarefa de várias instâncias de saudação em si e é executado somente por tarefa principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="55df4-123">Em uma solução baseada em [MS-MPI][msmpi_msdn], é onde você executa seu aplicativo habilitado para MPI usando o `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="55df4-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="55df4-124">Embora seja funcionalmente distinto, Olá "tarefa de várias instâncias" não é um tipo de exclusiva da tarefa como Olá [StartTask] [ net_starttask] ou [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="55df4-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="55df4-125">Olá várias instâncias é simplesmente uma tarefa de lote padrão ([CloudTask] [ net_task] no lote .NET) cujas configurações de várias instâncias foram configuradas.</span><span class="sxs-lookup"><span data-stu-id="55df4-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="55df4-126">Neste artigo, nós nos referimos toothis como Olá **tarefas de várias instâncias**.</span><span class="sxs-lookup"><span data-stu-id="55df4-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="55df4-127">Requisitos para tarefas de várias instâncias</span><span class="sxs-lookup"><span data-stu-id="55df4-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="55df4-128">As tarefas de várias instâncias exigem um pool com **comunicação entre nós habilitada** e com a **execução de tarefas simultâneas desabilitada**.</span><span class="sxs-lookup"><span data-stu-id="55df4-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="55df4-129">execução de tarefas simultâneas toodisable, Olá conjunto [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 de propriedade.</span><span class="sxs-lookup"><span data-stu-id="55df4-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="55df4-130">Este trecho de código mostra como toocreate um pool para várias instâncias tarefas usando biblioteca de lote .NET hello.</span><span class="sxs-lookup"><span data-stu-id="55df4-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="55df4-131">Se você tentar toorun uma tarefa de várias instâncias em um pool com na comunicação desabilitada ou com um *maxTasksPerNode* valor maior que 1, tarefa Olá nunca foi programada – indefinidamente, ele permanecerá no estado "ativo" hello.</span><span class="sxs-lookup"><span data-stu-id="55df4-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="55df4-132">As tarefas de várias instâncias poderão ser executadas somente em nós nos pools criados após 14 de dezembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="55df4-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="55df4-133">Use um tooinstall StartTask MPI</span><span class="sxs-lookup"><span data-stu-id="55df4-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="55df4-134">aplicativos de MPI toorun com uma tarefa de várias instâncias, você primeiro precisa tooinstall uma implementação de MPI (MS-MPI ou MPI Intel, por exemplo) em nós de computação Olá no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="55df4-135">Este é um bom momento toouse um [StartTask][net_starttask], que é executado sempre que um nó une um pool ou reiniciado.</span><span class="sxs-lookup"><span data-stu-id="55df4-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="55df4-136">Este trecho de código cria um StartTask que especifica o pacote de instalação Olá MS-MPI como um [arquivo de recurso][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="55df4-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="55df4-137">linha de comando da tarefa de saudação inicial é executada após o arquivo de recurso Olá nó toohello baixado.</span><span class="sxs-lookup"><span data-stu-id="55df4-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="55df4-138">Nesse caso, a linha de comando de saudação realiza uma instalação autônoma do MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="55df4-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="55df4-139">Acesso remoto direto à memória (RDMA)</span><span class="sxs-lookup"><span data-stu-id="55df4-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="55df4-140">Quando você escolhe um [tamanho compatíveis com RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como A9 para Olá nós de computação no pool de lote, seu aplicativo MPI pode tirar proveito da rede de acesso (RDMA) de alto desempenho e baixa latência memória direta remota do Azure.</span><span class="sxs-lookup"><span data-stu-id="55df4-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="55df4-141">Procure os tamanhos de saudação especificados como "Compatíveis com RDMA" no hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="55df4-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="55df4-142">Pools **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="55df4-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="55df4-143">[Tamanhos de serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md) (somente Windows)</span><span class="sxs-lookup"><span data-stu-id="55df4-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="55df4-144">Pools de **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="55df4-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="55df4-145">[Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="55df4-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="55df4-146">[Tamanhos das máquinas virtuais no Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="55df4-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="55df4-147">tootake vantagem de RDMA em [nós de computação Linux](batch-linux-nodes.md), você deve usar **Intel MPI** em nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="55df4-148">Para obter mais informações sobre pools de CloudServiceConfiguration e VirtualMachineConfiguration, consulte Olá Olá seção Pool [visão geral do recurso de lote](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="55df4-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="55df4-149">Criar uma tarefa de várias instâncias com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="55df4-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="55df4-150">Agora que falamos sobre requisitos de pool hello e instalação do pacote MPI, vamos criar tarefa de várias instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="55df4-151">Neste trecho de código, criamos uma [CloudTask][net_task] padrão e configuramos sua propriedade [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="55df4-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="55df4-152">Como mencionado anteriormente, tarefas de várias instâncias de saudação não é um tipo distinto de tarefas, mas uma tarefa de lote padrão configurado com configurações de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="55df4-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="55df4-153">Tarefa principal e subtarefas</span><span class="sxs-lookup"><span data-stu-id="55df4-153">Primary task and subtasks</span></span>
<span data-ttu-id="55df4-154">Quando você cria Olá configurações com várias instâncias de uma tarefa, você especifica o número de saudação de nós de computação que são tarefas de saudação tooexecute.</span><span class="sxs-lookup"><span data-stu-id="55df4-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="55df4-155">Ao enviar trabalho tooa hello, Olá serviço de lote cria um **primário** tarefa e suficiente **subtarefas** que corresponde o número de saudação de nós especificados juntos.</span><span class="sxs-lookup"><span data-stu-id="55df4-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="55df4-156">Essas tarefas são atribuídas a uma id de inteiro no intervalo 0 Olá muito*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="55df4-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="55df4-157">Olá tarefa com id 0 é Olá primário e todos os outros ids são subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="55df4-158">Por exemplo, se você criar hello configurações com várias instâncias de uma tarefa a seguir, tarefa primária Olá teria uma id 0 e subtarefas Olá teria ids de 1 a 9.</span><span class="sxs-lookup"><span data-stu-id="55df4-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="55df4-159">Nó mestre</span><span class="sxs-lookup"><span data-stu-id="55df4-159">Master node</span></span>
<span data-ttu-id="55df4-160">Quando você envia uma tarefa de várias instâncias, Olá serviço de lote designa uma saudação nós de computação como nó de "mestre" hello e agendas Olá tooexecute tarefa primária no nó mestre hello.</span><span class="sxs-lookup"><span data-stu-id="55df4-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="55df4-161">Olá subtarefas são agendada tooexecute no restante Olá Olá nós alocada toohello tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="55df4-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="55df4-162">comando de coordenação</span><span class="sxs-lookup"><span data-stu-id="55df4-162">Coordination command</span></span>
<span data-ttu-id="55df4-163">Olá **comando coordenação** é executado pelo Olá primário e subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="55df4-164">bloqueio de invocação de saudação do comando de coordenação hello – lote não executar comando de saudação do aplicativo até que o comando de coordenação de saudação retornou com êxito para todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="55df4-165">comando de coordenação Hello, portanto, deve iniciar todos os serviços necessários em segundo plano, verifique que estão prontos para uso e saia.</span><span class="sxs-lookup"><span data-stu-id="55df4-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="55df4-166">Por exemplo, este comando coordenação para uma solução usando o MS-MPI versão 7 inicia o serviço SMPD de saudação no nó hello e será encerrado:</span><span class="sxs-lookup"><span data-stu-id="55df4-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="55df4-167">Observe o uso de saudação do `start` nesse comando de coordenação.</span><span class="sxs-lookup"><span data-stu-id="55df4-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="55df4-168">Isso é necessário porque Olá `smpd.exe` aplicativo não retorna imediatamente após a execução.</span><span class="sxs-lookup"><span data-stu-id="55df4-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="55df4-169">Sem o uso de saudação de saudação [iniciar] [ cmd_start] de comando, esse comando de coordenação não retornaria e, portanto, seria bloqueada Olá aplicativo execução do comando.</span><span class="sxs-lookup"><span data-stu-id="55df4-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="55df4-170">Comando de aplicativo</span><span class="sxs-lookup"><span data-stu-id="55df4-170">Application command</span></span>
<span data-ttu-id="55df4-171">Quando Olá primário e todos os subtarefas terminarem de executar o comando de coordenação de saudação, linha de comando da tarefa de várias instâncias de saudação é executada pela tarefa primária Olá *somente*.</span><span class="sxs-lookup"><span data-stu-id="55df4-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="55df4-172">Chamamos essa Olá **comando aplicativo** toodistinguish do comando de coordenação de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="55df4-173">Para aplicativos do MS-MPI, use Olá aplicativo comando tooexecute seu aplicativo habilitado para MPI com `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="55df4-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="55df4-174">Por exemplo, eis um comando do aplicativo para uma solução usando o MS-MPI versão 7:</span><span class="sxs-lookup"><span data-stu-id="55df4-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="55df4-175">Como MS-MPI `mpiexec.exe` usa Olá `CCP_NODES` variável por padrão (consulte [variáveis de ambiente](#environment-variables)) exemplo hello acima da linha de comando de aplicativo exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="55df4-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="55df4-176">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="55df4-176">Environment variables</span></span>
<span data-ttu-id="55df4-177">Lote cria várias [variáveis de ambiente] [ msdn_env_var] tarefas específicas da instância de toomulti Olá nós alocada tooa tarefa de várias instâncias de computação.</span><span class="sxs-lookup"><span data-stu-id="55df4-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="55df4-178">As linhas de comando coordenação e o aplicativo pode fazer referência a essas variáveis de ambiente, que pode Olá scripts e programas que foram executadas.</span><span class="sxs-lookup"><span data-stu-id="55df4-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="55df4-179">Olá seguintes variáveis de ambiente são criados pelo serviço de lote Olá para uso pelas tarefas de várias instâncias:</span><span class="sxs-lookup"><span data-stu-id="55df4-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="55df4-180">Para obter detalhes completos sobre eles e hello outras variáveis de ambiente de nó da computação de lote, incluindo o conteúdo e a visibilidade, consulte [variáveis de ambiente do nó de computação][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="55df4-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="55df4-181">exemplo de código do lote Linux MPI Olá contém um exemplo de como vários dessas variáveis de ambiente podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="55df4-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="55df4-182">Olá [coordenação cmd] [ coord_cmd_example] Bash script faz o download de aplicativos comuns e arquivos de entrada do armazenamento do Azure, permite que um compartilhamento de sistema de arquivos de rede (NFS) no nó mestre hello e configura Olá outros nós alocada a tarefa de várias instâncias de toohello como clientes NFS.</span><span class="sxs-lookup"><span data-stu-id="55df4-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="55df4-183">Arquivos de recurso</span><span class="sxs-lookup"><span data-stu-id="55df4-183">Resource files</span></span>
<span data-ttu-id="55df4-184">Há dois conjuntos de tooconsider de arquivos de recursos para tarefas de várias instâncias: **arquivos comuns do recurso** que *todos os* tarefas baixar (principal e subtarefas) e hello **arquivosderecurso** especificado para hello várias instâncias de tarefas em si, que *somente Olá primário* downloads de tarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="55df4-185">Você pode especificar um ou mais **arquivos comuns do recurso** nas configurações de várias instâncias de saudação para uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="55df4-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="55df4-186">Esses arquivos de recursos comuns são baixados de [armazenamento do Azure](../storage/common/storage-introduction.md) em cada nó **diretório compartilhado de tarefa** Olá primária e todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="55df4-187">Você pode acessar o diretório compartilhado de tarefa de saudação do aplicativo e a coordenação de linhas de comando usando Olá `AZ_BATCH_TASK_SHARED_DIR` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="55df4-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="55df4-188">Olá `AZ_BATCH_TASK_SHARED_DIR` caminho é idêntico em todas as tarefas de várias instâncias do nó toohello alocado, assim, você pode compartilhar um comando único coordenação entre hello primária e todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="55df4-189">Lote não "compartilhar" hello diretório em um sentido de acesso remoto, mas você pode usá-lo como uma montagem ou compartilhar um ponto, conforme mencionado anteriormente na ponta de saudação em variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="55df4-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="55df4-190">Arquivos de recursos que você especificar para a própria tarefa de várias instâncias hello são diretório de trabalho da tarefa toohello baixado, `AZ_BATCH_TASK_WORKING_DIR`, por padrão.</span><span class="sxs-lookup"><span data-stu-id="55df4-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="55df4-191">Conforme mencionado, por outro lado toocommon arquivos de recursos, somente tarefa principal de saudação baixa arquivos de recurso especificados para tarefa de várias instâncias de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="55df4-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55df4-192">Sempre use variáveis de ambiente Olá `AZ_BATCH_TASK_SHARED_DIR` e `AZ_BATCH_TASK_WORKING_DIR` toorefer diretórios toothese as linhas de comando.</span><span class="sxs-lookup"><span data-stu-id="55df4-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="55df4-193">Não tente caminhos de saudação tooconstruct manualmente.</span><span class="sxs-lookup"><span data-stu-id="55df4-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="55df4-194">Tempo de vida da tarefa</span><span class="sxs-lookup"><span data-stu-id="55df4-194">Task lifetime</span></span>
<span data-ttu-id="55df4-195">tempo de vida de saudação do tempo de vida do hello tarefa primária controles Olá da tarefa de toda a multi-instância Olá.</span><span class="sxs-lookup"><span data-stu-id="55df4-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="55df4-196">Quando Olá primário for encerrada, todas as subtarefas Olá são encerradas.</span><span class="sxs-lookup"><span data-stu-id="55df4-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="55df4-197">código de saída de saudação do hello primário é Olá código de saída da tarefa de saudação e é, portanto, toodetermine usado Olá êxito ou falha da tarefa Olá para fins de repetição.</span><span class="sxs-lookup"><span data-stu-id="55df4-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="55df4-198">Se qualquer Olá subtarefas falhar, sair com um código de retorno diferente de zero, por exemplo, Olá toda multi-instância de tarefa falhará.</span><span class="sxs-lookup"><span data-stu-id="55df4-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="55df4-199">tarefa de várias instâncias de saudação é encerrada e repetida, o limite de tentativas de tooits.</span><span class="sxs-lookup"><span data-stu-id="55df4-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="55df4-200">Quando você exclui uma tarefa de várias instâncias, hello primária e todas as subtarefas também são excluídas pelo serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="55df4-201">Todos os diretórios de subtarefa e seus arquivos são excluídos de nós de computação hello, como uma tarefa padrão.</span><span class="sxs-lookup"><span data-stu-id="55df4-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="55df4-202">[TaskConstraints] [ net_taskconstraints] para uma tarefa de várias instâncias, como Olá [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], e [RetentionTime] [ net_taskconstraint_retention] propriedades, são respeitadas conforme elas são para uma tarefa padrão e aplicam toohello primário e todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="55df4-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="55df4-203">No entanto, se você alterar Olá [RetentionTime] [ net_taskconstraint_retention] propriedade depois de adicionar Olá várias instâncias toohello trabalho, essa alteração é aplicada toohello somente principal tarefa.</span><span class="sxs-lookup"><span data-stu-id="55df4-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="55df4-204">Todas as subtarefas Olá continuam toouse Olá original [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="55df4-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="55df4-205">Lista de tarefas recentes de um nó de computação reflete id Olá uma subtarefa se tarefa recente Olá fizer parte de uma tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="55df4-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="55df4-206">Obtenha informações sobre subtarefas</span><span class="sxs-lookup"><span data-stu-id="55df4-206">Obtain information about subtasks</span></span>
<span data-ttu-id="55df4-207">informações de tooobtain subtarefas usando biblioteca de lote .NET hello, chamada hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] método.</span><span class="sxs-lookup"><span data-stu-id="55df4-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="55df4-208">Esse método retorna informações sobre todas as subtarefas e informações sobre Olá computação nó Olá tarefas executadas.</span><span class="sxs-lookup"><span data-stu-id="55df4-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="55df4-209">Essas informações, você pode determinar o diretório raiz de cada da subtarefa, id do pool hello, seu estado atual, código de saída e muito mais.</span><span class="sxs-lookup"><span data-stu-id="55df4-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="55df4-210">Você pode usar essas informações em combinação com hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] arquivos da subtarefa do método tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="55df4-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="55df4-211">Observe que esse método não retorna informações de tarefa principal de saudação (id 0).</span><span class="sxs-lookup"><span data-stu-id="55df4-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="55df4-212">A menos que indicado o contrário, os métodos do .NET em lotes que operam em Olá várias instâncias [CloudTask] [ net_task] se aplicar *somente* toohello principal tarefa.</span><span class="sxs-lookup"><span data-stu-id="55df4-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="55df4-213">Por exemplo, quando você chama Olá [CloudTask.ListNodeFiles] [ net_task_listnodefiles] método em uma tarefa de várias instâncias, somente os arquivos da tarefa primária Olá são retornados.</span><span class="sxs-lookup"><span data-stu-id="55df4-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="55df4-214">Olá trecho de código a seguir mostra como tooobtain subtarefa informações, bem como solicitar o conteúdo do arquivo de nós Olá na qual eles executado.</span><span class="sxs-lookup"><span data-stu-id="55df4-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="55df4-215">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="55df4-215">Code sample</span></span>
<span data-ttu-id="55df4-216">Olá [MultiInstanceTasks] [ github_mpi] exemplo de código no GitHub demonstra como toouse uma instância de várias tarefas toorun um [MS-MPI] [ msmpi_msdn] aplicativo em nós de computação do lote.</span><span class="sxs-lookup"><span data-stu-id="55df4-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="55df4-217">Siga as etapas de saudação em [preparação](#preparation) e [execução](#execution) exemplo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="55df4-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="55df4-218">Preparação</span><span class="sxs-lookup"><span data-stu-id="55df4-218">Preparation</span></span>
1. <span data-ttu-id="55df4-219">Execute as duas primeiras etapas Olá no [como toocompile e executar um programa simple do MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="55df4-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="55df4-220">Isso atende etapa prerequesites Olá para Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="55df4-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="55df4-221">Criar um *versão* versão do hello [MPIHelloWorld] [ helloworld_proj] programa MPI de exemplo.</span><span class="sxs-lookup"><span data-stu-id="55df4-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="55df4-222">Este é o programa de saudação que será executado em nós de computação pela tarefa de várias instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="55df4-223">Criar um arquivo zip contendo `MPIHelloWorld.exe` (compilado na etapa 2) e `MSMpiSetup.exe` (baixado na etapa 1).</span><span class="sxs-lookup"><span data-stu-id="55df4-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="55df4-224">Você carregará o arquivo zip como um pacote de aplicativo na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="55df4-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="55df4-225">Saudação de uso [portal do Azure] [ portal] toocreate um lote [aplicativo](batch-application-packages.md) chamado "MPIHelloWorld" e especifique o arquivo zip de saudação criado na etapa anterior hello como "1.0" da versão do pacote de aplicativo Hello.</span><span class="sxs-lookup"><span data-stu-id="55df4-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="55df4-226">Veja [Carregar e gerenciar aplicativos](batch-application-packages.md#upload-and-manage-applications) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="55df4-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="55df4-227">Criar um *versão* versão do `MPIHelloWorld.exe` para que você não tenha tooinclude dependências adicionais (por exemplo, `msvcp140d.dll` ou `vcruntime140d.dll`) em seu pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55df4-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="55df4-228">Execução</span><span class="sxs-lookup"><span data-stu-id="55df4-228">Execution</span></span>
1. <span data-ttu-id="55df4-229">Baixar Olá [exemplos de lote do azure] [ github_samples_zip] do GitHub.</span><span class="sxs-lookup"><span data-stu-id="55df4-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="55df4-230">Abra Olá MultiInstanceTasks **solução** no Visual Studio 2015 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="55df4-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="55df4-231">Olá `MultiInstanceTasks.sln` arquivo de solução está localizado em:</span><span class="sxs-lookup"><span data-stu-id="55df4-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="55df4-232">Insira suas credenciais de conta de lote e armazenamento em `AccountSettings.settings` em Olá **Microsoft.Azure.Batch.Samples.Common** projeto.</span><span class="sxs-lookup"><span data-stu-id="55df4-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="55df4-233">**Compilar e executar** Olá MultiInstanceTasks solução tooexecute Olá exemplo aplicativo MPI em nós de computação em um pool de lote.</span><span class="sxs-lookup"><span data-stu-id="55df4-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="55df4-234">*Opcional*: Olá Use [portal do Azure] [ portal] ou hello [Explorer lote] [ batch_explorer] tooexamine pool de exemplo hello, trabalho, e tarefa ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") antes de excluir os recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="55df4-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="55df4-235">Você pode baixar o [Visual Studio Community][visual_studio] gratuitamente se não tiver o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55df4-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="55df4-236">Saída de `MultiInstanceTasks.exe` é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="55df4-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="55df4-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55df4-237">Next steps</span></span>
* <span data-ttu-id="55df4-238">blog da equipe de lote do Azure e Microsoft HPC Olá discute [MPI suporte para Linux em lote do Azure][blog_mpi_linux]e inclui informações sobre como usar [OpenFOAM] [ openfoam] com o lote.</span><span class="sxs-lookup"><span data-stu-id="55df4-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="55df4-239">Você pode encontrar exemplos de código do Python para Olá [OpenFOAM exemplo no GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="55df4-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="55df4-240">Saiba como muito[criar pools de nós de computação Linux](batch-linux-nodes.md) para uso em suas soluções MPI de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="55df4-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Visão geral de várias instâncias"
