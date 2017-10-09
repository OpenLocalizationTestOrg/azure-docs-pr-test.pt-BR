---
title: aaaCreate uma imagem personalizada do Azure DevTest Labs de uma VM | Microsoft Docs
description: "Saiba como toocreate uma imagem personalizada no Azure DevTest Labs de uma VM provisionados usando Olá portal do Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="4e7d0-103">Criar uma imagem personalizada de uma VM</span><span class="sxs-lookup"><span data-stu-id="4e7d0-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4e7d0-104">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="4e7d0-104">Step-by-step instructions</span></span>

<span data-ttu-id="4e7d0-105">Você pode criar uma imagem personalizada de uma VM provisionada e depois usar essa imagem personalizada toocreate VMs idênticas.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="4e7d0-106">Olá, as etapas a seguir ilustra como toocreate um personalizado da imagem de uma VM:</span><span class="sxs-lookup"><span data-stu-id="4e7d0-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="4e7d0-107">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4e7d0-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4e7d0-108">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="4e7d0-109">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="4e7d0-110">Na folha do laboratório hello, selecione **minhas máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="4e7d0-111">Em Olá **minhas máquinas virtuais** folha, selecione Olá VM do qual você deseja imagem personalizada do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="4e7d0-112">Na folha de saudação da VM, selecione **criar imagem personalizada (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Criar item de menu de imagem personalizada](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="4e7d0-114">Em Olá **criar imagem** folha, insira um nome e uma descrição para sua imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="4e7d0-115">Essa informação é exibida na lista de saudação de bases de dados quando você cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Criar folha de imagem personalizada](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="4e7d0-117">Selecione se o sysprep foi executado no hello VM.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="4e7d0-118">Se sysprep Olá não foi executado no hello VM, especifique se você deseja executar quando uma VM é criada usando essa imagem personalizada do sysprep.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="4e7d0-119">Selecione **Okey** quando terminar de toocreate Olá imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="4e7d0-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4e7d0-120">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="4e7d0-120">Related blog posts</span></span>

- [<span data-ttu-id="4e7d0-121">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="4e7d0-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4e7d0-122">Copiar imagens personalizadas entre Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4e7d0-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4e7d0-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e7d0-123">Next steps</span></span>

- [<span data-ttu-id="4e7d0-124">Adicionar um laboratório de tooyour VM</span><span class="sxs-lookup"><span data-stu-id="4e7d0-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
