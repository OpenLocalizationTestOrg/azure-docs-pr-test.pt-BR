---
title: "aaaTutorial - compilação de um aplicativo altamente disponível em VMs do Azure | Microsoft Docs"
description: "Saiba como toocreate um aplicativo altamente disponível e seguro entre três máquinas virtuais do Windows com um balanceador de carga no Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Criar um aplicativo altamente disponível com balanceamento de carga em máquinas virtuais Windows no Azure

Neste tutorial, você deve criar um aplicativo altamente disponível está eventos toomaintenance resiliente. aplicativo Hello usa três máquinas virtuais do Windows (VMs) de um balanceador de carga e um conjunto de disponibilidade. Este tutorial instala o IIS, que você pode usar este tutorial toodeploy uma estrutura de aplicativo diferente usando Olá diretrizes e os mesmos componentes de alta disponibilidade. 

## <a name="step-1---azure-prerequisites"></a>Etapa 1: pré-requisitos do Azure

toocomplete neste tutorial, certifique-se de que você instalou hello mais recente [Azure PowerShell](/powershell/azure/overview) módulo.

Primeiro, login tooyour assinatura do Azure com hello comando AzureRmAccount de logon e siga a saudação na tela instruções.

```powershell
Login-AzureRmAccount
```

Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. Antes de criar todos os outros recursos do Azure, você precisa toocreate um grupo de recursos com [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` região: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Etapa 2: criar conjunto de disponibilidade

As máquinas virtuais podem ser criadas em domínios lógicos de falhas e de atualização. Cada domínio lógico representa uma parte do hardware no data center do Azure subjacente hello. Quando você cria duas ou mais VMs, seus recursos de computação e armazenamento são distribuídos entre esses domínios. Essa distribuição mantém a disponibilidade de saudação do seu aplicativo se precisar de um componente de hardware de manutenção. Os conjuntos de disponibilidade permitem que você defina esses domínios lógicos de falha e de atualização.

Crie um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Etapa 3: criar um balanceador de carga

Um Azure Load Balancer distribui o tráfego entre um conjunto de VMs definidas usando regras de balanceador de carga. Um teste de integridade monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.

### <a name="create-public-ip-address"></a>Criar um endereço IP público

tooaccess seu aplicativo em Olá Internet, atribua um balanceador de carga do toohello de endereço IP público. Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Olá, exemplo a seguir cria um endereço IP público denominado `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Criar um balanceador de carga

Crie um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Olá, exemplo a seguir cria um endereço IP de front-end denominado `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Crie um pool de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Olá, exemplo a seguir cria um pool de endereços de back-end denominado `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Agora, crie o balanceador de carga Olá com [AzureRmLoadBalancer novo](/powershell/module/azurerm.network/new-azurermloadbalancer). Olá, exemplo a seguir cria um balanceador de carga denominado `myLoadBalancer` usando Olá `myPublicIP` endereço:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Criar uma investigação de integridade

tooallow Olá balanceador toomonitor Olá status de carga do seu aplicativo, você usar uma investigação de integridade. investigação de integridade Olá dinamicamente adiciona ou remove as VMs de rotação do balanceador de carga de saudação com base em suas verificações de toohealth de resposta. Por padrão, uma máquina virtual é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundos.

Crie uma investigação de integridade com [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Olá, exemplo a seguir cria um teste de integridade chamado `myHealthProbe` que monitora a cada VM:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Criar uma regra para o balanceador de carga

Uma regra de Balanceador de carga é toodefine usado como o tráfego é distribuído toohello VMs.

Crie uma regra de balanceador de carga com [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Olá, exemplo a seguir cria uma regra de Balanceador de carga denominada `myLoadBalancerRule` e saldos de tráfego na porta `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Atualizar balanceador de carga Olá com [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Etapa 4: configurar a rede

Cada VM tem um ou mais virtual placas de rede (NICs) que se conectam a rede virtual tooa. Esta rede virtual está protegida toofilter tráfego com base nas regras de acesso definidas.

### <a name="create-virtual-network"></a>Criar rede virtual

Primeiro, configure uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Olá, exemplo a seguir cria uma sub-rede denominada `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooyour de conectividade de rede tooprovide VMs, crie uma rede virtual com [AzureRmVirtualNetwork novo](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Olá, exemplo a seguir cria uma rede virtual denominada `myVnet` com `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Configurar a segurança de rede

Um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) (NSG) do Azure controla o tráfego de entrada e saída em uma ou mais máquinas virtuais. As regras de grupo de segurança de rede permitem ou negam o tráfego de rede em uma porta específica ou em um intervalo de porta. Essas regras também podem incluir um prefixo do endereço de origem para que somente o tráfego originado em uma fonte predefinida possa se comunicar com uma máquina virtual.

tooallow web tooreach de tráfego em seu aplicativo, crie uma regra de grupo de segurança de rede com [AzureRmNetworkSecurityRuleConfig novo](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Olá, exemplo a seguir cria uma regra de grupo de segurança de rede denominada `myNetworkSecurityGroupRule`:

```powershell
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
```

Crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Olá, exemplo a seguir cria um NSG denominado `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Adicionar sub-rede de toohello de grupo de segurança da rede do hello com [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Rede virtual de saudação de atualização com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Criar placas de interface de rede virtual

Carregar a função balanceadores com recurso NIC virtual Olá em vez de Olá VM real. Olá NIC virtual é conectada toohello balanceador de carga e, em seguida, anexado tooa VM.

Crie uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Olá, exemplo a seguir cria três NICs virtuais. (Uma NIC virtual para cada VM você criar para seu aplicativo no hello seguindo as etapas):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Etapa 5 – Criar máquinas virtuais

Com hello todos os componentes no lugar de base, agora você pode criar seu aplicativo de toorun de máquinas virtuais altamente disponível. 

Obter Olá nome de usuário e a senha necessários para a conta de administrador de saudação em máquina virtual Olá [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Criar VMs Olá com [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [conjunto AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage conjunto](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface adicionar](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), e [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm). saudação de exemplo a seguir cria três VMs:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Ele usa várias toocreate de minutos e configurar todas as três VMs. Olá investigação de integridade do balanceador de carga detecta automaticamente quando o aplicativo hello está em execução em cada VM. Depois que o aplicativo hello está em execução, regra de Balanceador de carga Olá inicia toodistribute tráfego.

### <a name="install-hello-app"></a>Instalar o aplicativo hello 

Extensões de máquina virtual do Azure são tarefas de configuração de máquina virtual tooautomate usado como instalar aplicativos e configurar o sistema operacional de saudação. Olá [extensão do script personalizado para o Windows](./../virtual-machines-windows-extensions-customscript.md) é toorun usada em qualquer script do PowerShell na máquina virtual de saudação. script Hello pode ser armazenado no armazenamento do Azure, qualquer ponto de extremidade HTTP acessível, ou na configuração de extensão do script personalizado hello. Ao usar a extensão do script personalizado Olá, o agente de VM do Azure Olá gerencia a execução do script hello.

Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) extensão do script personalizado Olá tooinstall. Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá IIS webserver:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Testar seu aplicativo

Obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá, exemplo a seguir obtém endereço IP hello `myPublicIP` criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Insira o endereço IP público de saudação no navegador da web de tooa. Com a regra NSG Olá em vigor, site padrão do IIS Olá é exibida. 

![Site do IIS padrão](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Etapa 6 – Tarefas de gerenciamento

Talvez seja necessário tooperform manutenção Olá VMs que executam seu aplicativo, como ao instalar atualizações do sistema operacional. toodeal com o aumento no tráfego tooyour aplicativo, talvez seja necessário tooadd VMs adicionais. Esta seção mostra como tooremove ou adicionar uma VM do balanceador de carga de saudação. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Remover uma máquina virtual do balanceador de carga Olá

Remova uma máquina virtual do pool de endereços de back-end Olá redefinindo a propriedade de LoadBalancerBackendAddressPools Olá da placa de interface de rede de saudação.

Obter a placa de interface de rede Olá com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Defina a propriedade de LoadBalancerBackendAddressPools de saudação da placa de interface de rede Olá muito null$:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Placa de interface de rede de saudação de atualização:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Adicionar um balanceador de carga de toohello VM

Depois de executar a manutenção VM, ou se você precisar de capacidade de tooexpand, adicionando Olá NIC de um pool de endereços de back-end do VM toohello saudação do balanceador de carga.

Obter o balanceador de carga hello:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Adicione pool de endereços de back-end de saudação da placa de interface de rede de toohello de Balanceador de carga de saudação:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Placa de interface de rede de saudação de atualização:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Próximas etapas

Amostras – [Scripts de exemplo do PowerShell na Máquina Virtual do Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
