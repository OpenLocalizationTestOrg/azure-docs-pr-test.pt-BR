---
title: "aaaAdd um laboratório de tooa claimable VM no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooadd um laboratório de tooa claimable máquina de virtual no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="4a0d8-103">Adicionar um laboratório de tooa claimable VM no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4a0d8-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="4a0d8-104">Adicionar um laboratório de tooa claimable VM em um toohow de maneira semelhante você [adicionar uma VM padrão](devtest-lab-add-vm.md) – de uma *base* seja um [imagem personalizada](devtest-lab-create-template.md), [fórmula](devtest-lab-manage-formulas.md), ou [imagem do Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="4a0d8-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="4a0d8-105">Este tutorial orienta você a usar Olá tooadd portal do Azure um laboratório de tooa VM claimable DevTest Labs e mostra o processo de saudação que um usuário segue tooclaim Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0d8-106">Se você implantar máquinas virtuais do laboratório por meio de [modelos do Azure Resource Manager](devtest-lab-create-environment-from-arm.md), você pode criar VMs claimable por configuração Olá **allowClaim** tootrue de propriedade na seção de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="4a0d8-107">Etapas tooadd um laboratório de tooa claimable VM no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4a0d8-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="4a0d8-108">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4a0d8-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4a0d8-109">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="4a0d8-110">Saudação de laboratórios, selecione lista laboratório Olá no qual você deseja toocreate Olá claimable VM.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="4a0d8-111">No laboratório de saudação **visão geral** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="4a0d8-113">Em Olá **escolher uma base** folha, selecione uma base para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="4a0d8-114">Em Olá **Máquina Virtual** folha, digite um nome para a máquina virtual da nova Olá no hello **nome da máquina Virtual** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="4a0d8-116">Insira um **nome de usuário** que tem privilégios de administrador na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="4a0d8-117">Se você quiser toouse uma senha armazenada em seu [armazenamento secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecione **usar um segredo salvo**e especifique um valor de chave que corresponde a tooyour segredo (senha).</span><span class="sxs-lookup"><span data-stu-id="4a0d8-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="4a0d8-118">Caso contrário, digite uma senha no campo de texto de saudação rotulado **digite um valor**.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="4a0d8-119">Olá **tipo de disco de máquina Virtual** determina qual tipo de disco de armazenamento será permitido para máquinas virtuais de saudação laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="4a0d8-120">Selecione **tamanho da máquina Virtual** e selecione uma das Olá predefinidos itens que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="4a0d8-121">Selecione **artefatos** e, na lista de saudação de artefatos, selecionar e configurar os artefatos de saudação que deseja que a imagem base do tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="4a0d8-122">Se você for novo laboratórios de tooDevTest ou configurando artefatos, consulte toohello [adicionar um tooa de artefato existente VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) seção e, em seguida, retornar aqui quando terminar.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="4a0d8-123">Selecione **configurações avançadas** opções de opções e expiração de rede da VM do tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="4a0d8-124">Em **opções de declaração**, escolha **Sim** máquina de saudação toomake claimable.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![Escolha toomake Olá claimable de VM.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="4a0d8-126">Se você quiser tooview ou copia modelo do Azure Resource Manager Olá, consulte toohello [do Azure Resource Manager Salvar modelo](devtest-lab-add-vm.md#save-azure-resource-manager-template) seção e retornar aqui quando terminar.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="4a0d8-127">Selecione **criar** tooadd Olá especificado laboratório toohello de VM.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="4a0d8-128">folha de laboratório Olá exibe o status de saudação da criação da VM Olá - primeiro como **criando**, em seguida, como **executando** após Olá VM foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="4a0d8-129">Usando uma VM declarável</span><span class="sxs-lookup"><span data-stu-id="4a0d8-129">Using a claimable VM</span></span>

<span data-ttu-id="4a0d8-130">Um usuário pode declaração qualquer VM na lista de saudação de "Máquinas de virtuais Claimable" seguindo uma destas etapas:</span><span class="sxs-lookup"><span data-stu-id="4a0d8-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="4a0d8-131">Na lista de saudação de "Máquinas de virtuais Claimable" na parte inferior da saudação da folha de visão geral do laboratório hello, com o botão direito em uma saudação VMs na lista de saudação e escolha **máquina declaração**.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![Solicite uma VM declarável específica.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="4a0d8-133">Na parte superior de saudação do hello **visão geral** folha, escolha **declaração qualquer**.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="4a0d8-134">Uma máquina virtual aleatória é atribuída na lista de saudação de VMs claimable.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![Solicite uma VM declarável.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="4a0d8-136">Depois que um usuário declara uma VM, ela é movida para cima em sua lista de “Minhas máquinas virtuais” e não é mais declarável por nenhum outro usuário.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a0d8-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a0d8-137">Next steps</span></span>
* <span data-ttu-id="4a0d8-138">Uma vez Olá VM tiver sido criada, você pode se conectar toohello VM selecionando **conectar** na folha de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="4a0d8-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="4a0d8-139">Explorar Olá [DevTest Labs Azure Resource Manager QuickStart Galeria de modelos](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="4a0d8-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
