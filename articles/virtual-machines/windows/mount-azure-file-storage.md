---
title: Montar armazenamento de arquivos do Azure com base em uma VM do Windows Azure | Microsoft Docs
description: "Armazene o arquivo na nuvem com o armazenamento de arquivos do Azure e monte o compartilhamento de arquivos de nuvem de uma VM (máquina virtual) do Azure."
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
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="a6856-103">Usar compartilhamentos de arquivos do Azure com VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="a6856-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="a6856-104">Você pode usar compartilhamentos de arquivos do Azure como uma maneira de armazenar e acessar arquivos na VM.</span><span class="sxs-lookup"><span data-stu-id="a6856-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="a6856-105">Por exemplo, você pode armazenar um script ou um arquivo de configuração de aplicativo que deseja que todas as VMs compartilhem.</span><span class="sxs-lookup"><span data-stu-id="a6856-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="a6856-106">Neste tópico, mostramos como criar e montar um compartilhamento de arquivos do Azure e como carregar e baixar arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="a6856-107">Conectar a um compartilhamento de arquivo por meio de uma VM</span><span class="sxs-lookup"><span data-stu-id="a6856-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="a6856-108">Esta seção pressupõe que você já tenha um compartilhamento de arquivos ao qual deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="a6856-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="a6856-109">Se você precisar criar um, confira [Criar um compartilhamento de arquivos](#create-a-file-share) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="a6856-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="a6856-110">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6856-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6856-111">No menu à esquerda, clique em **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a6856-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="a6856-112">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a6856-112">Choose your storage account.</span></span>
4. <span data-ttu-id="a6856-113">Na página **Visão geral**, em **Serviços**, selecione **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a6856-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="a6856-114">Selecione um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-114">Select a file share.</span></span>
6. <span data-ttu-id="a6856-115">Clique em **Conectar** para abrir uma página que mostra a sintaxe de linha de comando para montar o compartilhamento de arquivos do Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="a6856-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="a6856-116">Realce a sintaxe do comando e cole-a no Bloco de Notas ou em outro lugar em que você possa acessá-la facilmente.</span><span class="sxs-lookup"><span data-stu-id="a6856-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="a6856-117">Edite a sintaxe para remover o **> ** inicial e substitua *[letra da unidade]* pela letra da unidade (por exemplo, **y:**) em que você deseja montar o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="a6856-118">Conecte-se à VM e abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a6856-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="a6856-119">Cole a sintaxe de conexão editado e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a6856-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="a6856-120">Quando a conexão tiver sido criada, você receberá a mensagem **O comando foi concluído com êxito.**</span><span class="sxs-lookup"><span data-stu-id="a6856-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="a6856-121">Verifique a conexão digitando a letra da unidade para alternar para a unidade e digite **dir** para ver o conteúdo do compartilhamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6856-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="a6856-122">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="a6856-122">Create a file share</span></span> 
1. <span data-ttu-id="a6856-123">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6856-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6856-124">No menu à esquerda, clique em **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a6856-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="a6856-125">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a6856-125">Choose your storage account.</span></span>
4. <span data-ttu-id="a6856-126">Na página **Visão geral**, em **Serviços**, selecione **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a6856-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="a6856-127">Na página de Serviço de Arquivo, clique em **+Compartilhamento de arquivos** para criar o primeiro compartilhamento de arquivos.\\</span><span class="sxs-lookup"><span data-stu-id="a6856-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="a6856-128">Preencha o nome do compartilhamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6856-128">Fill in the file share name.</span></span> <span data-ttu-id="a6856-129">Nomes de compartilhamento de arquivos podem usar letras minúsculas, números e hifens únicos.</span><span class="sxs-lookup"><span data-stu-id="a6856-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="a6856-130">O nome não pode começar com um hífen e não é possível usar várias hifens consecutivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="a6856-131">Preencha o limite de tamanho do arquivo, até 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="a6856-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="a6856-132">Clique em **OK** para implantar o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="a6856-133">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="a6856-133">Upload files</span></span>
1. <span data-ttu-id="a6856-134">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6856-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6856-135">No menu à esquerda, clique em **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a6856-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="a6856-136">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a6856-136">Choose your storage account.</span></span>
4. <span data-ttu-id="a6856-137">Na página **Visão geral**, em **Serviços**, selecione **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a6856-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="a6856-138">Selecione um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-138">Select a file share.</span></span>
6. <span data-ttu-id="a6856-139">Clique em **Carregar** para abrir a página **Carregar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a6856-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="a6856-140">Clique no ícone de pasta para procurar no sistema de arquivos local um arquivo para carregar.</span><span class="sxs-lookup"><span data-stu-id="a6856-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="a6856-141">Clique em **Carregar** para carregar o arquivo para o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="a6856-142">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="a6856-142">Download files</span></span>
1. <span data-ttu-id="a6856-143">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6856-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6856-144">No menu à esquerda, clique em **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a6856-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="a6856-145">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a6856-145">Choose your storage account.</span></span>
4. <span data-ttu-id="a6856-146">Na página **Visão geral**, em **Serviços**, selecione **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a6856-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="a6856-147">Selecione um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6856-147">Select a file share.</span></span>
6. <span data-ttu-id="a6856-148">Clique com o botão direito do mouse no arquivo e escolha **Baixar** para baixá-lo no computador local.</span><span class="sxs-lookup"><span data-stu-id="a6856-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="a6856-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6856-149">Next steps</span></span>

<span data-ttu-id="a6856-150">Você também pode criar e gerenciar compartilhamentos de arquivos usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6856-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="a6856-151">Para obter mais informações, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="a6856-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
