---
title: Criar uma imagem personalizada do Azure DevTest Labs de uma VM | Microsoft Docs
description: Saiba como criar uma imagem personalizada no Azure DevTest Labs de uma VM provisionada usando o Portal do Azure
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
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="534a2-103">Criar uma imagem personalizada de uma VM</span><span class="sxs-lookup"><span data-stu-id="534a2-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="534a2-104">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="534a2-104">Step-by-step instructions</span></span>

<span data-ttu-id="534a2-105">Você pode criar uma imagem personalizada de uma VM provisionada e depois usá-la para criar VMs idênticas.</span><span class="sxs-lookup"><span data-stu-id="534a2-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="534a2-106">As etapas a seguir ilustram como criar uma imagem personalizada com base em uma VM:</span><span class="sxs-lookup"><span data-stu-id="534a2-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="534a2-107">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="534a2-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="534a2-108">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="534a2-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="534a2-109">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="534a2-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="534a2-110">Na folha do laboratório, selecione **Minhas máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="534a2-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="534a2-111">Na folha **Minhas máquinas virtuais** , selecione a VM com base na qual você deseja criar a imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="534a2-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="534a2-112">Na folha da VM, selecione **Criar imagem personalizada (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="534a2-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Criar item de menu de imagem personalizada](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="534a2-114">Na folha **Criar imagem** , digite um nome e uma descrição para a sua imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="534a2-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="534a2-115">Essas informações são exibidas na lista de bases quando você cria uma VM.</span><span class="sxs-lookup"><span data-stu-id="534a2-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Criar folha de imagem personalizada](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="534a2-117">Selecione se o sysprep foi executado na VM.</span><span class="sxs-lookup"><span data-stu-id="534a2-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="534a2-118">Se o sysprep não tiver sido executado na VM, especifique se deseja que o sysprep seja executado quando uma VM for criada usando essa imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="534a2-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="534a2-119">Selecione **OK** quando tiver terminado de criar a imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="534a2-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="534a2-120">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="534a2-120">Related blog posts</span></span>

- [<span data-ttu-id="534a2-121">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="534a2-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="534a2-122">Copiar imagens personalizadas entre Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="534a2-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="534a2-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="534a2-123">Next steps</span></span>

- [<span data-ttu-id="534a2-124">Adicionar uma VM ao laboratório</span><span class="sxs-lookup"><span data-stu-id="534a2-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
