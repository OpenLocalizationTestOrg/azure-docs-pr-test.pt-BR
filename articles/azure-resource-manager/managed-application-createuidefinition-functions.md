---
title: "Funções Criar definições de interface do usuário de aplicativos gerenciados pelo Azure | Microsoft Docs"
description: "Descreve as funções para uso na criação de definições de interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="73a94-103">Funções de CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="73a94-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="73a94-104">Esta seção contém as assinaturas para todas as funções com suporte de uma CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="73a94-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="73a94-105">Para usar uma função, coloque a declaração entre colchetes.</span><span class="sxs-lookup"><span data-stu-id="73a94-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="73a94-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="73a94-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="73a94-107">Cadeias de caracteres e outras funções podem ser referenciadas como parâmetros de uma função, mas as cadeias de caracteres devem estar entre aspas simples.</span><span class="sxs-lookup"><span data-stu-id="73a94-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="73a94-108">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="73a94-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="73a94-109">Quando aplicável, referencie propriedades da saída de uma função usando o operador de ponto.</span><span class="sxs-lookup"><span data-stu-id="73a94-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="73a94-110">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="73a94-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="73a94-111">Referenciando funções</span><span class="sxs-lookup"><span data-stu-id="73a94-111">Referencing functions</span></span>
<span data-ttu-id="73a94-112">Essas funções podem ser usadas para referenciar saídas das propriedades ou o contexto de uma CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="73a94-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="73a94-113">conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="73a94-113">basics</span></span>
<span data-ttu-id="73a94-114">Retorna os valores de saída de um elemento que é definido na etapa Conceitos básicos.</span><span class="sxs-lookup"><span data-stu-id="73a94-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="73a94-115">O seguinte exemplo retorna a saída do elemento chamado `foo` na etapa Conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="73a94-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="73a94-116">etapas</span><span class="sxs-lookup"><span data-stu-id="73a94-116">steps</span></span>
<span data-ttu-id="73a94-117">Retorna os valores de saída de um elemento que é definido na etapa especificada.</span><span class="sxs-lookup"><span data-stu-id="73a94-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="73a94-118">Para obter os valores de saída de elementos na etapa Conceitos básicos, use `basics()`.</span><span class="sxs-lookup"><span data-stu-id="73a94-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="73a94-119">O seguinte exemplo retorna a saída do elemento chamado `bar` na etapa chamada `foo`:</span><span class="sxs-lookup"><span data-stu-id="73a94-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="73a94-120">location</span><span class="sxs-lookup"><span data-stu-id="73a94-120">location</span></span>
<span data-ttu-id="73a94-121">Retorna a localização selecionada na etapa Conceitos básicos ou o contexto atual.</span><span class="sxs-lookup"><span data-stu-id="73a94-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="73a94-122">O seguinte exemplo poderá retornar `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="73a94-123">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-123">String functions</span></span>
<span data-ttu-id="73a94-124">Essas funções podem ser usadas apenas com cadeias de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="73a94-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="73a94-125">concat</span><span class="sxs-lookup"><span data-stu-id="73a94-125">concat</span></span>
<span data-ttu-id="73a94-126">Concatena uma ou mais cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="73a94-127">Por exemplo, se o valor de saída `element1` for `"bar"`, este exemplo retornará a cadeia de caracteres `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="73a94-128">substring</span><span class="sxs-lookup"><span data-stu-id="73a94-128">substring</span></span>
<span data-ttu-id="73a94-129">Retorna a subcadeia de caracteres da cadeia de caracteres especificada.</span><span class="sxs-lookup"><span data-stu-id="73a94-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="73a94-130">A subcadeia de caracteres começa no índice especificado e tem o comprimento especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="73a94-131">O exemplo a seguir retorna `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="73a94-132">substitui</span><span class="sxs-lookup"><span data-stu-id="73a94-132">replace</span></span>
<span data-ttu-id="73a94-133">Retorna uma cadeia de caracteres na qual todas as ocorrências da cadeia de caracteres especificada na cadeia de caracteres atual são substituídas por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="73a94-134">O exemplo a seguir retorna `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="73a94-135">GUID</span><span class="sxs-lookup"><span data-stu-id="73a94-135">guid</span></span>
<span data-ttu-id="73a94-136">Gera uma cadeia de caracteres global exclusiva (GUID).</span><span class="sxs-lookup"><span data-stu-id="73a94-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="73a94-137">O seguinte exemplo poderá retornar `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="73a94-138">toLower</span><span class="sxs-lookup"><span data-stu-id="73a94-138">toLower</span></span>
<span data-ttu-id="73a94-139">Retorna uma cadeia de caracteres convertida em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="73a94-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="73a94-140">O exemplo a seguir retorna `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="73a94-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="73a94-141">toUpper</span></span>
<span data-ttu-id="73a94-142">Retorna uma cadeia de caracteres convertida em maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="73a94-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="73a94-143">O exemplo a seguir retorna `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="73a94-144">Funções de coleção</span><span class="sxs-lookup"><span data-stu-id="73a94-144">Collection functions</span></span>
<span data-ttu-id="73a94-145">Essas funções podem ser usadas com coleções, como cadeias de caracteres JSON, matrizes e objetos.</span><span class="sxs-lookup"><span data-stu-id="73a94-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="73a94-146">contains</span><span class="sxs-lookup"><span data-stu-id="73a94-146">contains</span></span>
<span data-ttu-id="73a94-147">Retorna `true` se uma cadeia de caracteres contém a subcadeia de caracteres especificada, uma matriz contém o valor especificado ou um objeto contém a chave especificada.</span><span class="sxs-lookup"><span data-stu-id="73a94-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-148">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-148">Example 1: string</span></span>
<span data-ttu-id="73a94-149">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-150">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-150">Example 2: array</span></span>
<span data-ttu-id="73a94-151">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-152">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-153">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-153">Example 3: object</span></span>
<span data-ttu-id="73a94-154">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="73a94-155">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="73a94-156">length</span><span class="sxs-lookup"><span data-stu-id="73a94-156">length</span></span>
<span data-ttu-id="73a94-157">Retorna o número de caracteres em uma cadeia de caracteres, o número de valores em uma matriz ou o número de chaves em um objeto.</span><span class="sxs-lookup"><span data-stu-id="73a94-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-158">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-158">Example 1: string</span></span>
<span data-ttu-id="73a94-159">O exemplo a seguir retorna `6`:</span><span class="sxs-lookup"><span data-stu-id="73a94-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-160">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-160">Example 2: array</span></span>
<span data-ttu-id="73a94-161">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-162">O exemplo a seguir retorna `3`:</span><span class="sxs-lookup"><span data-stu-id="73a94-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-163">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-163">Example 3: object</span></span>
<span data-ttu-id="73a94-164">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="73a94-165">O exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="73a94-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="73a94-166">empty</span><span class="sxs-lookup"><span data-stu-id="73a94-166">empty</span></span>
<span data-ttu-id="73a94-167">Retorna `true` se a cadeia de caracteres, matriz ou objeto é nulo ou vazio.</span><span class="sxs-lookup"><span data-stu-id="73a94-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-168">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-168">Example 1: string</span></span>
<span data-ttu-id="73a94-169">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-170">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-170">Example 2: array</span></span>
<span data-ttu-id="73a94-171">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-172">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-173">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-173">Example 3: object</span></span>
<span data-ttu-id="73a94-174">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="73a94-175">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="73a94-176">Exemplo 4: nulo e indefinido</span><span class="sxs-lookup"><span data-stu-id="73a94-176">Example 4: null and undefined</span></span>
<span data-ttu-id="73a94-177">Suponha que `element1` é `null` ou indefinido.</span><span class="sxs-lookup"><span data-stu-id="73a94-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="73a94-178">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="73a94-179">first</span><span class="sxs-lookup"><span data-stu-id="73a94-179">first</span></span>
<span data-ttu-id="73a94-180">Retorna o primeiro caractere da cadeia de caracteres especificada, o primeiro valor da matriz especificada ou a primeira chave e valor do objeto especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-181">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-181">Example 1: string</span></span>
<span data-ttu-id="73a94-182">O exemplo a seguir retorna `"f"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-183">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-183">Example 2: array</span></span>
<span data-ttu-id="73a94-184">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-185">O exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="73a94-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-186">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-186">Example 3: object</span></span>
<span data-ttu-id="73a94-187">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="73a94-188">O exemplo a seguir retorna `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="73a94-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="73a94-189">last</span><span class="sxs-lookup"><span data-stu-id="73a94-189">last</span></span>
<span data-ttu-id="73a94-190">Retorna o último caractere da cadeia de caracteres especificada, o último valor da matriz especificada ou a última chave e valor do objeto especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-191">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-191">Example 1: string</span></span>
<span data-ttu-id="73a94-192">O exemplo a seguir retorna `"r"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-193">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-193">Example 2: array</span></span>
<span data-ttu-id="73a94-194">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-195">O exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="73a94-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-196">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-196">Example 3: object</span></span>
<span data-ttu-id="73a94-197">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="73a94-198">O exemplo a seguir retorna `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="73a94-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="73a94-199">take</span><span class="sxs-lookup"><span data-stu-id="73a94-199">take</span></span>
<span data-ttu-id="73a94-200">Retorna um número especificado de caracteres contíguos do início da cadeia de caracteres, um número especificado de valores contíguos do início da matriz ou um número especificado de chaves e valores contíguos do início do objeto.</span><span class="sxs-lookup"><span data-stu-id="73a94-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-201">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-201">Example 1: string</span></span>
<span data-ttu-id="73a94-202">O exemplo a seguir retorna `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-203">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-203">Example 2: array</span></span>
<span data-ttu-id="73a94-204">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-205">O exemplo a seguir retorna `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="73a94-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-206">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-206">Example 3: object</span></span>
<span data-ttu-id="73a94-207">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="73a94-208">O exemplo a seguir retorna `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="73a94-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="73a94-209">skip</span><span class="sxs-lookup"><span data-stu-id="73a94-209">skip</span></span>
<span data-ttu-id="73a94-210">Ignora um número especificado de elementos em uma coleção e, em seguida, retorna os elementos restantes.</span><span class="sxs-lookup"><span data-stu-id="73a94-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="73a94-211">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="73a94-211">Example 1: string</span></span>
<span data-ttu-id="73a94-212">O exemplo a seguir retorna `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="73a94-213">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="73a94-213">Example 2: array</span></span>
<span data-ttu-id="73a94-214">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="73a94-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="73a94-215">O exemplo a seguir retorna `[3]`:</span><span class="sxs-lookup"><span data-stu-id="73a94-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="73a94-216">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="73a94-216">Example 3: object</span></span>
<span data-ttu-id="73a94-217">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="73a94-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="73a94-218">O exemplo a seguir retorna `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="73a94-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="73a94-219">Funções lógicas</span><span class="sxs-lookup"><span data-stu-id="73a94-219">Logical functions</span></span>
<span data-ttu-id="73a94-220">Essas funções podem ser usadas em condicionais.</span><span class="sxs-lookup"><span data-stu-id="73a94-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="73a94-221">Algumas funções podem não dar suporte a todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="73a94-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="73a94-222">equals</span><span class="sxs-lookup"><span data-stu-id="73a94-222">equals</span></span>
<span data-ttu-id="73a94-223">Retorna `true` se ambos os parâmetros têm o mesmo tipo e valor.</span><span class="sxs-lookup"><span data-stu-id="73a94-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="73a94-224">Essa função dá suporte a todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="73a94-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="73a94-225">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="73a94-226">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="73a94-227">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="73a94-228">less</span><span class="sxs-lookup"><span data-stu-id="73a94-228">less</span></span>
<span data-ttu-id="73a94-229">Retorna `true` se o primeiro parâmetro é estritamente menor que o segundo parâmetro.</span><span class="sxs-lookup"><span data-stu-id="73a94-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="73a94-230">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="73a94-231">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="73a94-232">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="73a94-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="73a94-233">lessOrEquals</span></span>
<span data-ttu-id="73a94-234">Retorna `true` se o primeiro parâmetro é menor ou igual ao segundo parâmetro.</span><span class="sxs-lookup"><span data-stu-id="73a94-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="73a94-235">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="73a94-236">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="73a94-237">greater</span><span class="sxs-lookup"><span data-stu-id="73a94-237">greater</span></span>
<span data-ttu-id="73a94-238">Retorna `true` se o primeiro parâmetro é estritamente maior que o segundo parâmetro.</span><span class="sxs-lookup"><span data-stu-id="73a94-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="73a94-239">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="73a94-240">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="73a94-241">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="73a94-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="73a94-242">greaterOrEquals</span></span>
<span data-ttu-id="73a94-243">Retorna `true` se o primeiro parâmetro é maior ou igual ao segundo parâmetro.</span><span class="sxs-lookup"><span data-stu-id="73a94-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="73a94-244">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="73a94-245">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="73a94-246">e</span><span class="sxs-lookup"><span data-stu-id="73a94-246">and</span></span>
<span data-ttu-id="73a94-247">Retorna `true` se todos os parâmetros são avaliados como `true`.</span><span class="sxs-lookup"><span data-stu-id="73a94-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="73a94-248">Essa função dá suporte apenas a dois ou mais parâmetros do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="73a94-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="73a94-249">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="73a94-250">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="73a94-251">ou o</span><span class="sxs-lookup"><span data-stu-id="73a94-251">or</span></span>
<span data-ttu-id="73a94-252">Retorna `true` se, pelo menos, um dos parâmetros é avaliado como `true`.</span><span class="sxs-lookup"><span data-stu-id="73a94-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="73a94-253">Essa função dá suporte apenas a dois ou mais parâmetros do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="73a94-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="73a94-254">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="73a94-255">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="73a94-256">não</span><span class="sxs-lookup"><span data-stu-id="73a94-256">not</span></span>
<span data-ttu-id="73a94-257">Retorna `true` se o parâmetro é avaliado como `false`.</span><span class="sxs-lookup"><span data-stu-id="73a94-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="73a94-258">Essa função dá suporte apenas a parâmetros do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="73a94-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="73a94-259">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="73a94-260">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="73a94-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="73a94-261">coalesce</span></span>
<span data-ttu-id="73a94-262">Retorna o valor do primeiro parâmetro não nulo.</span><span class="sxs-lookup"><span data-stu-id="73a94-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="73a94-263">Essa função dá suporte a todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="73a94-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="73a94-264">Suponha que `element1` e `element2` são indefinidos.</span><span class="sxs-lookup"><span data-stu-id="73a94-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="73a94-265">O exemplo a seguir retorna `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="73a94-266">Funções de conversão</span><span class="sxs-lookup"><span data-stu-id="73a94-266">Conversion functions</span></span>
<span data-ttu-id="73a94-267">Essas funções podem ser usadas para converter valores entre tipos de dados JSON e codificações.</span><span class="sxs-lookup"><span data-stu-id="73a94-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="73a94-268">int</span><span class="sxs-lookup"><span data-stu-id="73a94-268">int</span></span>
<span data-ttu-id="73a94-269">Converte o parâmetro em um inteiro.</span><span class="sxs-lookup"><span data-stu-id="73a94-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="73a94-270">Essa função dá suporte a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="73a94-271">O exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="73a94-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="73a94-272">O exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="73a94-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="73a94-273">flutuante</span><span class="sxs-lookup"><span data-stu-id="73a94-273">float</span></span>
<span data-ttu-id="73a94-274">Converte o parâmetro em um ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="73a94-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="73a94-275">Essa função dá suporte a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="73a94-276">O exemplo a seguir retorna `1.0`:</span><span class="sxs-lookup"><span data-stu-id="73a94-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="73a94-277">O exemplo a seguir retorna `2.9`:</span><span class="sxs-lookup"><span data-stu-id="73a94-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="73a94-278">string</span><span class="sxs-lookup"><span data-stu-id="73a94-278">string</span></span>
<span data-ttu-id="73a94-279">Converte o parâmetro em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-279">Converts the parameter to a string.</span></span> <span data-ttu-id="73a94-280">Essa função dá suporte a parâmetros de todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="73a94-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="73a94-281">O exemplo a seguir retorna `"1"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="73a94-282">O exemplo a seguir retorna `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="73a94-283">O exemplo a seguir retorna `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="73a94-284">O exemplo a seguir retorna `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="73a94-285">bool</span><span class="sxs-lookup"><span data-stu-id="73a94-285">bool</span></span>
<span data-ttu-id="73a94-286">Converte o parâmetro em um booliano.</span><span class="sxs-lookup"><span data-stu-id="73a94-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="73a94-287">Essa função dá suporte a parâmetros dos tipos número, cadeia de caracteres e booliano.</span><span class="sxs-lookup"><span data-stu-id="73a94-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="73a94-288">Semelhante aos boolianos no JavaScript, qualquer valor, exceto `0` ou `'false'`, retorna `true`.</span><span class="sxs-lookup"><span data-stu-id="73a94-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="73a94-289">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="73a94-290">O exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="73a94-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="73a94-291">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="73a94-292">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="73a94-293">analisar</span><span class="sxs-lookup"><span data-stu-id="73a94-293">parse</span></span>
<span data-ttu-id="73a94-294">Converte o parâmetro em um tipo nativo.</span><span class="sxs-lookup"><span data-stu-id="73a94-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="73a94-295">Em outras palavras, essa função é o inverso de `string()`.</span><span class="sxs-lookup"><span data-stu-id="73a94-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="73a94-296">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="73a94-297">O exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="73a94-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="73a94-298">O exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="73a94-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="73a94-299">O exemplo a seguir retorna `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="73a94-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="73a94-300">O exemplo a seguir retorna `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="73a94-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="73a94-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="73a94-301">encodeBase64</span></span>
<span data-ttu-id="73a94-302">Codifica o parâmetro em uma cadeia de caracteres codificada em base 64.</span><span class="sxs-lookup"><span data-stu-id="73a94-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="73a94-303">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="73a94-304">O exemplo a seguir retorna `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="73a94-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="73a94-305">decodeBase64</span></span>
<span data-ttu-id="73a94-306">Decodifica o parâmetro de uma cadeia de caracteres codificada em base 64.</span><span class="sxs-lookup"><span data-stu-id="73a94-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="73a94-307">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="73a94-308">O exemplo a seguir retorna `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="73a94-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="73a94-309">encodeUriComponent</span></span>
<span data-ttu-id="73a94-310">Codifica o parâmetro em uma cadeia de caracteres codificada em URL.</span><span class="sxs-lookup"><span data-stu-id="73a94-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="73a94-311">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="73a94-312">O exemplo a seguir retorna `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="73a94-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="73a94-313">decodeUriComponent</span></span>
<span data-ttu-id="73a94-314">Decodifica o parâmetro de uma cadeia de caracteres codificada em URL.</span><span class="sxs-lookup"><span data-stu-id="73a94-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="73a94-315">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73a94-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="73a94-316">O exemplo a seguir retorna `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="73a94-317">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="73a94-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="73a94-318">Adicionar</span><span class="sxs-lookup"><span data-stu-id="73a94-318">add</span></span>
<span data-ttu-id="73a94-319">Adiciona dois números e retorna o resultado.</span><span class="sxs-lookup"><span data-stu-id="73a94-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="73a94-320">O exemplo a seguir retorna `3`:</span><span class="sxs-lookup"><span data-stu-id="73a94-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="73a94-321">sub</span><span class="sxs-lookup"><span data-stu-id="73a94-321">sub</span></span>
<span data-ttu-id="73a94-322">Subtrai o segundo número do primeiro número e retorna o resultado.</span><span class="sxs-lookup"><span data-stu-id="73a94-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="73a94-323">O exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="73a94-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="73a94-324">mul</span><span class="sxs-lookup"><span data-stu-id="73a94-324">mul</span></span>
<span data-ttu-id="73a94-325">Multiplica dois números e retorna o resultado.</span><span class="sxs-lookup"><span data-stu-id="73a94-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="73a94-326">O exemplo a seguir retorna `6`:</span><span class="sxs-lookup"><span data-stu-id="73a94-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="73a94-327">div</span><span class="sxs-lookup"><span data-stu-id="73a94-327">div</span></span>
<span data-ttu-id="73a94-328">Divide o primeiro número pelo segundo número e retorna o resultado.</span><span class="sxs-lookup"><span data-stu-id="73a94-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="73a94-329">O resultado é sempre um inteiro.</span><span class="sxs-lookup"><span data-stu-id="73a94-329">The result is always an integer.</span></span>

