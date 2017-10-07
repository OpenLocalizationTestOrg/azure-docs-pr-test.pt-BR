---
title: "tráfego de aaaVerify com Azure rede Inspetor IP fluxo verificar - CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual é permitido ou negado usando a CLI do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifique se o tráfego é permitido ou negado tooor de uma VM com IP fluxo verificar um componente do observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST do Azure](network-watcher-check-ip-flow-verify-rest.md)


Fluxo de IP Verifique se é um recurso do observador de rede que permite que você tooverify se o tráfego é permitido tooor de uma máquina virtual. Esse cenário é útil tooget um estado atual do se uma máquina virtual pode se comunicar recursos externos tooan ou back-end. Fluxo IP, verifique se pode ser usado tooverify se suas regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas fluxos que estão sendo bloqueados por regras NSG. Outro motivo para usar IP fluxo Verifique se está tooensure tráfego que deseja bloquear está sendo bloqueado corretamente pelo Olá NSG.

Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede. cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.

## <a name="scenario"></a>Cenário

Esse cenário usa tooverify IP fluxo verificar se uma máquina virtual pode se comunicar tooa conhecido endereço IP do Bing. Se Olá tráfego é negado, ele retornará regra de segurança de saudação que está negando esse tráfego. toolearn mais sobre IP fluxo verificar, visite [fluxo verificar a visão geral de IP](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>Obter uma VM

Fluxo IP verificar tooor de tráfego de testes de um endereço IP no tooor máquina virtual de um destino remoto. Uma Id de uma máquina virtual é necessária para o cmdlet hello. Se você já souber a ID de saudação do hello toouse de máquina virtual, você pode ignorar esta etapa.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>Obter Olá NICS

endereço IP de saudação de uma NIC na máquina virtual de saudação é necessária neste exemplo recuperamos Olá NICs em uma máquina virtual. Se você já souber Olá IP endereço que você deseja tootest na máquina virtual de saudação, você pode ignorar esta etapa.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Executar a verificação de fluxo de IP

Agora que temos informações Olá necessário toorun Olá cmdlet, executamos Olá `network watcher ip-flow-verify` tráfego de saudação do cmdlet tootest. Neste exemplo, estamos usando endereço IP primeiro Olá em Olá primeira NIC.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> Fluxo de IP verificar requer que o recurso VM hello está alocado toorun.

## <a name="review-results"></a>Analisar Resultados

Depois de executar `network watcher ip-flow-verify` Olá resultados são retornados, hello, exemplo a seguir é resultados Olá de saudação anterior da etapa.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Próximas etapas

Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que são definidas.

Saiba tooaudit suas configurações NSG visitando [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
