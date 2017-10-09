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
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>Criando Conjuntos de Escala de Máquina Virtual usando cmdlets do PowerShell
Este artigo o orienta por meio de um exemplo de como toocreate uma escala de máquina Virtual configurada (VMSS). Ele cria um conjunto de dimensionamento de três nós, com a rede e o armazenamento associados.

## <a name="first-steps"></a>Primeiras Etapas
Certifique-se de ter hello mais recente do Azure PowerShell module instalada, toomake se você tem os cmdlets do PowerShell Olá necessário toomaintain e criar conjuntos de escala.
Acesse ferramentas de linha de comando toohello [aqui](http://aka.ms/webpi-azps) para hello mais recente disponível módulos do Azure.

toofind VMSS relacionados commandlets, use a cadeia de caracteres de pesquisa Olá \*VMSS\*. Por exemplo, _gcm *vmss*_

## <a name="creating-a-vmss"></a>Criando uma VMSS
#### <a name="create-resource-group"></a>Criar grupo de recursos
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>Criar Rede (Rede Virtual/Sub-rede)
#### <a name="subnet-specification"></a>Especificação de Sub-rede
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>Especificação de Rede Virtual
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>Criar recurso IP público tooAllow acesso externo
Isso será associado toohello balanceador de carga.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>Criar balanceador de carga
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

#### <a name="configure-load-balancer"></a>Configurar o Balanceador de Carga
Criar a configuração de Pool de endereços de back-end, isso será compartilhado por NICs Olá Olá VMs no conjunto de escala de saudação.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

Definir a porta de investigação com balanceamento de carga, alterar as configurações de saudação conforme apropriado para seu aplicativo.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

Criar um pool NAT de entrada para conectividade direta roteada (não com balanceamento de carga) toohello VMs em escala Olá definidas por meio do hello balanceador de carga. Isso é toodemonstrate usando o RDP e não pode ser necessário em seu aplicativo.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Crie hello de carga balanceada regra, este exemplo mostra a carga balanceamento porta 80 das solicitações, usando as configurações de saudação de etapas anteriores.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

Criar o Balanceador de Carga com a configuração.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

Verifique as configurações de balanceamento de carga, verifique a carga de configurações de porta equilibrada, observe que você não verá as regras de NAT de entrada até Olá VMs no conjunto de escala de saudação são criadas.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>Configurar e criar hello escala definida
Observe que este exemplo de infraestrutura mostra como distribuir tooset backup e o tráfego de web escala em conjunto de escala hello, mas Olá imagens de máquinas virtuais especificadas aqui não têm serviços web instalados.

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

Associar tooLoad NIC balanceador e subrede

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

Criar configuração de conjunto de dimensionamento

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

Criar a configuração do conjunto de dimensionamento

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

Agora você criou o conjunto de escala hello. Você pode testar conexão toohello VM individual usando o RDP neste exemplo:

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
