---
title: Balanceador de carga aaaCreate um com a Internet com o IPv6 - CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um Internet oposto balanceador de carga com o IPv6 no Gerenciador de recursos do Azure usando Olá CLI do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="341d5-104">Criar uma balanceador de carga com o IPv6 no Azure Resource Manager usando Olá CLI do Azure da Internet</span><span class="sxs-lookup"><span data-stu-id="341d5-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="341d5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="341d5-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="341d5-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="341d5-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="341d5-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="341d5-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="341d5-108">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="341d5-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="341d5-109">o balanceador de carga Olá fornece alta disponibilidade através da distribuição de tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="341d5-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="341d5-110">O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.</span><span class="sxs-lookup"><span data-stu-id="341d5-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="341d5-111">Exemplo de cenário de implantação</span><span class="sxs-lookup"><span data-stu-id="341d5-111">Example deployment scenario</span></span>

<span data-ttu-id="341d5-112">Olá, diagrama a seguir ilustra Olá solução balanceamento de carga que está sendo implantado usando o modelo de exemplo hello descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="341d5-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="341d5-114">Nesse cenário, você criará hello Azure recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="341d5-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="341d5-115">duas VMs (máquinas virtuais)</span><span class="sxs-lookup"><span data-stu-id="341d5-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="341d5-116">uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos</span><span class="sxs-lookup"><span data-stu-id="341d5-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="341d5-117">um balanceador de carga voltado para a Internet com um IPv4 e um endereço IP público IPv6</span><span class="sxs-lookup"><span data-stu-id="341d5-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="341d5-118">um conjunto de disponibilidade toothat contém Olá duas VMs</span><span class="sxs-lookup"><span data-stu-id="341d5-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="341d5-119">dois carregar balanceamento regras toomap Olá VIPs toohello privados pontos de extremidade públicos</span><span class="sxs-lookup"><span data-stu-id="341d5-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="341d5-120">Implantar solução hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="341d5-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="341d5-121">Olá etapas a seguir mostra como toocreate um voltados à Internet carregar balanceador usando o Gerenciador de recursos do Azure com CLI.</span><span class="sxs-lookup"><span data-stu-id="341d5-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="341d5-122">No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente e juntar toocreate um recurso.</span><span class="sxs-lookup"><span data-stu-id="341d5-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="341d5-123">toodeploy um balanceador de carga, que você crie e configure Olá seguintes objetos:</span><span class="sxs-lookup"><span data-stu-id="341d5-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="341d5-124">Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="341d5-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="341d5-125">Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="341d5-126">Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="341d5-127">Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="341d5-128">Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="341d5-129">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="341d5-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="341d5-130">Configurar seu ambiente de CLI toouse Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="341d5-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="341d5-131">Neste exemplo, estamos executando ferramentas CLI de saudação em uma janela de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="341d5-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="341d5-132">Não estamos usando cmdlets do PowerShell do Azure Olá mas usamos a legibilidade de tooimprove de recursos e reutilização de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="341d5-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="341d5-133">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="341d5-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="341d5-134">Executar Olá **modo de configuração do azure** modo do comando tooswitch tooResource Gerenciador.</span><span class="sxs-lookup"><span data-stu-id="341d5-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="341d5-135">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="341d5-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="341d5-136">Entre no tooAzure e obter uma lista de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="341d5-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="341d5-137">Inserir as credenciais do Azure quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="341d5-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="341d5-138">Escolha a assinatura Olá que deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="341d5-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="341d5-139">Anote a Id de assinatura de saudação para a próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="341d5-140">Configure variáveis do PowerShell para uso com os comandos CLI hello.</span><span class="sxs-lookup"><span data-stu-id="341d5-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="341d5-141">Crie um grupo de recursos, um balanceador de carga, uma rede virtual e sub-redes</span><span class="sxs-lookup"><span data-stu-id="341d5-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="341d5-142">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="341d5-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="341d5-143">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="341d5-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="341d5-144">Criar uma rede virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="341d5-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="341d5-145">Criar duas sub-redes nessa VNet.</span><span class="sxs-lookup"><span data-stu-id="341d5-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="341d5-146">Crie endereços IP públicos para o pool de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="341d5-147">Definir variáveis do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="341d5-148">Crie um público Olá front-end IP pool de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="341d5-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="341d5-149">Balanceador de carga Olá usa o rótulo de domínio de saudação do IP público Olá como seu FQDN.</span><span class="sxs-lookup"><span data-stu-id="341d5-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="341d5-150">Esta uma alteração de implantação clássica, que usa o nome do serviço de nuvem Olá Olá FQDN do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="341d5-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="341d5-151">Neste exemplo, hello FQDN é *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="341d5-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="341d5-152">Criar pools de front-end e back-end</span><span class="sxs-lookup"><span data-stu-id="341d5-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="341d5-153">Este exemplo cria um pool IP de front-end Olá que recebe o tráfego de rede entrada hello no balanceador de carga hello e pool IP de back-end Olá onde o pool de front-end Olá envia tráfego de rede com balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="341d5-154">Definir variáveis do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="341d5-155">Crie um pool IP de front-end associando Olá IP público criado na etapa anterior hello e balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="341d5-156">Criar regras de balanceamento de carga, regras NAT e investigação Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="341d5-157">Este exemplo cria Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="341d5-157">This example creates hello following items:</span></span>

