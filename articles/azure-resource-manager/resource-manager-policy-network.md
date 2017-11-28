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
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="1b643-103">Aplicar recurso políticas toonetwork recursos</span><span class="sxs-lookup"><span data-stu-id="1b643-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="1b643-104">Este artigo mostra um exemplo [diretiva recursos](resource-manager-policy.md) você pode aplicar tooAzure gateways de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="1b643-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="1b643-105">Essa política garante a consistência dos gateways implantados em sua organização.</span><span class="sxs-lookup"><span data-stu-id="1b643-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="1b643-106">Definir o SKU do gateway de rede virtual permitido</span><span class="sxs-lookup"><span data-stu-id="1b643-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="1b643-107">Olá após diretiva restringe quais SKUs podem ser implantados para gateways de rede virtual:</span><span class="sxs-lookup"><span data-stu-id="1b643-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1b643-108">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b643-108">Next steps</span></span>
* <span data-ttu-id="1b643-109">Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="1b643-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="1b643-110">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="1b643-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="1b643-111">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b643-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="1b643-112">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="1b643-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="1b643-113">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="1b643-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

