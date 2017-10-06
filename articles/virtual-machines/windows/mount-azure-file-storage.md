---
title: aaaMount armazenamento de arquivo do Azure de uma VM do Windows Azure | Microsoft Docs
description: "Armazene o arquivo na nuvem Olá com armazenamento de arquivos do Azure e montar o compartilhamento de arquivos de nuvem a partir de uma máquina virtual do Azure (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="abeab-103">Usar compartilhamentos de arquivos do Azure com VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="abeab-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="abeab-104">Você pode usar compartilhamentos de arquivos do Azure como uma maneira toostore e acessar arquivos de sua VM.</span><span class="sxs-lookup"><span data-stu-id="abeab-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="abeab-105">Por exemplo, você pode armazenar um script ou um arquivo de configuração de aplicativo que você deseja que todos os seu tooshare de VMs.</span><span class="sxs-lookup"><span data-stu-id="abeab-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="abeab-106">Neste tópico, mostramos como compartilhamento de arquivos de montagem do Azure e toocreate e tooupload e download de arquivos.</span><span class="sxs-lookup"><span data-stu-id="abeab-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="abeab-107">Conecte-se o compartilhamento de arquivos tooa de uma VM</span><span class="sxs-lookup"><span data-stu-id="abeab-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="abeab-108">Esta seção pressupõe que você já tiver um compartilhamento de arquivos que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="abeab-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="abeab-109">Se você precisar toocreate um, consulte [criar um compartilhamento de arquivos](#create-a-file-share) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="abeab-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="abeab-110">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abeab-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abeab-111">No menu à esquerda do hello, clique em **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="abeab-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="abeab-112">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="abeab-112">Choose your storage account.</span></span>
4. <span data-ttu-id="abeab-113">Em Olá **visão geral** página em **serviços**, selecione **arquivos**.</span><span class="sxs-lookup"><span data-stu-id="abeab-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="abeab-114">Selecione um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="abeab-114">Select a file share.</span></span>
6. <span data-ttu-id="abeab-115">Clique em **conectar** tooopen uma página que mostra a sintaxe de linha de comando Olá montagem Olá para compartilhamento de arquivos do Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="abeab-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="abeab-116">Realçar a sintaxe de saudação do comando hello e cole-o no bloco de notas ou em outro lugar onde você pode acessá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="abeab-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="abeab-117">Editar à esquerda do hello sintaxe tooremove hello * * > * * e substituir *[letra da unidade]* com a letra de unidade de saudação (por exemplo, **y:**) onde deseja que o compartilhamento de arquivos toomount hello.</span><span class="sxs-lookup"><span data-stu-id="abeab-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="abeab-118">Conecte-se tooyour VM e abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="abeab-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="abeab-119">Colar em Olá editado sintaxe de conexão e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="abeab-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="abeab-120">Quando a conexão Olá tiver sido criado, você obter mensagem de saudação **Olá comando foi concluído com êxito.**</span><span class="sxs-lookup"><span data-stu-id="abeab-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="abeab-121">Verifique a conexão Olá digitando Olá letra tooswitch toothat unidade e, em seguida, digite **dir** toosee conteúdo de saudação do compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="abeab-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="abeab-122">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="abeab-122">Create a file share</span></span> 
1. <span data-ttu-id="abeab-123">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abeab-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abeab-124">No menu à esquerda do hello, clique em **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="abeab-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="abeab-125">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="abeab-125">Choose your storage account.</span></span>
4. <span data-ttu-id="abeab-126">Em Olá **visão geral** página em **serviços**, selecione **arquivos**.</span><span class="sxs-lookup"><span data-stu-id="abeab-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="abeab-127">Na página de serviço de arquivo hello, clique em **+ compartilhamento de arquivos** toocreate do primeiro arquivo compartilhar. \\</span><span class="sxs-lookup"><span data-stu-id="abeab-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="abeab-128">Preencha o nome de compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="abeab-128">Fill in hello file share name.</span></span> <span data-ttu-id="abeab-129">Nomes de compartilhamento de arquivos podem usar letras minúsculas, números e hifens únicos.</span><span class="sxs-lookup"><span data-stu-id="abeab-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="abeab-130">Olá nome não pode começar com um hífen e não é possível usar várias hifens consecutivos.</span><span class="sxs-lookup"><span data-stu-id="abeab-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="abeab-131">Preencha um limite no arquivo de saudação como grande pode ser a too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="abeab-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="abeab-132">Clique em **Okey** toodeploy compartilhamento de arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="abeab-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="abeab-133">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="abeab-133">Upload files</span></span>
1. <span data-ttu-id="abeab-134">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abeab-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abeab-135">No menu à esquerda do hello, clique em **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="abeab-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="abeab-136">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="abeab-136">Choose your storage account.</span></span>
4. <span data-ttu-id="abeab-137">Em Olá **visão geral** página em **serviços**, selecione **arquivos**.</span><span class="sxs-lookup"><span data-stu-id="abeab-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="abeab-138">Selecione um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="abeab-138">Select a file share.</span></span>
6. <span data-ttu-id="abeab-139">Clique em **carregar** tooopen Olá **carregar arquivos** página.</span><span class="sxs-lookup"><span data-stu-id="abeab-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="abeab-140">Clique em Olá toobrowse de ícone de pasta sistema de arquivos local para tooupload um arquivo.</span><span class="sxs-lookup"><span data-stu-id="abeab-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="abeab-141">Clique em **carregar** tooupload Olá toohello arquivo compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="abeab-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="abeab-142">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="abeab-142">Download files</span></span>
1. <span data-ttu-id="abeab-143">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abeab-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abeab-144">No menu à esquerda do hello, clique em **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="abeab-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="abeab-145">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="abeab-145">Choose your storage account.</span></span>
4. <span data-ttu-id="abeab-146">Em Olá **visão geral** página em **serviços**, selecione **arquivos**.</span><span class="sxs-lookup"><span data-stu-id="abeab-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="abeab-147">Selecione um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="abeab-147">Select a file share.</span></span>
6. <span data-ttu-id="abeab-148">Clique com botão direito no arquivo hello e escolha **baixar** toodownload-computador local tooyour.</span><span class="sxs-lookup"><span data-stu-id="abeab-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="abeab-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abeab-149">Next steps</span></span>

<span data-ttu-id="abeab-150">Você também pode criar e gerenciar compartilhamentos de arquivos usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abeab-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="abeab-151">Para obter mais informações, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="abeab-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
