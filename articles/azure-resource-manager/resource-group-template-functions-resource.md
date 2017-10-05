---
title: "Funções de modelo do Azure Resource Manager – recursos | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Azure Resource Manager para recuperar valores sobre recursos."
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
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funções de recursos para modelos do Azure Resource Manager

O Gerenciador de Recursos fornece as seguintes funções para obter valores de recurso:

* [listKeys e list{Value}](#listkeys)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscription](#subscription)

Para obter valores de parâmetros, de variáveis ou da implantação atual, veja [Funções de valor de implantação](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys e list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Retorna os valores para qualquer tipo de recurso que ofereça suporte à operação de lista. O uso mais comum é `listKeys`. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| resourceName ou resourceIdentifier |Sim |string |Identificador exclusivo para o recurso. |
| apiVersion |Sim |string |Versão de API do estado de tempo de execução do recurso. Normalmente, no formato **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor de retorno

O objeto retornado de listKeys tem o seguinte formato:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Outras funções de lista têm formatos diferentes de retorno. Para ver o formato de uma função, inclua-a na seção de saídas, conforme mostra o exemplo de modelo. 

### <a name="remarks"></a>Comentários

Qualquer operação que começa com **list** pode ser usada como uma função no seu modelo. As operações disponíveis não incluem apenas listKeys, mas também operações como `list`, `listAdminKeys` e `listStatus`. No entanto, você não pode usar **lista** as operações que exigem valores no corpo da solicitação. Por exemplo, o [lista conta SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operação requer parâmetros de corpo de solicitação como *signedExpiry*, portanto, você não pode usá-lo em um modelo.

Para determinar quais tipos de recursos têm uma operação de lista, use as seguintes opções:

* Veja as [operações da API REST](/rest/api/) de um provedor de recursos e procure por operações de lista. Por exemplo, as contas de armazenamento têm a [operação listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Use o cmdlet do PowerShell [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation). O exemplo a seguir obtém todas as operações de lista de contas de armazenamento:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Use o seguinte comando da CLI do Azure para filtrar apenas as operações de lista:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Especifique o recurso usando a [função resourceId](#resourceid) ou o formato `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Exemplo

O exemplo a seguir mostra como retornar as chaves primárias e secundárias de uma conta de armazenamento na seção de saídas.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>providers
`providers(providerNamespace, [resourceType])`

Retorna informações sobre um provedor de recursos e seus tipos de recursos com suporte. Se você não fornecer um tipo de recurso, a função retornará todos os tipos com suporte para o provedor de recursos.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| providerNamespace |Sim |string |Namespace do provedor |
| resourceType |Não |string |O tipo de recurso no namespace especificado. |

### <a name="return-value"></a>Valor de retorno

Cada tipo com suporte é retornado no seguinte formato: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

A ordenação de matriz dos valores retornados não é garantida.

### <a name="example"></a>Exemplo

O exemplo a seguir mostra como usar a função provider:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

O exemplo anterior retorna um objeto no seguinte formato:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

Retorna um objeto que representa o estado de tempo de execução de um recurso.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| resourceName ou resourceIdentifier |Sim |string |Nome ou identificador exclusivo de um recurso. |
| apiVersion |Não |string |Versão da API do recurso especificado. Inclua esse parâmetro quando o recurso não estiver provisionado no mesmo modelo. Normalmente, no formato **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor de retorno

Cada tipo de recurso retorna propriedades diferentes para a função de referência. A função não retorna um único formato predefinido. Para ver as propriedades de um tipo de recurso, retorne o objeto na seção de saída, conforme mostra o exemplo.

### <a name="remarks"></a>Comentários

A função de referência deriva seu valor de um estado de tempo de execução e, portanto, não pode ser usada na seção de variáveis. Ela pode ser usada na seção de saídas de um modelo. 

Usando a função de referência, você declara implicitamente que um recurso depende de outro recurso se o recurso referenciado é provisionado no mesmo modelo. Você não precisa usar a propriedade dependsOn também. A função não é avaliada até que o recurso referenciado conclua a implantação.

Para ver os valores e nomes de propriedade para um tipo de recurso, crie um modelo que retorne o objeto na seção de saídas . Se você tiver um recurso existente desse tipo, o modelo retornará o objeto sem implantar qualquer recurso. 

Normalmente, você usa a função **reference** para retornar um valor específico de um objeto, como o URI do ponto de extremidade de blob ou o nome de domínio totalmente qualificado.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Exemplo

Para implantar e fazer referência ao recurso no mesmo modelo, use:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

O exemplo anterior retorna um objeto no seguinte formato:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

O exemplo a seguir faz referência a uma conta de armazenamento implantada nesse modelo. A conta de armazenamento já existe dentro do mesmo grupo de recursos.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Retorna um objeto que representa o grupo de recursos atual. 

### <a name="return-value"></a>Valor de retorno

O objeto retornado está no seguinte formato:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Comentários

Um uso comum da função resourceGroup é criar recursos no mesmo local que o grupo de recursos. O exemplo a seguir usa o local do grupo de recursos para atribuir o local de um site Web.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Exemplo

O modelo a seguir retorna as propriedades do grupo de recursos.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

O exemplo anterior retorna um objeto no seguinte formato:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Retorna o identificador exclusivo de um recurso. Você pode usar essa função quando o nome do recurso é ambíguo ou não provisionado no mesmo modelo. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| subscriptionId |Não |string (no formato GUID) |O valor padrão é a assinatura atual. Especifique esse valor quando você precisar recuperar um recurso em outra assinatura. |
| resourceGroupName |Não |string |O valor padrão é o grupo de recursos atual. Especifique esse valor quando você precisar recuperar um recurso em outro grupo de recursos. |
| resourceType |Sim |string |Tipo de recurso, incluindo o namespace do provedor de recursos. |
| resourceName1 |Sim |string |Nome do recurso. |
| resourceName2 |Não |string |Próximo segmento de nome do recurso se o recurso está aninhado. |

### <a name="return-value"></a>Valor de retorno

O identificador é retornado no seguinte formato:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Comentários

Os valores de parâmetro que você especifica dependem se o recurso está na mesma assinatura e grupo de recursos que a implantação atual.

Para obter a ID de recurso de uma conta de armazenamento na mesma assinatura e grupo de recursos, use:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

Para obter a ID de recurso de uma conta de armazenamento na mesma assinatura, mas em um grupo de recursos diferente, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Para obter a ID de recurso de uma conta de armazenamento em uma assinatura e grupo de recursos diferentes, use:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Para obter a ID de recurso para um banco de dados em um grupo de recursos diferente, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Frequentemente, você precisa usar essa função ao usar uma conta de armazenamento ou rede virtual em um grupo de recursos alternativo. O exemplo a seguir mostra como um recurso de um grupo de recursos externo pode ser facilmente usado:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Exemplo

O exemplo a seguir retorna a ID de recurso de uma conta de armazenamento no grupo de recursos:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

A saída do exemplo anterior com os valores padrão é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| sameRGOutput | Cadeia de caracteres | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Cadeia de caracteres | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Cadeia de caracteres | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Cadeia de caracteres | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subscription
`subscription()`

Retorna detalhes sobre a assinatura da implantação atual. 

### <a name="return-value"></a>Valor de retorno

A função retorna o seguinte formato:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Exemplo

O exemplo a seguir mostra a função de assinatura chamada na seção de saídas. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Próximas etapas
* Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).
* Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).
* Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

