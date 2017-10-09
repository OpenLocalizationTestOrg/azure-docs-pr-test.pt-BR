---
title: aaaMove tooand de dados do armazenamento de BLOBs do Azure usando Python | Microsoft Docs
description: Mover dados tooand do armazenamento de BLOBs do Azure usando Python
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
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="b0762-103">Mover dados tooand do armazenamento de BLOBs do Azure usando Python</span><span class="sxs-lookup"><span data-stu-id="b0762-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="b0762-104">Este tópico descreve como toolist, carregar e baixar blobs usando Olá API de Python.</span><span class="sxs-lookup"><span data-stu-id="b0762-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="b0762-105">Com hello API Python fornecido no SDK do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="b0762-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="b0762-106">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="b0762-106">Create a container</span></span>
* <span data-ttu-id="b0762-107">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="b0762-107">Upload a blob into a container</span></span>
* <span data-ttu-id="b0762-108">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="b0762-108">Download blobs</span></span>
* <span data-ttu-id="b0762-109">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="b0762-109">List hello blobs in a container</span></span>
* <span data-ttu-id="b0762-110">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="b0762-110">Delete a blob</span></span>

<span data-ttu-id="b0762-111">Para obter mais informações sobre como usar o hello Python API, consulte [como tooUse Olá serviço de armazenamento de Blob do Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b0762-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="b0762-112">Se você estiver usando a VM que foi configurado com scripts Olá fornecidos pela [máquinas virtuais de ciência de dados no Azure](machine-learning-data-science-virtual-machines.md), em seguida, AzCopy já está instalado na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0762-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b0762-113">Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e muito[serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0762-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b0762-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0762-114">Prerequisites</span></span>
<span data-ttu-id="b0762-115">Este documento assume que você tenha uma assinatura do Azure, uma conta de armazenamento e chave de armazenamento correspondente Olá para essa conta.</span><span class="sxs-lookup"><span data-stu-id="b0762-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="b0762-116">Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0762-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="b0762-117">tooset uma assinatura do Azure, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0762-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b0762-118">Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b0762-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="b0762-119">Carregar dados tooBlob</span><span class="sxs-lookup"><span data-stu-id="b0762-119">Upload Data tooBlob</span></span>
<span data-ttu-id="b0762-120">Adicione Olá trecho superior Olá de qualquer código Python no qual você deseja acesso tooprogrammatically armazenamento do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0762-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="b0762-121">Olá **BlobService** objeto permite que você trabalhe com contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="b0762-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="b0762-122">saudação de código a seguir cria um objeto de BlobService usando a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="b0762-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="b0762-123">Substitua o nome e a chave de conta pela sua conta e chave reais.</span><span class="sxs-lookup"><span data-stu-id="b0762-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="b0762-124">Use Olá blob de tooa métodos tooupload dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0762-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="b0762-125">colocar\_bloco\_blob\_de\_caminho (carrega o conteúdo de saudação de um arquivo do caminho especificado Olá)</span><span class="sxs-lookup"><span data-stu-id="b0762-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="b0762-126">colocar\_block_blob\_de\_(carrega o conteúdo de saudação de um arquivo já aberto/fluxo) de arquivo</span><span class="sxs-lookup"><span data-stu-id="b0762-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="b0762-127">put\_block\_blob\_from\_bytes (carrega uma matriz de bytes)</span><span class="sxs-lookup"><span data-stu-id="b0762-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="b0762-128">colocar\_bloco\_blob\_de\_texto (carrega Olá especificado valor de texto usando Olá codificação especificada)</span><span class="sxs-lookup"><span data-stu-id="b0762-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="b0762-129">Olá, código de exemplo a seguir carrega um contêiner de tooa arquivo local:</span><span class="sxs-lookup"><span data-stu-id="b0762-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="b0762-130">Olá seguinte exemplo de código carrega todos os arquivos de saudação (excluindo diretórios) em um armazenamento de tooblob do diretório local:</span><span class="sxs-lookup"><span data-stu-id="b0762-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="b0762-131">Baixar Dados de Blob</span><span class="sxs-lookup"><span data-stu-id="b0762-131">Download Data from Blob</span></span>
<span data-ttu-id="b0762-132">Use Olá seguintes dados de toodownload de métodos de um blob:</span><span class="sxs-lookup"><span data-stu-id="b0762-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="b0762-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="b0762-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="b0762-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="b0762-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="b0762-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="b0762-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="b0762-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="b0762-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="b0762-137">Esses métodos que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="b0762-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="b0762-138">Olá, código de exemplo seguinte baixa conteúdo Olá de um blob em um arquivo local do contêiner tooa:</span><span class="sxs-lookup"><span data-stu-id="b0762-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="b0762-139">Olá seguinte código de exemplo baixa todos os blobs de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="b0762-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="b0762-140">Ele usa a lista\_blobs tooget lista de saudação de blobs disponíveis no contêiner hello e baixar os arquivos tooa diretório de local.</span><span class="sxs-lookup"><span data-stu-id="b0762-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
            print "something wrong happened when downloading hello data %s"%blob.name
