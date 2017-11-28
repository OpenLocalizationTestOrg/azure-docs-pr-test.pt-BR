---
title: "políticas de recursos aaaAzure para convenções de nomenclatura | Microsoft Docs"
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
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="c0064-103">Aplicar políticas de recursos a nomes e texto</span><span class="sxs-lookup"><span data-stu-id="c0064-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="c0064-104">Este tópico mostra vários [políticas de recursos](resource-manager-policy.md) você pode aplicar as convenções de nomenclatura e texto tooestablish.</span><span class="sxs-lookup"><span data-stu-id="c0064-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="c0064-105">Essas políticas garantem a consistência de nomes de recursos e valores de marcação.</span><span class="sxs-lookup"><span data-stu-id="c0064-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="c0064-106">Definir a convenção de nomenclatura com um curinga</span><span class="sxs-lookup"><span data-stu-id="c0064-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="c0064-107">Olá, exemplo a seguir mostra uso Olá de caractere curinga, que é suportado pelo Olá **como** condição.</span><span class="sxs-lookup"><span data-stu-id="c0064-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="c0064-108">Olá condição declara que se hello nome corresponder padrão mencionadas hello (namePrefix\*nameSuffix), em seguida, negar a solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="c0064-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="c0064-109">Definir a convenção de nomenclatura com um padrão</span><span class="sxs-lookup"><span data-stu-id="c0064-109">Set naming convention with pattern</span></span>

<span data-ttu-id="c0064-110">toospecify que os nomes de recursos correspondem a um padrão, use Olá correspondem à condição.</span><span class="sxs-lookup"><span data-stu-id="c0064-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="c0064-111">exemplo a seguir Hello requer nomes toostart com `contoso` e conter seis letras adicionais:</span><span class="sxs-lookup"><span data-stu-id="c0064-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="c0064-112">Definir um padrão de data para um valor de marcação</span><span class="sxs-lookup"><span data-stu-id="c0064-112">Set date pattern for tag value</span></span>

<span data-ttu-id="c0064-113">toorequire um padrão de data de dois dígitos, hífen, três letras, traço e quatro dígitos, use:</span><span class="sxs-lookup"><span data-stu-id="c0064-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c0064-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0064-114">Next steps</span></span>
* <span data-ttu-id="c0064-115">Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="c0064-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="c0064-116">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="c0064-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="c0064-117">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c0064-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c0064-118">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="c0064-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="c0064-119">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c0064-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

