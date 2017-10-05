---
title: "Atribuir e gerenciar políticas de recursos do Azure | Microsoft Docs"
description: "Descreve como aplicar as políticas de recursos do Azure a assinaturas e grupos de recursos e como exibir políticas de recursos."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="6660e-103">Atribuir e gerenciar políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="6660e-103">Assign and manage resource policies</span></span>

<span data-ttu-id="6660e-104">Para implantar uma política, é necessário executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6660e-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="6660e-105">Verifique as definições de política (incluindo políticas internas fornecidas pelo Azure) para saber se já existe na sua assinatura que atende aos requisitos.</span><span class="sxs-lookup"><span data-stu-id="6660e-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="6660e-106">Se existir, obtenha seu nome.</span><span class="sxs-lookup"><span data-stu-id="6660e-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="6660e-107">Se não, defina a regra de política com JSON e adicione-a como uma definição de política em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="6660e-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="6660e-108">Essa etapa disponibiliza a política para atribuição, mas não aplica as regras à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="6660e-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="6660e-109">Para qualquer caso, atribua a política a um escopo (como uma assinatura ou grupo de recursos).</span><span class="sxs-lookup"><span data-stu-id="6660e-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="6660e-110">As regras da política agora são impostas.</span><span class="sxs-lookup"><span data-stu-id="6660e-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="6660e-111">Este artigo ressalta as etapas para criação de uma definição de política e atribuição dessa definição a um escopo por meio da API REST, do PowerShell ou da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6660e-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="6660e-112">Se preferir usar o portal para atribuir políticas, consulte [Usar o portal do Azure para atribuir e gerenciar políticas de recurso](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6660e-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="6660e-113">Este artigo não tem como foco a sintaxe para criação da definição de política.</span><span class="sxs-lookup"><span data-stu-id="6660e-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="6660e-114">Para obter informações sobre a sintaxe da política, confira [Visão geral da política de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6660e-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="6660e-115">API REST</span><span class="sxs-lookup"><span data-stu-id="6660e-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="6660e-116">Criar definição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-116">Create policy definition</span></span>

<span data-ttu-id="6660e-117">Você pode criar uma política com a [API REST para Definições de Política](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="6660e-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="6660e-118">A API REST permite que você crie e exclua as definições de políticas e obtenha informações sobre as definições existentes.</span><span class="sxs-lookup"><span data-stu-id="6660e-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="6660e-119">Para criar uma definição de política, execute:</span><span class="sxs-lookup"><span data-stu-id="6660e-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="6660e-120">Inclua um corpo de solicitação semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6660e-120">Include a request body similar to the following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="6660e-121">Atribuir política</span><span class="sxs-lookup"><span data-stu-id="6660e-121">Assign policy</span></span>

<span data-ttu-id="6660e-122">Você pode aplicar a definição de política no escopo desejado por meio da [API REST para atribuições de política](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="6660e-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="6660e-123">A API REST permite que você crie e exclua as atribuições de políticas e obtenha informações sobre as atribuições existentes.</span><span class="sxs-lookup"><span data-stu-id="6660e-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="6660e-124">Para criar uma atribuição de política, execute:</span><span class="sxs-lookup"><span data-stu-id="6660e-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="6660e-125">A {Atribuição da política} é o nome da atribuição da política.</span><span class="sxs-lookup"><span data-stu-id="6660e-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="6660e-126">Inclua um corpo de solicitação semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6660e-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="6660e-127">Exibir política</span><span class="sxs-lookup"><span data-stu-id="6660e-127">View policy</span></span>
<span data-ttu-id="6660e-128">Para obter uma política, use a operação [Obter definição de política](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get).</span><span class="sxs-lookup"><span data-stu-id="6660e-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="6660e-129">Obter aliases</span><span class="sxs-lookup"><span data-stu-id="6660e-129">Get aliases</span></span>
<span data-ttu-id="6660e-130">Você pode recuperar aliases por meio da API REST:</span><span class="sxs-lookup"><span data-stu-id="6660e-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="6660e-131">O exemplo a seguir mostra uma definição de um alias.</span><span class="sxs-lookup"><span data-stu-id="6660e-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="6660e-132">Como é possível ver, um alias define caminhos em diferentes versões de API, mesmo quando há uma alteração de nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="6660e-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="6660e-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6660e-133">PowerShell</span></span>

<span data-ttu-id="6660e-134">Antes de continuar com os exemplos do PowerShell, verifique se você tem [instalada a versão mais recente](/powershell/azure/install-azurerm-ps) do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6660e-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="6660e-135">Parâmetros de política foram adicionados na versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="6660e-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="6660e-136">Se você tiver uma versão mais antiga, os exemplos retornam um erro indicando que o parâmetro não pode ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="6660e-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="6660e-137">Exibir definições de políticas</span><span class="sxs-lookup"><span data-stu-id="6660e-137">View policy definitions</span></span>
<span data-ttu-id="6660e-138">Para visualizar todas as definições de política em sua assinatura, utilize o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6660e-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="6660e-139">Ele retorna todas as definições de política disponíveis, incluindo políticas internas.</span><span class="sxs-lookup"><span data-stu-id="6660e-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="6660e-140">Cada política é retornada no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="6660e-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="6660e-141">Antes de continuar a criar uma definição de política, observe as políticas internas.</span><span class="sxs-lookup"><span data-stu-id="6660e-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="6660e-142">Se você encontrar uma política interna que aplica os limites necessários, você poderá ignorar a criação de uma definição de política.</span><span class="sxs-lookup"><span data-stu-id="6660e-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="6660e-143">Em vez disso, atribua a política interna ao escopo desejado.</span><span class="sxs-lookup"><span data-stu-id="6660e-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="6660e-144">Criar definição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-144">Create policy definition</span></span>
<span data-ttu-id="6660e-145">Você pode criar uma definição de política usando o cmdlet `New-AzureRmPolicyDefinition`.</span><span class="sxs-lookup"><span data-stu-id="6660e-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

<span data-ttu-id="6660e-146">A saída é armazenada em um objeto `$definition`, que é usado durante a atribuição da política.</span><span class="sxs-lookup"><span data-stu-id="6660e-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="6660e-147">Em vez de especificar o JSON como um parâmetro, você pode fornecer o caminho para um arquivo .json que contém a regra de política.</span><span class="sxs-lookup"><span data-stu-id="6660e-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="6660e-148">O exemplo a seguir cria uma definição de política que inclui parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6660e-148">The following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="6660e-149">Atribuir política</span><span class="sxs-lookup"><span data-stu-id="6660e-149">Assign policy</span></span>

<span data-ttu-id="6660e-150">Aplique a política no escopo desejado usando o cmdlet `New-AzureRmPolicyAssignment`.</span><span class="sxs-lookup"><span data-stu-id="6660e-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="6660e-151">O exemplo a seguir atribui a política a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6660e-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="6660e-152">Para atribuir uma política que requer parâmetros, crie e objete com esses valores.</span><span class="sxs-lookup"><span data-stu-id="6660e-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="6660e-153">O seguinte exemplo recupera uma política interna e passa em valores de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6660e-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="6660e-154">Exibir atribuição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-154">View policy assignment</span></span>

<span data-ttu-id="6660e-155">Para obter uma atribuição de política específica, use:</span><span class="sxs-lookup"><span data-stu-id="6660e-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="6660e-156">Para exibir a regra de política de uma definição de política, use:</span><span class="sxs-lookup"><span data-stu-id="6660e-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="6660e-157">Remover atribuição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-157">Remove policy assignment</span></span> 

<span data-ttu-id="6660e-158">Para remover uma atribuição de política, use:</span><span class="sxs-lookup"><span data-stu-id="6660e-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="6660e-159">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6660e-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="6660e-160">Exibir definições de políticas</span><span class="sxs-lookup"><span data-stu-id="6660e-160">View policy definitions</span></span>
<span data-ttu-id="6660e-161">Para visualizar todas as definições de política em sua assinatura, utilize o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6660e-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="6660e-162">Ele retorna todas as definições de política disponíveis, incluindo políticas internas.</span><span class="sxs-lookup"><span data-stu-id="6660e-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="6660e-163">Cada política é retornada no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="6660e-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="6660e-164">Antes de continuar a criar uma definição de política, observe as políticas internas.</span><span class="sxs-lookup"><span data-stu-id="6660e-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="6660e-165">Se você encontrar uma política interna que aplica os limites necessários, você poderá ignorar a criação de uma definição de política.</span><span class="sxs-lookup"><span data-stu-id="6660e-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="6660e-166">Em vez disso, atribua a política interna ao escopo desejado.</span><span class="sxs-lookup"><span data-stu-id="6660e-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="6660e-167">Criar definição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-167">Create policy definition</span></span>

<span data-ttu-id="6660e-168">Você pode criar uma definição de política usando a CLI do Azure com o comando de definição de política.</span><span class="sxs-lookup"><span data-stu-id="6660e-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="6660e-169">Atribuir política</span><span class="sxs-lookup"><span data-stu-id="6660e-169">Assign policy</span></span>

<span data-ttu-id="6660e-170">Você pode aplicar a política para o escopo desejado usando o comando de atribuição de política.</span><span class="sxs-lookup"><span data-stu-id="6660e-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="6660e-171">O exemplo a seguir atribui uma política a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6660e-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="6660e-172">Exibir atribuição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-172">View policy assignment</span></span>

<span data-ttu-id="6660e-173">Para exibir uma atribuição de política, forneça o nome da atribuição de política e o escopo:</span><span class="sxs-lookup"><span data-stu-id="6660e-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="6660e-174">Remover atribuição de política</span><span class="sxs-lookup"><span data-stu-id="6660e-174">Remove policy assignment</span></span> 

<span data-ttu-id="6660e-175">Para remover uma atribuição de política, use:</span><span class="sxs-lookup"><span data-stu-id="6660e-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="6660e-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6660e-176">Next steps</span></span>
* <span data-ttu-id="6660e-177">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6660e-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

