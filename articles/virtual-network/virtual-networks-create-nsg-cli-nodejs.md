---
title: "aaaCreate 1.0 da CLI do Azure de grupos de segurança - rede | Microsoft Docs"
description: "Saiba como toocreate e implantar grupos de segurança de rede usando Olá 1.0 da CLI do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="e91af-103">Criar grupos de segurança usando hello Azure CLI 1.0 de rede</span><span class="sxs-lookup"><span data-stu-id="e91af-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e91af-104">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="e91af-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="e91af-105">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="e91af-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="e91af-106">[1.0 de CLI do Azure](#how-to-create-the-nsg-for-the-front-end-subnet) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="e91af-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e91af-107">[2.0 do CLI do Azure](virtual-networks-create-nsg-arm-cli.md) -nosso CLI de última geração para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="e91af-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="e91af-108">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e91af-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="e91af-109">Você também pode [criar NSGs no modelo de implantação clássico Olá](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e91af-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="e91af-110">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="e91af-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="e91af-111">Como toocreate Olá NSG para Olá sub-rede front-end</span><span class="sxs-lookup"><span data-stu-id="e91af-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="e91af-112">toocreate um NSG chamado denominado *NSG-front-end* com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="e91af-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="e91af-113">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="e91af-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e91af-114">Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e91af-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="e91af-115">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="e91af-116">Executar Olá **nsg de rede do azure criar** comando toocreate um NSG.</span><span class="sxs-lookup"><span data-stu-id="e91af-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="e91af-117">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="e91af-118">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="e91af-118">Parameters:</span></span>
   
   * <span data-ttu-id="e91af-119">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="e91af-120">Nome do grupo de recursos de saudação onde Olá NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="e91af-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="e91af-121">Para o nosso cenário, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="e91af-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="e91af-122">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-122">**-l (or --location)**.</span></span> <span data-ttu-id="e91af-123">Região do Azure onde hello novo NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="e91af-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="e91af-124">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="e91af-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="e91af-125">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-125">**-n (or --name)**.</span></span> <span data-ttu-id="e91af-126">Nome para Olá novo NSG.</span><span class="sxs-lookup"><span data-stu-id="e91af-126">Name for hello new NSG.</span></span> <span data-ttu-id="e91af-127">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e91af-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="e91af-128">Executar Olá **criar regra nsg de rede do azure** comando toocreate uma regra que permita acesso tooport 3389 (RDP) de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="e91af-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="e91af-129">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="e91af-130">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="e91af-130">Parameters:</span></span>
   
   * <span data-ttu-id="e91af-131">**-a (or --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="e91af-132">Nome do NSG Olá quais Olá regra será criada.</span><span class="sxs-lookup"><span data-stu-id="e91af-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="e91af-133">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e91af-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="e91af-134">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-134">**-n (or --name)**.</span></span> <span data-ttu-id="e91af-135">Nome para a nova regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="e91af-135">Name for hello new rule.</span></span> <span data-ttu-id="e91af-136">Para o nosso cenário, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="e91af-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="e91af-137">**-c (or --access)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-137">**-c (or --access)**.</span></span> <span data-ttu-id="e91af-138">Nível de acesso para a regra de saudação (Deny ou permitir).</span><span class="sxs-lookup"><span data-stu-id="e91af-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="e91af-139">**-p (or --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="e91af-140">Protocolo (Tcp, Udp ou *) para a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="e91af-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="e91af-141">**-r (or --direction)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-141">**-r (or --direction)**.</span></span> <span data-ttu-id="e91af-142">Direção da conexão (Entrada ou Saída).</span><span class="sxs-lookup"><span data-stu-id="e91af-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="e91af-143">**-y (or --priority)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-143">**-y (or --priority)**.</span></span> <span data-ttu-id="e91af-144">Prioridade de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="e91af-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="e91af-145">**-f (or --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="e91af-146">Prefixo do endereço de origem no CIDR ou uso de marcas padrão.</span><span class="sxs-lookup"><span data-stu-id="e91af-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="e91af-147">**-o (or --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="e91af-148">Porta de origem ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="e91af-148">Source port, or port range.</span></span>
   * <span data-ttu-id="e91af-149">**-e (or --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="e91af-150">Prefixo do endereço de destino no CIDR ou uso de marcas padrão.</span><span class="sxs-lookup"><span data-stu-id="e91af-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="e91af-151">**-u (or --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="e91af-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="e91af-152">Porta de destino ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="e91af-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="e91af-153">Executar Olá **criar regra nsg de rede do azure** comando toocreate uma regra que permita acesso tooport 80 (HTTP) de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="e91af-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="e91af-154">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="e91af-155">Executar Olá **conjunto de sub-rede de rede virtual de rede do azure** comando toolink Olá NSG toohello front-end subrede.</span><span class="sxs-lookup"><span data-stu-id="e91af-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="e91af-156">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="e91af-157">Como toocreate Olá NSG para Olá volta terminar subrede</span><span class="sxs-lookup"><span data-stu-id="e91af-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="e91af-158">toocreate um NSG chamado denominado *back-end NSG* com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="e91af-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="e91af-159">Executar Olá **nsg de rede do azure criar** comando toocreate um NSG.</span><span class="sxs-lookup"><span data-stu-id="e91af-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="e91af-160">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="e91af-161">Executar Olá **criar regra nsg de rede do azure** comando toocreate uma regra que permita acesso tooport 1433 (SQL) da sub-rede de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="e91af-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="e91af-162">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="e91af-163">Executar Olá **criar regra nsg de rede do azure** comando toocreate uma regra que nega acesso toohello Internet do.</span><span class="sxs-lookup"><span data-stu-id="e91af-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="e91af-164">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="e91af-165">Executar Olá **conjunto de sub-rede de rede virtual de rede do azure** comando toolink Olá NSG toohello volta end subrede.</span><span class="sxs-lookup"><span data-stu-id="e91af-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="e91af-166">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="e91af-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

