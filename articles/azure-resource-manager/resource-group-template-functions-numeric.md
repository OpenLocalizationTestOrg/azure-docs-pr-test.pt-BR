---
title: "funções de modelo Gerenciador de recursos aaaAzure - numéricas | Microsoft Docs"
description: "Descreve Olá toouse de funções em um toowork de modelo do Gerenciador de recursos do Azure com números."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Funções numéricas para modelos do Azure Resource Manager

Gerenciador de recursos fornece Olá seguintes funções para trabalhar com números inteiros:

* [adicionar](#add)
* [copyIndex](#copyindex)
* [div](#div)
* [float](#float)
* [int](#int)
* [min](#min)
* [max](#max)
* [mod](#mod)
* [mul](#mul)
* [sub](#sub)

<a id="add" />

## <a name="add"></a>adicionar
`add(operand1, operand2)`

Retorna Olá soma de números inteiros de fornecido hello.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- | 
|operand1 |Sim |int |Primeiro número tooadd. |
|operand2 |Sim |int |Segundo tooadd número. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que contém a soma de saudação de parâmetros de saudação.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir adiciona dois parâmetros.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Retorna Olá índice de um loop de iteração. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| loopName | Não | string | nome de saudação de loop Olá para obtenção de iteração de saudação. |
| deslocamento |Não |int |Olá valor numérico de tooadd toohello iteração com base em zero. |

### <a name="remarks"></a>Comentários

Essa função é sempre usada com um objeto **copy** . Se nenhum valor for fornecido para **deslocamento**, o valor de iteração atual Olá é retornado. valor de iteração Olá começa em zero.

Olá **loopName** propriedade permite que você toospecify se copyIndex se refere a iteração de recurso tooa ou iteração de propriedade. Se nenhum valor for fornecido para **loopName**, Olá atual iteração de tipo de recurso é usada. Forneça um valor para **loopName** durante a iteração em uma propriedade. 
 
Para obter uma descrição completa de como usar **copyIndex**, confira [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra um loop e hello índice valor cópia incluído no nome de saudação. 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa o índice de iteração Olá atual hello.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

Retorna Olá divisão de dois inteiros de fornecido hello.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| operand1 |Sim |int |número de Hello está sendo dividido. |
| operand2 |Sim |int |Olá número toodivide usado. Não pode ser 0. |

### <a name="return-value"></a>Valor de retorno

Divisão de saudação representando um inteiro.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir divide um parâmetro por outro parâmetro.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>flutuante
`float(arg1)`

Converte Olá valor tooa número de ponto flutuante. Você só usar essa função ao passar parâmetros personalizados tooan aplicativo, como um aplicativo lógico.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |string ou int |Olá valor tooconvert tooa número de ponto flutuante. |

### <a name="return-value"></a>Valor de retorno
Um número de ponto flutuante.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como toouse float toopass parâmetros tooa lógica de aplicativo:

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a>int
`int(valueToConvert)`

Converte o inteiro de tooan Olá valor especificado.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| valueToConvert |Sim |string ou int |inteiro de tooan tooconvert do valor Hello. |

### <a name="return-value"></a>Valor de retorno

Um inteiro de valor Olá convertido.

### <a name="example"></a>Exemplo

Olá, exemplo a seguir converte Olá toointeger de valor de parâmetro fornecido pelo usuário.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>Min
`min (arg1)`

Retorna Olá valor mínimo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz de inteiros ou lista de inteiros separados por vírgulas |Olá coleção tooget Olá valor mínimo. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa o valor mínimo da coleção de saudação.

### <a name="example"></a>Exemplo

Olá mostrado no exemplo a seguir como min toouse com uma matriz e uma lista de números inteiros:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max (arg1)`

Retorna Olá valor máximo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz de inteiros ou lista de inteiros separados por vírgulas |Olá coleção tooget Olá valor máximo. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa o valor máximo de saudação da coleção de saudação.

### <a name="example"></a>Exemplo

Olá mostrado no exemplo a seguir como toouse max com uma matriz e uma lista de números inteiros:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Retorna o resto de saudação de divisão hello usando números inteiros de fornecido hello.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| operand1 |Sim |int |número de Hello está sendo dividido. |
| operand2 |Sim |int |número de saudação toodivide usado, não pode ser 0. |

### <a name="return-value"></a>Valor de retorno
Um resto Olá representando inteiro.

### <a name="example"></a>Exemplo

Olá, exemplo a seguir retorna Olá resto da divisão de um parâmetro por outro parâmetro.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Retorna Olá multiplicação de dois inteiros de fornecido hello.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| operand1 |Sim |int |Primeiro número toomultiply. |
| operand2 |Sim |int |Segundo toomultiply número. |

### <a name="return-value"></a>Valor de retorno

Multiplicação de saudação representando um número inteiro.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir multiplica um parâmetro por outro parâmetro.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>sub
`sub(operand1, operand2)`

Retorna Olá subtração dos números inteiros de fornecido hello.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| operand1 |Sim |int |número de saudação que é subtraído. |
| operand2 |Sim |int |número de saudação que é subtraído. |

### <a name="return-value"></a>Valor de retorno
Subtração de saudação representando um número inteiro.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir subtrai um parâmetro de outro parâmetro.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Próximas etapas
* Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).
* toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

