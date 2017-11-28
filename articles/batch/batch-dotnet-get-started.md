---
title: "aaaTutorial - biblioteca de cliente do uso Olá lote do Azure para .NET | Microsoft Docs"
description: "Aprenda os conceitos básicos de saudação do lote do Azure e criar uma solução simple usando o .NET."
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
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="6de11-103">Começar a criar soluções com biblioteca de cliente Olá Batch para .NET</span><span class="sxs-lookup"><span data-stu-id="6de11-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6de11-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6de11-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="6de11-105">Python</span><span class="sxs-lookup"><span data-stu-id="6de11-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="6de11-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="6de11-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="6de11-107">Aprenda noções básicas de saudação do [do Azure Batch] [ azure_batch] e hello [Batch .NET] [ net_api] biblioteca neste artigo discutir um c# exemplo aplicativo passo etapa.</span><span class="sxs-lookup"><span data-stu-id="6de11-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="6de11-108">Vamos examinar como o aplicativo de exemplo hello aproveita tooprocess de serviço de lote Olá uma carga de trabalho paralela em nuvem hello e como ele interage com [armazenamento do Azure](../storage/common/storage-introduction.md) para preparação de arquivo e de recuperação.</span><span class="sxs-lookup"><span data-stu-id="6de11-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="6de11-109">Você vai aprender um fluxo de trabalho de aplicativo comuns em lotes e obter uma compreensão básica de Olá principais componentes do lote, como trabalhos, tarefas, pools de e nós de computação.</span><span class="sxs-lookup"><span data-stu-id="6de11-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="6de11-110">![Fluxo de trabalho da solução do Lote (básico)][11]</span><span class="sxs-lookup"><span data-stu-id="6de11-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="6de11-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6de11-111">Prerequisites</span></span>
<span data-ttu-id="6de11-112">Este artigo pressupõe que você tenha um conhecimento prático do C# e do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6de11-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="6de11-113">Ele também pressupõe que você é capaz de toosatisfy Olá conta criação requisitos especificados abaixo para o Azure e Olá lote e serviços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="6de11-114">Contas</span><span class="sxs-lookup"><span data-stu-id="6de11-114">Accounts</span></span>
* <span data-ttu-id="6de11-115">**Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="6de11-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="6de11-116">**Conta do Lote**: quando você tiver uma assinatura do Azure, [crie uma conta do Lote do Azure](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="6de11-117">**Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6de11-118">Em lotes atualmente oferece suporte a *somente* Olá **geral** tipo de conta de armazenamento, conforme descrito na etapa &#5; [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) no [sobre o Azure contas de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="6de11-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6de11-119">Visual Studio</span></span>
<span data-ttu-id="6de11-120">Você deve ter **Visual Studio 2015 ou mais recente** projeto de exemplo hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="6de11-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="6de11-121">Você pode encontrar versões de avaliação e gratuitas do Visual Studio no hello [visão geral dos produtos do Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="6de11-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="6de11-122">*DotNetTutorial* </span><span class="sxs-lookup"><span data-stu-id="6de11-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="6de11-123">Olá [DotNetTutorial] [ github_dotnettutorial] exemplo é uma saudação muitos exemplos de código do lote encontrados no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="6de11-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="6de11-124">Você pode baixar todos os exemplos de saudação clicando **Clone ou download > baixar ZIP** na home page do repositório de hello, ou clicando em Olá [azure lote-exemplos master.zip] [ github_samples_zip]link de download direto.</span><span class="sxs-lookup"><span data-stu-id="6de11-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="6de11-125">Depois de extrair o conteúdo de saudação do arquivo ZIP de Olá, você pode encontrar solução Olá Olá pasta a seguir:</span><span class="sxs-lookup"><span data-stu-id="6de11-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="6de11-126">Gerenciador do Lote do Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="6de11-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="6de11-127">Olá [Gerenciador de lote do Azure] [ github_batchexplorer] é um utilitário livre que está incluído no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="6de11-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="6de11-128">Ao toocomplete não é necessária neste tutorial, ele pode ser útil ao desenvolvimento e depuração de suas soluções de lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="6de11-129">Visão geral do projeto de exemplo DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="6de11-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="6de11-130">Olá *DotNetTutorial* código de exemplo é uma solução do Visual Studio que consiste em dois projetos: **DotNetTutorial** e **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="6de11-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="6de11-131">**DotNetTutorial** é o aplicativo cliente hello que interage com tooexecute de serviços de lote e armazenamento Olá uma carga de trabalho paralela em nós de computação (máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="6de11-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="6de11-132">O DotNetTutorial é executado em sua estação de trabalho local.</span><span class="sxs-lookup"><span data-stu-id="6de11-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="6de11-133">**TaskApplication** é Olá programa que é executado em nós de computação no trabalho do Azure tooperform Olá real.</span><span class="sxs-lookup"><span data-stu-id="6de11-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="6de11-134">No exemplo hello, `TaskApplication.exe` analisa Olá texto em um arquivo baixado do armazenamento do Azure (arquivo de entrada hello).</span><span class="sxs-lookup"><span data-stu-id="6de11-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="6de11-135">Em seguida, ele produz um arquivo de texto (arquivo de saída de hello) que contém uma lista de palavras de três principais Olá que aparecem no arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="6de11-136">Depois que ele cria o arquivo de saída de hello, TaskApplication carrega Olá arquivo tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="6de11-137">Isso torna aplicativo de cliente toohello disponível para download.</span><span class="sxs-lookup"><span data-stu-id="6de11-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="6de11-138">TaskApplication é executado em paralelo em vários nós de computação Olá serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="6de11-139">Olá, diagrama a seguir ilustra operações principais de saudação que são executadas pelo aplicativo de cliente hello, *DotNetTutorial*e o aplicativo hello executado pelas tarefas de saudação *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="6de11-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="6de11-140">Esse fluxo de trabalho básico é típico de muitas soluções de computação criadas com o Lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="6de11-141">Embora não demonstra todos os recursos disponíveis no serviço de lote de hello, quase todos os cenários de lote incluem partes desse fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6de11-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="6de11-142">![Fluxo de trabalho de exemplo do Lote][8]</span><span class="sxs-lookup"><span data-stu-id="6de11-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="6de11-143">**Etapa 1.**</span><span class="sxs-lookup"><span data-stu-id="6de11-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="6de11-144">Crie **contêineres** no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="6de11-145">
[**Etapa 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="6de11-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="6de11-146">Arquivos de aplicativo de tarefa de carregamento e toocontainers de arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="6de11-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="6de11-147">
[**Etapa 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="6de11-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="6de11-148">Criar um **pool** do Lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="6de11-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="6de11-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="6de11-150">Olá pool **StartTask** downloads Olá tarefa arquivos binários (TaskApplication) toonodes ao entrarem pool hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="6de11-151">
[**Etapa 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="6de11-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="6de11-152">Crie um **trabalho** do Lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="6de11-153">
[**Etapa 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="6de11-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="6de11-154">Adicionar **tarefas** toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="6de11-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="6de11-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="6de11-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="6de11-156">tarefas de saudação são agendado tooexecute em nós.</span><span class="sxs-lookup"><span data-stu-id="6de11-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="6de11-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="6de11-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="6de11-158">Cada tarefa baixa seus dados de entrada do Armazenamento do Azure e então inicia a execução.</span><span class="sxs-lookup"><span data-stu-id="6de11-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="6de11-159">
[**Etapa 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="6de11-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="6de11-160">Monitore as tarefas.</span><span class="sxs-lookup"><span data-stu-id="6de11-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="6de11-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="6de11-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="6de11-162">Como as tarefas são concluídas, carregar seu dados de saída tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="6de11-163">
[**Etapa 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="6de11-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="6de11-164">Baixe a saída da tarefa do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-164">Download task output from Storage.</span></span>

<span data-ttu-id="6de11-165">Conforme mencionado, não todas as soluções em lotes executa essas etapas e podem incluir muitas, mas Olá *DotNetTutorial* aplicativo de exemplo demonstra processos comuns encontrados em uma solução de lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="6de11-166">Criar hello *DotNetTutorial* projeto de exemplo</span><span class="sxs-lookup"><span data-stu-id="6de11-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="6de11-167">Antes de executar com êxito exemplo hello, você deve especificar credenciais de conta de armazenamento e de lote no hello *DotNetTutorial* do projeto `Program.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="6de11-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="6de11-168">Se você não tiver feito isso, abra a solução Olá no Visual Studio clicando duas vezes Olá `DotNetTutorial.sln` arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="6de11-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="6de11-169">Ou abri-lo de dentro do Visual Studio usando Olá **arquivo > Abrir > projeto/solução** menu.</span><span class="sxs-lookup"><span data-stu-id="6de11-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="6de11-170">Abra `Program.cs` em Olá *DotNetTutorial* projeto.</span><span class="sxs-lookup"><span data-stu-id="6de11-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="6de11-171">Adicione as credenciais conforme especificado superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="6de11-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="6de11-172">Conforme mencionado acima, você deve especificar atualmente credenciais Olá para um **geral** conta de armazenamento no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="6de11-173">Seus aplicativos de lote usam armazenamento de blob em Olá **geral** conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="6de11-174">Não especifique credenciais Olá para uma conta de armazenamento que foi criado selecionando Olá *armazenamento de Blob* tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="6de11-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="6de11-175">Você pode encontrar suas credenciais de conta de lote e armazenamento na folha da conta de saudação de cada serviço em Olá [portal do Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="6de11-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="6de11-176">![As credenciais no portal de saudação do lote][9]
![credenciais de armazenamento no portal de saudação][10]</span><span class="sxs-lookup"><span data-stu-id="6de11-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="6de11-177">Agora que você atualizou o projeto Olá com suas credenciais, clique com botão direito solução Olá no Gerenciador de soluções e clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="6de11-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="6de11-178">Confirme restauração de saudação de todos os pacotes NuGet, se você for solicitado.</span><span class="sxs-lookup"><span data-stu-id="6de11-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="6de11-179">Se os pacotes do NuGet Olá não são restaurados automaticamente ou se você encontrar erros sobre os pacotes de saudação de toorestore uma falha, certifique-se de que você tenha Olá [NuGet Package Manager] [ nuget_packagemgr] instalado.</span><span class="sxs-lookup"><span data-stu-id="6de11-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="6de11-180">Em seguida, habilite Olá de download de pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="6de11-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="6de11-181">Consulte [habilitar pacote restaurar durante a compilação] [ nuget_restore] tooenable download do pacote.</span><span class="sxs-lookup"><span data-stu-id="6de11-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="6de11-182">Olá seções a seguir, é dividir o aplicativo de exemplo hello em etapas de saudação que ela seja executada tooprocess uma carga de trabalho no serviço de lote de saudação e discutem em detalhes essas etapas.</span><span class="sxs-lookup"><span data-stu-id="6de11-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="6de11-183">Recomendamos que você toorefer toohello abrir solução no Visual Studio enquanto você trabalha até rest Olá deste artigo, pois nem toda linha de código no exemplo hello é discutida.</span><span class="sxs-lookup"><span data-stu-id="6de11-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="6de11-184">Navegue toohello superior de saudação `MainAsync` método hello *DotNetTutorial* do projeto `Program.cs` arquivo toostart com a etapa 1.</span><span class="sxs-lookup"><span data-stu-id="6de11-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="6de11-185">Cada etapa abaixo e aproximadamente chamadas de maneira Olá progressão de método em `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="6de11-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="6de11-186">Etapa 1: Criar contêineres do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="6de11-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="6de11-187">![Criar contêineres no Armazenamento do Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="6de11-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="6de11-188">O Lote inclui suporte interno para a interação com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="6de11-189">Contêineres em sua conta de armazenamento fornecerá arquivos Olá necessários para tarefas de saudação que são executados em sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="6de11-190">contêineres de saudação também fornecem um lugar toostore Olá dados da saída tarefas Olá produzem.</span><span class="sxs-lookup"><span data-stu-id="6de11-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="6de11-191">primeiro Olá Olá *DotNetTutorial* aplicativo cliente é criar três contêineres [armazenamento de BLOBs do Azure](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="6de11-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="6de11-192">**aplicativo**: este contêiner armazena aplicativo hello executando tarefas hello, bem como qualquer uma de suas dependências, como DLLs.</span><span class="sxs-lookup"><span data-stu-id="6de11-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="6de11-193">**entrada**: tarefas baixarão tooprocess de arquivos de dados de saudação do hello *entrada* contêiner.</span><span class="sxs-lookup"><span data-stu-id="6de11-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="6de11-194">**saída**: quando tarefas concluir o processamento do arquivo de entrada, eles carregará Olá resultados toohello *saída* contêiner.</span><span class="sxs-lookup"><span data-stu-id="6de11-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="6de11-195">Em ordem toointeract com um armazenamento de conta e criar contêineres, usamos Olá [biblioteca de cliente de armazenamento do Azure para .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="6de11-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="6de11-196">Podemos criar uma conta de toohello de referência com [CloudStorageAccount][net_cloudstorageaccount]e do que criar um [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="6de11-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="6de11-197">Usamos Olá `blobClient` referência em todo o aplicativo hello e passá-lo como um parâmetro tooseveral métodos.</span><span class="sxs-lookup"><span data-stu-id="6de11-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="6de11-198">É um exemplo no bloco de código Olá que segue imediatamente Olá acima, onde podemos chamar `CreateContainerIfNotExistAsync` tooactually criar contêineres de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
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

<span data-ttu-id="6de11-199">Depois que criar contêineres de hello, aplicativo hello agora pode carregar arquivos de saudação que serão usados pelas tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="6de11-200">[Como toouse armazenamento de BLOBs no .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fornece uma boa visão geral de como trabalhar com contêineres de armazenamento do Azure e blobs.</span><span class="sxs-lookup"><span data-stu-id="6de11-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="6de11-201">Como começar a trabalhar com o lote, ele deve ser superior Olá da sua lista de leitura.</span><span class="sxs-lookup"><span data-stu-id="6de11-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="6de11-202">Etapa 2: carregar aplicativos e de tarefa e arquivos de dados </span><span class="sxs-lookup"><span data-stu-id="6de11-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="6de11-203">![Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)][2]
</span><span class="sxs-lookup"><span data-stu-id="6de11-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="6de11-204">Operação, de carregamento no arquivo hello *DotNetTutorial* primeiro define coleções de **aplicativo** e **entrada** caminhos de arquivo que existem no computador local hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="6de11-205">Em seguida, ele carrega esses contêineres de toohello de arquivos que você criou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="6de11-206">Há dois métodos em `Program.cs` que estão envolvidos no processo de carregamento de saudação:</span><span class="sxs-lookup"><span data-stu-id="6de11-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="6de11-207">`UploadFilesToContainerAsync`: Esse método retorna uma coleção de [ResourceFile] [ net_resourcefile] objetos (abordados abaixo) e internamente chamadas `UploadFileToContainerAsync` tooupload cada arquivo que é passado Olá *filePaths* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6de11-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="6de11-208">`UploadFileToContainerAsync`: Este é o método hello que realmente executa o carregamento do arquivo hello e cria Olá [ResourceFile] [ net_resourcefile] objetos.</span><span class="sxs-lookup"><span data-stu-id="6de11-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="6de11-209">Depois de carregar o arquivo hello, ele obtém uma assinatura de acesso compartilhado (SAS) para o arquivo hello e retorna um objeto de ResourceFile que o representa.</span><span class="sxs-lookup"><span data-stu-id="6de11-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="6de11-210">As assinaturas de acesso compartilhado também são discutidas abaixo.</span><span class="sxs-lookup"><span data-stu-id="6de11-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="6de11-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="6de11-211">ResourceFiles</span></span>
<span data-ttu-id="6de11-212">Um [ResourceFile] [ net_resourcefile] fornece tarefas em lote com o arquivo de tooa URL Olá no armazenamento do Azure que é baixado tooa nó de computação para que essa tarefa seja executada.</span><span class="sxs-lookup"><span data-stu-id="6de11-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="6de11-213">Olá [ResourceFile.BlobSource] [ net_resourcefile_blobsource] propriedade especifica a URL completa do arquivo Olá Olá conforme ela existe no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="6de11-214">Olá URL também pode incluir uma assinatura de acesso compartilhado (SAS) que fornece acesso seguro toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="6de11-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="6de11-215">A maioria dos tipos de tarefas no .NET do Lote inclui uma propriedade *ResourceFiles* , incluindo:</span><span class="sxs-lookup"><span data-stu-id="6de11-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="6de11-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="6de11-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="6de11-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="6de11-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="6de11-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="6de11-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="6de11-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="6de11-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="6de11-220">Olá DotNetTutorial aplicativo de exemplo não usa Olá JobPreparationTask ou tipos de tarefa JobReleaseTask, mas você pode ler mais sobre eles em [nós de computação de tarefas de preparação e conclusão de trabalho de execução em lote do Azure](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="6de11-221">Assinatura de acesso compartilhado (SAS)</span><span class="sxs-lookup"><span data-stu-id="6de11-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="6de11-222">Acesso compartilhado, as assinaturas são cadeias de caracteres que, quando incluído como parte de uma URL — forneça acesso seguro toocontainers e blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="6de11-223">Olá DotNetTutorial aplicativo usa ambos os BLOBs e contêiner compartilhadas URLs de assinatura de acesso e demonstra como tooobtain esses compartilhado acessar cadeias de caracteres de assinatura de saudação serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="6de11-224">**Assinaturas de acesso compartilhado de blob**: StartTask do pool de saudação em DotNetTutorial usa assinaturas de acesso compartilhado de blob ao baixar arquivos de dados de entrada e binários do aplicativo hello do armazenamento (consulte a etapa 3 abaixo).</span><span class="sxs-lookup"><span data-stu-id="6de11-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="6de11-225">Olá `UploadFileToContainerAsync` do DotNetTutorial método `Program.cs` contém código Olá que obtém a assinatura de acesso compartilhado de cada blob.</span><span class="sxs-lookup"><span data-stu-id="6de11-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="6de11-226">Isso é feito chamando [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="6de11-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="6de11-227">**Assinaturas de acesso compartilhado do contêiner**: como cada tarefa termina o trabalho no nó de computação hello, ele carrega sua toohello do arquivo de saída *saída* contêiner no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="6de11-228">toodo assim, TaskApplication usa uma assinatura de acesso compartilhado do contêiner que fornece acesso de gravação toohello contêiner como parte do caminho de saudação quando ele carrega o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="6de11-229">Obter assinatura de acesso compartilhado do contêiner Olá é feita de maneira semelhante, como quando o blob de saudação obter assinatura de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="6de11-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="6de11-230">DotNetTutorial, você encontrará esse Olá `GetContainerSasUrl` chamadas de método auxiliar [GetSharedAccessSignature] [ net_sas_container] toodo para.</span><span class="sxs-lookup"><span data-stu-id="6de11-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="6de11-231">Você poderá ler mais sobre como TaskApplication usa o contêiner de saudação compartilhado assinatura de acesso na "etapa 6: monitorar tarefas."</span><span class="sxs-lookup"><span data-stu-id="6de11-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="6de11-232">Check-out da série de duas partes da saudação em assinaturas de acesso compartilhado, [parte 1: Olá Noções básicas sobre compartilhado modelo de assinatura (SAS) de acesso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: criar e usar uma assinatura de acesso compartilhado (SAS) com o armazenamento de Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn mais sobre como fornecer acesso seguro toodata na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="6de11-233">Etapa 3: Criar pool do Lote</span><span class="sxs-lookup"><span data-stu-id="6de11-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="6de11-234">![Criar um pool do Lote][3]
</span><span class="sxs-lookup"><span data-stu-id="6de11-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="6de11-235">Um **pool** do Lote é uma coleção de nós de computação (máquinas virtuais) nos quais o Lote executa as tarefas de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="6de11-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="6de11-236">Depois de carregar o aplicativo hello e arquivos de dados toohello conta de armazenamento com APIs de armazenamento do Azure, *DotNetTutorial* começa a fazer chamadas toohello o serviço de lote com APIs fornecidas pela biblioteca de saudação do .NET em lotes.</span><span class="sxs-lookup"><span data-stu-id="6de11-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="6de11-237">Olá código cria primeiro um [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="6de11-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="6de11-238">Em seguida, exemplo hello cria um conjunto de nós de computação na conta do lote Olá com uma chamada muito`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="6de11-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="6de11-239">`CreatePoolIfNotExistsAsync`Olá usa [BatchClient.PoolOperations.CreatePool] [ net_pool_create] método toocreate um novo pool de saudação serviço de lote:</span><span class="sxs-lookup"><span data-stu-id="6de11-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="6de11-240">Quando você cria um pool com [CreatePool][net_pool_create], você especificar vários parâmetros, como número de saudação de nós de computação, hello [tamanho de nós Olá](../cloud-services/cloud-services-sizes-specs.md), e Olá operacional de nós sistema.</span><span class="sxs-lookup"><span data-stu-id="6de11-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="6de11-241">Em *DotNetTutorial*, usamos [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 de [serviços de nuvem](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="6de11-242">Você também pode criar pools de nós de computação que são máquinas virtuais (VMs) Azure especificando Olá [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] para o pool.</span><span class="sxs-lookup"><span data-stu-id="6de11-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="6de11-243">Você pode criar um conjunto de nós de computação de VM de [imagens Linux](batch-linux-nodes.md) ou Windows.</span><span class="sxs-lookup"><span data-stu-id="6de11-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="6de11-244">fonte de saudação para as imagens VM pode ser:</span><span class="sxs-lookup"><span data-stu-id="6de11-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="6de11-245">Olá [Marketplace de máquinas virtuais do Azure][vm_marketplace], que fornece imagens do Windows e Linux que estão prontos para uso.</span><span class="sxs-lookup"><span data-stu-id="6de11-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="6de11-246">Uma imagem personalizada preparada e fornecida por você.</span><span class="sxs-lookup"><span data-stu-id="6de11-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="6de11-247">Para obter mais detalhes sobre imagens personalizadas, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="6de11-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6de11-248">Você é cobrado pelos recursos de computação no Lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="6de11-249">toominimize custos, você pode reduzir `targetDedicatedComputeNodes` too1 antes de executar o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="6de11-250">Com essas propriedades de nó físico, você também pode especificar um [StartTask] [ net_pool_starttask] para pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="6de11-251">Olá StartTask executa em cada nó como nó une pool Olá, e cada vez que um nó é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="6de11-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="6de11-252">Olá StartTask é especialmente útil para instalar aplicativos em execução de toohello anterior de nós de computação de tarefas.</span><span class="sxs-lookup"><span data-stu-id="6de11-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="6de11-253">Por exemplo, se suas tarefas de processam os dados por meio de scripts de Python, você poderá usar um tooinstall StartTask Python em nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="6de11-254">Neste aplicativo de exemplo, Olá StartTask copia arquivos de saudação que baixa de armazenamento (que são especificados usando Olá [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] propriedade) do diretório compartilhado do toohello de diretório de trabalho do hello StartTask que *todos os* tarefas em execução no nó Olá podem acessar.</span><span class="sxs-lookup"><span data-stu-id="6de11-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="6de11-255">Essencialmente, isso copia `TaskApplication.exe` e sua dependências toohello diretório compartilhado em cada nó como nó Olá une pool hello, para que as tarefas que são executados no nó Olá podem acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="6de11-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="6de11-256">Olá **pacotes de aplicativos** recurso de lote do Azure fornece tooget de outra maneira seu aplicativo em nós de computação de saudação em um pool.</span><span class="sxs-lookup"><span data-stu-id="6de11-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="6de11-257">Consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6de11-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="6de11-258">Também notável no trecho de código Olá acima é use Olá das duas variáveis de ambiente no hello *CommandLine* propriedade Olá StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` e `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="6de11-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="6de11-259">Cada nó de computação em um pool de lote é automaticamente configurado com diversas variáveis de ambiente que são tooBatch específico.</span><span class="sxs-lookup"><span data-stu-id="6de11-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="6de11-260">Qualquer processo que é executado por uma tarefa tem acesso toothese as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="6de11-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="6de11-261">toofind mais informações sobre variáveis de ambiente Olá que estão disponíveis em nós de computação em um pool de lote e obter informações sobre pastas de trabalho de tarefas, consulte Olá [configurações de ambiente para tarefas](batch-api-basics.md#environment-settings-for-tasks) e [arquivos e diretórios ](batch-api-basics.md#files-and-directories) seções Olá [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="6de11-262">Etapa 4: Criar o trabalho do Lote</span><span class="sxs-lookup"><span data-stu-id="6de11-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="6de11-263">![Criar trabalho do Lote][4]</span><span class="sxs-lookup"><span data-stu-id="6de11-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="6de11-264">Um **trabalho** do Lote é uma coleção de tarefas associadas a um pool de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="6de11-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="6de11-265">tarefas de saudação em um trabalho executar em nós de computação do pool Olá associado.</span><span class="sxs-lookup"><span data-stu-id="6de11-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="6de11-266">Você pode usar um trabalho, não apenas para a organização e controle de tarefas em cargas de trabalho relacionadas, mas também para impor certas restrições – como Olá tempo de execução máximo para o trabalho de saudação (e, por extensão, suas tarefas), bem como a prioridade do trabalho em trabalhos de tooother de relação no lote de saudação conta.</span><span class="sxs-lookup"><span data-stu-id="6de11-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="6de11-267">No entanto, neste exemplo, o trabalho de saudação é associado apenas ao pool de saudação que foi criado na etapa &#3;.</span><span class="sxs-lookup"><span data-stu-id="6de11-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="6de11-268">Nenhuma propriedade adicional será configurada.</span><span class="sxs-lookup"><span data-stu-id="6de11-268">No additional properties are configured.</span></span>

<span data-ttu-id="6de11-269">Todos os trabalhos do Lotes estão associados a um pool específico.</span><span class="sxs-lookup"><span data-stu-id="6de11-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="6de11-270">Essa associação indica quais nós tarefas saudação do trabalho serão executado em.</span><span class="sxs-lookup"><span data-stu-id="6de11-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="6de11-271">Você pode especificar isso usando Olá [CloudJob.PoolInformation] [ net_job_poolinfo] propriedade, conforme mostrado no trecho de código Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="6de11-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="6de11-272">Agora que um trabalho tiver sido criado, as tarefas são adicionadas tooperform trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="6de11-273">Etapa 5: Adicionar tarefas toojob</span><span class="sxs-lookup"><span data-stu-id="6de11-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="6de11-274">![Adicionar tarefas toojob][5]</span><span class="sxs-lookup"><span data-stu-id="6de11-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="6de11-275">
*(1) as tarefas são adicionadas toohello trabalho, tarefas de saudação (2) são agendado toorun em nós e tarefas de saudação (3) Baixar Olá tooprocess de arquivos de dados*</span><span class="sxs-lookup"><span data-stu-id="6de11-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="6de11-276">Lote **tarefas** são nós de computação Olá unidades individuais de trabalho que executam em hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="6de11-277">Uma tarefa tem uma linha de comando e executa os scripts de saudação ou executáveis que você especificar na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6de11-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="6de11-278">tooactually executar o trabalho, tarefas devem ser adicionadas tooa trabalho.</span><span class="sxs-lookup"><span data-stu-id="6de11-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="6de11-279">Cada [CloudTask] [ net_task] é configurada por meio de uma propriedade de linha de comando e [ResourceFiles] [ net_task_resourcefiles] (assim como acontece com StartTask do pool Olá) que tarefa Olá baixa toohello nó antes de sua linha de comando é executada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6de11-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="6de11-280">Em Olá *DotNetTutorial* projeto de exemplo, cada tarefa processa apenas um arquivo.</span><span class="sxs-lookup"><span data-stu-id="6de11-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="6de11-281">Portanto, sua coleção ResourceFiles contém um único elemento.</span><span class="sxs-lookup"><span data-stu-id="6de11-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
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

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="6de11-282">Quando eles acessar variáveis de ambiente, como `%AZ_BATCH_NODE_SHARED_DIR%` ou executar um aplicativo não encontrado no nó de saudação `PATH`, linhas de comando de tarefa devem ser prefixadas com `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="6de11-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="6de11-283">Isso explicitamente executar o interpretador de comandos hello e instruí-la tooterminate depois de executar o comando.</span><span class="sxs-lookup"><span data-stu-id="6de11-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="6de11-284">Esse requisito é desnecessário se suas tarefas de executar um aplicativo no nó de saudação `PATH` (como *robocopy.exe* ou *powershell.exe*) e nenhuma variável de ambiente é usados.</span><span class="sxs-lookup"><span data-stu-id="6de11-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="6de11-285">Dentro de saudação `foreach` loop no trecho de código Olá acima, você pode ver que linha de comando Olá para tarefa de saudação é construída, de modo que três argumentos de linha de comando são passados muito*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="6de11-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="6de11-286">Olá **primeiro argumento** é o caminho de saudação de tooprocess de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="6de11-287">Este é o arquivo de toohello de caminho local do hello existente no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="6de11-288">Olá quando o objeto ResourceFile no `UploadFileToContainerAsync` foi criado acima, o nome do arquivo hello foi usado para esta propriedade (como um construtor de ResourceFile do parâmetro toohello).</span><span class="sxs-lookup"><span data-stu-id="6de11-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="6de11-289">Isso indica que esse arquivo hello pode ser encontrado no hello mesmo diretório como *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="6de11-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="6de11-290">Olá **segundo argumento** Especifica que superior Olá *N* palavras devem ser escritas toohello arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="6de11-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="6de11-291">No exemplo hello, isso é embutido para que as palavras de três principais Olá são gravadas toohello arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="6de11-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="6de11-292">Olá **terceiro argumento** é a assinatura de acesso compartilhado da saudação (SAS) que fornece acesso de gravação toohello **saída** contêiner no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="6de11-293">*TaskApplication.exe* Use isso compartilhado URL de assinatura de acesso quando ele carrega tooAzure de arquivo de saída de hello armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de11-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="6de11-294">Você pode encontrar o código de saudação para isso no hello `UploadFileToContainer` método no projeto Olá TaskApplication `Program.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="6de11-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
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

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="6de11-295">Etapa 6: Monitorar tarefas</span><span class="sxs-lookup"><span data-stu-id="6de11-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="6de11-296">![Monitorar tarefas][6]</span><span class="sxs-lookup"><span data-stu-id="6de11-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="6de11-297">
*Olá cliente (1) os monitores Olá tarefas para conclusão e o status de êxito e aplicativos (2) Olá tarefas carregamento resultado dados tooAzure armazenamento*</span><span class="sxs-lookup"><span data-stu-id="6de11-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="6de11-298">Quando tarefas são adicionadas tooa trabalho, eles são automaticamente na fila e agendados para execução em nós de computação no pool de saudação associado ao trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="6de11-299">Com base nas configurações de saudação que você especificar, lote trata enfileiramento de mensagens todas as tarefas, agendamento, repetir e outras tarefas de administração de tarefa para você.</span><span class="sxs-lookup"><span data-stu-id="6de11-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="6de11-300">Há muitas abordagens toomonitoring a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="6de11-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="6de11-301">O DotNetTutorial mostra um exemplo simples que relata apenas a conclusão e a falha de tarefas ou os estados de êxito.</span><span class="sxs-lookup"><span data-stu-id="6de11-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="6de11-302">Dentro de saudação `MonitorTasks` do DotNetTutorial método `Program.cs`, há três conceitos de lote .NET que garantem a discussão.</span><span class="sxs-lookup"><span data-stu-id="6de11-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="6de11-303">Eles são listados na ordem em que aparecem:</span><span class="sxs-lookup"><span data-stu-id="6de11-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="6de11-304">**ODATADetailLevel**: a especificação de um [ODATADetailLevel][net_odatadetaillevel] na lista de operações (como a obtenção de uma lista de tarefas do trabalho) é essencial para garantir o desempenho do aplicativo do Lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="6de11-305">Adicionar [consultar o serviço de lote do Azure Olá com eficiência](batch-efficient-list-queries.md) tooyour ler lista se você planeja fazer qualquer tipo de monitoramento de status em seus aplicativos de lote.</span><span class="sxs-lookup"><span data-stu-id="6de11-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="6de11-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] fornece aplicativos .NET do Lote com utilitários auxiliares para monitorar estados da tarefa.</span><span class="sxs-lookup"><span data-stu-id="6de11-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="6de11-307">Em `MonitorTasks`, *DotNetTutorial* aguarda tooreach de todas as tarefas [TaskState.Completed] [ net_taskstate] dentro de um limite de tempo.</span><span class="sxs-lookup"><span data-stu-id="6de11-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="6de11-308">Em seguida, encerra o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="6de11-309">**TerminateJobAsync**: encerrando um trabalho com [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (ou Olá bloqueando JobOperations.TerminateJob) marca trabalho como concluído.</span><span class="sxs-lookup"><span data-stu-id="6de11-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="6de11-310">É essencial toodo se sua solução de lote usa um [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="6de11-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="6de11-311">Esse é um tipo especial de tarefa, descrita em [Tarefas de preparação e de conclusão do trabalho](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="6de11-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="6de11-312">Olá `MonitorTasks` método de *DotNetTutorial*do `Program.cs` é exibida abaixo:</span><span class="sxs-lookup"><span data-stu-id="6de11-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
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

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="6de11-313">Etapa 7: Baixar a saída da tarefa</span><span class="sxs-lookup"><span data-stu-id="6de11-313">Step 7: Download task output</span></span>
<span data-ttu-id="6de11-314">![Baixar a saída da tarefa do Armazenamento][7]</span><span class="sxs-lookup"><span data-stu-id="6de11-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="6de11-315">Agora que hello trabalho é concluído, saída de hello das tarefas de saudação pode ser baixada do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de11-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="6de11-316">Isso é feito com uma chamada muito`DownloadBlobsFromContainerAsync` na *DotNetTutorial*do `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="6de11-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="6de11-317">Olá chamada muito`DownloadBlobsFromContainerAsync` em Olá *DotNetTutorial* aplicativo especifica que arquivos Olá devem ser baixado tooyour `%TEMP%` pasta.</span><span class="sxs-lookup"><span data-stu-id="6de11-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="6de11-318">Sinta-se livre toomodify este local de saída.</span><span class="sxs-lookup"><span data-stu-id="6de11-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="6de11-319">Etapa 8: Excluir contêineres</span><span class="sxs-lookup"><span data-stu-id="6de11-319">Step 8: Delete containers</span></span>
<span data-ttu-id="6de11-320">Como você é cobrado pelos dados que residem no armazenamento do Azure, é sempre blobs de tooremove uma boa ideia que não são mais necessários para seus trabalhos em lotes.</span><span class="sxs-lookup"><span data-stu-id="6de11-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="6de11-321">Do DotNetTutorial `Program.cs`, isso é feito com o método de auxiliar três chamadas toohello `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="6de11-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="6de11-322">método Hello em si simplesmente obtém um contêiner de toohello de referência e, em seguida, chama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="6de11-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="6de11-323">Etapa 9: Excluir trabalho hello e pool Olá</span><span class="sxs-lookup"><span data-stu-id="6de11-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="6de11-324">Na etapa final do hello, você está toodelete solicitadas Olá trabalho Olá pool e que foram criados pelo aplicativo de DotNetTutorial hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="6de11-325">Embora você não seja cobrado pelos trabalhos e pelas tarefas, *será* cobrado pelos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="6de11-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="6de11-326">Portanto, recomendamos que você aloque os nós conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6de11-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="6de11-327">A exclusão de pools não utilizados pode fazer parte de seu processo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6de11-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="6de11-328">Olá BatchClient [JobOperations] [ net_joboperations] e [PoolOperations] [ net_pooloperations] têm métodos correspondentes de exclusão, que são chamados se usuário de saudação Confirmar exclusão:</span><span class="sxs-lookup"><span data-stu-id="6de11-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
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
> <span data-ttu-id="6de11-329">Tenha em mente que você será cobrado pelos recursos de computação, a exclusão dos pools não utilizados reduzirá o custo.</span><span class="sxs-lookup"><span data-stu-id="6de11-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="6de11-330">Além disso, esteja ciente que a exclusão do pool de exclui todos os nós de computação no pool, e que os dados em nós hello serão irrecuperáveis depois Olá pool é excluído.</span><span class="sxs-lookup"><span data-stu-id="6de11-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="6de11-331">Executar Olá *DotNetTutorial* exemplo</span><span class="sxs-lookup"><span data-stu-id="6de11-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="6de11-332">Quando você executa o aplicativo de exemplo hello, saída de console hello será a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="6de11-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="6de11-333">Durante a execução, você terá uma pausa em `Awaiting task completion, timeout in 00:30:00...` enquanto nós de computação do pool de saudação são iniciados.</span><span class="sxs-lookup"><span data-stu-id="6de11-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="6de11-334">Saudação de uso [portal do Azure] [ azure_portal] toomonitor seu pool, nós de computação, trabalhos e tarefas durante e após a execução.</span><span class="sxs-lookup"><span data-stu-id="6de11-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="6de11-335">Saudação de uso [portal do Azure] [ azure_portal] ou hello [Azure Storage Explorer] [ storage_explorers] tooview Olá recursos de armazenamento (contêineres e blobs) que são criado por um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6de11-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="6de11-336">Tempo de execução típico é **aproximadamente 5 minutos** quando você executa o aplicativo hello em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="6de11-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="6de11-337">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6de11-337">Next steps</span></span>
<span data-ttu-id="6de11-338">Sinta-se livre toomake alterações muito*DotNetTutorial* e *TaskApplication* tooexperiment com diferentes cenários de computação.</span><span class="sxs-lookup"><span data-stu-id="6de11-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="6de11-339">Por exemplo, tente adicionar um atraso de execução muito*TaskApplication*, tal como com [Sleep][net_thread_sleep], toosimulate demoradas tarefas e monitorá-los no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="6de11-340">Tente adicionar mais tarefas ou ajustar Olá número de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="6de11-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="6de11-341">Adicionar lógica toocheck para e permitir o uso de saudação de um tempo de execução toospeed pool existente (*dica*: check-out `ArticleHelpers.cs` em Olá [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] project no [exemplos de lote do azure][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="6de11-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="6de11-342">Agora que você está familiarizado com o fluxo de trabalho básico de uma solução de lote Olá, é hora toodig em toohello de recursos adicionais do serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="6de11-343">Saudação de revisão [recursos de visão geral do Azure Batch](batch-api-basics.md) artigo, que é recomendável que você confirme o novo serviço toohello.</span><span class="sxs-lookup"><span data-stu-id="6de11-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="6de11-344">Início na Olá outros artigos de desenvolvimento de lote em **desenvolvimento detalhado** em Olá [de aprendizado em lotes][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="6de11-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="6de11-345">Check-out de uma implementação diferente de processamento de carga de trabalho hello "top N palavras" usando o lote em Olá [TopNWords] [ github_topnwords] exemplo.</span><span class="sxs-lookup"><span data-stu-id="6de11-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="6de11-346">Saudação de revisão .NET em lotes [notas de versão](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) para alterações mais recentes de saudação na biblioteca de saudação.</span><span class="sxs-lookup"><span data-stu-id="6de11-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Criar pool do Lote"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Criar trabalho em lotes"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Adicionar tarefas toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorar tarefas"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Baixar a saída da tarefa do Armazenamento"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Fluxo de trabalho da solução do Lote (diagrama completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenciais do Lote no Portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenciais do Armazenamento no Portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Fluxo de trabalho da solução do Lote (diagrama mínimo)"
