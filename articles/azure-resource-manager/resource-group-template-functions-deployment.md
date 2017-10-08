---
title: "funções de modelo do Gerenciador de recursos aaaAzure - implantação | Microsoft Docs"
description: "Descreve Olá funções toouse um informações de implantação do Azure Resource Manager modelo tooretrieve."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Funções de implantação para modelos do Azure Resource Manager 

Gerenciador de recursos fornece a seguinte Olá funções para obter valores de seções do modelo de saudação e valores relacionados toohello implantação:

* [implantação](#deployment)
* [parâmetros](#parameters)
* [variáveis](#variables)

tooget valores de recursos, grupos de recursos ou assinaturas, consulte [funções de recurso](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>implantação
`deployment()`

Retorna informações sobre a operação de implantação atual hello.

### <a name="return-value"></a>Valor de retorno

Esta função retorna o objeto Olá passado durante a implantação. propriedades Olá Olá retornada objeto diferem com base em se hello implantação objeto é passado como um link ou como um objeto na linha. Quando o objeto de implantação de saudação é passado na linha, como ao usar Olá **- TemplateFile** parâmetro no Azure PowerShell toopoint tooa arquivo local, Olá retornou objeto tem Olá formato a seguir:

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

Quando o objeto de saudação é passado como um link, como quando usando Olá **- TemplateUri** parâmetro toopoint tooa remoto do objeto, Olá objeto é retornado no hello formato a seguir: 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>Comentários

Você pode usar deployment() toolink tooanother modelo com base em Olá URI do modelo-Olá pai.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Exemplo

Olá, exemplo a seguir retorna o objeto de implantação hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

Olá, exemplo anterior retorna Olá objeto a seguir:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>parâmetros
`parameters(parameterName)`

Retorna um valor de parâmetro. nome do parâmetro especificado Olá deve ser definido na seção de parâmetros de saudação do modelo de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| parameterName |Sim |string |nome de saudação do hello tooreturn de parâmetro. |

### <a name="return-value"></a>Valor de retorno

valor Olá Olá especificado o parâmetro.

### <a name="remarks"></a>Comentários

Normalmente, você pode usar valores de parâmetros de recursos tooset. Olá exemplo a seguir define nome de saudação do valor de parâmetro do site da web toohello passado durante a implantação.

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>Exemplo

Olá, exemplo a seguir mostra um uso simplificado da função de parâmetros de saudação.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| stringOutput | Cadeia de caracteres | opção 1 |
| intOutput | int | 1 |
| objectOutput | Objeto | {"one": "a", "two": "b"} |
| arrayOutput | Matriz | [1, 2, 3] |
| crossOutput | Cadeia de caracteres | opção 1 |

<a id="variables" />

## <a name="variables"></a>variáveis
`variables(variableName)`

Retorna Olá valor da variável. Olá nome de variável especificado deve ser definido na seção de variáveis de saudação do modelo de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| variableName |Sim |Cadeia de caracteres |nome de saudação do tooreturn variável hello. |

### <a name="return-value"></a>Valor de retorno

valor Olá Olá especificado variável.

### <a name="remarks"></a>Comentários

Normalmente, você usa variáveis toosimplify seu modelo Criando valores complexos, apenas uma vez. Olá, exemplo a seguir constrói um nome exclusivo para uma conta de armazenamento.

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>Exemplo

modelo de exemplo Hello retorna valores de variável diferentes.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| exampleOutput1 | Cadeia de caracteres | myVariable |
| exampleOutput2 | Matriz | [1, 2, 3, 4] |
| exampleOutput3 | Cadeia de caracteres | myVariable |
| exampleOutput4 |  Objeto | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Próximas etapas
* Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).
* toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

