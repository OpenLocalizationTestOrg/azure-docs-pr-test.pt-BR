---
title: "conjunto de escala de uma máquina virtual do Azure aaaCreate | Microsoft Docs"
description: "Crie e implante um conjunto de dimensionamento de máquinas virtuais Linux ou Windows do Azure com a CLI do Azure, o PowerShell, um modelo ou o Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Criar e implantar um conjunto de dimensionamento de máquinas virtuais
Conjuntos de escala de máquinas virtuais tornam mais fácil para você toodeploy e gerenciam máquinas virtuais idênticas como um conjunto. Os conjuntos de dimensionamento fornecem uma camada de computação altamente escalonável e personalizável para aplicativos de hiperescala e suporte a imagens da plataforma Windows, imagens da plataforma Linux, imagens personalizadas e extensões. Para obter mais informações sobre conjuntos de dimensionamento, consulte [Conjuntos de dimensionamento de máquinas virtuais](virtual-machine-scale-sets-overview.md).

Este tutorial mostra como toocreate uma escala de máquina virtual configurada **sem** usando Olá portal do Azure. Para obter informações sobre como toouse Olá portal do Azure, consulte [como toocreate uma escala de máquina virtual definido com hello portal do Azure](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Para saber mais sobre os recursos do Azure Resource Manager, confira [Azure Resource Manager vs. Implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>Entrar tooAzure

Se você estiver usando uma escala de toocreate 2.0 do CLI do Azure ou o Azure PowerShell definida, é necessário primeiro toosign tooyour assinatura.

Para obter mais informações sobre como tooinstall, configurar e entre em tooAzure com CLI do Azure ou o PowerShell, consulte [guia de Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) ou [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

É necessário primeiro toocreate um grupo de recursos que o conjunto de escala de máquina virtual hello está associado.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Criar com a CLI do Azure

Com a CLI do Azure, você pode criar um conjunto de dimensionamento de máquinas virtuais com esforço mínimo. Se você omitir valores padrão, eles serão fornecidos para você. Por exemplo, se você não especificar as informações de rede virtual, uma rede virtual será criada para você. Se você omitir Olá partes a seguir, são criadas para você: 
- Um balanceador de carga
- Uma rede virtual
- Um endereço IP público

Ao escolher hello imagem da máquina virtual que você deseja toouse no conjunto de escalas da máquina virtual hello, você tem algumas opções:

- URN  
Identificador de saudação de um recurso:  
**Win2012R2Datacenter**

- Alias do URN  
nome amigável de saudação de um URN:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- ID de recurso personalizado  
Olá caminho tooan recursos do Azure:  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- Recurso da Web  
Olá caminho tooan URI HTTP:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>Você pode encontrar a lista de imagens disponíveis com `az vm image list`.

toocreate definido de uma escala de máquina virtual, você deve especificar o seguinte hello:

- Grupo de recursos 
- Nome
- Imagem do sistema operacional
- Informações de autenticação 
 
saudação de exemplo a seguir cria um conjunto de escala básica da máquina virtual (esta etapa pode levar alguns minutos).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Depois que o comando Olá é concluído, você terá a escala de máquina virtual definido criado. Endereço IP de saudação tooget da máquina virtual de saudação talvez seja necessário para que você possa conectar tooit. Você pode obter muitas informações diferentes sobre a máquina virtual de saudação (incluindo o endereço IP de saudação) com hello comando a seguir. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Criar com o PowerShell

O PowerShell é mais complicado toouse de CLI do Azure. Enquanto a CLI do Azure fornece padrões para recursos relacionados à rede (balanceadores de carga, endereços IP e redes virtuais), isso não ocorre com o PowerShell. Referenciar uma imagem com o PowerShell também é um pouco mais complicado. Você pode obter imagens com hello cmdlets a seguir:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

Olá cmdlets trabalho pode ser usado na sequência. Aqui está um exemplo de como tooget todas as imagens para Olá **Oeste dos EUA 2** região com um publicador que tem o nome da saudação **microsoft** nele.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

fluxo de trabalho Olá para a criação de um conjunto de escala de máquina virtual é o seguinte:

1. Crie um objeto de configuração que contém informações sobre o conjunto de escala hello.
2. Imagem de sistema operacional base Olá de referência.
3. Definir as configurações do sistema operacional Olá: autenticação, o prefixo do nome VM e o usuário/senha.
4. Configurar a rede.
5. Crie conjunto de escala de saudação.

Este exemplo cria um conjunto de dimensionamento básico de duas instâncias para um computador com o Windows Server 2016 instalado.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Usar uma imagem de máquina virtual personalizada
Se você estiver criando uma escala de conjunto de sua própria imagem personalizada, em vez de fazer referência a uma imagem de máquina virtual da Galeria hello, Olá _AzureRmVmssStorageProfile conjunto_ comando teria esta aparência:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Criar usando um modelo

Você pode implantar um conjunto de dimensionamento de máquinas virtuais usando um modelo do Azure Resource Manager. Você pode criar seu próprio modelo ou usar um de saudação [repositório de modelos](https://azure.microsoft.com/resources/templates/?term=vmss). Esses modelos podem ser implantados diretamente tooyour assinatura do Azure.

>[!NOTE]
>toocreate seu próprio modelo, você cria um arquivo de texto JSON. Para obter informações gerais sobre como toocreate e personalizar um modelo, consulte [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Um modelo de exemplo está disponível [no GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Para obter mais informações sobre como toocreate e usar esse exemplo, consulte [conjunto de escala viável mínimo](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Criar com o Visual Studio

Com o Visual Studio, você pode criar um projeto do grupo de recursos do Azure e adicionar que modelo tooit do conjunto de uma escala de máquina virtual. Você pode escolher se deseja tooimport do GitHub ou hello Galeria de aplicativos Web do Azure. Um script de implantação do PowerShell também é gerado para você. Para obter mais informações, consulte [como toocreate uma escala de máquina virtual definido com o Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Criar a partir de saudação portal do Azure

Olá portal do Azure fornece uma maneira conveniente tooquickly criar um conjunto de escala. Para obter mais informações, consulte [como toocreate uma escala de máquina virtual definido com hello portal do Azure](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [discos de dados](virtual-machine-scale-sets-attached-disks.md).

Saiba como muito[gerenciar seus aplicativos](virtual-machine-scale-sets-deploy-app.md).
