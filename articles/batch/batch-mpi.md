---
title: "Usar tarefas de várias instâncias para executar aplicativos MPI - Azure Batch | Microsoft Docs"
description: "Saiba como executar aplicativos de MPI (interface de transmissão de mensagens) usando o tipo de tarefa de várias instâncias no Lote do Azure."
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
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="599f6-103">Usar tarefas de várias instâncias para executar aplicativos de MPI (Interface de transmissão de mensagens) no Lote</span><span class="sxs-lookup"><span data-stu-id="599f6-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="599f6-104">As tarefas de várias instâncias permitem que você execute uma tarefa do Lote do Azure em vários nós de computação simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="599f6-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="599f6-105">Essas tarefas permitem cenários de computação de alto desempenho, como aplicativos MPI (Interface de Transmissão de Mensagens) no Lote.</span><span class="sxs-lookup"><span data-stu-id="599f6-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="599f6-106">Neste artigo, você aprende a executar tarefas de várias instâncias usando a biblioteca [.NET do Lote][api_net].</span><span class="sxs-lookup"><span data-stu-id="599f6-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="599f6-107">Embora os exemplos neste artigo se concentrem no Lote do .NET, MS-MPI e nós de computação do Windows, os conceitos de tarefa de várias instâncias discutidos aqui são aplicáveis a outras plataformas e tecnologias (por exemplo, Python e Intel MPI em nós Linux).</span><span class="sxs-lookup"><span data-stu-id="599f6-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="599f6-108">Visão geral da tarefa de várias instâncias</span><span class="sxs-lookup"><span data-stu-id="599f6-108">Multi-instance task overview</span></span>
<span data-ttu-id="599f6-109">No Lote, cada tarefa normalmente é executada em um nó de computação único: você envia várias tarefas para um trabalho e o serviço do Lote agenda cada tarefa para execução em um nó.</span><span class="sxs-lookup"><span data-stu-id="599f6-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="599f6-110">No entanto, ao definir as **configurações de várias instâncias** da tarefa, você dirá ao Lote para criar uma tarefa primário e várias subtarefas que estejam sendo executadas em vários nós.</span><span class="sxs-lookup"><span data-stu-id="599f6-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="599f6-111">![Visão geral da tarefa de várias instâncias][1]</span><span class="sxs-lookup"><span data-stu-id="599f6-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="599f6-112">Quando você envia uma tarefa com as configurações de várias instâncias para um trabalho, o Lote executa várias etapas exclusivas para tarefas de várias instâncias:</span><span class="sxs-lookup"><span data-stu-id="599f6-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="599f6-113">O serviço Lote cria um **primário** e várias **subtarefas** com base nas configurações de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="599f6-114">O número total de tarefas (as principais e todas as subtarefas) corresponde ao número de **instâncias** (nós de computação) que você especificar nas configurações de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="599f6-115">O Lote designa um de nós de computação como o **mestre** e agenda para ocorrer nele a execução a tarefa principal.</span><span class="sxs-lookup"><span data-stu-id="599f6-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="599f6-116">Ele agenda a execução das subtarefas para ocorrer no restante dos nós de computação alocados para a tarefa de várias instâncias, uma subtarefa por nó.</span><span class="sxs-lookup"><span data-stu-id="599f6-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="599f6-117">As tarefas principais e todas as subtarefas baixam os **arquivos de recurso comum** que você especificar nas configurações de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="599f6-118">Depois que os arquivos de recursos comuns tiverem sido baixados, a tarefa principal e as subtarefas executarão o **comando de coordenação** especificado nas configurações de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="599f6-119">O comando de coordenação normalmente é usado para preparar nós para executar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="599f6-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="599f6-120">Isso pode incluir a inicialização de serviços em segundo plano (como o `smpd.exe` do [Microsoft MPI][msmpi_msdn]) e verificar se os nós estão prontos para processar mensagens entre nós.</span><span class="sxs-lookup"><span data-stu-id="599f6-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="599f6-121">A tarefa principal executará o **comando de aplicativo** no nó mestre *após* o comando de coordenação ter sido concluído com êxito pela tarefa principal e por todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="599f6-122">O comando do aplicativo é a linha de comando da tarefa de várias instâncias em si, que é executada somente pela tarefa principal.</span><span class="sxs-lookup"><span data-stu-id="599f6-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="599f6-123">Em uma solução baseada em [MS-MPI][msmpi_msdn], é onde você executa seu aplicativo habilitado para MPI usando o `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="599f6-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="599f6-124">Embora seja funcionalmente distinto, “tarefa de várias instâncias" não é um tipo de tarefa exclusivo, como [StartTask][net_starttask] ou [JobPreparationTask][net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="599f6-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="599f6-125">A tarefa de várias instâncias é simplesmente uma tarefa do Lote Standard ([CloudTask][net_task] no .NET do Lote) cujas configurações de várias instâncias foram configuradas.</span><span class="sxs-lookup"><span data-stu-id="599f6-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="599f6-126">Neste artigo, nos referimos a isso como a **tarefa de várias instâncias**.</span><span class="sxs-lookup"><span data-stu-id="599f6-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="599f6-127">Requisitos para tarefas de várias instâncias</span><span class="sxs-lookup"><span data-stu-id="599f6-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="599f6-128">As tarefas de várias instâncias exigem um pool com **comunicação entre nós habilitada** e com a **execução de tarefas simultâneas desabilitada**.</span><span class="sxs-lookup"><span data-stu-id="599f6-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="599f6-129">Para desabilitar a execução de tarefas simultâneas, defina a propriedade [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) para 1.</span><span class="sxs-lookup"><span data-stu-id="599f6-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="599f6-130">Este trecho de código mostra como criar um pool para tarefas de várias instâncias usando a biblioteca do Lote para .NET.</span><span class="sxs-lookup"><span data-stu-id="599f6-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

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
> <span data-ttu-id="599f6-131">Se você tentar executar uma tarefa de várias instâncias em um pool com a comunicação entre nós desabilitada, ou com um valor *maxTasksPerNode* maior que 1, a tarefa nunca será agendada; ela permanecerá indefinidamente no estado "ativo".</span><span class="sxs-lookup"><span data-stu-id="599f6-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="599f6-132">As tarefas de várias instâncias poderão ser executadas somente em nós nos pools criados após 14 de dezembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="599f6-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="599f6-133">Usar uma StartTask para instalar MPI</span><span class="sxs-lookup"><span data-stu-id="599f6-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="599f6-134">Para executar aplicativos MPI com uma tarefa de várias instâncias, primeiro você precisa instalar uma implementação MPI (MS-MPI ou Intel MPI, por exemplo) em nós de computação no pool.</span><span class="sxs-lookup"><span data-stu-id="599f6-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="599f6-135">Esse é um bom momento para usar uma [StartTask][net_starttask], que é executada sempre que um nó ingressa em um pool ou é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="599f6-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="599f6-136">Esse trecho de código cria uma StartTask que especifica o pacote de instalação do MS-MPI como um [arquivo de recurso][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="599f6-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="599f6-137">A linha de comando da tarefa inicial é executada depois de baixar o arquivo de recurso para o nó.</span><span class="sxs-lookup"><span data-stu-id="599f6-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="599f6-138">Nesse caso, a linha de comando executa uma instalação autônoma do MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="599f6-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="599f6-139">Acesso remoto direto à memória (RDMA)</span><span class="sxs-lookup"><span data-stu-id="599f6-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="599f6-140">Quando você escolher um [tamanho compatível com RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) , como o A9 para os nós de computação em seu pool do Lote, o aplicativo MPI poderá tirar proveito da rede RDMA (acesso remoto direto à memória) de alto desempenho e baixa latência do Azure.</span><span class="sxs-lookup"><span data-stu-id="599f6-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="599f6-141">Procure os tamanhos especificados como "Compatível com RDMA" nos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="599f6-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="599f6-142">Pools **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="599f6-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="599f6-143">[Tamanhos de serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md) (somente Windows)</span><span class="sxs-lookup"><span data-stu-id="599f6-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="599f6-144">Pools de **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="599f6-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="599f6-145">[Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="599f6-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="599f6-146">[Tamanhos das máquinas virtuais no Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="599f6-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="599f6-147">Para tirar proveito dos RDMA nos [nós de computação Linux](batch-linux-nodes.md), você deverá usar **Intel MPI** nos nós.</span><span class="sxs-lookup"><span data-stu-id="599f6-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="599f6-148">Para obter mais informações sobre os pools CloudServiceConfiguration e VirtualMachineConfiguration, consulte a seção Pool da [visão geral do recurso Lote](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="599f6-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="599f6-149">Criar uma tarefa de várias instâncias com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="599f6-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="599f6-150">Agora que já abordamos os requisitos de pool e a instalação do pacote MPI, vamos criar a tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="599f6-151">Neste trecho de código, criamos uma [CloudTask][net_task] padrão e configuramos sua propriedade [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="599f6-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="599f6-152">Conforme mencionado anteriormente, a tarefa de várias instâncias não é um tipo de tarefa distinto, mas uma tarefa do Lote Standard definida com configuração de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="599f6-153">Tarefa principal e subtarefas</span><span class="sxs-lookup"><span data-stu-id="599f6-153">Primary task and subtasks</span></span>
<span data-ttu-id="599f6-154">Quando você cria as configurações de várias instâncias de uma tarefa, pode especificar o número de nós de computação que devem executar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="599f6-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="599f6-155">Ao enviar a tarefa a um trabalho, o serviço de Lote cria uma tarefa **principal** **subtarefas** suficientes para corresponder ao número de nós que você especificou.</span><span class="sxs-lookup"><span data-stu-id="599f6-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="599f6-156">Essas tarefas são atribuídas a uma ID de número inteiro no intervalo de 0 a *numberOfInstances* – 1.</span><span class="sxs-lookup"><span data-stu-id="599f6-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="599f6-157">A tarefa com ID 0 é a tarefa principal e todas as outras IDs são subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="599f6-158">Por exemplo, se você criar as configurações de várias instâncias abaixo para uma tarefa, a tarefa principal terá uma id 0 e as subtarefas terão ids de 1 a 9.</span><span class="sxs-lookup"><span data-stu-id="599f6-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="599f6-159">Nó mestre</span><span class="sxs-lookup"><span data-stu-id="599f6-159">Master node</span></span>
<span data-ttu-id="599f6-160">Quando você envia uma tarefa de várias instâncias, o serviço de Lote designa um dos nós de computação como o "mestre" e agenda para ocorrer nele a execução a tarefa principal.</span><span class="sxs-lookup"><span data-stu-id="599f6-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="599f6-161">Ele agenda a execução das subtarefas para ocorrer no restante dos nós alocados para a tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="599f6-162">comando de coordenação</span><span class="sxs-lookup"><span data-stu-id="599f6-162">Coordination command</span></span>
<span data-ttu-id="599f6-163">O **comando de coordenação** é executado pela tarefa principal e subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="599f6-164">A invocação do comando de coordenação está bloqueando. O Lote não executa o comando do aplicativo até que o comando de coordenação retorne com êxito para todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="599f6-165">O comando de coordenação, portanto, deve iniciar todos os serviços em segundo plano necessários, verificar se eles estão prontos para uso e sair.</span><span class="sxs-lookup"><span data-stu-id="599f6-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="599f6-166">Por exemplo, este comando de coordenação para uma solução com a versão 7 do MS-MPI inicia o serviço SMPD no nó e sai:</span><span class="sxs-lookup"><span data-stu-id="599f6-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="599f6-167">Observe o uso de `start` neste comando de coordenação.</span><span class="sxs-lookup"><span data-stu-id="599f6-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="599f6-168">Isso é necessário porque o aplicativo `smpd.exe` não retorna imediatamente após a execução.</span><span class="sxs-lookup"><span data-stu-id="599f6-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="599f6-169">Sem usar o comando [start][cmd_start], esse comando de coordenação não retornaria e, portanto, bloquearia a execução do comando do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="599f6-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="599f6-170">Comando de aplicativo</span><span class="sxs-lookup"><span data-stu-id="599f6-170">Application command</span></span>
<span data-ttu-id="599f6-171">Depois que a tarefa principal e todas as subtarefas concluírem a execução do comando de coordenação, a linha de comando da tarefa de várias instâncias é executada *somente*pela tarefa principal.</span><span class="sxs-lookup"><span data-stu-id="599f6-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="599f6-172">Nós o chamamos de **comando de aplicativo** para distingui-lo do comando de coordenação.</span><span class="sxs-lookup"><span data-stu-id="599f6-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="599f6-173">Para os aplicativos MS-MPI, use o comando de aplicativo para executar o aplicativo habilitado para MPI com `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="599f6-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="599f6-174">Por exemplo, eis um comando do aplicativo para uma solução usando o MS-MPI versão 7:</span><span class="sxs-lookup"><span data-stu-id="599f6-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="599f6-175">Como o `mpiexec.exe` do MS-MPI usa a variável `CCP_NODES` por padrão (veja [Variáveis de ambiente](#environment-variables)), a linha de comando do aplicativo de exemplo acima a exclui.</span><span class="sxs-lookup"><span data-stu-id="599f6-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="599f6-176">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="599f6-176">Environment variables</span></span>
<span data-ttu-id="599f6-177">O Lote cria diversas [variáveis de ambiente][msdn_env_var] específicas a tarefas de várias instâncias nos nós de computação alocados a uma tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="599f6-178">Suas linhas de comando de coordenação e do aplicativo podem fazer referência a essas variáveis de ambiente, assim como podem fazê-lo os scripts e programas executados por elas.</span><span class="sxs-lookup"><span data-stu-id="599f6-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="599f6-179">As variáveis de ambiente a seguir são criadas pelo serviço de Lote para uso por tarefas de várias instâncias:</span><span class="sxs-lookup"><span data-stu-id="599f6-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="599f6-180">Para obter detalhes completos sobre essas e outras variáveis de ambiente do nó de computação do Lote, incluindo seu conteúdo e visibilidade, veja [Variáveis de ambiente do nó de computação][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="599f6-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="599f6-181">O exemplo de código MPI para Linux do Lote contém um exemplo de como várias dessas variáveis de ambiente podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="599f6-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="599f6-182">O script de Bash [coordination-cmd][coord_cmd_example] baixa arquivos de entrada e de aplicativos comuns do Armazenamento do Azure, habilita um compartilhamento de NFS (sistema de arquivos de rede) no nó mestre e configura os outros nós alocados para a tarefa de várias instâncias, como clientes NFS.</span><span class="sxs-lookup"><span data-stu-id="599f6-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="599f6-183">Arquivos de recurso</span><span class="sxs-lookup"><span data-stu-id="599f6-183">Resource files</span></span>
<span data-ttu-id="599f6-184">Há dois conjuntos de arquivos de recursos a serem considerados para tarefas de várias instâncias: **arquivos de recurso comuns** que *todas* as tarefas baixam (principal e subtarefas) e **arquivos de recurso** especificados para a própria tarefa de várias instâncias, que é baixado *somente pela tarefa principal*.</span><span class="sxs-lookup"><span data-stu-id="599f6-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="599f6-185">Você pode especificar um ou mais **arquivos de recurso comum** nas configurações de várias instâncias de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="599f6-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="599f6-186">Esses arquivos de recurso comum são baixados do [Armazenamento do Azure](../storage/common/storage-introduction.md) no **diretório compartilhado da tarefa** de cada nó pela tarefa principal e por todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="599f6-187">Você pode acessar o diretório compartilhado da tarefa das linhas de comando do aplicativo e de coordenação usando a variável de ambiente `AZ_BATCH_TASK_SHARED_DIR` .</span><span class="sxs-lookup"><span data-stu-id="599f6-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="599f6-188">O caminho `AZ_BATCH_TASK_SHARED_DIR` é idêntico em todos os nós alocados para a tarefa de várias instâncias, assim você pode compartilhar um único comando de coordenação entre a tarefa principal e todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="599f6-189">O Lote não "compartilha" o diretório no sentido de acesso remoto, mas você pode usá-lo como um ponto de montagem ou compartilhamento conforme mencionado anteriormente na dica sobre variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="599f6-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="599f6-190">Os arquivos de recursos que você especificar para a tarefa de várias instâncias em si serão baixados para o diretório de trabalho da tarefa, `AZ_BATCH_TASK_WORKING_DIR` por padrão.</span><span class="sxs-lookup"><span data-stu-id="599f6-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="599f6-191">Conforme mencionado, em contraste com arquivos de recursos comuns, apenas a tarefa principal baixa arquivos de recurso especificados para a tarefa de várias instâncias em si.</span><span class="sxs-lookup"><span data-stu-id="599f6-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="599f6-192">Sempre use as variáveis de ambiente `AZ_BATCH_TASK_SHARED_DIR` e `AZ_BATCH_TASK_WORKING_DIR` para fazer referência a esses diretórios em suas linhas de comando.</span><span class="sxs-lookup"><span data-stu-id="599f6-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="599f6-193">Não tente construir os caminhos manualmente.</span><span class="sxs-lookup"><span data-stu-id="599f6-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="599f6-194">Tempo de vida da tarefa</span><span class="sxs-lookup"><span data-stu-id="599f6-194">Task lifetime</span></span>
<span data-ttu-id="599f6-195">O tempo de vida da tarefa principal controla o tempo de vida de toda a tarefa com várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="599f6-196">Quando a tarefa principal é encerrada, todas as subtarefas são encerradas.</span><span class="sxs-lookup"><span data-stu-id="599f6-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="599f6-197">O código de saída da tarefa principal é o código de saída da tarefa e, portanto, é usado para determinar o êxito ou a falha da tarefa para fins de repetição.</span><span class="sxs-lookup"><span data-stu-id="599f6-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="599f6-198">Se qualquer uma das subtarefas falhar, sair com um código de retorno diferente de zero, por exemplo, toda a tarefa de várias instâncias falhará.</span><span class="sxs-lookup"><span data-stu-id="599f6-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="599f6-199">A tarefa de várias instâncias é encerrada e repetida até o limite de repetição.</span><span class="sxs-lookup"><span data-stu-id="599f6-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="599f6-200">Quando você exclui uma tarefa de várias instâncias, a tarefa principal e todas as subtarefas são também excluídas pelo serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="599f6-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="599f6-201">Todos os diretórios de subtarefa e seus arquivos serão excluídos dos nós de computação, como ocorre com uma tarefa padrão.</span><span class="sxs-lookup"><span data-stu-id="599f6-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="599f6-202">[TaskConstraints][net_taskconstraints] para uma tarefa de várias instâncias, como as propriedades [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock] e [RetentionTime][net_taskconstraint_retention], são respeitadas da mesma forma que são para uma tarefa padrão e se aplicam à tarefa principal e a todas as subtarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="599f6-203">No entanto, se você alterar a propriedade [RetentionTime][net_taskconstraint_retention] depois de adicionar a tarefa de várias instâncias ao trabalho, essa alteração será aplicada somente à tarefa principal.</span><span class="sxs-lookup"><span data-stu-id="599f6-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="599f6-204">Todas as subtarefas continuam usando o [RetentionTime][net_taskconstraint_retention] original.</span><span class="sxs-lookup"><span data-stu-id="599f6-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="599f6-205">A lista de tarefas recentes de um nó de computação reflete a id da subtarefa se a tarefa recente fizer parte de uma tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="599f6-206">Obtenha informações sobre subtarefas</span><span class="sxs-lookup"><span data-stu-id="599f6-206">Obtain information about subtasks</span></span>
<span data-ttu-id="599f6-207">Para obter informações sobre subtarefas usando a biblioteca .NET do Lote, chame o método [CloudTask.ListSubtasks][net_task_listsubtasks].</span><span class="sxs-lookup"><span data-stu-id="599f6-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="599f6-208">Esse método retorna informações sobre todas as subtarefas e sobre o nó de computação que executou as tarefas.</span><span class="sxs-lookup"><span data-stu-id="599f6-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="599f6-209">Com essas informações, você pode determinar o diretório raiz de cada subtarefa, a id do pool, seu estado atual, o código de saída e muito mais.</span><span class="sxs-lookup"><span data-stu-id="599f6-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="599f6-210">Você pode usar essas informações em conjunto com o método [PoolOperations.GetNodeFile][poolops_getnodefile] para obter os arquivos da subtarefa.</span><span class="sxs-lookup"><span data-stu-id="599f6-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="599f6-211">Observe que esse método não retorna informações sobre a tarefa principal (id 0).</span><span class="sxs-lookup"><span data-stu-id="599f6-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="599f6-212">Salvo indicação contrária, os métodos .NET do Lote que operam na própria [CloudTask][net_task] de várias instâncias se aplicam *somente* à tarefa principal.</span><span class="sxs-lookup"><span data-stu-id="599f6-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="599f6-213">Por exemplo, quando você chama o método [CloudTask.ListNodeFiles][net_task_listnodefiles] em uma tarefa de várias instâncias, somente os arquivos da tarefa principal são retornados.</span><span class="sxs-lookup"><span data-stu-id="599f6-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="599f6-214">O trecho de código a seguir mostra como obter as informações sobre subtarefas, bem como solicitar o conteúdo do arquivo dos nós em que elas são executadas.</span><span class="sxs-lookup"><span data-stu-id="599f6-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="599f6-215">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="599f6-215">Code sample</span></span>
<span data-ttu-id="599f6-216">O exemplo de código [MultiInstanceTasks][github_mpi] no GitHub demonstra como usar uma tarefa de várias instâncias para executar um aplicativo [MS-MPI][msmpi_msdn] nos nós de computação do Lote.</span><span class="sxs-lookup"><span data-stu-id="599f6-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="599f6-217">Siga as etapas em [Preparação](#preparation) e [Execução](#execution) para executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="599f6-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="599f6-218">Preparação</span><span class="sxs-lookup"><span data-stu-id="599f6-218">Preparation</span></span>
1. <span data-ttu-id="599f6-219">Siga as duas primeiras etapas em [Como compilar e executar um programa MS-MPI simples][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="599f6-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="599f6-220">Isso atende aos pré-requisitos da etapa seguinte.</span><span class="sxs-lookup"><span data-stu-id="599f6-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="599f6-221">Compile uma versão de *Lançamento* do programa MPI de exemplo [MPIHelloWorld][helloworld_proj].</span><span class="sxs-lookup"><span data-stu-id="599f6-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="599f6-222">Este é o programa que será executado em nós de computação pela tarefa de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="599f6-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="599f6-223">Criar um arquivo zip contendo `MPIHelloWorld.exe` (compilado na etapa 2) e `MSMpiSetup.exe` (baixado na etapa 1).</span><span class="sxs-lookup"><span data-stu-id="599f6-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="599f6-224">Você vai carregar esse arquivo zip como um pacote de aplicativos na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="599f6-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="599f6-225">Use o [portal do Azure][portal] para criar um [aplicativo](batch-application-packages.md) do Lote chamado "MPIHelloWorld" e especifique o arquivo zip que você criou na etapa anterior como a versão "1.0" do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="599f6-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="599f6-226">Veja [Carregar e gerenciar aplicativos](batch-application-packages.md#upload-and-manage-applications) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="599f6-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="599f6-227">Compile uma versão de *Lançamento* do `MPIHelloWorld.exe` para que você não tenha de incluir as dependências adicionais (por exemplo, `msvcp140d.dll` ou `vcruntime140d.dll`) em seu pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="599f6-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="599f6-228">Execução</span><span class="sxs-lookup"><span data-stu-id="599f6-228">Execution</span></span>
1. <span data-ttu-id="599f6-229">Baixe [azure-batch-samples][github_samples_zip] do GitHub.</span><span class="sxs-lookup"><span data-stu-id="599f6-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="599f6-230">Abra a **solução** MultiInstanceTasks no Visual Studio 2015 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="599f6-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="599f6-231">O arquivo de solução `MultiInstanceTasks.sln` está localizado em:</span><span class="sxs-lookup"><span data-stu-id="599f6-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="599f6-232">Insira suas credenciais de conta do Lote e do Armazenamento no `AccountSettings.settings` no projeto **Microsoft.Azure.Batch.Samples.Common**.</span><span class="sxs-lookup"><span data-stu-id="599f6-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="599f6-233">**Compile e execute** a solução MultiInstanceTasks para executar o aplicativo de exemplo MPI nos nós de computação em um pool do Lote.</span><span class="sxs-lookup"><span data-stu-id="599f6-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="599f6-234">*Opcional*: use o [portal do Azure][portal] ou o [Gerenciador do Lote][batch_explorer] para examinar o pool, o trabalho e a tarefa de exemplo ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") antes de excluir os recursos.</span><span class="sxs-lookup"><span data-stu-id="599f6-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="599f6-235">Você pode baixar o [Visual Studio Community][visual_studio] gratuitamente se não tiver o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="599f6-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="599f6-236">A saída de `MultiInstanceTasks.exe` deverá ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="599f6-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

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

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="599f6-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="599f6-237">Next steps</span></span>
* <span data-ttu-id="599f6-238">O blog da Equipe de HPC e do Lote do Azure da Microsoft discute o [suporte do MPI para Linux no Lote do Azure][blog_mpi_linux] e inclui informações sobre como usar o [OpenFOAM][openfoam] com o Lote.</span><span class="sxs-lookup"><span data-stu-id="599f6-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="599f6-239">Você pode encontrar exemplos de código do Python para o [exemplo do OpenFOAM no GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="599f6-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="599f6-240">Saiba como [criar pools de nós de computação Linux](batch-linux-nodes.md) para uso em suas soluções MPI do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="599f6-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
