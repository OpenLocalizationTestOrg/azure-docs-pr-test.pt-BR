---
title: Como usar o PowerShell para gerenciar o Armazenamento de Arquivos do Azure | Microsoft Docs
description: Saiba como usar o PowerShell para gerenciar o Armazenamento de Arquivos do Azure.
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
ms.openlocfilehash: 148375b156c4ae1aa4bf203d215f7ed607a71b89
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="99a63-103">Como usar o PowerShell para gerenciar o Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="99a63-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="99a63-104">Você pode usar o Azure PowerShell para criar e gerenciar compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="99a63-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="99a63-105">Instalar os cmdlets do PowerShell para Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="99a63-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="99a63-106">Para se preparar para usar o PowerShell, baixe e instale os cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="99a63-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="99a63-107">Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azureps-cmdlets-docs) para obter o ponto e as instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="99a63-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="99a63-108">É recomendável baixar e instalar ou atualizar para o módulo mais recente do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="99a63-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="99a63-109">Abra uma janela do Azure PowerShell clicando em **Iniciar** e digitando **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="99a63-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="99a63-110">A janela do PowerShell carregará o módulo do Azure PowerShell para você.</span><span class="sxs-lookup"><span data-stu-id="99a63-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="99a63-111">Criar um contexto para sua conta e chave de armazenamento</span><span class="sxs-lookup"><span data-stu-id="99a63-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="99a63-112">Crie o contexto da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99a63-112">Create the storage account context.</span></span> <span data-ttu-id="99a63-113">O contexto encapsula a conta de armazenamento e a chave da conta.</span><span class="sxs-lookup"><span data-stu-id="99a63-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="99a63-114">Para obter instruções sobre como copiar a chave da conta no [portal do Azure](https://portal.azure.com), veja [Exibir e copiar chaves de acesso de armazenamento](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="99a63-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="99a63-115">Substitua `storage-account-name` e `storage-account-key` pelo nome e chave da sua conta de armazenamento no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="99a63-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="99a63-116">Criar um novo compartilhamento de arquivo</span><span class="sxs-lookup"><span data-stu-id="99a63-116">Create a new file share</span></span>
<span data-ttu-id="99a63-117">Crie o novo compartilhamento, denominado `logs`.</span><span class="sxs-lookup"><span data-stu-id="99a63-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="99a63-118">Agora você tem um compartilhamento de arquivo no armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="99a63-118">You now have a file share in File storage.</span></span> <span data-ttu-id="99a63-119">Em seguida, adicionaremos um diretório e um arquivo.</span><span class="sxs-lookup"><span data-stu-id="99a63-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99a63-120">O nome do seu compartilhamento de arquivo deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="99a63-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="99a63-121">Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="99a63-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="99a63-122">Criar um diretório no compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99a63-122">Create a directory in the file share</span></span>
<span data-ttu-id="99a63-123">Crie um diretório no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="99a63-123">Create a directory in the share.</span></span> <span data-ttu-id="99a63-124">No exemplo a seguir, o diretório é denominado `CustomLogs`:</span><span class="sxs-lookup"><span data-stu-id="99a63-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="99a63-125">Carregar um arquivo local no diretório</span><span class="sxs-lookup"><span data-stu-id="99a63-125">Upload a local file to the directory</span></span>
<span data-ttu-id="99a63-126">Agora, carregue um arquivo local no diretório.</span><span class="sxs-lookup"><span data-stu-id="99a63-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="99a63-127">O exemplo a seguir carrega um arquivo de `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="99a63-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="99a63-128">Edite o caminho do arquivo para que ele aponte para um arquivo válido em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="99a63-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="99a63-129">Listar os arquivos no diretório</span><span class="sxs-lookup"><span data-stu-id="99a63-129">List the files in the directory</span></span>
<span data-ttu-id="99a63-130">Para ver o arquivo no diretório, você pode listar todos os arquivos do diretório.</span><span class="sxs-lookup"><span data-stu-id="99a63-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="99a63-131">Esse comando retorna os arquivos e subdiretórios (se houver) no diretório CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="99a63-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="99a63-132">Get-AzureStorageFile retorna uma lista de arquivos e diretórios para qualquer objeto de diretório que é passado.</span><span class="sxs-lookup"><span data-stu-id="99a63-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="99a63-133">"Get-AzureStorageFile -Share $s" retorna uma lista de arquivos e diretórios no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="99a63-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="99a63-134">Para obter uma lista de arquivos em um subdiretório, você precisa passar o subdiretório para Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="99a63-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="99a63-135">É o que isso faz: a primeira parte do comando até o pipe retorna uma instância de diretório do subdiretório CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="99a63-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="99a63-136">Em seguida, ela é passada para Get-AzureStorageFile, que retorna os arquivos e diretórios em CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="99a63-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="99a63-137">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="99a63-137">Copy files</span></span>
<span data-ttu-id="99a63-138">A partir da versão 0.9.7 do Azure PowerShell, você pode copiar um arquivo em outro arquivo, um arquivo em um blob ou um blob em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="99a63-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="99a63-139">A seguir, demonstramos como executar essas operações de cópia usando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99a63-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="99a63-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99a63-140">Next steps</span></span>
<span data-ttu-id="99a63-141">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="99a63-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="99a63-142">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="99a63-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="99a63-143">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="99a63-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)