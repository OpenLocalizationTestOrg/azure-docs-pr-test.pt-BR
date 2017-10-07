---
title: "políticas de aaaAzure de recursos para recursos de rede | Microsoft Docs"
description: "Descreve as políticas do Gerenciador de recursos do Azure para gerenciar a implantação de saudação de recursos de rede."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a>Aplicar recurso políticas toonetwork recursos
Este artigo mostra um exemplo [diretiva recursos](resource-manager-policy.md) você pode aplicar tooAzure gateways de rede virtual. Essa política garante a consistência dos gateways implantados em sua organização. 

## <a name="define-permitted-virtual-network-gateway-sku"></a>Definir o SKU do gateway de rede virtual permitido

Olá após diretiva restringe quais SKUs podem ser implantados para gateways de rede virtual:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Próximas etapas
* Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo. escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso. políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md). 
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

