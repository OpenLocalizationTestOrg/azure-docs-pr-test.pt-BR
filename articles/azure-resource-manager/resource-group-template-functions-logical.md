---
title: "funções de modelo Gerenciador de recursos aaaAzure - lógicas | Microsoft Docs"
description: "Descreve Olá toouse de funções em valores lógicos do modelo toodetermine um Gerenciador de recursos do Azure."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Funções lógicas para modelos do Azure Resource Manager

O Resource Manager fornece várias funções para fazer comparações em seus modelos.

* [and](#and)
* [bool](#bool)
* [if](#if)
* [not](#not)
* [or](#or)

## <a name="and"></a>e
`and(arg1, arg2)`

Verifica se os dois valores de parâmetro são verdadeiros.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |Booliano |Olá primeiro toocheck de valor se for verdadeira. |
| arg2 |Sim |Booliano |Olá toocheck do segundo valor se for verdadeira. |

### <a name="return-value"></a>Valor de retorno

Retorna **True** se os dois valores forem verdadeiros; caso contrário, **False**.

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como toouse as funções lógicas.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

saída Olá Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | Bool | Falso |
| orExampleOutput | Bool | Verdadeiro |
| notExampleOutput | Bool | Falso |


## <a name="bool"></a>bool
`bool(arg1)`

Converte Olá tooa parâmetro booliano.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |string ou int |Olá tooa de tooconvert de valor booliano. |

### <a name="return-value"></a>Valor de retorno
Um valor booleano da saudação converter valor.

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como toouse bool com uma cadeia de caracteres ou um inteiro.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| trueString | Bool | True  |
| falseString | Bool | Falso |
| trueInt | Bool | True  |
| falseInt | Bool | Falso |

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

Retorna um valor com base em se uma condição é verdadeira ou falsa.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| condition |Sim |Booliano |Olá toocheck valor se for verdadeiro. |
| trueValue |Sim | cadeia de caracteres, inteiro, objeto ou matriz |Olá valor tooreturn quando Olá condição for verdadeira. |
| falseValue |Sim | cadeia de caracteres, inteiro, objeto ou matriz |Olá valor tooreturn quando Olá condição for falsa. |

### <a name="return-value"></a>Valor de retorno

Retorna o segundo parâmetro quando o primeiro parâmetro é **True**; caso contrário, retorna o terceiro parâmetro.

### <a name="remarks"></a>Comentários

Você pode usar esse conjunto de tooconditionally de função uma propriedade de recurso. Olá exemplo a seguir não é um modelo completo, mas ele mostra as partes relevantes de saudação para definir o conjunto de disponibilidade Olá condicionalmente.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como toouse Olá `if` função.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

saída Olá Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| yesOutput | Cadeia de caracteres | sim |
| noOutput | Cadeia de caracteres | não |


## <a name="not"></a>não
`not(arg1)`

Converte o valor booliano tooits oposta valor.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |Booliano |Olá tooconvert de valor. |


### <a name="return-value"></a>Valor de retorno

Retorna **True** quando o parâmetro é **False**. Retorna **False** quando o parâmetro é **True**.

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como toouse as funções lógicas.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

saída Olá Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | Bool | Falso |
| orExampleOutput | Bool | Verdadeiro |
| notExampleOutput | Bool | Falso |

Olá exemplo a seguir usa **não** com [é igual a](resource-group-template-functions-comparison.md#equals).

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

saída Olá Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkNotEquals | Bool | Verdadeiro |


## <a name="or"></a>ou o
`or(arg1, arg2)`

Verifica se o valor do parâmetro é true.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |Booliano |Olá primeiro toocheck de valor se for verdadeira. |
| arg2 |Sim |Booliano |Olá toocheck do segundo valor se for verdadeira. |

### <a name="return-value"></a>Valor de retorno

Retorna **True** se qualquer valor é verdadeiro; caso contrário, **False**.

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como toouse as funções lógicas.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

saída Olá Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | Bool | Falso |
| orExampleOutput | Bool | Verdadeiro |
| notExampleOutput | Bool | Falso |


## <a name="next-steps"></a>Próximas etapas
* Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).
* toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

