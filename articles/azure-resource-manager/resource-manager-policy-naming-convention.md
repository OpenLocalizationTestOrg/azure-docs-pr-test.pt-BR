---
title: "Políticas de recursos do Azure para convenções de nomenclatura | Microsoft Docs"
description: "Descreve as políticas do Azure Resource Manager para convenções de nomenclatura de recursos."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="2e845-103">Aplicar políticas de recursos a nomes e texto</span><span class="sxs-lookup"><span data-stu-id="2e845-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="2e845-104">Este tópico mostra várias [políticas de recursos](resource-manager-policy.md) que podem ser aplicadas para estabelecer as convenções de nomenclatura e texto.</span><span class="sxs-lookup"><span data-stu-id="2e845-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="2e845-105">Essas políticas garantem a consistência de nomes de recursos e valores de marcação.</span><span class="sxs-lookup"><span data-stu-id="2e845-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="2e845-106">Definir a convenção de nomenclatura com um curinga</span><span class="sxs-lookup"><span data-stu-id="2e845-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="2e845-107">O exemplo a seguir mostra o uso de curingas, que é compatível com a condição **like**.</span><span class="sxs-lookup"><span data-stu-id="2e845-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="2e845-108">A condição declara que, se o nome corresponder ao padrão mencionado (namePrefix\*nameSuffix), a solicitação será negada:</span><span class="sxs-lookup"><span data-stu-id="2e845-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="2e845-109">Definir a convenção de nomenclatura com um padrão</span><span class="sxs-lookup"><span data-stu-id="2e845-109">Set naming convention with pattern</span></span>

<span data-ttu-id="2e845-110">Para especificar que nomes de recurso correspondem a um padrão, use a condição match.</span><span class="sxs-lookup"><span data-stu-id="2e845-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="2e845-111">O exemplo a seguir exige que os nomes comecem com `contoso` e contenham seis letras adicionais:</span><span class="sxs-lookup"><span data-stu-id="2e845-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="2e845-112">Definir um padrão de data para um valor de marcação</span><span class="sxs-lookup"><span data-stu-id="2e845-112">Set date pattern for tag value</span></span>

<span data-ttu-id="2e845-113">Para exigir um padrão de data de dois dígitos, hífen, três letras, traço e quatro dígitos, use:</span><span class="sxs-lookup"><span data-stu-id="2e845-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2e845-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e845-114">Next steps</span></span>
* <span data-ttu-id="2e845-115">Depois de definir uma regra de política (conforme mostrado nos exemplos anteriores), você precisará criar a definição de política e atribuí-la a um escopo.</span><span class="sxs-lookup"><span data-stu-id="2e845-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="2e845-116">O escopo pode ser uma assinatura, grupo de recursos ou recurso.</span><span class="sxs-lookup"><span data-stu-id="2e845-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2e845-117">Para atribuir políticas por meio do portal, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e845-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2e845-118">Para atribuir políticas por meio da API REST, do PowerShell ou da CLI do Azure, consulte [Atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2e845-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="2e845-119">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2e845-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

