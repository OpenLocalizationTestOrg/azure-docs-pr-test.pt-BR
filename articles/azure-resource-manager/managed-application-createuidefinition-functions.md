---
title: "aaaAzure aplicativo gerenciado criar funções de definição de interface do usuário | Microsoft Docs"
description: "Descreve Olá funções toouse ao criar definições de interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a>Funções de CreateUiDefinition
Esta seção contém assinaturas Olá para todas as funções com suporte de um CreateUiDefinition.

toouse uma função, a declaração de saudação surround com colchetes. Por exemplo:

```json
"[function()]"
```

Cadeias de caracteres e outras funções podem ser referenciadas como parâmetros de uma função, mas as cadeias de caracteres devem estar entre aspas simples. Por exemplo:

```json
"[fn1(fn2(), 'foobar')]"
```

Onde aplicável, você pode fazer referência a propriedades de saída de saudação de uma função usando o operador de ponto de saudação. Por exemplo:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Referenciando funções
Essas funções podem ser usados tooreference saídas de propriedades de saudação ou contexto de um CreateUiDefinition.

### <a name="basics"></a>conceitos básicos
Retorna valores de saída de saudação de um elemento que é definido na etapa de Noções básicas de saudação.

Hello exemplo a seguir retorna a saudação saída de elemento de saudação chamado `foo` na etapa do hello Noções básicas:

```json
"[basics('foo')]"
```

### <a name="steps"></a>etapas
Retorna valores de saída de saudação de um elemento que está definido na etapa especificada hello. valores de saída de hello tooget de elementos na etapa de Noções básicas de Olá, use `basics()` em vez disso.

Hello exemplo a seguir retorna a saudação saída de elemento de saudação chamado `bar` na etapa Olá chamada `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Retorna o local de saudação selecionado na etapa de Noções básicas de saudação ou contexto atual hello.

Olá exemplo a seguir poderia retornar `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Funções de cadeia de caracteres
Essas funções podem ser usadas apenas com cadeias de caracteres JSON.

### <a name="concat"></a>concat
Concatena uma ou mais cadeias de caracteres.

Por exemplo, se o valor de saída de hello `element1` se `"bar"`, em seguida, este exemplo retorna a cadeia de caracteres hello `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Retorna subcadeia de caracteres de saudação do hello especificado a cadeia de caracteres. subcadeia de caracteres Hello começa no índice especificado da saudação e tem Olá comprimento especificado.

Olá exemplo a seguir retorna `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>substitui
Retorna uma cadeia de caracteres na qual todas as ocorrências de saudação especificado cadeia de caracteres na cadeia de caracteres atual hello serão substituídas por outra cadeia de caracteres.

Olá exemplo a seguir retorna `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
Gera uma cadeia de caracteres global exclusiva (GUID).

Olá exemplo a seguir poderia retornar `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Retorna uma cadeia de caracteres convertida toolowercase.

Olá exemplo a seguir retorna `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Retorna uma cadeia de caracteres convertida toouppercase.

Olá exemplo a seguir retorna `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Funções de coleção
Essas funções podem ser usadas com coleções, como cadeias de caracteres JSON, matrizes e objetos.

