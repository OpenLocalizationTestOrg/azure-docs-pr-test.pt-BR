---
title: Criar um balanceador de carga interno do Azure - PowerShell | Microsoft Docs
description: Saiba como criar um balanceador de carga interno no Gerenciador de Recursos usando o PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7bd31ab8f52ec5e81f6966000554be46eaa59396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="8e06a-103">Criar um balanceador de carga interno usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e06a-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e06a-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e06a-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="8e06a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e06a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="8e06a-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8e06a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="8e06a-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="8e06a-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8e06a-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8e06a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8e06a-109">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8e06a-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="8e06a-110">As etapas a seguir explicam como criar um balanceador de carga interno usando o Azure Resource Manager com PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e06a-110">The following steps explain how to create an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="8e06a-111">Com o Azure Resource Manager, os itens para criar um balanceador de carga interno são configurados individualmente e combinados para criar um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8e06a-111">With Azure Resource Manager, the items to create a Internal load balancer are configured individually and then combined to create a load balancer.</span></span>

<span data-ttu-id="8e06a-112">Você precisa criar e configurar os seguintes objetos para implantar um balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="8e06a-112">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="8e06a-113">Configuração do IP de front-end - vai configurar o endereço IP privado para tráfego de rede de entrada</span><span class="sxs-lookup"><span data-stu-id="8e06a-113">Front end IP configuration - will configure the private IP address for incoming network traffic</span></span>
* <span data-ttu-id="8e06a-114">Pool de endereços de back-end - vai configurar as interfaces de rede que receberão o tráfego com balanceamento de carga proveniente do pool de IPs de front-end</span><span class="sxs-lookup"><span data-stu-id="8e06a-114">Backend address pool - will configure the network interfaces which will receive the load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="8e06a-115">Regras de balanceamento de carga - configuração de porta local e de origem para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8e06a-115">Load balancing rules - source and local port configuration for the load balancer.</span></span>
* <span data-ttu-id="8e06a-116">Investigações - configura a investigação de status de integridade para instâncias de Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="8e06a-116">Probes - configures the health status probe for the Virtual Machine instances.</span></span>
* <span data-ttu-id="8e06a-117">Regras NAT de entrada - configura as regras de porta para acessar diretamente uma das instâncias de Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="8e06a-117">Inbound NAT rules - configures the port rules to directly access one of the Virtual Machine instances.</span></span>

