---
title: dados de aaaUpload para trabalhos de Hadoop em HDInsight | Microsoft Docs
description: "Saiba como tooupload e acessar dados para trabalhos de Hadoop no HDInsight usando Olá CLI do Azure, Azure Storage Explorer, Azure PowerShell, linha de comando do Hadoop hello ou Sqoop."
keywords: hadoop de etl, inserindo dados no hadoop, carregar dados no hadoop
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="4e7d0-104">Carregar dados para trabalhos do Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e7d0-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="4e7d0-105">O Azure HDInsight oferece um HDFS (Sistema de Arquivos Distribuído) do Hadoop completo no armazenamento de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="4e7d0-106">Ele foi projetado como uma extensão HDFS tooprovide uma perfeita experiência toocustomers.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="4e7d0-107">Ele permite que todo o conjunto de componentes em Olá Hadoop ecossistema toooperate diretamente nos dados de saudação gerencia hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="4e7d0-108">O armazenamento de blob do Azure e o HDFS são sistemas de arquivos distintos otimizados para armazenamento de dados e computação nesses dados.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="4e7d0-109">Para obter informações sobre os benefícios de saudação do uso de armazenamento de BLOBs do Azure, consulte [armazenamento de BLOBs do Azure Use com HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="4e7d0-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="4e7d0-110">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="4e7d0-110">**Prerequisites**</span></span>

<span data-ttu-id="4e7d0-111">Observe Olá requisito a seguir antes de começar:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="4e7d0-112">Um cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="4e7d0-113">Para obter instruções, consulte [Introdução ao Azure HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="4e7d0-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="4e7d0-114">Por que o armazenamento de blob?</span><span class="sxs-lookup"><span data-stu-id="4e7d0-114">Why blob storage?</span></span>
<span data-ttu-id="4e7d0-115">HDInsight do Azure clusters normalmente são implantados toorun trabalhos de MapReduce e clusters hello serão descartados depois de concluir essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="4e7d0-116">Manter os dados de saudação em clusters HDFS Olá após a conclusão computações seria uma forma caro toostore esses dados.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="4e7d0-117">Armazenamento de BLOBs do Azure é altamente disponível, altamente escalonável e de alta capacidade, a opção de armazenamento de baixo custo e podem ser compartilhadas para dados que são processada usando HDInsight de toobe.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="4e7d0-118">Armazenando dados em um blob permite que os clusters de HDInsight Olá que são usados para computação toobe lançado com segurança sem perda de dados.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="4e7d0-119">Diretórios</span><span class="sxs-lookup"><span data-stu-id="4e7d0-119">Directories</span></span>
<span data-ttu-id="4e7d0-120">Os contêineres de armazenamento de blob do Azure armazenam dados como pares de chave/valor e não há nenhuma hierarquia de diretório.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="4e7d0-121">No entanto hello "/" caractere pode ser usado em Olá nome da chave toomake ele aparece como se um arquivo é armazenado em uma estrutura de diretório.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="4e7d0-122">O HDInsight os vê como se fossem diretórios reais.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="4e7d0-123">Por exemplo, a chave de um blob pode ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="4e7d0-124">Nenhum diretório real de "entrado" existe, mas devido a presença de toohello de saudação caractere "/" no nome da chave Olá, ele tem a aparência de saudação de um caminho de arquivo.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="4e7d0-125">Por isso, se você usar as ferramentas do Gerenciador do Azure, poderá perceber alguns arquivos de 0 byte.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="4e7d0-126">Esses arquivos têm duas finalidades:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-126">These files serve two purposes:</span></span>

* <span data-ttu-id="4e7d0-127">Se houver pastas vazias, eles marcam de existência de saudação da pasta hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="4e7d0-128">Armazenamento de BLOBs do Azure é bastante inteligente tooknow que exista um blob denominado foo/barra, há uma pasta chamada **foo**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="4e7d0-129">Mas Olá toosignify de maneira somente uma pasta vazia chamada **foo** é ter esse arquivo especial de 0 byte em vigor.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="4e7d0-130">Mantenham metadados especial que é necessário por Olá Hadoop sistema de arquivos, especialmente permissões hello e proprietários para pastas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="4e7d0-131">Utilitários de linha de comando</span><span class="sxs-lookup"><span data-stu-id="4e7d0-131">Command-line utilities</span></span>
<span data-ttu-id="4e7d0-132">A Microsoft fornece Olá toowork utilitários com o armazenamento de BLOBs do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="4e7d0-133">Ferramenta</span><span class="sxs-lookup"><span data-stu-id="4e7d0-133">Tool</span></span> | <span data-ttu-id="4e7d0-134">Linux</span><span class="sxs-lookup"><span data-stu-id="4e7d0-134">Linux</span></span> | <span data-ttu-id="4e7d0-135">OS X</span><span class="sxs-lookup"><span data-stu-id="4e7d0-135">OS X</span></span> | <span data-ttu-id="4e7d0-136">Windows</span><span class="sxs-lookup"><span data-stu-id="4e7d0-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="4e7d0-137">[Interface de Linha de Comando do Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="4e7d0-138">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-138">✔</span></span> |<span data-ttu-id="4e7d0-139">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-139">✔</span></span> |<span data-ttu-id="4e7d0-140">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-140">✔</span></span> |
| <span data-ttu-id="4e7d0-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="4e7d0-142">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-142">✔</span></span> |
| <span data-ttu-id="4e7d0-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="4e7d0-144">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-144">✔</span></span> |
| [<span data-ttu-id="4e7d0-145">Comando do Hadoop</span><span class="sxs-lookup"><span data-stu-id="4e7d0-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="4e7d0-146">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-146">✔</span></span> |<span data-ttu-id="4e7d0-147">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-147">✔</span></span> |<span data-ttu-id="4e7d0-148">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="4e7d0-149">Embora Olá CLI do Azure, Azure PowerShell e AzCopy podem ser usados de fora do Azure, Olá Hadoop comando só está disponível no cluster do HDInsight hello e só permite carregar dados do sistema de arquivos local Olá para armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="4e7d0-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4e7d0-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="4e7d0-151">Olá CLI do Azure é uma ferramenta de plataforma cruzada que permite que você toomanage do Azure services.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="4e7d0-152">Use Olá armazenamento de Blob etapas tooupload dados tooAzure a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="4e7d0-153">[Instalar e configurar Olá CLI do Azure para Mac, Linux e Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="4e7d0-154">Abra um prompt de comando, bash ou outro shell e usar Olá tooauthenticate tooyour assinatura do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="4e7d0-155">Quando solicitado, digite Olá nome de usuário e senha para a sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="4e7d0-156">Digite hello contas de armazenamento de saudação do comando toolist para sua assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="4e7d0-157">Conta de armazenamento Olá Select que contém o blob Olá toowork, você deseja usar Olá comando tooretrieve Olá chave desta conta a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="4e7d0-158">Isso deve retornar as chaves **Primária** e **Secundária**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="4e7d0-159">Saudação de cópia **primário** valor de chave, pois ele será usado nas etapas Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="4e7d0-160">Use Olá tooretrieve comando uma lista de contêineres de blob na conta de armazenamento Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="4e7d0-161">Use Olá tooupload comandos a seguir e baixar arquivos toohello blob:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="4e7d0-162">tooupload um arquivo:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="4e7d0-163">toodownload um arquivo:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="4e7d0-164">Se você sempre trabalhará com hello mesma conta de armazenamento, você pode definir Olá seguintes variáveis de ambiente em vez de especificar a conta de saudação e a chave para cada comando:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="4e7d0-165">**AZURE\_armazenamento\_conta**: nome de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="4e7d0-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="4e7d0-166">**AZURE\_armazenamento\_acesso\_chave**: chave de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="4e7d0-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="4e7d0-167"><a id="powershell"></a>PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="4e7d0-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="4e7d0-168">PowerShell do Azure é um ambiente de script que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de suas cargas de trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="4e7d0-169">Para obter informações sobre como configurar toorun sua estação de trabalho do PowerShell do Azure, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="4e7d0-170">**tooupload tooAzure um arquivo local armazenamento de Blob**</span><span class="sxs-lookup"><span data-stu-id="4e7d0-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="4e7d0-171">Console do Azure PowerShell Olá aberta com as instruções no [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="4e7d0-172">Defina valores Olá Olá cinco primeiros variáveis em Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="4e7d0-173">Olá colar o script em hello Azure PowerShell console toorun-toocopy arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="4e7d0-174">Por exemplo, PowerShell scripts criados toowork com HDInsight, consulte [ferramentas HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="4e7d0-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="4e7d0-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="4e7d0-176">AzCopy é uma ferramenta de linha de comando que é projetado toosimplify tarefa de saudação de transferência de dados dentro e fora de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="4e7d0-177">Você pode usá-lo como uma ferramenta independente ou incorporar essa ferramenta em um aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="4e7d0-178">[Baixar o AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="4e7d0-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="4e7d0-179">Olá sintaxe AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="4e7d0-180">Para saber mais, consulte [AzCopy – Carregando/baixando arquivos para Blobs do Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="4e7d0-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="4e7d0-181"><a id="commandline"></a>Linha de comando do Hadoop</span><span class="sxs-lookup"><span data-stu-id="4e7d0-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="4e7d0-182">linha de comando do Hadoop Olá só é útil para armazenar dados no armazenamento de blob quando dados saudação já estão presentes no nó principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="4e7d0-183">Saudação de toouse ordem Hadoop comando, você deve primeiro se conectar toohello um nó principal usando um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="4e7d0-184">**HDInsight baseado em Windows**: [conecte-se usando a área de trabalho remota](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="4e7d0-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="4e7d0-185">**HDInsight baseados em Linux**: conectar-se usando o SSH ([Olá comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) ou [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="4e7d0-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="4e7d0-186">Uma vez conectado, você pode usar o hello tooupload sintaxe toostorage um arquivo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="4e7d0-187">Por exemplo, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="4e7d0-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="4e7d0-188">Como sistema de arquivos padrão Olá para HDInsight está no armazenamento de BLOBs do Azure, /example/data.txt, na verdade, está no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="4e7d0-189">Você também pode consultar o arquivo toohello como:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="4e7d0-190">ou o</span><span class="sxs-lookup"><span data-stu-id="4e7d0-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="4e7d0-191">Para obter uma lista dos outros comandos Hadoop que trabalham com os arquivos, consulte [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="4e7d0-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="4e7d0-192">Em clusters de HBase, tamanho de bloco saudação padrão usado quando a gravação de dados é 256KB.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="4e7d0-193">Enquanto isso funciona bem quando usando APIs do HBase ou APIs REST, usando Olá `hadoop` ou `hdfs dfs` dados de toowrite comandos maiores ~ 12 GB resulta em um erro.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="4e7d0-194">Consulte Olá [exceção de armazenamento para gravação no blob](#storageexception) seção abaixo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="4e7d0-195">Clientes gráficos</span><span class="sxs-lookup"><span data-stu-id="4e7d0-195">Graphical clients</span></span>
<span data-ttu-id="4e7d0-196">Também há vários aplicativos que fornecem uma interface gráfica para trabalhar com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="4e7d0-197">a seguir Olá é uma lista de alguns desses aplicativos:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="4e7d0-198">Cliente</span><span class="sxs-lookup"><span data-stu-id="4e7d0-198">Client</span></span> | <span data-ttu-id="4e7d0-199">Linux</span><span class="sxs-lookup"><span data-stu-id="4e7d0-199">Linux</span></span> | <span data-ttu-id="4e7d0-200">OS X</span><span class="sxs-lookup"><span data-stu-id="4e7d0-200">OS X</span></span> | <span data-ttu-id="4e7d0-201">Windows</span><span class="sxs-lookup"><span data-stu-id="4e7d0-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="4e7d0-202">Ferramentas do Microsoft Visual Studio para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e7d0-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="4e7d0-203">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-203">✔</span></span> |<span data-ttu-id="4e7d0-204">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-204">✔</span></span> |<span data-ttu-id="4e7d0-205">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-205">✔</span></span> |
| [<span data-ttu-id="4e7d0-206">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4e7d0-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="4e7d0-207">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-207">✔</span></span> |<span data-ttu-id="4e7d0-208">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-208">✔</span></span> |<span data-ttu-id="4e7d0-209">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-209">✔</span></span> |
| [<span data-ttu-id="4e7d0-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="4e7d0-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="4e7d0-211">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-211">✔</span></span> |
| [<span data-ttu-id="4e7d0-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="4e7d0-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="4e7d0-213">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-213">✔</span></span> |
| [<span data-ttu-id="4e7d0-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="4e7d0-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="4e7d0-215">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-215">✔</span></span> |
| [<span data-ttu-id="4e7d0-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="4e7d0-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="4e7d0-217">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-217">✔</span></span> |<span data-ttu-id="4e7d0-218">✔</span><span class="sxs-lookup"><span data-stu-id="4e7d0-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="4e7d0-219">Ferramentas do Visual Studio para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e7d0-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="4e7d0-220">Para obter mais informações, consulte [recursos vinculados do hello navegar](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="4e7d0-221"><a id="storageexplorer"></a>Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4e7d0-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="4e7d0-222">*Azure Storage Explorer* é uma ferramenta útil para inspecionar e alterar dados de saudação em blobs.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="4e7d0-223">É uma ferramenta de software livre que pode ser baixada em [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="4e7d0-224">Olá código-fonte está disponível a partir deste link também.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="4e7d0-225">Antes de usar a ferramenta hello, você deve saber a sua chave de nome e uma conta de conta do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="4e7d0-226">Para obter instruções sobre como obter essas informações, consulte hello "como: exibir, copiar e regenerar as contas de armazenamento de chaves de acesso" seção [criar, gerenciar ou excluir uma conta de armazenamento][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="4e7d0-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="4e7d0-227">Execute o Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="4e7d0-228">Se isso for Olá primeira vez você executou Olá Storage Explorer, você será solicitado para Olá **nome da conta _Storage** e **chave da conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="4e7d0-229">Se você tiver executado antes, use Olá **adicionar** botão tooadd um novo nome de conta de armazenamento e a chave.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="4e7d0-230">Digite hello nome e chave Olá conta de armazenamento usada por seu cluster HDInsight e, em seguida, selecione **Salvar & Abrir**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="4e7d0-232">Na lista de Olá da esquerda de toohello contêineres da interface de saudação, clique em nome Olá Olá do contêiner de que está associado ao seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="4e7d0-233">Por padrão, é o nome de saudação do cluster do HDInsight Olá, mas pode ser diferente se você digitou um nome específico ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="4e7d0-234">Na barra de ferramentas Olá, selecione o ícone de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-234">From hello tool bar, select hello upload icon.</span></span>

    ![Barra de ferramentas com ícone de upload destacado](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="4e7d0-236">Especifique um tooupload de arquivo e, em seguida, clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="4e7d0-237">Quando solicitado, selecione **carregar** raiz de toohello de arquivos tooupload Olá Olá do contêiner de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="4e7d0-238">Se você quiser caminho específico de tooa tooupload de arquivo hello, digite o caminho de saudação no hello **destino** campo e, em seguida, selecione **carregar**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Caixa de diálogo de upload do arquivo](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="4e7d0-240">Depois que o arquivo hello concluiu o carregamento, você pode usá-lo de trabalhos no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="4e7d0-241">Montar o Armazenamento de Blob do Azure como uma unidade Local</span><span class="sxs-lookup"><span data-stu-id="4e7d0-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="4e7d0-242">Confira [Montar o Armazenamento de Blob do Azure como uma unidade Local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="4e7d0-243">Serviços</span><span class="sxs-lookup"><span data-stu-id="4e7d0-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="4e7d0-244">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="4e7d0-244">Azure Data Factory</span></span>
<span data-ttu-id="4e7d0-245">Olá serviço fábrica de dados do Azure é um serviço totalmente gerenciado para compor serviços de movimentação de dados, processamento de dados e armazenamento de dados em pipelines de produção de dados simplificada, escalonável e confiável.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="4e7d0-246">A fábrica de dados do Azure pode ser usado toomove dados no armazenamento de BLOBs do Azure, ou toocreate pipelines de dados que usam recursos de HDInsight diretamente como Hive e Pig.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="4e7d0-247">Para obter mais informações, consulte Olá [documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="4e7d0-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="4e7d0-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="4e7d0-249">Sqoop é uma ferramenta desenvolvida de dados tootransfer entre Hadoop e bancos de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="4e7d0-250">Você pode usá-lo tooimport dados de um sistema de gerenciamento de banco de dados relacional (RDBMS), como SQL Server, MySQL ou Oracle no sistema de arquivo hello distribuído de Hadoop (HDFS), transformar dados Olá no Hadoop MapReduce ou Hive e, em seguida, exportar dados de saudação volta para um RDBMS.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="4e7d0-251">Para obter mais informações, consulte [Usar Sqoop com HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="4e7d0-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="4e7d0-252">SDKs de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="4e7d0-252">Development SDKs</span></span>
<span data-ttu-id="4e7d0-253">Armazenamento de BLOBs do Azure também pode ser acessado usando um SDK do Azure de saudação linguagens de programação a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="4e7d0-254">.NET</span><span class="sxs-lookup"><span data-stu-id="4e7d0-254">.NET</span></span>
* <span data-ttu-id="4e7d0-255">Java</span><span class="sxs-lookup"><span data-stu-id="4e7d0-255">Java</span></span>
* <span data-ttu-id="4e7d0-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="4e7d0-256">Node.js</span></span>
* <span data-ttu-id="4e7d0-257">PHP</span><span class="sxs-lookup"><span data-stu-id="4e7d0-257">PHP</span></span>
* <span data-ttu-id="4e7d0-258">Python</span><span class="sxs-lookup"><span data-stu-id="4e7d0-258">Python</span></span>
* <span data-ttu-id="4e7d0-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="4e7d0-259">Ruby</span></span>

<span data-ttu-id="4e7d0-260">Para obter mais informações sobre como instalar os SDKs do Azure hello, consulte [downloads do Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="4e7d0-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4e7d0-261">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="4e7d0-261">Troubleshooting</span></span>
### <span data-ttu-id="4e7d0-262"><a id="storageexception"></a>Exceção de armazenamento para gravar no blob</span><span class="sxs-lookup"><span data-stu-id="4e7d0-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="4e7d0-263">**Sintomas**: ao usar o hello `hadoop` ou `hdfs dfs` comandos toowrite arquivos que são ~ 12 GB ou maior, em um cluster HBase, você pode encontrar hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="4e7d0-264">**Causa**: HBase em HDInsight clusters de tamanho de bloco de tooa padrão de 256 KB ao escrever armazenamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="4e7d0-265">Enquanto isso funciona para APIs do HBase ou APIs REST, resultará em um erro ao usar o hello `hadoop` ou `hdfs dfs` utilitários de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="4e7d0-266">**Resolução**: Use `fs.azure.write.request.size` toospecify um maior tamanho de bloco.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="4e7d0-267">Você pode fazer isso em uma base por uso usando Olá `-D` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="4e7d0-268">Olá, a seguir é um exemplo que usa esse parâmetro com hello `hadoop` comando:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="4e7d0-269">Você também pode aumentar o valor de saudação do `fs.azure.write.request.size` global usando o Ambari.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="4e7d0-270">Olá etapas a seguir podem ser usado toochange valor de saudação em Olá da interface do usuário do Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="4e7d0-271">Em seu navegador, vá toohello Ambari Web UI para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="4e7d0-272">Isso é https://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="4e7d0-273">Quando solicitado, insira o nome de saudação do administrador e a senha para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="4e7d0-274">Olá lado esquerdo da tela hello, selecione **HDFS**e, em seguida, selecione Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="4e7d0-275">Em Olá **filtro...**  , digite `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="4e7d0-276">Isso exibirá o campo hello e o valor atual no meio de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="4e7d0-277">Altere o valor de saudação de 262144 (256KB) toohello novo valor.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="4e7d0-278">Por exemplo, 4194304 (4 MB).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-278">For example, 4194304 (4MB).</span></span>

![Imagem de alterar o valor de saudação por meio da interface do usuário do Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="4e7d0-280">Para obter mais informações sobre como usar o Ambari, consulte [gerenciar clusters HDInsight usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e7d0-281">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e7d0-281">Next steps</span></span>
<span data-ttu-id="4e7d0-282">Agora que você sabe como ler dados tooget em HDInsight, Olá toolearn artigos a seguir como tooperform análise:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="4e7d0-283">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="4e7d0-284">[Enviar trabalhos Hadoop de forma programática][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="4e7d0-285">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4e7d0-286">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4e7d0-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
