---
title: "aaaAssign e gerenciar políticas de recursos do Azure | Microsoft Docs"
description: "Descreve como tooapply Azure políticas toosubscriptions e o recurso grupos de recursos e como tooview políticas de recursos."
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
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="c9119-103">Atribuir e gerenciar políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="c9119-103">Assign and manage resource policies</span></span>

<span data-ttu-id="c9119-104">tooimplement uma política, você deve executar estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c9119-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="c9119-105">Verificar política definições (incluindo as políticas internas fornecidas pelo Azure) toosee se já existir em sua assinatura que atenda a seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="c9119-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="c9119-106">Se existir, obtenha seu nome.</span><span class="sxs-lookup"><span data-stu-id="c9119-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="c9119-107">Se não existir, definir a regra de política de saudação com JSON e adicioná-lo como uma definição de política na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c9119-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="c9119-108">Essa etapa disponibiliza para atribuição de política hello, mas não se aplica a assinatura de tooyour regras hello.</span><span class="sxs-lookup"><span data-stu-id="c9119-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="c9119-109">Para ambos os casos, atribua o escopo de tooa política hello (como um assinatura ou grupo de recursos).</span><span class="sxs-lookup"><span data-stu-id="c9119-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="c9119-110">regras de saudação da política de saudação agora são impostas.</span><span class="sxs-lookup"><span data-stu-id="c9119-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="c9119-111">Este artigo enfoca Olá etapas toocreate uma definição de política e atribuir esse escopo de tooa definição por meio da API REST, o PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9119-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="c9119-112">Se você preferir políticas de tooassign portal toouse hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9119-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c9119-113">Este artigo se concentra na sintaxe de Olá para criar a definição de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9119-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="c9119-114">Para obter informações sobre a sintaxe da política, confira [Visão geral da política de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c9119-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="c9119-115">API REST</span><span class="sxs-lookup"><span data-stu-id="c9119-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="c9119-116">Criar definição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-116">Create policy definition</span></span>

<span data-ttu-id="c9119-117">Você pode criar uma política com hello [API REST para definições de política](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="c9119-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="c9119-118">Olá REST API permite que você toocreate e excluir definições de política e obter informações sobre as definições existentes.</span><span class="sxs-lookup"><span data-stu-id="c9119-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="c9119-119">toocreate uma definição de política, execute:</span><span class="sxs-lookup"><span data-stu-id="c9119-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="c9119-120">Inclua um toohello semelhante de corpo de solicitação exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9119-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="c9119-121">Atribuir política</span><span class="sxs-lookup"><span data-stu-id="c9119-121">Assign policy</span></span>

<span data-ttu-id="c9119-122">Você pode aplicar a definição de política de saudação no escopo de saudação desejado por meio de saudação [API REST para atribuições de política](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="c9119-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="c9119-123">Olá REST API permite que você toocreate e excluir atribuições de política e obter informações sobre atribuições existentes.</span><span class="sxs-lookup"><span data-stu-id="c9119-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="c9119-124">toocreate uma atribuição de diretiva, execute:</span><span class="sxs-lookup"><span data-stu-id="c9119-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="c9119-125">Olá {atribuição de política} é o nome de saudação da atribuição de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9119-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="c9119-126">Inclua um toohello semelhante de corpo de solicitação exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9119-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="c9119-127">Exibir política</span><span class="sxs-lookup"><span data-stu-id="c9119-127">View policy</span></span>
<span data-ttu-id="c9119-128">tooget uma política, use Olá [obter a definição de política](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="c9119-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="c9119-129">Obter aliases</span><span class="sxs-lookup"><span data-stu-id="c9119-129">Get aliases</span></span>
<span data-ttu-id="c9119-130">Você pode recuperar os aliases a saudação API REST:</span><span class="sxs-lookup"><span data-stu-id="c9119-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="c9119-131">saudação de exemplo a seguir mostra uma definição de um alias.</span><span class="sxs-lookup"><span data-stu-id="c9119-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="c9119-132">Como é possível ver, um alias define caminhos em diferentes versões de API, mesmo quando há uma alteração de nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="c9119-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="c9119-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9119-133">PowerShell</span></span>

<span data-ttu-id="c9119-134">Antes de prosseguir com exemplos do PowerShell hello, verifique se você tem [instalado a versão mais recente do hello](/powershell/azure/install-azurerm-ps) do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9119-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="c9119-135">Parâmetros de política foram adicionados na versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="c9119-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="c9119-136">Se você tiver uma versão anterior, exemplos de saudação retornam que um parâmetro de saudação erro indicando que não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="c9119-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="c9119-137">Exibir definições de políticas</span><span class="sxs-lookup"><span data-stu-id="c9119-137">View policy definitions</span></span>
<span data-ttu-id="c9119-138">toosee todas as definições de política na sua assinatura, use Olá a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="c9119-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="c9119-139">Ele retorna todas as definições de política disponíveis, incluindo políticas internas.</span><span class="sxs-lookup"><span data-stu-id="c9119-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="c9119-140">Cada política é retornada no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9119-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="c9119-141">Antes de continuar toocreate uma definição de política, examine políticas internas hello.</span><span class="sxs-lookup"><span data-stu-id="c9119-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="c9119-142">Se você encontrar uma diretiva interna que se aplica a limites de saudação que é necessário, você pode ignorar a criação de uma definição de política.</span><span class="sxs-lookup"><span data-stu-id="c9119-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="c9119-143">Em vez disso, atribua escopo do hello diretiva interna toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="c9119-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="c9119-144">Criar definição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-144">Create policy definition</span></span>
<span data-ttu-id="c9119-145">Você pode criar uma definição de política usando Olá `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c9119-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
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

<span data-ttu-id="c9119-146">saudação de saída é armazenada em um `$definition` objeto, que é usado durante a atribuição de política.</span><span class="sxs-lookup"><span data-stu-id="c9119-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="c9119-147">Em vez de especificar Olá JSON como um parâmetro, você pode fornecer o arquivo hello caminho tooa. JSON que contém a regra de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9119-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="c9119-148">Olá, exemplo a seguir cria uma definição de política que inclui parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c9119-148">hello following example creates a policy definition that includes parameters:</span></span>

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
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="c9119-149">Atribuir política</span><span class="sxs-lookup"><span data-stu-id="c9119-149">Assign policy</span></span>

<span data-ttu-id="c9119-150">Aplicar política Olá no escopo de saudação desejado usando Olá `New-AzureRmPolicyAssignment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c9119-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="c9119-151">Olá exemplo a seguir atribui o grupo de recursos de tooa Olá política.</span><span class="sxs-lookup"><span data-stu-id="c9119-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="c9119-152">tooassign uma política que exige os parâmetros, crie e objeto com esses valores.</span><span class="sxs-lookup"><span data-stu-id="c9119-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="c9119-153">Olá exemplo a seguir recupera uma diretiva interna e passa os valores de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c9119-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="c9119-154">Exibir atribuição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-154">View policy assignment</span></span>

<span data-ttu-id="c9119-155">tooget uma atribuição de política específica, use:</span><span class="sxs-lookup"><span data-stu-id="c9119-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="c9119-156">regra de política tooview Olá para uma definição de política, use:</span><span class="sxs-lookup"><span data-stu-id="c9119-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="c9119-157">Remover atribuição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-157">Remove policy assignment</span></span> 

<span data-ttu-id="c9119-158">tooremove uma atribuição de política, use:</span><span class="sxs-lookup"><span data-stu-id="c9119-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="c9119-159">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c9119-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="c9119-160">Exibir definições de políticas</span><span class="sxs-lookup"><span data-stu-id="c9119-160">View policy definitions</span></span>
<span data-ttu-id="c9119-161">toosee todas as definições de política na sua assinatura, use Olá a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="c9119-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="c9119-162">Ele retorna todas as definições de política disponíveis, incluindo políticas internas.</span><span class="sxs-lookup"><span data-stu-id="c9119-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="c9119-163">Cada política é retornada no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9119-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
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

<span data-ttu-id="c9119-164">Antes de continuar toocreate uma definição de política, examine políticas internas hello.</span><span class="sxs-lookup"><span data-stu-id="c9119-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="c9119-165">Se você encontrar uma diretiva interna que se aplica a limites de saudação que é necessário, você pode ignorar a criação de uma definição de política.</span><span class="sxs-lookup"><span data-stu-id="c9119-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="c9119-166">Em vez disso, atribua escopo do hello diretiva interna toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="c9119-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="c9119-167">Criar definição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-167">Create policy definition</span></span>

<span data-ttu-id="c9119-168">Você pode criar uma definição de política usando a CLI do Azure com o comando de definição de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9119-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="c9119-169">Atribuir política</span><span class="sxs-lookup"><span data-stu-id="c9119-169">Assign policy</span></span>

<span data-ttu-id="c9119-170">Você pode aplicar o escopo da saudação política toohello desejado usando o comando de atribuição de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9119-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="c9119-171">saudação de exemplo a seguir atribui um grupo de recursos de tooa de política.</span><span class="sxs-lookup"><span data-stu-id="c9119-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="c9119-172">Exibir atribuição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-172">View policy assignment</span></span>

<span data-ttu-id="c9119-173">tooview uma atribuição de diretiva, fornecer nome de atribuição de política hello e escopo de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9119-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="c9119-174">Remover atribuição de política</span><span class="sxs-lookup"><span data-stu-id="c9119-174">Remove policy assignment</span></span> 

<span data-ttu-id="c9119-175">tooremove uma atribuição de política, use:</span><span class="sxs-lookup"><span data-stu-id="c9119-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="c9119-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9119-176">Next steps</span></span>
* <span data-ttu-id="c9119-177">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c9119-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

