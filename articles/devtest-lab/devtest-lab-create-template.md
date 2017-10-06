---
title: aaaCreate uma imagem personalizada do Azure DevTest Labs de um arquivo VHD | Microsoft Docs
description: "Saiba como toocreate uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="bb19f-103">Criar uma imagem personalizada de um arquivo VHD</span><span class="sxs-lookup"><span data-stu-id="bb19f-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="bb19f-104">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="bb19f-104">Step-by-step instructions</span></span>

<span data-ttu-id="bb19f-105">Olá etapas a seguir orientam você durante a criação de uma imagem personalizada de um arquivo VHD usando Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="bb19f-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="bb19f-106">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bb19f-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="bb19f-107">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb19f-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="bb19f-108">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="bb19f-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="bb19f-109">Na folha do laboratório hello, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="bb19f-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="bb19f-110">Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="bb19f-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="bb19f-111">Em Olá **imagens personalizadas** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bb19f-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Imagem de Adicionar Personalizado](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="bb19f-113">Insira o nome de saudação da imagem personalizada do hello.</span><span class="sxs-lookup"><span data-stu-id="bb19f-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="bb19f-114">Esse nome é exibido na lista de saudação de imagens de base ao criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="bb19f-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="bb19f-115">Insira a descrição de saudação da imagem personalizada do hello.</span><span class="sxs-lookup"><span data-stu-id="bb19f-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="bb19f-116">Essa descrição é exibida na lista de saudação de imagens de base ao criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="bb19f-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="bb19f-117">Selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="bb19f-117">Select **VHD**.</span></span>

1. <span data-ttu-id="bb19f-118">De saudação **VHD** folha, arquivo VHD selecione Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="bb19f-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="bb19f-119">Selecione **Okey** tooclose Olá **VHD** folha.</span><span class="sxs-lookup"><span data-stu-id="bb19f-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="bb19f-120">Selecione **Configuração do SO**.</span><span class="sxs-lookup"><span data-stu-id="bb19f-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="bb19f-121">Em Olá **configuração do sistema operacional** guia, selecione **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="bb19f-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="bb19f-122">Se **Windows** é selecionada, especifique por meio da caixa de seleção de saudação se *Sysprep* foi executado na máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb19f-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="bb19f-123">Selecione **Okey** tooclose Olá **configuração do sistema operacional** folha.</span><span class="sxs-lookup"><span data-stu-id="bb19f-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="bb19f-124">Selecione **Okey** imagem personalizada do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="bb19f-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="bb19f-125">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="bb19f-125">Related blog posts</span></span>

- [<span data-ttu-id="bb19f-126">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="bb19f-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="bb19f-127">Copiar imagens personalizadas entre Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bb19f-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="bb19f-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb19f-128">Next steps</span></span>

- [<span data-ttu-id="bb19f-129">Adicionar um laboratório de tooyour VM</span><span class="sxs-lookup"><span data-stu-id="bb19f-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
