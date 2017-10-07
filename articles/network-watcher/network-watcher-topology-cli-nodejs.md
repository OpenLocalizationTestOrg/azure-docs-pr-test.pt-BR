---
title: topologia do observador de rede do Azure aaaView - 1.0 da CLI do Azure | Microsoft Docs
description: Este artigo descreve como tooquery toouse 1.0 da CLI do Azure a topologia de rede.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a>Como exibir a topologia do Observador de rede com a CLI 1.0 do Azure

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [API REST](network-watcher-topology-rest.md)

recurso de topologia de saudação do observador de rede fornece uma representação visual dos recursos de rede de saudação em uma assinatura. No portal de hello, essa visualização é apresentada tooyou automaticamente. informações de Olá por trás de exibição de topologia Olá no portal de saudação podem ser recuperadas por meio do PowerShell.
Esse recurso cria informações de topologia hello mais versátil como Olá dados podem ser consumidos por outros toobuild ferramentas out visualização hello.

Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux. 

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

Nesse cenário, você usa Olá `network watcher topology` informações de topologia do cmdlet tooretrieve hello. Também há um artigo sobre como muito[recuperar a topologia de rede com a API REST](network-watcher-topology-rest.md).

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo recupera a resposta de topologia de saudação um determinado grupo de recursos.

## <a name="retrieve-topology"></a>Como recuperar a topologia

Olá `network watcher topology` cmdlet recupera a topologia de saudação um determinado grupo de recursos. Adicione o argumento hello "– json" tooview Olá oput no formato json

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Resultados

Olá resultados retornados tem uma propriedade de nome "recursos", que contém o corpo da resposta json Olá para Olá `network watcher topology` cmdlet.  resposta de saudação contém recursos Olá Olá grupo de segurança de rede e suas associações (ou seja, Contains, associado).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as regras de segurança de saudação que são recursos de rede aplicada tooyour visitando [visão geral de exibição de grupo de segurança](network-watcher-security-group-view-overview.md)
