---
title: Criar um balanceador de carga voltado para a Internet - CLI do Azure | Microsoft Docs
description: Saiba como criar um balanceador de carga voltado para a Internet no Gerenciador de Recursos usando a CLI do Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3b1780033cbc8aa3e108a213a4d2bfd0332fd7d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-load-balancer-using-the-azure-cli"></a><span data-ttu-id="b4305-103">Criar um balanceador de carga interno usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b4305-103">Creating an internet load balancer using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4305-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b4305-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="b4305-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4305-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="b4305-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b4305-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="b4305-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="b4305-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b4305-108">Este artigo aborda o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="b4305-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="b4305-109">Também é possível [Saber como criar um balanceador de carga para a Internet usando a implantação clássica](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b4305-109">You can also [Learn how to create an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="b4305-110">Implantar a solução usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b4305-110">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="b4305-111">As etapas a seguir mostram como criar um balanceador de carga para a Internet usando o Azure Resource Manager com a CLI.</span><span class="sxs-lookup"><span data-stu-id="b4305-111">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="b4305-112">Com o Azure Resource Manager, todos os recursos são criados e configurados individualmente e, em seguida, colocados juntos para criar um recurso.</span><span class="sxs-lookup"><span data-stu-id="b4305-112">With Azure Resource Manager each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="b4305-113">Você deve criar e configurar os seguintes objetos para implantar um balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="b4305-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="b4305-114">Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="b4305-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="b4305-115">Pool de endereços de back-end – contém NICs (interfaces de rede) para que as máquinas virtuais recebam o tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-115">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="b4305-116">Regras de balanceamento de carga – contém regras de mapeamento de uma porta pública no balanceador de carga para uma porta no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="b4305-116">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="b4305-117">Regras NAT de entrada – contém regras de mapeamento de uma porta pública no balanceador de carga para uma porta de uma máquina virtual específica no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="b4305-117">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="b4305-118">Investigações – contém investigações de integridade usadas para verificar a disponibilidade de instâncias de máquinas virtuais no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="b4305-118">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="b4305-119">Para obter mais informações, confira [Suporte do Azure Resource Manager para balanceador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b4305-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="b4305-120">Configurar a CLI para usar o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="b4305-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="b4305-121">Se você nunca usou a CLI do Azure, consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4305-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b4305-122">Execute o comando **azure config mode** para alternar para o modo do Gerenciador de Recursos, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4305-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="b4305-123">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4305-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="b4305-124">Criar uma rede virtual e um endereço IP público para o pool de IPs de front-end</span><span class="sxs-lookup"><span data-stu-id="b4305-124">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="b4305-125">Crie uma rede virtual (VNet) denominada *NRPVnet* no local Leste dos EUA usando um grupo de recursos denominado *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="b4305-125">Create a virtual network (VNet) named *NRPVnet* in the East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="b4305-126">Crie uma sub-rede denominada *NRPVnetSubnet* com um bloco CIDR de 10.0.0.0/24 na *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="b4305-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="b4305-127">Crie um endereço IP público denominado *NRPPublicIP* para ser usado por um pool de IPs front-end com nome DNS *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="b4305-127">Create a public IP address named *NRPPublicIP* to be used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span> <span data-ttu-id="b4305-128">O comando a seguir usa o tipo de alocação estática e o tempo limite de ociosidade de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="b4305-128">The command below uses the static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="b4305-129">O balanceador de carga usará o rótulo de domínio do IP público como FQDN.</span><span class="sxs-lookup"><span data-stu-id="b4305-129">The load balancer will use the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="b4305-130">Isso é uma mudança da implantação clássica, que usa o serviço de nuvem como o FQDN (nome de domínio totalmente qualificado) do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-130">This a change from classic deployment, which uses the cloud service as the load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="b4305-131">Neste exemplo, o FQDN é *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="b4305-131">In this example, the FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="b4305-132">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b4305-132">Create a load balancer</span></span>

<span data-ttu-id="b4305-133">O comando a seguir cria um balanceador de carga chamado *NRPlb* no grupo de recursos *NRPRG*, na localização do Azure *Leste dos EUA*.</span><span class="sxs-lookup"><span data-stu-id="b4305-133">The following command creates a load balancer named *NRPlb* in the *NRPRG* resource group in the *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="b4305-134">Criar um pool de IPs de front-end e um pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="b4305-134">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="b4305-135">Este exemplo demonstra como criar o pool de IPs de front-end, que recebe o tráfego de rede de entrada no balanceador de carga, e o pool de IPs de back-end, no qual o pool de front-end envia o tráfego de rede com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-135">This example demonstrates how to create the front-end IP pool that receives the incoming network traffic on the load balancer and the backend IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="b4305-136">Crie um pool de IPs de front-end associando o IP público criado na etapa anterior e o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-136">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="b4305-137">Configure um pool de endereços de back-end usado para receber o tráfego de entrada do pool de IPs de front-end.</span><span class="sxs-lookup"><span data-stu-id="b4305-137">Set up a back-end address pool used to receive incoming traffic from the front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="b4305-138">Criar regras de balanceamento de carga, regras NAT e investigação</span><span class="sxs-lookup"><span data-stu-id="b4305-138">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="b4305-139">Este exemplo cria os seguintes itens.</span><span class="sxs-lookup"><span data-stu-id="b4305-139">This example creates the following items.</span></span>

* <span data-ttu-id="b4305-140">uma regra NAT para converter todo o tráfego de entrada na porta 21 para a porta 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b4305-140">a NAT rule to translate all incoming traffic on port 21 to port 22<sup>1</sup></span></span>
* <span data-ttu-id="b4305-141">uma regra NAT para converter todo o tráfego de entrada na porta 23 para a porta 22</span><span class="sxs-lookup"><span data-stu-id="b4305-141">a NAT rule to translate all incoming traffic on port 23 to port 22</span></span>
* <span data-ttu-id="b4305-142">uma regra do balanceador de carga para equilibrar todo o tráfego de entrada na porta 80 para a porta 80 nos endereços no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="b4305-142">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="b4305-143">uma regra de investigação para verificar o status de integridade em uma página chamada *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="b4305-143">a probe rule to check the health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="b4305-144"><sup>1</sup> As regras NAT são associadas a uma instância de máquina virtual específica por trás do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-144"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="b4305-145">O tráfego de rede que chega à porta 21 é enviado a uma máquina virtual específica na porta 22 associada a esta regra NAT.</span><span class="sxs-lookup"><span data-stu-id="b4305-145">The network traffic arriving on port 21 is sent to a specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="b4305-146">Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT.</span><span class="sxs-lookup"><span data-stu-id="b4305-146">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="b4305-147">Ambos os protocolos não podem ser atribuídos à mesma porta.</span><span class="sxs-lookup"><span data-stu-id="b4305-147">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="b4305-148">Criar regras NAT.</span><span class="sxs-lookup"><span data-stu-id="b4305-148">Create the NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="b4305-149">Crie uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-149">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="b4305-150">Crie um teste de integridade.</span><span class="sxs-lookup"><span data-stu-id="b4305-150">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="b4305-151">Verifique suas configurações.</span><span class="sxs-lookup"><span data-stu-id="b4305-151">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="b4305-152">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4305-152">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up the load balancer "nrplb"
        + Looking up the public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="b4305-153">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="b4305-153">Create NICs</span></span>

<span data-ttu-id="b4305-154">Você precisa criar NICs (ou modificar as existentes) e associá-las a regras NAT, regras do balanceador de carga e testes.</span><span class="sxs-lookup"><span data-stu-id="b4305-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="b4305-155">Crie uma NIC chamada *lb-nic1-be* e a associe à regra NAT *rdp1* e ao pool de endereços de back-end *NRPbackendpool*.</span><span class="sxs-lookup"><span data-stu-id="b4305-155">Create a NIC named *lb-nic1-be*, and associate it with the *rdp1* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="b4305-156">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4305-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="b4305-157">Crie uma NIC chamada *lb-nic2-be* e a associe à regra NAT *rdp2* e ao pool de endereços de back-end *NRPbackendpool*.</span><span class="sxs-lookup"><span data-stu-id="b4305-157">Create a NIC named *lb-nic2-be*, and associate it with the *rdp2* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="b4305-158">Crie uma VM (máquina virtual) chamada *web1* e a associe ao NIC chamado *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="b4305-158">Create a virtual machine (VM) named *web1*, and associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="b4305-159">Uma conta de armazenamento denominada *web1nrp* foi criada antes da execução do comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4305-159">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b4305-160">As VMs em um balanceador de carga precisam estar no mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b4305-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="b4305-161">Use `azure availset create` para criar um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b4305-161">Use `azure availset create` to create an availability set.</span></span>

    <span data-ttu-id="b4305-162">A saída deverá ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="b4305-162">The output should be similar to the following:</span></span>

        info:    Executing command vm create
        + Looking up the VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using the VM Size "Standard_A1"
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account web1nrp
        + Looking up the availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up the NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in the NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="b4305-163">A mensagem informativa **Esta é uma NIC sem IP público configurado** é esperada, pois a NIC criada para o balanceador de carga se conecta à Internet usando o endereço IP público do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-163">The informational message **This is a NIC without publicIP configured** is expected since the NIC created for the load balancer connecting to Internet using the load balancer public IP address.</span></span>

    <span data-ttu-id="b4305-164">Como a NIC *lb-nic1-be* está associada à regra NAT *rdp1*, você pode se conectar ao *web1* usando o RDP por meio da porta 3441 no balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b4305-164">Since the *lb-nic1-be* NIC is associated with the *rdp1* NAT rule, you can connect to *web1* using RDP through port 3441 on the load balancer.</span></span>

4. <span data-ttu-id="b4305-165">Crie uma VM (máquina virtual) denominada *web2* e a associe à NIC denominada *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="b4305-165">Create a virtual machine (VM) named *web2*, and associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="b4305-166">Uma conta de armazenamento denominada *web1nrp* foi criada antes da execução do comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4305-166">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="b4305-167">Atualizar um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="b4305-167">Update an existing load balancer</span></span>
<span data-ttu-id="b4305-168">Você pode adicionar regras ao fazer referência a um balanceador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="b4305-168">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="b4305-169">No exemplo a seguir, uma nova regra de balanceador de carga é adicionada a um balanceador de carga **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="b4305-169">In the next example, a new load balancer rule is added to an existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="b4305-170">Excluir um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b4305-170">Delete a load balancer</span></span>
<span data-ttu-id="b4305-171">Para remover um balanceador de carga, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4305-171">Use the following command to remove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="b4305-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4305-172">Next steps</span></span>
[<span data-ttu-id="b4305-173">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="b4305-173">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="b4305-174">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b4305-174">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b4305-175">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b4305-175">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
