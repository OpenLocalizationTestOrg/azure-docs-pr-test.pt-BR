---
title: aaaUpload VHD arquivo tooAzure DevTest Labs usando o PowerShell | Microsoft Docs
description: Carregar conta de armazenamento do toolab do arquivo VHD usando o PowerShell
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="5e0b1-103">Carregar conta de armazenamento do toolab do arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e0b1-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="5e0b1-104">No Azure DevTest Labs, arquivos VHD podem ser imagens personalizadas usadas toocreate, que são máquinas virtuais de tooprovision usado.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="5e0b1-105">Olá etapas a seguir orientam você durante usando PowerShell tooupload conta de armazenamento de um VHD arquivo tooa lab.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="5e0b1-106">Depois de carregar seu arquivo VHD, Olá [próximas etapas seção](#next-steps) lista alguns artigos que ilustram como toocreate uma imagem personalizada do hello carregado o arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="5e0b1-107">Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="5e0b1-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="5e0b1-108">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="5e0b1-108">Step-by-step instructions</span></span>

<span data-ttu-id="5e0b1-109">as etapas a seguir de saudação da extensão de arquivo por meio de carregar um VHD tooAzure DevTest Labs usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="5e0b1-110">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5e0b1-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="5e0b1-111">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="5e0b1-112">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="5e0b1-113">Na folha do laboratório hello, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="5e0b1-114">Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="5e0b1-115">Em Olá **imagens personalizadas** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="5e0b1-116">Em Olá **imagem personalizada** folha, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="5e0b1-117">Em Olá **VHD** folha, selecione **carregar um VHD usando o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carregar o VHD usando o PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="5e0b1-119">Em Olá **carregue uma imagem usando o PowerShell** folha, editor de texto cópia Olá gerado do PowerShell script tooa.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="5e0b1-120">Modificar Olá **LocalFilePath** parâmetro hello **Add-AzureVhd** cmdlet toopoint toohello local do arquivo VHD que você deseja tooupload de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="5e0b1-121">Em um prompt do PowerShell, execute Olá **Add-AzureVhd** cmdlet (com hello modificado **LocalFilePath** parâmetro).</span><span class="sxs-lookup"><span data-stu-id="5e0b1-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="5e0b1-122">processo de saudação de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho de saudação do arquivo VHD hello e a velocidade de conexão.</span><span class="sxs-lookup"><span data-stu-id="5e0b1-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e0b1-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e0b1-123">Next steps</span></span>

- [<span data-ttu-id="5e0b1-124">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5e0b1-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="5e0b1-125">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e0b1-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
