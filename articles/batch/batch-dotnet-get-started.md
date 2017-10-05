---
title: Tutorial - Use a biblioteca de cliente do Lote do Azure para .NET | Microsoft Docs
description: "Aprenda os conceitos básicos do Lote do Azure e crie uma solução simples usando o .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="38019-103">Comece a criar soluções com a biblioteca de cliente do Lote para .NET</span><span class="sxs-lookup"><span data-stu-id="38019-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38019-104">.NET</span><span class="sxs-lookup"><span data-stu-id="38019-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="38019-105">Python</span><span class="sxs-lookup"><span data-stu-id="38019-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="38019-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="38019-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="38019-107">Conheça os fundamentos do [Lote do Azure][azure_batch] e da biblioteca [.NET do Lote][net_api] neste artigo, em que mostramos o passo a passo de um aplicativo de exemplo em C#.</span><span class="sxs-lookup"><span data-stu-id="38019-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="38019-108">Veremos como o aplicativo de exemplo aproveita o serviço Lote para processar uma carga de trabalho paralela na nuvem e como ele interage com o [Armazenamento do Azure](../storage/common/storage-introduction.md) para a preparação e a recuperação de arquivos.</span><span class="sxs-lookup"><span data-stu-id="38019-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="38019-109">Você verá um fluxo de trabalho comum do aplicativo Lote e obterá uma compreensão básica dos principais componentes do Lote, como trabalhos, tarefas, pools e nós de computação.</span><span class="sxs-lookup"><span data-stu-id="38019-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="38019-110">![Fluxo de trabalho da solução do Lote (básico)][11]</span><span class="sxs-lookup"><span data-stu-id="38019-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="38019-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="38019-111">Prerequisites</span></span>
<span data-ttu-id="38019-112">Este artigo pressupõe que você tenha um conhecimento prático do C# e do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38019-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="38019-113">Ele também pressupõe que você é capaz de satisfazer os requisitos de criação de conta especificados abaixo para o Azure e os serviços Lote e Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="38019-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="38019-114">Contas</span><span class="sxs-lookup"><span data-stu-id="38019-114">Accounts</span></span>
* <span data-ttu-id="38019-115">**Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="38019-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="38019-116">**Conta do Lote**: quando você tiver uma assinatura do Azure, [crie uma conta do Lote do Azure](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="38019-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="38019-117">**Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="38019-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38019-118">No momento, o Lote dá suporte *somente* ao tipo de conta de armazenamento de **uso geral**, conforme descrito na etapa 5 [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="38019-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="38019-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38019-119">Visual Studio</span></span>
<span data-ttu-id="38019-120">Você deve ter o **Visual Studio 2015 ou mais recente** para compilar o projeto de exemplo.</span><span class="sxs-lookup"><span data-stu-id="38019-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="38019-121">Você pode encontrar versões gratuitas e de avaliação do Visual Studio na [visão geral dos produtos do Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="38019-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="38019-122">*DotNetTutorial* </span><span class="sxs-lookup"><span data-stu-id="38019-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="38019-123">O exemplo [DotNetTutorial][github_dotnettutorial] é um dos vários exemplos de código de Lote encontrados no repositório [azure-batch-samples][github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="38019-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="38019-124">Você pode baixar todos os exemplos clicando no botão **Clonar ou baixar > Baixar ZIP** na home page do repositório ou clicando no link de download direto de [azure-batch-samples-master.zip][github_samples_zip].</span><span class="sxs-lookup"><span data-stu-id="38019-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="38019-125">Depois de extrair o conteúdo do arquivo ZIP, você poderá encontrar a solução na seguinte pasta:</span><span class="sxs-lookup"><span data-stu-id="38019-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="38019-126">Gerenciador do Lote do Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="38019-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="38019-127">O [Gerenciador do Lote do Azure][github_batchexplorer] é um utilitário gratuito incluído no repositório [azure-batch-samples][github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="38019-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="38019-128">Embora não seja necessário para concluir este tutorial, pode ser útil ao desenvolver e depurar suas soluções do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="38019-129">Visão geral do projeto de exemplo DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="38019-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="38019-130">O exemplo de código *DotNetTutorial* é uma solução do Visual Studio que consiste em dois projetos: **DotNetTutorial** e **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="38019-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="38019-131">**DotNetTutorial** é o aplicativo cliente que interage com os serviços Lote e Armazenamento para executar uma carga de trabalho paralela em nós de computação (máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="38019-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="38019-132">O DotNetTutorial é executado em sua estação de trabalho local.</span><span class="sxs-lookup"><span data-stu-id="38019-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="38019-133">**TaskApplication** é o programa executado em nós de computação no Azure para executar o trabalho real.</span><span class="sxs-lookup"><span data-stu-id="38019-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="38019-134">No exemplo, `TaskApplication.exe` analisa o texto em um arquivo baixado do Armazenamento do Azure (o arquivo de entrada).</span><span class="sxs-lookup"><span data-stu-id="38019-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="38019-135">Em seguida, ele produz um arquivo de texto (o arquivo de saída) que contém uma lista das três palavras principais que aparecem no arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="38019-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="38019-136">Após criar o arquivo de saída, TaskApplication carrega o arquivo no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="38019-137">Isso o disponibiliza para download para o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="38019-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="38019-138">O TaskApplication é executado em paralelo em vários nós de computação no serviço Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="38019-139">O diagrama a seguir ilustra as principais operações executadas pelo aplicativo cliente, *DotNetTutorial*, e o aplicativo executado pelas tarefas, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="38019-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="38019-140">Esse fluxo de trabalho básico é típico de muitas soluções de computação criadas com o Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="38019-141">Embora ele não demonstre todos os recursos disponíveis no serviço Lote, praticamente todos os cenários do Lote incluem partes desse fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="38019-142">![Fluxo de trabalho de exemplo do Lote][8]</span><span class="sxs-lookup"><span data-stu-id="38019-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="38019-143">**Etapa 1.**</span><span class="sxs-lookup"><span data-stu-id="38019-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="38019-144">Crie **contêineres** no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="38019-145">
[**Etapa 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="38019-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="38019-146">Carregue o aplicativo de tarefas e os arquivos de entrada nos contêineres.</span><span class="sxs-lookup"><span data-stu-id="38019-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="38019-147">
[**Etapa 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="38019-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="38019-148">Criar um **pool** do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="38019-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="38019-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="38019-150">O pool **StartTask** baixa os arquivos binários da tarefa (TaskApplication) para os nós quando eles ingressam no pool.</span><span class="sxs-lookup"><span data-stu-id="38019-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="38019-151">
[**Etapa 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="38019-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="38019-152">Crie um **trabalho** do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="38019-153">
[**Etapa 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="38019-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="38019-154">Adicione **tarefas** ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="38019-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="38019-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="38019-156">As tarefas serão agendadas para a execução em nós.</span><span class="sxs-lookup"><span data-stu-id="38019-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="38019-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="38019-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="38019-158">Cada tarefa baixa seus dados de entrada do Armazenamento do Azure e então inicia a execução.</span><span class="sxs-lookup"><span data-stu-id="38019-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="38019-159">
[**Etapa 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="38019-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="38019-160">Monitore as tarefas.</span><span class="sxs-lookup"><span data-stu-id="38019-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="38019-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="38019-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="38019-162">À medida que as tarefas são concluídas, elas carregam os dados de saída no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="38019-163">
[**Etapa 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="38019-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="38019-164">Baixe a saída da tarefa do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="38019-164">Download task output from Storage.</span></span>

<span data-ttu-id="38019-165">Como mencionado, nem todas as soluções do Lote executam essas etapas exatas e podem incluir muitas outras, mas o aplicativo de exemplo *DotNetTutorial* demonstra os processos comuns encontrados em uma solução do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="38019-166">Criar o projeto de exemplo *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="38019-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="38019-167">Antes de poder executar o exemplo com êxito, você deverá especificar as credenciais de conta do Lote e do Armazenamento no arquivo `Program.cs` do projeto *DotNetTutorial*.</span><span class="sxs-lookup"><span data-stu-id="38019-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="38019-168">Se você ainda não tiver feito isso, abra a solução no Visual Studio clicando duas vezes no arquivo de solução `DotNetTutorial.sln` .</span><span class="sxs-lookup"><span data-stu-id="38019-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="38019-169">Ou abra-a no Visual Studio usando o menu **Arquivo > Abrir > Projeto/Solução**.</span><span class="sxs-lookup"><span data-stu-id="38019-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="38019-170">Abra `Program.cs` no projeto *DotNetTutorial* .</span><span class="sxs-lookup"><span data-stu-id="38019-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="38019-171">Em seguida, adicione as credenciais como especificado próximo à parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="38019-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="38019-172">Como mencionado acima, no momento você deve especificar as credenciais para uma conta de armazenamento de **uso geral** no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="38019-173">Os aplicativos do Lote usa o armazenamento de blobs na conta de armazenamento de **uso geral**.</span><span class="sxs-lookup"><span data-stu-id="38019-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="38019-174">Não especifique as credenciais de uma conta do Armazenamento criada por meio da seleção do tipo de conta do *armazenamento de Blobs* .</span><span class="sxs-lookup"><span data-stu-id="38019-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="38019-175">Você pode encontrar suas credenciais de conta do Lote e de Armazenamento na folha da conta de cada serviço no [Portal do Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="38019-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="38019-176">![Credenciais de Lote no portal][9]
![Credenciais de armazenamento no portal][10]</span><span class="sxs-lookup"><span data-stu-id="38019-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="38019-177">Agora que você atualizou o projeto com suas credenciais, clique com botão direito do mouse na solução no Gerenciador de Soluções e clique em **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="38019-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="38019-178">Confirme a restauração de qualquer pacote NuGet, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="38019-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="38019-179">Se os pacotes NuGet não forem automaticamente restaurados ou se você encontrar erros sobre uma falha ao restaurar os pacotes, verifique se você tem o [Gerenciador de Pacotes NuGet][nuget_packagemgr] instalado.</span><span class="sxs-lookup"><span data-stu-id="38019-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="38019-180">Em seguida, habilite o download de pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="38019-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="38019-181">Confira [Habilitando a Restauração de Pacotes Durante o Build][nuget_restore] para habilitar o download de pacotes.</span><span class="sxs-lookup"><span data-stu-id="38019-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="38019-182">Nas seções a seguir, dividimos o aplicativo de exemplo nas etapas executadas para processar uma carga de trabalho no serviço Lote e discutimos essas etapas detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="38019-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="38019-183">Você deve fazer referência à solução aberta no Visual Studio enquanto estiver trabalhando até o restante deste artigo já que nem todas as linhas de código do exemplo serão discutidas.</span><span class="sxs-lookup"><span data-stu-id="38019-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="38019-184">Navegue até a parte superior do método `MainAsync` no arquivo `Program.cs` do projeto *DotNetTutorial* para começar pela Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="38019-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="38019-185">Cada etapa abaixo segue aproximadamente a progressão de chamadas de método em `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="38019-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="38019-186">Etapa 1: Criar contêineres do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="38019-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="38019-187">![Criar contêineres no Armazenamento do Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="38019-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="38019-188">O Lote inclui suporte interno para a interação com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="38019-189">Os contêineres em sua conta do Armazenamento fornecerão os arquivos necessários às tarefas que serão executadas em sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="38019-190">Os contêineres também fornecem um local para armazenar os dados de saída produzidos pelas tarefas.</span><span class="sxs-lookup"><span data-stu-id="38019-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="38019-191">A primeira coisa que o aplicativo cliente *DotNetTutorial* faz é criar três contêineres no [Armazenamento de Blobs do Azure](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="38019-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="38019-192">**application**: esse contêiner hospedará o aplicativo executado pelas tarefas, além de qualquer uma de suas dependências, como DLLs.</span><span class="sxs-lookup"><span data-stu-id="38019-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="38019-193">**input**: as tarefas baixarão os arquivos de dados a serem processados do contêiner *input* .</span><span class="sxs-lookup"><span data-stu-id="38019-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="38019-194">**output**: quando as tarefas concluírem o processamento dos arquivos de entrada, carregarão os resultados no contêiner *output* .</span><span class="sxs-lookup"><span data-stu-id="38019-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="38019-195">Para interagir com uma conta de Armazenamento e criar contêineres, usamos a [Biblioteca de Cliente do Armazenamento do Azure para .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="38019-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="38019-196">Podemos criar uma referência à conta com [CloudStorageAccount][net_cloudstorageaccount] e dela criar um [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="38019-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="38019-197">Usamos a referência `blobClient` em todo o aplicativo e o passamos como um parâmetro para diversos métodos.</span><span class="sxs-lookup"><span data-stu-id="38019-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="38019-198">Um exemplo disso é o bloco de código logo após o trecho mostrado acima, onde chamamos `CreateContainerIfNotExistAsync` para realmente criarmos os contêineres.</span><span class="sxs-lookup"><span data-stu-id="38019-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="38019-199">Depois que os contêineres tiverem sido criados, o aplicativo poderá carregar os arquivos que serão usados pelas tarefas.</span><span class="sxs-lookup"><span data-stu-id="38019-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="38019-200">[Como usar o Armazenamento de Blobs do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fornece uma boa visão geral de como trabalhar com blobs e contêineres do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="38019-201">Ele deverá estar próximo à parte superior da lista de leitura quando você começar a trabalhar com o Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="38019-202">Etapa 2: carregar aplicativos e de tarefa e arquivos de dados </span><span class="sxs-lookup"><span data-stu-id="38019-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="38019-203">![Carregar arquivos de aplicativo e de entrada (dados) da tarefa nos contêineres][2]
</span><span class="sxs-lookup"><span data-stu-id="38019-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="38019-204">Na operação de upload do arquivo, *DotNetTutorial* primeiro define as coleções de caminhos de arquivo **application** e **input** como eles existem no computador local.</span><span class="sxs-lookup"><span data-stu-id="38019-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="38019-205">Em seguida, ele carrega esses arquivos nos contêineres que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="38019-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="38019-206">Há dois métodos no `Program.cs` que estão envolvidos no processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="38019-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="38019-207">`UploadFilesToContainerAsync`: esse método retorna uma coleção de objetos [ResourceFile][net_resourcefile] (discutidos abaixo) e internamente chama `UploadFileToContainerAsync` para carregar cada arquivo passado no parâmetro *filePaths*.</span><span class="sxs-lookup"><span data-stu-id="38019-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="38019-208">`UploadFileToContainerAsync`: é o método que realmente executa o upload do arquivo e cria os objetos [ResourceFile][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="38019-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="38019-209">Depois de carregar o arquivo, ele obtém uma assinatura de acesso compartilhado (SAS) para o arquivo e retorna um objeto ResourceFile que a representa.</span><span class="sxs-lookup"><span data-stu-id="38019-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="38019-210">As assinaturas de acesso compartilhado também são discutidas abaixo.</span><span class="sxs-lookup"><span data-stu-id="38019-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="38019-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="38019-211">ResourceFiles</span></span>
<span data-ttu-id="38019-212">O [ResourceFile][net_resourcefile] fornece tarefas no Lote com a URL para um arquivo no Armazenamento do Azure que é baixado para um nó de computação antes da execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="38019-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="38019-213">A propriedade [ResourceFile.BlobSource][net_resourcefile_blobsource] especifica a URL completa do arquivo como ela existe no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="38019-214">A URL também pode incluir uma assinatura de acesso compartilhado (SAS) que fornece acesso seguro ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="38019-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="38019-215">A maioria dos tipos de tarefas no .NET do Lote inclui uma propriedade *ResourceFiles* , incluindo:</span><span class="sxs-lookup"><span data-stu-id="38019-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="38019-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="38019-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="38019-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="38019-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="38019-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="38019-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="38019-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="38019-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="38019-220">O aplicativo de exemplo DotNetTutorial não usa os tipos de tarefa JobPreparationTask ou a JobReleaseTask, mas você pode ler mais sobre isso em [Executar tarefas de preparação e de conclusão de trabalhos em nós de computação do Lote do Azure](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="38019-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="38019-221">Assinatura de acesso compartilhado (SAS)</span><span class="sxs-lookup"><span data-stu-id="38019-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="38019-222">As assinaturas de acesso compartilhado são cadeias de caracteres que, quando incluídas como parte de uma URL, oferecem acesso seguro a contêineres e a blobs no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="38019-223">O aplicativo DotNetTutorial usa URLs de assinatura de acesso compartilhado de blob e de contêiner e demonstra como obter essas cadeias de caracteres de assinatura de acesso compartilhado do serviço de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="38019-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="38019-224">**Assinaturas de acesso compartilhado do Blob**: a StartTask do pool em DotNetTutorial usa assinaturas de acesso compartilhado de blob ao baixar os binários do aplicativo e os dados de entrada de arquivos de Armazenamento (confira a Etapa 3 abaixo).</span><span class="sxs-lookup"><span data-stu-id="38019-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="38019-225">O método `UploadFileToContainerAsync` no `Program.cs` do DotNetTutorial contém o código que obtém a assinatura de acesso compartilhado de cada blob.</span><span class="sxs-lookup"><span data-stu-id="38019-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="38019-226">Isso é feito chamando [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="38019-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="38019-227">**Assinaturas de acesso compartilhado do contêiner**: como cada tarefa conclui seu trabalho em nós de computação, ele carrega o arquivo de saída no contêiner *output* no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="38019-228">Para fazer isso, o TaskApplication usa uma assinatura de acesso compartilhado de contêiner que fornece acesso de gravação ao contêiner como parte do caminho ao carregar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="38019-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="38019-229">Você obtém a assinatura de acesso compartilhado do contêiner da mesma forma como obtém a assinatura de acesso compartilhado do blob.</span><span class="sxs-lookup"><span data-stu-id="38019-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="38019-230">No DotNetTutorial, você verá que o método auxiliar `GetContainerSasUrl` chama [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="38019-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="38019-231">Leia mais sobre como o TaskApplication usa a assinatura de acesso compartilhado do contêiner na “Etapa 6: Monitorar tarefas".</span><span class="sxs-lookup"><span data-stu-id="38019-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="38019-232">Confira a série de duas partes sobre as assinaturas de acesso compartilhado, [Parte 1: Compreendendo o modelo de assinatura de acesso compartilhado (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [Parte 2: Criar e usar uma assinatura de acesso compartilhado (SAS) com o armazenamento de Blobs](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), para saber mais sobre como fornecer acesso seguro aos dados em sua conta do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="38019-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="38019-233">Etapa 3: Criar pool do Lote</span><span class="sxs-lookup"><span data-stu-id="38019-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="38019-234">![Criar um pool do Lote][3]
</span><span class="sxs-lookup"><span data-stu-id="38019-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="38019-235">Um **pool** do Lote é uma coleção de nós de computação (máquinas virtuais) nos quais o Lote executa as tarefas de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="38019-236">Depois de carregar o aplicativo e os arquivos de dados para a conta de armazenamento com APIs do Armazenamento do Azure, o *DotNetTutorial* começa a fazer chamadas para o serviço Lote com APIs fornecidas pela biblioteca .NET do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="38019-237">O código cria primeiro um [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="38019-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="38019-238">Em seguida, o exemplo cria um pool de nós de computação na conta do Lote com uma chamada para `CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="38019-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="38019-239">`CreatePoolIfNotExistsAsync` usa o método [BatchClient.PoolOperations.CreatePool][net_pool_create] para criar um novo pool no serviço Lote:</span><span class="sxs-lookup"><span data-stu-id="38019-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="38019-240">Ao criar um pool com [CreatePool][net_pool_create], você especificará diversos parâmetros, como o número de nós de computação, o [tamanho dos nós](../cloud-services/cloud-services-sizes-specs.md) e o sistema operacional dos nós.</span><span class="sxs-lookup"><span data-stu-id="38019-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="38019-241">Em *DotNetTutorial*, usamos [CloudServiceConfiguration][net_cloudserviceconfiguration] para especificar o Windows Server 2012 R2 do [Serviços de Nuvem](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="38019-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="38019-242">Você também pode criar pools de nós de computação que são VMs (máquinas virtuais) do Azure especificando a [VirtualMachineConfiguration][net_virtualmachineconfiguration] para o pool.</span><span class="sxs-lookup"><span data-stu-id="38019-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="38019-243">Você pode criar um conjunto de nós de computação de VM de [imagens Linux](batch-linux-nodes.md) ou Windows.</span><span class="sxs-lookup"><span data-stu-id="38019-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="38019-244">A fonte para as imagens de VM pode ser:</span><span class="sxs-lookup"><span data-stu-id="38019-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="38019-245">O [Marketplace de Máquinas Virtuais do Azure][vm_marketplace], que fornece imagens de Windows e Linux prontas para uso.</span><span class="sxs-lookup"><span data-stu-id="38019-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="38019-246">Uma imagem personalizada preparada e fornecida por você.</span><span class="sxs-lookup"><span data-stu-id="38019-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="38019-247">Para obter mais detalhes sobre imagens personalizadas, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="38019-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38019-248">Você é cobrado pelos recursos de computação no Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="38019-249">Para minimizar os custos, você poderá diminuir `targetDedicatedComputeNodes` para 1 antes de executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="38019-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="38019-250">Junto com essas propriedades de nó físico, você também poderá especificar uma [StartTask][net_pool_starttask] para o pool.</span><span class="sxs-lookup"><span data-stu-id="38019-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="38019-251">StartTask é executado em cada nó quando o nó ingressa no pool e sempre que um nó é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="38019-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="38019-252">A StartTask é especialmente útil para instalar aplicativos em nós de computação antes da execução de tarefas.</span><span class="sxs-lookup"><span data-stu-id="38019-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="38019-253">Por exemplo, se suas tarefas processassem dados usando scripts Python, você poderia usar uma StartTask para instalar o Python nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="38019-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="38019-254">Neste aplicativo de exemplo, a StartTask copia os arquivos baixados do Armazenamento (especificados usando a propriedade [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles]) do diretório de trabalho StartTask para o diretório compartilhado que *todas* as tarefas em execução no nó podem acessar.</span><span class="sxs-lookup"><span data-stu-id="38019-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="38019-255">Essencialmente, isso copia `TaskApplication.exe` e suas dependências para um diretório compartilhado em cada nó à medida que o nó se une o pool para que qualquer tarefa executada no nó possa acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="38019-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="38019-256">O recurso **pacotes de aplicativos** do Lote do Azure fornece outra maneira de colocar seu aplicativo nos nós de computação em seu pool.</span><span class="sxs-lookup"><span data-stu-id="38019-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="38019-257">Veja [Implantar aplicativos em nós de computação com pacotes de aplicativos do Lote](batch-application-packages.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="38019-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="38019-258">Também podemos notar no trecho de código acima o uso de duas variáveis de ambiente na propriedade *CommandLine* da StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` e `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="38019-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="38019-259">Cada nó de computação em um pool do Lote é configurado automaticamente com diversas variáveis de ambiente específicas para o Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="38019-260">Qualquer processo executado por uma tarefa tem acesso a essas variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="38019-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="38019-261">Para saber mais sobre as variáveis de ambiente disponíveis em nós de computação em um pool do Lote, além de informações sobre os diretórios de trabalho da tarefa, confira as seções [Configurações de ambiente para tarefas](batch-api-basics.md#environment-settings-for-tasks) e [Arquivos e diretórios](batch-api-basics.md#files-and-directories) na [Visão geral do recurso Lote para desenvolvedores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="38019-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="38019-262">Etapa 4: Criar o trabalho do Lote</span><span class="sxs-lookup"><span data-stu-id="38019-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="38019-263">![Criar trabalho do Lote][4]</span><span class="sxs-lookup"><span data-stu-id="38019-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="38019-264">Um **trabalho** do Lote é uma coleção de tarefas associadas a um pool de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="38019-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="38019-265">As tarefas em um trabalho são executadas nos nós de computação do pool associado.</span><span class="sxs-lookup"><span data-stu-id="38019-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="38019-266">Você pode usar um trabalho não apenas para organizar e acompanhar tarefas relacionadas de cargas de trabalho, mas também pode impor certas restrições, como o tempo máximo de execução do trabalho (e, por extensão, de suas tarefas), além da prioridade do trabalho em relação a outros trabalhos na conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="38019-267">No entanto, neste exemplo, o trabalho só estará associado ao pool criado na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="38019-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="38019-268">Nenhuma propriedade adicional será configurada.</span><span class="sxs-lookup"><span data-stu-id="38019-268">No additional properties are configured.</span></span>

<span data-ttu-id="38019-269">Todos os trabalhos do Lotes estão associados a um pool específico.</span><span class="sxs-lookup"><span data-stu-id="38019-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="38019-270">Essa associação indica em quais nós as tarefas do trabalho serão executadas.</span><span class="sxs-lookup"><span data-stu-id="38019-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="38019-271">Especifique isso usando a propriedade [CloudJob.PoolInformation][net_job_poolinfo], como mostrado no trecho de código abaixo.</span><span class="sxs-lookup"><span data-stu-id="38019-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="38019-272">Agora que um trabalho foi criado, as tarefas serão adicionadas para a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="38019-273">Etapa 5: Adicionar tarefas ao trabalho</span><span class="sxs-lookup"><span data-stu-id="38019-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="38019-274">![Adicionar tarefas ao trabalho][5]</span><span class="sxs-lookup"><span data-stu-id="38019-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="38019-275">
*(1) As tarefas são adicionadas ao trabalho, (2) as tarefas são agendadas para execução em nós e (3) as tarefas baixam os arquivos de dados para processamento*</span><span class="sxs-lookup"><span data-stu-id="38019-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="38019-276">As **tarefas** do Lote são as unidades individuais de trabalho executadas nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="38019-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="38019-277">Uma tarefa tem uma linha de comando e executa os scripts ou os executáveis especificados na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="38019-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="38019-278">Para realmente executar o trabalho, as tarefas devem ser adicionadas a um trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="38019-279">Cada [CloudTask][net_task] é configurada usando uma propriedade de linha de comando e [ResourceFiles][net_task_resourcefiles] (assim como acontece com a StartTask do pool) que a tarefa baixa para o nó antes de a linha de comando ser executada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="38019-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="38019-280">No projeto de exemplo *DotNetTutorial* , cada tarefa processa apenas um arquivo.</span><span class="sxs-lookup"><span data-stu-id="38019-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="38019-281">Portanto, sua coleção ResourceFiles contém um único elemento.</span><span class="sxs-lookup"><span data-stu-id="38019-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="38019-282">Quando acessarem variáveis de ambiente como `%AZ_BATCH_NODE_SHARED_DIR%` ou executam um aplicativo não encontrado no `PATH` do nó, as linhas de comando da tarefa deverão ser prefixadas com `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="38019-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="38019-283">Isso executará explicitamente o interpretador de comandos e o instruirá a terminar após a execução do comando.</span><span class="sxs-lookup"><span data-stu-id="38019-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="38019-284">Esse requisito será desnecessário se suas tarefas executarem um aplicativo no `PATH` do nó (como *robocopy.exe* ou *powershell.exe*) e se nenhuma variável de ambiente for usada.</span><span class="sxs-lookup"><span data-stu-id="38019-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="38019-285">No loop `foreach` no trecho de código acima, você verá que a linha de comando da tarefa é construída de forma que três argumentos de linha de comando sejam passados para *TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="38019-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="38019-286">O **primeiro argumento** é o caminho do arquivo a ser processado.</span><span class="sxs-lookup"><span data-stu-id="38019-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="38019-287">Esse é o caminho local para o arquivo conforme ele existe no nó.</span><span class="sxs-lookup"><span data-stu-id="38019-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="38019-288">Quando o objeto ResourceFile em `UploadFileToContainerAsync` foi criado acima, o nome do arquivo foi usado para essa propriedade (como um parâmetro para o construtor ResourceFile).</span><span class="sxs-lookup"><span data-stu-id="38019-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="38019-289">Isso indica que o arquivo pode ser encontrado no mesmo diretório que *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="38019-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="38019-290">O **segundo argumento** especifica que as *N* palavras principais devem ser gravadas no arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="38019-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="38019-291">No exemplo, isso é codificado para que as três palavras principais sejam gravadas no arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="38019-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="38019-292">O **terceiro argumento** é a assinatura de acesso compartilhado (SAS) que fornece acesso de gravação ao contêiner **output** no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="38019-293">*TaskApplication.exe* usa essa URL de assinatura de acesso compartilhado quando carrega o arquivo de saída no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="38019-294">Você pode encontrar o código para isso no método `UploadFileToContainer` do arquivo `Program.cs` do projeto TaskApplication:</span><span class="sxs-lookup"><span data-stu-id="38019-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="38019-295">Etapa 6: Monitorar tarefas</span><span class="sxs-lookup"><span data-stu-id="38019-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="38019-296">![Monitorar tarefas][6]</span><span class="sxs-lookup"><span data-stu-id="38019-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="38019-297">
*O aplicativo cliente (1) monitora as tarefas para a conclusão e o status de êxito e (2) os dados resultantes do upload de tarefas para o Armazenamento do Azure*</span><span class="sxs-lookup"><span data-stu-id="38019-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="38019-298">Quando as tarefas são adicionadas a um trabalho, são automaticamente enfileiradas e agendadas para execução em nós de computação no pool associado ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="38019-299">Com base nas configurações especificadas, o Lote manipula o enfileiramento, o agendamento, a repetição de todas as tarefas e outras obrigações de administração de tarefas para você.</span><span class="sxs-lookup"><span data-stu-id="38019-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="38019-300">Há muitas abordagens para o monitoramento da execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="38019-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="38019-301">O DotNetTutorial mostra um exemplo simples que relata apenas a conclusão e a falha de tarefas ou os estados de êxito.</span><span class="sxs-lookup"><span data-stu-id="38019-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="38019-302">No método `MonitorTasks` no `Program.cs` do DotNetTutorial, há três conceitos do .NET do Lote que garantem a discussão.</span><span class="sxs-lookup"><span data-stu-id="38019-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="38019-303">Eles são listados na ordem em que aparecem:</span><span class="sxs-lookup"><span data-stu-id="38019-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="38019-304">**ODATADetailLevel**: a especificação de um [ODATADetailLevel][net_odatadetaillevel] na lista de operações (como a obtenção de uma lista de tarefas do trabalho) é essencial para garantir o desempenho do aplicativo do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="38019-305">Adicione [Consultar o serviço Lote do Azure com eficiência](batch-efficient-list-queries.md) à sua lista de leitura se você planejar fazer qualquer tipo de monitoramento de status em seus aplicativos do Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="38019-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] fornece aplicativos .NET do Lote com utilitários auxiliares para monitorar estados da tarefa.</span><span class="sxs-lookup"><span data-stu-id="38019-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="38019-307">Em `MonitorTasks`, *DotNetTutorial* aguarda que todas as tarefas alcancem [TaskState.Completed][net_taskstate] dentro de um limite de tempo.</span><span class="sxs-lookup"><span data-stu-id="38019-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="38019-308">Em seguida, ele conclui o trabalho.</span><span class="sxs-lookup"><span data-stu-id="38019-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="38019-309">**TerminateJobAsync**: o encerramento de um trabalho com [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (ou o bloqueio de JobOperations.TerminateJob) marca esse trabalho como concluído.</span><span class="sxs-lookup"><span data-stu-id="38019-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="38019-310">Será essencial fazer isso se sua solução do Lote usar um [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="38019-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="38019-311">Esse é um tipo especial de tarefa, descrita em [Tarefas de preparação e de conclusão do trabalho](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="38019-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="38019-312">O método `MonitorTasks` no `Program.cs` do *DotNetTutorial* aparece abaixo:</span><span class="sxs-lookup"><span data-stu-id="38019-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="38019-313">Etapa 7: Baixar a saída da tarefa</span><span class="sxs-lookup"><span data-stu-id="38019-313">Step 7: Download task output</span></span>
<span data-ttu-id="38019-314">![Baixar a saída da tarefa do Armazenamento][7]</span><span class="sxs-lookup"><span data-stu-id="38019-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="38019-315">Agora que o trabalho foi concluído, a saída das tarefas pode ser baixada do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38019-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="38019-316">Isso é feito com uma chamada a `DownloadBlobsFromContainerAsync` no `Program.cs` do *DotNetTutorial*:</span><span class="sxs-lookup"><span data-stu-id="38019-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="38019-317">A chamada a `DownloadBlobsFromContainerAsync` no aplicativo *DotNetTutorial* especifica que os arquivos devem ser baixados para a pasta `%TEMP%`.</span><span class="sxs-lookup"><span data-stu-id="38019-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="38019-318">Fique à vontade para modificar esse local de saída.</span><span class="sxs-lookup"><span data-stu-id="38019-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="38019-319">Etapa 8: Excluir contêineres</span><span class="sxs-lookup"><span data-stu-id="38019-319">Step 8: Delete containers</span></span>
<span data-ttu-id="38019-320">Como você é cobrado pelos dados que residem no Armazenamento do Azure, sempre será uma boa ideia remover os blobs que não sejam mais necessários para seus trabalhos em lotes.</span><span class="sxs-lookup"><span data-stu-id="38019-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="38019-321">No `Program.cs` do DotNetTutorial, isso é feito com três chamadas para o método auxiliar `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="38019-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="38019-322">O próprio método simplesmente obtém uma referência para o contêiner e, em seguida, chama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="38019-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="38019-323">Etapa 9: excluir o trabalho e o pool</span><span class="sxs-lookup"><span data-stu-id="38019-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="38019-324">Na etapa final, é solicitado que você exclua o trabalho e o pool criados pelo aplicativo DotNetTutorial.</span><span class="sxs-lookup"><span data-stu-id="38019-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="38019-325">Embora você não seja cobrado pelos trabalhos e pelas tarefas, *será* cobrado pelos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="38019-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="38019-326">Portanto, recomendamos que você aloque os nós conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="38019-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="38019-327">A exclusão de pools não utilizados pode fazer parte de seu processo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="38019-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="38019-328">As [JobOperations][net_joboperations] e as [PoolOperations][net_pooloperations] do BatchClient têm métodos de exclusão correspondentes, chamados se o usuário confirmar a exclusão:</span><span class="sxs-lookup"><span data-stu-id="38019-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="38019-329">Tenha em mente que você será cobrado pelos recursos de computação, a exclusão dos pools não utilizados reduzirá o custo.</span><span class="sxs-lookup"><span data-stu-id="38019-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="38019-330">Além disso, lembre-se de que a exclusão de um pool exclui todos os nós de computação no pool e que os dados em nós não poderão ser recuperados depois que o pool for excluído.</span><span class="sxs-lookup"><span data-stu-id="38019-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="38019-331">Executar o exemplo *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="38019-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="38019-332">Quando você executar o aplicativo de exemplo, a saída do console será semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="38019-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="38019-333">Durante a execução, você terá uma pausa em `Awaiting task completion, timeout in 00:30:00...` enquanto os nós de computação do pool são iniciados.</span><span class="sxs-lookup"><span data-stu-id="38019-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="38019-334">Use o [Portal do Azure][azure_portal] para monitorar o pool, os nós de computação, o trabalho e as tarefas durante e após a execução.</span><span class="sxs-lookup"><span data-stu-id="38019-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="38019-335">Use o [Portal do Azure][azure_portal] ou o [Gerenciador de Armazenamento do Azure][storage_explorers] para exibir os recursos do Armazenamento (contêineres e blobs) criados pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38019-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="38019-336">O tempo de execução típico é de **aproximadamente 5 minutos** ao executar o aplicativo em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="38019-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="38019-337">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38019-337">Next steps</span></span>
<span data-ttu-id="38019-338">Fique à vontade para fazer alterações em *DotNetTutorial* e em *TaskApplication* para fazer experiências com cenários de computação diferentes.</span><span class="sxs-lookup"><span data-stu-id="38019-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="38019-339">Por exemplo, tente adicionar um atraso de execução para *TaskApplication*, como com [Thread.Sleep][net_thread_sleep], para simular tarefas demoradas e para monitorá-las no portal.</span><span class="sxs-lookup"><span data-stu-id="38019-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="38019-340">Tente adicionar mais tarefas ou ajustar o número de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="38019-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="38019-341">Adicione lógica para verificar e permitir o uso de um pool existente para acelerar o tempo de execução (*dica*: confira `ArticleHelpers.cs` no projeto [Microsoft.Azure.Batch.Samples.Common][github_samples_common] em [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="38019-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="38019-342">Agora que você está familiarizado com o fluxo de trabalho básico de uma solução do Lote, é hora de se aprofundar nos recursos adicionais do serviço Lote.</span><span class="sxs-lookup"><span data-stu-id="38019-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="38019-343">Examine o artigo [Visão geral dos recursos do Lote do Azure](batch-api-basics.md) , que é recomendável se ainda não estiver familiarizado com o serviço.</span><span class="sxs-lookup"><span data-stu-id="38019-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="38019-344">Comece pelos outros artigos de desenvolvimento do Lote em **Desenvolvimento detalhado** no [Roteiro de aprendizagem do Lote][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="38019-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="38019-345">Confira uma implementação diferente do processamento da carga de trabalho "N palavras principais" usando o Lote no exemplo [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="38019-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="38019-346">Confira as [notas de versão](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) do Batch .NET para conhecer as alterações mais recentes na biblioteca.</span><span class="sxs-lookup"><span data-stu-id="38019-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Criar contêineres no Armazenamento do Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Carregar arquivos de aplicativo e de entrada (dados) da tarefa nos contêineres"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Criar pool do Lote"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Criar trabalho em lotes"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Adicionar tarefas ao trabalho"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorar tarefas"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Baixar a saída da tarefa do Armazenamento"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Fluxo de trabalho da solução do Lote (diagrama completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenciais do Lote no Portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenciais do Armazenamento no Portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Fluxo de trabalho da solução do Lote (diagrama mínimo)"
