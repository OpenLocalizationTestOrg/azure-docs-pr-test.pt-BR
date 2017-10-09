---
title: "aaaHow tooload equilibrar máquinas virtuais do Windows no Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure carregar balanceador toocreate um aplicativo altamente disponível e seguro entre três máquinas virtuais do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Como o tooload equilibrar a máquinas virtuais do Windows no Azure toocreate um aplicativo altamente disponível
O balanceamento de carga fornece um nível mais alto de disponibilidade, distribuindo as solicitações de entrada em várias máquinas virtuais. Neste tutorial, você aprenderá sobre Olá diferentes componentes do balanceador de carga do Azure Olá que distribuir o tráfego e fornecem alta disponibilidade. Você aprenderá como:

> [!div class="checklist"]
> * Criar um balanceador de carga do Azure
> * Criar uma investigação de integridade do balanceador de carga
> * Criar regras de tráfego para o balanceador de carga
> * Use Olá extensão de Script personalizado toocreate um site IIS básico
> * Criar máquinas virtuais e anexar tooa balanceador de carga
> * Exibir um balanceador de carga em ação
> * Adicionar e remover as VMs de um balanceador de carga

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Visão geral do Balanceador de Carga do Azure
Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros. Um teste de integridade do balanceador de carga monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.

Você define uma configuração de IP de front-end que contém um ou mais endereços IP públicos. Essa configuração de IP de front-end permite que seu toobe de aplicativos e o balanceador de carga acessível pela Internet da saudação. 

Máquinas virtuais conectar-se usando sua placa de interface de rede virtual (NIC) de Balanceador de carga tooa. tráfego de toodistribute toohello VMs, um pool de endereços de back-end contém endereços IP Olá Olá virtual (NICs) toohello conectados do balanceador de carga.

fluxo de saudação toocontrol de tráfego, você definir regras de Balanceador de carga para portas e protocolos que mapeiam tooyour VMs específicos.


## <a name="create-azure-load-balancer"></a>Criar o balanceador de carga do Azure
Esta seção fornece detalhes sobre como você pode criar e configurar cada componente de saudação do balanceador de carga. Antes de criar seu balanceador de carga, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupLoadBalancer* em Olá *EastUS* local:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Criar um endereço IP público
tooaccess Olá de seu aplicativo na Internet, é necessário um endereço IP público Olá balanceador de carga. Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Olá, exemplo a seguir cria um endereço IP público denominado *myPublicIP* em Olá *myResourceGroupLoadBalancer* grupo de recursos:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Criar um balanceador de carga
Crie um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Olá, exemplo a seguir cria um endereço IP de front-end denominado *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Crie um pool de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Olá, exemplo a seguir cria um pool de endereços de back-end denominado *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Agora, crie o balanceador de carga Olá com [AzureRmLoadBalancer novo](/powershell/module/azurerm.network/new-azurermloadbalancer). Olá, exemplo a seguir cria um balanceador de carga denominado *myLoadBalancer* usando Olá *myPublicIP* endereço:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Criar uma investigação de integridade
tooallow Olá balanceador toomonitor Olá status de carga do seu aplicativo, você usar uma investigação de integridade. investigação de integridade Olá dinamicamente adiciona ou remove as VMs de rotação do balanceador de carga de saudação com base em suas verificações de toohealth de resposta. Por padrão, uma máquina virtual é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundos. Crie uma investigação de integridade com base em um protocolo ou página de verificação de integridade específica ao seu aplicativo. 

saudação de exemplo a seguir cria uma investigação TCP. Você também pode criar investigações de HTTP personalizadas para obter verificações de integridade mais refinadas. Ao usar uma investigação personalizada de HTTP, você deve criar página de verificação de integridade hello, tais como *healthcheck.aspx*. investigação de saudação deve retornar um **HTTP 200 Okey** resposta para Olá carga balanceador tookeep Olá host rotação.

