---
title: aaaConfigure uma rede virtual no Azure DevTest Labs | Microsoft Docs
description: "Saiba como tooconfigure uma rede virtual existente e a sub-rede e usá-los em uma VM com o Azure DevTest Labs"
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
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="e8c2c-103">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e8c2c-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="e8c2c-104">Conforme explicado no artigo hello, [adicionar uma VM com o laboratório de tooa artefatos](devtest-lab-add-vm-with-artifacts.md), quando você cria uma VM em um laboratório, você pode especificar uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="e8c2c-105">Um cenário para fazer isso é se você precisar tooaccess seus recursos de rede corporativa de suas VMs usando Olá rede virtual que foi configurado com a rota expressa ou VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="e8c2c-106">Olá seções a seguir ilustram como tooadd sua rede virtual existente nas configurações de rede Virtual do laboratório para que ela seja toochoose disponível ao criar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="e8c2c-107">Configurar uma rede virtual para um laboratório com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8c2c-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="e8c2c-108">Olá etapas a seguir orientam na adição de um laboratório de tooa rede (e subrede) de virtual existente para que ele pode ser usado ao criar uma VM em Olá mesmo laboratório.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="e8c2c-109">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e8c2c-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e8c2c-110">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="e8c2c-111">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="e8c2c-112">Na folha do laboratório hello, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="e8c2c-113">No laboratório de saudação **configuração** folha, selecione **redes virtuais**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="e8c2c-114">Em Olá **redes virtuais** folha, verá uma lista de redes virtuais configuradas para o laboratório atual hello, bem como saudação padrão rede virtual que é criado para o laboratório.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="e8c2c-115">Selecione **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-115">Select **+ Add**.</span></span>
   
    ![Adicionar um laboratório de tooyour de rede virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="e8c2c-117">Em Olá **rede Virtual** folha, selecione **[Selecione rede virtual]**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selecionar uma rede virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="e8c2c-119">Em Olá **rede virtual escolha** folha, a rede virtual desejado de saudação select.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="e8c2c-120">folha Hello mostra todas as redes virtuais Olá que estão em Olá mesmo região na assinatura Olá laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="e8c2c-121">Depois de selecionar uma rede virtual, você retornará toohello **rede Virtual** clique Olá sub-rede na lista de saudação na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Lista de sub-redes](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="e8c2c-123">folha de sub-rede do laboratório de saudação é exibida.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-123">hello Lab Subnet blade is displayed.</span></span>

    ![Folha Sub-rede do laboratório](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="e8c2c-125">Especifique um **nome da Sub-rede do laboratório**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="e8c2c-126">tooallow um toobe sub-rede usada no laboratório de criação de VM, selecione **uso na criação da máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="e8c2c-127">tooenable um [compartilhado endereço IP público](devtest-lab-shared-ip.md), selecione **habilitar compartilhada IP público**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="e8c2c-128">Selecione tooallow de endereços IP públicos em uma sub-rede, **permitir a criação de IP pública**.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="e8c2c-129">Em Olá **máximo de máquinas virtuais por usuário** , especifique Olá VMs máximo por usuário para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="e8c2c-130">Se você quiser um número irrestrito de VMs, deixe esse campo em branco.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="e8c2c-131">Selecione **Okey** tooclose folha de sub-rede do laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="e8c2c-132">Selecione **salvar** folha de rede tooclose Olá Virtual.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="e8c2c-133">Hello rede virtual já está configurado, ele pode ser selecionado durante a criação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e8c2c-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="e8c2c-134">toosee como toocreate uma máquina virtual e especifique uma rede virtual, consulte o artigo toohello, [adicionar uma VM com o laboratório de tooa artefatos](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e8c2c-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="e8c2c-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8c2c-135">Next steps</span></span>
<span data-ttu-id="e8c2c-136">Depois que você adicionou a saudação desejado laboratório tooyour de rede virtual, a próxima etapa de saudação é muito[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e8c2c-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

