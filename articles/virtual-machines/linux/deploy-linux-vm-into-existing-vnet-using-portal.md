---
title: aaaDeploy VMs do Linux em uma rede existente com o portal do Azure | Microsoft Docs
description: "Implante uma VM do Linux em uma rede Virtual do Azure existente usando o portal de saudação."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="50a40-103">Como toodeploy uma máquina virtual do Linux em uma rede Virtual do Azure existente com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="50a40-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="50a40-104">Este artigo mostra como toodeploy uma máquina virtual (VM) em uma rede virtual existente (VNet).</span><span class="sxs-lookup"><span data-stu-id="50a40-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="50a40-105">Os ativos do Azure como VNets e grupos de segurança de rede devem ser recursos estáticos e de longa duração que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="50a40-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="50a40-106">Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por constantes reimplantações sem nenhuma infraestrutura de toohello efeitos adversos.</span><span class="sxs-lookup"><span data-stu-id="50a40-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="50a40-107">Pensar em uma rede virtual como sendo um tradicional comutador de rede de hardware - você não precisará tooconfigure alternar de um novo hardware com cada implantação.</span><span class="sxs-lookup"><span data-stu-id="50a40-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="50a40-108">Com uma rede virtual configurada corretamente, você pode continuar toodeploy novos servidores para essa rede virtual repetidamente com poucas, se houver, alterações necessárias sobre a vida útil de saudação do hello VNet.</span><span class="sxs-lookup"><span data-stu-id="50a40-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="50a40-109">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="50a40-109">Create hello resource group</span></span>

<span data-ttu-id="50a40-110">Primeiro, crie um tooorganize do grupo de recursos tudo que você cria neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="50a40-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="50a40-111">Para saber mais sobre os grupos de recursos do Azure, confira [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="50a40-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="50a40-113">Criar hello VNet</span><span class="sxs-lookup"><span data-stu-id="50a40-113">Create hello VNet</span></span>

<span data-ttu-id="50a40-114">Em seguida, crie VMs em uma saudação toolaunch de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="50a40-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="50a40-115">Olá VNet contém uma sub-rede e está associada ao grupo de segurança de rede Olá essa sub-rede em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="50a40-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="50a40-117">Adicionar uma sub-rede de toohello VNic</span><span class="sxs-lookup"><span data-stu-id="50a40-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="50a40-118">Placas de rede virtual (VNics) são importantes para você pode conectá-los toodifferent VMs.</span><span class="sxs-lookup"><span data-stu-id="50a40-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="50a40-119">Essa abordagem mantém Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário.</span><span class="sxs-lookup"><span data-stu-id="50a40-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="50a40-120">Crie uma VNic e associá-lo a sub-rede Olá criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="50a40-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="50a40-122">Criar grupo de segurança de rede Olá</span><span class="sxs-lookup"><span data-stu-id="50a40-122">Create hello network security group</span></span>

<span data-ttu-id="50a40-123">Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello.</span><span class="sxs-lookup"><span data-stu-id="50a40-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="50a40-124">Para obter mais informações sobre grupos de segurança de rede do Azure, confira [O que é um grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="50a40-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="50a40-126">Adicionar uma regra de permissão de SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="50a40-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="50a40-127">Olá VM precisa ter acesso de saudação à internet, para uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM é criada.</span><span class="sxs-lookup"><span data-stu-id="50a40-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="50a40-129">Associar Olá NSG sub-rede Olá</span><span class="sxs-lookup"><span data-stu-id="50a40-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="50a40-130">Com o hello rede virtual e sub-rede Olá criada, associe o grupo de segurança de rede Olá sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="50a40-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="50a40-131">Os grupos de segurança de rede podem ser associados a uma sub-rede inteira ou a uma VNic individual.</span><span class="sxs-lookup"><span data-stu-id="50a40-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="50a40-132">Com o firewall Olá filtrando o tráfego no nível de sub-rede Olá, todos os VNics e Olá VMs na sub-rede Olá são protegidos pelo grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="50a40-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="50a40-133">Olá outra abordagem é Olá sendo de grupo de segurança de rede associado a apenas uma único VNic e proteger apenas uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="50a40-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="50a40-135">Implantar hello VM em Olá VNet e NSG</span><span class="sxs-lookup"><span data-stu-id="50a40-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="50a40-136">Usando Olá portal do Azure, Olá VM do Linux é implantado toohello grupo de recursos do Azure, redes, sub-rede e VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="50a40-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="50a40-138">Usando recursos existentes do hello toochoose portal, você instruir Olá toodeploy Azure VM dentro da rede existente hello.</span><span class="sxs-lookup"><span data-stu-id="50a40-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="50a40-139">Depois que uma VNET e uma sub-rede forem implantadas, elas poderão ser mantidas como recursos estáticos ou permanentes na região do Azure.</span><span class="sxs-lookup"><span data-stu-id="50a40-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="50a40-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50a40-140">Next steps</span></span>

* [<span data-ttu-id="50a40-141">Usar um modelo de Gerenciador de recursos do Azure toocreate uma implantação específica</span><span class="sxs-lookup"><span data-stu-id="50a40-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="50a40-142">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="50a40-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="50a40-143">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="50a40-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
