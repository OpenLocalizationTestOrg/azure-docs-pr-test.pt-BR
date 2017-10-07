---
title: "funções de modelo do Gerenciador de recursos aaaAzure - recursos | Microsoft Docs"
description: "Descreve Olá toouse de funções em valores do Azure Resource Manager modelo tooretrieve sobre os recursos."
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
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funções de recursos para modelos do Azure Resource Manager

Gerenciador de recursos fornece Olá funções para obter valores de recursos a seguir:

* [listKeys e list{Value}](#listkeys)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscription](#subscription)

tooget valores de parâmetros, variáveis ou implantação atual do hello, consulte [funções com valor de implantação](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys e list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Retorna Olá valores para qualquer tipo de recurso que dá suporte à operação de lista de saudação. Olá o uso mais comum é `listKeys`. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| resourceName ou resourceIdentifier |Sim |string |Identificador exclusivo para o recurso de saudação. |
| apiVersion |Sim |string |Versão de API do estado de tempo de execução do recurso. Normalmente, no formato de saudação **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor de retorno

Olá retornou objeto do listkeys do tem Olá formato a seguir:

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

Outras funções de lista têm formatos diferentes de retorno. formato de saudação toosee de uma função, incluí-lo na seção de saídas Olá conforme mostrado no modelo de exemplo hello. 

### <a name="remarks"></a>Comentários

Qualquer operação que começa com **list** pode ser usada como uma função no seu modelo. Olá, as operações disponíveis incluem não só listkeys do, mas também operações como `list`, `listAdminKeys`, e `listStatus`. No entanto, você não pode usar **lista** as operações que exigem valores hello corpo da solicitação. Por exemplo, Olá [SAS de conta da lista](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operação requer parâmetros de corpo de solicitação como *signedExpiry*, portanto, você não pode usá-lo em um modelo.

toodetermine quais tipos de recursos tem uma operação de lista, você tem Olá as opções a seguir:

* Saudação de exibição [operações da API REST](/rest/api/) para um provedor de recursos e procure por operações de lista. Por exemplo, contas de armazenamento tem Olá [operação do listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Saudação de uso [AzureRmProviderOperation Get](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet do PowerShell. Olá, exemplo a seguir obtém todas as operações de lista de contas de armazenamento:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Use Olá comando CLI do Azure toofilter Olá somente operações de lista a seguir:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Especificar recursos hello usando qualquer Olá [função resourceId](#resourceid), ou o formato de saudação `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra como tooreturn Olá primários e secundários as chaves de conta de armazenamento no hello saídas de seção.

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

Retorna informações sobre um provedor de recursos e seus tipos de recursos com suporte. Se você não fornecer um tipo de recurso, a função hello retorna todos os tipos de Olá com suporte para provedor de recursos de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| providerNamespace |Sim |string |Namespace do provedor de saudação |
| resourceType |Não |string |tipo de saudação do recurso na saudação especificado namespace. |

### <a name="return-value"></a>Valor de retorno

Cada tipo com suporte é retornado no hello formato a seguir: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Ordenação de matriz de saudação retornado valores não é garantida.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como toouse Olá a função do provedor:

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

Olá exemplo anterior retorna um objeto no hello formato a seguir:

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
| apiVersion |Não |string |Versão de API do hello o recurso especificado. Inclua esse parâmetro quando o recurso de saudação não está provisionado no mesmo modelo. Normalmente, no formato de saudação **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor de retorno

Cada tipo de recurso retorna propriedades diferentes para a função de referência de saudação. função Hello não retorna um único formato predefinido. Propriedades de saudação toosee para um tipo de recurso, retornar objeto Olá Olá gera seção conforme mostrado no exemplo hello.

### <a name="remarks"></a>Comentários

função de referência Olá deriva seu valor de um estado de tempo de execução e, portanto, não pode ser usada na seção de variáveis de saudação. Ela pode ser usada na seção de saídas de um modelo. 

Usando a função de referência hello, você implicitamente declarar que um recurso depende de outro recurso se o recurso Olá referenciado é provisionado no mesmo modelo. Propriedade do tooalso use Olá dependsOn não é necessário. Olá função não será avaliada até hello recurso referenciado tiver concluído a implantação.

toosee Olá nomes e valores de um tipo de recurso, criar um modelo que retorna o objeto de Olá Olá saídas de seção. Se você tiver um recurso existente do mesmo tipo, o modelo retorna objeto Olá sem implantar os novos recursos. 

Normalmente, você usa Olá **referência** função tooreturn um valor específico de um objeto, como o ponto de extremidade de blob de saudação URI ou o nome de domínio totalmente qualificado.

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

toodeploy e referência de recurso de saudação em Olá mesmo modelo, use:

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

Olá exemplo anterior retorna um objeto no hello formato a seguir:

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

Olá exemplo a seguir faz referência a uma conta de armazenamento que não foi implantada nesse modelo. Olá conta de armazenamento já existe no hello mesmo grupo de recursos.

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

Retorna um objeto que representa o grupo de recursos atual hello. 

### <a name="return-value"></a>Valor de retorno

Olá retornou objeto está em Olá formato a seguir:

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

Um uso comum da função de resourceGroup Olá é toocreate recursos Olá mesmo local que o grupo de recursos de saudação. Olá exemplo a seguir usa Olá recurso grupo tooassign Olá local para um site da web.

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

Olá modelo a seguir retorna propriedades de Olá Olá do grupo de recursos.

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

Olá exemplo anterior retorna um objeto no hello formato a seguir:

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

Retorna Olá identificador exclusivo de um recurso. Usar essa função quando o nome do recurso de saudação é ambíguo ou não provisionado em Olá mesmo modelo. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| subscriptionId |Não |string (no formato GUID) |Valor padrão é assinatura atual hello. Especifique esse valor quando precisar tooretrieve um recurso em outra assinatura. |
| resourceGroupName |Não |string |O valor padrão é o grupo de recursos atual. Especifique esse valor quando precisar tooretrieve um recurso em outro grupo de recursos. |
| resourceType |Sim |string |Tipo de recurso, incluindo o namespace do provedor de recursos. |
| resourceName1 |Sim |string |Nome do recurso. |
| resourceName2 |Não |string |Próximo segmento de nome do recurso se o recurso está aninhado. |

### <a name="return-value"></a>Valor de retorno

Identificador de saudação é retornado no hello formato a seguir:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Comentários

Olá valores de parâmetro especificados dependem se o recurso de saudação é em hello mesmo grupo de assinatura e o recurso de implantação atual hello.

ID de recurso de saudação tooget para uma conta de armazenamento Olá mesmo assinatura e grupo de recursos, use:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID de recurso Olá tooget para uma conta de armazenamento Olá mesma assinatura, mas um grupo de recursos diferente, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID do recurso Olá tooget para uma conta de armazenamento em uma assinatura diferente e o grupo de recursos, use:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID do recurso Olá tooget para um banco de dados em um grupo de recursos diferente, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Geralmente, é necessário toouse essa função ao usar uma conta de armazenamento ou a rede virtual em um grupo de recurso alternativo. Olá exemplo a seguir mostra como um recurso de um grupo de recursos externos pode ser facilmente usado:

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

Olá exemplo a seguir retorna ID de recurso Olá para uma conta de armazenamento no grupo de recursos de saudação:

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

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| sameRGOutput | Cadeia de caracteres | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Cadeia de caracteres | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Cadeia de caracteres | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Cadeia de caracteres | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subscription
`subscription()`

Retorna detalhes sobre assinatura Olá para implantação de saudação atual. 

### <a name="return-value"></a>Valor de retorno

função Hello retorna Olá formato a seguir:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra função de assinatura hello chamada hello saídas de seção. 

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
* Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).
* toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

