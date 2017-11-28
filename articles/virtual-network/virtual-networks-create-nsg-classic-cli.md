---
title: "Olá aaaHow toocreate NSGs no modo clássico, usando a CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate e implantar os NSGs em modo clássico usando Olá CLI do Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="b7f3d-103">Como toocreate NSGs (clássicos) na Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b7f3d-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b7f3d-104">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="b7f3d-105">Você também pode [criar NSGs no modelo de implantação do Gerenciador de recursos de saudação](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b7f3d-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="b7f3d-106">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="b7f3d-107">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá por [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b7f3d-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="b7f3d-108">Como toocreate Olá NSG para Olá sub-rede front-end</span><span class="sxs-lookup"><span data-stu-id="b7f3d-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="b7f3d-109">toocreate um NSG chamado denominado **NSG-front-end** com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b7f3d-110">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b7f3d-111">Executar Olá  **`azure config mode`**  tooswitch tooclassic modo de comando, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="b7f3d-112">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="b7f3d-113">Executar Olá  **`azure network nsg create`**  comando toocreate um NSG.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="b7f3d-114">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="b7f3d-115">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-115">Parameters:</span></span>
   
   * <span data-ttu-id="b7f3d-116">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-116">**-l (or --location)**.</span></span> <span data-ttu-id="b7f3d-117">Região do Azure onde hello novo NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="b7f3d-118">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="b7f3d-119">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-119">**-n (or --name)**.</span></span> <span data-ttu-id="b7f3d-120">Nome para Olá novo NSG.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-120">Name for hello new NSG.</span></span> <span data-ttu-id="b7f3d-121">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="b7f3d-122">Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que permita acesso tooport 3389 (RDP) de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="b7f3d-123">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="b7f3d-124">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-124">Parameters:</span></span>
   
   * <span data-ttu-id="b7f3d-125">**-a (or --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="b7f3d-126">Nome do NSG Olá quais Olá regra será criada.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="b7f3d-127">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="b7f3d-128">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-128">**-n (or --name)**.</span></span> <span data-ttu-id="b7f3d-129">Nome para a nova regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-129">Name for hello new rule.</span></span> <span data-ttu-id="b7f3d-130">Para o nosso cenário, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="b7f3d-131">**-c (or --action)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-131">**-c (or --action)**.</span></span> <span data-ttu-id="b7f3d-132">Nível de acesso para a regra de saudação (Deny ou permitir).</span><span class="sxs-lookup"><span data-stu-id="b7f3d-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="b7f3d-133">**-p (or --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="b7f3d-134">Protocolo (Tcp, Udp ou *) para a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="b7f3d-135">**-r (or --type)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-135">**-r (or --type)**.</span></span> <span data-ttu-id="b7f3d-136">Direção da conexão (Entrada ou Saída).</span><span class="sxs-lookup"><span data-stu-id="b7f3d-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="b7f3d-137">**-y (or --priority)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-137">**-y (or --priority)**.</span></span> <span data-ttu-id="b7f3d-138">Prioridade de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="b7f3d-139">**-f (or --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="b7f3d-140">Prefixo do endereço de origem no CIDR ou uso de marcas padrão.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="b7f3d-141">**-o (or --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="b7f3d-142">Porta de origem ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-142">Source port, or port range.</span></span>
   * <span data-ttu-id="b7f3d-143">**-e (or --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="b7f3d-144">Prefixo do endereço de destino no CIDR ou uso de marcas padrão.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="b7f3d-145">**-u (or --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="b7f3d-146">Porta de destino ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="b7f3d-147">Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que permita acesso tooport 80 (HTTP) de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="b7f3d-148">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="b7f3d-149">Executar Olá  **`azure network nsg subnet add`**  comando toolink Olá NSG toohello front-end subrede.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="b7f3d-150">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="b7f3d-151">Como toocreate Olá NSG para Olá volta terminar subrede</span><span class="sxs-lookup"><span data-stu-id="b7f3d-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="b7f3d-152">toocreate um NSG chamado denominado *back-end NSG* com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b7f3d-153">Executar Olá  **`azure network nsg create`**  comando toocreate um NSG.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="b7f3d-154">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="b7f3d-155">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-155">Parameters:</span></span>
   
   * <span data-ttu-id="b7f3d-156">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-156">**-l (or --location)**.</span></span> <span data-ttu-id="b7f3d-157">Região do Azure onde hello novo NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="b7f3d-158">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="b7f3d-159">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-159">**-n (or --name)**.</span></span> <span data-ttu-id="b7f3d-160">Nome para Olá novo NSG.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-160">Name for hello new NSG.</span></span> <span data-ttu-id="b7f3d-161">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="b7f3d-162">Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que permita acesso tooport 1433 (SQL) da sub-rede de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="b7f3d-163">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="b7f3d-164">Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que nega acesso toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="b7f3d-165">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="b7f3d-166">Executar Olá  **`azure network nsg subnet add`**  toolink Olá NSG toohello volta end subrede de comando.</span><span class="sxs-lookup"><span data-stu-id="b7f3d-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="b7f3d-167">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b7f3d-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

