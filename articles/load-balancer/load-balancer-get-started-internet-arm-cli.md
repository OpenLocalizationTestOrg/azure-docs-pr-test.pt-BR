---
title: aaaCreate um voltados para Internet carregar balanceador - CLI do Azure | Microsoft Docs
description: "Saiba como um balanceador de carga voltado para Internet usando o Gerenciador de recursos de toocreate Olá CLI do Azure"
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
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="862b5-103">Criando um balanceador de carga de internet usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="862b5-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="862b5-104">Portal</span><span class="sxs-lookup"><span data-stu-id="862b5-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="862b5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="862b5-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="862b5-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="862b5-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="862b5-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="862b5-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="862b5-108">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="862b5-109">Você também pode [Saiba como toocreate um voltados à Internet carregar balanceador de implantação clássico](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="862b5-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="862b5-110">Implantar solução hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="862b5-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="862b5-111">Olá etapas a seguir mostra como toocreate um voltados à Internet carregar balanceador usando o Gerenciador de recursos do Azure com CLI.</span><span class="sxs-lookup"><span data-stu-id="862b5-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="862b5-112">Com o Azure Resource Manager cada recurso é criado e configurado individualmente, em seguida, juntar toocreate um recurso.</span><span class="sxs-lookup"><span data-stu-id="862b5-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="862b5-113">Você deve criar e configurar Olá objetos toodeploy um balanceador de carga a seguir:</span><span class="sxs-lookup"><span data-stu-id="862b5-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="862b5-114">Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="862b5-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="862b5-115">Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="862b5-116">Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="862b5-117">Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="862b5-118">Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="862b5-119">Para obter mais informações, confira [Suporte do Azure Resource Manager para balanceador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="862b5-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="862b5-120">Configurar CLI toouse Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="862b5-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="862b5-121">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="862b5-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="862b5-122">Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="862b5-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="862b5-123">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="862b5-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="862b5-124">Criar uma rede virtual e um endereço IP público para o pool de IP de front-end de saudação</span><span class="sxs-lookup"><span data-stu-id="862b5-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="862b5-125">Criar uma rede virtual (VNet) denominada *NRPVnet* no local do Leste dos EUA hello usando um grupo de recursos denominado *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="862b5-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="862b5-126">Crie uma sub-rede denominada *NRPVnetSubnet* com um bloco CIDR de 10.0.0.0/24 na *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="862b5-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="862b5-127">Criar um endereço IP público denominado *NRPPublicIP* toobe usado por um pool IP de front-end com o nome DNS *loadbalancernrp.eastus.cloudapp.azure.com*. comando de saudação abaixo usa o tipo de alocação estática hello e tempo limite de ociosidade de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="862b5-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="862b5-128">Balanceador de carga Olá usará o rótulo de domínio de saudação do IP público hello como seu FQDN.</span><span class="sxs-lookup"><span data-stu-id="862b5-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="862b5-129">Esta uma alteração de implantação clássica, que usa o serviço de nuvem Olá Olá totalmente o nome de domínio qualificado (FQDN) do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="862b5-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="862b5-130">Neste exemplo, hello FQDN é *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="862b5-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="862b5-131">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="862b5-131">Create a load balancer</span></span>

<span data-ttu-id="862b5-132">Olá, comando a seguir cria um balanceador de carga denominado *NRPlb* em Olá *NRPRG* grupo de recursos em Olá *Leste dos EUA* local do Azure.</span><span class="sxs-lookup"><span data-stu-id="862b5-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="862b5-133">Criar um pool de IPs de front-end e um pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="862b5-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="862b5-134">Este exemplo demonstra como toocreate Olá pool IP front-end que recebe o tráfego de rede entrada hello em hello balanceador de carga e Olá pool IP de back-end em que o pool de front-end Olá envia Olá tráfego de rede de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="862b5-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="862b5-135">Crie um pool IP de front-end associando Olá IP público criado na etapa anterior hello e balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="862b5-136">Configurar um pool de endereços de back-end usado tooreceive o tráfego de entrada hello front-end do pool de IP.</span><span class="sxs-lookup"><span data-stu-id="862b5-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="862b5-137">Criar regras de balanceamento de carga, regras NAT e investigação</span><span class="sxs-lookup"><span data-stu-id="862b5-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="862b5-138">Este exemplo cria Olá itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="862b5-138">This example creates hello following items.</span></span>

* <span data-ttu-id="862b5-139">regra de NAT tootranslate todo o tráfego de entrada na porta 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="862b5-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="862b5-140">regra de NAT tootranslate todo o tráfego de entrada na porta 23 tooport 22</span><span class="sxs-lookup"><span data-stu-id="862b5-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="862b5-141">um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="862b5-142">um status de integridade de saudação do teste regra toocheck em uma página chamada *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="862b5-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="862b5-143"><sup>1</sup> regras NAT são tooa associado instância de máquina virtual por trás do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="862b5-144">tráfego de rede de saudação que chegam a porta 21 é enviado tooa específico de máquina virtual na porta 22 associado a esta regra NAT.</span><span class="sxs-lookup"><span data-stu-id="862b5-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="862b5-145">Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT.</span><span class="sxs-lookup"><span data-stu-id="862b5-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="862b5-146">Os dois protocolos não podem ser atribuído toohello a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="862b5-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="862b5-147">Crie regras NAT de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="862b5-148">Crie uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="862b5-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="862b5-149">Crie um teste de integridade.</span><span class="sxs-lookup"><span data-stu-id="862b5-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="862b5-150">Verifique suas configurações.</span><span class="sxs-lookup"><span data-stu-id="862b5-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="862b5-151">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="862b5-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
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

## <a name="create-nics"></a><span data-ttu-id="862b5-152">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="862b5-152">Create NICs</span></span>

<span data-ttu-id="862b5-153">Você precisa toocreate NICs (ou modificar as existentes) e associá-los tooNAT regras, regras de Balanceador de carga e testes.</span><span class="sxs-lookup"><span data-stu-id="862b5-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="862b5-154">Criar uma NIC denominada *lb-nic1 ser*e associá-lo a saudação *rdp1* NAT regra e hello *NRPbackendpool* pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="862b5-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="862b5-155">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="862b5-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
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

2. <span data-ttu-id="862b5-156">Criar uma NIC denominada *lb-nic2 ser*e associá-lo a saudação *rdp2* NAT regra e hello *NRPbackendpool* pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="862b5-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="862b5-157">Criar uma máquina virtual (VM) denominada *web1*e associá-lo a saudação NIC denominado *lb-nic1 ser*.</span><span class="sxs-lookup"><span data-stu-id="862b5-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="862b5-158">Uma conta de armazenamento chamado *web1nrp* foi criado antes de executar o comando de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="862b5-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="862b5-159">Máquinas virtuais em um toobe de necessidade de Balanceador de carga no hello mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="862b5-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="862b5-160">Use `azure availset create` toocreate um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="862b5-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="862b5-161">saída de Hello deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="862b5-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="862b5-162">mensagem informativa Olá **isso é uma NIC sem publicIP configurado** é esperado porque hello NIC criada Olá balanceador de carga conectando tooInternet usando Olá pública IP balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="862b5-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="862b5-163">Desde Olá *lb-nic1 ser* NIC está associada à saudação *rdp1* regra de NAT, você pode conectar-se muito*web1* usando o RDP pela porta 3441 no balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="862b5-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="862b5-164">Criar uma máquina virtual (VM) denominada *web2*e associá-lo a saudação NIC denominado *lb-nic2 ser*.</span><span class="sxs-lookup"><span data-stu-id="862b5-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="862b5-165">Uma conta de armazenamento chamado *web1nrp* foi criado antes de executar o comando de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="862b5-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="862b5-166">Atualizar um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="862b5-166">Update an existing load balancer</span></span>
<span data-ttu-id="862b5-167">Você pode adicionar regras ao fazer referência a um balanceador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="862b5-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="862b5-168">No exemplo a seguir hello, uma nova regra de Balanceador de carga é adicionada balanceador de carga existente tooan **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="862b5-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="862b5-169">Excluir um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="862b5-169">Delete a load balancer</span></span>
<span data-ttu-id="862b5-170">Use Olá comando tooremove um balanceador de carga a seguir:</span><span class="sxs-lookup"><span data-stu-id="862b5-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="862b5-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="862b5-171">Next steps</span></span>
[<span data-ttu-id="862b5-172">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="862b5-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="862b5-173">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="862b5-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="862b5-174">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="862b5-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
