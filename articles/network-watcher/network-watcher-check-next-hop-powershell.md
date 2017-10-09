---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - PowerShell | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e usando o endereço ip do próximo salto usando o PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Descobrir que tipo de próximo salto Olá está usando o recurso de próximo salto Olá no Inspetor de rede do Azure usando o PowerShell

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST do Azure](network-watcher-check-next-hop-rest.md)

Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada. Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.

## <a name="before-you-begin"></a>Antes de começar

Nesse cenário, você usará a saudação tipo toofind portal do Azure Olá de próximo salto e o endereço IP.

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede. cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo usa um recurso do observador de rede que localiza o tipo de próximo salto hello e endereço IP para um recurso de próximo salto. toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Recuperar o Observador de Rede

Olá primeira etapa é a instância do tooretrieve Olá observador de rede. Olá `$networkWatcher` variável é passada toohello próximo salto verificar cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Obter uma máquina virtual

Próximo salto retorna o próximo salto de saudação e endereço IP de saudação do próximo salto de saudação de uma máquina virtual. Uma Id de uma máquina virtual é necessária para o cmdlet hello. Se você já souber a ID de saudação do hello toouse de máquina virtual, você pode ignorar esta etapa.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Próximo salto requer que o recurso VM hello está alocado toorun.

## <a name="get-hello-network-interfaces"></a>Obter interfaces de rede Olá

endereço IP de saudação de uma NIC na máquina virtual de saudação é necessária neste exemplo recuperamos Olá NICs em uma máquina virtual. Se você já souber Olá IP endereço que você deseja tootest na máquina virtual de saudação, você pode ignorar esta etapa.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Obter o próximo salto

Agora podemos chamar hello `Get-AzureRmNetworkWatcherNextHop` cmdlet. Podemos passar Olá cmdlet Olá observador de rede, a máquina virtual Id, endereço IP e endereço IP de destino de origem. Neste exemplo, o endereço IP de destino Olá é tooa VM em outra rede virtual. Há um gateway de rede virtual entre duas redes virtuais de saudação.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Analisar resultados

Ao concluir, resultados de saudação são fornecidos. Olá próximo endereço IP será retornado, bem como o tipo de saudação do recurso é. Nesse cenário, é endereço IP público de saudação do gateway de rede virtual hello.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

Hello lista a seguir mostra valores de NextHopType disponíveis no momento da saudação:

**Tipo do próximo salto**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Nenhum

## <a name="next-steps"></a>Próximas etapas

Saiba como tooreview as configurações de grupo de segurança de rede por meio de programação visitando [NSG auditoria com o observador de rede](network-watcher-nsg-auditing-powershell.md)

















