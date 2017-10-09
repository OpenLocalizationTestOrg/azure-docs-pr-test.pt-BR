---
title: "aaaHow toomanage armazenamento de arquivo do Azure de saudação portal do Azure | Microsoft Docs"
description: "Saiba o armazenamento de arquivo do Azure toouse Olá toomanage portal do Azure."
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
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="f7803-103">Como o armazenamento de arquivo do Azure toouse de Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f7803-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="f7803-104">Olá [portal do Azure](https://portal.azure.com) fornece uma interface de usuário para gerenciar o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7803-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="f7803-105">Você pode executar Olá ações a seguir em seu navegador da web:</span><span class="sxs-lookup"><span data-stu-id="f7803-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="f7803-106">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="f7803-106">Create a File Share</span></span>
* <span data-ttu-id="f7803-107">Carregar e baixar arquivos tooand do seu compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f7803-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="f7803-108">Monitorar o uso real de cada compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f7803-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="f7803-109">Ajuste a cota de tamanho de compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f7803-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="f7803-110">Copie Olá montagem comandos toouse toomount o arquivo de compartilhamento de um cliente Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="f7803-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="f7803-111">Criar o compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="f7803-111">Create file share</span></span>
1. <span data-ttu-id="f7803-112">Entrar toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7803-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="f7803-113">No menu de navegação hello, clique em **contas de armazenamento** ou **contas de armazenamento (clássico)**.</span><span class="sxs-lookup"><span data-stu-id="f7803-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="f7803-115">Escolha sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f7803-115">Choose your storage account.</span></span>

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="f7803-117">Escolha o serviço "Arquivos".</span><span class="sxs-lookup"><span data-stu-id="f7803-117">Choose "Files" service.</span></span>

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="f7803-119">Clique em "Compartilhamentos de arquivos" e siga Olá link toocreate compartilhar seu primeiro arquivo.</span><span class="sxs-lookup"><span data-stu-id="f7803-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="f7803-121">Preencha o compartilhamento de arquivos primeiro em nome de compartilhamento de arquivo hello e tamanho de saudação de toocreate de compartilhamento (até too5120 GB) de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f7803-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="f7803-122">Quando o compartilhamento de arquivo hello tiver sido criado, você pode montá-lo de qualquer sistema de arquivos com suporte para SMB 2.1 ou SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="f7803-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="f7803-123">Você pode clicar em **cota** em tamanho Olá arquivo compartilhamento toochange saudação do arquivo hello a too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="f7803-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="f7803-124">Consulte também[Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate custo de armazenamento de saudação do uso de armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7803-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="f7803-126">Carregar e baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="f7803-126">Upload and download files</span></span>
1. <span data-ttu-id="f7803-127">Escolha um compartilhamento de arquivos que já tenha sido criado.</span><span class="sxs-lookup"><span data-stu-id="f7803-127">Choose one file share your have already created.</span></span>

    ![Captura de tela que mostra como tooupload e baixe arquivos de Olá portal](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="f7803-129">Clique em **carregar** para abrir a interface do usuário Olá para carregamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f7803-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Captura de tela que mostra como os arquivos de tooupload do portal de saudação](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="f7803-131">Conecte-se o compartilhamento de toofile</span><span class="sxs-lookup"><span data-stu-id="f7803-131">Connect toofile share</span></span>
-  <span data-ttu-id="f7803-132">Clique em **conectar** ao obter linha de comando Olá montagem Olá para compartilhamento de arquivos do Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="f7803-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="f7803-133">Para os usuários do Linux, você também pode consultar muito[como toouse armazenamento de arquivo do Azure com Linux](../storage-how-to-use-files-linux.md) para obter mais instruções de montagem para outras distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="f7803-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Captura de tela que mostra como toomount Olá compartilhamento de arquivos](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="f7803-135">Você pode copiar Olá comandos para montar o arquivo de compartilhamento no Windows ou Linux e execução-lo a sua máquina local ou de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7803-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Captura de tela que mostra os comandos de montagem de saudação para Windows e Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="f7803-137">**Dica:**</span><span class="sxs-lookup"><span data-stu-id="f7803-137">**Tip:**</span></span>  
<span data-ttu-id="f7803-138">chave de acesso de conta de armazenamento da saudação do toofind para montagem, clique em **teclas de acesso de exibição para essa conta de armazenamento** final Olá Olá página de conexão.</span><span class="sxs-lookup"><span data-stu-id="f7803-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7803-139">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f7803-139">See also</span></span>
<span data-ttu-id="f7803-140">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7803-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="f7803-141">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f7803-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="f7803-142">Solução de problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="f7803-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="f7803-143">Solução de problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="f7803-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    