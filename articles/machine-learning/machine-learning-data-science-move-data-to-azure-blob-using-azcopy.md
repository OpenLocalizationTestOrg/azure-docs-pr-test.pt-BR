---
title: aaaMove tooand de dados do armazenamento de BLOBs do Azure usando AzCopy | Microsoft Docs
description: Mover dados tooand do armazenamento de BLOBs do Azure usando AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="24adf-103">Mover dados tooand do armazenamento de BLOBs do Azure usando AzCopy</span><span class="sxs-lookup"><span data-stu-id="24adf-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="24adf-104">AzCopy é um utilitário de linha de comando projetado para carregar, baixar e tooand cópia de dados de blob do Microsoft Azure, arquivo e armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="24adf-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="24adf-105">Para obter instruções sobre como instalar o AzCopy e informações adicionais em usá-lo com hello plataforma Windows Azure, consulte [guia de Introdução com hello o utilitário de linha de comando AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="24adf-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="24adf-106">Se você estiver usando a VM que foi configurado com scripts Olá fornecidos pela [máquinas virtuais de ciência de dados no Azure](machine-learning-data-science-virtual-machines.md), em seguida, AzCopy já está instalado na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="24adf-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="24adf-107">Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e muito[serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="24adf-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="24adf-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24adf-108">Prerequisites</span></span>
<span data-ttu-id="24adf-109">Este documento presume que você tenha uma assinatura do Azure, uma conta de armazenamento e Olá a correspondente chave de armazenamento para essa conta.</span><span class="sxs-lookup"><span data-stu-id="24adf-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="24adf-110">Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="24adf-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="24adf-111">tooset uma assinatura do Azure, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24adf-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="24adf-112">Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="24adf-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="24adf-113">Executar comandos do AzCopy</span><span class="sxs-lookup"><span data-stu-id="24adf-113">Run AzCopy commands</span></span>
<span data-ttu-id="24adf-114">comandos do AzCopy toorun, abra uma janela de comando e navegue toohello AzCopy diretório de instalação no seu computador, em que o executável de AzCopy.exe hello está localizado.</span><span class="sxs-lookup"><span data-stu-id="24adf-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="24adf-115">Olá a sintaxe básica para comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="24adf-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="24adf-116">Você pode adicionar o caminho de sistema de tooyour Olá AzCopy instalação local e, em seguida, execute os comandos de saudação de qualquer diretório.</span><span class="sxs-lookup"><span data-stu-id="24adf-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="24adf-117">Por padrão, AzCopy é instalado muito*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* ou *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="24adf-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="24adf-118">Carregar arquivos tooan BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="24adf-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="24adf-119">tooupload um arquivo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="24adf-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="24adf-120">Baixe arquivos em um blob do Azure</span><span class="sxs-lookup"><span data-stu-id="24adf-120">Download files from an Azure blob</span></span>
<span data-ttu-id="24adf-121">toodownload um arquivo de um blob do Azure, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="24adf-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="24adf-122">Transferir os blobs entre os contêineres do Azure</span><span class="sxs-lookup"><span data-stu-id="24adf-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="24adf-123">blobs tootransfer entre contêineres do Azure, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="24adf-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="24adf-124">Dicas para usar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="24adf-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="24adf-125">Ao **carregar** arquivos, */S* carregará arquivos recursivamente.</span><span class="sxs-lookup"><span data-stu-id="24adf-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="24adf-126">Sem esse parâmetro, arquivos em subpastas não serão carregados.</span><span class="sxs-lookup"><span data-stu-id="24adf-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="24adf-127">Quando **baixando** arquivo, */S* pesquisas Olá contêiner de forma recursiva até que todos os arquivos no diretório especificado hello e seus subdiretórios, ou todos os arquivos que correspondem a Olá padrão especificado no hello fornecido diretório e seus subdiretórios, são baixadas.</span><span class="sxs-lookup"><span data-stu-id="24adf-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="24adf-128">Não é possível especificar um **arquivo blob específico** toodownload usando Olá */fonte* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="24adf-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="24adf-129">toodownload um arquivo específico, especifique usando Olá dos toodownload de nome de arquivo hello blob */padrão* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="24adf-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="24adf-130">**/S** parâmetro pode ser usado toohave AzCopy procure um recursivamente de padrão de nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="24adf-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="24adf-131">Sem o parâmetro de padrão de hello, AzCopy baixa todos os arquivos nesse diretório.</span><span class="sxs-lookup"><span data-stu-id="24adf-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