<span data-ttu-id="8e06a-118">É possível obter mais informações sobre componentes do balanceador de carga com o gerenciador de recursos do Azure em [Suporte do Gerenciador de Recursos do Azure para balanceador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8e06a-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="8e06a-119">As etapas a seguir explicam como configurar um balanceador de carga entre duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8e06a-119">The following steps explain how to configure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-to-use-resource-manager"></a><span data-ttu-id="8e06a-120">Configurar o PowerShell para usar o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="8e06a-120">Setup PowerShell to use Resource Manager</span></span>

<span data-ttu-id="8e06a-121">Certifique-se de ter a versão de produção mais recente do módulo do Azure para PowerShell e de configurar corretamente o PowerShell para acessar sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e06a-121">Make sure you have the latest production version of the Azure module for PowerShell, and have PowerShell setup correctly to access your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="8e06a-122">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8e06a-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="8e06a-123">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8e06a-123">Step 2</span></span>

<span data-ttu-id="8e06a-124">Verificar as assinaturas da conta</span><span class="sxs-lookup"><span data-stu-id="8e06a-124">Check the subscriptions for the account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="8e06a-125">Você deverá se autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="8e06a-125">You will be prompted to Authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="8e06a-126">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="8e06a-126">Step 3</span></span>

<span data-ttu-id="8e06a-127">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="8e06a-127">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="8e06a-128">Criar grupo de recursos para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8e06a-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="8e06a-129">Crie um grupo de recursos (pule esta etapa se você estiver usando um grupo de recursos existente)</span><span class="sxs-lookup"><span data-stu-id="8e06a-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="8e06a-130">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="8e06a-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8e06a-131">Ele é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="8e06a-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="8e06a-132">Certifique-se de que todos os comandos para criar um balanceador de carga usarão o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8e06a-132">Make sure all commands to create a load balancer will use the same resource group.</span></span>

<span data-ttu-id="8e06a-133">No exemplo anterior, criamos um grupo de recursos denominado "NRP-RG" e o local "Oeste dos EUA".</span><span class="sxs-lookup"><span data-stu-id="8e06a-133">In the example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="8e06a-134">Crie a Rede virtual e um endereço IP privado para o pool de IP front-end</span><span class="sxs-lookup"><span data-stu-id="8e06a-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="8e06a-135">Cria uma sub-rede para a rede virtual e atribui à variável $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="8e06a-135">Creates a subnet for the virtual network and assigns to variable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="8e06a-136">Criar uma rede virtual:</span><span class="sxs-lookup"><span data-stu-id="8e06a-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="8e06a-137">Cria a rede virtual e adiciona a sub-rede lb-subnet-be à rede virtual NRPVNet e atribui à variável $vnet.</span><span class="sxs-lookup"><span data-stu-id="8e06a-137">Creates the virtual network and adds the subnet lb-subnet-be to the virtual network NRPVNet and assigns to variable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="8e06a-138">Criar o pool de IP front-end e pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="8e06a-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="8e06a-139">Configure um pool de IP front-end para o tráfego de rede do balanceador de carga de entrada e pool de endereços de back-end para receber o tráfego balanceado de carga.</span><span class="sxs-lookup"><span data-stu-id="8e06a-139">Setting up a front end IP pool for the incoming load balancer network traffic and backend address pool to receive the load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="8e06a-140">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8e06a-140">Step 1</span></span>

<span data-ttu-id="8e06a-141">Crie um pool de IPs de front-end usando o endereço IP privado 10.0.2.5 para a sub-rede 10.0.2.0/24, que será o ponto de extremidade do tráfego de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="8e06a-141">Create a front end IP pool using the private IP address 10.0.2.5 for the subnet 10.0.2.0/24 which will be the incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="8e06a-142">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8e06a-142">Step 2</span></span>

<span data-ttu-id="8e06a-143">Configure um pool de endereços de back-end usado para receber o tráfego de entrada de pool de IP front-end:</span><span class="sxs-lookup"><span data-stu-id="8e06a-143">Set up a back end address pool used to receive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="8e06a-144">Criar regras de balanceamento de carga, regras de NAT, teste e balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8e06a-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="8e06a-145">Depois de criar o pool de IP front-end e o pool de endereços de back-end, você precisa criar as regras que pertencem o recurso de balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="8e06a-145">After creating the front end IP pool and the backend address pool, you will need to create the rules which will belong to the load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="8e06a-146">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8e06a-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="8e06a-147">O exemplo acima é a criação dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8e06a-147">The example above is creating the following items:</span></span>

* <span data-ttu-id="8e06a-148">Regra de NAT em que todo o tráfego de entrada para a porta 3441 irá para a porta 3389.</span><span class="sxs-lookup"><span data-stu-id="8e06a-148">NAT rule which all incoming traffic to port 3441 will go to port 3389.</span></span>
* <span data-ttu-id="8e06a-149">uma segunda regra de NAT em que todo o tráfego de entrada para a porta 3442 irá para a porta 3389.</span><span class="sxs-lookup"><span data-stu-id="8e06a-149">a second NAT rule which all incoming traffic to port 3442 will go to port 3389.</span></span>
* <span data-ttu-id="8e06a-150">uma regra que balanceará a carga de todo o tráfego de entrada na porta pública 80 para a porta local 80 no pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="8e06a-150">a load balancer rule which will load balance all incoming traffic on public port 80 to local port 80 in the back end address pool.</span></span>
* <span data-ttu-id="8e06a-151">uma regra de investigação que verificará o status de integridade para o caminho "HealthProbe.aspx"</span><span class="sxs-lookup"><span data-stu-id="8e06a-151">a probe rule which will check the health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="8e06a-152">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8e06a-152">Step 2</span></span>

<span data-ttu-id="8e06a-153">Criar o balanceador de carga adicionando todos os objetos (regras de NAT, regras do balanceador de carga, configurações de teste) juntos:</span><span class="sxs-lookup"><span data-stu-id="8e06a-153">Create the load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="8e06a-154">Criar interfaces de rede</span><span class="sxs-lookup"><span data-stu-id="8e06a-154">Create network interfaces</span></span>

<span data-ttu-id="8e06a-155">Depois de criar o balanceador de carga interno, você precisa definir quais interfaces de rede estarão recebendo o tráfego de rede com balanceamento de carga entrada, regras de NAT e teste.</span><span class="sxs-lookup"><span data-stu-id="8e06a-155">After creating the internal load balancer, you need define which network interfaces will be receiving the incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="8e06a-156">Nesse caso, a interface de rede é configurada individualmente e pode ser atribuída a uma máquina virtual posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8e06a-156">The network interface in this case is configured individually and can be assigned to a virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="8e06a-157">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8e06a-157">Step 1</span></span>

<span data-ttu-id="8e06a-158">Obtenha a rede virtual do recurso e a sub-rede para criar interfaces de rede:</span><span class="sxs-lookup"><span data-stu-id="8e06a-158">Get the resource virtual network and subnet to create network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="8e06a-159">Esta etapa cria uma interface de rede que pertencerá ao pool de back-end do balanceador de carga e associará a primeira regra NAT para RDP para essa interface de rede:</span><span class="sxs-lookup"><span data-stu-id="8e06a-159">This step creates a network interface which will belong to the load balancer back end pool and associate the first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="8e06a-160">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8e06a-160">Step 2</span></span>

<span data-ttu-id="8e06a-161">Criar uma segunda chamada de interface de rede chamada LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="8e06a-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="8e06a-162">Esta etapa cria uma segunda interface de rede, atribuindo o mesmo pool de back-end do balanceador de carga e associando a segunda regra de NAT criada para RDP:</span><span class="sxs-lookup"><span data-stu-id="8e06a-162">This step creates a second network interface, assigning to the same load balancer back end pool and associating the second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="8e06a-163">O resultado mostrará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8e06a-163">The end result will show the following:</span></span>

    $backendnic1

<span data-ttu-id="8e06a-164">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="8e06a-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="8e06a-165">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="8e06a-165">Step 3</span></span>

<span data-ttu-id="8e06a-166">Use o comando Add-AzureRmVMNetworkInterface para atribuir a NIC a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8e06a-166">Use the command Add-AzureRmVMNetworkInterface to assign the NIC to a virtual Machine.</span></span>

<span data-ttu-id="8e06a-167">Você pode encontrar as instruções passo a passo para criar uma máquina virtual e atribuir a uma NIC de acordo com a documentação: [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8e06a-167">You can find the step by step instructions to create a virtual machine and assign to a NIC following the documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface"></a><span data-ttu-id="8e06a-168">Adicionar a interface de rede</span><span class="sxs-lookup"><span data-stu-id="8e06a-168">Add the network interface</span></span>

<span data-ttu-id="8e06a-169">Se já tiver uma máquina virtual criada, você poderá adicionar a interface de rede com as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e06a-169">If you already have a virtual machine created, you can add the network interface with the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="8e06a-170">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8e06a-170">Step 1</span></span>

<span data-ttu-id="8e06a-171">Carregue o recurso de balanceador de carga em uma variável (se ainda não tiver feito isso).</span><span class="sxs-lookup"><span data-stu-id="8e06a-171">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="8e06a-172">A variável usada é chamada de $lb e usa os mesmos nomes do recurso de balanceador de carga criado acima.</span><span class="sxs-lookup"><span data-stu-id="8e06a-172">The variable used is called $lb and use the same names from the load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="8e06a-173">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8e06a-173">Step 2</span></span>

<span data-ttu-id="8e06a-174">Carregue a configuração de back-end em uma variável.</span><span class="sxs-lookup"><span data-stu-id="8e06a-174">Load the backend configuration to a variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="8e06a-175">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="8e06a-175">Step 3</span></span>

<span data-ttu-id="8e06a-176">Carregue a interface de rede já criada em uma variável.</span><span class="sxs-lookup"><span data-stu-id="8e06a-176">Load the already created network interface into a variable.</span></span> <span data-ttu-id="8e06a-177">O nome da variável usada é $nic.</span><span class="sxs-lookup"><span data-stu-id="8e06a-177">the variable name used is $nic.</span></span> <span data-ttu-id="8e06a-178">O nome da interface de rede usada é o mesmo do exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="8e06a-178">The network interface name used is the same from the example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="8e06a-179">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="8e06a-179">Step 4</span></span>

<span data-ttu-id="8e06a-180">Altere a configuração de back-end na interface de rede.</span><span class="sxs-lookup"><span data-stu-id="8e06a-180">Change the backend configuration on the network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="8e06a-181">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="8e06a-181">Step 5</span></span>

<span data-ttu-id="8e06a-182">Salve o objeto de interface de rede.</span><span class="sxs-lookup"><span data-stu-id="8e06a-182">Save the network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="8e06a-183">Depois que uma interface de rede é adicionada ao pool de back-end do balanceador de carga, ela começa a receber tráfego de rede com base nas regras de balanceamento de carga para esse recurso de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8e06a-183">After a network interface is added to the load balancer backend pool, it starts receiving network traffic based on the load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="8e06a-184">Atualizar um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="8e06a-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="8e06a-185">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8e06a-185">Step 1</span></span>
<span data-ttu-id="8e06a-186">Usando o balanceador de carga do exemplo acima, atribua o objeto balanceador de carga à variável $slb usando Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="8e06a-186">Using the load balancer from the example above, assign load balancer object to variable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="8e06a-187">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8e06a-187">Step 2</span></span>

<span data-ttu-id="8e06a-188">No exemplo a seguir, você adicionará uma nova regra de NAT de entrada usando a porta 81 no front-end e a porta 8181 do pool de back-end a um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="8e06a-188">In the following example, you will add a new Inbound NAT rule using port 81 in the front end and port 8181 for the back end pool to an existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="8e06a-189">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="8e06a-189">Step 3</span></span>

<span data-ttu-id="8e06a-190">Salvar a nova configuração usando Set-AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="8e06a-190">Save the new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="8e06a-191">Remover um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8e06a-191">Remove a load balancer</span></span>

<span data-ttu-id="8e06a-192">Use o comando Remove-AzureRmLoadBalancer para excluir um balanceador de carga criado anteriormente denominado "NRP-LB" em um grupo de recursos chamado "NRP-RG"</span><span class="sxs-lookup"><span data-stu-id="8e06a-192">Use the command Remove-AzureRmLoadBalancer to delete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="8e06a-193">Você pode usar a opção -Force para evitar a solicitação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="8e06a-193">You can use the optional switch -Force to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e06a-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e06a-194">Next steps</span></span>

[<span data-ttu-id="8e06a-195">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8e06a-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8e06a-196">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8e06a-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
