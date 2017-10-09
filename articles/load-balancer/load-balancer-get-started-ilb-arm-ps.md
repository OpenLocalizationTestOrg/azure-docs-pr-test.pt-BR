---
title: aaaCreate interno do Azure carregar balanceador - PowerShell | Microsoft Docs
description: Saiba como o toocreate um interno balanceador usando o PowerShell no Gerenciador de recursos de carga
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
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="09006-103">Criar um balanceador de carga interno usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="09006-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09006-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="09006-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="09006-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09006-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="09006-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="09006-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="09006-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="09006-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="09006-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="09006-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="09006-109">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="09006-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="09006-110">Olá etapas a seguir explica como toocreate um interno carregar balanceador usando o Gerenciador de recursos do Azure com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09006-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="09006-111">No Gerenciador de recursos do Azure, Olá itens toocreate um balanceador de carga interno são configuradas individualmente e, em seguida, combinados toocreate um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="09006-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="09006-112">Você precisa toocreate e configurar Olá objetos toodeploy um balanceador de carga a seguir:</span><span class="sxs-lookup"><span data-stu-id="09006-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="09006-113">Configuração de IP de final de front - irá configurar o endereço IP privado de saudação para tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="09006-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="09006-114">Pool de endereços de back-end - irá configurar interfaces de rede de saudação que irá receber o tráfego de balanceamento de carga hello proveniente do pool IP de front-end</span><span class="sxs-lookup"><span data-stu-id="09006-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="09006-115">Regras de balanceamento de carga - fonte e a configuração de porta local para Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="09006-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="09006-116">Testes - configura a investigação de status de integridade Olá para instâncias de máquina Virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="09006-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="09006-117">Regras NAT de entrada - configura o acesso toodirectly de regras de porta de saudação uma das instâncias de máquina Virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="09006-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="09006-118">É possível obter mais informações sobre componentes do balanceador de carga com o gerenciador de recursos do Azure em [Suporte do Gerenciador de Recursos do Azure para balanceador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="09006-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="09006-119">Olá etapas a seguir explicam como tooconfigure um balanceador de carga entre duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="09006-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="09006-120">Instalação do PowerShell toouse Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="09006-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="09006-121">Verifique se você possui hello, a última versão de produção do hello módulo do Azure para o PowerShell e ter PowerShell instalação tooaccess corretamente sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="09006-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="09006-122">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="09006-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="09006-123">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="09006-123">Step 2</span></span>

<span data-ttu-id="09006-124">Verificar as assinaturas de saudação conta Olá</span><span class="sxs-lookup"><span data-stu-id="09006-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="09006-125">Será solicitada tooAuthenticate com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="09006-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="09006-126">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="09006-126">Step 3</span></span>

<span data-ttu-id="09006-127">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="09006-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="09006-128">Criar grupo de recursos para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="09006-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="09006-129">Crie um grupo de recursos (pule esta etapa se você estiver usando um grupo de recursos existente)</span><span class="sxs-lookup"><span data-stu-id="09006-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="09006-130">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="09006-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="09006-131">Isso é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09006-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="09006-132">Verifique se todos os comandos toocreate um balanceador de carga usará Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09006-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="09006-133">Em Olá exemplo acima é criado um grupo de recursos chamado "NRP-RG" e o local "Oeste US".</span><span class="sxs-lookup"><span data-stu-id="09006-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="09006-134">Crie a Rede virtual e um endereço IP privado para o pool de IP front-end</span><span class="sxs-lookup"><span data-stu-id="09006-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="09006-135">Cria uma sub-rede da rede virtual hello e atribui toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="09006-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="09006-136">Criar uma rede virtual:</span><span class="sxs-lookup"><span data-stu-id="09006-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="09006-137">Criar rede virtual hello e adiciona Olá sub-rede toohello lb sub-rede ser virtual rede NRPVNet e atribui toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="09006-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="09006-138">Criar o pool de IP front-end e pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="09006-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="09006-139">Configurar um pool IP de front-end para entrada de saudação carregar o tráfego de rede do balanceador e tráfego de balanceamento de carga do back-end endereço pool tooreceive Olá.</span><span class="sxs-lookup"><span data-stu-id="09006-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="09006-140">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="09006-140">Step 1</span></span>

<span data-ttu-id="09006-141">Crie um pool IP de front-end usando o endereço IP privado Olá 10.0.2.5 para Olá sub-rede 10.0.2.0/24 que será endpoint de tráfego de rede de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="09006-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="09006-142">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="09006-142">Step 2</span></span>

<span data-ttu-id="09006-143">Configurar um pool de endereços de back-end usado tooreceive o tráfego de entrada de pool de IP de front-end:</span><span class="sxs-lookup"><span data-stu-id="09006-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="09006-144">Criar regras de balanceamento de carga, regras de NAT, teste e balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="09006-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="09006-145">Depois de criar o pool IP de front-end hello e pool de endereços de back-end Olá, você precisará de regras de saudação toocreate que pertencem o recurso de Balanceador de carga toohello:</span><span class="sxs-lookup"><span data-stu-id="09006-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="09006-146">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="09006-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="09006-147">exemplo Hello acima está criando Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="09006-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="09006-148">Regra NAT que todo tráfego tooport 3441 irá tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="09006-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="09006-149">uma segunda regra NAT que todo tráfego tooport 3442 irá tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="09006-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="09006-150">uma regra de Balanceador de carga que será carregado equilibrar todo o tráfego de entrada na porta 80 do toolocal porta pública 80 no pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="09006-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="09006-151">uma regra de teste que irá verificar o status de integridade de saudação de caminho "HealthProbe.aspx"</span><span class="sxs-lookup"><span data-stu-id="09006-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="09006-152">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="09006-152">Step 2</span></span>