toocreate uma investigação de integridade TCP, use [AzureRmLoadBalancerProbeConfig adicionar](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Olá, exemplo a seguir cria um teste de integridade chamado *myHealthProbe* que monitora a cada VM:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Atualizar balanceador de carga Olá com [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Criar uma regra de balanceador de carga
Uma regra de Balanceador de carga é toodefine usado como o tráfego é distribuído toohello VMs. Você definir a configuração de IP front-end Olá para o tráfego de entrada hello e Olá back-end pool tooreceive Olá tráfego IP, juntamente com a origem de saudação necessários e porta de destino. toomake-se de que apenas as VMs íntegras receberem tráfego, você também definir Olá toouse de investigação de integridade.

Crie uma regra de balanceador de carga com [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Olá, exemplo a seguir cria uma regra de Balanceador de carga denominada *myLoadBalancerRule* e saldos de tráfego na porta *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Atualizar balanceador de carga Olá com [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Configurar rede virtual
Antes de implantar algumas máquinas virtuais e testar seu balanceador, crie hello dando suporte a recursos de rede virtual. Para obter mais informações sobre redes virtuais, consulte Olá [gerenciar redes virtuais do Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Criar recursos da rede
Crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Criar uma regra de grupo de segurança de rede com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), em seguida, crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Adicionar sub-rede de toohello de grupo de segurança da rede do hello com [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e, em seguida, atualize a rede virtual Olá com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Olá, exemplo a seguir cria uma regra de grupo de segurança de rede denominada *myNetworkSecurityGroup* e aplica muito*mySubnet*:

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

As NICs virtuais são criadas com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Olá, exemplo a seguir cria três NICs virtuais. (Uma NIC virtual para cada VM que você criou para seu aplicativo no hello seguindo as etapas.) Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-los toohello balanceador de carga:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Criar máquinas virtuais
tooimprove Olá alta disponibilidade do seu aplicativo, colocar suas VMs em um conjunto de disponibilidade.

Crie um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Definir um administrador de nome de usuário e senha para Olá VMs com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Agora você pode criar VMs Olá com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm). saudação de exemplo a seguir cria três VMs:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Ele usa toocreate de alguns minutos e configurar todas as três VMs.

### <a name="install-iis-with-custom-script-extension"></a>Instalar o IIS com a extensão de script personalizado
Um tutorial anterior em [como toocustomize uma máquina virtual Windows](tutorial-automate-vm-deployment.md), você aprendeu como tooautomate personalização de VM com hello extensão para janelas de Script personalizado. Você pode usar o hello mesma abordagem tooinstall e configurar o IIS em suas VMs.

Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado. Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá hostname de saudação VM:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Testar o balanceador de carga
Obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

Você pode inserir o endereço IP público de saudação no navegador da web de tooa. Olá site é exibido, incluindo o nome de host de saudação do hello VM balanceador de carga que Olá distribuído tooas de tráfego em Olá exemplo a seguir:

![Site do IIS em execução](./media/tutorial-load-balancer/running-iis-website.png)

Balanceador de carga toosee Olá distribuir tráfego entre todas as três VMs executando o aplicativo, você pode forçar atualização de seu navegador da web.


## <a name="add-and-remove-vms"></a>Adicionar e remover as VMs
Talvez seja necessário tooperform manutenção Olá VMs que executam seu aplicativo, como ao instalar atualizações do sistema operacional. toodeal com o aumento no tráfego tooyour aplicativo, talvez seja necessário tooadd VMs adicionais. Esta seção mostra como tooremove ou adicionar uma VM do balanceador de carga de saudação.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Remover uma máquina virtual do balanceador de carga Olá
Obter a placa de interface de rede Olá com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), Olá de conjunto, em seguida, *LoadBalancerBackendAddressPools* propriedade Olá NIC virtual muito*$null*. Por fim, atualize o NIC virtual. hello:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Balanceador de carga toosee Olá distribuir o tráfego entre Olá restantes duas VMs que executam seu aplicativo você pode forçar atualização de seu navegador da web. Agora você pode realizar uma manutenção em Olá VM, como instalar atualizações do sistema operacional ou executar uma reinicialização da VM.

### <a name="add-a-vm-toohello-load-balancer"></a>Adicionar um balanceador de carga de toohello VM
Após executar a manutenção VM, ou se você precisar de capacidade de tooexpand, defina Olá *LoadBalancerBackendAddressPools* propriedade Olá virtual NIC toohello *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Obter o balanceador de carga hello:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um balanceador de carga e anexado VMs tooit. Você aprendeu como:

> [!div class="checklist"]
> * Criar um balanceador de carga do Azure
> * Criar uma investigação de integridade do balanceador de carga
> * Criar regras de tráfego para o balanceador de carga
> * Use Olá extensão de Script personalizado toocreate um site IIS básico
> * Criar máquinas virtuais e anexar tooa balanceador de carga
> * Exibir um balanceador de carga em ação
> * Adicionar e remover as VMs de um balanceador de carga

Avançar toohello toolearn de tutorial Avançar como rede de VM toomanage.

> [!div class="nextstepaction"]
> [Gerencie VMs e redes virtuais](./tutorial-virtual-network.md)
