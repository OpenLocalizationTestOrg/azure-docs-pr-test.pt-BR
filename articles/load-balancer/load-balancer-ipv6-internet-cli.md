---
title: Criar um balanceador de carga voltado para a Internet com o IPv6 - CLI do Azure | Microsoft Docs
description: Saiba como criar um balanceador de carga voltado para a Internet com IPv6 no Azure Resource Manager usando a CLI do Azure
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="f5da4-104">Criar um balanceador de carga voltado para a Internet com IPv6 no Azure Resource Manager usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f5da4-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5da4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5da4-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="f5da4-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f5da4-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="f5da4-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="f5da4-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="f5da4-108">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="f5da4-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="f5da4-109">O balanceador de carga fornece alta disponibilidade, distribuindo o tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="f5da4-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="f5da4-110">O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.</span><span class="sxs-lookup"><span data-stu-id="f5da4-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="f5da4-111">Exemplo de cenário de implantação</span><span class="sxs-lookup"><span data-stu-id="f5da4-111">Example deployment scenario</span></span>

<span data-ttu-id="f5da4-112">O diagrama a seguir ilustra a solução de balanceamento de carga que está sendo implantada usando o exemplo de modelo descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f5da4-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="f5da4-114">Nesse cenário, você criará os seguintes recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="f5da4-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="f5da4-115">duas VMs (máquinas virtuais)</span><span class="sxs-lookup"><span data-stu-id="f5da4-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="f5da4-116">uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos</span><span class="sxs-lookup"><span data-stu-id="f5da4-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="f5da4-117">um balanceador de carga voltado para a Internet com um IPv4 e um endereço IP público IPv6</span><span class="sxs-lookup"><span data-stu-id="f5da4-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="f5da4-118">um Conjunto de disponibilidade que contém as duas VMs</span><span class="sxs-lookup"><span data-stu-id="f5da4-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="f5da4-119">duas regras de balanceamento de carga para mapear os VIPs públicos para os pontos de extremidade privados</span><span class="sxs-lookup"><span data-stu-id="f5da4-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="f5da4-120">Implantar a solução usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f5da4-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="f5da4-121">As etapas a seguir mostram como criar um balanceador de carga para a Internet usando o Azure Resource Manager com a CLI.</span><span class="sxs-lookup"><span data-stu-id="f5da4-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="f5da4-122">Com o Azure Resource Manager, todos os recursos são criados e configurados individualmente e colocados juntos para criar um recurso.</span><span class="sxs-lookup"><span data-stu-id="f5da4-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="f5da4-123">Para implantar um balanceador de carga, crie e configure os seguintes objetos:</span><span class="sxs-lookup"><span data-stu-id="f5da4-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="f5da4-124">Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="f5da4-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="f5da4-125">Pool de endereços de back-end – contém NICs (interfaces de rede) para que as máquinas virtuais recebam o tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f5da4-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="f5da4-126">Regras de balanceamento de carga – contém regras de mapeamento de uma porta pública no balanceador de carga para uma porta no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="f5da4-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="f5da4-127">Regras NAT de entrada – contém regras de mapeamento de uma porta pública no balanceador de carga para uma porta de uma máquina virtual específica no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="f5da4-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="f5da4-128">Investigações – contém investigações de integridade usadas para verificar a disponibilidade de instâncias de máquinas virtuais no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="f5da4-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="f5da4-129">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f5da4-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="f5da4-130">Configurar seu ambiente da CLI para usar o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5da4-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="f5da4-131">Neste exemplo, executamos as ferramentas da CLI em uma janela de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5da4-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="f5da4-132">Não estamos usando os cmdlets do Azure PowerShell, mas podemos usar recursos de script do PowerShell para melhorar a legibilidade e a reutilização.</span><span class="sxs-lookup"><span data-stu-id="f5da4-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="f5da4-133">Se você nunca usou a CLI do Azure, veja [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5da4-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f5da4-134">Execute o comando **azure config mode** para alternar para o modo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5da4-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f5da4-135">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f5da4-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f5da4-136">Entrar no Azure e obter uma lista de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f5da4-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="f5da4-137">Inserir as credenciais do Azure quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="f5da4-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="f5da4-138">Localize a assinatura que você quer usar.</span><span class="sxs-lookup"><span data-stu-id="f5da4-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="f5da4-139">Anote a Id da assinatura para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="f5da4-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="f5da4-140">Configure variáveis do PowerShell para uso com os comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="f5da4-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="f5da4-141">Crie um grupo de recursos, um balanceador de carga, uma rede virtual e sub-redes</span><span class="sxs-lookup"><span data-stu-id="f5da4-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="f5da4-142">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="f5da4-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="f5da4-143">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f5da4-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="f5da4-144">Criar uma rede virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="f5da4-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="f5da4-145">Criar duas sub-redes nessa VNet.</span><span class="sxs-lookup"><span data-stu-id="f5da4-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="f5da4-146">Criar endereços IP públicos para o pool de front-end</span><span class="sxs-lookup"><span data-stu-id="f5da4-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="f5da4-147">Configurar as variáveis do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5da4-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="f5da4-148">Crie endereços IP públicos para o pool de front-end.</span><span class="sxs-lookup"><span data-stu-id="f5da4-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f5da4-149">O balanceador de carga usa o rótulo de domínio do IP público como FQDN.</span><span class="sxs-lookup"><span data-stu-id="f5da4-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="f5da4-150">Isso é uma mudança da implantação clássica, que usa o nome do serviço de nuvem como o FQDN do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f5da4-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="f5da4-151">Neste exemplo, o FQDN é *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f5da4-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="f5da4-152">Criar pools de front-end e back-end</span><span class="sxs-lookup"><span data-stu-id="f5da4-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="f5da4-153">Este exemplo cria o pool de IPs de front-end, que recebe o tráfego de rede de entrada no balanceador de carga, e o pool de IPs de back-end, no qual o pool de front-end envia o tráfego de rede com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="f5da4-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="f5da4-154">Configurar as variáveis do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5da4-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="f5da4-155">Crie um pool de IPs de front-end associando o IP público criado na etapa anterior e o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f5da4-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="f5da4-156">Criar a investigação, regras de NAT e regras de LB</span><span class="sxs-lookup"><span data-stu-id="f5da4-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="f5da4-157">Este exemplo cria os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f5da4-157">This example creates the following items:</span></span>

* <span data-ttu-id="f5da4-158">uma regra de investigação para verificar se há conectividade com a porta TCP 80</span><span class="sxs-lookup"><span data-stu-id="f5da4-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="f5da4-159">uma regra NAT para converter todo o tráfego de entrada na porta 3389 para a porta 3389<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f5da4-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="f5da4-160">uma regra NAT para converter todo o tráfego de entrada na porta 3391 para a porta 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f5da4-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="f5da4-161">uma regra do balanceador de carga para equilibrar todo o tráfego de entrada na porta 80 para a porta 80 nos endereços no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="f5da4-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="f5da4-162"><sup>1</sup> As regras NAT são associadas a uma instância de máquina virtual específica por trás do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f5da4-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="f5da4-163">O tráfego de rede que chega à porta 3389 é enviado a uma máquina virtual específica e à porta 22 associada a essa regra NAT.</span><span class="sxs-lookup"><span data-stu-id="f5da4-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="f5da4-164">Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT.</span><span class="sxs-lookup"><span data-stu-id="f5da4-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="f5da4-165">Ambos os protocolos não podem ser atribuídos à mesma porta.</span><span class="sxs-lookup"><span data-stu-id="f5da4-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="f5da4-166">Configurar as variáveis do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5da4-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="f5da4-167">Criar a investigação</span><span class="sxs-lookup"><span data-stu-id="f5da4-167">Create the probe</span></span>

    <span data-ttu-id="f5da4-168">O exemplo a seguir cria uma investigação TCP que verifica a conectividade com a porta TCP 80 back-end a cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="f5da4-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="f5da4-169">Ele marcará os recursos de back-end como não disponíveis após duas falhas consecutivas.</span><span class="sxs-lookup"><span data-stu-id="f5da4-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="f5da4-170">Criar regras NAT de entrada que permitam conexões RDP com os recursos de back-end</span><span class="sxs-lookup"><span data-stu-id="f5da4-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="f5da4-171">Criar regras de balanceador de carga que enviam tráfego para portas de back-end diferentes, dependendo de qual front-end recebeu a solicitação</span><span class="sxs-lookup"><span data-stu-id="f5da4-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="f5da4-172">Verifique suas configurações</span><span class="sxs-lookup"><span data-stu-id="f5da4-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="f5da4-173">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f5da4-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="f5da4-174">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="f5da4-174">Create NICs</span></span>

<span data-ttu-id="f5da4-175">Crie NICs e associe-os às regras NAT, regras do balanceador de carga e investigações.</span><span class="sxs-lookup"><span data-stu-id="f5da4-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="f5da4-176">Configurar as variáveis do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5da4-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="f5da4-177">Crie um NIC para cada back-end e adicione uma configuração de IPv6.</span><span class="sxs-lookup"><span data-stu-id="f5da4-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="f5da4-178">Crie os recursos de VM de back-end e anexe cada NIC</span><span class="sxs-lookup"><span data-stu-id="f5da4-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="f5da4-179">Para criar VMs, você deve ter uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f5da4-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="f5da4-180">Para o balanceamento de carga, as VMs precisam ser membros de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="f5da4-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="f5da4-181">Para saber mais sobre a criação de VMs, consulte [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f5da4-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="f5da4-182">Configurar as variáveis do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5da4-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="f5da4-183">Este exemplo usa o nome de usuário e a senha para as VMs em texto não sem formatação.</span><span class="sxs-lookup"><span data-stu-id="f5da4-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="f5da4-184">Tome o cuidado apropriado ao usar credenciais de modo transparente.</span><span class="sxs-lookup"><span data-stu-id="f5da4-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="f5da4-185">Para um método mais seguro de tratamento de credenciais no PowerShell, consulte o cmdlet [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f5da4-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="f5da4-186">Criar o conjunto de disponibilidade e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f5da4-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="f5da4-187">Você pode usar uma conta de armazenamento existente ao cria as VMs.</span><span class="sxs-lookup"><span data-stu-id="f5da4-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="f5da4-188">O comando a seguir cria uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f5da4-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="f5da4-189">Em seguida, crie o conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="f5da4-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="f5da4-190">Criar as máquinas virtuais com NICs associados</span><span class="sxs-lookup"><span data-stu-id="f5da4-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="f5da4-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5da4-191">Next steps</span></span>

[<span data-ttu-id="f5da4-192">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="f5da4-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="f5da4-193">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f5da4-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f5da4-194">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f5da4-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
