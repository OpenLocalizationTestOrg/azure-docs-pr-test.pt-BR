---
title: "Verifique se o tráfego aaaVerify com fluxo de IP de Inspetor de rede do Azure - REST | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual é permitido ou negado"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifique se o tráfego é permitido ou negado com a verificação de fluxo de IP, um componente do Observador de Rede do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST do Azure](network-watcher-check-ip-flow-verify-rest.md)


Fluxo IP, verifique se é um recurso do observador de rede que permite que você tooverify se o tráfego é permitido tooor de uma máquina virtual. validação de saudação pode ser executada para o tráfego de entrada ou saído. Esse cenário é útil tooget um estado atual do se uma máquina virtual pode se comunicar recursos externos tooan ou back-end. Fluxo IP, verifique se pode ser usado tooverify se suas regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas fluxos que estão sendo bloqueados por regras NSG. Outro motivo para usar IP fluxo Verifique se está tooensure tráfego que deseja bloquear está sendo bloqueado corretamente pelo Olá NSG.

## <a name="before-you-begin"></a>Antes de começar

ARMclient é toocall usado Olá REST API usando o PowerShell. O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

## <a name="scenario"></a>Cenário

Esse cenário usa IP fluxo verificar tooverify se uma máquina virtual pode se comunicar tooanother máquina pela porta 443. Se Olá tráfego é negado, ele retornará regra de segurança de saudação que está negando esse tráfego. toolearn mais sobre o fluxo de IP verificar, visite [fluxo IP verificar a visão geral](network-watcher-ip-flow-verify-overview.md)

Nesse cenário, você irá:

* Recuperar uma máquina virtual
* Chamar a verificação de fluxo de IP
* Verificar os resultados

## <a name="log-in-with-armclient"></a>Fazer logon com o ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperar uma máquina virtual

Execute Olá tooreturn de script a seguir em uma máquina virtual. Olá código a seguir precisa de valores para variáveis de saudação:

* **subscriptionId** -Olá toouse de Id de assinatura.
* **resourceGroupName** - Olá nome de um grupo de recursos que contém máquinas virtuais.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

as informações necessárias Hello são id de saudação em tipo hello `Microsoft.Compute/virtualMachines`. resultados de saudação devem ser semelhante toohello exemplo de código a seguir:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>Chamar a Verificação de fluxo de IP

Olá, exemplo a seguir cria um solicitação tooverify Olá o tráfego para uma máquina virtual especificada. resposta de saudação retorna se Olá tráfego é permitido ou se Olá tráfego é negado. Se o tráfego é negado a que ele também retorna quais blocos de regra Olá tráfego.

> [!NOTE]
> Fluxo IP verificar requer que o recurso VM hello está alocado.

script Hello requer recursos Olá Id de uma máquina virtual e de uma placa de interface de rede na máquina virtual de saudação. Esses valores são fornecidos pelo Olá precede a saída.

> [!Important]
> Para todos os demais de Inspetor de rede chamadas Olá nome do grupo de recursos na solicitação Olá que URI é hello aquele que contém a instância do observador de rede hello, não recursos Olá estiver executando ações de diagnóstico de saudação em.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Entendendo os resultados da saudação

resposta de saudação que voltar informa se o tráfego de saudação é permitido ou negado. resposta de saudação semelhante a um Olá exemplos a seguir:

**Permitido**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**Negado**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>Próximas etapas

Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn mais sobre grupos de segurança de rede.












