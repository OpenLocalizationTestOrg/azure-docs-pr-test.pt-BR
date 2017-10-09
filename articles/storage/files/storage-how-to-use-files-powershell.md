---
title: aaaHow toouse PowerShell toomanage armazenamento de arquivo do Azure | Microsoft Docs
description: Saiba o armazenamento de arquivo do Azure toouse PowerShell toomanage.
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="2a096-103">Como toouse PowerShell toomanage armazenamento de arquivo do Azure</span><span class="sxs-lookup"><span data-stu-id="2a096-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="2a096-104">Você pode usar o Azure PowerShell toocreate e gerenciar compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="2a096-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="2a096-105">Instalar cmdlets do PowerShell Olá para o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2a096-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="2a096-106">tooprepare toouse PowerShell, baixe e instale Olá cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a096-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2a096-107">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para Olá instalar ponto e instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="2a096-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="2a096-108">É recomendável baixar e instalar ou atualizar toohello último módulo do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a096-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="2a096-109">Abra uma janela do Azure PowerShell clicando em **Iniciar** e digitando **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2a096-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="2a096-110">janela do PowerShell Olá carrega o módulo do Powershell do Azure Olá para você.</span><span class="sxs-lookup"><span data-stu-id="2a096-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="2a096-111">Criar um contexto para sua conta e chave de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2a096-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="2a096-112">Crie o contexto de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="2a096-112">Create hello storage account context.</span></span> <span data-ttu-id="2a096-113">contexto de saudação encapsula a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="2a096-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="2a096-114">Para obter instruções sobre como copiar a chave da conta de saudação [portal do Azure](https://portal.azure.com), consulte [exibir e copiar chaves de acesso de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="2a096-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="2a096-115">Substituir `storage-account-name` e `storage-account-key` com o nome da conta de armazenamento e a chave no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a096-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="2a096-116">Criar um novo compartilhamento de arquivo</span><span class="sxs-lookup"><span data-stu-id="2a096-116">Create a new file share</span></span>
<span data-ttu-id="2a096-117">Criar novo compartilhamento hello, denominado `logs`.</span><span class="sxs-lookup"><span data-stu-id="2a096-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="2a096-118">Agora você tem um compartilhamento de arquivo no armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="2a096-118">You now have a file share in File storage.</span></span> <span data-ttu-id="2a096-119">Em seguida, adicionaremos um diretório e um arquivo.</span><span class="sxs-lookup"><span data-stu-id="2a096-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a096-120">nome de saudação do seu compartilhamento de arquivo deve ser todas minúscula.</span><span class="sxs-lookup"><span data-stu-id="2a096-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="2a096-121">Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a096-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="2a096-122">Criar um diretório no compartilhamento de arquivo hello</span><span class="sxs-lookup"><span data-stu-id="2a096-122">Create a directory in hello file share</span></span>
<span data-ttu-id="2a096-123">Crie um diretório no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a096-123">Create a directory in hello share.</span></span> <span data-ttu-id="2a096-124">Olá exemplo a seguir, o diretório de saudação é denominado `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="2a096-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="2a096-125">Carregar um diretório do arquivo local toohello</span><span class="sxs-lookup"><span data-stu-id="2a096-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="2a096-126">Agora, carregar um diretório de toohello arquivo local.</span><span class="sxs-lookup"><span data-stu-id="2a096-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="2a096-127">Olá, exemplo a seguir carrega um arquivo de `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="2a096-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="2a096-128">Edite o caminho do arquivo hello para que ele aponte tooa de arquivo válido na sua máquina local.</span><span class="sxs-lookup"><span data-stu-id="2a096-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="2a096-129">Listar Olá arquivos no diretório de saudação</span><span class="sxs-lookup"><span data-stu-id="2a096-129">List hello files in hello directory</span></span>
<span data-ttu-id="2a096-130">arquivo de saudação do toosee no diretório de saudação, você pode listar todos os arquivos do diretório hello.</span><span class="sxs-lookup"><span data-stu-id="2a096-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="2a096-131">Esse comando retorna subdiretórios e arquivos de saudação (se houver) no diretório de CustomLogs hello.</span><span class="sxs-lookup"><span data-stu-id="2a096-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="2a096-132">Get-AzureStorageFile retorna uma lista de arquivos e diretórios para qualquer objeto de diretório que é passado.</span><span class="sxs-lookup"><span data-stu-id="2a096-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="2a096-133">"Get-AzureStorageFile-compartilhar $s" retorna uma lista de arquivos e diretórios no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a096-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="2a096-134">tooget uma lista de arquivos em um subdiretório, você tem toopass Olá subdiretório tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="2a096-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="2a096-135">--Que é o que isso faz a primeira parte saudação do comando Olá o pipe toohello retorna uma instância de diretório do subdiretório Olá CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="2a096-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="2a096-136">Em seguida, que é passado para Get-AzureStorageFile, que retorna Olá arquivos e diretórios em CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="2a096-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="2a096-137">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="2a096-137">Copy files</span></span>
<span data-ttu-id="2a096-138">A partir da versão 0.9.7 do PowerShell do Azure, você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="2a096-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="2a096-139">Abaixo, demonstraremos como tooperform esses copiam operações usando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a096-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="2a096-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a096-140">Next steps</span></span>
<span data-ttu-id="2a096-141">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a096-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="2a096-142">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="2a096-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="2a096-143">Solução de problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="2a096-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="2a096-144">Solução de problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="2a096-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    