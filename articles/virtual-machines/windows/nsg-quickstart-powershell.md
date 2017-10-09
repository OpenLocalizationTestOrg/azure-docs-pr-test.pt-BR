---
title: aaaOpen portas tooa VM usando o PowerShell do Azure | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Windows usando o modo de implantação do Gerenciador de recursos do Azure hello e do PowerShell do Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>Como tooopen tooa portas e os pontos de extremidade de VM no Azure usando o PowerShell
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandos rápidos
Grupo de segurança de rede toocreate e precisar de regras de ACL [versão mais recente de saudação do Azure PowerShell instalado](/powershell/azureps-cmdlets-docs). Você também pode [executar essas etapas usando o portal do Azure de saudação](nsg-quickstart-portal.md).

Faça logon no tooyour conta do Azure:

```powershell
Login-AzureRmAccount
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.

Crie uma regra com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRule* tooallow *tcp* o tráfego na porta *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

Em seguida, crie o grupo de segurança de rede com [AzureRmNetworkSecurityGroup novo](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e atribuir Olá HTTP regra recém-criada da seguinte maneira. Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Agora vamos atribuir a sub-rede de tooa do grupo de segurança de rede. Olá, exemplo a seguir atribui uma rede virtual existente chamada *myVnet* toohello variável *$vnet* com [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Associe seu Grupo de Segurança de Rede à sub-rede com [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig). Olá, exemplo a seguir associa sub-rede Olá denominada *mySubnet* com seu grupo de segurança de rede:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Por fim, atualize sua rede virtual com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork) para que o efeito de tootake alterações:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Mais informações sobre os Grupos de Segurança de Rede
Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM. Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso. Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](tutorial-virtual-network.md#manage-internal-traffic).

Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure. Balanceador de carga Olá distribui tráfego tooVMs, com um grupo de segurança de rede que fornece filtragem. Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas no Azure toocreate um aplicativo altamente disponível](tutorial-load-balancer.md).

## <a name="next-steps"></a>Próximas etapas
Neste exemplo, você criou um tráfego HTTP de tooallow regra simples. Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:

* [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [O que é um NSG (grupo de segurança de rede)?](../../virtual-network/virtual-networks-nsg.md)
* [Visão Geral do Azure Resource Manager para Balanceadores de Carga](../../load-balancer/load-balancer-arm.md)