<span data-ttu-id="73a94-330">O exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="73a94-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="73a94-331">mod</span><span class="sxs-lookup"><span data-stu-id="73a94-331">mod</span></span>
<span data-ttu-id="73a94-332">Divide o primeiro número pelo segundo número e retorna a sobra.</span><span class="sxs-lookup"><span data-stu-id="73a94-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="73a94-333">O exemplo a seguir retorna `0`:</span><span class="sxs-lookup"><span data-stu-id="73a94-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="73a94-334">O exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="73a94-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="73a94-335">Min</span><span class="sxs-lookup"><span data-stu-id="73a94-335">min</span></span>
<span data-ttu-id="73a94-336">Retorna o menor dos dois números.</span><span class="sxs-lookup"><span data-stu-id="73a94-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="73a94-337">O exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="73a94-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="73a94-338">max</span><span class="sxs-lookup"><span data-stu-id="73a94-338">max</span></span>
<span data-ttu-id="73a94-339">Retorna o maior dos dois números.</span><span class="sxs-lookup"><span data-stu-id="73a94-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="73a94-340">O exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="73a94-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="73a94-341">range</span><span class="sxs-lookup"><span data-stu-id="73a94-341">range</span></span>
<span data-ttu-id="73a94-342">Gera uma sequência de números integrais dentro do intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="73a94-343">O exemplo a seguir retorna `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="73a94-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="73a94-344">rand</span><span class="sxs-lookup"><span data-stu-id="73a94-344">rand</span></span>
<span data-ttu-id="73a94-345">Retorna um número integral aleatório dentro do intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="73a94-346">Essa função não gera números aleatórios criptograficamente seguros.</span><span class="sxs-lookup"><span data-stu-id="73a94-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="73a94-347">O seguinte exemplo poderá retornar `42`:</span><span class="sxs-lookup"><span data-stu-id="73a94-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="73a94-348">floor</span><span class="sxs-lookup"><span data-stu-id="73a94-348">floor</span></span>
<span data-ttu-id="73a94-349">Retorna o maior inteiro menor ou igual ao número especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="73a94-350">O exemplo a seguir retorna `3`:</span><span class="sxs-lookup"><span data-stu-id="73a94-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="73a94-351">ceil</span><span class="sxs-lookup"><span data-stu-id="73a94-351">ceil</span></span>
<span data-ttu-id="73a94-352">Retorna o maior inteiro maior ou igual ao número especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="73a94-353">O exemplo a seguir retorna `4`:</span><span class="sxs-lookup"><span data-stu-id="73a94-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="73a94-354">Funções de data</span><span class="sxs-lookup"><span data-stu-id="73a94-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="73a94-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="73a94-355">utcNow</span></span>
<span data-ttu-id="73a94-356">Retorna uma cadeia de caracteres no formato ISO 8601 da data e hora atuais no computador local.</span><span class="sxs-lookup"><span data-stu-id="73a94-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="73a94-357">O seguinte exemplo poderá retornar `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="73a94-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="73a94-358">addSeconds</span></span>
<span data-ttu-id="73a94-359">Adiciona um número integral de segundos ao carimbo de data/hora especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="73a94-360">O exemplo a seguir retorna `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="73a94-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="73a94-361">addMinutes</span></span>
<span data-ttu-id="73a94-362">Adiciona um número integral de minutos ao carimbo de data/hora especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="73a94-363">O exemplo a seguir retorna `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="73a94-364">addHours</span><span class="sxs-lookup"><span data-stu-id="73a94-364">addHours</span></span>
<span data-ttu-id="73a94-365">Adiciona um número integral de horas ao carimbo de data/hora especificado.</span><span class="sxs-lookup"><span data-stu-id="73a94-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="73a94-366">O exemplo a seguir retorna `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="73a94-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="73a94-367">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73a94-367">Next steps</span></span>
* <span data-ttu-id="73a94-368">Para obter uma introdução ao Azure Resource Manager, consulte [Visão geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="73a94-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

