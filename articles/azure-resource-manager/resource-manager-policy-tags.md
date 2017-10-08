---
title: "políticas de recursos aaaAzure marcas | Microsoft Docs"
description: "Fornece exemplos de políticas de recurso para gerenciamento de marcas em recursos"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="4d6b1-103">Aplicar políticas de recurso a marcas</span><span class="sxs-lookup"><span data-stu-id="4d6b1-103">Apply resource policies for tags</span></span>

<span data-ttu-id="4d6b1-104">Este tópico fornece a você pode aplicar o uso consistente de marcas tooensure nos recursos de regras de política comum.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="4d6b1-105">Aplicação de um grupo de recursos de tooa de política de marca ou a assinatura com recursos existentes não se aplicam retroativamente recursos de toothose política hello.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="4d6b1-106">políticas de saudação do tooenforce sobre os recursos, disparar uma toohello de atualização existente de recursos.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="4d6b1-107">Este artigo inclui um exemplo do PowerShell para disparar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="4d6b1-108">Garantir que todos os recursos em um grupo de recursos tenham um valor/marca</span><span class="sxs-lookup"><span data-stu-id="4d6b1-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="4d6b1-109">Um requisito comum é o de que todos os recursos em um grupo de recursos tenham uma marca e um valor específicos.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="4d6b1-110">Esse requisito é geralmente custos tootrack necessárias pelo departamento.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="4d6b1-111">Olá condições a seguir deve ser atendido:</span><span class="sxs-lookup"><span data-stu-id="4d6b1-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="4d6b1-112">Olá necessário marca e valor são acrescentado toonew e recursos que não têm marca Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="4d6b1-113">Olá necessário marca e o valor não pode ser removido de todos os recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="4d6b1-114">Você atender a esse requisito, aplicando o grupo de recursos do duas políticas internas tooa.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="4d6b1-115">ID</span><span class="sxs-lookup"><span data-stu-id="4d6b1-115">ID</span></span> | <span data-ttu-id="4d6b1-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="4d6b1-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="4d6b1-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="4d6b1-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="4d6b1-118">Aplica uma marca necessária e seu valor padrão quando não for especificado pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="4d6b1-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="4d6b1-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="4d6b1-120">Impõe uma marca necessária e seu valor.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="4d6b1-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d6b1-121">PowerShell</span></span>

<span data-ttu-id="4d6b1-122">saudação de script do PowerShell a seguir atribui o grupo de recursos do hello política interna duas definições tooa.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="4d6b1-123">Antes de executar o script hello, atribua todas as marcas necessárias toohello recurso grupo.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="4d6b1-124">Cada marca no grupo de recursos de saudação é necessária para recursos de saudação no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="4d6b1-125">grupos de recursos de tooall tooassign em sua assinatura, não fornecem Olá `-Name` parâmetro ao obter grupos de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="4d6b1-126">Depois de atribuir políticas hello, você pode disparar um tooall de atualização existente políticas de recursos tooenforce Olá marca que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="4d6b1-127">Olá, script a seguir retém outras marcas que existiam em recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="4d6b1-127">hello following script retains any other tags that existed on hello resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="4d6b1-128">Exigir marcas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="4d6b1-128">Require tags for a resource type</span></span>
<span data-ttu-id="4d6b1-129">saudação de exemplo a seguir mostra como toonest operadores lógicos toorequire um aplicativo de marca para apenas um tipo de recurso especificado (neste caso, as contas de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="4d6b1-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="4d6b1-130">Exigir marca</span><span class="sxs-lookup"><span data-stu-id="4d6b1-130">Require tag</span></span>
<span data-ttu-id="4d6b1-131">Olá seguinte política nega as solicitações que não têm uma marca que contém a chave "costCenter" (qualquer valor pode ser aplicado):</span><span class="sxs-lookup"><span data-stu-id="4d6b1-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="4d6b1-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d6b1-132">Next steps</span></span>
* <span data-ttu-id="4d6b1-133">Depois de definir uma regra de política (conforme mostrado no hello anterior exemplos), você precisa de definição de política de saudação toocreate e atribuí-la tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="4d6b1-134">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="4d6b1-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="4d6b1-135">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d6b1-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="4d6b1-136">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="4d6b1-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="4d6b1-137">Para políticas de tooresource uma introdução, consulte [visão geral do recurso política](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4d6b1-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="4d6b1-138">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4d6b1-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

