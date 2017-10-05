---
title: Criar uma imagem personalizada do Azure DevTest Labs de um arquivo VHD | Microsoft Docs
description: Saiba como criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o Portal do Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="89907-103">Criar uma imagem personalizada de um arquivo VHD</span><span class="sxs-lookup"><span data-stu-id="89907-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="89907-104">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="89907-104">Step-by-step instructions</span></span>

<span data-ttu-id="89907-105">As seguintes etapas orientam você durante a criação de uma imagem personalizada de um arquivo VHD usando o Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="89907-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="89907-106">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="89907-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="89907-107">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="89907-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="89907-108">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="89907-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="89907-109">Na folha do laboratório, selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="89907-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="89907-110">Na folha **Configuração** do laboratório, selecione **Imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="89907-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="89907-111">Na folha **Imagens personalizadas**, selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="89907-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Imagem de Adicionar Personalizado](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="89907-113">Insira o nome da imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="89907-113">Enter the name of the custom image.</span></span> <span data-ttu-id="89907-114">Esse nome é exibido na lista de imagens base durante a criação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="89907-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="89907-115">Insira a descrição da imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="89907-115">Enter the description of the custom image.</span></span> <span data-ttu-id="89907-116">Essa descrição é exibida na lista de imagens base durante a criação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="89907-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="89907-117">Selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="89907-117">Select **VHD**.</span></span>

1. <span data-ttu-id="89907-118">Na folha **VHD**, selecione o arquivo VHD desejado.</span><span class="sxs-lookup"><span data-stu-id="89907-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="89907-119">Selecione **OK** para fechar a folha **VHD**.</span><span class="sxs-lookup"><span data-stu-id="89907-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="89907-120">Selecione **Configuração do SO**.</span><span class="sxs-lookup"><span data-stu-id="89907-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="89907-121">Na guia **Configuração do SO**, selecione **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="89907-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="89907-122">Se **Windows** for selecionado, especifique por meio da caixa de seleção se o *Sysprep* foi executado na máquina.</span><span class="sxs-lookup"><span data-stu-id="89907-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="89907-123">Selecione **OK** para fechar a folha **Configuração do SO**.</span><span class="sxs-lookup"><span data-stu-id="89907-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="89907-124">Selecione **OK** para criar a imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="89907-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="89907-125">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="89907-125">Related blog posts</span></span>

- [<span data-ttu-id="89907-126">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="89907-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="89907-127">Copiar imagens personalizadas entre Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="89907-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="89907-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89907-128">Next steps</span></span>

- [<span data-ttu-id="89907-129">Adicionar uma VM ao laboratório</span><span class="sxs-lookup"><span data-stu-id="89907-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
