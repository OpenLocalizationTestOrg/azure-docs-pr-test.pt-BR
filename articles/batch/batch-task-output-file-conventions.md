---
title: "Manter saída de trabalhos e tarefas no armazenamento do Azure com a biblioteca de Convenções de Arquivo para .NET – Lote do Azure | Microsoft Docs"
description: "Saiba como usar a biblioteca de Convenções de Arquivo em Lote do Azure para .NET para manter a saída de tarefa e trabalho em Lote no Armazenamento do Azure e exibir a saída mantida no portal do Azure."
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
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="0dc45-103">Manter os dados de trabalho e tarefa no Armazenamento do Azure com a biblioteca de Convenções de Arquivo em Lotes para o .NET manter</span><span class="sxs-lookup"><span data-stu-id="0dc45-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="0dc45-104">Uma maneira de manter os dados de tarefa é usar a [biblioteca Convenções de Arquivo em Lote do Azure para .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="0dc45-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="0dc45-105">A biblioteca de Convenções de Arquivo simplifica o processo de armazenar dados de saída de tarefa no Armazenamento do Azure e recuperá-los.</span><span class="sxs-lookup"><span data-stu-id="0dc45-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="0dc45-106">Você pode usar a biblioteca de Convenções de Arquivo em código tanto do cliente quanto de &mdash; no código de tarefa para manter arquivos e no código do cliente para listá-los e recuperá-los.</span><span class="sxs-lookup"><span data-stu-id="0dc45-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="0dc45-107">Seu código de tarefa também pode usar a biblioteca para recuperar as saídas de tarefas upstream, como em um cenário de [dependências de tarefa](batch-task-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="0dc45-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="0dc45-108">Para recuperar arquivos de saída com a biblioteca de Convenções de Arquivo, você pode localizar os arquivos para um determinado trabalho ou tarefa listando-os por ID e finalidade.</span><span class="sxs-lookup"><span data-stu-id="0dc45-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="0dc45-109">Você não precisa saber os nomes nem os locais dos arquivos.</span><span class="sxs-lookup"><span data-stu-id="0dc45-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="0dc45-110">Por exemplo, você pode usar a biblioteca de Convenções de Arquivo para listar todos os arquivos intermediários para uma determinada tarefa ou obter um arquivo de versão prévia para um determinado trabalho.</span><span class="sxs-lookup"><span data-stu-id="0dc45-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="0dc45-111">Começando com a versão de 01/05/2017, a API de serviço de Lote dá suporte a manter dados de saída para o Armazenamento do Azure para tarefas e tarefas do gerenciador de trabalho que são executadas em pools criados com a configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0dc45-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="0dc45-112">A API do serviço de Lote oferece uma maneira simples de manter a saída de dentro do código que cria uma tarefa e serve como uma alternativa à biblioteca de Convenções de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="0dc45-113">Você pode modificar seus aplicativos cliente em Lotes para manter a saída sem necessidade de atualizar o aplicativo que sua tarefa está executando.</span><span class="sxs-lookup"><span data-stu-id="0dc45-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="0dc45-114">Para obter mais informações, consulte [Manter dados de tarefa no Armazenamento do Azure com a API de serviço em Lote](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="0dc45-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="0dc45-115">Quando usar a biblioteca Convenções de Arquivo para manter a saída da tarefa?</span><span class="sxs-lookup"><span data-stu-id="0dc45-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="0dc45-116">O Lote do Azure fornece mais de uma maneira de manter a saída da tarefa.</span><span class="sxs-lookup"><span data-stu-id="0dc45-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="0dc45-117">A biblioteca Convenções de Arquivo é ideal para estes cenários:</span><span class="sxs-lookup"><span data-stu-id="0dc45-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="0dc45-118">Você pode facilmente modificar o código para o aplicativo que sua tarefa está executando para manter os arquivos usando a biblioteca Convenções de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="0dc45-119">Você desejar transmitir dados para o Armazenamento do Azure enquanto a tarefa ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="0dc45-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="0dc45-120">Você desejar manter os dados dos pools criados com a configuração do serviço de nuvem ou a configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0dc45-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="0dc45-121">O aplicativo cliente ou outras tarefas no trabalho precisar localizar e baixar arquivos de saída de tarefas por ID ou por finalidade.</span><span class="sxs-lookup"><span data-stu-id="0dc45-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="0dc45-122">Você desejar exibir a saída da tarefa no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc45-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="0dc45-123">Se seu cenário for diferente daqueles listados acima, poderá ser necessário considerar uma abordagem diferente.</span><span class="sxs-lookup"><span data-stu-id="0dc45-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="0dc45-124">Para obter mais informações sobre outras opções para manter a saída da tarefa, consulte [Manter saída de trabalho e tarefa no Armazenamento do Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="0dc45-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="0dc45-125">O que é o padrão Convenções do Arquivo em Lote?</span><span class="sxs-lookup"><span data-stu-id="0dc45-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="0dc45-126">O [padrão Convenções de Arquivo em Lote](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornece um esquema de nomenclatura para os contêineres de destino e os caminhos de blob nos quais os arquivos de saída são gravados.</span><span class="sxs-lookup"><span data-stu-id="0dc45-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="0dc45-127">Os arquivos mantidos no Armazenamento do Azure que segue o padrão Convenções de Arquivo ficam automaticamente disponíveis para exibição no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc45-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="0dc45-128">O portal está ciente da convenção de nomenclatura e, portanto, pode exibir arquivos que aderem a ela.</span><span class="sxs-lookup"><span data-stu-id="0dc45-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="0dc45-129">A biblioteca Convenções de Arquivo para .NET nomeia automaticamente seus contêineres de armazenamento e os arquivos de saída de tarefa acordo com o padrão de Convenções de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="0dc45-130">A biblioteca Convenções de Arquivo também fornece métodos para consultar arquivos de saída no Armazenamento do Azure acordo com a ID do trabalho, a ID da tarefa ou a finalidade.</span><span class="sxs-lookup"><span data-stu-id="0dc45-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="0dc45-131">Se você estiver desenvolvendo com uma linguagem que não .NET, poderá implementar o padrão de Convenções de Arquivo você mesmo em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="0dc45-132">Para obter mais informações, consulte [Sobre o padrão de Convenções de Arquivo em Lote](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="0dc45-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="0dc45-133">Vincular uma conta de Armazenamento do Azure à sua conta do Lote</span><span class="sxs-lookup"><span data-stu-id="0dc45-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="0dc45-134">Para manter os dados de saída no Armazenamento do Azure usando a biblioteca Convenções de Arquivo, primeiro vincule uma conta de Armazenamento do Azure à sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="0dc45-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="0dc45-135">Se ainda não tiver fez isso, vincule uma conta de Armazenamento à sua conta do Lote usando o [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="0dc45-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="0dc45-136">Navegue até sua conta do Lote no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc45-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="0dc45-137">Em **Configurações**, selecione **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="0dc45-138">Se você ainda não tiver uma conta de Armazenamento associada à sua conta do Lote, clique em **Conta de Armazenamento (Nenhuma)**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="0dc45-139">Selecione uma conta de Armazenamento na lista para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0dc45-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="0dc45-140">Para melhor desempenho, use uma conta de Armazenamento do Azure que esteja na mesma região que a conta do Lote em que as tarefas estão em execução.</span><span class="sxs-lookup"><span data-stu-id="0dc45-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="0dc45-141">Manter os dados de saída</span><span class="sxs-lookup"><span data-stu-id="0dc45-141">Persist output data</span></span>

<span data-ttu-id="0dc45-142">Para manter os dados de saída de trabalho e tarefa com a biblioteca Convenções de Arquivo, crie um contêiner no Armazenamento do Azure e salve a saída no contêiner.</span><span class="sxs-lookup"><span data-stu-id="0dc45-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="0dc45-143">Use a [biblioteca de cliente do Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) em seu código de tarefa para carregar a saída da tarefa para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="0dc45-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="0dc45-144">Para obter mais informações sobre como trabalhar com contêineres e blobs no Armazenamento do Azure, consulte [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="0dc45-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="0dc45-145">Todas as saídas de trabalho e tarefa mantidas com a biblioteca Convenções de Arquivo são armazenadas no mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="0dc45-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="0dc45-146">Se um grande número de tarefas tentar manter arquivos ao mesmo tempo, poderão ser impostos [limites de limitação de armazenamento](../storage/common/storage-performance-checklist.md#blobs).</span><span class="sxs-lookup"><span data-stu-id="0dc45-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="0dc45-147">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0dc45-147">Create storage container</span></span>

<span data-ttu-id="0dc45-148">Para manter a saída da tarefa no Armazenamento do Azure, primeiro crie um contêiner chamando [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="0dc45-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="0dc45-149">Esse método de extensão usa um objeto [CloudStorageAccount][net_cloudstorageaccount] como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0dc45-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="0dc45-150">Ele cria um contêiner nomeado de acordo com o padrão de Convenções de Arquivo, de modo que seu conteúdo é detectável pelo portal do Azure e os métodos de recuperação discutidos posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="0dc45-151">Normalmente, você coloca o código para criar um contêiner no seu aplicativo cliente &mdash; o aplicativo que cria os pools, os trabalhos e as tarefas.</span><span class="sxs-lookup"><span data-stu-id="0dc45-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="0dc45-152">Armazenar saídas de tarefas</span><span class="sxs-lookup"><span data-stu-id="0dc45-152">Store task outputs</span></span>

<span data-ttu-id="0dc45-153">Agora que você preparou um contêiner no Armazenamento do Azure, as tarefas podem salvar a saída no contêiner usando a classe [TaskOutputStorage][net_taskoutputstorage] encontrada na biblioteca Convenções de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="0dc45-154">No código da tarefa, primeiro crie um objeto [TaskOutputStorage][net_taskoutputstorage]. Em seguida, quando a tarefa concluir seu trabalho, chame o método [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] para salvar sua saída no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc45-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="0dc45-155">O parâmetro `kind` do método [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) categoriza os arquivos mantidos.</span><span class="sxs-lookup"><span data-stu-id="0dc45-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="0dc45-156">Há quatro tipos predefinidos de [TaskOutputKind][net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog` e `TaskIntermediate.`. Você também pode definir as categorias personalizadas da saída.</span><span class="sxs-lookup"><span data-stu-id="0dc45-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="0dc45-157">Esses tipos de saída permitem que você especifique qual tipo de saídas listar ao consultar posteriormente o Lote para obter as saídas persistentes de determinada tarefa.</span><span class="sxs-lookup"><span data-stu-id="0dc45-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="0dc45-158">Em outras palavras, ao listar as saídas de uma tarefa, você pode filtrar a lista em um dos tipos de saída.</span><span class="sxs-lookup"><span data-stu-id="0dc45-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="0dc45-159">Por exemplo, "Forneça a saída de *visualização* da tarefa *109*".</span><span class="sxs-lookup"><span data-stu-id="0dc45-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="0dc45-160">Mais informações sobre listagem e recuperação de saídas estão disponíveis em [Recuperar saída](#retrieve-output) , mais adiante no artigo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="0dc45-161">O tipo de saída também designa em que ponto no portal do Azure um arquivo específico é exibido: arquivos categorizados por *TaskOutput* aparecem em **Arquivos de saída de tarefa** e arquivos de *TaskLog* aparecem em **Logs de tarefa**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="0dc45-162">Armazenar saídas de trabalhos</span><span class="sxs-lookup"><span data-stu-id="0dc45-162">Store job outputs</span></span>

<span data-ttu-id="0dc45-163">Além de armazenar as saídas de tarefas, você pode armazenar as saídas associadas a um trabalho inteiro.</span><span class="sxs-lookup"><span data-stu-id="0dc45-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="0dc45-164">Por exemplo, na tarefa de mesclagem de um trabalho de renderização de filme, você pode persistir o filme totalmente renderizado como uma saída de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0dc45-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="0dc45-165">Quando seu trabalho estiver concluído, o aplicativo cliente poderá simplesmente listar e recuperar as saídas para o trabalho e não precisará consultar as tarefas individuais.</span><span class="sxs-lookup"><span data-stu-id="0dc45-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="0dc45-166">Armazene a saída de trabalho chamando o método [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] e especifique o [JobOutputKind][net_joboutputkind] e o nome de arquivo:</span><span class="sxs-lookup"><span data-stu-id="0dc45-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="0dc45-167">Assim como o tipo **TaskOutputKind** para saídas de tarefa, você usa o parâmetro [JobOutputKind][net_joboutputkind] para categorizar os arquivos mantidos de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="0dc45-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="0dc45-168">Esse parâmetro permite que você consulte posteriormente para (listar) um tipo específico de saída.</span><span class="sxs-lookup"><span data-stu-id="0dc45-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="0dc45-169">O tipo **JobOutputKind** inclui as categorias de saída e versão prévia e dá suporte à criação de categorias personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0dc45-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="0dc45-170">Armazenar logs de tarefas</span><span class="sxs-lookup"><span data-stu-id="0dc45-170">Store task logs</span></span>

<span data-ttu-id="0dc45-171">Além de manter um arquivo no armazenamento durável quando uma tarefa ou trabalho é concluído, talvez seja necessário manter arquivos atualizados durante a execução de uma tarefa: arquivos de log &mdash; ou `stdout.txt` e `stderr.txt`, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="0dc45-172">Para essa finalidade, a biblioteca de Convenções de Arquivo do Lote do Azure fornece o método [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="0dc45-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="0dc45-173">Com [SaveTrackedAsync][net_savetrackedasync], você pode acompanhar atualizações de um arquivo no nó (em um intervalo que você especificar) e persistir essas atualizações no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc45-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="0dc45-174">No trecho de código a seguir, usamos [SaveTrackedAsync] para atualizar [net_savetrackedasync]`stdout.txt` no Armazenamento do Azure a cada 15 segundos durante a execução da tarefa:</span><span class="sxs-lookup"><span data-stu-id="0dc45-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="0dc45-175">A seção comentada `Code to process data and produce output file(s)` é um espaço reservado para o código que sua tarefa normalmente executaria.</span><span class="sxs-lookup"><span data-stu-id="0dc45-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="0dc45-176">Por exemplo, você pode ter código que baixa dados do Armazenamento do Azure e executa uma transformação ou um cálculo neles.</span><span class="sxs-lookup"><span data-stu-id="0dc45-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="0dc45-177">A parte importante desse trecho de código é demonstrar como você pode encapsular o código em um bloco `using` para atualizar periodicamente um arquivo com [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="0dc45-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="0dc45-178">O agente do nó é um programa executado em cada nó no pool e fornece a interface de comando e controle entre o nó e o serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="0dc45-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="0dc45-179">A chamada `Task.Delay` é necessária no final deste bloco `using` para garantir que o agente do nó tenha tempo para liberar o conteúdo do padrão que sai para o arquivo stdout.txt no nó.</span><span class="sxs-lookup"><span data-stu-id="0dc45-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="0dc45-180">Sem esse atraso, é possível ignorar os últimos segundos de saída.</span><span class="sxs-lookup"><span data-stu-id="0dc45-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="0dc45-181">Esse atraso pode não ser necessário para todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="0dc45-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc45-182">Quando você habilita o acompanhamento de arquivo com **SaveTrackedAsync**, apenas *acréscimos* ao arquivo rastreado acompanhado são mantidos no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc45-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="0dc45-183">Use esse método somente para acompanhar arquivos de log não rotativos ou outros arquivos que são gravados com operações de acréscimo ao final do arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="0dc45-184">Recuperar dados de saída</span><span class="sxs-lookup"><span data-stu-id="0dc45-184">Retrieve output data</span></span>

<span data-ttu-id="0dc45-185">Quando você recupera sua saída persistente usando a biblioteca de Convenções de Arquivo do Lote do Azure, pode fazer isso de maneira voltada para tarefas e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="0dc45-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="0dc45-186">Você pode solicitar a saída para determinada tarefa ou trabalho sem precisar saber o caminho no Armazenamento do Azure nem mesmo seu nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="0dc45-187">Em vez disso, você pode solicitar os arquivos de saída pela ID de tarefa ou trabalho.</span><span class="sxs-lookup"><span data-stu-id="0dc45-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="0dc45-188">O trecho de código a seguir itera em todas as tarefas de um trabalho, imprime algumas informações sobre os arquivos de saída para a tarefa e então baixa os arquivos do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0dc45-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="0dc45-189">Exibir arquivos de saída no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0dc45-189">View output files in the Azure portal</span></span>

<span data-ttu-id="0dc45-190">O portal do Azure exibe os arquivos de saída de tarefa e os logs que são mantidos para uma conta de Armazenamento do Azure vinculado usando o [padrão de Convenções de Arquivo em Lote](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="0dc45-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="0dc45-191">Você mesmo pode implementar essas convenções em uma linguagem de sua escolha ou pode usar a biblioteca de Convenções de Arquivo em seus aplicativos .NET.</span><span class="sxs-lookup"><span data-stu-id="0dc45-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="0dc45-192">Para habilitar a exibição de seus arquivos de saída no portal, você deve atender aos seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="0dc45-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="0dc45-193">[Vincular uma conta do Armazenamento do Azure](#requirement-linked-storage-account) à sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="0dc45-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="0dc45-194">Seguir as convenções de nomenclatura predefinidas para os arquivos e contêineres de Armazenamento ao persistir saídas.</span><span class="sxs-lookup"><span data-stu-id="0dc45-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="0dc45-195">Você pode encontrar a definição dessas convenções na biblioteca Convenções de Arquivo [LEIAME][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="0dc45-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="0dc45-196">Se você usar a biblioteca [Convenções de Arquivo em Lote do Azure] [nuget_package] para manter sua saída, seus arquivos serão mantidos de acordo com o padrão de Convenções de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="0dc45-197">Para exibir logs e arquivos de saída de tarefa no portal do Azure, navegue até a tarefa em cuja saída você está interessado e clique em **Arquivos de saída salvos** ou **Logs salvos**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="0dc45-198">Esta imagem mostra os **Arquivos de saída salvos** para a tarefa com a ID "007":</span><span class="sxs-lookup"><span data-stu-id="0dc45-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="0dc45-199">![Folha de saídas de tarefa no portal do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="0dc45-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="0dc45-200">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="0dc45-200">Code sample</span></span>

<span data-ttu-id="0dc45-201">O projeto de exemplo [PersistOutputs][github_persistoutputs] é um dos [exemplos de código do Lote do Azure][github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="0dc45-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="0dc45-202">Essa solução do Visual Studio demonstra como usar a biblioteca de Convenções de Arquivo de Lote do Azure para persistir a saída da tarefa para o armazenamento durável.</span><span class="sxs-lookup"><span data-stu-id="0dc45-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="0dc45-203">Para executar o exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0dc45-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="0dc45-204">Abra o projeto no **Visual Studio 2015 ou mais recente**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="0dc45-205">Adicione suas **credenciais de conta** do Lote e do Armazenamento a **AccountSettings.settings** no projeto Microsoft.Azure.Batch.Samples.Common.</span><span class="sxs-lookup"><span data-stu-id="0dc45-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="0dc45-206">**Compile** (mas não execute) a solução.</span><span class="sxs-lookup"><span data-stu-id="0dc45-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="0dc45-207">Restaure todos os pacotes NuGet, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="0dc45-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="0dc45-208">Use o portal do Azure para carregar um [pacote de aplicativos](batch-application-packages.md) para **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="0dc45-209">Inclua o `PersistOutputsTask.exe` e seus assemblies dependentes no pacote .zip, defina a ID do aplicativo como "PersistOutputsTask" e a versão do pacote de aplicativos como "1.0".</span><span class="sxs-lookup"><span data-stu-id="0dc45-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="0dc45-210">**Inicie** (execute) o projeto **PersistOutputs**.</span><span class="sxs-lookup"><span data-stu-id="0dc45-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="0dc45-211">Quando solicitado a escolher a tecnologia de persistência a usar para executar o exemplo, digite **1** para executar o exemplo usando a biblioteca Convenções de Arquivo para manter a saída da tarefa.</span><span class="sxs-lookup"><span data-stu-id="0dc45-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0dc45-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dc45-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="0dc45-213">Obter a biblioteca Convenções de Arquivo em Lote para .NET</span><span class="sxs-lookup"><span data-stu-id="0dc45-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="0dc45-214">A biblioteca Convenções de Arquivo em Lote para .NET está disponível em [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="0dc45-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="0dc45-215">A biblioteca amplia as classes [CloudJob][net_cloudjob] e [CloudTask][net_cloudtask] com novos métodos.</span><span class="sxs-lookup"><span data-stu-id="0dc45-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="0dc45-216">Consulte também a [documentação de referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) para a biblioteca Convenções de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="0dc45-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="0dc45-217">O [código-fonte][github_file_conventions] para a biblioteca Convenções de Arquivo está disponível no GitHub no repositório do SDK do Microsoft Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="0dc45-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="0dc45-218">Explorar outras abordagens para manter dados de saída</span><span class="sxs-lookup"><span data-stu-id="0dc45-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="0dc45-219">Consulte [Manter saída de trabalho e tarefa para Armazenamento do Azure](batch-task-output.md) para obter uma visão geral de persistir dados de tarefa e trabalho.</span><span class="sxs-lookup"><span data-stu-id="0dc45-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="0dc45-220">Consulte [Manter dados de tarefa para o Armazenamento do Azure com a API de serviço de Lote](batch-task-output-files.md) para aprender a usar a API de serviço de Lote para manter os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="0dc45-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Folha de saídas de tarefa no portal do Azure"
