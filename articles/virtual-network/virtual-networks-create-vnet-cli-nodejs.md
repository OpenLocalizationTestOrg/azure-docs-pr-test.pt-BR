---
title: Criar uma rede virtual usando a CLI do Azure 1.0 | Microsoft Docs
description: Saiba como criar uma rede virtual usando a CLI do Azure 1.0 | Resource Manager.
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="17b4f-103">Criar uma rede virtual usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="17b4f-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="17b4f-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="17b4f-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="17b4f-105">A Microsoft recomenda criar recursos por meio do modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="17b4f-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="17b4f-106">Para saber mais sobre as diferenças entre os dois modelos, leia o artigo [Entender os modelos de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="17b4f-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="17b4f-107">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="17b4f-107">CLI versions to complete the task</span></span>
<span data-ttu-id="17b4f-108">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="17b4f-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="17b4f-109">[CLI do Azure 2.0](virtual-networks-create-vnet-arm-cli.md) – nossa próxima geração de CLI para o modelo de implantação do resource manager</span><span class="sxs-lookup"><span data-stu-id="17b4f-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="17b4f-110">[CLI 1.0 do Azure](#create-a-virtual-network) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="17b4f-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="17b4f-111">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="17b4f-111">Create a virtual network</span></span>

<span data-ttu-id="17b4f-112">Para criar uma rede virtual usando a CLI do Azure, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="17b4f-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="17b4f-113">Instale e configure a CLI do Azure seguindo as etapas do artigo [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="17b4f-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="17b4f-114">Crie uma VNet e uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="17b4f-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="17b4f-115">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="17b4f-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="17b4f-116">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="17b4f-116">Parameters used:</span></span>

   * <span data-ttu-id="17b4f-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-117">**--vnet**.</span></span> <span data-ttu-id="17b4f-118">Nome da rede virtual a ser criada.</span><span class="sxs-lookup"><span data-stu-id="17b4f-118">Name of the VNet to be created.</span></span> <span data-ttu-id="17b4f-119">Para o nosso cenário, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="17b4f-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="17b4f-120">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="17b4f-121">Espaço de endereço da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="17b4f-121">VNet address space.</span></span> <span data-ttu-id="17b4f-122">Para o nosso cenário, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="17b4f-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="17b4f-123">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="17b4f-124">Máscara de rede no formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="17b4f-124">Network mask in CIDR format.</span></span> <span data-ttu-id="17b4f-125">Para o nosso cenário, *16*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="17b4f-126">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="17b4f-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="17b4f-127">Nome da primeira sub-rede.</span><span class="sxs-lookup"><span data-stu-id="17b4f-127">Name of the first subnet.</span></span> <span data-ttu-id="17b4f-128">Para o nosso cenário, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="17b4f-129">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="17b4f-130">Endereço IP inicial da sub-rede ou espaço de endereço da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="17b4f-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="17b4f-131">Em nosso cenário, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="17b4f-132">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="17b4f-133">Máscara de rede no formato CIDR para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="17b4f-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="17b4f-134">Para o nosso cenário, *24*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="17b4f-135">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-135">**-l (or --location)**.</span></span> <span data-ttu-id="17b4f-136">Região do Azure em que a VNet é criada.</span><span class="sxs-lookup"><span data-stu-id="17b4f-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="17b4f-137">Para o nosso cenário, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="17b4f-138">Crie uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="17b4f-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="17b4f-139">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="17b4f-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="17b4f-140">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="17b4f-140">Parameters used:</span></span>

   * <span data-ttu-id="17b4f-141">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="17b4f-142">Nome da rede virtual onde a sub-rede será criada.</span><span class="sxs-lookup"><span data-stu-id="17b4f-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="17b4f-143">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="17b4f-144">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-144">**-n (or --name)**.</span></span> <span data-ttu-id="17b4f-145">Nome da nova sub-rede.</span><span class="sxs-lookup"><span data-stu-id="17b4f-145">Name of the new subnet.</span></span> <span data-ttu-id="17b4f-146">Para o nosso cenário, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="17b4f-147">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="17b4f-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="17b4f-148">Bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="17b4f-148">Subnet CIDR block.</span></span> <span data-ttu-id="17b4f-149">Para o nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="17b4f-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="17b4f-150">Para exibir as propriedades da nova VNet:</span><span class="sxs-lookup"><span data-stu-id="17b4f-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="17b4f-151">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="17b4f-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="17b4f-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="17b4f-152">Next steps</span></span>

<span data-ttu-id="17b4f-153">Saiba como se conectar:</span><span class="sxs-lookup"><span data-stu-id="17b4f-153">Learn how to connect:</span></span>

- <span data-ttu-id="17b4f-154">Uma VM (máquina virtual) em uma rede virtual lendo o artigo [Criar uma VM Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="17b4f-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="17b4f-155">Em vez de criar uma rede virtual e sub-rede nas etapas dos artigos, você pode selecionar uma rede virtual e uma sub-rede existente para se conectar a uma VM.</span><span class="sxs-lookup"><span data-stu-id="17b4f-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="17b4f-156">A rede virtual para outras redes virtuais, lendo o artigo [Conectar VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17b4f-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="17b4f-157">A rede virtual para uma rede local usando uma VPN (rede privada virtual) site a site ou um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="17b4f-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="17b4f-158">Saiba como lendo [Conectar uma VNet a uma rede local usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [Vincular uma VNet a um circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="17b4f-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>