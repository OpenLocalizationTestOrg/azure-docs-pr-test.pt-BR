---
title: "aaaCreate usando uma rede virtual Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate usando uma rede virtual Olá 1.0 da CLI do Azure | Gerenciador de recursos."
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
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="b9d5b-103">Criar uma rede virtual usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b9d5b-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="b9d5b-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="b9d5b-105">A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="b9d5b-106">mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b9d5b-107">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="b9d5b-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b9d5b-108">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b9d5b-109">[2.0 do CLI do Azure](virtual-networks-create-vnet-arm-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="b9d5b-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="b9d5b-110">[1.0 de CLI do Azure](#create-a-virtual-network) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="b9d5b-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="b9d5b-111">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="b9d5b-111">Create a virtual network</span></span>

<span data-ttu-id="b9d5b-112">toocreate usando uma rede virtual Olá CLI do Azure, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="b9d5b-113">Instalar e configurar Olá CLI do Azure por Olá seguir as etapas em Olá [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="b9d5b-114">Crie uma VNet e uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="b9d5b-115">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="b9d5b-116">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-116">Parameters used:</span></span>

   * <span data-ttu-id="b9d5b-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-117">**--vnet**.</span></span> <span data-ttu-id="b9d5b-118">Nome da saudação VNet toobe criado.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="b9d5b-119">Para o nosso cenário, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="b9d5b-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="b9d5b-120">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="b9d5b-121">Espaço de endereço da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-121">VNet address space.</span></span> <span data-ttu-id="b9d5b-122">Para o nosso cenário, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="b9d5b-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="b9d5b-123">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="b9d5b-124">Máscara de rede no formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-124">Network mask in CIDR format.</span></span> <span data-ttu-id="b9d5b-125">Para o nosso cenário, *16*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="b9d5b-126">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="b9d5b-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="b9d5b-127">Nome da sub-rede primeiro hello.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-127">Name of hello first subnet.</span></span> <span data-ttu-id="b9d5b-128">Para o nosso cenário, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="b9d5b-129">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="b9d5b-130">Endereço IP inicial da sub-rede ou espaço de endereço da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="b9d5b-131">Em nosso cenário, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="b9d5b-132">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="b9d5b-133">Máscara de rede no formato CIDR para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="b9d5b-134">Para o nosso cenário, *24*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="b9d5b-135">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-135">**-l (or --location)**.</span></span> <span data-ttu-id="b9d5b-136">Região do Azure onde Olá VNet é criada.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="b9d5b-137">Para o nosso cenário, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="b9d5b-138">Crie uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="b9d5b-139">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="b9d5b-140">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-140">Parameters used:</span></span>

   * <span data-ttu-id="b9d5b-141">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="b9d5b-142">Nome da saudação redes onde sub-rede Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="b9d5b-143">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="b9d5b-144">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-144">**-n (or --name)**.</span></span> <span data-ttu-id="b9d5b-145">Nome da nova subrede hello.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-145">Name of hello new subnet.</span></span> <span data-ttu-id="b9d5b-146">Para o nosso cenário, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="b9d5b-147">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="b9d5b-148">Bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-148">Subnet CIDR block.</span></span> <span data-ttu-id="b9d5b-149">Para o nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="b9d5b-150">Propriedades de saudação tooview de Olá nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="b9d5b-151">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
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

## <a name="next-steps"></a><span data-ttu-id="b9d5b-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9d5b-152">Next steps</span></span>

<span data-ttu-id="b9d5b-153">Saiba como tooconnect:</span><span class="sxs-lookup"><span data-stu-id="b9d5b-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="b9d5b-154">Uma rede virtual de tooa de máquina virtual (VM) lendo Olá [criar uma VM do Linux](../virtual-machines/linux/quick-create-cli.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="b9d5b-155">Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="b9d5b-156">Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="b9d5b-157">Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="b9d5b-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="b9d5b-158">Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b9d5b-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
