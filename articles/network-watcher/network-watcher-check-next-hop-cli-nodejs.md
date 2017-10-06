---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - 1.0 da CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e usando o endereço ip do próximo salto usando a CLI do Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a>Descobrir que tipo de próximo salto Olá está usando o recurso de próximo salto Olá no Inspetor de rede do Azure usando o Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST do Azure](network-watcher-check-next-hop-rest.md)

Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada. Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.

Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.

## <a name="before-you-begin"></a>Antes de começar

Nesse cenário, você usará hello tipo de próximo salto do CLI do Azure toofind hello e endereço IP.

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede. cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo usa um recurso do observador de rede que localiza o tipo de próximo salto hello e endereço IP para um recurso de próximo salto. toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Obter o próximo salto

tooget Olá próximo salto chamamos Olá `azure netowrk watcher next-hop` cmdlet. Passamos o grupo de recursos do hello cmdlet Olá observador de rede, Olá NetworkWatcher, a máquina virtual Id, endereço IP de origem e endereço IP de destino. Neste exemplo, o endereço IP de destino Olá é tooa VM em outra rede virtual. Há um gateway de rede virtual entre duas redes virtuais de saudação. 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
Se Olá VM tiver várias NICs e encaminhamento de IP está habilitado em qualquer um dos Olá NICs, Olá, em seguida, o parâmetro NIC (-i nic id) deve ser especificado. Caso contrário, será opcional.

## <a name="review-results"></a>Analisar resultados

Ao concluir, resultados de saudação são fornecidos. Olá próximo endereço IP será retornado, bem como o tipo de saudação do recurso é.

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
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
