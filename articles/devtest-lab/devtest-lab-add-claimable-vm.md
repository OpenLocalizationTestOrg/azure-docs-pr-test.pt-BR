---
title: "Adicionar uma VM declarável a um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como adicionar uma máquina virtual declarável a um laboratório no Azure DevTest Labs"
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
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="fb41d-103">Adicionar uma VM declarável a um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fb41d-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="fb41d-104">Você adiciona uma VM declarável a um laboratório de maneira semelhante a como [adiciona uma VM padrão](devtest-lab-add-vm.md) – de uma *base* que é uma [imagem personalizada](devtest-lab-create-template.md), [fórmula](devtest-lab-manage-formulas.md), ou [imagem do Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="fb41d-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="fb41d-105">Este tutorial explica como usar o portal do Azure para adicionar uma VM declarável a um laboratório no DevTest Labs e mostra o processo que um usuário segue para declarar a VM.</span><span class="sxs-lookup"><span data-stu-id="fb41d-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="fb41d-106">Se você implantar VMs de laboratório por meio de [modelos do Azure Resource Manager](devtest-lab-create-environment-from-arm.md), poderá criar VMs declaráveis definindo a propriedade **allowClaim** como verdadeiro na seção de propriedades.</span><span class="sxs-lookup"><span data-stu-id="fb41d-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="fb41d-107">Etapas para adicionar uma VM declarável a um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fb41d-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="fb41d-108">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fb41d-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="fb41d-109">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="fb41d-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="fb41d-110">Na lista de laboratórios, selecione o laboratório no qual você deseja criar a VM de declaração.</span><span class="sxs-lookup"><span data-stu-id="fb41d-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="fb41d-111">Na folha **Visão geral** do laboratório, selecione **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fb41d-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="fb41d-113">Na folha **Escolher uma base** , selecione uma base para a VM.</span><span class="sxs-lookup"><span data-stu-id="fb41d-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="fb41d-114">Na folha **Máquina virtual**, insira um nome para a nova máquina virtual na caixa de texto **Nome da máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="fb41d-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="fb41d-116">Insira um **Nome de Usuário** que receberá privilégios de administrador na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fb41d-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="fb41d-117">Se você quiser usar uma senha armazenada em seu [repositório secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecione **Usar um segredo salvo** e especifique um valor de chave que corresponda ao seu segredo (senha).</span><span class="sxs-lookup"><span data-stu-id="fb41d-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="fb41d-118">Caso contrário, digite uma senha no campo de texto rotulado **Digite um valor**.</span><span class="sxs-lookup"><span data-stu-id="fb41d-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="fb41d-119">O **tipo de disco de máquina virtual** determina que tipo de disco de armazenamento é permitido para as máquinas virtuais no laboratório.</span><span class="sxs-lookup"><span data-stu-id="fb41d-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="fb41d-120">Selecione **Tamanho da máquina virtual** e selecione um dos itens predefinidos que especificam os núcleos de processador, o tamanho da RAM e o tamanho do disco rígido da VM a ser criada.</span><span class="sxs-lookup"><span data-stu-id="fb41d-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="fb41d-121">Selecione **Artefatos** e, na lista de artefatos, selecione e configure os artefatos que você deseja adicionar à imagem base.</span><span class="sxs-lookup"><span data-stu-id="fb41d-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="fb41d-122">Se você for iniciante em Laboratórios de Desenvolvimento/Teste ou na configuração de artefatos, veja a seção [Adicionar um artefato existente a uma VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) e volte aqui quando terminar.</span><span class="sxs-lookup"><span data-stu-id="fb41d-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="fb41d-123">Selecione **Configurações avançadas** para configurar as opções de expiração e as opções de rede da VM.</span><span class="sxs-lookup"><span data-stu-id="fb41d-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="fb41d-124">Em **Opções de declaração**, escolha **Sim** para tornar a máquina declarável.</span><span class="sxs-lookup"><span data-stu-id="fb41d-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Opte por tornar a VM declarável.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="fb41d-126">Se quiser exibir ou copiar o modelo do Azure Resource Manager, veja a seção [Salvar modelo do Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) e retorne para cá quando terminar.</span><span class="sxs-lookup"><span data-stu-id="fb41d-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="fb41d-127">Selecione **Criar** para adicionar a VM especificada ao laboratório.</span><span class="sxs-lookup"><span data-stu-id="fb41d-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="fb41d-128">A folha do laboratório exibe o status da criação da VM; primeiro como **Criando** e como **Executando** após a inicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="fb41d-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="fb41d-129">Usando uma VM declarável</span><span class="sxs-lookup"><span data-stu-id="fb41d-129">Using a claimable VM</span></span>

<span data-ttu-id="fb41d-130">Um usuário pode declarar qualquer VM na lista de “Máquinas virtuais declaráveis” realizando uma destas etapas:</span><span class="sxs-lookup"><span data-stu-id="fb41d-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="fb41d-131">Na lista de “Máquinas virtuais declaráveis” na parte inferior da folha Visão Geral do laboratório, clique com o botão direito do mouse em uma das VMs da lista e escolha **Declarar computador**.</span><span class="sxs-lookup"><span data-stu-id="fb41d-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Solicite uma VM declarável específica.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="fb41d-133">Na parte superior da folha **Visão Geral**, escolha **Declarar qualquer um**.</span><span class="sxs-lookup"><span data-stu-id="fb41d-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="fb41d-134">Uma máquina virtual aleatória é atribuída da lista de VMs declaráveis.</span><span class="sxs-lookup"><span data-stu-id="fb41d-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Solicite uma VM declarável.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="fb41d-136">Depois que um usuário declara uma VM, ela é movida para cima em sua lista de “Minhas máquinas virtuais” e não é mais declarável por nenhum outro usuário.</span><span class="sxs-lookup"><span data-stu-id="fb41d-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb41d-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb41d-137">Next steps</span></span>
* <span data-ttu-id="fb41d-138">Após a criação da VM, você poderá se conectar à VM selecionando **Conectar** na folha da VM.</span><span class="sxs-lookup"><span data-stu-id="fb41d-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="fb41d-139">Explorar a [galeria de modelos de Início Rápido do Azure Resource Manager do DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="fb41d-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
