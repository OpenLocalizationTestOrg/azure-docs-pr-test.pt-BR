---
title: "aaaPersist trabalhos e tarefas de saída tooAzure armazenamento com biblioteca de convenções de arquivo hello para .NET - lote do Azure | Microsoft Docs"
description: "Saiba como toouse biblioteca de convenções de arquivo de lote do Azure para .NET toopersist tarefa em lotes e tooAzure de saída do trabalho armazenamento e Olá exibição persistentes saída Olá portal do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="f4a46-103">Manter o trabalho e dados tooAzure armazenamento com biblioteca de convenções de arquivo em lotes Olá para .NET toopersist de tarefas</span><span class="sxs-lookup"><span data-stu-id="f4a46-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="f4a46-104">Dados de tarefa toopersist unidirecional são Olá toouse [biblioteca convenções de arquivo de lote do Azure para .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="f4a46-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="f4a46-105">Olá, biblioteca de convenções de arquivo simplifica o processo de saudação de armazenar a saída da tarefa dados tooAzure armazenamento e recuperá-los.</span><span class="sxs-lookup"><span data-stu-id="f4a46-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="f4a46-106">Você pode usar Olá convenções arquivo biblioteca em código de cliente e de tarefa &mdash; no código de tarefa para manter arquivos e no cliente de código toolist e recuperá-las.</span><span class="sxs-lookup"><span data-stu-id="f4a46-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="f4a46-107">O código de tarefa também pode usar Olá biblioteca tooretrieve Olá saída upstream tarefas, como em um [dependências entre tarefas](batch-task-dependencies.md) cenário.</span><span class="sxs-lookup"><span data-stu-id="f4a46-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="f4a46-108">tooretrieve saída arquivos com biblioteca de convenções de arquivo hello, você pode localizar arquivos de saudação para um determinado trabalho ou tarefa listá-los por ID e a finalidade.</span><span class="sxs-lookup"><span data-stu-id="f4a46-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="f4a46-109">Você não precisa tooknow nomes de saudação ou locais dos arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4a46-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="f4a46-110">Por exemplo, você pode usar toolist de biblioteca de convenções de arquivo hello todos os arquivos intermediários para uma determinada tarefa ou obter um arquivo de visualização para um determinado trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4a46-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="f4a46-111">Começando com a versão de 2017-05-01, Olá API do serviço de lote dá suporte a tooAzure de dados persistentes saída armazenamento para tarefas e tarefas do Gerenciador de trabalho que são executados em pools criados com a configuração de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4a46-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="f4a46-112">Olá API do serviço de lote fornece um toopersist de maneira simples de saída de dentro do código de saudação que cria uma tarefa e serve como uma biblioteca de convenções de arquivo toohello alternativo.</span><span class="sxs-lookup"><span data-stu-id="f4a46-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="f4a46-113">Você pode modificar a saída de toopersist de aplicativos de cliente de lote sem a necessidade de aplicativo hello tooupdate que a tarefa está em execução.</span><span class="sxs-lookup"><span data-stu-id="f4a46-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="f4a46-114">Para obter mais informações, consulte [persistir dados de tarefa tooAzure armazenamento com a API do serviço de lote de saudação](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="f4a46-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="f4a46-115">Quando usar o hello convenções arquivo biblioteca toopersist a saída da tarefa?</span><span class="sxs-lookup"><span data-stu-id="f4a46-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="f4a46-116">Lote do Azure fornece uma maneira toopersist a saída da tarefa.</span><span class="sxs-lookup"><span data-stu-id="f4a46-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="f4a46-117">Olá convenções de arquivo é melhor cenários de toothese adequados:</span><span class="sxs-lookup"><span data-stu-id="f4a46-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="f4a46-118">Você pode modificar facilmente o código Olá para o aplicativo hello se a tarefa está em execução toopersist arquivos usando biblioteca de convenções de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="f4a46-119">Você deseja toostream dados tooAzure armazenamento enquanto a tarefa Olá ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="f4a46-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="f4a46-120">Você deseja toopersist dados pools criados com a configuração do serviço de nuvem hello ou configuração de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4a46-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="f4a46-121">O aplicativo cliente ou outras tarefas no hello toolocate necessidades de trabalho e baixar arquivos de saída de tarefas por ID ou por finalidade.</span><span class="sxs-lookup"><span data-stu-id="f4a46-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="f4a46-122">Você deseja tooview saída da tarefa no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a46-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="f4a46-123">Se seu cenário diferente daqueles listados acima, talvez seja necessário tooconsider uma abordagem diferente.</span><span class="sxs-lookup"><span data-stu-id="f4a46-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="f4a46-124">Para obter mais informações sobre outras opções para persistir a saída da tarefa, consulte [Persist trabalhos e tarefas de saída tooAzure armazenamento](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="f4a46-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="f4a46-125">O que é Olá convenções do arquivo de lote padrão?</span><span class="sxs-lookup"><span data-stu-id="f4a46-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="f4a46-126">Olá [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornece um esquema de nomenclatura para contêineres de destino hello e toowhich de caminhos de blob, os arquivos de saída são gravados.</span><span class="sxs-lookup"><span data-stu-id="f4a46-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="f4a46-127">Arquivos persistente tooAzure armazenamento que seguem toohello convenções de arquivo padrão são automaticamente disponíveis para visualização no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a46-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="f4a46-128">portal de Hello está ciente de convenção de nomenclatura hello e portanto pode exibir arquivos que seguem tooit.</span><span class="sxs-lookup"><span data-stu-id="f4a46-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="f4a46-129">biblioteca de convenções de arquivo Hello para .NET nomeia automaticamente seus contêineres de armazenamento e arquivos de saída de tarefa de acordo com o toohello convenções de arquivo padrão.</span><span class="sxs-lookup"><span data-stu-id="f4a46-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="f4a46-130">biblioteca de convenções de arquivo Hello também fornece métodos tooquery arquivos de saída no armazenamento do Azure toojob ID, ID da tarefa ou finalidade de acordo com.</span><span class="sxs-lookup"><span data-stu-id="f4a46-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="f4a46-131">Se você estiver desenvolvendo com um idioma diferente do .NET, você pode implementar Olá convenções de arquivo padrão por conta própria em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4a46-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="f4a46-132">Para obter mais informações, consulte [sobre padrão de convenções de arquivo em lotes Olá](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="f4a46-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="f4a46-133">Vincular uma conta de armazenamento do Azure tooyour conta em lotes</span><span class="sxs-lookup"><span data-stu-id="f4a46-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="f4a46-134">dados de saída de toopersist tooAzure armazenamento usando a biblioteca de convenções de arquivo hello, primeiro você deve vincular uma conta de armazenamento do Azure tooyour conta do lote.</span><span class="sxs-lookup"><span data-stu-id="f4a46-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="f4a46-135">Se você ainda não tiver feito isso, vincular uma conta de armazenamento tooyour conta em lotes usando Olá [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="f4a46-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="f4a46-136">Navegue tooyour conta de lote no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a46-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="f4a46-137">Em **Configurações**, selecione **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="f4a46-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="f4a46-138">Se você ainda não tiver uma conta de Armazenamento associada à sua conta do Lote, clique em **Conta de Armazenamento (Nenhuma)**.</span><span class="sxs-lookup"><span data-stu-id="f4a46-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="f4a46-139">Selecione uma conta de armazenamento na lista Olá para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f4a46-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="f4a46-140">Para melhor desempenho, use uma conta de armazenamento do Azure que está em Olá mesma região Olá conta do lote onde as tarefas estão em execução.</span><span class="sxs-lookup"><span data-stu-id="f4a46-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="f4a46-141">Manter os dados de saída</span><span class="sxs-lookup"><span data-stu-id="f4a46-141">Persist output data</span></span>

<span data-ttu-id="f4a46-142">tarefa toopersist trabalho de saída de dados com a biblioteca de convenções de arquivo hello, criar um contêiner no armazenamento do Azure e salvar o contêiner de toohello Olá saída.</span><span class="sxs-lookup"><span data-stu-id="f4a46-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="f4a46-143">Saudação de uso [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) em seu contêiner de toohello tarefa código tooupload Olá tarefa saída.</span><span class="sxs-lookup"><span data-stu-id="f4a46-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="f4a46-144">Para obter mais informações sobre como trabalhar com contêineres e blobs no Armazenamento do Azure, consulte [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f4a46-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="f4a46-145">Todas as saídas de trabalho e tarefa persistentes Olá convenções de arquivo de biblioteca são armazenados no mesmo contêiner de hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="f4a46-146">Se um grande número de tarefas tente toopersist arquivos no hello mesmo tempo, [redução dos limites de armazenamento](../storage/common/storage-performance-checklist.md#blobs) pode ser imposta.</span><span class="sxs-lookup"><span data-stu-id="f4a46-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="f4a46-147">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f4a46-147">Create storage container</span></span>

<span data-ttu-id="f4a46-148">tooAzure de saída de tarefa toopersist armazenamento, primeiro crie um contêiner chamando [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="f4a46-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="f4a46-149">Esse método de extensão usa um objeto [CloudStorageAccount][net_cloudstorageaccount] como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f4a46-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="f4a46-150">Ele cria um contêiner nomeado acordo toohello convenções de arquivo padrão, para que seu conteúdo é detectável pelo Olá métodos de recuperação de portal e hello Azure discutidos posteriormente no artigo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4a46-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="f4a46-151">Você normalmente colocar Olá código toocreate um contêiner em seu aplicativo cliente &mdash; Olá aplicativo que cria o pools, trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="f4a46-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="f4a46-152">Armazenar saídas de tarefas</span><span class="sxs-lookup"><span data-stu-id="f4a46-152">Store task outputs</span></span>

<span data-ttu-id="f4a46-153">Agora que você preparou um contêiner no armazenamento do Azure, tarefas podem salvar o contêiner de toohello de saída usando Olá [TaskOutputStorage] [ net_taskoutputstorage] classe encontrada na biblioteca de convenções de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="f4a46-154">Em seu código de tarefa, primeiro crie um [TaskOutputStorage] [ net_taskoutputstorage] do objeto, em seguida, quando a tarefa de saudação concluiu seu trabalho, chame Olá [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] método toosave tooAzure sua saída armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4a46-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="f4a46-155">Olá `kind` parâmetro hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) método categoriza Olá persistente de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f4a46-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="f4a46-156">Há quatro tipos predefinidos de [TaskOutputKind][net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog` e `TaskIntermediate.`. Você também pode definir as categorias personalizadas da saída.</span><span class="sxs-lookup"><span data-stu-id="f4a46-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="f4a46-157">Esses tipos de saída permitem que você toospecify qual tipo de saídas toolist quando você consulta posteriormente em lotes para Olá persistentes saídas de uma determinada tarefa.</span><span class="sxs-lookup"><span data-stu-id="f4a46-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="f4a46-158">Em outras palavras, quando você lista Olá saídas para uma tarefa, você pode filtrar a lista de saudação em um dos tipos de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="f4a46-159">Por exemplo, "Envie-me Olá *visualização* de saída de tarefa *109*."</span><span class="sxs-lookup"><span data-stu-id="f4a46-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="f4a46-160">Mais informações sobre a listagem e recuperando saídas aparece na [recuperar a saída](#retrieve-output) posteriormente Olá artigo.</span><span class="sxs-lookup"><span data-stu-id="f4a46-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="f4a46-161">Olá tipo de saída também determina onde no hello Azure portal um determinado arquivo aparece: *TaskOutput*-arquivos categorizados aparecem sob **arquivos de saída de tarefa**, e *TaskLog*arquivos aparecem sob **tarefa logs**.</span><span class="sxs-lookup"><span data-stu-id="f4a46-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="f4a46-162">Armazenar saídas de trabalhos</span><span class="sxs-lookup"><span data-stu-id="f4a46-162">Store job outputs</span></span>

<span data-ttu-id="f4a46-163">Além disso gera toostoring tarefa, você pode armazenar saídas Olá associadas a um trabalho inteiro.</span><span class="sxs-lookup"><span data-stu-id="f4a46-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="f4a46-164">Por exemplo, na tarefa de mesclagem de saudação de um trabalho de processamento de filme, você pode persistir filme Olá totalmente processado como uma saída de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4a46-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="f4a46-165">Quando o trabalho for concluído, seu aplicativo cliente pode listar recuperar Olá saídas de trabalho hello e não precisa tooquery Olá tarefas individuais.</span><span class="sxs-lookup"><span data-stu-id="f4a46-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="f4a46-166">Armazenar a saída de trabalho por chamada hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] método e especifique Olá [JobOutputKind] [ net_joboutputkind] e nome de arquivo:</span><span class="sxs-lookup"><span data-stu-id="f4a46-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="f4a46-167">Assim como acontece com hello **TaskOutputKind** tipo para saídas de tarefa, você usar Olá [JobOutputKind] [ net_joboutputkind] tipo toocategorize um trabalho da mantidas arquivos.</span><span class="sxs-lookup"><span data-stu-id="f4a46-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="f4a46-168">Esse parâmetro permite consultar toolater (lista) de um tipo específico de saída.</span><span class="sxs-lookup"><span data-stu-id="f4a46-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="f4a46-169">Olá **JobOutputKind** tipo inclui as categorias de saída e visualização e oferece suporte à criação de categorias personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f4a46-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="f4a46-170">Armazenar logs de tarefas</span><span class="sxs-lookup"><span data-stu-id="f4a46-170">Store task logs</span></span>

<span data-ttu-id="f4a46-171">Além disso toopersisting que um armazenamento de toodurable arquivo quando uma tarefa ou trabalho conclui, talvez você precise toopersist arquivos que são atualizados durante a execução de uma tarefa Olá &mdash; arquivos de log ou `stdout.txt` e `stderr.txt`, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="f4a46-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="f4a46-172">Para essa finalidade, biblioteca de convenções de arquivo de lote do Azure Olá fornece Olá [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] método.</span><span class="sxs-lookup"><span data-stu-id="f4a46-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="f4a46-173">Com [SaveTrackedAsync][net_savetrackedasync], você pode rastrear o arquivo de tooa de atualizações no nó de saudação (em um intervalo que você especificar) e manter esses tooAzure atualizações armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4a46-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="f4a46-174">Olá trecho de código a seguir, usamos [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` no armazenamento do Azure durante a execução de saudação da tarefa de saudação a cada 15 segundos:</span><span class="sxs-lookup"><span data-stu-id="f4a46-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="f4a46-175">seção de comentários Olá `Code tooprocess data and produce output file(s)` é um espaço reservado para o código de saudação que normalmente executará a tarefa.</span><span class="sxs-lookup"><span data-stu-id="f4a46-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="f4a46-176">Por exemplo, você pode ter código que baixa dados do Armazenamento do Azure e executa uma transformação ou um cálculo neles.</span><span class="sxs-lookup"><span data-stu-id="f4a46-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="f4a46-177">parte importante Olá este trecho de código é demonstrar como você pode encapsular esse código em um `using` tooperiodically bloco atualizar um arquivo com [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="f4a46-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="f4a46-178">agente do nó de saudação é um programa que é executado em cada nó no pool de saudação e fornece a interface de comando e controle de saudação entre nó hello e serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4a46-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="f4a46-179">Olá `Task.Delay` chamada é necessária no final da saudação deste `using` tooensure de bloco que Olá agente nó tem tempo tooflush Olá conteúdo padrão toohello stdout.txt arquivo no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4a46-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="f4a46-180">Sem esse atraso, é possível toomiss Olá últimos segundos de saída.</span><span class="sxs-lookup"><span data-stu-id="f4a46-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="f4a46-181">Esse atraso pode não ser necessário para todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="f4a46-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="f4a46-182">Quando você habilita o arquivo de controle com **SaveTrackedAsync**, apenas *acrescenta* arquivo rastreado toohello são persistente tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4a46-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="f4a46-183">Use esse método somente para rastrear arquivos de log não girando ou outros arquivos que são gravados toowith acrescentar a fim de toohello operações de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="f4a46-184">Recuperar dados de saída</span><span class="sxs-lookup"><span data-stu-id="f4a46-184">Retrieve output data</span></span>

<span data-ttu-id="f4a46-185">Quando você recupera a saída persistente usando Olá convenções de arquivo de lote do Azure biblioteca, você pode fazer isso de forma centralizada em tarefas e trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4a46-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="f4a46-186">Você pode solicitar a saudação de saída para determinada tarefa ou trabalho sem a necessidade de tooknow seu caminho no armazenamento do Azure ou o mesmo nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="f4a46-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="f4a46-187">Em vez disso, você pode solicitar os arquivos de saída pela ID de tarefa ou trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4a46-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="f4a46-188">Hello trecho de código a seguir itera por meio de tarefas do trabalho, imprime algumas informações sobre os arquivos de saída Olá para tarefa hello e baixa os arquivos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4a46-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="f4a46-189">Exibir arquivos de saída no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a46-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="f4a46-190">portal do Azure Hello exibe os arquivos de saída de tarefa e logs que são persistente tooa vinculado conta de armazenamento do Azure usando Olá [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="f4a46-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="f4a46-191">Você pode implementar essas convenções em Olá um idioma de sua escolha, ou você pode usar a biblioteca de convenções de arquivo hello em seus aplicativos .NET.</span><span class="sxs-lookup"><span data-stu-id="f4a46-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="f4a46-192">exibição de saudação tooenable dos seus arquivos de saída no portal de Olá, é preciso atender Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4a46-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="f4a46-193">[Vincular uma conta de armazenamento do Azure](#requirement-linked-storage-account) tooyour conta do lote.</span><span class="sxs-lookup"><span data-stu-id="f4a46-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="f4a46-194">Aderir toohello predefinido convenções de nomenclatura para arquivos e contêineres de armazenamento quando a persistência de saídas.</span><span class="sxs-lookup"><span data-stu-id="f4a46-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="f4a46-195">Você pode encontrar a definição de saudação essas convenções na biblioteca de convenções de arquivo hello [Leiame][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="f4a46-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="f4a46-196">Se você usar o hello [convenções de arquivo de lote do Azure] [ nuget_package] toopersist biblioteca sua saída, os arquivos são mantidos toohello convenções de arquivo padrão de acordo com.</span><span class="sxs-lookup"><span data-stu-id="f4a46-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="f4a46-197">a saída da tarefa tooview arquivos e os logs na Olá portal do Azure, navegue até a tarefa toohello cuja saída você está interessado, em seguida, clique em **arquivos de saída salvo** ou **registros salvos**.</span><span class="sxs-lookup"><span data-stu-id="f4a46-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="f4a46-198">Esta imagem mostra Olá **arquivos de saída salvo** para tarefa de saudação com ID "007":</span><span class="sxs-lookup"><span data-stu-id="f4a46-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="f4a46-199">![Saídas de tarefas folha em Olá portal do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="f4a46-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="f4a46-200">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="f4a46-200">Code sample</span></span>

<span data-ttu-id="f4a46-201">Olá [PersistOutputs] [ github_persistoutputs] projeto de exemplo é uma saudação [exemplos de código do Azure Batch] [ github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f4a46-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="f4a46-202">Essa solução do Visual Studio demonstra como armazenamento toodurable de saída da tarefa de toopersist de biblioteca do toouse Olá convenções de arquivo de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a46-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="f4a46-203">Olá toorun de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f4a46-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="f4a46-204">Projeto aberto Olá no **Visual Studio 2015 ou mais recente**.</span><span class="sxs-lookup"><span data-stu-id="f4a46-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="f4a46-205">Adicionar o lote e o armazenamento **as credenciais de conta** muito**AccountSettings.settings** no projeto de Microsoft.Azure.Batch.Samples.Common hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="f4a46-206">**Criar** (mas não executam) Olá solução.</span><span class="sxs-lookup"><span data-stu-id="f4a46-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="f4a46-207">Restaure todos os pacotes NuGet, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="f4a46-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="f4a46-208">Saudação de uso do Azure tooupload portal um [pacote de aplicativo](batch-application-packages.md) para **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="f4a46-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="f4a46-209">Incluir Olá `PersistOutputsTask.exe` e seus assemblies dependentes no pacote. zip de hello, ID do conjunto de aplicativo hello muito "PersistOutputsTask" e o aplicativo hello pacote versão muito "1.0".</span><span class="sxs-lookup"><span data-stu-id="f4a46-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="f4a46-210">**Iniciar** hello (Executar) **PersistOutputs** projeto.</span><span class="sxs-lookup"><span data-stu-id="f4a46-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="f4a46-211">Quando solicitadas toochoose Olá persistência tecnologia toouse para execução do exemplo hello, digite **1** toorun Olá exemplo hello convenções arquivo biblioteca toopersist a saída da tarefa.</span><span class="sxs-lookup"><span data-stu-id="f4a46-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f4a46-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4a46-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="f4a46-213">Obter a biblioteca de convenções de arquivo em lotes de saudação para .NET</span><span class="sxs-lookup"><span data-stu-id="f4a46-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="f4a46-214">Olá convenções de arquivo em lotes biblioteca para .NET estão disponível no [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="f4a46-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="f4a46-215">estende a biblioteca de Olá Olá [CloudJob] [ net_cloudjob] e [CloudTask] [ net_cloudtask] classes com novos métodos.</span><span class="sxs-lookup"><span data-stu-id="f4a46-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="f4a46-216">Consulte também Olá [documentação de referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) para a biblioteca de convenções de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f4a46-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="f4a46-217">Olá [código-fonte] [ github_file_conventions] para Olá convenções do arquivo de biblioteca está disponível no GitHub no hello SDK do Microsoft Azure para o repositório do .NET.</span><span class="sxs-lookup"><span data-stu-id="f4a46-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="f4a46-218">Explorar outras abordagens para manter dados de saída</span><span class="sxs-lookup"><span data-stu-id="f4a46-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="f4a46-219">Consulte [Persist trabalhos e tarefas de saída tooAzure armazenamento](batch-task-output.md) para obter uma visão geral de persistir dados de tarefa e o trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4a46-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="f4a46-220">Consulte [persistir dados de tarefa tooAzure armazenamento com a API do serviço de lote de saudação](batch-task-output-files.md) toolearn como toouse Olá API do serviço de lote toopersist dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f4a46-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Arquivos de saída salvos e Seletores de logs salvos no portal"
[2]: ./media/batch-task-output/task-output-02.png "Saídas de tarefas folha em Olá portal do Azure"
