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
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="4cc92-103">Criar um Compartilhamento de Arquivos no Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="4cc92-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="4cc92-104">Você pode criar compartilhamentos de arquivos do Azure usando [portal do Azure](https://portal.azure.com/), Olá cmdlets do PowerShell do armazenamento do Azure, Olá bibliotecas de cliente de armazenamento do Azure ou Olá API de REST do armazenamento do Azure. Neste tutorial, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="4cc92-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="4cc92-105">Como toocreate um arquivo Azure compartilhar usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4cc92-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="4cc92-106">Como toocreate um Azure compartilhamento de arquivos usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="4cc92-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="4cc92-107">Como toocreate um arquivo Azure compartilhar usando a CLI</span><span class="sxs-lookup"><span data-stu-id="4cc92-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="4cc92-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4cc92-108">Prerequisites</span></span>
<span data-ttu-id="4cc92-109">toocreate um compartilhamento de arquivos do Azure, você pode usar uma conta de armazenamento que já existe, ou [criar uma nova conta de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cc92-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="4cc92-110">toocreate um compartilhamento de arquivos do Azure com o PowerShell, você precisará de chave da conta de saudação e o nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4cc92-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="4cc92-111">Chave de conta de armazenamento será necessário se você planejar toouse Powershell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="4cc92-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="4cc92-112">Criar compartilhamento de arquivos por meio do Portal de saudação</span><span class="sxs-lookup"><span data-stu-id="4cc92-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="4cc92-113">**Folha de conta de tooStorage vá no Portal do Azure**:</span><span class="sxs-lookup"><span data-stu-id="4cc92-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="4cc92-114">![Folha Conta de Armazenamento](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="4cc92-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="4cc92-115">**Clique no botão Adicionar Compartilhamento de arquivos**:</span><span class="sxs-lookup"><span data-stu-id="4cc92-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="4cc92-116">![Clique em Olá adicionar um botão de compartilhamento de arquivo](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="4cc92-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="4cc92-117">**Forneça o Nome e a Cota. A cota atualmente pode ter um máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="4cc92-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="4cc92-118">![Forneça um nome e uma cota desejada para o novo compartilhamento de arquivo hello](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="4cc92-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="4cc92-119">**Exiba o novo compartilhamento de arquivos**: ![Exiba o novo compartilhamento de arquivos](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="4cc92-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="4cc92-120">**Carregue um arquivo**: ![Carregue um arquivo](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="4cc92-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="4cc92-121">**Navegue o compartilhamento de arquivos e gerencie seus diretórios e arquivos**: ![Navegue o compartilhamento de arquivos](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="4cc92-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="4cc92-122">Criar um compartilhamento de arquivos com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cc92-122">Create file share through PowerShell</span></span>
<span data-ttu-id="4cc92-123">tooprepare toouse PowerShell, baixe e instale Olá cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cc92-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4cc92-124">Consulte [como tooinstall e configurar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para Olá instalar ponto e instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="4cc92-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="4cc92-125">É recomendável baixar e instalar ou atualizar toohello último módulo do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cc92-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="4cc92-126">**Criar um contexto para a conta de armazenamento e a chave** contexto Olá encapsula a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="4cc92-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="4cc92-127">Para obter instruções sobre como copiar a chave da conta no [portal do Azure](https://portal.azure.com/), veja [Exibir e copiar chaves de acesso de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="4cc92-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="4cc92-128">**Criar um novo compartilhamento de arquivos**:</span><span class="sxs-lookup"><span data-stu-id="4cc92-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="4cc92-129">nome de saudação do seu compartilhamento de arquivo deve ser todas minúscula.</span><span class="sxs-lookup"><span data-stu-id="4cc92-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="4cc92-130">Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cc92-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="4cc92-131">Criar um compartilhamento de arquivos com a Interface da Linha de Comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="4cc92-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="4cc92-132">**tooprepare toouse uma Interface de linha de comando (CLI), baixe e instale Olá CLI do Azure.**</span><span class="sxs-lookup"><span data-stu-id="4cc92-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="4cc92-133">Consulte [Instalar a CLI do Azure 2.0](/cli/azure/install-az-cli2.md) e [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4cc92-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="4cc92-134">**Crie uma conta de armazenamento conexão cadeia de caracteres toohello onde você deseja que o compartilhamento de saudação toocreate.**</span><span class="sxs-lookup"><span data-stu-id="4cc92-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="4cc92-135">Substituir ```<storage-account>``` e ```<resource_group>``` com seu grupo de recursos e o nome da conta de armazenamento no hello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4cc92-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="4cc92-136">**Criar um compartilhamento de arquivos**</span><span class="sxs-lookup"><span data-stu-id="4cc92-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="4cc92-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4cc92-137">Next steps</span></span>
* [<span data-ttu-id="4cc92-138">Conecte e Monte o Compartilhamento de Arquivos - Windows</span><span class="sxs-lookup"><span data-stu-id="4cc92-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="4cc92-139">Conecte e Monte o Compartilhamento de Arquivos - Linux</span><span class="sxs-lookup"><span data-stu-id="4cc92-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="4cc92-140">Conecte e Monte o Compartilhamento de Arquivos - macOS</span><span class="sxs-lookup"><span data-stu-id="4cc92-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="4cc92-141">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cc92-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="4cc92-142">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="4cc92-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="4cc92-143">Solução de problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="4cc92-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="4cc92-144">Solução de problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="4cc92-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   