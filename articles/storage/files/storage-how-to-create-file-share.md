---
title: Como criar um Compartilhamento de Arquivos do Azure | Microsoft Docs
description: Como criar um compartilhamento de arquivos do Azure no Armazenamento de arquivos do Azure usando o portal do Azure, PowerShell e CLI do Azure.
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
ms.openlocfilehash: b81701e2544ace092f007e5d98b3141e1f7da724
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="0c91f-103">Criar um Compartilhamento de Arquivos no Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="0c91f-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="0c91f-104">É possível criar Compartilhamentos de arquivos do Azure usando o [portal do Azure](https://portal.azure.com/), cmdlets do PowerShell do Armazenamento do Azure, bibliotecas de clientes do Armazenamento do Azure ou API REST do Armazenamento do Azure. Neste tutorial, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="0c91f-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="0c91f-105">Como criar um Compartilhamento de arquivos do Azure usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0c91f-105">How to create an Azure File share using the Azure portal</span></span>](#Create file share through the Portal)
* [<span data-ttu-id="0c91f-106">Como criar um Compartilhamento de arquivos do Azure usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="0c91f-106">How to create an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="0c91f-107">Como criar um Compartilhamento de arquivos do Azure usando a CLI</span><span class="sxs-lookup"><span data-stu-id="0c91f-107">How to create an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="0c91f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c91f-108">Prerequisites</span></span>
<span data-ttu-id="0c91f-109">Para criar um Compartilhamento de arquivos do Azure, você pode usar uma conta de armazenamento que já existe ou [criar uma nova conta de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c91f-109">To create an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="0c91f-110">Para criar um Compartilhamento de arquivos do Azure com o PowerShell, serão necessários a chave da conta e o nome de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0c91f-110">To create an Azure File share with PowerShell, you will need the account key and name of your storage account..</span></span> <span data-ttu-id="0c91f-111">Você precisará da chave da Conta de armazenamento se planejar usar o Powershell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="0c91f-111">You will need Storage account key if you plan to use Powershell or CLI.</span></span>

## <a name="create-file-share-through-the-portal"></a><span data-ttu-id="0c91f-112">Criar um compartilhamento de arquivos com o Portal</span><span class="sxs-lookup"><span data-stu-id="0c91f-112">Create file share through the Portal</span></span>
1. <span data-ttu-id="0c91f-113">**Vá para a folha Conta de Armazenamento no Portal do Azure**:</span><span class="sxs-lookup"><span data-stu-id="0c91f-113">**Go to Storage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="0c91f-114">![Folha Conta de Armazenamento](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="0c91f-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="0c91f-115">**Clique no botão Adicionar Compartilhamento de arquivos**:</span><span class="sxs-lookup"><span data-stu-id="0c91f-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="0c91f-116">![Clique no botão adicionar compartilhamento de arquivos](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="0c91f-116">![Click the add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="0c91f-117">**Forneça o Nome e a Cota. A cota atualmente pode ter um máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="0c91f-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="0c91f-118">![Forneça um nome e uma cota desejada para o novo compartilhamento de arquivos](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="0c91f-118">![Provide a name and a desired quota for the new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="0c91f-119">**Exiba o novo compartilhamento de arquivos**: ![Exiba o novo compartilhamento de arquivos](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="0c91f-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="0c91f-120">**Carregue um arquivo**: ![Carregue um arquivo](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="0c91f-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="0c91f-121">**Navegue o compartilhamento de arquivos e gerencie seus diretórios e arquivos**: ![Navegue o compartilhamento de arquivos](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="0c91f-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="0c91f-122">Criar um compartilhamento de arquivos com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c91f-122">Create file share through PowerShell</span></span>
<span data-ttu-id="0c91f-123">Para se preparar para usar o PowerShell, baixe e instale os cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c91f-123">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0c91f-124">Consulte [Como instalar e configurar o PowerShell do Azure](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para obter o ponto e as instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="0c91f-124">See [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for the install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="0c91f-125">É recomendável baixar e instalar ou atualizar para o módulo mais recente do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c91f-125">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="0c91f-126">**Crie um contexto para a conta de armazenamento e a chave** O contexto encapsula o nome da conta de armazenamento e a chave da conta.</span><span class="sxs-lookup"><span data-stu-id="0c91f-126">**Create a context for your storage account and key** The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="0c91f-127">Para obter instruções sobre como copiar a chave da conta no [portal do Azure](https://portal.azure.com/), veja [Exibir e copiar chaves de acesso de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="0c91f-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="0c91f-128">**Criar um novo compartilhamento de arquivos**:</span><span class="sxs-lookup"><span data-stu-id="0c91f-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="0c91f-129">O nome do seu compartilhamento de arquivo deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0c91f-129">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="0c91f-130">Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c91f-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="0c91f-131">Criar um compartilhamento de arquivos com a Interface da Linha de Comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="0c91f-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="0c91f-132">**Para se preparar para usar uma Interface da Linha de Comando (CLI), baixe e instale a CLI do Azure.**</span><span class="sxs-lookup"><span data-stu-id="0c91f-132">**To prepare to use a Command Line Interface (CLI), download and install the Azure CLI.**</span></span>  
    <span data-ttu-id="0c91f-133">Consulte [Instalar a CLI do Azure 2.0](/cli/azure/install-az-cli2.md) e [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0c91f-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="0c91f-134">**Crie uma cadeia de conexão para a conta de armazenamento na qual você deseja criar o compartilhamento.**</span><span class="sxs-lookup"><span data-stu-id="0c91f-134">**Create a connection string to the storage account where you want to create the share.**</span></span>  
    <span data-ttu-id="0c91f-135">Substitua ```<storage-account>``` e ```<resource_group>``` pelo nome da conta de armazenamento e o grupo de recursos no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0c91f-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in the following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. <span data-ttu-id="0c91f-136">**Criar um compartilhamento de arquivos**</span><span class="sxs-lookup"><span data-stu-id="0c91f-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="0c91f-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c91f-137">Next steps</span></span>
* [<span data-ttu-id="0c91f-138">Conecte e Monte o Compartilhamento de Arquivos - Windows</span><span class="sxs-lookup"><span data-stu-id="0c91f-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="0c91f-139">Conecte e Monte o Compartilhamento de Arquivos - Linux</span><span class="sxs-lookup"><span data-stu-id="0c91f-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="0c91f-140">Conecte e Monte o Compartilhamento de Arquivos - macOS</span><span class="sxs-lookup"><span data-stu-id="0c91f-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="0c91f-141">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c91f-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="0c91f-142">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="0c91f-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="0c91f-143">Solução de problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="0c91f-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="0c91f-144">Solução de problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="0c91f-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   