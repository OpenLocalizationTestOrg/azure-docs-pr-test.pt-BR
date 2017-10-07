---
title: "modelo do Gerenciador de recursos de aaaAzure funções - matrizes e objetos | Microsoft Docs"
description: "Descreve Olá toouse de funções em um modelo do Gerenciador de recursos do Azure para trabalhar com objetos e matrizes."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Funções de matriz e objeto para modelos do Azure Resource Manager 

O Resource Manager fornece diversas funções para trabalhar com matrizes e objetos.

* [array](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [length](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

tooget uma matriz de valores de cadeia de caracteres delimitada por um valor, consulte [dividir](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

Converte Olá valor tooan matriz.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| convertToArray |Sim |int, string, array ou object |matriz de tooan tooconvert do valor Hello. |

### <a name="return-value"></a>Valor de retorno

Uma matriz.

### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra como toouse Olá a função de matriz com tipos diferentes.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| intOutput | Matriz | [1] |
| stringOutput | Matriz | ["a"] |
| objectOutput | Matriz | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

Retorna o primeiro valor não nulo de parâmetros de saudação. Cadeias de caracteres vazias, matrizes vazias e objetos vazios não são nulos.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |int, string, array ou object |Olá primeiro tootest de valor para null. |
| argumentos adicionais |Não |int, string, array ou object |Tootest valores adicionais para null. |

### <a name="return-value"></a>Valor de retorno

valor de saudação do hello primeiro parâmetros não nulos, que pode ser uma cadeia de caracteres, int, matriz ou objeto. Null se todos os parâmetros forem nulos. 

### <a name="example"></a>Exemplo

Olá, exemplo a seguir mostra saída Olá usa diferentes de adesão.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| stringOutput | Cadeia de caracteres | padrão |
| intOutput | int | 1 |
| objectOutput | Objeto | {"first": "default"} |
| arrayOutput | Matriz | [1] |
| emptyOutput | Bool | True  |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Combina vários conjuntos e retorna Olá concatenado matriz, ou combina vários valores de cadeia de caracteres e retorna a cadeia de caracteres hello concatenado. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá primeira matriz ou cadeia de caracteres para concatenação. |
| argumentos adicionais |Não |matriz ou cadeia de caracteres |Matrizes ou cadeias de caractere adicionais em ordem sequencial para concatenação. |

Essa função pode conter qualquer número de argumentos e pode aceitar cadeias de caracteres ou matrizes de parâmetros de saudação.

### <a name="return-value"></a>Valor de retorno
Uma cadeia de caracteres ou matriz de valores concatenados.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como toocombine duas matrizes.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| retorno | Matriz | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

saudação de exemplo a seguir mostra como toocombine dois valores de cadeia de caracteres e retorna uma cadeia de caracteres concatenada.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| concatOutput | Cadeia de caracteres | prefix-5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

Verifica se uma matriz contém um valor, um objeto contém uma chave ou uma cadeia de caracteres contém uma subcadeia de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| contêiner |Sim |matriz, objeto ou cadeia de caracteres |valor de saudação que contém Olá toofind de valor. |
| itemToFind |Sim |string ou int |Olá toofind de valor. |

### <a name="return-value"></a>Valor de retorno

**True** se o item de saudação for encontrado; caso contrário, **False**.

### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra como toouse contém com tipos diferentes:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| stringTrue | Bool | True  |
| stringFalse | Bool | Falso |
| objectTrue | Bool | True  |
| objectFalse | Bool | Falso |
| arrayTrue | Bool | True  |
| arrayFalse | Bool | Falso |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Cria uma matriz de parâmetros de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |String, Inteiro, Matriz ou Objeto |primeiro valor na matriz Olá Olá. |
| argumentos adicionais |Não |String, Inteiro, Matriz ou Objeto |Valores adicionais na matriz de saudação. |

### <a name="return-value"></a>Valor de retorno

Uma matriz.

### <a name="example"></a>Exemplo

Olá mostrado no exemplo a seguir como toouse createArray com tipos diferentes:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| stringArray | Matriz | ["a", "b", "c"] |
| intArray | Matriz | [1, 2, 3] |
| objectArray | Matriz | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | Matriz | [["one", "two", "three"]] |

<a id="empty" />

## <a name="empty"></a>empty

`empty(itemToTest)`

Determina se uma matriz, objeto ou uma cadeia de caracteres está vazio.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| itemToTest |Sim |matriz, objeto ou cadeia de caracteres |Olá toocheck valor se ele estiver vazio. |

### <a name="return-value"></a>Valor de retorno

Retorna **True** se o valor de saudação está vazio; caso contrário, **False**.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir verifica se uma matriz, objeto e a cadeia de caracteres estão vazios.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayEmpty | Bool | True  |
| objectEmpty | Bool | True  |
| stringEmpty | Bool | True  |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Retorna Olá primeiro elemento da matriz de saudação ou o primeiro caractere da cadeia de caracteres de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá valor tooretrieve Olá primeiro elemento ou um caractere. |

### <a name="return-value"></a>Valor de retorno

tipo de saudação (string, int, matriz ou objeto) do primeiro elemento Olá em uma matriz, ou o primeiro caractere de saudação de uma cadeia de caracteres.

### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra como toouse Olá primeira função com uma matriz e a cadeia de caracteres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | Cadeia de caracteres | one |
| stringOutput | Cadeia de caracteres | O |

<a id="intersection" />

## <a name="intersection"></a>interseção
`intersection(arg1, arg2, arg3, ...)`

Retorna uma matriz ou objeto com elementos comuns Olá de parâmetros de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |objeto ou matriz |Olá primeiro toouse de valor para a localização de elementos comuns. |
| arg2 |Sim |objeto ou matriz |Olá segundo toouse de valor para a localização de elementos comuns. |
| argumentos adicionais |Não |objeto ou matriz |Toouse valores adicionais para a localização de elementos comuns. |

### <a name="return-value"></a>Valor de retorno

Uma matriz ou objeto com elementos comuns hello.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como a interseção de toouse com matrizes e objetos:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| objectOutput | Objeto | {"one": "a", "three": "c"} |
| arrayOutput | Matriz | ["two", "three"] |


## <a name="json"></a>json
`json(arg1)`

Retorna um objeto JSON.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |string |Olá valor tooconvert tooJSON. |


### <a name="return-value"></a>Valor de retorno

objeto JSON de saudação do hello especificado a cadeia de caracteres ou um objeto vazio quando **nulo** for especificado.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como a interseção de toouse com matrizes e objetos:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| jsonOutput | Objeto | {"a": "b"} |
| nullOutput | Booliano | True |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Retorna Olá último elemento da matriz de saudação ou o último caractere da cadeia de caracteres de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá valor tooretrieve Olá último elemento ou um caractere. |

### <a name="return-value"></a>Valor de retorno

tipo de saudação (string, int, matriz ou objeto) do hello último elemento em uma matriz, ou o último caractere saudação de uma cadeia de caracteres.

### <a name="example"></a>Exemplo

Olá exemplo a seguir mostra como toouse Olá última função com uma matriz e a cadeia de caracteres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | Cadeia de caracteres | três |
| stringOutput | Cadeia de caracteres | e |

<a id="length" />

## <a name="length"></a>length
`length(arg1)`

Retorna o número de saudação de elementos em uma matriz ou uma cadeia de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá toouse de matriz para obter o número de saudação de elementos ou Olá toouse de cadeia de caracteres para obter o número de saudação de caracteres. |

### <a name="return-value"></a>Valor de retorno

Um inteiro. 

### <a name="example"></a>Exemplo

Olá mostrado no exemplo a seguir como comprimento toouse com uma matriz e a cadeia de caracteres:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

Você pode usar essa função com um número de saudação do toospecify de matriz de iterações ao criar recursos. Em Olá exemplo a seguir, Olá parâmetro **siteNames** faz referência a matriz de tooan de toouse nomes durante a criação de sites da web de saudação.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Para saber mais sobre como usar essa função com uma matriz, confira [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

Retorna Olá valor mínimo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz de inteiros ou lista de inteiros separados por vírgulas |Olá coleção tooget Olá valor mínimo. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa o valor mínimo de saudação.

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
`max(arg1)`

Retorna Olá valor máximo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz de inteiros ou lista de inteiros separados por vírgulas |Olá coleção tooget Olá valor máximo. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa o valor máximo de saudação.

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

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

Cria uma matriz de inteiros a partir de um inteiro inicial e contendo um número de itens.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| startingInteger |Sim |int |primeiro inteiro na matriz Olá Olá. |
| numberofElements |Sim |int |número de saudação de inteiros na matriz de saudação. |

### <a name="return-value"></a>Valor de retorno

Uma matriz de inteiros.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como toouse Olá função range:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| rangeOutput | Matriz | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Retorna uma matriz com todos os elementos de saudação depois Olá número especificado na matriz hello, ou retorna uma cadeia de caracteres com todos os caracteres de saudação depois Olá número especificado na cadeia de caracteres de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| originalValue |Sim |matriz ou cadeia de caracteres |Olá toouse matriz ou cadeia de caracteres para ignorar. |
| numberToSkip |Sim |int |número de saudação de elementos ou caracteres tooskip. Se esse valor for 0 ou menos, todos os elementos de hello ou caracteres no valor de saudação são retornados. Se for maior do que o tamanho de cadeia de caracteres ou matriz Olá Olá, uma matriz vazia ou cadeia de caracteres é retornada. |

### <a name="return-value"></a>Valor de retorno

Uma matriz ou cadeia de caracteres.

### <a name="example"></a>Exemplo

Olá seguindo o exemplo ignora Olá número especificado de elementos na matriz de saudação e Olá número especificado de caracteres em uma cadeia de caracteres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | Matriz | ["three"] |
| stringOutput | Cadeia de caracteres | two three |

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Retorna uma matriz com hello número especificado de elementos de Olá início da matriz hello, ou uma cadeia de caracteres com hello número especificado de caracteres do início de saudação de cadeia de caracteres de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| originalValue |Sim |matriz ou cadeia de caracteres |Olá cadeia ou matriz de elementos de saudação tootake do. |
| numberToTake |Sim |int |número de saudação de elementos ou caracteres tootake. Se esse valor for 0 ou menos, uma matriz ou cadeia de caracteres vazia será retornada. Se for maior do que o comprimento de saudação do hello considerando a cadeia de caracteres ou matriz, todos os elementos de saudação na cadeia de caracteres ou matriz hello serão retornados. |

### <a name="return-value"></a>Valor de retorno

Uma matriz ou cadeia de caracteres.

### <a name="example"></a>Exemplo

Olá seguindo o exemplo usa Olá número especificado de elementos da matriz hello e caracteres de uma cadeia de caracteres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | Matriz | ["one", "two"] |
| stringOutput | Cadeia de caracteres | em |

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

Retorna uma matriz ou objeto com todos os elementos de parâmetros de saudação. Valores duplicados ou chaves só são incluídos uma vez.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |objeto ou matriz |Olá toouse valor primeiro para ingressar em elementos. |
| arg2 |Sim |objeto ou matriz |Olá toouse valor segundo para ingressar em elementos. |
| argumentos adicionais |Não |objeto ou matriz |Toouse valores adicionais para ingressar em elementos. |

### <a name="return-value"></a>Valor de retorno

Uma matriz ou objeto.

### <a name="example"></a>Exemplo

saudação de exemplo a seguir mostra como união toouse com matrizes e objetos:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| objectOutput | Objeto | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | Matriz | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>Próximas etapas
* Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).
* toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