### <a name="contains"></a>contains
Retorna `true` se uma cadeia de caracteres contiver Olá subcadeia de caracteres especificada, que contém uma matriz Olá especificado valor ou um objeto contém a chave especificada hello.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Olá exemplo a seguir retorna `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>length
Retorna o número de saudação de caracteres em uma cadeia de caracteres, Olá número de valores em uma matriz ou Olá número de chaves em um objeto.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Olá exemplo a seguir retorna `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
Retorna `true` se a cadeia de caracteres hello, matriz ou objeto é nulo ou vazio.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Olá exemplo a seguir retorna `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Exemplo 4: nulo e indefinido
Suponha que `element1` é `null` ou indefinido. Olá exemplo a seguir retorna `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
Retorna Olá primeiro caractere da saudação especificado de cadeia de caracteres; primeiro valor da matriz especificada de saudação; ou Olá primeira chave e o valor do objeto especificado hello.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Olá exemplo a seguir retorna `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
Retorna Olá último caractere da saudação especificado string, o último valor de saudação do hello matriz especificada, a ou Olá a última chave e o valor do objeto especificado hello.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Olá exemplo a seguir retorna `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
Retorna um número especificado de caracteres contíguos do início de saudação de cadeia de caracteres hello, um número especificado de valores contíguos do início de saudação da matriz hello ou um número especificado de contíguas chaves e valores de início de saudação do objeto de saudação.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Olá exemplo a seguir retorna `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
Ignora um número especificado de elementos em uma coleção e, em seguida, retorna Olá elementos restantes.

#### <a name="example-1-string"></a>Exemplo 1: cadeia de caracteres
Olá exemplo a seguir retorna `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Exemplo 2: matriz
Suponha que `element1` retorne `[1, 2, 3]`. Olá exemplo a seguir retorna `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Exemplo 3: objeto
Suponha que `element1` retorne:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Olá exemplo a seguir retorna `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Funções lógicas
Essas funções podem ser usadas em condicionais. Algumas funções podem não dar suporte a todos os tipos de dados JSON.

### <a name="equals"></a>equals
Retorna `true` se ambos os parâmetros tiverem Olá mesmo tipo e valor. Essa função dá suporte a todos os tipos de dados JSON.

Olá exemplo a seguir retorna `true`:

```json
"[equals(0, 0)]"
```

Olá exemplo a seguir retorna `true`:

```json
"[equals('foo', 'foo')]"
```

Olá exemplo a seguir retorna `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
Retorna `true` se Olá primeiro parâmetro é estritamente menor do que o segundo parâmetro de saudação. Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.

Olá exemplo a seguir retorna `true`:

```json
"[less(1, 2)]"
```

Olá exemplo a seguir retorna `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Retorna `true` se Olá primeiro parâmetro for menor ou igual toohello segundo parâmetro. Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.

Olá exemplo a seguir retorna `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
Retorna `true` se Olá primeiro parâmetro é estritamente maior que o segundo parâmetro de saudação. Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.

Olá exemplo a seguir retorna `false`:

```json
"[greater(1, 2)]"
```

Olá exemplo a seguir retorna `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Retorna `true` se Olá primeiro parâmetro for maior que ou igual toohello segundo parâmetro. Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.

Olá exemplo a seguir retorna `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>e
Retorna `true` se todos os parâmetros de saudação avaliam muito`true`. Essa função dá suporte apenas a dois ou mais parâmetros do tipo booliano.

Olá exemplo a seguir retorna `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Olá exemplo a seguir retorna `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>ou o
Retorna `true` se pelo menos um dos parâmetros de saudação avalia muito`true`. Essa função dá suporte apenas a dois ou mais parâmetros do tipo booliano.

Olá exemplo a seguir retorna `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Olá exemplo a seguir retorna `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>não
Retorna `true` se o parâmetro hello avalia muito`false`. Essa função dá suporte apenas a parâmetros do tipo booliano.

Olá exemplo a seguir retorna `true`:

```json
"[not(false)]"
```

Olá exemplo a seguir retorna `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
Retorna Olá valor Olá não nulo do parâmetro da primeira. Essa função dá suporte a todos os tipos de dados JSON.

Suponha que `element1` e `element2` são indefinidos. Olá exemplo a seguir retorna `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Funções de conversão
Essas funções podem ser valores de tooconvert usado entre codificações e tipos de dados JSON.

### <a name="int"></a>int
Converte o inteiro de tooan parâmetro hello. Essa função dá suporte a parâmetros dos tipos número e cadeia de caracteres.

Olá exemplo a seguir retorna `1`:

```json
"[int('1')]"
```

Olá exemplo a seguir retorna `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>flutuante
Converte Olá parâmetro tooa ponto flutuante. Essa função dá suporte a parâmetros dos tipos número e cadeia de caracteres.

Olá exemplo a seguir retorna `1.0`:

```json
"[float('1.0')]"
```

