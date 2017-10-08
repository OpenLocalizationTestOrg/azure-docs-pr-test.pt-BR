---
title: "políticas de recursos aaaAzure | Microsoft Docs"
description: "Descreve como as propriedades de recurso consistente do toouse do Azure Resource Manager políticas tooensure são definidas durante a implantação. Políticas podem ser aplicadas a grupos de assinatura ou o recurso de saudação."
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="056f2-104">Visão geral de políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="056f2-104">Resource policy overview</span></span>
<span data-ttu-id="056f2-105">Políticas de recursos permitem que você tooestablish convenções para recursos em sua organização.</span><span class="sxs-lookup"><span data-stu-id="056f2-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="056f2-106">Definindo as convenções, você pode controlar os custos e muito mais fácil gerenciar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="056f2-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="056f2-107">Por exemplo, você pode especificar que somente determinados tipos de máquinas virtuais são permitidos.</span><span class="sxs-lookup"><span data-stu-id="056f2-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="056f2-108">Ou você pode exigir que todos os recursos tenham uma marca específica.</span><span class="sxs-lookup"><span data-stu-id="056f2-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="056f2-109">As políticas são herdadas por todos os recursos filho.</span><span class="sxs-lookup"><span data-stu-id="056f2-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="056f2-110">Portanto, se uma política for aplicada tooa grupo de recursos, é aplicável tooall recursos de saudação desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="056f2-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="056f2-111">Há dois toounderstand conceitos sobre as políticas de:</span><span class="sxs-lookup"><span data-stu-id="056f2-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="056f2-112">definição de política - descrevem quando a política de saudação é imposta e qual ação tootake</span><span class="sxs-lookup"><span data-stu-id="056f2-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="056f2-113">atribuição de política - aplicar Olá política definição tooa escopo (assinatura ou grupo de recursos)</span><span class="sxs-lookup"><span data-stu-id="056f2-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="056f2-114">Este tópico se concentra na definição de política.</span><span class="sxs-lookup"><span data-stu-id="056f2-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="056f2-115">Para obter informações sobre atribuição de política, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md) ou [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="056f2-116">Políticas são avaliadas durante a criação e atualização de recursos (PUT e operações de PATCHES).</span><span class="sxs-lookup"><span data-stu-id="056f2-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="056f2-117">Atualmente, política não avalia os tipos de recursos que não oferecem suporte a marcas, tipo e local, como o tipo de recurso de Microsoft.Resources/deployments hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="056f2-118">Esse suporte será adicionado no futuro.</span><span class="sxs-lookup"><span data-stu-id="056f2-118">This support will be added at a future time.</span></span> <span data-ttu-id="056f2-119">tooavoid problemas de compatibilidade com versões anteriores, você deve especificar explicitamente as tipo ao criar políticas.</span><span class="sxs-lookup"><span data-stu-id="056f2-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="056f2-120">Por exemplo, uma política de marcação que não especifica tipos é aplicada a todos os tipos.</span><span class="sxs-lookup"><span data-stu-id="056f2-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="056f2-121">Nesse caso, uma implantação de modelo poderá falhar se houver um recurso aninhado que não oferece suporte a marcas e tipo de recurso de implantação de saudação foi adicionado toopolicy avaliação.</span><span class="sxs-lookup"><span data-stu-id="056f2-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="056f2-122">Qual é a diferença dela em relação ao RBAC?</span><span class="sxs-lookup"><span data-stu-id="056f2-122">How is it different from RBAC?</span></span>
<span data-ttu-id="056f2-123">Há algumas diferenças importantes entre a política e o RBAC (controle de acesso baseado em função).</span><span class="sxs-lookup"><span data-stu-id="056f2-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="056f2-124">O RBAC se concentra nas ações do **usuário** em escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="056f2-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="056f2-125">Por exemplo, você é adicionados toohello a função de Colaborador para um grupo de recursos no escopo de saudação desejado, para que você pode fazer alterações toothat grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="056f2-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="056f2-126">Diretiva enfoca **recursos** propriedades durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="056f2-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="056f2-127">Por exemplo, por meio de políticas, você pode controlar os tipos de saudação de recursos que podem ser provisionados.</span><span class="sxs-lookup"><span data-stu-id="056f2-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="056f2-128">Ou, você pode restringir os locais Olá no qual recursos Olá podem ser provisionados.</span><span class="sxs-lookup"><span data-stu-id="056f2-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="056f2-129">Ao contrário do RBAC, a política é um sistema de permissão padrão e negação explícita.</span><span class="sxs-lookup"><span data-stu-id="056f2-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="056f2-130">políticas de toouse, você deve ser autenticado por meio de RBAC.</span><span class="sxs-lookup"><span data-stu-id="056f2-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="056f2-131">Especificamente, a conta precisa de:</span><span class="sxs-lookup"><span data-stu-id="056f2-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="056f2-132">`Microsoft.Authorization/policydefinitions/write`permissão toodefine uma política</span><span class="sxs-lookup"><span data-stu-id="056f2-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="056f2-133">`Microsoft.Authorization/policyassignments/write`permissão tooassign uma política</span><span class="sxs-lookup"><span data-stu-id="056f2-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="056f2-134">Essas permissões não são incluídas no hello **Colaborador** função.</span><span class="sxs-lookup"><span data-stu-id="056f2-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="056f2-135">Políticas internas</span><span class="sxs-lookup"><span data-stu-id="056f2-135">Built-in policies</span></span>

<span data-ttu-id="056f2-136">O Azure fornece algumas definições de políticas internas que podem reduzir o número de saudação de políticas de você ter toodefine.</span><span class="sxs-lookup"><span data-stu-id="056f2-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="056f2-137">Antes de continuar com as definições de política, você deve considerar se uma política interna já fornece definição Olá que necessária.</span><span class="sxs-lookup"><span data-stu-id="056f2-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="056f2-138">definições de políticas internas de saudação são:</span><span class="sxs-lookup"><span data-stu-id="056f2-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="056f2-139">Locais permitidos</span><span class="sxs-lookup"><span data-stu-id="056f2-139">Allowed locations</span></span>
* <span data-ttu-id="056f2-140">Tipos de recursos permitidos</span><span class="sxs-lookup"><span data-stu-id="056f2-140">Allowed resource types</span></span>
* <span data-ttu-id="056f2-141">SKUs de contas de armazenamento permitidas</span><span class="sxs-lookup"><span data-stu-id="056f2-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="056f2-142">SKUs de máquinas virtuais permitidas</span><span class="sxs-lookup"><span data-stu-id="056f2-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="056f2-143">Aplicar a marca e o valor padrão</span><span class="sxs-lookup"><span data-stu-id="056f2-143">Apply tag and default value</span></span>
* <span data-ttu-id="056f2-144">Impor a marca e o valor</span><span class="sxs-lookup"><span data-stu-id="056f2-144">Enforce tag and value</span></span>
* <span data-ttu-id="056f2-145">Tipos de recursos não permitidos</span><span class="sxs-lookup"><span data-stu-id="056f2-145">Not allowed resource types</span></span>
* <span data-ttu-id="056f2-146">Requer o SQL Server versão 12.0</span><span class="sxs-lookup"><span data-stu-id="056f2-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="056f2-147">Exigir criptografia de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="056f2-147">Require storage account encryption</span></span>

<span data-ttu-id="056f2-148">Você pode atribuir qualquer essas políticas por meio de saudação [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), ou [CLI do Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="056f2-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="056f2-149">Estrutura da definição de política</span><span class="sxs-lookup"><span data-stu-id="056f2-149">Policy definition structure</span></span>
<span data-ttu-id="056f2-150">Use o JSON toocreate uma definição de política.</span><span class="sxs-lookup"><span data-stu-id="056f2-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="056f2-151">definição de política de saudação contém elementos para:</span><span class="sxs-lookup"><span data-stu-id="056f2-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="056f2-152">parâmetros</span><span class="sxs-lookup"><span data-stu-id="056f2-152">parameters</span></span>
* <span data-ttu-id="056f2-153">nome de exibição</span><span class="sxs-lookup"><span data-stu-id="056f2-153">display name</span></span>
* <span data-ttu-id="056f2-154">descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-154">description</span></span>
* <span data-ttu-id="056f2-155">regra de política</span><span class="sxs-lookup"><span data-stu-id="056f2-155">policy rule</span></span>
  * <span data-ttu-id="056f2-156">avaliação de lógica</span><span class="sxs-lookup"><span data-stu-id="056f2-156">logical evaluation</span></span>
  * <span data-ttu-id="056f2-157">efeito</span><span class="sxs-lookup"><span data-stu-id="056f2-157">effect</span></span>

<span data-ttu-id="056f2-158">saudação de exemplo a seguir mostra uma diretiva que limita quais recursos são implantados:</span><span class="sxs-lookup"><span data-stu-id="056f2-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="056f2-159">parâmetros</span><span class="sxs-lookup"><span data-stu-id="056f2-159">Parameters</span></span>
<span data-ttu-id="056f2-160">Usando parâmetros ajuda a simplificar o gerenciamento de política reduzindo Olá número de definições de política.</span><span class="sxs-lookup"><span data-stu-id="056f2-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="056f2-161">Definir uma política para uma propriedade de recurso (como limitar onde os recursos podem ser implantados de locais de saudação) e incluir parâmetros na definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="056f2-162">Em seguida, reutilize essa definição de política para diferentes cenários passando valores diferentes (por exemplo, a especificação de um conjunto de locais para uma assinatura) quando a atribuição de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="056f2-163">Declare parâmetros ao criar definições de política.</span><span class="sxs-lookup"><span data-stu-id="056f2-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="056f2-164">tipo de saudação de um parâmetro pode ser um cadeia de caracteres ou matriz.</span><span class="sxs-lookup"><span data-stu-id="056f2-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="056f2-165">propriedade de metadados de saudação é usada para as ferramentas como informações amigáveis toodisplay portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="056f2-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="056f2-166">Na regra de política de saudação, você fazer referência a parâmetros com hello sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="056f2-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="056f2-167">Nome de exibição e descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-167">Display name and description</span></span>

<span data-ttu-id="056f2-168">Use Olá **displayName** e **descrição** tooidentify Olá definição de política e fornecer contexto para quando ele é usado.</span><span class="sxs-lookup"><span data-stu-id="056f2-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="056f2-169">Regra de política</span><span class="sxs-lookup"><span data-stu-id="056f2-169">Policy rule</span></span>

<span data-ttu-id="056f2-170">regra de política de saudação consiste em **se** e **, em seguida,** blocos.</span><span class="sxs-lookup"><span data-stu-id="056f2-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="056f2-171">Em Olá **se** bloco, você define uma ou mais condições que especificam quando a política de saudação é imposta.</span><span class="sxs-lookup"><span data-stu-id="056f2-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="056f2-172">Você pode aplicar os operadores lógicos toothese condições tooprecisely definir cenário Olá para uma política.</span><span class="sxs-lookup"><span data-stu-id="056f2-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="056f2-173">Em Olá **, em seguida,** bloco, definir o efeito de saudação que acontece quando hello **se** condições sejam cumpridas.</span><span class="sxs-lookup"><span data-stu-id="056f2-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="056f2-174">Operadores lógicos</span><span class="sxs-lookup"><span data-stu-id="056f2-174">Logical operators</span></span>
<span data-ttu-id="056f2-175">operadores lógicos Olá com suporte são:</span><span class="sxs-lookup"><span data-stu-id="056f2-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="056f2-176">Olá **não** sintaxe inverte o resultado de saudação da condição de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="056f2-177">Olá **allOf** sintaxe (semelhante toohello lógica **e** operação) requer true de toobe todas as condições.</span><span class="sxs-lookup"><span data-stu-id="056f2-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="056f2-178">Olá **nenhum** sintaxe (semelhante toohello lógica **ou** operação) requer um ou mais true de toobe de condições.</span><span class="sxs-lookup"><span data-stu-id="056f2-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="056f2-179">Você pode aninhar operadores lógicos.</span><span class="sxs-lookup"><span data-stu-id="056f2-179">You can nest logical operators.</span></span> <span data-ttu-id="056f2-180">Olá mostrado no exemplo a seguir um **não** operação é aninhada dentro de uma **allOf** operação.</span><span class="sxs-lookup"><span data-stu-id="056f2-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="056f2-181">Condições</span><span class="sxs-lookup"><span data-stu-id="056f2-181">Conditions</span></span>
<span data-ttu-id="056f2-182">Olá condição avalia se um **campo** atenda a certos critérios.</span><span class="sxs-lookup"><span data-stu-id="056f2-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="056f2-183">condições de saudação com suporte são:</span><span class="sxs-lookup"><span data-stu-id="056f2-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="056f2-184">Ao usar o hello **como** condição, você pode fornecer um curinga (*) no valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="056f2-185">Ao usar o hello **corresponder** condição, fornecer `#` toorepresent um dígito, `?` para uma letra e qualquer outro caractere toorepresent esse caractere real.</span><span class="sxs-lookup"><span data-stu-id="056f2-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="056f2-186">Para obter exemplos, consulte [Aplicar políticas de recursos para nomes e texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="056f2-187">Campos</span><span class="sxs-lookup"><span data-stu-id="056f2-187">Fields</span></span>
<span data-ttu-id="056f2-188">As condições são formadas usando campos.</span><span class="sxs-lookup"><span data-stu-id="056f2-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="056f2-189">Um campo representa as propriedades na carga de solicitação de recurso de saudação que é o estado de saudação toodescribe usado do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="056f2-190">Olá campos a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="056f2-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="056f2-191">aliases de propriedade - para obter uma lista, confira [Aliases](#aliases).</span><span class="sxs-lookup"><span data-stu-id="056f2-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="056f2-192">Efeito</span><span class="sxs-lookup"><span data-stu-id="056f2-192">Effect</span></span>
<span data-ttu-id="056f2-193">A política dá suporte a três tipos de efeito - `deny`, `audit` e `append`.</span><span class="sxs-lookup"><span data-stu-id="056f2-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="056f2-194">**Negar** gera um evento no log de auditoria de saudação e falha de solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="056f2-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="056f2-195">**Auditoria** gera um evento de aviso no log de auditoria, mas não falha solicitação Olá</span><span class="sxs-lookup"><span data-stu-id="056f2-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="056f2-196">**Acrescentar** adiciona Olá definido pelo conjunto de campos toohello solicitação</span><span class="sxs-lookup"><span data-stu-id="056f2-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="056f2-197">Para **acrescentar**, você deve fornecer Olá detalhes a seguir:</span><span class="sxs-lookup"><span data-stu-id="056f2-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="056f2-198">valor de saudação pode ser uma cadeia de caracteres ou um objeto no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="056f2-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="056f2-199">Aliases</span><span class="sxs-lookup"><span data-stu-id="056f2-199">Aliases</span></span>

<span data-ttu-id="056f2-200">Você pode usar aliases tooaccess específico de propriedades para um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="056f2-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="056f2-201">Aliases permitem que você toorestrict quais valores ou condições são permitidas para uma propriedade em um recurso.</span><span class="sxs-lookup"><span data-stu-id="056f2-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="056f2-202">Cada alias mapeia toopaths em diferentes versões de API para um tipo de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="056f2-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="056f2-203">Durante a avaliação de política, o mecanismo de políticas de saudação obtém caminho da propriedade Olá para essa versão de API.</span><span class="sxs-lookup"><span data-stu-id="056f2-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="056f2-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="056f2-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="056f2-205">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-205">Alias</span></span> | <span data-ttu-id="056f2-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="056f2-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="056f2-208">Defina se da porta do servidor de Redis de não ssl hello (6379) está habilitado.</span><span class="sxs-lookup"><span data-stu-id="056f2-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="056f2-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="056f2-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="056f2-210">Definir o número de saudação de fragmentos toobe criado em um Cache de Cluster Premium.</span><span class="sxs-lookup"><span data-stu-id="056f2-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="056f2-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="056f2-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="056f2-212">Definir tamanho de saudação do hello Redis cache toodeploy.</span><span class="sxs-lookup"><span data-stu-id="056f2-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="056f2-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="056f2-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="056f2-214">Definir toouse família de SKU de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="056f2-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="056f2-216">Definir o tipo de saudação da Cache Redis toodeploy.</span><span class="sxs-lookup"><span data-stu-id="056f2-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="056f2-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="056f2-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="056f2-218">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-218">Alias</span></span> | <span data-ttu-id="056f2-219">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="056f2-221">Definir nome Olá Olá preço.</span><span class="sxs-lookup"><span data-stu-id="056f2-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="056f2-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="056f2-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="056f2-223">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-223">Alias</span></span> | <span data-ttu-id="056f2-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="056f2-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="056f2-226">Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="056f2-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="056f2-228">Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="056f2-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="056f2-230">Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="056f2-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="056f2-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="056f2-232">Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="056f2-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="056f2-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="056f2-234">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-234">Alias</span></span> | <span data-ttu-id="056f2-235">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="056f2-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="056f2-237">Identificador de saudação da máquina virtual do hello imagem usada toocreate saudação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="056f2-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="056f2-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="056f2-239">Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="056f2-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="056f2-241">Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="056f2-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="056f2-243">Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="056f2-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="056f2-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="056f2-245">Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="056f2-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="056f2-247">Defina essa imagem hello ou o disco está licenciado no local.</span><span class="sxs-lookup"><span data-stu-id="056f2-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="056f2-248">Esse valor é usado apenas para imagens que contêm o sistema de operacional de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="056f2-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="056f2-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="056f2-250">Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="056f2-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="056f2-252">Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="056f2-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="056f2-254">Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="056f2-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="056f2-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="056f2-256">Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="056f2-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="056f2-258">Defina o vhd Olá URI.</span><span class="sxs-lookup"><span data-stu-id="056f2-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="056f2-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="056f2-260">Definir tamanho de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="056f2-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="056f2-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="056f2-262">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-262">Alias</span></span> | <span data-ttu-id="056f2-263">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="056f2-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="056f2-265">Definir nome de saudação do editor da extensão hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="056f2-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="056f2-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="056f2-267">Definir o tipo de saudação da extensão.</span><span class="sxs-lookup"><span data-stu-id="056f2-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="056f2-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="056f2-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="056f2-269">Defina a versão de saudação da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="056f2-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="056f2-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="056f2-271">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-271">Alias</span></span> | <span data-ttu-id="056f2-272">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="056f2-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="056f2-274">Identificador de saudação da máquina virtual do hello imagem usada toocreate saudação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="056f2-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="056f2-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="056f2-276">Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="056f2-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="056f2-278">Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="056f2-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="056f2-280">Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="056f2-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="056f2-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="056f2-282">Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="056f2-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="056f2-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="056f2-284">Defina essa imagem hello ou o disco está licenciado no local.</span><span class="sxs-lookup"><span data-stu-id="056f2-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="056f2-285">Esse valor é usado apenas para imagens que contêm o sistema de operacional de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="056f2-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="056f2-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="056f2-287">Defina o prefixo do nome de computador Olá para todas as máquinas virtuais de saudação no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="056f2-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="056f2-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="056f2-289">Defina o URI do blob Olá para imagem do usuário.</span><span class="sxs-lookup"><span data-stu-id="056f2-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="056f2-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="056f2-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="056f2-291">Definir URLs de contêiner de saudação são discos do sistema operacional toostore usado para o conjunto de escala hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="056f2-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="056f2-293">Defina o tamanho de saudação de máquinas virtuais em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="056f2-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="056f2-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="056f2-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="056f2-295">Camada de saudação do conjunto de máquinas virtuais em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="056f2-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="056f2-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="056f2-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="056f2-297">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-297">Alias</span></span> | <span data-ttu-id="056f2-298">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="056f2-300">Definir tamanho de saudação do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="056f2-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="056f2-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="056f2-302">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-302">Alias</span></span> | <span data-ttu-id="056f2-303">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="056f2-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="056f2-305">Defina o tipo de saudação desse gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="056f2-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="056f2-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="056f2-307">Definir nome do SKU de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="056f2-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="056f2-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="056f2-309">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-309">Alias</span></span> | <span data-ttu-id="056f2-310">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="056f2-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="056f2-312">Defina a versão de saudação do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="056f2-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="056f2-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="056f2-314">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-314">Alias</span></span> | <span data-ttu-id="056f2-315">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="056f2-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="056f2-317">Definir a edição de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="056f2-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="056f2-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="056f2-319">Nome do conjunto de saudação do banco de dados de saudação do pool Elástico hello está em.</span><span class="sxs-lookup"><span data-stu-id="056f2-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="056f2-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="056f2-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="056f2-321">Olá conjunto configurado ID objetivo de nível de serviço de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="056f2-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="056f2-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="056f2-323">Nome do conjunto de saudação do hello configurado objetivo de nível de serviço de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="056f2-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="056f2-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="056f2-325">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-325">Alias</span></span> | <span data-ttu-id="056f2-326">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-327">servidores/elasticpools</span><span class="sxs-lookup"><span data-stu-id="056f2-327">servers/elasticpools</span></span> | <span data-ttu-id="056f2-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="056f2-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="056f2-329">Total de saudação do conjunto compartilhado DTU de pool Elástico de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="056f2-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="056f2-330">servidores/elasticpools</span><span class="sxs-lookup"><span data-stu-id="056f2-330">servers/elasticpools</span></span> | <span data-ttu-id="056f2-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="056f2-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="056f2-332">Definir a edição de saudação do pool Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="056f2-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="056f2-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="056f2-334">Alias</span><span class="sxs-lookup"><span data-stu-id="056f2-334">Alias</span></span> | <span data-ttu-id="056f2-335">Descrição</span><span class="sxs-lookup"><span data-stu-id="056f2-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="056f2-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="056f2-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="056f2-337">Camada de acesso de saudação conjunto usada para cobrança.</span><span class="sxs-lookup"><span data-stu-id="056f2-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="056f2-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="056f2-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="056f2-339">Nome do SKU de saudação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="056f2-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="056f2-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="056f2-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="056f2-341">Defina se o serviço Olá criptografa os dados de saudação conforme eles são armazenados no serviço de armazenamento de blob hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="056f2-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="056f2-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="056f2-343">Defina se o serviço de saudação criptografa os dados de saudação conforme eles são armazenados no serviço de armazenamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="056f2-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="056f2-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="056f2-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="056f2-345">Nome do SKU de saudação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="056f2-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="056f2-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="056f2-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="056f2-347">Configure serviço de toostorage de tráfego de https apenas tooallow.</span><span class="sxs-lookup"><span data-stu-id="056f2-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="056f2-348">Exemplos de políticas</span><span class="sxs-lookup"><span data-stu-id="056f2-348">Policy examples</span></span>

<span data-ttu-id="056f2-349">Olá tópicos a seguir contêm exemplos de política:</span><span class="sxs-lookup"><span data-stu-id="056f2-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="056f2-350">Para obter exemplos de políticas de marca, veja [Aplicar políticas de recursos para marcas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="056f2-351">Para obter exemplos de padrões de nomenclatura e texto, confira [Aplicar políticas de recursos a nomes e texto](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="056f2-352">Para obter exemplos de políticas de armazenamento, consulte [se aplicam a contas do recurso políticas toostorage](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="056f2-353">Para obter exemplos de políticas de máquina virtual, consulte [aplicar políticas de recursos tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) e [aplicar políticas de recursos tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="056f2-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="056f2-354">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="056f2-354">Next steps</span></span>
* <span data-ttu-id="056f2-355">Depois de definir uma regra de política, atribua-tooa escopo.</span><span class="sxs-lookup"><span data-stu-id="056f2-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="056f2-356">políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="056f2-357">políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="056f2-358">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="056f2-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="056f2-359">esquema de política de saudação é publicado em [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="056f2-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

