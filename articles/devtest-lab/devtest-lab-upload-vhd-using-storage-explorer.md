---
title: aaaUpload VHD arquivo tooAzure DevTest Labs usando o Microsoft Azure Storage Explorer | Microsoft Docs
description: Carregar conta de armazenamento do toolab do arquivo VHD usando o Microsoft Azure Storage Explorer
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="804a4-103">Carregar conta de armazenamento do toolab do arquivo VHD usando o Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="804a4-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="804a4-104">No Azure DevTest Labs, arquivos VHD podem ser imagens personalizadas usadas toocreate, que são máquinas virtuais de tooprovision usado.</span><span class="sxs-lookup"><span data-stu-id="804a4-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="804a4-105">Este artigo ilustra como toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) conta de armazenamento do laboratório tooa tooupload um VHD do arquivo.</span><span class="sxs-lookup"><span data-stu-id="804a4-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="804a4-106">Depois de carregar seu arquivo VHD, Olá [próximas etapas seção](#next-steps) lista alguns artigos que ilustram como toocreate uma imagem personalizada do hello carregado o arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="804a4-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="804a4-107">Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="804a4-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="804a4-108">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="804a4-108">Step-by-step instructions</span></span>

<span data-ttu-id="804a4-109">Olá seguintes etapas walk arquivo por meio de carregar um VHD laboratórios tooDevTest usando [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="804a4-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="804a4-110">[Baixe e instale a versão mais recente de saudação do hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="804a4-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="804a4-111">Obter nome de saudação do laboratório de saudação conta de armazenamento usando Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="804a4-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="804a4-112">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="804a4-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="804a4-113">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="804a4-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="804a4-114">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="804a4-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="804a4-115">Na folha do laboratório hello, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="804a4-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="804a4-116">Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="804a4-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="804a4-117">Em Olá **imagens personalizadas** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="804a4-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="804a4-118">Em Olá **imagem personalizada** folha, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="804a4-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="804a4-119">Em Olá **VHD** folha, selecione **carregar um VHD usando o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="804a4-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Carregar o VHD usando o PowerShell][0]
    
    1. <span data-ttu-id="804a4-121">Olá **carregue uma imagem usando o PowerShell** folha exibe uma chamada toohello **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="804a4-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="804a4-122">Olá primeiro parâmetro (*destino*) contém o nome de conta de armazenamento Olá para o laboratório Olá Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="804a4-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="804a4-123">https://<NOME-DA-CONTA-DE-ARMAZENAMENTO>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="804a4-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="804a4-124">Anote o nome de conta de armazenamento hello, como ele é usado em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="804a4-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="804a4-125">Conecte-se tooan conta de assinatura do Azure usando o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="804a4-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="804a4-126">O Explorer do Armazenamento dá suporte a várias opções de conexão.</span><span class="sxs-lookup"><span data-stu-id="804a4-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="804a4-127">Esta seção ilustra a conta de armazenamento tooa conexão associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="804a4-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="804a4-128">toosee Olá outras opções de conexão tem suportadas pelo Gerenciador de armazenamento, consulte o artigo toohello, [guia de Introdução ao Gerenciador de armazenamento](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="804a4-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="804a4-129">Abra o Explorer do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="804a4-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="804a4-130">No Explorer do Armazenamento, selecione **Configurações de Conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="804a4-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Configurações de conta do Azure][1]
    
    1. <span data-ttu-id="804a4-132">painel esquerdo Olá exibe você fez logon para contas da Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="804a4-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="804a4-133">conta de tooanother tooconnect, selecione **adicionar uma conta**e siga Olá toosign de caixas de diálogo com uma conta da Microsoft que está associada a pelo menos uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="804a4-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Adicionar uma conta][2]
    
    1. <span data-ttu-id="804a4-135">Depois que você entrar com êxito com uma conta da Microsoft, o painel esquerdo Olá preenche com hello assinaturas do Azure associadas a essa conta.</span><span class="sxs-lookup"><span data-stu-id="804a4-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="804a4-136">Selecione Olá assinaturas do Azure com o qual você deseja toowork e, em seguida, selecione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="804a4-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="804a4-137">(Selecionar **todas as assinaturas** alterna Olá seleção de todos ou nenhum Olá listadas assinaturas do Azure.)</span><span class="sxs-lookup"><span data-stu-id="804a4-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Selecionar assinaturas do Azure][3]
    
    1. <span data-ttu-id="804a4-139">painel esquerdo Olá exibe as contas de armazenamento Olá associadas a assinaturas do Azure Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="804a4-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Assinaturas do Azure selecionadas][4]

1. <span data-ttu-id="804a4-141">Localize a conta de armazenamento do laboratório hello:</span><span class="sxs-lookup"><span data-stu-id="804a4-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="804a4-142">No painel esquerdo do Gerenciador de armazenamento hello, localize e expanda nó Olá Olá assinatura do Azure que possui o laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="804a4-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="804a4-143">No nó da assinatura hello, expanda **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="804a4-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="804a4-144">Expandir nós de tooreveal de nó do laboratório Olá armazenamento conta para **contêineres de Blob**, **compartilhamentos de arquivos**, **filas**, e **tabelas**.</span><span class="sxs-lookup"><span data-stu-id="804a4-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="804a4-145">Expanda Olá **contêineres de Blob** nó.</span><span class="sxs-lookup"><span data-stu-id="804a4-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="804a4-146">Selecione toodisplay de contêiner de blob de carregamentos de saudação seu conteúdo no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="804a4-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Diretório de carregamento][5]

1. <span data-ttu-id="804a4-148">Carregar arquivo VHD hello usando o Gerenciador de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="804a4-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="804a4-149">No painel à direita do Gerenciador de armazenamento hello, você deve ver uma lista dos blobs Olá Olá **carrega** contêiner de blob da conta de armazenamento do laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="804a4-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="804a4-150">Em ferramentas do editor de blob hello, selecione **carregar**</span><span class="sxs-lookup"><span data-stu-id="804a4-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Botão Carregar][6]
    
    1. <span data-ttu-id="804a4-152">De saudação **carregar** menu suspenso, selecione **carregar arquivos...** .</span><span class="sxs-lookup"><span data-stu-id="804a4-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="804a4-153">Em Olá **carregar arquivos** caixa de diálogo, reticências Olá select.</span><span class="sxs-lookup"><span data-stu-id="804a4-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Escolher arquivo][8]  

    1. <span data-ttu-id="804a4-155">Em Olá **tooupload Selecione arquivos** caixa de diálogo, procurar toohello desejado arquivo VHD, selecioná-lo e, em seguida, selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="804a4-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="804a4-156">Quando retornado toohello **carregar arquivos** caixa de diálogo, altere **tipo de Blob** muito**Blob de página**.</span><span class="sxs-lookup"><span data-stu-id="804a4-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="804a4-157">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="804a4-157">Select **Upload**.</span></span>

        ![Escolher arquivo][9]  
    
    1. <span data-ttu-id="804a4-159">Olá Storage Explorer **Log de atividades** painel mostra o status do download de saudação (junto com links toocancel Olá carregamento).</span><span class="sxs-lookup"><span data-stu-id="804a4-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="804a4-160">processo de saudação de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho de saudação do arquivo VHD hello e a velocidade de conexão.</span><span class="sxs-lookup"><span data-stu-id="804a4-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Status de carregamento do arquivo][10]  

## <a name="next-steps"></a><span data-ttu-id="804a4-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="804a4-162">Next steps</span></span>

- [<span data-ttu-id="804a4-163">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="804a4-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="804a4-164">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="804a4-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
