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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Criar um conjunto de dimensionamento de máquinas virtuais e implantar um aplicativo altamente disponível no Windows
Um conjunto de escala de máquina virtual permite que você toodeploy e gerenciar um conjunto de máquinas virtuais idênticos e o dimensionamento automático. Você pode dimensionar o número de saudação de VMs no conjunto de escala de saudação manualmente ou definir tooautoscale regras com base no uso da CPU, a demanda por memória ou o tráfego de rede. Neste tutorial, você implantará um conjunto de dimensionamento de máquinas virtuais no Azure. Você aprenderá como:

> [!div class="checklist"]
> * Use Olá extensão de Script personalizado toodefine um tooscale de site do IIS
> * Criar um balanceador de carga para o conjunto de dimensionamento
> * Criar um conjunto de dimensionamento de máquinas virtuais
> * Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala
> * Criar regras de dimensionamento automático

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Visão geral do conjunto de escala
Conjuntos de escala usar conceitos semelhantes de como você aprendeu no tutorial anterior Olá muito[criar VMs altamente disponíveis](tutorial-availability-sets.md). As VMs em um conjunto de dimensionamento são distribuídas entre domínios de falha e de atualização, assim como as VMs em um conjunto de disponibilidade.

VMs são criadas conforme necessário em um conjunto de escala. Definir toocontrol de regras de dimensionamento automático como e quando as VMs são adicionadas ou removidas do conjunto de escala de saudação. Essas regras podem ser disparados com base em métricas como carga de CPU, utilização de memória ou tráfego de rede.

Escala define o suporte de too1, 000 VMs quando você usar uma imagem da plataforma Windows Azure. Para cargas de trabalho com instalação significativos ou requisitos de personalização de VM, pode ser muito[criar uma imagem VM personalizada](tutorial-custom-images.md). Você pode criar máquinas virtuais de too100 em uma escala definida ao usar uma imagem personalizada.


## <a name="create-an-app-tooscale"></a>Criar um aplicativo tooscale
Antes de criar um conjunto de dimensionamento, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAutomate* em Olá *EastUS* local:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

Um tutorial anterior, você aprendeu como muito[configuração da VM automatizar](tutorial-automate-vm-deployment.md) usando Olá extensão de Script personalizado. Criar a configuração de um conjunto de escala, em seguida, aplicar tooinstall uma extensão de Script personalizado e configurar o IIS:

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

## <a name="create-scale-load-balancer"></a>Criar um balanceador de carga de dimensionamento
Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros. Um teste de integridade do balanceador de carga monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM. Para obter mais informações, consulte o tutorial de Avançar de saudação em [como tooload equilibrar as máquinas virtuais do Windows](tutorial-load-balancer.md).

Crie um balanceador de carga que tenha um endereço IP público e distribua o tráfego da Web na porta 80:

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

## <a name="create-a-scale-set"></a>Criar um conjunto de escala
Agora, crie um conjunto de dimensionamento de máquinas virtuais com [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Olá, exemplo a seguir cria uma conjunto nomeada de escalas *myScaleSet*:

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

Ele usa toocreate de alguns minutos e configurar todos os recursos de conjunto de escala hello e máquinas virtuais.


## <a name="test-your-app"></a>Testar seu aplicativo
toosee seu site do IIS em ação, obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado como parte do conjunto de escala hello:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Insira o endereço IP público de saudação no navegador da web de tooa. aplicativo Hello é exibido, incluindo o nome de host de saudação do hello VM que Olá a carga do tráfego do balanceador distribuída para:

![Execução do site do IIS](./media/tutorial-create-vmss/running-iis-site.png)

a escala de saudação toosee definida em ação, você pode forçar atualização sua carga de saudação do toosee de navegador da web balanceador distribuir o tráfego entre todas as VMs Olá executando o aplicativo.


## <a name="management-tasks"></a>Tarefas de gerenciamento
Ciclo de vida de saudação do conjunto de escala hello, talvez seja necessário toorun uma ou mais tarefas de gerenciamento. Além disso, talvez você queira toocreate scripts que automatizam várias tarefas de ciclo de vida. PowerShell do Azure fornece uma maneira rápida toodo essas tarefas. Estas são algumas tarefas comuns.

### <a name="view-vms-in-a-scale-set"></a>Exibição de VMs em um conjunto de escala
uma lista de VMs em execução em escala de seu conjunto de tooview, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) da seguinte maneira:

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


### <a name="increase-or-decrease-vm-instances"></a>Aumentar ou diminuir as instâncias de VM
toosee Olá número de instâncias atualmente têm em uma escala de definido, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) e consultar *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Você pode, em seguida, manualmente aumentar ou diminuir Olá número de máquinas virtuais em escala Olá com [AzureRmVmss atualização](/powershell/module/azurerm.compute/update-azurermvmss). Olá exemplo a seguir define Olá número de VMs em sua escala definida muito*5*:

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

Se usa Olá de tooupdate alguns minutos número especificado de instâncias no seu conjunto de escala.


### <a name="configure-autoscale-rules"></a>Configurar regras de dimensionamento automático
Em vez de dimensionamento manualmente número Olá de instâncias em sua escala definida, você pode definir regras de dimensionamento automático. Essas regras monitoram Olá instâncias em sua escala definida e respondem adequadamente com base nas métricas e limites que você definir. saudação de exemplo a seguir se expande número Olá de instâncias por um quando carga da CPU média de saudação é maior que 60% durante um período de 5 minutos. Se a carga de média de CPU de saudação cair abaixo de 30% em um período de 5 minutos, instâncias de saudação são dimensionadas em por uma instância:

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


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você criou um conjunto de dimensionamento de máquinas virtuais. Você aprendeu como:

> [!div class="checklist"]
> * Use Olá extensão de Script personalizado toodefine um tooscale de site do IIS
> * Criar um balanceador de carga para o conjunto de dimensionamento
> * Criar um conjunto de dimensionamento de máquinas virtuais
> * Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala
> * Criar regras de dimensionamento automático

Toohello toolearn de tutorial Avançar adiantar mais sobre conceitos para máquinas virtuais de balanceamento de carga.

> [!div class="nextstepaction"]
> [Balancear carga de máquinas virtuais](tutorial-load-balancer.md)
