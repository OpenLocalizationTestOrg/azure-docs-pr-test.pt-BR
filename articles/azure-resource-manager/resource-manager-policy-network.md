---
title: "Políticas de recursos do Azure para recursos de rede | Microsoft Docs"
description: "Descreve as políticas do Azure Resource Manager para gerenciar a implantação de recursos de rede."
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
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="2ec47-103">Aplicar as políticas de recursos a recursos de rede</span><span class="sxs-lookup"><span data-stu-id="2ec47-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="2ec47-104">Este artigo mostra uma [política de recursos](resource-manager-policy.md) de exemplo que pode ser aplicada a gateways de rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec47-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="2ec47-105">Essa política garante a consistência dos gateways implantados em sua organização.</span><span class="sxs-lookup"><span data-stu-id="2ec47-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="2ec47-106">Definir o SKU do gateway de rede virtual permitido</span><span class="sxs-lookup"><span data-stu-id="2ec47-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="2ec47-107">A seguinte política restringe quais SKUs podem ser implantados em gateways de rede virtual:</span><span class="sxs-lookup"><span data-stu-id="2ec47-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2ec47-108">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ec47-108">Next steps</span></span>
* <span data-ttu-id="2ec47-109">Depois de definir uma regra de política (conforme mostrado nos exemplos anteriores), você precisará criar a definição de política e atribuí-la a um escopo.</span><span class="sxs-lookup"><span data-stu-id="2ec47-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="2ec47-110">O escopo pode ser uma assinatura, grupo de recursos ou recurso.</span><span class="sxs-lookup"><span data-stu-id="2ec47-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2ec47-111">Para atribuir políticas por meio do portal, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2ec47-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2ec47-112">Para atribuir políticas por meio da API REST, do PowerShell ou da CLI do Azure, consulte [Atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2ec47-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="2ec47-113">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2ec47-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

