---
title: Carregar o arquivo VHD no Azure DevTest Labs usando o Explorer do Armazenamento do Microsoft Azure | Microsoft Docs
description: "Carregar o arquivo VHD na conta de armazenamento do laboratório usando o Explorer do Armazenamento do Microsoft Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="4cf31-103">Carregar o arquivo VHD na conta de armazenamento do laboratório usando o Explorer do Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4cf31-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="4cf31-104">No Azure DevTest Labs, os arquivos VHD podem ser usados para criar imagens personalizadas, que são usadas para provisionar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="4cf31-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="4cf31-105">Este artigo ilustra como usar o [Explorer do Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) para carregar um arquivo VHD em uma conta de armazenamento do laboratório.</span><span class="sxs-lookup"><span data-stu-id="4cf31-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="4cf31-106">Depois de carregar seu arquivo VHD, a [seção Próximas etapas](#next-steps) lista alguns dos artigos que ilustram como criar uma imagem personalizada do arquivo VHD carregado.</span><span class="sxs-lookup"><span data-stu-id="4cf31-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="4cf31-107">Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="4cf31-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="4cf31-108">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="4cf31-108">Step-by-step instructions</span></span>

<span data-ttu-id="4cf31-109">As etapas a seguir mostram como carregar um arquivo VHD no DevTest Labs usando o [Explorer do Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="4cf31-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="4cf31-110">[Baixe e instale a versão mais recente do Explorer do Armazenamento do Microsoft Azure](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="4cf31-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="4cf31-111">Obtenha o nome da conta de armazenamento do laboratório usando o Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="4cf31-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="4cf31-112">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4cf31-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="4cf31-113">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="4cf31-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="4cf31-114">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="4cf31-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="4cf31-115">Na folha do laboratório, selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="4cf31-116">Na folha **Configuração** do laboratório, selecione **Imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="4cf31-117">Na folha **Imagens personalizadas**, selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="4cf31-118">Na folha **Imagem personalizada**, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="4cf31-119">Na folha **VHD**, selecione **Carregar um VHD usando o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Carregar o VHD usando o PowerShell][0]
    
    1. <span data-ttu-id="4cf31-121">A folha **Carregar uma imagem usando o PowerShell** exibe uma chamada ao cmdlet **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="4cf31-122">O primeiro parâmetro (*Destino*) contém o nome da conta de armazenamento do laboratório no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="4cf31-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="4cf31-123">https://<NOME-DA-CONTA-DE-ARMAZENAMENTO>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="4cf31-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="4cf31-124">Anote o nome da conta de armazenamento, pois ele será usado em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="4cf31-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="4cf31-125">Conecte-se a uma conta de assinatura do Azure usando o Explorer do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4cf31-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="4cf31-126">O Explorer do Armazenamento dá suporte a várias opções de conexão.</span><span class="sxs-lookup"><span data-stu-id="4cf31-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="4cf31-127">Esta seção ilustra como se conectar a uma conta de armazenamento associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf31-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="4cf31-128">Para ver as outras opções de conexão compatíveis com o Explorer do Armazenamento, veja o artigo [Introdução ao Explorer do Armazenamento](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="4cf31-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="4cf31-129">Abra o Explorer do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4cf31-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="4cf31-130">No Explorer do Armazenamento, selecione **Configurações de Conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Configurações de conta do Azure][1]
    
    1. <span data-ttu-id="4cf31-132">O painel esquerdo exibe as contas da Microsoft em que você fez logon.</span><span class="sxs-lookup"><span data-stu-id="4cf31-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="4cf31-133">Para se conectar a outra conta, selecione **Adicionar uma conta**e siga os diálogos para entrar com uma conta da Microsoft associada a pelo menos uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf31-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Adicionar uma conta][2]
    
    1. <span data-ttu-id="4cf31-135">Depois de entrar com êxito usando uma conta da Microsoft, o painel esquerdo é preenchido com as assinaturas do Azure associadas à conta.</span><span class="sxs-lookup"><span data-stu-id="4cf31-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="4cf31-136">Selecione as assinaturas do Azure com as quais você deseja trabalhar e selecione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="4cf31-137">(A seleção de **Todas as assinaturas** alterna a seleção de todas ou de nenhuma das assinaturas listadas do Azure.)</span><span class="sxs-lookup"><span data-stu-id="4cf31-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Selecionar assinaturas do Azure][3]
    
    1. <span data-ttu-id="4cf31-139">O painel esquerdo exibe as contas de armazenamento associadas às assinaturas do Azure selecionadas.</span><span class="sxs-lookup"><span data-stu-id="4cf31-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Assinaturas do Azure selecionadas][4]

1. <span data-ttu-id="4cf31-141">Localize a conta de armazenamento do laboratório:</span><span class="sxs-lookup"><span data-stu-id="4cf31-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="4cf31-142">No painel esquerdo do Explorer do Armazenamento, localize e expanda o nó da assinatura do Azure que possui o laboratório.</span><span class="sxs-lookup"><span data-stu-id="4cf31-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="4cf31-143">No nó da assinatura, expanda **Contas de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="4cf31-144">Expanda o nó da conta de armazenamento do laboratório para revelar nós de **Contêineres de Blob**, **Compartilhamentos de Arquivos**, **Filas** e **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="4cf31-145">Expanda o nó **Contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="4cf31-146">Escolha o contêiner de blobs de carregamentos para exibir seu conteúdo no painel direito.</span><span class="sxs-lookup"><span data-stu-id="4cf31-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Diretório de carregamento][5]

1. <span data-ttu-id="4cf31-148">Carregue o arquivo VHD usando o Explorer do Armazenamento:</span><span class="sxs-lookup"><span data-stu-id="4cf31-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="4cf31-149">No painel direito do Explorer do Armazenamento, você deve ver uma listagem dos blobs no contêiner de blob **carregamentos** da conta de armazenamento do laboratório.</span><span class="sxs-lookup"><span data-stu-id="4cf31-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="4cf31-150">Na barra de ferramentas do editor de blobs, escolha **Carregar**</span><span class="sxs-lookup"><span data-stu-id="4cf31-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Botão Carregar][6]
    
    1. <span data-ttu-id="4cf31-152">No menu suspenso **Carregar**, escolha **Carregar arquivos...**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="4cf31-153">Na caixa de diálogo **Carregar arquivos**, escolha as reticências.</span><span class="sxs-lookup"><span data-stu-id="4cf31-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Escolher arquivo][8]  

    1. <span data-ttu-id="4cf31-155">Na caixa de diálogo **Selecionar arquivo para carregar**, navegue até o arquivo VHD desejado, selecione-o e escolha **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="4cf31-156">Quando retornar para a caixa de diálogo **Carregar arquivos**, altere **Tipo de blob** para **Blob de páginas**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="4cf31-157">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="4cf31-157">Select **Upload**.</span></span>

        ![Escolher arquivo][9]  
    
    1. <span data-ttu-id="4cf31-159">O painel **Log de Atividades** do Explorer do Armazenamento mostra o status de download (com os links para cancelar o carregamento).</span><span class="sxs-lookup"><span data-stu-id="4cf31-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="4cf31-160">O processo de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho do arquivo VHD e da velocidade de conexão.</span><span class="sxs-lookup"><span data-stu-id="4cf31-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![Status de carregamento do arquivo][10]  

## <a name="next-steps"></a><span data-ttu-id="4cf31-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4cf31-162">Next steps</span></span>

- [<span data-ttu-id="4cf31-163">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4cf31-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="4cf31-164">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cf31-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
