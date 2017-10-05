---
title: "Criar a primeira VM em um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como criar a primeira máquina virtual em um laboratório no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="af03b-103">Criar a primeira VM no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="af03b-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="af03b-104">Ao acessar inicialmente o DevTest Labs e desejar criar a primeira VM, você deverá fazer isso usando uma [imagem do Marketplace base](devtest-lab-configure-marketplace-images.md) pré-carregada.</span><span class="sxs-lookup"><span data-stu-id="af03b-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="af03b-105">No futuro, você também poderá escolher uma imagem personalizada [ e uma fórmula](devtest-lab-add-vm.md) ao criar mais VMs.</span><span class="sxs-lookup"><span data-stu-id="af03b-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="af03b-106">Este tutorial orienta você pelo Portal do Azure para adicionar uma VM a um laboratório no DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="af03b-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="af03b-107">Etapas para adicionar a primeira VM a um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="af03b-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="af03b-108">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="af03b-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="af03b-109">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="af03b-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="af03b-110">Na lista de laboratórios, selecione o laboratório no qual você deseja criar a VM.</span><span class="sxs-lookup"><span data-stu-id="af03b-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="af03b-111">Na folha **Visão geral** do laboratório, selecione **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="af03b-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="af03b-113">Na folha **Escolher uma base**, selecione uma imagem do Marketplace para a VM.</span><span class="sxs-lookup"><span data-stu-id="af03b-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="af03b-114">Na folha **Máquina virtual**, insira um nome para a nova máquina virtual na caixa de texto **Nome da máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="af03b-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="af03b-116">Insira um **Nome de Usuário** que receberá privilégios de administrador na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af03b-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="af03b-117">Digite uma senha no campo de texto identificado como **Digite um valor**.</span><span class="sxs-lookup"><span data-stu-id="af03b-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="af03b-118">O **tipo de disco de máquina virtual** determina que tipo de disco de armazenamento é permitido para as máquinas virtuais no laboratório.</span><span class="sxs-lookup"><span data-stu-id="af03b-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="af03b-119">Selecione **Tamanho da máquina virtual** e selecione um dos itens predefinidos que especificam os núcleos de processador, o tamanho da RAM e o tamanho do disco rígido da VM a ser criada.</span><span class="sxs-lookup"><span data-stu-id="af03b-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="af03b-120">Selecione **Artefatos** e, na lista de artefatos, selecione e configure os artefatos que você deseja adicionar à imagem base.</span><span class="sxs-lookup"><span data-stu-id="af03b-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="af03b-121">**Observação:** se você for iniciante em Laboratórios de Desenvolvimento/Teste ou na configuração de artefatos, veja a seção [Adicionar um artefato existente a uma VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) e volte aqui quando terminar.</span><span class="sxs-lookup"><span data-stu-id="af03b-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="af03b-122">Selecione **Criar** para adicionar a VM especificada ao laboratório.</span><span class="sxs-lookup"><span data-stu-id="af03b-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="af03b-123">A folha do laboratório exibe o status da criação da VM; primeiro como **Criando** e como **Executando** após a inicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="af03b-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af03b-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af03b-124">Next steps</span></span>
* <span data-ttu-id="af03b-125">Após a criação da VM, você poderá se conectar à VM selecionando **Conectar** na folha da VM.</span><span class="sxs-lookup"><span data-stu-id="af03b-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="af03b-126">Marque [Adicionar uma VM a um laboratório](devtest-lab-add-vm.md) para informações mais completas sobre como adicionar VMs subsequentes no laboratório.</span><span class="sxs-lookup"><span data-stu-id="af03b-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="af03b-127">Explore a [galeria de modelos de Início Rápido do Azure Resource Manager do DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="af03b-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
