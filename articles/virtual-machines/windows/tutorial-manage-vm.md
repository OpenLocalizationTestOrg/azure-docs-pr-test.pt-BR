---
title: "aaaCreate e gerenciar máquinas virtuais do Windows com hello módulo PowerShell do Azure | Microsoft Docs"
description: "Tutorial - criar e gerenciar máquinas virtuais do Windows com hello módulo PowerShell do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Criar e gerenciar máquinas virtuais do Windows com hello módulo PowerShell do Azure

Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível. Este tutorial aborda itens básicos de implantação de máquina virtual do Azure, como a seleção de um tamanho de VM, seleção de uma imagem de VM e implantação de uma VM. Você aprenderá como:

> [!div class="checklist"]
> * Criar e conectar tooa VM
> * Selecionar e usar imagens de VM
> * Exibir e usar tamanhos específicos de VM
> * Redimensionar uma VM
> * Exibir e compreender o estado da VM

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Criar grupo de recursos

Criar um grupo de recursos com hello [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. 

Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. Você deve criar um grupo de recursos antes de criar uma máquina virtual. Neste exemplo, um grupo de recursos denominado *myResourceGroupVM* é criado no hello *EastUS* região. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

grupo de recursos de saudação é especificado ao criar ou modificar uma VM, que pode ser vista em todo este tutorial.

## <a name="create-virtual-machine"></a>Criar máquina virtual

Uma máquina virtual deve ser uma rede virtual tooa conectado. Você se comunicar com a máquina virtual de saudação usando um endereço IP público por meio de uma placa de interface de rede.

### <a name="create-virtual-network"></a>Criar rede virtual

Crie uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Criar um endereço IP público

Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Criar a placa da interface de rede

Crie a placa de interface de rede com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Criar um grupo de segurança de rede

Um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) (NSG) do Azure controla o tráfego de entrada e saída em uma ou mais máquinas virtuais. As regras de grupo de segurança de rede permitem ou negam o tráfego de rede em uma porta específica ou em um intervalo de porta. Essas regras também podem incluir um prefixo do endereço de origem para que somente o tráfego originado em uma fonte predefinida possa se comunicar com uma máquina virtual. tooaccess Olá IIS Web farm que você está instalando, você deve adicionar uma regra de entrada do NSG.