<span data-ttu-id="09006-153">Crie o balanceador de carga Olá somar todos os objetos (regras NAT, regras de Balanceador de carga, configurações de teste):</span><span class="sxs-lookup"><span data-stu-id="09006-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="09006-154">Criar interfaces de rede</span><span class="sxs-lookup"><span data-stu-id="09006-154">Create network interfaces</span></span>

<span data-ttu-id="09006-155">Depois de criar o balanceador de carga interno hello, você precisa definir quais interfaces de rede receberá Olá com balanceamento de carga tráfego de rede, as regras de NAT e investigação.</span><span class="sxs-lookup"><span data-stu-id="09006-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="09006-156">interface de rede Olá nesse caso é configurada individualmente e pode ter tooa VM mais tarde.</span><span class="sxs-lookup"><span data-stu-id="09006-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="09006-157">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="09006-157">Step 1</span></span>

<span data-ttu-id="09006-158">Obter recurso Olá interfaces de rede virtuais de toocreate de rede e sub-rede:</span><span class="sxs-lookup"><span data-stu-id="09006-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="09006-159">Essa etapa cria uma interface de rede que pertencem a toohello pool de back-end do balanceador de carga e associar a primeira regra NAT Olá para RDP para essa interface de rede:</span><span class="sxs-lookup"><span data-stu-id="09006-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="09006-160">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="09006-160">Step 2</span></span>

<span data-ttu-id="09006-161">Criar uma segunda chamada de interface de rede chamada LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="09006-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="09006-162">Essa etapa cria uma segunda interface de rede, atribuindo toohello mesmo balanceador de carga novamente terminar pool e associar a segunda regra NAT Olá criado para RDP:</span><span class="sxs-lookup"><span data-stu-id="09006-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="09006-163">resultado final de saudação mostrará o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="09006-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="09006-164">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="09006-164">Expected output:</span></span>

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



### <a name="step-3"></a><span data-ttu-id="09006-165">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="09006-165">Step 3</span></span>

<span data-ttu-id="09006-166">Use Olá comando Add-AzureRmVMNetworkInterface tooassign Olá NIC tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="09006-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="09006-167">Você pode encontrar hello instruções passo a passo toocreate uma máquina virtual e atribua tooa NIC documentação Olá a seguir: [criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09006-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="09006-168">Adicionar a interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="09006-168">Add hello network interface</span></span>

<span data-ttu-id="09006-169">Se você já tiver uma máquina virtual criada, você pode adicionar a interface de rede de saudação com Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="09006-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="09006-170">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="09006-170">Step 1</span></span>

<span data-ttu-id="09006-171">Carregar o recurso de Balanceador de carga de saudação em uma variável (se você ainda não tiver feito isso ainda).</span><span class="sxs-lookup"><span data-stu-id="09006-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="09006-172">variável Olá usado é chamado $lb e use Olá mesmos nomes de recurso de Balanceador de carga Olá criados acima.</span><span class="sxs-lookup"><span data-stu-id="09006-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="09006-173">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="09006-173">Step 2</span></span>

<span data-ttu-id="09006-174">Variável de tooa de configuração de back-end de saudação de carga.</span><span class="sxs-lookup"><span data-stu-id="09006-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="09006-175">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="09006-175">Step 3</span></span>

<span data-ttu-id="09006-176">Carregar a interface de rede Olá já criado em uma variável.</span><span class="sxs-lookup"><span data-stu-id="09006-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="09006-177">nome da variável Olá usado é NIC $.</span><span class="sxs-lookup"><span data-stu-id="09006-177">hello variable name used is $nic.</span></span> <span data-ttu-id="09006-178">nome de interface de rede Olá usado Olá mesmo do exemplo hello acima.</span><span class="sxs-lookup"><span data-stu-id="09006-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="09006-179">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="09006-179">Step 4</span></span>

<span data-ttu-id="09006-180">Alterar configuração de back-end de saudação na interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="09006-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="09006-181">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="09006-181">Step 5</span></span>

<span data-ttu-id="09006-182">Salve o objeto de interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="09006-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="09006-183">Depois que uma interface de rede é adicionada toohello pool de back-end do balanceador de carga, ele começa a receber o tráfego de rede com base em regras para esse recurso de Balanceador de carga de balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="09006-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="09006-184">Atualizar um balanceador de carga existente</span><span class="sxs-lookup"><span data-stu-id="09006-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="09006-185">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="09006-185">Step 1</span></span>
<span data-ttu-id="09006-186">Usar o balanceador de carga de saudação do exemplo hello acima, atribuir toovariable de objeto do balanceador de carga $slb usando Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="09006-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="09006-187">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="09006-187">Step 2</span></span>

<span data-ttu-id="09006-188">Em Olá exemplo a seguir, você adicionará uma nova regra de NAT de entrada usando a porta 81 no front-end hello e porta 8181 volta Olá terminar balanceador de carga existente do pool tooan</span><span class="sxs-lookup"><span data-stu-id="09006-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="09006-189">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="09006-189">Step 3</span></span>

<span data-ttu-id="09006-190">Salve Olá nova configuração usando Set-AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="09006-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="09006-191">Remover um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="09006-191">Remove a load balancer</span></span>

<span data-ttu-id="09006-192">Use Olá comando Remove-AzureRmLoadBalancer toodelete um balanceador de carga criado anteriormente denominado "NRP LB" em um grupo de recursos chamado "RG NRP"</span><span class="sxs-lookup"><span data-stu-id="09006-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="09006-193">Você pode usar o hello opcional alternar - Force tooavoid Olá Solicitar exclusão.</span><span class="sxs-lookup"><span data-stu-id="09006-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09006-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09006-194">Next steps</span></span>

[<span data-ttu-id="09006-195">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="09006-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="09006-196">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="09006-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
