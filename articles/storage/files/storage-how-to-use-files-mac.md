---
title: Montagem do compartilhamento de arquivos do Azure no SMB com macOS | Microsoft Docs
description: Saiba como montar um compartilhamento de arquivos do Azure no SMB com macOS.
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
ms.openlocfilehash: bc3d67745afb8bbffe7ec3462e995104daff9632
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="00f2e-103">Montagem do compartilhamento de arquivos do Azure no SMB com macOS</span><span class="sxs-lookup"><span data-stu-id="00f2e-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="00f2e-104">O [Armazenamento de arquivos do Azure](../storage-dotnet-how-to-use-files.md) é um serviço da Microsoft que permite criar e usar compartilhamentos de arquivos de rede no Azure usando o padrão do setor.</span><span class="sxs-lookup"><span data-stu-id="00f2e-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="00f2e-105">Os compartilhamentos de arquivos do Azure podem ser montados em macOS Sierra (10.12) e El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="00f2e-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="00f2e-106">Este artigo mostra duas maneiras diferentes para montar um compartilhamento de arquivos do Azure no macOS com a interface do usuário do Localizador e usando o Terminal.</span><span class="sxs-lookup"><span data-stu-id="00f2e-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="00f2e-107">Antes de montar um compartilhamento de arquivos do Azure no SMB, é recomendável desabilitar a assinatura de pacote SMB.</span><span class="sxs-lookup"><span data-stu-id="00f2e-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="00f2e-108">Isso pode resultar em baixo desempenho ao acessar o compartilhamento de arquivos do Azure no macOS.</span><span class="sxs-lookup"><span data-stu-id="00f2e-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="00f2e-109">Sua conexão SMB será criptografada para que isso não afete a segurança de sua conexão.</span><span class="sxs-lookup"><span data-stu-id="00f2e-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="00f2e-110">No terminal, os comandos a seguir desabilitarão a assinatura de pacotes SMB, conforme descrito por este [Artigo do suporte da Apple sobre como desabilitar a assinatura de pacote SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="00f2e-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="00f2e-111">Pré-requisitos para montar um compartilhamento de arquivos do Azure no macOS</span><span class="sxs-lookup"><span data-stu-id="00f2e-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="00f2e-112">**Nome da conta de armazenamento**: para montar um compartilhamento de arquivos do Azure, você precisará do nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="00f2e-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="00f2e-113">**Chave da conta de armazenamento**: para montar um compartilhamento de arquivos do Azure, você precisará do nome da chave de armazenamento primária (ou secundária).</span><span class="sxs-lookup"><span data-stu-id="00f2e-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="00f2e-114">Atualmente, as chaves SAS não têm suporte para montagem.</span><span class="sxs-lookup"><span data-stu-id="00f2e-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="00f2e-115">**Certifique-se de que a porta 445 está aberta**: SMB se comunica pela porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="00f2e-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="00f2e-116">No computador cliente (Mac), verifique se o firewall não está bloqueando a porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="00f2e-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="00f2e-117">Montar um compartilhamento de arquivos do Azure por meio do Localizador</span><span class="sxs-lookup"><span data-stu-id="00f2e-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="00f2e-118">**Abrir o Localizador**: o Localizador é aberto no macOS por padrão, mas você pode garantir que ele é o aplicativo selecionado clicando no "ícone de rosto do macOS" no encaixe:</span><span class="sxs-lookup"><span data-stu-id="00f2e-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="00f2e-119">![O ícone de rosto do macOS](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="00f2e-119">![The macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="00f2e-120">**Selecione "Conectar ao Servidor" no Menu "Go"**: usando o caminho UNC dos [pré-requisitos](#preq), converta a barra invertida dupla de início (`\\`) para `smb://` e todas as barras invertidas (`\`) para barras de encaminhamento (`/`).</span><span class="sxs-lookup"><span data-stu-id="00f2e-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="00f2e-121">O link deve ser semelhante ao seguinte: ![a caixa de diálogo "Conectar ao servidor"](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="00f2e-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="00f2e-122">**Use o nome do compartilhamento e a chave da conta de armazenamento quando solicitado a fornecer um nome de usuário e senha**: ao clicar em "Conectar" na caixa de diálogo "Conectar ao servidor", você será solicitado a fornecer o nome de usuário e senha (Isso será preenchido automaticamente com seu nome de usuário macOS).</span><span class="sxs-lookup"><span data-stu-id="00f2e-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="00f2e-123">Você tem a opção de colocar a chave da conta de armazenamento/nome do compartilhamento em seu conjunto de chaves do macOS.</span><span class="sxs-lookup"><span data-stu-id="00f2e-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="00f2e-124">**Usar o compartilhamento de arquivos do Azure conforme desejado**: depois de substituir o nome de compartilhamento e a chave da conta de armazenamento pelo nome de usuário e senha, o compartilhamento será montado.</span><span class="sxs-lookup"><span data-stu-id="00f2e-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="00f2e-125">Você pode usar isso como você normalmente usa um compartilhamento de arquivo/pasta local, incluindo a opção de arrastar e soltar arquivos no compartilhamento de arquivos:</span><span class="sxs-lookup"><span data-stu-id="00f2e-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Um instantâneo de um compartilhamento de arquivos montado do Azure](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="00f2e-127">Montar um compartilhamento de arquivos do Azure por meio do Terminal</span><span class="sxs-lookup"><span data-stu-id="00f2e-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="00f2e-128">Substitua `<storage-account-name>` com o nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="00f2e-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="00f2e-129">Quando solicitado, forneça a chave da conta de armazenamento como a senha.</span><span class="sxs-lookup"><span data-stu-id="00f2e-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="00f2e-130">**Usar o compartilhamento de arquivos do Azure conforme desejado**: o compartilhamento de arquivos do Azure será montado no ponto de montagem especificado pelo comando anterior.</span><span class="sxs-lookup"><span data-stu-id="00f2e-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Um instantâneo do compartilhamento de arquivos montado do Azure](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="00f2e-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00f2e-132">Next steps</span></span>
<span data-ttu-id="00f2e-133">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="00f2e-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="00f2e-134">Artigo de suporte da Apple - Como conectar-se com o compartilhamento de arquivos em seu Mac</span><span class="sxs-lookup"><span data-stu-id="00f2e-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="00f2e-135">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="00f2e-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="00f2e-136">Solução de problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="00f2e-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="00f2e-137">Solução de problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="00f2e-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    