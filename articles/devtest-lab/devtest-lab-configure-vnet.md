---
title: Configurar uma rede virtual no Azure DevTest Labs | Microsoft Docs
description: "Saiba como configurar uma rede virtual e sub-rede existente e usá-las em uma VM com o Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="ed6ac-103">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ed6ac-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="ed6ac-104">Conforme explicado no artigo [Adicionar uma VM com artefatos a um laboratório](devtest-lab-add-vm-with-artifacts.md), quando cria uma VM em um laboratório, você pode especificar uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="ed6ac-105">Um cenário no qual isso é possível é quando você precisa acessar os recursos da rede corporativa por meio de suas VMs usando a rede virtual configurada com o ExpressRoute ou a VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="ed6ac-106">As seções a seguir ilustram como adicionar sua rede virtual existente às configurações de Rede Virtual de um laboratório, para que ela esteja disponível para escolha durante a criação de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="ed6ac-107">Configurar uma rede virtual para um laboratório usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ed6ac-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="ed6ac-108">As etapas a seguir orientarão você pela adição de uma rede virtual (e sub-rede) existente a um laboratório, para que ela possa ser usada durante a criação de uma VM no mesmo Laboratório.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="ed6ac-109">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ed6ac-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="ed6ac-110">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="ed6ac-111">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="ed6ac-112">Na folha do laboratório, selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="ed6ac-113">Na folha **Configuração** do laboratório, selecione **Redes virtuais**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="ed6ac-114">Na folha **Redes virtuais** , você vê uma lista das redes virtuais configuradas para o laboratório atual, bem como a rede virtual padrão que é criada para o laboratório.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="ed6ac-115">Selecione **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-115">Select **+ Add**.</span></span>
   
    ![Adicionar uma rede virtual existente ao seu laboratório](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="ed6ac-117">Na folha **Rede virtual**, selecione **[Selecionar rede virtual]**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selecionar uma rede virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="ed6ac-119">Na folha **Escolher rede virtual** , selecione a rede virtual desejada.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="ed6ac-120">A folha mostra todas as redes virtuais que estão na mesma região da assinatura do que o laboratório.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="ed6ac-121">Depois de selecionar uma rede virtual, você retornará à **Rede virtual**. Clique na sub-rede na lista na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Lista de sub-redes](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="ed6ac-123">A Folha de Sub-rede do laboratório é exibida.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-123">The Lab Subnet blade is displayed.</span></span>

    ![Folha Sub-rede do laboratório](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="ed6ac-125">Especifique um **nome da Sub-rede do laboratório**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="ed6ac-126">Para permitir o uso de uma sub-rede na criação da VM do laboratório, selecione **Usar na criação da máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="ed6ac-127">Para habilitar um [endereço IP público compartilhado](devtest-lab-shared-ip.md), selecione **Habilitar IP público compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="ed6ac-128">Para permitir endereços IP públicos em uma sub-rede, selecione **Permitir criação de IP público**.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="ed6ac-129">No campo **Máximo de máquinas virtuais por usuário**, especifique o número máximo de VMs por usuário para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="ed6ac-130">Se você quiser um número irrestrito de VMs, deixe esse campo em branco.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="ed6ac-131">Selecione **OK** para fechar a folha Sub-rede do Laboratório.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="ed6ac-132">Selecione **Salvar** para fechar a folha da Rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="ed6ac-133">Agora que a rede virtual está configurada, ela poderá ser selecionada durante a criação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="ed6ac-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="ed6ac-134">Para saber como criar uma VM e especificar uma rede virtual, consulte o artigo [Adicionar uma VM com artefatos a um laboratório](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="ed6ac-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="ed6ac-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed6ac-135">Next steps</span></span>
<span data-ttu-id="ed6ac-136">Depois de adicionar a rede virtual desejada ao seu laboratório, a próxima etapa será [adicionar uma VM ao seu laboratório](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="ed6ac-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

