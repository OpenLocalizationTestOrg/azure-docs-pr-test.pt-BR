---
title: "aaaTutorial - Olá Use SDK de lote do Azure para Python | Microsoft Docs"
description: "Aprenda os conceitos básicos de saudação do lote do Azure e criar uma solução simple usando Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="1d8e2-103">Introdução ao Olá lote SDK para Python</span><span class="sxs-lookup"><span data-stu-id="1d8e2-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d8e2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1d8e2-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="1d8e2-105">Python</span><span class="sxs-lookup"><span data-stu-id="1d8e2-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="1d8e2-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d8e2-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="1d8e2-107">Conheça os fundamentos de saudação do [do Azure Batch] [ azure_batch] e hello [lote Python] [ py_azure_sdk] cliente discutir um pequeno aplicativo lote escrito em Python.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="1d8e2-108">Vamos examinar como duas amostras scripts use Olá lote serviço tooprocess uma carga de trabalho paralela em máquinas virtuais do Linux na nuvem hello e como eles interagem com [armazenamento do Azure](../storage/common/storage-introduction.md) para preparação de arquivo e de recuperação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="1d8e2-109">Você vai aprender um fluxo de trabalho de aplicativo comuns em lotes e obter uma compreensão básica de Olá principais componentes do lote, como trabalhos, tarefas, pools de e nós de computação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="1d8e2-110">![Fluxo de trabalho da solução do Lote (básico)][11]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="1d8e2-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1d8e2-111">Prerequisites</span></span>
<span data-ttu-id="1d8e2-112">Este artigo pressupõe que você tenha um conhecimento prático do Python e que esteja familiarizado com o Linux.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="1d8e2-113">Ele também pressupõe que você é capaz de toosatisfy Olá conta criação requisitos especificados abaixo para o Azure e Olá lote e serviços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="1d8e2-114">Contas</span><span class="sxs-lookup"><span data-stu-id="1d8e2-114">Accounts</span></span>
* <span data-ttu-id="1d8e2-115">**Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="1d8e2-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="1d8e2-116">**Conta do Lote**: quando você tiver uma assinatura do Azure, [crie uma conta do Lote do Azure](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="1d8e2-117">**Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="1d8e2-118">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="1d8e2-118">Code sample</span></span>
<span data-ttu-id="1d8e2-119">tutorial de Python Olá [exemplo de código] [ github_article_samples] é uma saudação muitos exemplos de código do lote encontrados no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="1d8e2-120">Você pode baixar todos os exemplos de saudação clicando **Clone ou download > baixar ZIP** na home page do repositório de hello, ou clicando em Olá [azure lote-exemplos master.zip] [ github_samples_zip]link de download direto.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="1d8e2-121">Depois de extrair o conteúdo de saudação do arquivo ZIP de saudação, scripts Olá dois para este tutorial são encontrados em Olá `article_samples` diretório:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="1d8e2-122">Ambiente do Python</span><span class="sxs-lookup"><span data-stu-id="1d8e2-122">Python environment</span></span>
<span data-ttu-id="1d8e2-123">Olá toorun *python_tutorial_client.py* script de exemplo em sua estação de trabalho local, é necessário um **intérprete Python** compatível com a versão **2.7** ou **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="1d8e2-124">script Hello foi testado no Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="1d8e2-125">dependências de criptografia</span><span class="sxs-lookup"><span data-stu-id="1d8e2-125">cryptography dependencies</span></span>
<span data-ttu-id="1d8e2-126">Você deve instalar dependências Olá Olá [criptografia] [ crypto] biblioteca, exigida pelo Olá `azure-batch` e `azure-storage` pacotes Python.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="1d8e2-127">Execute uma saudação após operações adequadas para sua plataforma, ou consulte toohello [instalação criptografia] [ crypto_install] detalhes para obter mais informações:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="1d8e2-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1d8e2-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="1d8e2-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="1d8e2-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="1d8e2-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="1d8e2-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="1d8e2-131">Windows</span><span class="sxs-lookup"><span data-stu-id="1d8e2-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="1d8e2-132">Se a instalação da Python 3.3 + no Linux, use equivalentes de python3 Olá dependências de Python Olá.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="1d8e2-133">Por exemplo, no Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="1d8e2-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="1d8e2-134">Pacotes do Azure</span><span class="sxs-lookup"><span data-stu-id="1d8e2-134">Azure packages</span></span>
<span data-ttu-id="1d8e2-135">Em seguida, instalar Olá **do Azure Batch** e **armazenamento do Azure** pacotes Python.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="1d8e2-136">Você pode instalar os dois pacotes usando **pip** e hello *requirements.txt* encontrado aqui:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="1d8e2-137">Problema a seguir **pip** tooinstall Olá lote e armazenamento de pacotes de comando:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="1d8e2-138">Ou, você pode instalar Olá [do azure batch] [ pypi_batch] e [armazenamento do azure] [ pypi_storage] Python pacotes manualmente:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="1d8e2-139">Se você estiver usando uma conta sem privilégios, talvez seja necessário tooprefix seus comandos com `sudo`.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="1d8e2-140">Por exemplo: `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="1d8e2-141">Para saber mais sobre como instalar pacotes Python, veja [Installing Packages][pypi_install] (Instalando pacotes) em python.org.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="1d8e2-142">Exemplo de código do tutorial do Python do Lote</span><span class="sxs-lookup"><span data-stu-id="1d8e2-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="1d8e2-143">exemplo de tutorial código Python de lote Hello consiste em dois scripts Python e alguns arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="1d8e2-144">**python_tutorial_client.py**: interage com tooexecute de serviços de lote e armazenamento Olá uma carga de trabalho paralela em nós de computação (máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="1d8e2-145">Olá *python_tutorial_client.py* script é executado na sua estação de trabalho local.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="1d8e2-146">**python_tutorial_task.py**: script hello executado em nós de computação no trabalho do Azure tooperform Olá real.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="1d8e2-147">No exemplo hello, *python_tutorial_task.py* analisa Olá texto em um arquivo baixado do armazenamento do Azure (arquivo de entrada hello).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="1d8e2-148">Em seguida, ele produz um arquivo de texto (arquivo de saída de hello) que contém uma lista de palavras de três principais Olá que aparecem no arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="1d8e2-149">Depois que ele cria o arquivo de saída de hello, *python_tutorial_task.py* carregamentos Olá arquivo tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="1d8e2-150">Isso disponibiliza download toohello script de cliente em execução em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="1d8e2-151">Olá *python_tutorial_task.py* script será executado em paralelo em vários nós de computação em Olá serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="1d8e2-152">**./Data/taskdata\*. txt**: esses arquivos de três texto fornecem entrada Olá para tarefas de saudação que são executados em Olá nós de computação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="1d8e2-153">Olá diagrama a seguir ilustra as operações primário Olá executadas pelos scripts de cliente e a tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="1d8e2-154">Esse fluxo de trabalho básico é típico de muitas soluções de computação criadas com o Lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="1d8e2-155">Embora não demonstra todos os recursos disponíveis no serviço de lote de hello, quase todos os cenários de lote incluem partes desse fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="1d8e2-156">![Fluxo de trabalho de exemplo do Lote][8]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="1d8e2-157">**Etapa 1.**</span><span class="sxs-lookup"><span data-stu-id="1d8e2-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="1d8e2-158">Crie **contêineres** no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="1d8e2-159">
[**Etapa 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="1d8e2-160">Carregar toocontainers de arquivos de script e a entrada de tarefa.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="1d8e2-161">
[**Etapa 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="1d8e2-162">Criar um **pool** do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="1d8e2-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="1d8e2-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="1d8e2-164">Olá pool **StartTask** downloads Olá tarefa script (python_tutorial_task.py) toonodes ao entrarem pool hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="1d8e2-165">
[**Etapa 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="1d8e2-166">Crie um **trabalho** do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="1d8e2-167">
[**Etapa 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="1d8e2-168">Adicionar **tarefas** toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="1d8e2-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="1d8e2-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="1d8e2-170">tarefas de saudação são agendado tooexecute em nós.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="1d8e2-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="1d8e2-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="1d8e2-172">Cada tarefa baixa seus dados de entrada do Armazenamento do Azure e então inicia a execução.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="1d8e2-173">
[**Etapa 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="1d8e2-174">Monitore as tarefas.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="1d8e2-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="1d8e2-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="1d8e2-176">Como as tarefas são concluídas, carregar seu dados de saída tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="1d8e2-177">
[**Etapa 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="1d8e2-178">Baixe a saída da tarefa do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-178">Download task output from Storage.</span></span>

<span data-ttu-id="1d8e2-179">Como mencionado, nem todas as soluções do Lote executam essas etapas exatas, e elas podem incluir muitas outras, mas este exemplo demonstra os processos comuns encontrados em uma solução do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="1d8e2-180">Preparar o script de cliente</span><span class="sxs-lookup"><span data-stu-id="1d8e2-180">Prepare client script</span></span>
<span data-ttu-id="1d8e2-181">Antes de executar o exemplo hello, adicione suas credenciais de conta de armazenamento e de lote muito*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="1d8e2-182">Se você não tiver feito isso, abra o arquivo de saudação em seu favorito Olá editor e a atualização de linhas com as credenciais a seguir.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="1d8e2-183">Você pode encontrar suas credenciais de conta de lote e armazenamento na folha da conta de saudação de cada serviço em Olá [portal do Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="1d8e2-184">![As credenciais no portal de saudação do lote][9]
![credenciais de armazenamento no portal de saudação][10]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="1d8e2-185">Olá seções a seguir, podemos analisar etapas Olá usadas pelo Olá scripts tooprocess uma carga de trabalho no serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="1d8e2-186">Recomendamos que você regularmente toorefer toohello scripts em seu editor enquanto você vai restantes de saudação do artigo hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="1d8e2-187">Navegue toohello a seguinte linha no **python_tutorial_client.py** toostart com a etapa 1:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="1d8e2-188">Etapa 1: Criar contêineres do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="1d8e2-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="1d8e2-189">![Criar contêineres no Armazenamento do Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="1d8e2-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="1d8e2-190">O Lote inclui suporte interno para a interação com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="1d8e2-191">Contêineres em sua conta de armazenamento fornecerá arquivos Olá necessários para tarefas de saudação que são executados em sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="1d8e2-192">contêineres de saudação também fornecem um lugar toostore Olá dados da saída tarefas Olá produzem.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="1d8e2-193">primeiro Olá Olá *python_tutorial_client.py* script faz é criar três contêineres [armazenamento de BLOBs do Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="1d8e2-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="1d8e2-194">**aplicativo**: este contêiner armazena script de Python Olá executado pelas tarefas de saudação *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="1d8e2-195">**entrada**: tarefas baixarão tooprocess de arquivos de dados de saudação do hello *entrada* contêiner.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="1d8e2-196">**saída**: quando tarefas concluir o processamento do arquivo de entrada, eles carregará Olá resultados toohello *saída* contêiner.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="1d8e2-197">Em ordem toointeract com um armazenamento de conta e criar contêineres, usamos Olá [armazenamento do azure] [ pypi_storage] pacote toocreate um [BlockBlobService] [ py_blockblobservice] objeto - Olá "cliente blob".</span><span class="sxs-lookup"><span data-stu-id="1d8e2-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="1d8e2-198">Em seguida, podemos criar três contêineres na conta de armazenamento hello usando o cliente do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="1d8e2-199">Depois que criar contêineres de hello, aplicativo hello agora pode carregar arquivos de saudação que serão usados pelas tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="1d8e2-200">[Como toouse armazenamento de BLOBs do Azure do Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) fornece uma boa visão geral de como trabalhar com contêineres de armazenamento do Azure e blobs.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="1d8e2-201">Como começar a trabalhar com o lote, ele deve ser superior Olá da sua lista de leitura.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="1d8e2-202">Etapa 2: Carregar o script de tarefa e os arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="1d8e2-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="1d8e2-203">![Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)][2]
</span><span class="sxs-lookup"><span data-stu-id="1d8e2-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="1d8e2-204">Operação, de carregamento no arquivo hello *python_tutorial_client.py* primeiro define coleções de **aplicativo** e **entrada** caminhos de arquivo que existem no computador local hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="1d8e2-205">Em seguida, ele carrega esses contêineres de toohello de arquivos que você criou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="1d8e2-206">Usando a compreensão da lista, Olá `upload_file_to_container` função é chamada para cada arquivo em coleções de saudação e dois [ResourceFile] [ py_resource_file] coleções são preenchidas.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="1d8e2-207">Olá `upload_file_to_container` função é exibida abaixo:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="1d8e2-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="1d8e2-208">ResourceFiles</span></span>
<span data-ttu-id="1d8e2-209">Um [ResourceFile] [ py_resource_file] fornece tarefas em lote com o arquivo de tooa URL Olá no armazenamento do Azure que é baixado tooa nó de computação para que essa tarefa seja executada.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="1d8e2-210">Olá [ResourceFile][py_resource_file]. **blob_source** propriedade especifica a URL completa do arquivo Olá Olá conforme ela existe no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="1d8e2-211">Olá URL também pode incluir uma assinatura de acesso compartilhado (SAS) que fornece acesso seguro toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="1d8e2-212">A maioria dos tipos de tarefas do Lote tem uma propriedade *ResourceFiles* , incluindo:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="1d8e2-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="1d8e2-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="1d8e2-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="1d8e2-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="1d8e2-217">Este exemplo não usa Olá JobPreparationTask ou tipos de tarefa JobReleaseTask, mas você pode ler mais sobre eles em [nós de computação de tarefas de preparação e conclusão de trabalho de execução em lote do Azure](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="1d8e2-218">Assinatura de acesso compartilhado (SAS)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="1d8e2-219">Assinaturas de acesso compartilhado são cadeias de caracteres que fornecem acesso seguro toocontainers e blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="1d8e2-220">Olá *python_tutorial_client.py* script usa ambos os BLOBs e contêiner assinaturas de acesso compartilhado e demonstra como tooobtain esses compartilhado acessar cadeias de caracteres de assinatura de saudação serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="1d8e2-221">**Assinaturas de acesso compartilhado de blob**: usa de StartTask do pool de saudação ao baixar arquivos de dados Olá tarefa script e a entrada do armazenamento de blob assinaturas de acesso compartilhado (consulte [etapa 3](#step-3-create-batch-pool) abaixo).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="1d8e2-222">Olá `upload_file_to_container` funcionar em *python_tutorial_client.py* contém código Olá que obtém a assinatura de acesso compartilhado de cada blob.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="1d8e2-223">Isso é feito chamando [BlockBlobService.make_blob_url] [ py_make_blob_url] no módulo de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="1d8e2-224">**Assinatura de acesso compartilhado do contêiner**: como cada tarefa termina o trabalho no nó de computação hello, ele carrega sua toohello do arquivo de saída *saída* contêiner no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="1d8e2-225">toodo, *python_tutorial_task.py* usa uma assinatura de acesso compartilhado do contêiner que fornece acesso de gravação toohello contêiner.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="1d8e2-226">Olá `get_container_sas_token` funcionar em *python_tutorial_client.py* obtém a assinatura de acesso compartilhado do contêiner hello, que é passada como tarefas de toohello um argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="1d8e2-227">Etapa 5 de # [trabalho de tooa adicionar tarefas](#step-5-add-tasks-to-job), discute o uso de saudação do SAS do contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="1d8e2-228">Check-out da série de duas partes da saudação em assinaturas de acesso compartilhado, [parte 1: modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: criar e usar uma SAS com hello serviço Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn mais sobre como fornecer acesso seguro toodata em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="1d8e2-229">Etapa 3: Criar pool do Lote</span><span class="sxs-lookup"><span data-stu-id="1d8e2-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="1d8e2-230">![Criar um pool do Lote][3]
</span><span class="sxs-lookup"><span data-stu-id="1d8e2-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="1d8e2-231">Um **pool** do Lote é uma coleção de nós de computação (máquinas virtuais) nos quais o Lote executa as tarefas de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="1d8e2-232">Depois que ele carrega Olá tarefa script e dados de arquivos toohello conta de armazenamento, *python_tutorial_client.py* inicia sua interação com o serviço de lote hello usando o módulo de lote Python hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="1d8e2-233">toodo, um [BatchServiceClient] [ py_batchserviceclient] é criada:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="1d8e2-234">Em seguida, um conjunto de nós de computação é criado na conta do lote com uma chamada de saudação muito`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="1d8e2-235">Quando você cria um pool, você define uma [PoolAddParameter] [ py_pooladdparam] que especifica as várias propriedades de pool de saudação:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="1d8e2-236">**ID** do pool de saudação (*id* - obrigatório)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="1d8e2-237">Como acontece com a maioria das entidades no Lote, seu novo pool deverá ter uma ID exclusiva em sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="1d8e2-238">Seu código refere-se usando sua ID do pool de toothis, e é assim que você identifica pool Olá no hello Azure [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="1d8e2-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="1d8e2-239">**Número de nós de computação** (*target_dedicated* – obrigatório)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="1d8e2-240">Essa propriedade especifica como muitas máquinas virtuais devem ser implantados no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="1d8e2-241">É importante toonote todas as contas de lote têm um padrão **cota** limites Olá inúmeros **núcleos** (e, portanto, nós de computação) em uma conta de lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="1d8e2-242">Você pode encontrar as cotas de padrão de saudação e instruções sobre como muito[aumentar cota](batch-quota-limit.md#increase-a-quota) (como o número máximo de saudação de núcleos em sua conta em lotes) em [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="1d8e2-243">Se você estiver se perguntando "Por que meu pool não alcança mais do que X nós?",</span><span class="sxs-lookup"><span data-stu-id="1d8e2-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="1d8e2-244">Essa cota de núcleos pode ser a causa de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="1d8e2-245">**Sistema operacional** para nós (*virtual_machine_configuration* **ou** *cloud_service_configuration* – obrigatório)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="1d8e2-246">Em *python_tutorial_client.py*, podemos criar um pool de nós do Linux usando um [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="1d8e2-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="1d8e2-247">Olá `select_latest_verified_vm_image_with_node_agent_sku` funcionar em `common.helpers` simplifica o trabalho com [Marketplace de máquinas virtuais do Azure] [ vm_marketplace] imagens.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="1d8e2-248">Veja [Provisionar nós de computação do Linux em pools do Lote do Azure](batch-linux-nodes.md) para saber mais sobre o uso de imagens do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="1d8e2-249">**Tamanho de nós de computação** (*vm_size* – obrigatório)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="1d8e2-250">Já que estamos especificando nós do Linux para a nossa [VirtualMachineConfiguration][py_vm_config], especificamos um tamanho de VM (neste exemplo, `STANDARD_A1`) de [Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1d8e2-251">Novamente, veja [Provisionar nós de computação Linux em pools do Lote do Azure](batch-linux-nodes.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="1d8e2-252">**Iniciar tarefa** (*start_task* – não obrigatório)</span><span class="sxs-lookup"><span data-stu-id="1d8e2-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="1d8e2-253">Juntamente com hello acima de propriedades de nó físico, você também pode especificar um [StartTask] [ py_starttask] para pool de saudação (não é necessário).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="1d8e2-254">Olá StartTask executa em cada nó como nó une pool Olá, e cada vez que um nó é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="1d8e2-255">Olá StartTask é especialmente útil para preparar nós de computação para execução de saudação de tarefas, como aplicativos de saudação que executam as tarefas de instalação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="1d8e2-256">Neste aplicativo de exemplo, Olá StartTask copia arquivos de saudação que baixa de armazenamento (que é especificado por meio da saudação StartTask **resource_files** propriedade) do hello StartTask *dodiretóriodetrabalho* toohello *compartilhado* diretório que podem acessar todas as tarefas em execução no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="1d8e2-257">Essencialmente, isso copia `python_tutorial_task.py` toohello diretório compartilhado em cada nó como nó Olá une pool hello, para que as tarefas que são executados no nó Olá podem acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="1d8e2-258">Você pode perceber Olá chamada toohello `wrap_commands_in_shell` função auxiliar.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="1d8e2-259">Essa função usa um conjunto de comandos separados e cria uma única linha de comando apropriada para a propriedade de linha de comando da tarefa.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="1d8e2-260">Também notável no trecho de código Olá acima é use Olá das duas variáveis de ambiente no hello **linha_de_comando** propriedade Olá StartTask: `AZ_BATCH_TASK_WORKING_DIR` e `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="1d8e2-261">Cada nó de computação em um pool de lote é automaticamente configurado com diversas variáveis de ambiente que são tooBatch específico.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="1d8e2-262">Qualquer processo que é executado por uma tarefa tem acesso toothese as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="1d8e2-263">toofind mais informações sobre variáveis de ambiente Olá que estão disponíveis em nós de computação em um pool de lote, bem como informações sobre pastas de trabalho de tarefas, consulte **configurações de ambiente para tarefas** e **arquivos e diretórios**  em Olá [visão geral dos recursos do Azure Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="1d8e2-264">Etapa 4: Criar o trabalho do Lote</span><span class="sxs-lookup"><span data-stu-id="1d8e2-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="1d8e2-265">![Criar trabalho do Lote][4]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="1d8e2-266">Um **trabalho** do Lote é uma coleção de tarefas associadas a um pool de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="1d8e2-267">tarefas de saudação em um trabalho executar em nós de computação do pool Olá associado.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="1d8e2-268">Você pode usar um trabalho, não apenas para a organização e controle de tarefas em cargas de trabalho relacionadas, mas também para impor certas restrições – como Olá tempo de execução máximo para o trabalho de saudação (e, por extensão, suas tarefas) e a prioridade do trabalho em trabalhos de tooother de relação no hello conta do lote.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="1d8e2-269">No entanto, neste exemplo, o trabalho de saudação é associado apenas ao pool de saudação que foi criado na etapa &#3;.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="1d8e2-270">Nenhuma propriedade adicional será configurada.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-270">No additional properties are configured.</span></span>

<span data-ttu-id="1d8e2-271">Todos os trabalhos do Lotes estão associados a um pool específico.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="1d8e2-272">Essa associação indica quais nós executar tarefas do trabalho Olá no.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="1d8e2-273">Especificar o pool Olá usando Olá [PoolInformation] [ py_poolinfo] propriedade, conforme mostrado no trecho de código Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="1d8e2-274">Agora que um trabalho tiver sido criado, as tarefas são adicionadas tooperform trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="1d8e2-275">Etapa 5: Adicionar tarefas toojob</span><span class="sxs-lookup"><span data-stu-id="1d8e2-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="1d8e2-276">![Adicionar tarefas toojob][5]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="1d8e2-277">
*(1) as tarefas são adicionadas toohello trabalho, tarefas de saudação (2) são agendado toorun em nós e tarefas de saudação (3) Baixar Olá tooprocess de arquivos de dados*</span><span class="sxs-lookup"><span data-stu-id="1d8e2-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="1d8e2-278">Lote **tarefas** são nós de computação Olá unidades individuais de trabalho que executam em hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="1d8e2-279">Uma tarefa tem uma linha de comando e executa os scripts de saudação ou executáveis que você especificar na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="1d8e2-280">tooactually executar o trabalho, tarefas devem ser adicionadas tooa trabalho.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="1d8e2-281">Cada [CloudTask] [ py_task] é configurado com uma propriedade de linha de comando e [ResourceFiles] [ py_resource_file] (assim como acontece com StartTask do pool Olá) que Olá tarefa baixa toohello nó antes de sua linha de comando é executada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="1d8e2-282">Exemplo hello, cada tarefa processa apenas um arquivo.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="1d8e2-283">Portanto, sua coleção ResourceFiles contém um único elemento.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="1d8e2-284">Quando eles acessar variáveis de ambiente, como `$AZ_BATCH_NODE_SHARED_DIR` ou executar um aplicativo não encontrado no nó de saudação `PATH`, linhas de comando da tarefa deve chamar hello shell explicitamente, como com `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="1d8e2-285">Esse requisito é desnecessário se suas tarefas de executar um aplicativo no nó de saudação `PATH` e não referenciam as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="1d8e2-286">Dentro de saudação `for` loop no trecho de código Olá acima, você pode ver que a linha de comando Olá para tarefa de saudação é construída com cinco argumentos de linha de comando que são passados muito*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="1d8e2-287">**FilePath**: Este é o arquivo de toohello de caminho local do hello existente no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="1d8e2-288">Olá quando o objeto ResourceFile no `upload_file_to_container` foi criado na etapa 2 acima, o nome do arquivo hello foi usado para esta propriedade (Olá `file_path` parâmetro no construtor de ResourceFile Olá).</span><span class="sxs-lookup"><span data-stu-id="1d8e2-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="1d8e2-289">Isso indica que esse arquivo hello pode ser encontrado no hello mesmo diretório no nó hello como *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="1d8e2-290">**NUMWORDS**: superior Olá *N* palavras devem ser escritas toohello arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="1d8e2-291">**storageaccount**: nome de saudação do hello conta de armazenamento que possui a saída da tarefa Olá Olá contêiner toowhich deve ser carregado.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="1d8e2-292">**storagecontainer**: nome de saudação do Olá Olá de toowhich do contêiner de armazenamento de saída de arquivos devem ser carregados.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="1d8e2-293">**sastoken**: assinatura de acesso compartilhado da saudação (SAS) que fornece acesso de gravação toohello **saída** contêiner no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="1d8e2-294">Olá *python_tutorial_task.py* script usa essa assinatura de acesso compartilhado quando cria sua referência BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="1d8e2-295">Isso fornece acesso de gravação toohello contêiner sem a necessidade de uma chave de acesso para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="1d8e2-296">Etapa 6: Monitorar tarefas</span><span class="sxs-lookup"><span data-stu-id="1d8e2-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="1d8e2-297">![Monitorar tarefas][6]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="1d8e2-298">
*Olá tarefas de saudação do script monitores (1) para o status de conclusão e tarefas (2) Olá carregar dados de resultado tooAzure armazenamento*</span><span class="sxs-lookup"><span data-stu-id="1d8e2-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="1d8e2-299">Quando tarefas são adicionadas tooa trabalho, eles são automaticamente na fila e agendados para execução em nós de computação no pool de saudação associado ao trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="1d8e2-300">Com base nas configurações de saudação que você especificar, lote trata enfileiramento de mensagens todas as tarefas, agendamento, repetir e outras tarefas de administração de tarefa para você.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="1d8e2-301">Há muitas abordagens toomonitoring a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="1d8e2-302">Olá `wait_for_tasks_to_complete` funcionar em *python_tutorial_client.py* fornece um exemplo simples de tarefas de monitoramento para um determinado estado, nesse caso, hello [concluída] [ py_taskstate] estado.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="1d8e2-303">Etapa 7: Baixar a saída da tarefa</span><span class="sxs-lookup"><span data-stu-id="1d8e2-303">Step 7: Download task output</span></span>
<span data-ttu-id="1d8e2-304">![Baixar a saída da tarefa do Armazenamento][7]</span><span class="sxs-lookup"><span data-stu-id="1d8e2-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="1d8e2-305">Agora que hello trabalho é concluído, saída de hello das tarefas de saudação pode ser baixada do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="1d8e2-306">Isso é feito com uma chamada muito`download_blobs_from_container` na *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="1d8e2-307">Olá chamada muito`download_blobs_from_container` na *python_tutorial_client.py* Especifica que arquivos Olá devem ser o diretório base tooyour baixado.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="1d8e2-308">Sinta-se livre toomodify este local de saída.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="1d8e2-309">Etapa 8: Excluir contêineres</span><span class="sxs-lookup"><span data-stu-id="1d8e2-309">Step 8: Delete containers</span></span>
<span data-ttu-id="1d8e2-310">Como você é cobrado pelos dados que residem no armazenamento do Azure, é sempre tooremove uma boa ideia que todos os blobs que não é mais necessário para seus trabalhos em lotes.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="1d8e2-311">Em *python_tutorial_client.py*, isso é feito com três chamadas muito[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="1d8e2-312">Etapa 9: Excluir trabalho hello e pool Olá</span><span class="sxs-lookup"><span data-stu-id="1d8e2-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="1d8e2-313">Na etapa final do hello, você está toodelete solicitadas Olá trabalho Olá pool e que foram criados pelo Olá *python_tutorial_client.py* script.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="1d8e2-314">Embora você não seja cobrado pelos trabalhos e pelas tarefas, *será* cobrado pelos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="1d8e2-315">Portanto, recomendamos que você aloque os nós conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="1d8e2-316">A exclusão de pools não utilizados pode fazer parte de seu processo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="1d8e2-317">Olá BatchServiceClient [JobOperations] [ py_job] e [PoolOperations] [ py_pool] têm métodos correspondentes de exclusão, que são chamado se Confirmar exclusão:</span><span class="sxs-lookup"><span data-stu-id="1d8e2-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="1d8e2-318">Tenha em mente que você será cobrado pelos recursos de computação, a exclusão dos pools não utilizados reduzirá o custo.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="1d8e2-319">Além disso, esteja ciente que a exclusão do pool de exclui todos os nós de computação no pool, e que os dados em nós hello serão irrecuperáveis depois Olá pool é excluído.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="1d8e2-320">Execute o script de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="1d8e2-320">Run hello sample script</span></span>
<span data-ttu-id="1d8e2-321">Quando você executa Olá *python_tutorial_client.py* script tutorial Olá [exemplo de código][github_article_samples], saída do console Olá é a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="1d8e2-322">Há uma pausa em `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` enquanto nós de computação do pool de saudação são criados, iniciado, e comandos Olá na tarefa de início do pool de saudação são executados.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="1d8e2-323">Saudação de uso [portal do Azure] [ azure_portal] toomonitor seu pool, nós de computação, trabalhos e tarefas durante e após a execução.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="1d8e2-324">Saudação de uso [portal do Azure] [ azure_portal] ou hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview Olá os recursos de armazenamento (contêineres e blobs) que são criados pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="1d8e2-325">Executar Olá *python_tutorial_client.py* script de dentro de saudação `azure-batch-samples/Python/Batch/article_samples` directory.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="1d8e2-326">Ele usa um caminho relativo para Olá `common.helpers` importação do módulo, para que você pode ver `ImportError: No module named 'common'` se você não executar o script de saudação do dentro dessa pasta.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="1d8e2-327">Tempo de execução típico é **cerca de 5 a 7 minutos** quando você executar o exemplo hello em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="1d8e2-328">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d8e2-328">Next steps</span></span>
<span data-ttu-id="1d8e2-329">Sinta-se livre toomake alterações muito*python_tutorial_client.py* e *python_tutorial_task.py* tooexperiment com diferentes cenários de computação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="1d8e2-330">Por exemplo, tente adicionar um atraso de execução muito*python_tutorial_task.py* toosimulate demoradas tarefas e monitorá-los no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="1d8e2-331">Tente adicionar mais tarefas ou ajustar Olá número de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="1d8e2-332">Adicionar lógica toocheck para e permitir o uso de saudação de um tempo de execução toospeed pool existente.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="1d8e2-333">Agora que você está familiarizado com o fluxo de trabalho básico de uma solução de lote Olá, é hora toodig em toohello de recursos adicionais do serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="1d8e2-334">Saudação de revisão [recursos de visão geral do Azure Batch](batch-api-basics.md) artigo, que é recomendável que você confirme o novo serviço toohello.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="1d8e2-335">Início na Olá outros artigos de desenvolvimento de lote em **desenvolvimento detalhado** em Olá [de aprendizado em lotes][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="1d8e2-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="1d8e2-336">Check-out de uma implementação de processamento de carga de trabalho do hello "top N palavras" com o lote em Olá [TopNWords] [ github_topnwords] exemplo.</span><span class="sxs-lookup"><span data-stu-id="1d8e2-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Criar contêineres no Armazenamento do Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Criar pool do Lote"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Criar trabalho em lotes"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Adicionar tarefas toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Monitorar tarefas"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Baixar a saída da tarefa do Armazenamento"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Fluxo de trabalho da solução do Lote (diagrama completo)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Credenciais do Lote no Portal"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Credenciais do Armazenamento no Portal"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Fluxo de trabalho da solução do Lote (diagrama mínimo)"