toocreate uma regra de entrada NSG, use [AzureRmNetworkSecurityRuleConfig adicionar](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Olá, exemplo a seguir cria uma regra NSG denominada *myNSGRule* que abre a porta *3389* para a máquina virtual de saudação:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Criar hello NSG usando *myNSGRule* com [AzureRmNetworkSecurityGroup novo](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Adicionar sub-rede de toohello NSG Olá na rede virtual de saudação com [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Rede virtual de saudação de atualização com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Criar máquina virtual

Há várias opções disponíveis ao criar uma máquina virtual, como a imagem do sistema operacional, as credenciais administrativas e o dimensionamento do disco. Neste exemplo, uma máquina virtual é criada com um nome de *myVM* versão mais recente de execução saudação do Datacenter do Windows Server 2016.

Definir Olá nome de usuário e a senha necessários para a conta de administrador de saudação em máquina virtual Olá [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Criar a configuração inicial da máquina virtual de saudação com hello [AzureRmVMConfig novo](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Adicionar sistema operacional Olá informações sobre configuração de máquina virtual toohello com [AzureRmVMOperatingSystem conjunto](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Adicionar configuração da máquina virtual Olá imagem informações toohello com [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Adicionar configurações do hello sistema operacional disco toohello máquina virtual com [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Adicionar Olá placa de rede que você criou anteriormente toohello configuração da máquina virtual com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Criar a máquina virtual Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Conecte-se tooVM

Após a implantação de hello, crie uma conexão de área de trabalho remota com a máquina virtual de saudação.

Execute Olá comandos tooreturn Olá endereço IP público da máquina virtual de saudação a seguir. Anote esse endereço IP para tooit possa se conectar com a conectividade do navegador tootest web em uma etapa futura.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

A seguir Olá Use o comando toocreate uma sessão de área de trabalho remota com a máquina virtual de saudação. Substitua o endereço IP de saudação com hello *publicIPAddress* de sua máquina virtual. Quando solicitado, insira as credenciais de saudação usadas ao criar a máquina virtual de saudação.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>Entender as imagens de VM

Olá marketplace do Azure inclui várias imagens de máquinas virtuais que podem ser usada toocreate uma nova máquina virtual. Nas etapas anteriores do hello, uma máquina virtual foi criada usando a imagem do Windows Server 2016-Datacenter hello. Nesta etapa, o módulo do PowerShell de saudação está marketplace de saudação toosearch usado para outras imagens do Windows, que pode também como base para novas VMs. Esse processo consiste em localizar publicador hello, oferta e nome da imagem hello (Sku). 

Saudação de uso [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) tooreturn comando uma lista de editores de imagem.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Saudação de uso [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn uma lista de ofertas de imagem. Com este comando, Olá retornado lista é filtrada no publicador especificado hello. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Olá [AzureRmVMImageSku Get](/powershell/module/azurerm.compute/get-azurermvmimagesku) comando, em seguida, filtrará Olá tooreturn de nome de publicador e oferecem uma lista de nomes de imagem.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Essas informações podem ser usada toodeploy uma VM com uma imagem específica. Este exemplo define o nome da imagem Olá no objeto da VM hello. Consulte os exemplos anteriores toohello neste tutorial para etapas de implantação completa.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>Entender os tamanhos de VM

Um tamanho de máquina virtual determina a quantidade de saudação de recursos de computação, como memória, CPU e GPU que são feitas a máquina virtual de toohello disponíveis. Máquinas virtuais precisam toobe criado com um tamanho apropriado para Olá espera que a carga de trabalho. Se a carga de trabalho aumentar, uma máquina virtual existente pode ser redimensionada.

### <a name="vm-sizes"></a>Tamanhos de VM

Olá, a tabela a seguir categoriza tamanhos em casos de uso.  

| Tipo                     | Tamanhos           |    Descrição       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Propósito geral         |DSv2, Dv2, DS, D, Av2, A0-7| CPU/memória equilibrados. Ideal para desenvolvimento / teste e pequenas toomedium soluções de aplicativos e dados.  |
| Otimizado para computação      | Fs, F             | Relação de CPU/memória alta. Boa para aplicativos de tráfego médio, dispositivos de rede e processos em lote.        |
| Otimizado para memória       | GS, G, DSv2, DS, Dv2, D   | Relação de memória/núcleo alta. Excelente para bancos de dados relacionais, caches toolarge médios e análise de memória.                 |
| Otimizado para armazenamento       | Ls                | Alta taxa de transferência de disco e de E/S. Ideal para Big Data, SQL e bancos de dados NoSQL.                                                         |
| GPU           | NV, NC            | VMs especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.       |
| Alto desempenho | H, A8-11          | Nossas VMs de CPU mais potentes com adaptadores de rede de alto rendimento (RDMA) opcionais. 


### <a name="find-available-vm-sizes"></a>Encontrar tamanhos de VM disponíveis

toosee uma lista de VM tamanhos disponíveis em uma determinada região, use Olá [AzureRmVMSize Get](/powershell/module/azurerm.compute/get-azurermvmsize) comando.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>Redimensionar uma VM

Depois que uma máquina virtual foi implantada, pode ser redimensionada tooincrease ou diminuir a alocação de recursos.

Antes de redimensionar uma VM, verifique se hello tamanho desejado está disponível no cluster da VM atual hello. Olá [AzureRmVMSize Get](/powershell/module/azurerm.compute/get-azurermvmsize) comando retorna uma lista de tamanhos. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Se Olá desejado tamanho estiver disponível, hello VM pode ser redimensionada de um estado ligado, mas ele é reinicializado durante a operação de saudação.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Se o tamanho desejado de saudação não está em cluster atual hello, Olá VM necessidades toobe desalocada antes da operação de redimensionamento Olá pode ocorrer. Observe que, quando Olá VM está ligada novamente, os dados no disco temporário Olá são removidos e endereço IP público de saudação alterar, a menos que um endereço IP estático está sendo usado. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>Estados de energia da VM

Uma VM do Azure pode ter um dentre vários estados de energia. Nesse estado representa o estado atual de saudação do hello VM do ponto de vista de saudação do hipervisor Olá. 

### <a name="power-states"></a>Estados de energia

| Estado de energia | Descrição
|----|----|
| Iniciando | Indica a máquina virtual de hello está sendo iniciada. |
| Executando | Indica que a máquina virtual hello está em execução. |
| Parando | Indica que a máquina virtual hello está sendo interrompida. | 
| Parada | Indica que a máquina virtual hello está parada. Observe que máquinas virtuais no estado interrompido de saudação ainda incorrerá em encargos de computação.  |
| Desalocando | Indica que a máquina virtual hello está sendo desalocada. |
| Desalocada | Indica que a máquina virtual Olá foi completamente removida do hipervisor Olá mas ainda estará disponível no plano de controle de saudação. Máquinas virtuais no estado desalocada da saudação não incorrerá em encargos de computação. |
| - | Indica que o estado de energia de saudação da máquina virtual de saudação é desconhecido. |

### <a name="find-power-state"></a>Localizar o estado de energia

estado de saudação tooretrieve de uma VM específica, use Olá [AzureRmVM Get](/powershell/module/azurerm.compute/get-azurermvm) comando. Ser toospecify se um nome válido para uma máquina virtual e o grupo de recursos. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Saída:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Tarefas de gerenciamento

Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual. Além disso, talvez você queira toocreate scripts tooautomate repetitivas ou complexas tarefas. Usando o Azure PowerShell, muitas tarefas comuns de gerenciamento podem ser executadas da linha de comando hello, ou em scripts.

### <a name="stop-virtual-machine"></a>Como interromper uma máquina virtual

Pare e desaloque uma máquina virtual com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Se você quiser tookeep Olá VM em um estado de provisionamento, use o parâmetro de - StayProvisioned de saudação.

### <a name="start-virtual-machine"></a>Como iniciar uma máquina virtual

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Excluir grupo de recursos

Excluir um grupo de recursos exclui todos os recursos contidos nele.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre a criação e o gerenciamento básico de VM e como:

> [!div class="checklist"]
> * Criar e conectar tooa VM
> * Selecionar e usar imagens de VM
> * Exibir e usar tamanhos específicos de VM
> * Redimensionar uma VM
> * Exibir e compreender o estado da VM

Avançar toohello toolearn próximo de tutorial sobre discos de VM.  

> [!div class="nextstepaction"]
> [Criar e gerenciar discos de VM](./tutorial-manage-data-disk.md)
