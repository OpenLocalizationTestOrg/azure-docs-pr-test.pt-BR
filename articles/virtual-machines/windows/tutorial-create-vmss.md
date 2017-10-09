---
title: "aaaCreate uma máquina Virtual escala conjuntos para Windows no Azure | Microsoft Docs"
description: "Criar e implantar um aplicativo altamente disponível em VMs Windows usando um conjunto de dimensionamento de máquinas virtuais"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="f5e3f-103">Criar um conjunto de dimensionamento de máquinas virtuais e implantar um aplicativo altamente disponível no Windows</span><span class="sxs-lookup"><span data-stu-id="f5e3f-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="f5e3f-104">Um conjunto de escala de máquina virtual permite que você toodeploy e gerenciar um conjunto de máquinas virtuais idênticos e o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="f5e3f-105">Você pode dimensionar o número de saudação de VMs no conjunto de escala de saudação manualmente ou definir tooautoscale regras com base no uso da CPU, a demanda por memória ou o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="f5e3f-106">Neste tutorial, você implantará um conjunto de dimensionamento de máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="f5e3f-107">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5e3f-108">Use Olá extensão de Script personalizado toodefine um tooscale de site do IIS</span><span class="sxs-lookup"><span data-stu-id="f5e3f-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="f5e3f-109">Criar um balanceador de carga para o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="f5e3f-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="f5e3f-110">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f5e3f-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="f5e3f-111">Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="f5e3f-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="f5e3f-112">Criar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="f5e3f-112">Create autoscale rules</span></span>

