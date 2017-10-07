---
title: compartilhamento de arquivo do Azure aaaMount via SMB com macOS | Microsoft Docs
description: Saiba como toomount um arquivo Azure compartilhar em SMB com macOS.
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
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="e6ed4-103">Montagem do compartilhamento de arquivos do Azure no SMB com macOS</span><span class="sxs-lookup"><span data-stu-id="e6ed4-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="e6ed4-104">[Armazenamento de arquivo do Azure](../storage-dotnet-how-to-use-files.md) é usando o serviço da Microsoft que permite que você toocreate e use compartilhamentos de arquivos de rede no hello Azure padrão da indústria hello.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="e6ed4-105">Os compartilhamentos de arquivos do Azure podem ser montados em macOS Sierra (10.12) e El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="e6ed4-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="e6ed4-106">Este artigo mostra toomount de duas formas diferentes um compartilhamento de arquivos do Azure em macOS com hello localizador de interface do usuário e usando Olá Terminal.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="e6ed4-107">Antes de montar um compartilhamento de arquivos do Azure no SMB, é recomendável desabilitar a assinatura de pacote SMB.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="e6ed4-108">Isso pode resultar em baixo desempenho ao acessar o compartilhamento de arquivos do Azure de saudação do macOS.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="e6ed4-109">Sua conexão SMB sejam criptografado, para que isso não afeta a segurança de saudação da sua conexão.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="e6ed4-110">De Olá terminal, hello comandos a seguir desabilitará a assinatura de pacotes SMB, conforme descrito por esta [artigo do suporte da Apple ao desabilitar a assinatura de pacote SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="e6ed4-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="e6ed4-111">Pré-requisitos para montar um compartilhamento de arquivos do Azure no macOS</span><span class="sxs-lookup"><span data-stu-id="e6ed4-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="e6ed4-112">**Nome da conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o nome da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="e6ed4-113">**Chave de conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o chave de armazenamento primária (ou secundário).</span><span class="sxs-lookup"><span data-stu-id="e6ed4-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="e6ed4-114">Atualmente, as chaves SAS não têm suporte para montagem.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="e6ed4-115">**Certifique-se de que a porta 445 está aberta**: SMB se comunica pela porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="e6ed4-116">No computador cliente (Olá Mac), verifique toomake se que o firewall não está bloqueando a porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="e6ed4-117">Montar um compartilhamento de arquivos do Azure por meio do Localizador</span><span class="sxs-lookup"><span data-stu-id="e6ed4-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="e6ed4-118">**Abrir o localizador**: localizador é aberta no macOS por padrão, mas você pode garantir é Olá atualmente selecionada aplicativo clicando hello "macOS enfrentam ícone" no encaixe hello:</span><span class="sxs-lookup"><span data-stu-id="e6ed4-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="e6ed4-119">![Olá macOS enfrentam ícone](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="e6ed4-119">![hello macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="e6ed4-120">**Selecione "TooServer conectar-se" Olá "Go" Menu**: usando o caminho UNC de saudação do hello [pré-requisitos](#preq), converter barra invertida dupla de início da saudação (`\\`) muito`smb://` e todas as outras barras invertidas (`\`) barras de tooforwards (`/`).</span><span class="sxs-lookup"><span data-stu-id="e6ed4-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="e6ed4-121">O link deve ter aparência a seguir Olá: ![caixa de diálogo de "TooServer conectar-se" Olá](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="e6ed4-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="e6ed4-122">**Use Olá compartilhamento nome e o armazenamento de chave da conta quando solicitado a fornecer um nome de usuário e senha**: quando você clica em "Conectar" na caixa de diálogo de "TooServer conectar-se" Olá, você será solicitado para Olá nome de usuário e senha (Isso será autopopulated com seu macOS nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="e6ed4-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="e6ed4-123">Você tem a opção de saudação de colocar chave de conta de nome/armazenamento de compartilhamento de saudação em seu conjunto de chaves macOS.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="e6ed4-124">**Compartilhamento de arquivo do Azure Use Olá conforme desejado**: após substituindo Olá compartilhamento nome e o armazenamento de chave da conta para Olá username e password, compartilhamento hello será montado.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="e6ed4-125">Você pode usar isso como você normalmente usa um compartilhamento de arquivo/pasta local, incluindo arrastando e soltando arquivos em um compartilhamento de arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="e6ed4-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Um instantâneo de um compartilhamento de arquivos montado do Azure](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="e6ed4-127">Montar um compartilhamento de arquivos do Azure por meio do Terminal</span><span class="sxs-lookup"><span data-stu-id="e6ed4-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="e6ed4-128">Substituir `<storage-account-name>` com nome de saudação da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="e6ed4-129">Quando solicitado, forneça a chave da conta de armazenamento como a senha.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="e6ed4-130">**Compartilhamento de arquivo do Azure Use Olá conforme desejado**: compartilhamento de arquivo do Azure Olá será montado no ponto de montagem de saudação especificado pelo comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Um instantâneo do compartilhamento de arquivo do Azure Olá montado](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="e6ed4-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6ed4-132">Next steps</span></span>
<span data-ttu-id="e6ed4-133">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6ed4-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="e6ed4-134">Artigo de suporte da Apple - como tooconnect com o compartilhamento de arquivo no seu Mac</span><span class="sxs-lookup"><span data-stu-id="e6ed4-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="e6ed4-135">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="e6ed4-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="e6ed4-136">Solução de problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="e6ed4-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="e6ed4-137">Solução de problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="e6ed4-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    