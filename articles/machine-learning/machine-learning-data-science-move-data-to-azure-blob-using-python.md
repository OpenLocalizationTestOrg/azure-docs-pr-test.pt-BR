---
title: Mover dados de e para o Armazenamento de Blobs do Azure usando Python | Microsoft Docs
description: Mover dados de e para o Armazenamento de Blobs do Azure usando Python
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="63fcf-103">Mover dados de e para o Armazenamento de Blobs do Azure usando Python</span><span class="sxs-lookup"><span data-stu-id="63fcf-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="63fcf-104">Este tópico descreve como listar, carregar e baixar blobs usando a API Python.</span><span class="sxs-lookup"><span data-stu-id="63fcf-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="63fcf-105">Com a API do Python fornecida no SDK do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="63fcf-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="63fcf-106">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="63fcf-106">Create a container</span></span>
* <span data-ttu-id="63fcf-107">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="63fcf-107">Upload a blob into a container</span></span>
* <span data-ttu-id="63fcf-108">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="63fcf-108">Download blobs</span></span>
* <span data-ttu-id="63fcf-109">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="63fcf-109">List the blobs in a container</span></span>
* <span data-ttu-id="63fcf-110">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="63fcf-110">Delete a blob</span></span>

<span data-ttu-id="63fcf-111">Para obter mais informações sobre como usar a API Python, consulte [Como usar o serviço de armazenamento de blob do Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="63fcf-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="63fcf-112">Se você estiver usando a VM que foi configurada com os scripts fornecidos pelas [Máquinas virtuais de ciência de dados no Azure](machine-learning-data-science-virtual-machines.md), o AzCopy já estará instalado na VM.</span><span class="sxs-lookup"><span data-stu-id="63fcf-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="63fcf-113">Para obter uma introdução completa ao Armazenamento de Blobs do Azure, consulte [Noções básicas do Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e [Serviço de Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="63fcf-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="63fcf-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="63fcf-114">Prerequisites</span></span>
<span data-ttu-id="63fcf-115">Este documento pressupõe que você tenha uma assinatura, uma conta de armazenamento do Azure e a chave de armazenamento correspondente dessa conta.</span><span class="sxs-lookup"><span data-stu-id="63fcf-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="63fcf-116">Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="63fcf-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="63fcf-117">Para configurar uma assinatura do Azure, consulte [Avaliação gratuita de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63fcf-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="63fcf-118">Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="63fcf-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="63fcf-119">Carregar dados para Blob</span><span class="sxs-lookup"><span data-stu-id="63fcf-119">Upload Data to Blob</span></span>
<span data-ttu-id="63fcf-120">Adicione o trecho de código a seguir à parte superior de qualquer código Python no qual você deseja acessar programaticamente o Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="63fcf-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="63fcf-121">O objeto **serviço Blob** permite que você trabalhe com contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="63fcf-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="63fcf-122">O código a seguir cria um objeto BlobService usando o nome da conta de armazenamento e a chave da conta.</span><span class="sxs-lookup"><span data-stu-id="63fcf-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="63fcf-123">Substitua o nome e a chave de conta pela sua conta e chave reais.</span><span class="sxs-lookup"><span data-stu-id="63fcf-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="63fcf-124">Use os seguintes métodos para carregar dados para um blob:</span><span class="sxs-lookup"><span data-stu-id="63fcf-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="63fcf-125">put\_block\_blob\_from\_path (carrega o conteúdo de um arquivo do caminho especificado)</span><span class="sxs-lookup"><span data-stu-id="63fcf-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="63fcf-126">put\_block_blob\_from\_file (carrega o conteúdo de um arquivo/fluxo já aberto)</span><span class="sxs-lookup"><span data-stu-id="63fcf-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="63fcf-127">put\_block\_blob\_from\_bytes (carrega uma matriz de bytes)</span><span class="sxs-lookup"><span data-stu-id="63fcf-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="63fcf-128">put\_block\_blob\_from\_text (carrega o valor de texto especificado usando a codificação especificada)</span><span class="sxs-lookup"><span data-stu-id="63fcf-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="63fcf-129">O código de exemplo a seguir carrega um arquivo local para um contêiner:</span><span class="sxs-lookup"><span data-stu-id="63fcf-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="63fcf-130">O código de exemplo a seguir carrega todos os arquivos (exceto diretórios) em um diretório local para o armazenamento de blob:</span><span class="sxs-lookup"><span data-stu-id="63fcf-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="63fcf-131">Baixar Dados de Blob</span><span class="sxs-lookup"><span data-stu-id="63fcf-131">Download Data from Blob</span></span>
<span data-ttu-id="63fcf-132">Use os métodos a seguir para baixar dados de um blob:</span><span class="sxs-lookup"><span data-stu-id="63fcf-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="63fcf-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="63fcf-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="63fcf-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="63fcf-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="63fcf-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="63fcf-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="63fcf-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="63fcf-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="63fcf-137">Esses métodos realizam a divisão necessária quando o tamanho dos dados excede 64 MB.</span><span class="sxs-lookup"><span data-stu-id="63fcf-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="63fcf-138">O código de exemplo a seguir baixa o conteúdo de um blob em um contêiner para um arquivo local:</span><span class="sxs-lookup"><span data-stu-id="63fcf-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="63fcf-139">O código de exemplo a seguir baixa todos os blobs de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="63fcf-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="63fcf-140">Ele usa list\_blobs para obter a lista de blobs disponíveis no contêiner e baixá-los para um diretório local.</span><span class="sxs-lookup"><span data-stu-id="63fcf-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading the data %s"%blob.name
