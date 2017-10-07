---
title: "aaaCreate sua primeira VM em um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como toocreate sua primeira máquina virtual em um laboratório no Azure DevTest Labs"
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
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="27ea0-103">Criar a primeira VM no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="27ea0-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="27ea0-104">Quando você inicialmente acessar DevTest Labs e deseja toocreate sua VM primeiro, você provavelmente vai fazer isso usando um pré-carregados [imagem do marketplace base](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="27ea0-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="27ea0-105">Posteriormente no, você também será capaz de toochoose de um [imagem personalizada e uma fórmula](devtest-lab-add-vm.md) ao criar mais VMs.</span><span class="sxs-lookup"><span data-stu-id="27ea0-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="27ea0-106">Este tutorial orienta usando Olá tooadd portal do Azure laboratório em DevTest Labs tooa VM primeiro.</span><span class="sxs-lookup"><span data-stu-id="27ea0-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="27ea0-107">Etapas tooadd seu primeiro laboratório tooa VM no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="27ea0-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="27ea0-108">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="27ea0-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="27ea0-109">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="27ea0-110">Saudação de laboratórios, selecione lista laboratório Olá no qual você deseja toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="27ea0-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="27ea0-111">No laboratório de saudação **visão geral** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="27ea0-113">Em Olá **escolher uma base** folha, selecione a imagem de um mercado para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="27ea0-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="27ea0-114">Em Olá **Máquina Virtual** folha, digite um nome para a máquina virtual da nova Olá no hello **nome da máquina Virtual** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="27ea0-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="27ea0-116">Insira um **nome de usuário** que tem privilégios de administrador na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="27ea0-117">Digite uma senha no campo de texto de saudação rotulado **digite um valor**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="27ea0-118">Olá **tipo de disco de máquina Virtual** determina qual tipo de disco de armazenamento será permitido para máquinas virtuais de saudação laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="27ea0-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="27ea0-119">Selecione **tamanho da máquina Virtual** e selecione uma das Olá predefinidos itens que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate.</span><span class="sxs-lookup"><span data-stu-id="27ea0-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="27ea0-120">Selecione **artefatos** - lista de saudação de artefatos - e selecione Configurar artefatos Olá que deseja que a imagem base do tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="27ea0-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="27ea0-121">**Observação:** se você for novo laboratórios de tooDevTest ou configurando artefatos, consulte toohello [adicionar um tooa de artefato existente VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) seção e, em seguida, retornar aqui quando terminar.</span><span class="sxs-lookup"><span data-stu-id="27ea0-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="27ea0-122">Selecione **criar** tooadd Olá especificado laboratório toohello de VM.</span><span class="sxs-lookup"><span data-stu-id="27ea0-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="27ea0-123">folha de laboratório Olá exibe o status de saudação da criação da VM Olá - primeiro como **criando**, em seguida, como **executando** após Olá VM foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="27ea0-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27ea0-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27ea0-124">Next steps</span></span>
* <span data-ttu-id="27ea0-125">Uma vez Olá VM tiver sido criada, você pode se conectar toohello VM selecionando **conectar** na folha de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="27ea0-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="27ea0-126">Check-out [adicionar um laboratório de tooa VM](devtest-lab-add-vm.md) para obter informações mais completas sobre como adicionar VMs subsequentes no laboratório.</span><span class="sxs-lookup"><span data-stu-id="27ea0-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="27ea0-127">Explorar Olá [Galeria de modelos do DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="27ea0-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
