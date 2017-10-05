---
title: "Políticas de recurso do Azure | Microsoft Docs"
description: "Descreve como usar as políticas do Azure Resource Manager para garantir recursos consistentes propriedades são definidas durante a implantação. As políticas podem ser aplicadas em grupos de recursos ou de assinatura."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="6c18f-104">Visão geral de políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="6c18f-104">Resource policy overview</span></span>
<span data-ttu-id="6c18f-105">Políticas de recursos permitem que você estabeleça convenções para recursos em sua organização.</span><span class="sxs-lookup"><span data-stu-id="6c18f-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="6c18f-106">Definindo as convenções, você pode controlar os custos e muito mais fácil gerenciar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="6c18f-107">Por exemplo, você pode especificar que somente determinados tipos de máquinas virtuais são permitidos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="6c18f-108">Ou você pode exigir que todos os recursos tenham uma marca específica.</span><span class="sxs-lookup"><span data-stu-id="6c18f-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="6c18f-109">As políticas são herdadas por todos os recursos filho.</span><span class="sxs-lookup"><span data-stu-id="6c18f-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="6c18f-110">Então, se uma política for aplicada a um grupo de recursos, ela será aplicável a todos os recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="6c18f-111">Há dois conceitos a entender sobre políticas:</span><span class="sxs-lookup"><span data-stu-id="6c18f-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="6c18f-112">definição da política - descrevem quando a política é aplicada e qual ação tomar</span><span class="sxs-lookup"><span data-stu-id="6c18f-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="6c18f-113">atribuição de política - aplicar a definição de política a um escopo (assinatura ou grupo de recursos)</span><span class="sxs-lookup"><span data-stu-id="6c18f-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="6c18f-114">Este tópico se concentra na definição de política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="6c18f-115">Para obter informações sobre a atribuição de política, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](resource-manager-policy-portal.md) ou [Atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="6c18f-116">Políticas são avaliadas durante a criação e atualização de recursos (PUT e operações de PATCHES).</span><span class="sxs-lookup"><span data-stu-id="6c18f-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="6c18f-117">Atualmente, a política não avalia os tipos de recursos que não dão suporte a marcas, tipo e local, como o tipo de recurso Microsoft.Resources/deployments.</span><span class="sxs-lookup"><span data-stu-id="6c18f-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="6c18f-118">Esse suporte será adicionado no futuro.</span><span class="sxs-lookup"><span data-stu-id="6c18f-118">This support will be added at a future time.</span></span> <span data-ttu-id="6c18f-119">Para evitar problemas de compatibilidade com versões anteriores, você deve especificar explicitamente o tipo ao criar políticas.</span><span class="sxs-lookup"><span data-stu-id="6c18f-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="6c18f-120">Por exemplo, uma política de marcação que não especifica tipos é aplicada a todos os tipos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="6c18f-121">Nesse caso, uma implantação de modelo poderá falhar se houver um recurso aninhado que não dê suporte a marcas e o tipo de recurso de implantação tiver sido adicionado à avaliação da política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="6c18f-122">Qual é a diferença dela em relação ao RBAC?</span><span class="sxs-lookup"><span data-stu-id="6c18f-122">How is it different from RBAC?</span></span>
<span data-ttu-id="6c18f-123">Há algumas diferenças importantes entre a política e o RBAC (controle de acesso baseado em função).</span><span class="sxs-lookup"><span data-stu-id="6c18f-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="6c18f-124">O RBAC se concentra nas ações do **usuário** em escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="6c18f-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="6c18f-125">Por exemplo, você é adicionado à função de colaborador de um grupo de recursos no escopo do desejado, para que você possa fazer alterações a esse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="6c18f-126">Diretiva enfoca **recursos** propriedades durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="6c18f-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="6c18f-127">Por exemplo, por meio de políticas, você pode controlar os tipos de recursos que podem ser provisionados.</span><span class="sxs-lookup"><span data-stu-id="6c18f-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="6c18f-128">Ou você pode restringir os locais em que os recursos podem ser provisionados.</span><span class="sxs-lookup"><span data-stu-id="6c18f-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="6c18f-129">Ao contrário do RBAC, a política é um sistema de permissão padrão e negação explícita.</span><span class="sxs-lookup"><span data-stu-id="6c18f-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="6c18f-130">Para usar políticas, você deve estar autenticado pelo RBAC.</span><span class="sxs-lookup"><span data-stu-id="6c18f-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="6c18f-131">Especificamente, a conta precisa de:</span><span class="sxs-lookup"><span data-stu-id="6c18f-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="6c18f-132">`Microsoft.Authorization/policydefinitions/write` permissão para definir uma política</span><span class="sxs-lookup"><span data-stu-id="6c18f-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="6c18f-133">`Microsoft.Authorization/policyassignments/write` permissão para atribuir uma política</span><span class="sxs-lookup"><span data-stu-id="6c18f-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="6c18f-134">Essas permissões não estão incluídas na função **Colaborador**.</span><span class="sxs-lookup"><span data-stu-id="6c18f-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="6c18f-135">Políticas internas</span><span class="sxs-lookup"><span data-stu-id="6c18f-135">Built-in policies</span></span>

<span data-ttu-id="6c18f-136">O Azure fornece algumas definições de política internas que podem reduzir o número de políticas que você precisa definir.</span><span class="sxs-lookup"><span data-stu-id="6c18f-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="6c18f-137">Antes de continuar com as definições de política, você deve considerar se uma política interna já fornece a definição de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="6c18f-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="6c18f-138">As definições de políticas internas são:</span><span class="sxs-lookup"><span data-stu-id="6c18f-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="6c18f-139">Locais permitidos</span><span class="sxs-lookup"><span data-stu-id="6c18f-139">Allowed locations</span></span>
* <span data-ttu-id="6c18f-140">Tipos de recursos permitidos</span><span class="sxs-lookup"><span data-stu-id="6c18f-140">Allowed resource types</span></span>
* <span data-ttu-id="6c18f-141">SKUs de contas de armazenamento permitidas</span><span class="sxs-lookup"><span data-stu-id="6c18f-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="6c18f-142">SKUs de máquinas virtuais permitidas</span><span class="sxs-lookup"><span data-stu-id="6c18f-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="6c18f-143">Aplicar a marca e o valor padrão</span><span class="sxs-lookup"><span data-stu-id="6c18f-143">Apply tag and default value</span></span>
* <span data-ttu-id="6c18f-144">Impor a marca e o valor</span><span class="sxs-lookup"><span data-stu-id="6c18f-144">Enforce tag and value</span></span>
* <span data-ttu-id="6c18f-145">Tipos de recursos não permitidos</span><span class="sxs-lookup"><span data-stu-id="6c18f-145">Not allowed resource types</span></span>
* <span data-ttu-id="6c18f-146">Requer o SQL Server versão 12.0</span><span class="sxs-lookup"><span data-stu-id="6c18f-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="6c18f-147">Exigir criptografia de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="6c18f-147">Require storage account encryption</span></span>

<span data-ttu-id="6c18f-148">Você pode atribuir qualquer uma dessas políticas por meio do [portal](resource-manager-policy-portal.md), do [PowerShell](resource-manager-policy-create-assign.md#powershell) ou da [CLI do Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c18f-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="6c18f-149">Estrutura da definição de política</span><span class="sxs-lookup"><span data-stu-id="6c18f-149">Policy definition structure</span></span>
<span data-ttu-id="6c18f-150">Você usa JSON para criar uma definição de política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="6c18f-151">A definição de política contém elementos para:</span><span class="sxs-lookup"><span data-stu-id="6c18f-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="6c18f-152">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6c18f-152">parameters</span></span>
* <span data-ttu-id="6c18f-153">nome de exibição</span><span class="sxs-lookup"><span data-stu-id="6c18f-153">display name</span></span>
* <span data-ttu-id="6c18f-154">descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-154">description</span></span>
* <span data-ttu-id="6c18f-155">regra de política</span><span class="sxs-lookup"><span data-stu-id="6c18f-155">policy rule</span></span>
  * <span data-ttu-id="6c18f-156">avaliação de lógica</span><span class="sxs-lookup"><span data-stu-id="6c18f-156">logical evaluation</span></span>
  * <span data-ttu-id="6c18f-157">efeito</span><span class="sxs-lookup"><span data-stu-id="6c18f-157">effect</span></span>

<span data-ttu-id="6c18f-158">O exemplo a seguir mostra uma política que limita os locais em que os recursos são implantados:</span><span class="sxs-lookup"><span data-stu-id="6c18f-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="6c18f-159">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6c18f-159">Parameters</span></span>
<span data-ttu-id="6c18f-160">O uso de parâmetros ajuda a simplificar o gerenciamento de política, reduzindo o número de definições de política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="6c18f-161">Defina uma política para uma propriedade de recurso (por exemplo, limitando os locais onde os recursos podem ser implantados) e incluir parâmetros na definição.</span><span class="sxs-lookup"><span data-stu-id="6c18f-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="6c18f-162">Em seguida, reutilizar essa definição de política para diferentes cenários pela passagem de valores diferentes (como especificar um conjunto de locais para uma assinatura) quando atribuir a política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="6c18f-163">Declare parâmetros ao criar definições de política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="6c18f-164">O tipo de um parâmetro pode ser cadeia de caracteres ou matriz.</span><span class="sxs-lookup"><span data-stu-id="6c18f-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="6c18f-165">A propriedade de metadados é usada para que ferramentas como o portal do Azure exibam informações amigáveis ao usuário.</span><span class="sxs-lookup"><span data-stu-id="6c18f-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="6c18f-166">Na regra de política, você fazer referência a parâmetros com a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="6c18f-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="6c18f-167">Nome de exibição e descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-167">Display name and description</span></span>

<span data-ttu-id="6c18f-168">Você usa o **displayName** e **description** para identificar a definição de política e fornecer contexto para quando ele é usado.</span><span class="sxs-lookup"><span data-stu-id="6c18f-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="6c18f-169">Regra de política</span><span class="sxs-lookup"><span data-stu-id="6c18f-169">Policy rule</span></span>

<span data-ttu-id="6c18f-170">A regra de política consiste em **se** e **, em seguida,** blocos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="6c18f-171">No **se** bloco, você define uma ou mais condições que especificam quando a política é aplicada.</span><span class="sxs-lookup"><span data-stu-id="6c18f-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="6c18f-172">Você pode aplicar os operadores lógicos para essas condições para definir exatamente o cenário para uma política.</span><span class="sxs-lookup"><span data-stu-id="6c18f-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="6c18f-173">No **, em seguida,** bloco, você define o efeito que acontecerá quando o **se** condições sejam atendidas.</span><span class="sxs-lookup"><span data-stu-id="6c18f-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="6c18f-174">Operadores lógicos</span><span class="sxs-lookup"><span data-stu-id="6c18f-174">Logical operators</span></span>
<span data-ttu-id="6c18f-175">Os operadores lógicos com suporte são:</span><span class="sxs-lookup"><span data-stu-id="6c18f-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="6c18f-176">O **não** sintaxe inverte o resultado da condição.</span><span class="sxs-lookup"><span data-stu-id="6c18f-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="6c18f-177">A sintaxe de **allOf** (semelhante à operação **E** lógica) requer que todas as condições sejam verdadeiras.</span><span class="sxs-lookup"><span data-stu-id="6c18f-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="6c18f-178">A sintaxe de **anyOf** (semelhante à operação **Ou** lógica) requer que uma ou mais condições sejam verdadeiras.</span><span class="sxs-lookup"><span data-stu-id="6c18f-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="6c18f-179">Você pode aninhar operadores lógicos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-179">You can nest logical operators.</span></span> <span data-ttu-id="6c18f-180">A exemplo a seguir mostra uma operação **not** operação é aninhada dentro de uma operação **allOf**.</span><span class="sxs-lookup"><span data-stu-id="6c18f-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
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
```

### <a name="conditions"></a><span data-ttu-id="6c18f-181">Condições</span><span class="sxs-lookup"><span data-stu-id="6c18f-181">Conditions</span></span>
<span data-ttu-id="6c18f-182">Uma condição avalia se um **campo** atende a determinados critérios.</span><span class="sxs-lookup"><span data-stu-id="6c18f-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="6c18f-183">As condições com suporte são:</span><span class="sxs-lookup"><span data-stu-id="6c18f-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="6c18f-184">Ao usar a condição **like**, você pode fornecer um curinga (*) no valor.</span><span class="sxs-lookup"><span data-stu-id="6c18f-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="6c18f-185">Ao usar a condição **match**, forneça `#` para representar um dígito, `?` para uma letra e outro caractere para representar o caractere real.</span><span class="sxs-lookup"><span data-stu-id="6c18f-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="6c18f-186">Para obter exemplos, consulte [Aplicar políticas de recursos para nomes e texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="6c18f-187">Campos</span><span class="sxs-lookup"><span data-stu-id="6c18f-187">Fields</span></span>
<span data-ttu-id="6c18f-188">As condições são formadas usando campos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="6c18f-189">Um campo representa as propriedades na carga de solicitação de recurso que é usada para descrever o estado do recurso.</span><span class="sxs-lookup"><span data-stu-id="6c18f-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="6c18f-190">Há suporte para os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="6c18f-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="6c18f-191">aliases de propriedade - para obter uma lista, confira [Aliases](#aliases).</span><span class="sxs-lookup"><span data-stu-id="6c18f-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="6c18f-192">Efeito</span><span class="sxs-lookup"><span data-stu-id="6c18f-192">Effect</span></span>
<span data-ttu-id="6c18f-193">A política dá suporte a três tipos de efeito - `deny`, `audit` e `append`.</span><span class="sxs-lookup"><span data-stu-id="6c18f-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="6c18f-194">**Negar** gera um evento no log de auditoria e causa uma falha da solicitação</span><span class="sxs-lookup"><span data-stu-id="6c18f-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="6c18f-195">**Auditar** gera um evento de aviso no log de auditoria, mas não causa falha da solicitação</span><span class="sxs-lookup"><span data-stu-id="6c18f-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="6c18f-196">**Acrescentar** adiciona o conjunto de campos definido à solicitação</span><span class="sxs-lookup"><span data-stu-id="6c18f-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="6c18f-197">Para **acrescentar**, você precisa fornecer os detalhes abaixo:</span><span class="sxs-lookup"><span data-stu-id="6c18f-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="6c18f-198">O valor pode ser uma cadeia de caracteres ou um objeto no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="6c18f-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="6c18f-199">Aliases</span><span class="sxs-lookup"><span data-stu-id="6c18f-199">Aliases</span></span>

<span data-ttu-id="6c18f-200">Você pode usar aliases de propriedade para acessar propriedades específicas para um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="6c18f-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="6c18f-201">Os aliases permitem restringir quais valores ou condições são permitidas para uma propriedade em um recurso.</span><span class="sxs-lookup"><span data-stu-id="6c18f-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="6c18f-202">Cada alias é mapeado para caminhos em diferentes versões de API para um tipo de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="6c18f-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="6c18f-203">Durante a avaliação de política, o mecanismo de políticas obtém o caminho de propriedade para essa versão de API.</span><span class="sxs-lookup"><span data-stu-id="6c18f-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="6c18f-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="6c18f-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="6c18f-205">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-205">Alias</span></span> | <span data-ttu-id="6c18f-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="6c18f-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="6c18f-208">Defina se a porta (6379) do servidor Redis não ssl está habilitada.</span><span class="sxs-lookup"><span data-stu-id="6c18f-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="6c18f-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="6c18f-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="6c18f-210">Defina o número de fragmentos a serem criados em um Cache de Cluster Premium.</span><span class="sxs-lookup"><span data-stu-id="6c18f-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="6c18f-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="6c18f-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="6c18f-212">Defina o tamanho do cache Redis a ser implantado.</span><span class="sxs-lookup"><span data-stu-id="6c18f-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="6c18f-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="6c18f-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="6c18f-214">Veja a família de SKU a ser usada.</span><span class="sxs-lookup"><span data-stu-id="6c18f-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="6c18f-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="6c18f-216">Defina o tipo de Cache Redis a ser implantado.</span><span class="sxs-lookup"><span data-stu-id="6c18f-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="6c18f-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="6c18f-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="6c18f-218">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-218">Alias</span></span> | <span data-ttu-id="6c18f-219">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="6c18f-221">Defina o nome do tipo de preços.</span><span class="sxs-lookup"><span data-stu-id="6c18f-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="6c18f-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="6c18f-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="6c18f-223">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-223">Alias</span></span> | <span data-ttu-id="6c18f-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6c18f-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="6c18f-226">Defina a oferta da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6c18f-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="6c18f-228">Defina o editor da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="6c18f-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="6c18f-230">Defina a SKU da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6c18f-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="6c18f-232">Defina a versão da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="6c18f-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="6c18f-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="6c18f-234">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-234">Alias</span></span> | <span data-ttu-id="6c18f-235">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="6c18f-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="6c18f-237">Defina o identificador da imagem usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6c18f-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="6c18f-239">Defina a oferta da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6c18f-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="6c18f-241">Defina o editor da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="6c18f-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="6c18f-243">Defina a SKU da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6c18f-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="6c18f-245">Defina a versão da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="6c18f-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="6c18f-247">Defina que a imagem ou o disco está licenciado no local.</span><span class="sxs-lookup"><span data-stu-id="6c18f-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="6c18f-248">Esse valor é usado apenas para imagens que contêm o sistema operacional Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6c18f-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="6c18f-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6c18f-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="6c18f-250">Defina a oferta da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6c18f-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="6c18f-252">Defina o editor da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="6c18f-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="6c18f-254">Defina a SKU da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6c18f-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="6c18f-256">Defina a versão da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="6c18f-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="6c18f-258">Defina o URI do vhd.</span><span class="sxs-lookup"><span data-stu-id="6c18f-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="6c18f-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="6c18f-260">Defina o tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="6c18f-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="6c18f-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="6c18f-262">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-262">Alias</span></span> | <span data-ttu-id="6c18f-263">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="6c18f-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="6c18f-265">Defina o nome do publicador da extensão.</span><span class="sxs-lookup"><span data-stu-id="6c18f-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="6c18f-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="6c18f-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="6c18f-267">Defina o tipo de extensão.</span><span class="sxs-lookup"><span data-stu-id="6c18f-267">Set the type of extension.</span></span> |
| <span data-ttu-id="6c18f-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="6c18f-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="6c18f-269">Defina a versão da extensão.</span><span class="sxs-lookup"><span data-stu-id="6c18f-269">Set the version of the extension.</span></span> |

<span data-ttu-id="6c18f-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="6c18f-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="6c18f-271">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-271">Alias</span></span> | <span data-ttu-id="6c18f-272">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="6c18f-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="6c18f-274">Defina o identificador da imagem usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="6c18f-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="6c18f-276">Defina a oferta da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="6c18f-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="6c18f-278">Defina o editor da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="6c18f-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="6c18f-280">Defina a SKU da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="6c18f-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="6c18f-282">Defina a versão da imagem da plataforma ou da imagem do marketplace usada para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="6c18f-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="6c18f-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="6c18f-284">Defina que a imagem ou o disco está licenciado no local.</span><span class="sxs-lookup"><span data-stu-id="6c18f-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="6c18f-285">Esse valor é usado apenas para imagens que contêm o sistema operacional Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6c18f-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="6c18f-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="6c18f-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="6c18f-287">Defina o prefixo do nome do computador para todas as máquinas virtuais no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6c18f-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="6c18f-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="6c18f-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="6c18f-289">Defina o URI de blob da imagem de usuário.</span><span class="sxs-lookup"><span data-stu-id="6c18f-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="6c18f-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="6c18f-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="6c18f-291">Defina as URLs de contêiner que são usadas para armazenar discos do sistema operacional para o conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6c18f-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="6c18f-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="6c18f-293">Defina o tamanho das máquinas virtuais em um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6c18f-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="6c18f-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="6c18f-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="6c18f-295">Defina o nível de máquinas virtuais em um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6c18f-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="6c18f-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="6c18f-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="6c18f-297">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-297">Alias</span></span> | <span data-ttu-id="6c18f-298">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="6c18f-300">Defina o tamanho do gateway.</span><span class="sxs-lookup"><span data-stu-id="6c18f-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="6c18f-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="6c18f-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="6c18f-302">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-302">Alias</span></span> | <span data-ttu-id="6c18f-303">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="6c18f-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="6c18f-305">Defina o tipo deste gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6c18f-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="6c18f-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="6c18f-307">Defina o nome da SKU de gateway.</span><span class="sxs-lookup"><span data-stu-id="6c18f-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="6c18f-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="6c18f-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="6c18f-309">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-309">Alias</span></span> | <span data-ttu-id="6c18f-310">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="6c18f-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="6c18f-312">Defina a versão do servidor.</span><span class="sxs-lookup"><span data-stu-id="6c18f-312">Set the version of the server.</span></span> |

<span data-ttu-id="6c18f-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="6c18f-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="6c18f-314">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-314">Alias</span></span> | <span data-ttu-id="6c18f-315">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="6c18f-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="6c18f-317">Defina a edição do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c18f-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="6c18f-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="6c18f-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="6c18f-319">Defina o nome do pool elástico em que o banco de dados está.</span><span class="sxs-lookup"><span data-stu-id="6c18f-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="6c18f-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="6c18f-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="6c18f-321">Defina a ID de objetivo de nível de serviço configurada do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c18f-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="6c18f-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="6c18f-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="6c18f-323">Defina o nome do objetivo de nível de serviço configurado do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c18f-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="6c18f-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="6c18f-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="6c18f-325">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-325">Alias</span></span> | <span data-ttu-id="6c18f-326">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-327">servidores/elasticpools</span><span class="sxs-lookup"><span data-stu-id="6c18f-327">servers/elasticpools</span></span> | <span data-ttu-id="6c18f-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="6c18f-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="6c18f-329">Defina o DTU compartilhado total para o pool elástico de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c18f-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="6c18f-330">servidores/elasticpools</span><span class="sxs-lookup"><span data-stu-id="6c18f-330">servers/elasticpools</span></span> | <span data-ttu-id="6c18f-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="6c18f-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="6c18f-332">Defina a edição do pool elástico.</span><span class="sxs-lookup"><span data-stu-id="6c18f-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="6c18f-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="6c18f-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="6c18f-334">Alias</span><span class="sxs-lookup"><span data-stu-id="6c18f-334">Alias</span></span> | <span data-ttu-id="6c18f-335">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c18f-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6c18f-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="6c18f-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="6c18f-337">Defina o nível de acesso usado para cobrança.</span><span class="sxs-lookup"><span data-stu-id="6c18f-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="6c18f-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="6c18f-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="6c18f-339">Defina o nome da SKU.</span><span class="sxs-lookup"><span data-stu-id="6c18f-339">Set the SKU name.</span></span> |
| <span data-ttu-id="6c18f-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="6c18f-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="6c18f-341">Defina se o serviço criptografa os dados conforme eles são armazenados no serviço de armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="6c18f-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="6c18f-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="6c18f-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="6c18f-343">Defina se o serviço criptografa os dados conforme eles são armazenados no serviço de armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="6c18f-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="6c18f-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="6c18f-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="6c18f-345">Defina o nome da SKU.</span><span class="sxs-lookup"><span data-stu-id="6c18f-345">Set the SKU name.</span></span> |
| <span data-ttu-id="6c18f-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="6c18f-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="6c18f-347">Configurado para permitir somente o tráfego https para o serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6c18f-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="6c18f-348">Exemplos de políticas</span><span class="sxs-lookup"><span data-stu-id="6c18f-348">Policy examples</span></span>

<span data-ttu-id="6c18f-349">Os tópicos a seguir contêm exemplos de política:</span><span class="sxs-lookup"><span data-stu-id="6c18f-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="6c18f-350">Para obter exemplos de políticas de marca, veja [Aplicar políticas de recursos para marcas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="6c18f-351">Para obter exemplos de padrões de nomenclatura e texto, confira [Aplicar políticas de recursos a nomes e texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="6c18f-352">Para obter exemplos de políticas de armazenamento, veja [Aplicar políticas de recursos para contas de armazenamento](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="6c18f-353">Para obter exemplos de políticas de máquina virtual, veja [Aplicar políticas de recursos a VMs Linux](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) e [Aplicar políticas de recursos a VMs do Windows](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6c18f-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="6c18f-354">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c18f-354">Next steps</span></span>
* <span data-ttu-id="6c18f-355">Depois de definir uma regra de política, atribua um escopo.</span><span class="sxs-lookup"><span data-stu-id="6c18f-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="6c18f-356">Para atribuir políticas por meio do portal, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="6c18f-357">Para atribuir políticas por meio da API REST, do PowerShell ou da CLI do Azure, consulte [Atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="6c18f-358">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6c18f-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="6c18f-359">O esquema da política é publicado em [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="6c18f-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

