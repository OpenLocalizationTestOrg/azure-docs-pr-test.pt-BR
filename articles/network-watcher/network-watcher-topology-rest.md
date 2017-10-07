---
title: topologia do observador de rede do Azure aaaView - API REST | Microsoft Docs
description: Este artigo descreve como toouse REST API tooquery a topologia de rede.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Exibir a topologia do Observador de rede com a API REST

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [API REST](network-watcher-topology-rest.md)

recurso de topologia de saudação do observador de rede fornece uma representação visual dos recursos de rede de saudação em uma assinatura. No portal de hello, essa visualização é apresentada tooyou automaticamente. informações de Olá por trás de exibição de topologia Olá no portal de saudação podem ser recuperadas por meio do PowerShell.
Esse recurso cria informações de topologia hello mais versátil como Olá dados podem ser consumidos por outros toobuild ferramentas out visualização hello.

interconexão de saudação é modelada em duas relações.

- **Confinamento** - exemplo: a VNet contém uma sub-rede que contém uma NIC
- **Associados** - exemplo: a NIC está associada a uma VM

Olá lista a seguir é propriedades que são retornadas ao consultar Olá API de REST de topologia.

* **nome** - Olá nome do recurso de saudação
* **ID** -Olá uri do recurso de saudação.
* **local** -Olá localização onde o recurso de saudação.
* **associações** -uma lista de associações toohello Referência de objeto.
    * **nome** -nome de saudação do hello referenciado recursos.
    * **resourceId** -Olá resourceId é o uri de saudação do recurso Olá referenciado na associação de saudação.
    * **associationType** -relação Olá entre o objeto do hello filho e pai Olá faz referência a esse valor. Os valores válidos são **Contém** ou **Associado**.

## <a name="before-you-begin"></a>Antes de começar

Neste cenário, para recuperar informações de topologia de saudação. ARMclient é toocall usado Olá REST API usando o PowerShell. O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo recupera a resposta de topologia de saudação um determinado grupo de recursos.

## <a name="log-in-with-armclient"></a>Fazer logon com o ARMClient

Faça logon no tooarmclient com suas credenciais do Azure.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Como recuperar a topologia

saudação de exemplo a seguir solicita topologia Olá Olá API REST.  exemplo Hello é parametrizada tooallow flexibilidade na criação de um exemplo.  Substitua todos os valores por \< \> ao redor deles.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

saudação de resposta a seguir está um exemplo de uma resposta reduzido que é retornado quando recuperar a topologia para um grupo de recursos:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Próximas etapas

Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

