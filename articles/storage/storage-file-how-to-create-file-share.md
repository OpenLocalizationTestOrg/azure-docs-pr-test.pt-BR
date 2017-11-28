---
title: aaaHow toocreate um compartilhamento de arquivos do Azure | Microsoft Docs
description: "Como toocreate um arquivo do Azure compartilham no armazenamento de arquivo do Azure usando Olá portal do Azure, PowerShell e Olá CLI do Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="4ef4d-103">Criar um Compartilhamento de Arquivos no Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4ef4d-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="4ef4d-104">Você pode criar compartilhamentos de arquivos do Azure usando [portal do Azure](https://portal.azure.com/), Olá cmdlets do PowerShell do armazenamento do Azure, Olá bibliotecas de cliente de armazenamento do Azure ou Olá API de REST do armazenamento do Azure. Neste tutorial, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="4ef4d-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="4ef4d-105">Como toocreate um arquivo Azure compartilhar usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4ef4d-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="4ef4d-106">Como toocreate um Azure compartilhamento de arquivos usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="4ef4d-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="4ef4d-107">Como toocreate um arquivo Azure compartilhar usando a CLI</span><span class="sxs-lookup"><span data-stu-id="4ef4d-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="4ef4d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ef4d-108">Prerequisites</span></span>
<span data-ttu-id="4ef4d-109">toocreate um compartilhamento de arquivos do Azure, você pode usar uma conta de armazenamento que já existe, ou [criar uma nova conta de armazenamento do Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4ef4d-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="4ef4d-110">toocreate um compartilhamento de arquivos do Azure com o PowerShell, você precisará de chave da conta de saudação e o nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="4ef4d-111">Chave de conta de armazenamento será necessário se você planejar toouse Powershell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="4ef4d-112">Criar compartilhamento de arquivos por meio do Portal de saudação</span><span class="sxs-lookup"><span data-stu-id="4ef4d-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="4ef4d-113">**Folha de conta de tooStorage vá no Portal do Azure**:</span><span class="sxs-lookup"><span data-stu-id="4ef4d-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="4ef4d-114">![Folha Conta de Armazenamento](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="4ef4d-115">**Clique no botão Adicionar Compartilhamento de arquivos**:</span><span class="sxs-lookup"><span data-stu-id="4ef4d-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="4ef4d-116">![Clique em Olá adicionar um botão de compartilhamento de arquivo](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="4ef4d-117">**Forneça o Nome e a Cota. A cota atualmente pode ter um máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="4ef4d-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="4ef4d-118">![Forneça um nome e uma cota desejada para o novo compartilhamento de arquivo hello](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="4ef4d-119">**Exiba o novo compartilhamento de arquivos**: ![Exiba o novo compartilhamento de arquivos](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="4ef4d-120">**Carregue um arquivo**: ![Carregue um arquivo](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="4ef4d-121">**Navegue o compartilhamento de arquivos e gerencie seus diretórios e arquivos**: ![Navegue o compartilhamento de arquivos](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="4ef4d-122">Criar um compartilhamento de arquivos com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ef4d-122">Create file share through PowerShell</span></span>
<span data-ttu-id="4ef4d-123">tooprepare toouse PowerShell, baixe e instale Olá cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4ef4d-124">Consulte [como tooinstall e configurar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para Olá instalar ponto e instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="4ef4d-125">É recomendável baixar e instalar ou atualizar toohello último módulo do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="4ef4d-126">**Criar um contexto para a conta de armazenamento e a chave** contexto Olá encapsula a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="4ef4d-127">Para obter instruções sobre como copiar a chave da conta no [portal do Azure](https://portal.azure.com/), veja [Exibir e copiar chaves de acesso de armazenamento](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="4ef4d-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="4ef4d-128">**Criar um novo compartilhamento de arquivos**:</span><span class="sxs-lookup"><span data-stu-id="4ef4d-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="4ef4d-129">nome de saudação do seu compartilhamento de arquivo deve ser todas minúscula.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="4ef4d-130">Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ef4d-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="4ef4d-131">Criar um compartilhamento de arquivos com a Interface da Linha de Comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="4ef4d-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="4ef4d-132">**tooprepare toouse uma Interface de linha de comando (CLI), baixe e instale Olá CLI do Azure.**</span><span class="sxs-lookup"><span data-stu-id="4ef4d-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="4ef4d-133">Consulte [Instalar a CLI do Azure 2.0](/cli/azure/install-az-cli2.md) e [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4ef4d-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="4ef4d-134">**Crie uma conta de armazenamento conexão cadeia de caracteres toohello onde você deseja que o compartilhamento de saudação toocreate.**</span><span class="sxs-lookup"><span data-stu-id="4ef4d-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="4ef4d-135">Substituir ```<storage-account>``` e ```<resource_group>``` com seu grupo de recursos e o nome da conta de armazenamento no hello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="4ef4d-136">**Criar um compartilhamento de arquivos**</span><span class="sxs-lookup"><span data-stu-id="4ef4d-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="4ef4d-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ef4d-137">Next steps</span></span>
* [<span data-ttu-id="4ef4d-138">Conecte e Monte o Compartilhamento de Arquivos - Windows</span><span class="sxs-lookup"><span data-stu-id="4ef4d-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="4ef4d-139">Conecte e Monte o Compartilhamento de Arquivos - Linux</span><span class="sxs-lookup"><span data-stu-id="4ef4d-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="4ef4d-140">Conecte e Monte o Compartilhamento de Arquivos - macOS</span><span class="sxs-lookup"><span data-stu-id="4ef4d-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="4ef4d-141">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4d-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="4ef4d-142">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="4ef4d-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="4ef4d-143">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="4ef4d-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)