* <span data-ttu-id="341d5-158">um toocheck de regra de teste para a porta 80 do tooTCP de conectividade</span><span class="sxs-lookup"><span data-stu-id="341d5-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="341d5-159">um NAT regra tootranslate todo o tráfego de entrada na porta 3389 tooport 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="341d5-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="341d5-160">um NAT regra tootranslate todo o tráfego de entrada na porta 3391 tooport 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="341d5-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="341d5-161">um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="341d5-162"><sup>1</sup> regras NAT são tooa associado instância de máquina virtual por trás do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="341d5-163">tráfego de rede de saudação que chegam na porta 3389 é enviado toohello específico de máquina virtual e a porta associada à regra NAT hello.</span><span class="sxs-lookup"><span data-stu-id="341d5-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="341d5-164">Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT.</span><span class="sxs-lookup"><span data-stu-id="341d5-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="341d5-165">Os dois protocolos não podem ser atribuído toohello a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="341d5-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="341d5-166">Definir variáveis do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="341d5-167">Criar a investigação de saudação</span><span class="sxs-lookup"><span data-stu-id="341d5-167">Create hello probe</span></span>

    <span data-ttu-id="341d5-168">Olá exemplo a seguir cria uma investigação TCP verifica para conectividade tooback-end a porta TCP 80 a cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="341d5-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="341d5-169">Ele marcará recursos de back-end Olá indisponível após duas falhas consecutivas.</span><span class="sxs-lookup"><span data-stu-id="341d5-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="341d5-170">Criar regras de NAT de entrada que permitem conexões RDP toohello recursos de back-end</span><span class="sxs-lookup"><span data-stu-id="341d5-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="341d5-171">Criar regras que enviam tráfego de portas de back-end toodifferent dependendo de qual solicitação de saudação do front-end recebida de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="341d5-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="341d5-172">Verifique suas configurações</span><span class="sxs-lookup"><span data-stu-id="341d5-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="341d5-173">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="341d5-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="341d5-174">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="341d5-174">Create NICs</span></span>

<span data-ttu-id="341d5-175">Criar NICs e associá-los tooNAT regras, regras de Balanceador de carga e testes.</span><span class="sxs-lookup"><span data-stu-id="341d5-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="341d5-176">Definir variáveis do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="341d5-177">Crie um NIC para cada back-end e adicione uma configuração de IPv6.</span><span class="sxs-lookup"><span data-stu-id="341d5-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="341d5-178">Criar recursos de back-end de saudação VM e conecte cada NIC</span><span class="sxs-lookup"><span data-stu-id="341d5-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="341d5-179">toocreate VMs, você deve ter uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="341d5-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="341d5-180">Balanceamento de carga, Olá VMs necessário toobe membros de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="341d5-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="341d5-181">Para saber mais sobre a criação de VMs, consulte [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="341d5-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="341d5-182">Definir variáveis do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="341d5-183">Este exemplo usa Olá username e password para VMs Olá em texto não criptografado.</span><span class="sxs-lookup"><span data-stu-id="341d5-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="341d5-184">Apropriado deve ter cuidado ao usando as credenciais em Olá claro.</span><span class="sxs-lookup"><span data-stu-id="341d5-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="341d5-185">Para um método mais seguro de tratamento de credenciais no PowerShell, consulte Olá [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="341d5-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="341d5-186">Criar conjunto de disponibilidade e a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="341d5-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="341d5-187">Quando você cria Olá VMs, você pode usar uma conta de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="341d5-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="341d5-188">saudação de comando a seguir cria uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="341d5-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="341d5-189">Em seguida, crie o conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="341d5-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="341d5-190">Criar máquinas virtuais de saudação com NICs Olá associado</span><span class="sxs-lookup"><span data-stu-id="341d5-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="341d5-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="341d5-191">Next steps</span></span>

[<span data-ttu-id="341d5-192">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="341d5-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="341d5-193">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="341d5-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="341d5-194">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="341d5-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