<span data-ttu-id="f5e3f-113">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f5e3f-114">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f5e3f-115">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="f5e3f-116">Visão geral do conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="f5e3f-116">Scale Set overview</span></span>
<span data-ttu-id="f5e3f-117">Conjuntos de escala usar conceitos semelhantes de como você aprendeu no tutorial anterior Olá muito[criar VMs altamente disponíveis](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="f5e3f-118">As VMs em um conjunto de dimensionamento são distribuídas entre domínios de falha e de atualização, assim como as VMs em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="f5e3f-119">VMs são criadas conforme necessário em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="f5e3f-120">Definir toocontrol de regras de dimensionamento automático como e quando as VMs são adicionadas ou removidas do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="f5e3f-121">Essas regras podem ser disparados com base em métricas como carga de CPU, utilização de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="f5e3f-122">Escala define o suporte de too1, 000 VMs quando você usar uma imagem da plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="f5e3f-123">Para cargas de trabalho com instalação significativos ou requisitos de personalização de VM, pode ser muito[criar uma imagem VM personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="f5e3f-124">Você pode criar máquinas virtuais de too100 em uma escala definida ao usar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="f5e3f-125">Criar um aplicativo tooscale</span><span class="sxs-lookup"><span data-stu-id="f5e3f-125">Create an app tooscale</span></span>
<span data-ttu-id="f5e3f-126">Antes de criar um conjunto de dimensionamento, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f5e3f-127">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAutomate* em Olá *EastUS* local:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="f5e3f-128">Um tutorial anterior, você aprendeu como muito[configuração da VM automatizar](tutorial-automate-vm-deployment.md) usando Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="f5e3f-129">Criar a configuração de um conjunto de escala, em seguida, aplicar tooinstall uma extensão de Script personalizado e configurar o IIS:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="f5e3f-130">Criar um balanceador de carga de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="f5e3f-130">Create scale load balancer</span></span>
<span data-ttu-id="f5e3f-131">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="f5e3f-132">Um teste de integridade do balanceador de carga monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="f5e3f-133">Para obter mais informações, consulte o tutorial de Avançar de saudação em [como tooload equilibrar as máquinas virtuais do Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="f5e3f-134">Crie um balanceador de carga que tenha um endereço IP público e distribua o tráfego da Web na porta 80:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="f5e3f-135">Criar um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="f5e3f-135">Create a scale set</span></span>
<span data-ttu-id="f5e3f-136">Agora, crie um conjunto de dimensionamento de máquinas virtuais com [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="f5e3f-137">Olá, exemplo a seguir cria uma conjunto nomeada de escalas *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="f5e3f-138">Ele usa toocreate de alguns minutos e configurar todos os recursos de conjunto de escala hello e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="f5e3f-139">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f5e3f-139">Test your app</span></span>
<span data-ttu-id="f5e3f-140">toosee seu site do IIS em ação, obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f5e3f-141">Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado como parte do conjunto de escala hello:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="f5e3f-142">Insira o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="f5e3f-143">aplicativo Hello é exibido, incluindo o nome de host de saudação do hello VM que Olá a carga do tráfego do balanceador distribuída para:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Execução do site do IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="f5e3f-145">a escala de saudação toosee definida em ação, você pode forçar atualização sua carga de saudação do toosee de navegador da web balanceador distribuir o tráfego entre todas as VMs Olá executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="f5e3f-146">Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="f5e3f-146">Management tasks</span></span>
<span data-ttu-id="f5e3f-147">Ciclo de vida de saudação do conjunto de escala hello, talvez seja necessário toorun uma ou mais tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="f5e3f-148">Além disso, talvez você queira toocreate scripts que automatizam várias tarefas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="f5e3f-149">PowerShell do Azure fornece uma maneira rápida toodo essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="f5e3f-150">Estas são algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="f5e3f-151">Exibição de VMs em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="f5e3f-151">View VMs in a scale set</span></span>
<span data-ttu-id="f5e3f-152">uma lista de VMs em execução em escala de seu conjunto de tooview, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="f5e3f-153">Aumentar ou diminuir as instâncias de VM</span><span class="sxs-lookup"><span data-stu-id="f5e3f-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="f5e3f-154">toosee Olá número de instâncias atualmente têm em uma escala de definido, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) e consultar *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="f5e3f-155">Você pode, em seguida, manualmente aumentar ou diminuir Olá número de máquinas virtuais em escala Olá com [AzureRmVmss atualização](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="f5e3f-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="f5e3f-156">Olá exemplo a seguir define Olá número de VMs em sua escala definida muito*5*:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="f5e3f-157">Se usa Olá de tooupdate alguns minutos número especificado de instâncias no seu conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="f5e3f-158">Configurar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="f5e3f-158">Configure autoscale rules</span></span>
<span data-ttu-id="f5e3f-159">Em vez de dimensionamento manualmente número Olá de instâncias em sua escala definida, você pode definir regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="f5e3f-160">Essas regras monitoram Olá instâncias em sua escala definida e respondem adequadamente com base nas métricas e limites que você definir.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="f5e3f-161">saudação de exemplo a seguir se expande número Olá de instâncias por um quando carga da CPU média de saudação é maior que 60% durante um período de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="f5e3f-162">Se a carga de média de CPU de saudação cair abaixo de 30% em um período de 5 minutos, instâncias de saudação são dimensionadas em por uma instância:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="f5e3f-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5e3f-163">Next steps</span></span>
<span data-ttu-id="f5e3f-164">Neste tutorial, você criou um conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="f5e3f-165">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="f5e3f-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5e3f-166">Use Olá extensão de Script personalizado toodefine um tooscale de site do IIS</span><span class="sxs-lookup"><span data-stu-id="f5e3f-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="f5e3f-167">Criar um balanceador de carga para o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="f5e3f-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="f5e3f-168">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f5e3f-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="f5e3f-169">Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="f5e3f-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="f5e3f-170">Criar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="f5e3f-170">Create autoscale rules</span></span>

<span data-ttu-id="f5e3f-171">Toohello toolearn de tutorial Avançar adiantar mais sobre conceitos para máquinas virtuais de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="f5e3f-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f5e3f-172">Balancear carga de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f5e3f-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
