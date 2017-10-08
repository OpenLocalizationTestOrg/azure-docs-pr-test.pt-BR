---
title: "a cadeia de caracteres de funções de modelo do Gerenciador de recursos de aaaAzure - | Microsoft Docs"
description: "Descreve Olá toouse de funções em um toowork de modelo do Gerenciador de recursos do Azure com cadeias de caracteres."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Funções de cadeia de caracteres para modelos do Azure Resource Manager

Gerenciador de recursos fornece Olá funções para trabalhar com cadeias de caracteres a seguir:

* [base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [contains](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [empty](#empty)
* [endsWith](#endswith)
* [first](#first)
* [indexOf](#indexof)
* [last](#last)
* [lastIndexOf](#lastindexof)
* [length](#length)
* [padLeft](#padleft)
* [substitui](#replace)
* [skip](#skip)
* [split](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [string](#string)
* [substring](#substring)
* [take](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [cortar](#trim)
* [uniqueString](#uniquestring)
* [uri](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>base64
`base64(inputString)`

Retorna Olá representação de cadeia de caracteres de entrada hello base 64.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| inputString |Sim |string |Olá tooreturn valor como uma representação em base64. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres que contém a representação de base64 hello.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como toouse Olá função base64.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| base64Output | Cadeia de caracteres | b25lLCB0d28sIHRocmVl |
| toStringOutput | Cadeia de caracteres | um, dois, três |
| toJsonOutput | Objeto | {"one": "a", "two": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Converte um objeto JSON de tooa de representação de base64.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| base64Value |Sim |string |objeto Olá base64 representação tooconvert tooa JSON. |

### <a name="return-value"></a>Valor de retorno

Um objeto JSON.

### <a name="examples"></a>Exemplos

Olá, exemplo a seguir usa Olá base64ToJson função tooconvert um valor base64:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| base64Output | Cadeia de caracteres | b25lLCB0d28sIHRocmVl |
| toStringOutput | Cadeia de caracteres | um, dois, três |
| toJsonOutput | Objeto | {"one": "a", "two": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Converte uma cadeia de caracteres base64 representação tooa.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| base64Value |Sim |string |cadeia de caracteres do Hello base64 representação tooconvert tooa. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres de saudação convertido valor base64.

### <a name="examples"></a>Exemplos

Olá, exemplo a seguir usa Olá base64ToString função tooconvert um valor base64:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| base64Output | Cadeia de caracteres | b25lLCB0d28sIHRocmVl |
| toStringOutput | Cadeia de caracteres | um, dois, três |
| toJsonOutput | Objeto | {"one": "a", "two": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

Combina vários valores de cadeia de caracteres e retorna a cadeia de caracteres hello concatenado, ou combina vários conjuntos e retorna a matriz Olá concatenado.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |cadeia de caracteres ou matriz |primeiro valor de concatenação Hello. |
| argumentos adicionais |Não |string |Valores adicionais em ordem sequencial para concatenação. |

### <a name="return-value"></a>Valor de retorno
Uma cadeia de caracteres ou matriz de valores concatenados.

### <a name="examples"></a>Exemplos

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

<a id="contains" />

## <a name="contains"></a>contains
`contains (container, itemToFind)`

Verifica se uma matriz contém um valor, um objeto contém uma chave ou uma cadeia de caracteres contém uma subcadeia de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| contêiner |Sim |matriz, objeto ou cadeia de caracteres |valor de saudação que contém Olá toofind de valor. |
| itemToFind |Sim |string ou int |Olá toofind de valor. |

### <a name="return-value"></a>Valor de retorno

**True** se o item de saudação for encontrado; caso contrário, **False**.

### <a name="examples"></a>Exemplos

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

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

Converte um dado do valor tooa URI.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToConvert |Sim |string |Olá tooconvert tooa dados de valor URI. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres formatada como um URI de dados.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir converte um dado do valor tooa URI e converte uma cadeia de caracteres do URI tooa de dados:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| dataUriOutput | Cadeia de caracteres | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | Cadeia de caracteres | Hello, World! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

Converte um URI de dados formatados de cadeia de caracteres do valor tooa.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |Sim |string |dados de saudação tooconvert de valor do URI. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres que contém a saudação convertido valor.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir converte um dado do valor tooa URI e converte uma cadeia de caracteres do URI tooa de dados:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| dataUriOutput | Cadeia de caracteres | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | Cadeia de caracteres | Hello, World! |

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

### <a name="examples"></a>Exemplos

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

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

Determina se uma cadeia de caracteres termina com um valor. comparação de saudação diferencia maiusculas de minúsculas.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToSearch |Sim |string |valor de saudação que contém Olá toofind de item. |
| stringToFind |Sim |string |Olá toofind de valor. |

### <a name="return-value"></a>Valor de retorno

**True** se Olá último ou mais caracteres de cadeia de caracteres hello corresponder ao valor de saudação; caso contrário, **False**.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como toouse Olá startsWith e endsWith funções:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| startsTrue | Bool | True  |
| startsCapTrue | Bool | True  |
| startsFalse | Bool | Falso |
| endsTrue | Bool | True  |
| endsCapTrue | Bool | True  |
| endsFalse | Bool | Falso |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Retorna Olá primeiro caractere da cadeia de caracteres de saudação ou o primeiro elemento da matriz de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá valor tooretrieve Olá primeiro elemento ou um caractere. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres primeiro hello, ou tipo hello (string, int, matriz ou objeto) do primeiro elemento Olá em uma matriz.

### <a name="examples"></a>Exemplos

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

<a id="indexof" />

## <a name="indexof"></a>indexOf
`indexOf(stringToSearch, stringToFind)`

Retorna Olá primeira posição de um valor em uma cadeia de caracteres. comparação de saudação diferencia maiusculas de minúsculas.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToSearch |Sim |string |valor de saudação que contém Olá toofind de item. |
| stringToFind |Sim |string |Olá toofind de valor. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa a posição de saudação do hello toofind de item. valor de saudação é baseado em zero. Se o item de saudação não for encontrado, -1 será retornado.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como toouse Olá indexOf e lastIndexOf funções:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| NotFound | int | -1 |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Retorna a última caractere da cadeia de caracteres de saudação ou último elemento Olá da matriz de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá valor tooretrieve Olá último elemento ou um caractere. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres última hello ou tipo de saudação (string, int, matriz ou objeto) do hello último elemento em uma matriz.

### <a name="examples"></a>Exemplos

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

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

Retorna Olá última posição de um valor em uma cadeia de caracteres. comparação de saudação diferencia maiusculas de minúsculas.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToSearch |Sim |string |valor de saudação que contém Olá toofind de item. |
| stringToFind |Sim |string |Olá toofind de valor. |

### <a name="return-value"></a>Valor de retorno

Um inteiro que representa a última posição Olá da saudação toofind de item. valor de saudação é baseado em zero. Se o item de saudação não for encontrado, -1 será retornado.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como toouse Olá indexOf e lastIndexOf funções:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| NotFound | int | -1 |

<a id="length" />

## <a name="length"></a>length
`length(string)`

Retorna o número de saudação de caracteres em uma cadeia de caracteres ou elementos em uma matriz.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |matriz ou cadeia de caracteres |Olá toouse de matriz para obter o número de saudação de elementos ou Olá toouse de cadeia de caracteres para obter o número de saudação de caracteres. |

### <a name="return-value"></a>Valor de retorno

Um inteiro. 

### <a name="examples"></a>Exemplos

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

<a id="padleft" />

## <a name="padleft"></a>padLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Retorna uma cadeia de caracteres alinhada à direita, adicionando caracteres toohello esquerda até atingir o comprimento especificado total hello.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| valueToPad |Sim |string ou int |Olá valor tooright-alinhar. |
| totalLength |Sim |int |número total de saudação de caracteres em Olá retornou uma cadeia de caracteres. |
| paddingCharacter |Não |caractere único |Olá toouse de caractere para o preenchimento à esquerda até que o comprimento total Olá seja atingido. valor padrão de saudação é um espaço. |

Se a cadeia de caracteres original Olá for maior que o número de saudação do toopad caracteres, caracteres não é adicionado.

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres pelo menos Olá número de caracteres especificado.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como toopad Olá valor de parâmetro fornecido pelo usuário, adicionando Olá caractere zero até atingir o número total de saudação de caracteres. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| stringOutput | Cadeia de caracteres | 0000000123 |

<a id="replace" />

## <a name="replace"></a>substituir
`replace(originalString, oldString, newString)`

Retorna uma nova cadeia de caracteres com todas as instâncias de uma cadeia de caracteres substituídas por outra cadeia de caracteres.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| originalString |Sim |string |valor de saudação que tem todas as instâncias de uma cadeia de caracteres substituídas por outra cadeia de caracteres. |
| oldString |Sim |string |cadeia de caracteres de saudação toobe removida da cadeia de caracteres original hello. |
| newString |Sim |string |Olá tooadd de cadeia de caracteres em vez da saudação removido cadeia de caracteres. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres com hello caracteres foram substituídos.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como tooremove todos os traços de cadeia de caracteres fornecida pelo usuário hello e como parte de tooreplace de saudação cadeia de caracteres com outra cadeia de caracteres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| firstOutput | Cadeia de caracteres | 1231231234 |
| secodeOutput | Cadeia de caracteres | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Retorna uma cadeia de caracteres com todos os caracteres de saudação depois Olá número especificado de caracteres ou uma matriz com todos os elementos de saudação depois Olá número especificado de elementos.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| originalValue |Sim |matriz ou cadeia de caracteres |Olá toouse matriz ou cadeia de caracteres para ignorar. |
| numberToSkip |Sim |int |número de saudação de elementos ou caracteres tooskip. Se esse valor for 0 ou menos, todos os elementos de hello ou caracteres no valor de saudação são retornados. Se for maior do que o tamanho de cadeia de caracteres ou matriz Olá Olá, uma matriz vazia ou cadeia de caracteres é retornada. |

### <a name="return-value"></a>Valor de retorno

Uma matriz ou cadeia de caracteres.

### <a name="examples"></a>Exemplos

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
| stringOutput | Cadeia de caracteres | dois três |

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

Retorna uma matriz de cadeias de caracteres que contém as subcadeias de caracteres de saudação do hello cadeia de caracteres de entrada que é delimitadas por Olá especificado delimitadores.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| inputString |Sim |string |Olá toosplit de cadeia de caracteres. |
| delimiter |Sim |cadeia de caracteres ou matriz de cadeias de caracteres |Olá toouse delimitador para a divisão de cadeia de caracteres de saudação. |

### <a name="return-value"></a>Valor de retorno

Uma matriz de cadeias de caracteres.

### <a name="examples"></a>Exemplos

Olá exemplo a seguir divide Olá entrada cadeia de caracteres com uma vírgula e com uma vírgula ou ponto e vírgula.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| firstOutput | Matriz | ["one", "two", "three"] |
| secondOutput | Matriz | ["one", "two", "three"] |

<a id="startswith" />

## <a name="startswith"></a>startsWith
`startsWith(stringToSearch, stringToFind)`

Determina se uma cadeia de caracteres começa com um valor. comparação de saudação diferencia maiusculas de minúsculas.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToSearch |Sim |string |valor de saudação que contém Olá toofind de item. |
| stringToFind |Sim |string |Olá toofind de valor. |

### <a name="return-value"></a>Valor de retorno

**True** se Olá primeiro caractere ou caracteres de cadeia de caracteres hello corresponder ao valor de saudação; caso contrário, **False**.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como toouse Olá startsWith e endsWith funções:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| startsTrue | Bool | True  |
| startsCapTrue | Bool | True  |
| startsFalse | Bool | Falso |
| endsTrue | Bool | True  |
| endsCapTrue | Bool | True  |
| endsFalse | Bool | Falso |

<a id="string" />

## <a name="string"></a>string
`string(valueToConvert)`

Converte Olá especificado a cadeia de caracteres do valor tooa.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| valueToConvert |Sim | Qualquer |Olá valor tooconvert toostring. Qualquer tipo de valor pode ser convertido, incluindo objetos e matrizes. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres do valor de saudação convertida.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como tooconvert diferentes tipos de valores toostrings:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| objectOutput | Cadeia de caracteres | {"valueA":10,"valueB":"Example Text"} |
| arrayOutput | Cadeia de caracteres | ["a","b","c"] |
| intOutput | Cadeia de caracteres | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

Retorna uma subcadeia de caracteres que começa no hello especificado posição de caracteres e contém Olá número especificado de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToParse |Sim |string |Olá cadeia de caracteres original do qual Olá subcadeia de caracteres é extraída. |
| startIndex |Não |int |Olá com base em zero posição de caractere inicial de subcadeia de caracteres de saudação. |
| length |Não |int |número de saudação de caracteres de subcadeia de caracteres de saudação. Deve se referir tooa local dentro da cadeia de caracteres de saudação. |

### <a name="return-value"></a>Valor de retorno

subcadeia de caracteres Hello.

### <a name="remarks"></a>Comentários

função Hello falha quando a subcadeia de caracteres hello ultrapassa a fim de saudação da cadeia de caracteres de saudação. saudação de exemplo a seguir falhará com hello erro "parâmetros de índice e o comprimento da saudação devem se referir tooa local dentro da cadeia de caracteres de saudação. Olá parâmetro de índice: '0' hello parâmetro de comprimento: Olá '11', comprimento do parâmetro de cadeia de caracteres hello: '10'. ".

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir extrai uma subcadeia de caracteres de um parâmetro.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| substringOutput | Cadeia de caracteres | dois |


<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Retorna uma cadeia de caracteres com hello número especificado de caracteres do início de saudação do hello cadeia de caracteres ou uma matriz com hello número especificado de elementos do início de saudação da matriz de saudação.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| originalValue |Sim |matriz ou cadeia de caracteres |Olá cadeia ou matriz de elementos de saudação tootake do. |
| numberToTake |Sim |int |número de saudação de elementos ou caracteres tootake. Se esse valor for 0 ou menos, uma matriz ou cadeia de caracteres vazia será retornada. Se for maior do que o comprimento de saudação do hello considerando a cadeia de caracteres ou matriz, todos os elementos de saudação na cadeia de caracteres ou matriz hello serão retornados. |

### <a name="return-value"></a>Valor de retorno

Uma matriz ou cadeia de caracteres.

### <a name="examples"></a>Exemplos

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

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

Converte Olá especificado caso toolower de cadeia de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToChange |Sim |string |Olá valor tooconvert toolower maiusculas e minúsculas. |

### <a name="return-value"></a>Valor de retorno

cadeia de caracteres de saudação convertida toolower caso.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir converte um caso de toolower de valor de parâmetro e tooupper caso.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| toLowerOutput | Cadeia de caracteres | um dois três |
| toUpperOutput | Cadeia de caracteres | UM DOIS TRÊS |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

Converte Olá especificado caso tooupper de cadeia de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToChange |Sim |string |Olá valor tooconvert tooupper maiusculas e minúsculas. |

### <a name="return-value"></a>Valor de retorno

cadeia de caracteres de saudação convertida tooupper caso.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir converte um caso de toolower de valor de parâmetro e tooupper caso.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| toLowerOutput | Cadeia de caracteres | um dois três |
| toUpperOutput | Cadeia de caracteres | UM DOIS TRÊS |

<a id="trim" />

## <a name="trim"></a>cortar
`trim (stringToTrim)`

Remove todos os principais e caracteres de espaço em branco da saudação especificado cadeia de caracteres.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToTrim |Sim |string |Olá tootrim de valor. |

### <a name="return-value"></a>Valor de retorno

cadeia de caracteres de saudação sem à esquerda e caracteres de espaço em branco à direita.

### <a name="examples"></a>Exemplos

Olá, exemplo a seguir remove caracteres de espaço em branco de saudação do parâmetro hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| retorno | Cadeia de caracteres | um dois três |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

Cria uma cadeia de caracteres de hash determinística com base nos valores hello fornecidos como parâmetros. 

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| baseString |Sim |string |valor de saudação usado na toocreate de função de hash Olá uma cadeia de caracteres exclusiva. |
| parâmetros extras conforme necessário |Não |string |Você pode adicionar quantas cadeias de caracteres como valor de saudação toocreate necessário que especifica o nível de saudação de exclusividade. |

### <a name="remarks"></a>Comentários

Essa função é útil quando você precisa toocreate um nome exclusivo para um recurso. Você fornecer valores de parâmetro para limitam o escopo de saudação de exclusividade para o resultado de saudação. Você pode especificar se o nome da saudação é exclusivo para baixo toosubscription, no grupo de recursos ou implantação. 

Olá retornou o valor não é uma cadeia de caracteres aleatória, mas em vez disso, Olá resultado de uma função de hash. Olá retornou o valor é 13 caracteres. Não é globalmente exclusivo. Talvez você queira toocombine valor de saudação com um prefixo de seu toocreate de convenção de nomenclatura um nome que seja significativo. Olá, exemplo a seguir mostra formato Olá Olá retornada o valor. valor real Olá varia de acordo com hello parâmetros fornecido.

    tcvhiyu5h2o5o

Olá exemplos a seguir mostra como toouse uniqueString toocreate um único valor para comumente usados níveis.

Toosubscription escopo exclusivo

```json
"[uniqueString(subscription().subscriptionId)]"
```

Exclusivo tooresource no escopo de grupo

```json
"[uniqueString(resourceGroup().id)]"
```

Exclusivo toodeployment com escopo definido para um grupo de recursos

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

saudação de exemplo a seguir mostra como toocreate um nome exclusivo para uma conta de armazenamento com base em seu grupo de recursos. Dentro do grupo de recursos Olá, nome de saudação não é exclusivo se construída Olá mesma maneira.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres que contém 13 caracteres.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir retorna os resultados da uniquestring:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a>uri
`uri (baseUri, relativeUri)`

Cria um URI absoluto combinando Olá baseUri e cadeia de caracteres hello Uri_relativo.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| baseUri |Sim |string |Olá a cadeia de caracteres de uri de base. |
| relativeUri |Sim |string |Olá uri relativo cadeia de caracteres tooadd toohello uri base cadeia de caracteres. |

Olá valor Olá **baseUri** parâmetro pode incluir um arquivo específico, mas somente caminho base Olá é usado ao construir Olá URI. Por exemplo, passar `http://contoso.com/resources/azuredeploy.json` como resultados de parâmetro hello baseUri em um URI de base de `http://contoso.com/resources/`.

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres que representa Olá URI absoluto para valores de base e relativo hello.

### <a name="examples"></a>Exemplos

saudação de exemplo a seguir mostra como tooconstruct um modelo aninhado do link tooa com base no valor de saudação do modelo pai a saudação.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

Olá mostrado no exemplo a seguir como uri toouse, uriComponent e uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| uriOutput | Cadeia de caracteres | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | Cadeia de caracteres | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | Cadeia de caracteres | http://contoso.com/resources/nested/azuredeploy.json |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

Codifica um URI.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| stringToEncode |Sim |string |Olá tooencode de valor. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres de saudação URI valor codificado.

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como uri toouse, uriComponent e uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| uriOutput | Cadeia de caracteres | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | Cadeia de caracteres | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | Cadeia de caracteres | http://contoso.com/resources/nested/azuredeploy.json |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

Retorna uma cadeia de caracteres de um valor codificado em URI.

### <a name="parameters"></a>parâmetros

| Parâmetro | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| uriEncodedString |Sim |string |Olá URI codificado em cadeia de caracteres do valor tooconvert tooa. |

### <a name="return-value"></a>Valor de retorno

Uma cadeia de caracteres decodificada de valores codificados em URI.

### <a name="examples"></a>Exemplos

Olá mostrado no exemplo a seguir como uri toouse, uriComponent e uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

saudação de saída de saudação anterior exemplo com valores padrão de saudação é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| uriOutput | Cadeia de caracteres | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | Cadeia de caracteres | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | Cadeia de caracteres | http://contoso.com/resources/nested/azuredeploy.json |


## <a name="next-steps"></a>Próximas etapas
* Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).
* toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

