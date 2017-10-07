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
# <a name="assign-and-manage-resource-policies"></a>Atribuir e gerenciar políticas de recursos

tooimplement uma política, você deve executar estas etapas:

1. Verificar política definições (incluindo as políticas internas fornecidas pelo Azure) toosee se já existir em sua assinatura que atenda a seus requisitos.
2. Se existir, obtenha seu nome.
3. Se não existir, definir a regra de política de saudação com JSON e adicioná-lo como uma definição de política na sua assinatura. Essa etapa disponibiliza para atribuição de política hello, mas não se aplica a assinatura de tooyour regras hello.
4. Para ambos os casos, atribua o escopo de tooa política hello (como um assinatura ou grupo de recursos). regras de saudação da política de saudação agora são impostas.

Este artigo enfoca Olá etapas toocreate uma definição de política e atribuir esse escopo de tooa definição por meio da API REST, o PowerShell ou CLI do Azure. Se você preferir políticas de tooassign portal toouse hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md). Este artigo se concentra na sintaxe de Olá para criar a definição de política de saudação. Para obter informações sobre a sintaxe da política, confira [Visão geral da política de recursos](resource-manager-policy.md).

## <a name="rest-api"></a>API REST

### <a name="create-policy-definition"></a>Criar definição de política

Você pode criar uma política com hello [API REST para definições de política](/rest/api/resources/policydefinitions). Olá REST API permite que você toocreate e excluir definições de política e obter informações sobre as definições existentes.

toocreate uma definição de política, execute:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Inclua um toohello semelhante de corpo de solicitação exemplo a seguir:

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

### <a name="assign-policy"></a>Atribuir política

Você pode aplicar a definição de política de saudação no escopo de saudação desejado por meio de saudação [API REST para atribuições de política](/rest/api/resources/policyassignments). Olá REST API permite que você toocreate e excluir atribuições de política e obter informações sobre atribuições existentes.

toocreate uma atribuição de diretiva, execute:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Olá {atribuição de política} é o nome de saudação da atribuição de política de saudação.

Inclua um toohello semelhante de corpo de solicitação exemplo a seguir:

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

### <a name="view-policy"></a>Exibir política
tooget uma política, use Olá [obter a definição de política](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operação.

### <a name="get-aliases"></a>Obter aliases
Você pode recuperar os aliases a saudação API REST:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

saudação de exemplo a seguir mostra uma definição de um alias. Como é possível ver, um alias define caminhos em diferentes versões de API, mesmo quando há uma alteração de nome da propriedade. 

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

## <a name="powershell"></a>PowerShell

Antes de prosseguir com exemplos do PowerShell hello, verifique se você tem [instalado a versão mais recente do hello](/powershell/azure/install-azurerm-ps) do PowerShell do Azure. Parâmetros de política foram adicionados na versão 3.6.0. Se você tiver uma versão anterior, exemplos de saudação retornam que um parâmetro de saudação erro indicando que não foi encontrado.

### <a name="view-policy-definitions"></a>Exibir definições de políticas
toosee todas as definições de política na sua assinatura, use Olá a seguir de comando:

```powershell
Get-AzureRmPolicyDefinition
```

Ele retorna todas as definições de política disponíveis, incluindo políticas internas. Cada política é retornada no hello formato a seguir:

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

Antes de continuar toocreate uma definição de política, examine políticas internas hello. Se você encontrar uma diretiva interna que se aplica a limites de saudação que é necessário, você pode ignorar a criação de uma definição de política. Em vez disso, atribua escopo do hello diretiva interna toohello desejado.

### <a name="create-policy-definition"></a>Criar definição de política
Você pode criar uma definição de política usando Olá `New-AzureRmPolicyDefinition` cmdlet.

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

saudação de saída é armazenada em um `$definition` objeto, que é usado durante a atribuição de política. 

Em vez de especificar Olá JSON como um parâmetro, você pode fornecer o arquivo hello caminho tooa. JSON que contém a regra de política de saudação.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Olá, exemplo a seguir cria uma definição de política que inclui parâmetros:

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

### <a name="assign-policy"></a>Atribuir política

Aplicar política Olá no escopo de saudação desejado usando Olá `New-AzureRmPolicyAssignment` cmdlet. Olá exemplo a seguir atribui o grupo de recursos de tooa Olá política.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign uma política que exige os parâmetros, crie e objeto com esses valores. Olá exemplo a seguir recupera uma diretiva interna e passa os valores de parâmetros:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Exibir atribuição de política

tooget uma atribuição de política específica, use:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

regra de política tooview Olá para uma definição de política, use:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Remover atribuição de política 

tooremove uma atribuição de política, use:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>CLI do Azure

### <a name="view-policy-definitions"></a>Exibir definições de políticas
toosee todas as definições de política na sua assinatura, use Olá a seguir de comando:

```azurecli
az policy definition list
```

Ele retorna todas as definições de política disponíveis, incluindo políticas internas. Cada política é retornada no hello formato a seguir:

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

Antes de continuar toocreate uma definição de política, examine políticas internas hello. Se você encontrar uma diretiva interna que se aplica a limites de saudação que é necessário, você pode ignorar a criação de uma definição de política. Em vez disso, atribua escopo do hello diretiva interna toohello desejado.

### <a name="create-policy-definition"></a>Criar definição de política

Você pode criar uma definição de política usando a CLI do Azure com o comando de definição de política de saudação.

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

### <a name="assign-policy"></a>Atribuir política

Você pode aplicar o escopo da saudação política toohello desejado usando o comando de atribuição de política de saudação. saudação de exemplo a seguir atribui um grupo de recursos de tooa de política.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Exibir atribuição de política

tooview uma atribuição de diretiva, fornecer nome de atribuição de política hello e escopo de saudação:

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Remover atribuição de política 

tooremove uma atribuição de política, use:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Próximas etapas
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

