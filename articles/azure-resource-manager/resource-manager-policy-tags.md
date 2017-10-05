---
title: "Políticas de recurso do Azure para marcas | Microsoft Docs"
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
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="3a06e-103">Aplicar políticas de recurso a marcas</span><span class="sxs-lookup"><span data-stu-id="3a06e-103">Apply resource policies for tags</span></span>

<span data-ttu-id="3a06e-104">Este tópico fornece regras de política comuns que podem ser aplicadas para garantir o uso consistente de marcas em recursos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="3a06e-105">A aplicação de uma política de marca a um grupo de recursos ou a uma assinatura com recursos existentes não aplica retroativamente a política a esses recursos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="3a06e-106">Para impor as políticas a esses recursos, dispare uma atualização para os recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="3a06e-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="3a06e-107">Este artigo inclui um exemplo do PowerShell para disparar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="3a06e-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="3a06e-108">Garantir que todos os recursos em um grupo de recursos tenham um valor/marca</span><span class="sxs-lookup"><span data-stu-id="3a06e-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="3a06e-109">Um requisito comum é o de que todos os recursos em um grupo de recursos tenham uma marca e um valor específicos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="3a06e-110">Esse requisito geralmente é necessário para controlar custos por departamento.</span><span class="sxs-lookup"><span data-stu-id="3a06e-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="3a06e-111">As seguintes condições devem ser atendidas:</span><span class="sxs-lookup"><span data-stu-id="3a06e-111">The following conditions must be met:</span></span>

* <span data-ttu-id="3a06e-112">A marca necessária e o valor são acrescentados aos recursos novos e atualizados que não têm a marca.</span><span class="sxs-lookup"><span data-stu-id="3a06e-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="3a06e-113">A marca e o valor necessários não podem ser removidos de nenhum recurso existente.</span><span class="sxs-lookup"><span data-stu-id="3a06e-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="3a06e-114">Você pode atender a esse requisito aplicando a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="3a06e-115">ID</span><span class="sxs-lookup"><span data-stu-id="3a06e-115">ID</span></span> | <span data-ttu-id="3a06e-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="3a06e-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="3a06e-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="3a06e-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="3a06e-118">Aplica uma marca necessária e seu valor padrão quando não for especificado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="3a06e-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="3a06e-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="3a06e-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="3a06e-120">Impõe uma marca necessária e seu valor.</span><span class="sxs-lookup"><span data-stu-id="3a06e-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="3a06e-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a06e-121">PowerShell</span></span>

<span data-ttu-id="3a06e-122">O seguinte script PowerShell atribui as duas definições de diretiva interna para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="3a06e-123">Antes de executar o script, atribua todas as marcas necessárias para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="3a06e-124">Cada marca no grupo de recursos é necessária para os recursos do grupo.</span><span class="sxs-lookup"><span data-stu-id="3a06e-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="3a06e-125">Para atribuir a todos os grupos de recursos em sua assinatura, não fornece o `-Name` parâmetro ao obter os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a06e-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

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

<span data-ttu-id="3a06e-126">Depois de atribuir as políticas, você pode disparar uma atualização para todos os recursos existentes para impor as políticas de marca que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="3a06e-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="3a06e-127">O script a seguir mantém outras marcas que existiam nos recursos:</span><span class="sxs-lookup"><span data-stu-id="3a06e-127">The following script retains any other tags that existed on the resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="3a06e-128">Exigir marcas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="3a06e-128">Require tags for a resource type</span></span>
<span data-ttu-id="3a06e-129">O exemplo a seguir mostra como aninhar operadores lógicos para exigir uma marca de aplicativo somente para um tipo de recurso especificado (nesse caso, contas de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="3a06e-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="3a06e-130">Exigir marca</span><span class="sxs-lookup"><span data-stu-id="3a06e-130">Require tag</span></span>
<span data-ttu-id="3a06e-131">A seguinte política nega as solicitações que não têm uma marca contendo a chave "costCenter" (qualquer valor pode ser aplicado):</span><span class="sxs-lookup"><span data-stu-id="3a06e-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3a06e-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a06e-132">Next steps</span></span>
* <span data-ttu-id="3a06e-133">Depois de definir uma regra de política (conforme mostrado nos exemplos anteriores), você precisará criar a definição de política e atribuí-la a um escopo.</span><span class="sxs-lookup"><span data-stu-id="3a06e-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="3a06e-134">O escopo pode ser uma assinatura, grupo de recursos ou recurso.</span><span class="sxs-lookup"><span data-stu-id="3a06e-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="3a06e-135">Para atribuir políticas por meio do portal, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3a06e-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="3a06e-136">Para atribuir políticas por meio da API REST, do PowerShell ou da CLI do Azure, consulte [Atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="3a06e-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="3a06e-137">Para ver uma introdução às políticas de recurso, confira [Visão geral da política de recurso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3a06e-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="3a06e-138">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3a06e-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