Olá exemplo a seguir retorna `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>string
Converte a cadeia de caracteres hello parâmetro tooa. Essa função dá suporte a parâmetros de todos os tipos de dados JSON.

Olá exemplo a seguir retorna `"1"`:

```json
"[string(1)]"
```

Olá exemplo a seguir retorna `"2.9"`:

```json
"[string(2.9)]"
```

Olá exemplo a seguir retorna `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Olá exemplo a seguir retorna `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>bool
Converte Olá parâmetro tooa booliano. Essa função dá suporte a parâmetros dos tipos número, cadeia de caracteres e booliano. TooBooleans semelhante em JavaScript, qualquer valor exceto `0` ou `'false'` retorna `true`.

Olá exemplo a seguir retorna `true`:

```json
"[bool(1)]"
```

Olá exemplo a seguir retorna `false`:

```json
"[bool(0)]"
```

Olá exemplo a seguir retorna `true`:

```json
"[bool(true)]"
```

Olá exemplo a seguir retorna `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>analisar
Converte tipo nativo do hello parâmetro tooa. Em outras palavras, essa função é o inverso da saudação `string()`. Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.

Olá exemplo a seguir retorna `1`:

```json
"[parse('1')]"
```

Olá exemplo a seguir retorna `true`:

```json
"[parse('true')]"
```

Olá exemplo a seguir retorna `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Olá exemplo a seguir retorna `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Codifica Olá parâmetro tooa base 64 cadeia de caracteres codificada. Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.

Olá exemplo a seguir retorna `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Decodifica o parâmetro hello de uma cadeia de caracteres codificada de base 64. Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.

Olá exemplo a seguir retorna `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Codifica a cadeia de caracteres codificados de URL tooa de parâmetro de saudação. Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.

Olá exemplo a seguir retorna `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Decodifica o parâmetro hello de uma cadeia de caracteres codificados de URL. Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.

Olá exemplo a seguir retorna `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Funções matemáticas
### <a name="add"></a>adicionar
Adiciona dois números e retorna o resultado de saudação.

Olá exemplo a seguir retorna `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Subtrai o segundo o número do primeiro número de Olá Olá e retorna o resultado de saudação.

Olá exemplo a seguir retorna `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Multiplica dois números e retorna o resultado de saudação.

Olá exemplo a seguir retorna `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Divide o número de primeira Olá por segundo hello e retorna o resultado de saudação. resultado de saudação sempre é um inteiro.

Olá exemplo a seguir retorna `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
Divide o número de primeira Olá por segundo hello e retorna o resto de saudação.

Olá exemplo a seguir retorna `0`:

```json
"[mod(6, 3)]"
```

Olá exemplo a seguir retorna `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
Retorna Olá pequeno de números de saudação dois.

Olá exemplo a seguir retorna `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
Olá retorna mais de dois números de saudação.

Olá exemplo a seguir retorna `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
Gera uma sequência de integral números em Olá o intervalo especificado.

Olá exemplo a seguir retorna `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Retorna um aleatório número integral em Olá o intervalo especificado. Essa função não gera números aleatórios criptograficamente seguros.

Olá exemplo a seguir poderia retornar `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
Retorna o hello maior inteiro menor ou igual toohello no número especificado.

Olá exemplo a seguir retorna `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Retorna Olá maior número inteiro maior ou igual toohello no número especificado.

Olá exemplo a seguir retorna `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Funções de data
### <a name="utcnow"></a>utcNow
Retorna uma cadeia de caracteres no formato ISO 8601 de saudação data e hora no computador local Olá atuais.

Olá exemplo a seguir poderia retornar `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
Adiciona um número integral de toohello de segundos especificado timestamp.

Olá exemplo a seguir retorna `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Adiciona um número integral de toohello de minutos especificado timestamp.

Olá exemplo a seguir retorna `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Adiciona um número integral de toohello de horas especificado timestamp.

Olá exemplo a seguir retorna `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Próximas etapas
* Para uma introdução tooAzure Gerenciador de recursos, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).

