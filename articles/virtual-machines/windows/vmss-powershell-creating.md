---
title: "conjuntos de aaaCreating escala de máquinas virtuais usando cmdlets do PowerShell | Microsoft Docs"
description: "Introdução à criação e ao gerenciamento dos seus primeiros Conjuntos de Escalas de Máquina Virtual do Azure usando cmdlets do Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="f4b5a-103">Criando Conjuntos de Escala de Máquina Virtual usando cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4b5a-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="f4b5a-104">Este artigo o orienta por meio de um exemplo de como toocreate uma escala de máquina Virtual configurada (VMSS).</span><span class="sxs-lookup"><span data-stu-id="f4b5a-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="f4b5a-105">Ele cria um conjunto de dimensionamento de três nós, com a rede e o armazenamento associados.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="f4b5a-106">Primeiras Etapas</span><span class="sxs-lookup"><span data-stu-id="f4b5a-106">First Steps</span></span>
<span data-ttu-id="f4b5a-107">Certifique-se de ter hello mais recente do Azure PowerShell module instalada, toomake se você tem os cmdlets do PowerShell Olá necessário toomaintain e criar conjuntos de escala.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="f4b5a-108">Acesse ferramentas de linha de comando toohello [aqui](http://aka.ms/webpi-azps) para hello mais recente disponível módulos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="f4b5a-109">toofind VMSS relacionados commandlets, use a cadeia de caracteres de pesquisa Olá \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="f4b5a-110">Por exemplo, _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="f4b5a-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="f4b5a-111">Criando uma VMSS</span><span class="sxs-lookup"><span data-stu-id="f4b5a-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="f4b5a-112">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f4b5a-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="f4b5a-113">Criar Rede (Rede Virtual/Sub-rede)</span><span class="sxs-lookup"><span data-stu-id="f4b5a-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="f4b5a-114">Especificação de Sub-rede</span><span class="sxs-lookup"><span data-stu-id="f4b5a-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="f4b5a-115">Especificação de Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="f4b5a-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="f4b5a-116">Criar recurso IP público tooAllow acesso externo</span><span class="sxs-lookup"><span data-stu-id="f4b5a-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="f4b5a-117">Isso será associado toohello balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="f4b5a-118">Criar balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f4b5a-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="f4b5a-119">Configurar o Balanceador de Carga</span><span class="sxs-lookup"><span data-stu-id="f4b5a-119">Configure Load Balancer</span></span>
<span data-ttu-id="f4b5a-120">Criar a configuração de Pool de endereços de back-end, isso será compartilhado por NICs Olá Olá VMs no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="f4b5a-121">Definir a porta de investigação com balanceamento de carga, alterar as configurações de saudação conforme apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="f4b5a-122">Criar um pool NAT de entrada para conectividade direta roteada (não com balanceamento de carga) toohello VMs em escala Olá definidas por meio do hello balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="f4b5a-123">Isso é toodemonstrate usando o RDP e não pode ser necessário em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="f4b5a-124">Crie hello de carga balanceada regra, este exemplo mostra a carga balanceamento porta 80 das solicitações, usando as configurações de saudação de etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="f4b5a-125">Criar o Balanceador de Carga com a configuração.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="f4b5a-126">Verifique as configurações de balanceamento de carga, verifique a carga de configurações de porta equilibrada, observe que você não verá as regras de NAT de entrada até Olá VMs no conjunto de escala de saudação são criadas.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="f4b5a-127">Configurar e criar hello escala definida</span><span class="sxs-lookup"><span data-stu-id="f4b5a-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="f4b5a-128">Observe que este exemplo de infraestrutura mostra como distribuir tooset backup e o tráfego de web escala em conjunto de escala hello, mas Olá imagens de máquinas virtuais especificadas aqui não têm serviços web instalados.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="f4b5a-129">Associar tooLoad NIC balanceador e subrede</span><span class="sxs-lookup"><span data-stu-id="f4b5a-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="f4b5a-130">Criar configuração de conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="f4b5a-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="f4b5a-131">Criar a configuração do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="f4b5a-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="f4b5a-132">Agora você criou o conjunto de escala hello.</span><span class="sxs-lookup"><span data-stu-id="f4b5a-132">Now you have created hello scale set.</span></span> <span data-ttu-id="f4b5a-133">Você pode testar conexão toohello VM individual usando o RDP neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="f4b5a-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
