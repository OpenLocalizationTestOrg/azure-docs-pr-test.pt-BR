---
title: "Criação de conjuntos de dimensionamento de máquinas virtuais usando cmdlets do PowerShell | Microsoft Docs"
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
ms.openlocfilehash: a3a36028a75d6cb7eb36277f3e2b5ab833c96a96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="b26c4-103">Criando Conjuntos de Escala de Máquina Virtual usando cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b26c4-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="b26c4-104">Este artigo apresenta um exemplo de como criar um VMSS (conjunto de dimensionamento de máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="b26c4-104">This article walks through an example of how to create a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="b26c4-105">Ele cria um conjunto de dimensionamento de três nós, com a rede e o armazenamento associados.</span><span class="sxs-lookup"><span data-stu-id="b26c4-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="b26c4-106">Primeiras Etapas</span><span class="sxs-lookup"><span data-stu-id="b26c4-106">First Steps</span></span>
<span data-ttu-id="b26c4-107">Certifique-se de ter o módulo do Azure PowerShell mais recente instalado para assegurar que você tenha os cmdlets do PowerShell necessários para manter e criar conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b26c4-107">Ensure you have the latest Azure PowerShell module installed, to make sure you have the PowerShell commandlets needed to maintain, and create scale sets.</span></span>
<span data-ttu-id="b26c4-108">Vá para as ferramentas de linha de comando [aqui](http://aka.ms/webpi-azps) para os Módulos do Azure mais recentes disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b26c4-108">Go to the command line tools [here](http://aka.ms/webpi-azps) for the latest available Azure Modules.</span></span>

<span data-ttu-id="b26c4-109">Para localizar commandlets relacionados ao VMSS, use a cadeia de caracteres de pesquisa \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="b26c4-109">To find VMSS related commandlets, use the search string \*VMSS\*.</span></span> <span data-ttu-id="b26c4-110">Por exemplo, _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="b26c4-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="b26c4-111">Criando uma VMSS</span><span class="sxs-lookup"><span data-stu-id="b26c4-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="b26c4-112">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b26c4-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="b26c4-113">Criar Rede (Rede Virtual/Sub-rede)</span><span class="sxs-lookup"><span data-stu-id="b26c4-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="b26c4-114">Especificação de Sub-rede</span><span class="sxs-lookup"><span data-stu-id="b26c4-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="b26c4-115">Especificação de Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="b26c4-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume the new subnet is the only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-to-allow-external-access"></a><span data-ttu-id="b26c4-116">Criar Recurso IP Público para Permitir o Acesso Externo</span><span class="sxs-lookup"><span data-stu-id="b26c4-116">Create Public IP Resource to Allow External Access</span></span>
<span data-ttu-id="b26c4-117">Isso será associado ao balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b26c4-117">This will be bound to the Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="b26c4-118">Criar balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b26c4-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP to Load Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="b26c4-119">Configurar o Balanceador de Carga</span><span class="sxs-lookup"><span data-stu-id="b26c4-119">Configure Load Balancer</span></span>
<span data-ttu-id="b26c4-120">Criar Configuração de Pool de Endereços de Back-end, isso será compartilhado pelas NICs das VMs no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b26c4-120">Create Backend Address Pool Config, this will be shared by the NICs of the VMs in the scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="b26c4-121">Definir a Porta de Investigação com Balanceamento de Carga, altere as configurações conforme apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b26c4-121">Set Load Balanced Probe Port, change the settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="b26c4-122">Crie um pool de NAT de entrada para conectividade direta roteada (sem balanceamento de carga) para as VMs no conjunto de dimensionamento por meio do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b26c4-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) to the VMs in the scale set via the Load Balancer.</span></span> <span data-ttu-id="b26c4-123">Isso é demonstrar o uso do RDP e pode não ser necessário em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b26c4-123">This is to demonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="b26c4-124">Crie a Regra Balanceada de Carga, este exemplo mostra as solicitações da porta 80 de balanceamento de carga usando as configurações das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="b26c4-124">Create the Load Balanced Rule, this example shows load balancing port 80 requests, using the settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="b26c4-125">Criar o Balanceador de Carga com a configuração.</span><span class="sxs-lookup"><span data-stu-id="b26c4-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="b26c4-126">Verifique as configurações de LB, verifique as configurações da porta com balanceamento de carga, observe que você não verá regras de NAT de Entrada até que as VMs no conjunto de dimensionamento sejam criadas.</span><span class="sxs-lookup"><span data-stu-id="b26c4-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until the VMs in the scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-the-scale-set"></a><span data-ttu-id="b26c4-127">Configurar e criar o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="b26c4-127">Configure and Create the scale set</span></span>
<span data-ttu-id="b26c4-128">Observe que este exemplo de infraestrutura mostra como instalar a distribuição e o dimensionamento de tráfego da Web através do conjunto de dimensionamento, mas as imagens das VMs especificadas aqui não tem serviços Web instalados.</span><span class="sxs-lookup"><span data-stu-id="b26c4-128">Note, this infrastructure example shows how to set up distribute and scale web traffic across the scale set, but the VMs Images specified here do not have any web services installed.</span></span>

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

<span data-ttu-id="b26c4-129">Associar NIC ao Balanceador de Carga e à Sub-rede</span><span class="sxs-lookup"><span data-stu-id="b26c4-129">Bind NIC to Load Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="b26c4-130">Criar configuração de conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="b26c4-130">Create scale set Config</span></span>

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

<span data-ttu-id="b26c4-131">Criar a configuração do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="b26c4-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="b26c4-132">Agora você criou o conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b26c4-132">Now you have created the scale set.</span></span> <span data-ttu-id="b26c4-133">Você pode testar a conexão com a VM individual usando o RDP neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="b26c4-133">You can test connecting to the individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
