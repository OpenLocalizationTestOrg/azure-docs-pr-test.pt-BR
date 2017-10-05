---
title: Carregar dados para trabalhos do Hadoop no HDInsight | Microsoft Docs
description: Saiba como carregar e acessar os dados de trabalhos do Hadoop no HDInsight usando o Azure CLI, Azure Storage Explorer, Azure PowerShell, a linha de comando do Hadoop ou o Sqoop.
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="e5b4e-104">Carregar dados para trabalhos do Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5b4e-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="e5b4e-105">O Azure HDInsight oferece um HDFS (Sistema de Arquivos Distribuído) do Hadoop completo no armazenamento de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="e5b4e-106">Ele foi projetado como uma extensão HDFS para fornecer uma experiência perfeita aos clientes.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="e5b4e-107">Ele permite que o conjunto completo de componentes no ecossistema do Hadoop opere diretamente nos dados que ele gerencia.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="e5b4e-108">O armazenamento de blob do Azure e o HDFS são sistemas de arquivos distintos otimizados para armazenamento de dados e computação nesses dados.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="e5b4e-109">Para ver informações sobre os benefícios de usar o Armazenamento de Blobs do Azure, consulte [Usar o Armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="e5b4e-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="e5b4e-110">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="e5b4e-110">**Prerequisites**</span></span>

<span data-ttu-id="e5b4e-111">Observe os seguintes requisitos antes de começar:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="e5b4e-112">Um cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="e5b4e-113">Para obter instruções, consulte [Introdução ao Azure HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="e5b4e-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="e5b4e-114">Por que o armazenamento de blob?</span><span class="sxs-lookup"><span data-stu-id="e5b4e-114">Why blob storage?</span></span>
<span data-ttu-id="e5b4e-115">Os clusters do Azure HDInsight normalmente são implantados para executar trabalhos do MapReduce e são removidos quando esses trabalhos são concluídos.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="e5b4e-116">A manutenção dos dados nos clusters HDFS após a conclusão dos cálculos seria uma maneira cara de armazenar esses dados.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="e5b4e-117">O armazenamento de Blob do Azure é altamente disponível, escalonável, com alta capacidade, baixo custo e uma opção de armazenamento compartilhável para dados a serem processados usando o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="e5b4e-118">O armazenamento de dados em um blob permite que os clusters HDInsight usados para computação sejam liberados sem que ocorra perda de dados.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="e5b4e-119">Diretórios</span><span class="sxs-lookup"><span data-stu-id="e5b4e-119">Directories</span></span>
<span data-ttu-id="e5b4e-120">Os contêineres de armazenamento de blob do Azure armazenam dados como pares de chave/valor e não há nenhuma hierarquia de diretório.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="e5b4e-121">No entanto, o caractere "/" pode ser usado dentro do nome de chave para parecer que um arquivo está armazenado em uma estrutura de diretório.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="e5b4e-122">O HDInsight os vê como se fossem diretórios reais.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="e5b4e-123">Por exemplo, a chave de um blob pode ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="e5b4e-124">Não existe nenhum diretório de "entrada" real, mas devido à presença do caractere "/" no nome da chave, ele parece um caminho de arquivo.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="e5b4e-125">Por isso, se você usar as ferramentas do Gerenciador do Azure, poderá perceber alguns arquivos de 0 byte.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="e5b4e-126">Esses arquivos têm duas finalidades:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-126">These files serve two purposes:</span></span>

* <span data-ttu-id="e5b4e-127">Se houver pastas vazias, eles marcam a existência da pasta.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="e5b4e-128">O Armazenamento de blob do Azure é inteligente o suficiente para saber que se existir um blob denominado foo/bar, haverá uma pasta chamada **foo**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="e5b4e-129">Mas se você desejar ter uma pasta vazia chamada **foo** , a única maneira de indicar isso é tendo esse arquivo de 0 byte especial no lugar.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="e5b4e-130">Elas contêm alguns metadados especiais de que o sistema de arquivos Hadoop precisa, especialmente as permissões e os proprietários das pastas.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="e5b4e-131">Utilitários de linha de comando</span><span class="sxs-lookup"><span data-stu-id="e5b4e-131">Command-line utilities</span></span>
<span data-ttu-id="e5b4e-132">A Microsoft fornece os seguintes utilitários para trabalhar com armazenamento de Blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="e5b4e-133">Ferramenta</span><span class="sxs-lookup"><span data-stu-id="e5b4e-133">Tool</span></span> | <span data-ttu-id="e5b4e-134">Linux</span><span class="sxs-lookup"><span data-stu-id="e5b4e-134">Linux</span></span> | <span data-ttu-id="e5b4e-135">OS X</span><span class="sxs-lookup"><span data-stu-id="e5b4e-135">OS X</span></span> | <span data-ttu-id="e5b4e-136">Windows</span><span class="sxs-lookup"><span data-stu-id="e5b4e-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="e5b4e-137">[Interface de Linha de Comando do Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="e5b4e-138">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-138">✔</span></span> |<span data-ttu-id="e5b4e-139">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-139">✔</span></span> |<span data-ttu-id="e5b4e-140">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-140">✔</span></span> |
| <span data-ttu-id="e5b4e-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="e5b4e-142">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-142">✔</span></span> |
| <span data-ttu-id="e5b4e-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="e5b4e-144">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-144">✔</span></span> |
| [<span data-ttu-id="e5b4e-145">Comando do Hadoop</span><span class="sxs-lookup"><span data-stu-id="e5b4e-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="e5b4e-146">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-146">✔</span></span> |<span data-ttu-id="e5b4e-147">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-147">✔</span></span> |<span data-ttu-id="e5b4e-148">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="e5b4e-149">Enquanto o CLI do Azure, o Azure PowerShell e o AzCopy podem ser usados fora do Azure, o comando Hadoop só está disponível no cluster HDInsight e só permite carregar dados do sistema de arquivos local para o armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="e5b4e-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e5b4e-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="e5b4e-151">O Azure CLI é uma ferramenta de plataforma cruzada que permite que você gerencie os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="e5b4e-152">Use as seguintes etapas para carregar dados no armazenamento de Blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="e5b4e-153">[Instalar e configurar o Azure CLI para Mac, Linux e Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="e5b4e-154">Abra um prompt de comando, bash ou outro shell e use os dados a seguir para autenticar a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="e5b4e-155">Quando solicitado, insira o nome de usuário e senha para a sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="e5b4e-156">Use o seguinte comando para listar sites para as contas de armazenamento da sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="e5b4e-157">Selecione a conta de armazenamento que contém o blob com que você deseja trabalhar e use o seguinte comando para recuperar a chave para esta conta:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="e5b4e-158">Isso deve retornar as chaves **Primária** e **Secundária**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="e5b4e-159">Copie o valor de chave **Primária** , já que ele será usado nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="e5b4e-160">Use o seguinte comando para recuperar uma lista de contêineres de blob na conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="e5b4e-161">Use os seguintes comandos para carregar e baixar arquivos para o blob:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="e5b4e-162">Para carregar um arquivo:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="e5b4e-163">Para baixar um arquivo:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="e5b4e-164">Se você for sempre trabalhar com a mesma conta de armazenamento, pode definir as seguintes variáveis de ambiente em vez de especificar a conta e a chave para cada comando:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="e5b4e-165">**AZURE\_STORAGE\_ACCOUNT**: o nome da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e5b4e-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="e5b4e-166">**AZURE\_STORAGE\_ACCESS\_KEY**: a chave da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e5b4e-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="e5b4e-167"><a id="powershell"></a>PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b4e-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="e5b4e-168">O Azure PowerShell é um ambiente de script que você pode usar para controlar e automatizar a implantação e o gerenciamento de suas cargas de trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="e5b4e-169">Para saber mais sobre como configurar sua estação de trabalho para executar o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="e5b4e-170">**Para carregar um arquivo local para o Armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="e5b4e-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="e5b4e-171">Abra o console do PowerShell do Azure conforme instruído em [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="e5b4e-172">Defina os valores das cinco primeiras variáveis no script a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="e5b4e-173">Cole o script no console do Azure PowerShell para executá-lo para copiar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="e5b4e-174">Por exemplo, os scripts do PowerShell criados para funcionar com o HDInsight, consulte [Ferramentas HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="e5b4e-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="e5b4e-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="e5b4e-176">O AzCopy é uma ferramenta de linha de comando destinada a simplificar a tarefa de transferir dados de e para uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="e5b4e-177">Você pode usá-lo como uma ferramenta independente ou incorporar essa ferramenta em um aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="e5b4e-178">[Baixar o AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="e5b4e-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="e5b4e-179">A sintaxe do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="e5b4e-180">Para saber mais, consulte [AzCopy – Carregando/baixando arquivos para Blobs do Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="e5b4e-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="e5b4e-181"><a id="commandline"></a>Linha de comando do Hadoop</span><span class="sxs-lookup"><span data-stu-id="e5b4e-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="e5b4e-182">A linha de comando do Hadoop só é útil para armazenar dados no armazenamento de blob quando os dados já estão presentes no nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="e5b4e-183">Para usar o comando Hadoop, primeiro você deve se conectar ao nó de cabeçalho usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="e5b4e-184">**HDInsight baseado em Windows**: [conecte-se usando a área de trabalho remota](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="e5b4e-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="e5b4e-185">**HDInsight baseado em Linux**: conecte-se usando SSH ([o comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) ou [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="e5b4e-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="e5b4e-186">Uma vez conectado, você pode usar a seguinte sintaxe para carregar um arquivo no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="e5b4e-187">Por exemplo, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="e5b4e-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="e5b4e-188">Como o sistema de arquivos padrão para o HDInsight está no armazenamento de Blob do Azure, /example/data.txt está, na verdade, no armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="e5b4e-189">Você também pode fazer referência ao arquivo como:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="e5b4e-190">ou o</span><span class="sxs-lookup"><span data-stu-id="e5b4e-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="e5b4e-191">Para obter uma lista dos outros comandos Hadoop que trabalham com os arquivos, consulte [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="e5b4e-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="e5b4e-192">Em clusters HBase, o tamanho do bloco padrão usado na gravação de dados é de 256 KB.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="e5b4e-193">Embora isso funcione bem com APIs HBase ou APIs REST, usar os comandos `hadoop` ou `hdfs dfs` para gravar dados com mais de, aproximadamente, 12 GB resulta em um erro.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="e5b4e-194">Confira a seção abaixo [Exceção de armazenamento para gravar no blob](#storageexception) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="e5b4e-195">Clientes gráficos</span><span class="sxs-lookup"><span data-stu-id="e5b4e-195">Graphical clients</span></span>
<span data-ttu-id="e5b4e-196">Também há vários aplicativos que fornecem uma interface gráfica para trabalhar com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="e5b4e-197">Segue uma lista de alguns desses aplicativos:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="e5b4e-198">Cliente</span><span class="sxs-lookup"><span data-stu-id="e5b4e-198">Client</span></span> | <span data-ttu-id="e5b4e-199">Linux</span><span class="sxs-lookup"><span data-stu-id="e5b4e-199">Linux</span></span> | <span data-ttu-id="e5b4e-200">OS X</span><span class="sxs-lookup"><span data-stu-id="e5b4e-200">OS X</span></span> | <span data-ttu-id="e5b4e-201">Windows</span><span class="sxs-lookup"><span data-stu-id="e5b4e-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="e5b4e-202">Ferramentas do Microsoft Visual Studio para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5b4e-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="e5b4e-203">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-203">✔</span></span> |<span data-ttu-id="e5b4e-204">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-204">✔</span></span> |<span data-ttu-id="e5b4e-205">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-205">✔</span></span> |
| [<span data-ttu-id="e5b4e-206">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b4e-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="e5b4e-207">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-207">✔</span></span> |<span data-ttu-id="e5b4e-208">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-208">✔</span></span> |<span data-ttu-id="e5b4e-209">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-209">✔</span></span> |
| [<span data-ttu-id="e5b4e-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="e5b4e-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="e5b4e-211">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-211">✔</span></span> |
| [<span data-ttu-id="e5b4e-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="e5b4e-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="e5b4e-213">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-213">✔</span></span> |
| [<span data-ttu-id="e5b4e-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="e5b4e-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="e5b4e-215">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-215">✔</span></span> |
| [<span data-ttu-id="e5b4e-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="e5b4e-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="e5b4e-217">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-217">✔</span></span> |<span data-ttu-id="e5b4e-218">✔</span><span class="sxs-lookup"><span data-stu-id="e5b4e-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="e5b4e-219">Ferramentas do Visual Studio para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5b4e-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="e5b4e-220">Para saber mais, veja [Navegar nos recursos vinculados](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="e5b4e-221"><a id="storageexplorer"></a>Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b4e-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="e5b4e-222">*Gerenciador de Armazenamento do Azure* é uma ferramenta útil para inspecionar e alterar os dados nos blobs.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="e5b4e-223">É uma ferramenta de software livre que pode ser baixada em [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="e5b4e-224">O código-fonte está disponível também neste link.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="e5b4e-225">Para usar a ferramenta, conheça sua chave e seu nome da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="e5b4e-226">Para saber mais sobre como obter essas informações, confira a seção “Como exibir, copiar e regenerar chaves de acesso de armazenamento” em [Criar, gerenciar ou excluir uma conta de armazenamento][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="e5b4e-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="e5b4e-227">Execute o Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="e5b4e-228">Se esta for a primeira vez que você executou o Gerenciador de Armazenamento, será solicitado que você insira o **_Nome da conta de armazenamento** e a **Chave da conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="e5b4e-229">Caso o tenha executado antes, use botão **Adicionar** para adicionar um novo nome e chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="e5b4e-230">Insira o nome e a chave da conta de armazenamento usada pelo cluster HDInsight e, depois, selecione **SALVAR E ABRIR**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="e5b4e-232">Na lista de contêineres, clique no nome do contêiner que está associado ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="e5b4e-233">Por padrão, esse é o nome do cluster do HDInsight, mas pode ser diferente se você inseriu um nome específico ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="e5b4e-234">Na barra de ferramentas, selecione o ícone de upload.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-234">From the tool bar, select the upload icon.</span></span>

    ![Barra de ferramentas com ícone de upload destacado](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="e5b4e-236">Especifique um arquivo para carregar e **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="e5b4e-237">Quando solicitado, selecione **Carregar** para carregar o arquivo para a raiz do contêiner de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="e5b4e-238">Se você desejar carregar o arquivo em um caminho específico, digite o caminho no campo **Destino** e selecione **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Caixa de diálogo de upload do arquivo](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="e5b4e-240">Depois que o arquivo terminar de carregar, você pode usá-lo por meio dos trabalhos no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="e5b4e-241">Montar o Armazenamento de Blob do Azure como uma unidade Local</span><span class="sxs-lookup"><span data-stu-id="e5b4e-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="e5b4e-242">Confira [Montar o Armazenamento de Blob do Azure como uma unidade Local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="e5b4e-243">Serviços</span><span class="sxs-lookup"><span data-stu-id="e5b4e-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="e5b4e-244">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b4e-244">Azure Data Factory</span></span>
<span data-ttu-id="e5b4e-245">A Fábrica de Dados do Azure é um serviço completamente gerenciado para compor serviços de armazenamento, processamento e movimentação de dados em pipelines de produção de dados simplificada, escalonável e confiável.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="e5b4e-246">O Azure Data Factory pode ser usado para mover dados para o Armazenamento de Blob do Azure, ou para criar pipelines de dados que usam diretamente os recursos do HDInsight como Hive e Pig.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="e5b4e-247">Para obter mais informações, consulte a [Documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="e5b4e-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="e5b4e-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="e5b4e-249">O Sqoop é uma ferramenta desenvolvida para transferir dados entre bancos de dados relacionais e o Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="e5b4e-250">Você pode usá-lo para importar dados de um RDBMS (sistema de gerenciamento de banco de dados relacional), como SQL Server, MySQL ou Oracle para o HDFS (Sistema de Arquivos Distribuído) do Hadoop, transformar os dados no Hadoop com o MapReduce ou o Hive e, em seguida, exportar os dados de volta para um RDBMS.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="e5b4e-251">Para obter mais informações, consulte [Usar Sqoop com HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="e5b4e-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="e5b4e-252">SDKs de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="e5b4e-252">Development SDKs</span></span>
<span data-ttu-id="e5b4e-253">O Armazenamento de Blob do Azure também pode ser acessado usando um SDK do Azure com as seguintes linguagens de programação:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="e5b4e-254">.NET</span><span class="sxs-lookup"><span data-stu-id="e5b4e-254">.NET</span></span>
* <span data-ttu-id="e5b4e-255">Java</span><span class="sxs-lookup"><span data-stu-id="e5b4e-255">Java</span></span>
* <span data-ttu-id="e5b4e-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="e5b4e-256">Node.js</span></span>
* <span data-ttu-id="e5b4e-257">PHP</span><span class="sxs-lookup"><span data-stu-id="e5b4e-257">PHP</span></span>
* <span data-ttu-id="e5b4e-258">Python</span><span class="sxs-lookup"><span data-stu-id="e5b4e-258">Python</span></span>
* <span data-ttu-id="e5b4e-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="e5b4e-259">Ruby</span></span>

<span data-ttu-id="e5b4e-260">Para obter mais informações sobre como instalar os SDKs do Azure, consulte [Downloads do Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e5b4e-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e5b4e-261">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e5b4e-261">Troubleshooting</span></span>
### <span data-ttu-id="e5b4e-262"><a id="storageexception"></a>Exceção de armazenamento para gravar no blob</span><span class="sxs-lookup"><span data-stu-id="e5b4e-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="e5b4e-263">**Sintomas**: ao usar os comandos `hadoop` ou `hdfs dfs` para gravar arquivos que tenham aproximadamente 12 GB ou mais em um cluster HBase, você pode encontrar o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="e5b4e-264">**Causa**: os clusters HBase no HDInsight são padronizados para um tamanho de bloco de 256 KB na gravação no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="e5b4e-265">Embora isso funcione para APIs HBase ou APIs REST, resultará em erro no uso de utilitários de linha comando `hadoop` ou `hdfs dfs`.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="e5b4e-266">**Resolução**: use `fs.azure.write.request.size` para especificar um tamanho de bloco maior.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="e5b4e-267">Isso pode ser feito a cada uso com o parâmetro `-D`.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="e5b4e-268">Veja a seguir um exemplo de uso desse parâmetro com o comando `hadoop`:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="e5b4e-269">Você também pode aumentar o valor de `fs.azure.write.request.size` globalmente usando Ambari.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="e5b4e-270">As etapas a seguir podem ser usadas para alterar o valor na interface de usuário do Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="e5b4e-271">No navegador, acesse a interface de usuário do Ambari Web para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="e5b4e-272">Isto é, https://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="e5b4e-273">Quando solicitado, insira o nome de administrador e a senha de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="e5b4e-274">No lado esquerdo da tela, escolha **HDFS** e selecione a guia **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="e5b4e-275">No campo **Filtrar...**, insira `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="e5b4e-276">Isso exibirá o campo e o valor atual no meio da página.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="e5b4e-277">Altere o valor de 262144 (256 KB) para o novo valor.</span><span class="sxs-lookup"><span data-stu-id="e5b4e-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="e5b4e-278">Por exemplo, 4194304 (4 MB).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-278">For example, 4194304 (4MB).</span></span>

![Imagem de alteração de valor por meio da interface de usuário do Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="e5b4e-280">Para saber mais sobre como usar o Ambari, confira [Gerenciar clusters HDInsight interface de usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="e5b4e-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5b4e-281">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5b4e-281">Next steps</span></span>
<span data-ttu-id="e5b4e-282">Agora que você compreende como obter dados no HDInsight, leia os seguintes artigos para aprender a executar uma análise:</span><span class="sxs-lookup"><span data-stu-id="e5b4e-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="e5b4e-283">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="e5b4e-284">[Enviar trabalhos Hadoop de forma programática][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="e5b4e-285">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e5b4e-286">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e5b4e-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
