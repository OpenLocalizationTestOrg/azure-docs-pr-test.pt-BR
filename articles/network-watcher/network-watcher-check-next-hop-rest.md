---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - REST | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e endereço ip usando próximo salto Olá API REST do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Descobrir que tipo de próximo salto hello está usando o recurso de próximo salto Olá no Aure observador de rede usando a API REST do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST do Azure](network-watcher-check-next-hop-rest.md)

Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada. Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.

## <a name="before-you-begin"></a>Antes de começar

ARMclient é toocall usado Olá REST API usando o PowerShell. O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo usa um recurso do observador de rede que localiza o tipo de próximo salto hello e endereço IP para um recurso de próximo salto. toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).

Neste cenário, você:

* Recupere o próximo salto Olá para uma máquina virtual.

## <a name="log-in-with-armclient"></a>Fazer logon com o ARMClient

Faça logon no tooarmclient com suas credenciais do Azure.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperar uma máquina virtual

Execute Olá tooreturn de script a seguir em uma máquina virtual. Essas informações são necessárias para a execução do próximo salto.

saudação de código a seguir precisa de valores para Olá variáveis a seguir:

- **subscriptionId** -Olá toouse de Id de assinatura.
- **resourceGroupName** - Olá nome de um grupo de recursos que contém máquinas virtuais.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

De saída a seguir hello, id de saudação da máquina virtual de saudação é usado em Olá exemplo a seguir:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Obter o próximo salto

Depois de criar o cabeçalho de autorização hello, próximo salto saudação de uma máquina virtual pode ser recuperado. Olá valores a seguir devem ser substituídos para Olá toowork de exemplo de código.

> [!Important]
> Para a API de REST do Inspetor de rede chamadas Olá nome do grupo de recursos na solicitação Olá que URI é o grupo de recursos de saudação que contém Olá observador de rede, não os recursos de saudação estiver executando ações de diagnóstico Olá em.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Próximo salto requer que o recurso VM hello está alocado toorun.

## <a name="results"></a>Resultados

Olá trecho a seguir é um exemplo de saída de hello recebida. resultados de saudação contêm Olá valores a seguir:

* **nextHopType** -esse valor é um Olá valores a seguir: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway ou None.
* **nextHopIpAddress** -Olá o endereço IP do próximo salto de saudação.
* **routeTableId** - valor hello ou um uri para tabela de rota de saudação associada à rota hello, ou se não definida pelo usuário rota está valor definido Olá *sistema rota* é retornado.

Olá seguem resultados Olá no formato json.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Próximas etapas

Depois de ter sido capaz de toofind-out de próximo salto Olá para uma máquina virtual, você pode exibir segurança Olá dos recursos da rede visitando [visão geral do modo de segurança](network-watcher-security-group-view-overview.md)














