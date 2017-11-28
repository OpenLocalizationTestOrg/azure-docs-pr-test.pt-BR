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
# <a name="createuidefinition-functions"></a><span data-ttu-id="13e2d-103">Funções de CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="13e2d-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="13e2d-104">Esta seção contém assinaturas Olá para todas as funções com suporte de um CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="13e2d-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="13e2d-105">toouse uma função, a declaração de saudação surround com colchetes.</span><span class="sxs-lookup"><span data-stu-id="13e2d-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="13e2d-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="13e2d-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="13e2d-107">Cadeias de caracteres e outras funções podem ser referenciadas como parâmetros de uma função, mas as cadeias de caracteres devem estar entre aspas simples.</span><span class="sxs-lookup"><span data-stu-id="13e2d-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="13e2d-108">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="13e2d-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="13e2d-109">Onde aplicável, você pode fazer referência a propriedades de saída de saudação de uma função usando o operador de ponto de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="13e2d-110">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="13e2d-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="13e2d-111">Referenciando funções</span><span class="sxs-lookup"><span data-stu-id="13e2d-111">Referencing functions</span></span>
<span data-ttu-id="13e2d-112">Essas funções podem ser usados tooreference saídas de propriedades de saudação ou contexto de um CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="13e2d-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="13e2d-113">conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="13e2d-113">basics</span></span>
<span data-ttu-id="13e2d-114">Retorna valores de saída de saudação de um elemento que é definido na etapa de Noções básicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="13e2d-115">Hello exemplo a seguir retorna a saudação saída de elemento de saudação chamado `foo` na etapa do hello Noções básicas:</span><span class="sxs-lookup"><span data-stu-id="13e2d-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="13e2d-116">etapas</span><span class="sxs-lookup"><span data-stu-id="13e2d-116">steps</span></span>
<span data-ttu-id="13e2d-117">Retorna valores de saída de saudação de um elemento que está definido na etapa especificada hello.</span><span class="sxs-lookup"><span data-stu-id="13e2d-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="13e2d-118">valores de saída de hello tooget de elementos na etapa de Noções básicas de Olá, use `basics()` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="13e2d-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="13e2d-119">Hello exemplo a seguir retorna a saudação saída de elemento de saudação chamado `bar` na etapa Olá chamada `foo`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="13e2d-120">location</span><span class="sxs-lookup"><span data-stu-id="13e2d-120">location</span></span>
<span data-ttu-id="13e2d-121">Retorna o local de saudação selecionado na etapa de Noções básicas de saudação ou contexto atual hello.</span><span class="sxs-lookup"><span data-stu-id="13e2d-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="13e2d-122">Olá exemplo a seguir poderia retornar `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="13e2d-123">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-123">String functions</span></span>
<span data-ttu-id="13e2d-124">Essas funções podem ser usadas apenas com cadeias de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="13e2d-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="13e2d-125">concat</span><span class="sxs-lookup"><span data-stu-id="13e2d-125">concat</span></span>
<span data-ttu-id="13e2d-126">Concatena uma ou mais cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="13e2d-127">Por exemplo, se o valor de saída de hello `element1` se `"bar"`, em seguida, este exemplo retorna a cadeia de caracteres hello `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="13e2d-128">substring</span><span class="sxs-lookup"><span data-stu-id="13e2d-128">substring</span></span>
<span data-ttu-id="13e2d-129">Retorna subcadeia de caracteres de saudação do hello especificado a cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="13e2d-130">subcadeia de caracteres Hello começa no índice especificado da saudação e tem Olá comprimento especificado.</span><span class="sxs-lookup"><span data-stu-id="13e2d-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="13e2d-131">Olá exemplo a seguir retorna `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="13e2d-132">substitui</span><span class="sxs-lookup"><span data-stu-id="13e2d-132">replace</span></span>
<span data-ttu-id="13e2d-133">Retorna uma cadeia de caracteres na qual todas as ocorrências de saudação especificado cadeia de caracteres na cadeia de caracteres atual hello serão substituídas por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="13e2d-134">Olá exemplo a seguir retorna `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="13e2d-135">GUID</span><span class="sxs-lookup"><span data-stu-id="13e2d-135">guid</span></span>
<span data-ttu-id="13e2d-136">Gera uma cadeia de caracteres global exclusiva (GUID).</span><span class="sxs-lookup"><span data-stu-id="13e2d-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="13e2d-137">Olá exemplo a seguir poderia retornar `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="13e2d-138">toLower</span><span class="sxs-lookup"><span data-stu-id="13e2d-138">toLower</span></span>
<span data-ttu-id="13e2d-139">Retorna uma cadeia de caracteres convertida toolowercase.</span><span class="sxs-lookup"><span data-stu-id="13e2d-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="13e2d-140">Olá exemplo a seguir retorna `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="13e2d-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="13e2d-141">toUpper</span></span>
<span data-ttu-id="13e2d-142">Retorna uma cadeia de caracteres convertida toouppercase.</span><span class="sxs-lookup"><span data-stu-id="13e2d-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="13e2d-143">Olá exemplo a seguir retorna `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="13e2d-144">Funções de coleção</span><span class="sxs-lookup"><span data-stu-id="13e2d-144">Collection functions</span></span>
<span data-ttu-id="13e2d-145">Essas funções podem ser usadas com coleções, como cadeias de caracteres JSON, matrizes e objetos.</span><span class="sxs-lookup"><span data-stu-id="13e2d-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="13e2d-146">contains</span><span class="sxs-lookup"><span data-stu-id="13e2d-146">contains</span></span>
<span data-ttu-id="13e2d-147">Retorna `true` se uma cadeia de caracteres contiver Olá subcadeia de caracteres especificada, que contém uma matriz Olá especificado valor ou um objeto contém a chave especificada hello.</span><span class="sxs-lookup"><span data-stu-id="13e2d-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-148">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-148">Example 1: string</span></span>
<span data-ttu-id="13e2d-149">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-150">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-150">Example 2: array</span></span>
<span data-ttu-id="13e2d-151">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-152">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-153">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-153">Example 3: object</span></span>
<span data-ttu-id="13e2d-154">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="13e2d-155">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="13e2d-156">length</span><span class="sxs-lookup"><span data-stu-id="13e2d-156">length</span></span>
<span data-ttu-id="13e2d-157">Retorna o número de saudação de caracteres em uma cadeia de caracteres, Olá número de valores em uma matriz ou Olá número de chaves em um objeto.</span><span class="sxs-lookup"><span data-stu-id="13e2d-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-158">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-158">Example 1: string</span></span>
<span data-ttu-id="13e2d-159">Olá exemplo a seguir retorna `6`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-160">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-160">Example 2: array</span></span>
<span data-ttu-id="13e2d-161">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-162">Olá exemplo a seguir retorna `3`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-163">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-163">Example 3: object</span></span>
<span data-ttu-id="13e2d-164">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="13e2d-165">Olá exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="13e2d-166">empty</span><span class="sxs-lookup"><span data-stu-id="13e2d-166">empty</span></span>
<span data-ttu-id="13e2d-167">Retorna `true` se a cadeia de caracteres hello, matriz ou objeto é nulo ou vazio.</span><span class="sxs-lookup"><span data-stu-id="13e2d-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-168">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-168">Example 1: string</span></span>
<span data-ttu-id="13e2d-169">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-170">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-170">Example 2: array</span></span>
<span data-ttu-id="13e2d-171">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-172">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-173">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-173">Example 3: object</span></span>
<span data-ttu-id="13e2d-174">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="13e2d-175">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="13e2d-176">Exemplo 4: nulo e indefinido</span><span class="sxs-lookup"><span data-stu-id="13e2d-176">Example 4: null and undefined</span></span>
<span data-ttu-id="13e2d-177">Suponha que `element1` é `null` ou indefinido.</span><span class="sxs-lookup"><span data-stu-id="13e2d-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="13e2d-178">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="13e2d-179">first</span><span class="sxs-lookup"><span data-stu-id="13e2d-179">first</span></span>
<span data-ttu-id="13e2d-180">Retorna Olá primeiro caractere da saudação especificado de cadeia de caracteres; primeiro valor da matriz especificada de saudação; ou Olá primeira chave e o valor do objeto especificado hello.</span><span class="sxs-lookup"><span data-stu-id="13e2d-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-181">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-181">Example 1: string</span></span>
<span data-ttu-id="13e2d-182">Olá exemplo a seguir retorna `"f"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-183">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-183">Example 2: array</span></span>
<span data-ttu-id="13e2d-184">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-185">Olá exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-186">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-186">Example 3: object</span></span>
<span data-ttu-id="13e2d-187">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="13e2d-188">Olá exemplo a seguir retorna `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="13e2d-189">last</span><span class="sxs-lookup"><span data-stu-id="13e2d-189">last</span></span>
<span data-ttu-id="13e2d-190">Retorna Olá último caractere da saudação especificado string, o último valor de saudação do hello matriz especificada, a ou Olá a última chave e o valor do objeto especificado hello.</span><span class="sxs-lookup"><span data-stu-id="13e2d-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-191">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-191">Example 1: string</span></span>
<span data-ttu-id="13e2d-192">Olá exemplo a seguir retorna `"r"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-193">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-193">Example 2: array</span></span>
<span data-ttu-id="13e2d-194">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-195">Olá exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-196">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-196">Example 3: object</span></span>
<span data-ttu-id="13e2d-197">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="13e2d-198">Olá exemplo a seguir retorna `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="13e2d-199">take</span><span class="sxs-lookup"><span data-stu-id="13e2d-199">take</span></span>
<span data-ttu-id="13e2d-200">Retorna um número especificado de caracteres contíguos do início de saudação de cadeia de caracteres hello, um número especificado de valores contíguos do início de saudação da matriz hello ou um número especificado de contíguas chaves e valores de início de saudação do objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-201">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-201">Example 1: string</span></span>
<span data-ttu-id="13e2d-202">Olá exemplo a seguir retorna `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-203">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-203">Example 2: array</span></span>
<span data-ttu-id="13e2d-204">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-205">Olá exemplo a seguir retorna `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-206">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-206">Example 3: object</span></span>
<span data-ttu-id="13e2d-207">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="13e2d-208">Olá exemplo a seguir retorna `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="13e2d-209">skip</span><span class="sxs-lookup"><span data-stu-id="13e2d-209">skip</span></span>
<span data-ttu-id="13e2d-210">Ignora um número especificado de elementos em uma coleção e, em seguida, retorna Olá elementos restantes.</span><span class="sxs-lookup"><span data-stu-id="13e2d-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="13e2d-211">Exemplo 1: cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="13e2d-211">Example 1: string</span></span>
<span data-ttu-id="13e2d-212">Olá exemplo a seguir retorna `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="13e2d-213">Exemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="13e2d-213">Example 2: array</span></span>
<span data-ttu-id="13e2d-214">Suponha que `element1` retorne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="13e2d-215">Olá exemplo a seguir retorna `[3]`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="13e2d-216">Exemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="13e2d-216">Example 3: object</span></span>
<span data-ttu-id="13e2d-217">Suponha que `element1` retorne:</span><span class="sxs-lookup"><span data-stu-id="13e2d-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="13e2d-218">Olá exemplo a seguir retorna `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="13e2d-219">Funções lógicas</span><span class="sxs-lookup"><span data-stu-id="13e2d-219">Logical functions</span></span>
<span data-ttu-id="13e2d-220">Essas funções podem ser usadas em condicionais.</span><span class="sxs-lookup"><span data-stu-id="13e2d-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="13e2d-221">Algumas funções podem não dar suporte a todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="13e2d-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="13e2d-222">equals</span><span class="sxs-lookup"><span data-stu-id="13e2d-222">equals</span></span>
<span data-ttu-id="13e2d-223">Retorna `true` se ambos os parâmetros tiverem Olá mesmo tipo e valor.</span><span class="sxs-lookup"><span data-stu-id="13e2d-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="13e2d-224">Essa função dá suporte a todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="13e2d-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="13e2d-225">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="13e2d-226">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="13e2d-227">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="13e2d-228">less</span><span class="sxs-lookup"><span data-stu-id="13e2d-228">less</span></span>
<span data-ttu-id="13e2d-229">Retorna `true` se Olá primeiro parâmetro é estritamente menor do que o segundo parâmetro de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="13e2d-230">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="13e2d-231">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="13e2d-232">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="13e2d-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="13e2d-233">lessOrEquals</span></span>
<span data-ttu-id="13e2d-234">Retorna `true` se Olá primeiro parâmetro for menor ou igual toohello segundo parâmetro.</span><span class="sxs-lookup"><span data-stu-id="13e2d-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="13e2d-235">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="13e2d-236">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="13e2d-237">greater</span><span class="sxs-lookup"><span data-stu-id="13e2d-237">greater</span></span>
<span data-ttu-id="13e2d-238">Retorna `true` se Olá primeiro parâmetro é estritamente maior que o segundo parâmetro de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="13e2d-239">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="13e2d-240">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="13e2d-241">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="13e2d-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="13e2d-242">greaterOrEquals</span></span>
<span data-ttu-id="13e2d-243">Retorna `true` se Olá primeiro parâmetro for maior que ou igual toohello segundo parâmetro.</span><span class="sxs-lookup"><span data-stu-id="13e2d-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="13e2d-244">Essa função dá suporte apenas a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="13e2d-245">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="13e2d-246">e</span><span class="sxs-lookup"><span data-stu-id="13e2d-246">and</span></span>
<span data-ttu-id="13e2d-247">Retorna `true` se todos os parâmetros de saudação avaliam muito`true`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="13e2d-248">Essa função dá suporte apenas a dois ou mais parâmetros do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="13e2d-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="13e2d-249">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="13e2d-250">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="13e2d-251">ou o</span><span class="sxs-lookup"><span data-stu-id="13e2d-251">or</span></span>
<span data-ttu-id="13e2d-252">Retorna `true` se pelo menos um dos parâmetros de saudação avalia muito`true`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="13e2d-253">Essa função dá suporte apenas a dois ou mais parâmetros do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="13e2d-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="13e2d-254">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="13e2d-255">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="13e2d-256">não</span><span class="sxs-lookup"><span data-stu-id="13e2d-256">not</span></span>
<span data-ttu-id="13e2d-257">Retorna `true` se o parâmetro hello avalia muito`false`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="13e2d-258">Essa função dá suporte apenas a parâmetros do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="13e2d-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="13e2d-259">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="13e2d-260">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="13e2d-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="13e2d-261">coalesce</span></span>
<span data-ttu-id="13e2d-262">Retorna Olá valor Olá não nulo do parâmetro da primeira.</span><span class="sxs-lookup"><span data-stu-id="13e2d-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="13e2d-263">Essa função dá suporte a todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="13e2d-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="13e2d-264">Suponha que `element1` e `element2` são indefinidos.</span><span class="sxs-lookup"><span data-stu-id="13e2d-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="13e2d-265">Olá exemplo a seguir retorna `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="13e2d-266">Funções de conversão</span><span class="sxs-lookup"><span data-stu-id="13e2d-266">Conversion functions</span></span>
<span data-ttu-id="13e2d-267">Essas funções podem ser valores de tooconvert usado entre codificações e tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="13e2d-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="13e2d-268">int</span><span class="sxs-lookup"><span data-stu-id="13e2d-268">int</span></span>
<span data-ttu-id="13e2d-269">Converte o inteiro de tooan parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="13e2d-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="13e2d-270">Essa função dá suporte a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="13e2d-271">Olá exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="13e2d-272">Olá exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="13e2d-273">flutuante</span><span class="sxs-lookup"><span data-stu-id="13e2d-273">float</span></span>
<span data-ttu-id="13e2d-274">Converte Olá parâmetro tooa ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="13e2d-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="13e2d-275">Essa função dá suporte a parâmetros dos tipos número e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="13e2d-276">Olá exemplo a seguir retorna `1.0`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="13e2d-277">Olá exemplo a seguir retorna `2.9`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="13e2d-278">string</span><span class="sxs-lookup"><span data-stu-id="13e2d-278">string</span></span>
<span data-ttu-id="13e2d-279">Converte a cadeia de caracteres hello parâmetro tooa.</span><span class="sxs-lookup"><span data-stu-id="13e2d-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="13e2d-280">Essa função dá suporte a parâmetros de todos os tipos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="13e2d-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="13e2d-281">Olá exemplo a seguir retorna `"1"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="13e2d-282">Olá exemplo a seguir retorna `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="13e2d-283">Olá exemplo a seguir retorna `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="13e2d-284">Olá exemplo a seguir retorna `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="13e2d-285">bool</span><span class="sxs-lookup"><span data-stu-id="13e2d-285">bool</span></span>
<span data-ttu-id="13e2d-286">Converte Olá parâmetro tooa booliano.</span><span class="sxs-lookup"><span data-stu-id="13e2d-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="13e2d-287">Essa função dá suporte a parâmetros dos tipos número, cadeia de caracteres e booliano.</span><span class="sxs-lookup"><span data-stu-id="13e2d-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="13e2d-288">TooBooleans semelhante em JavaScript, qualquer valor exceto `0` ou `'false'` retorna `true`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="13e2d-289">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="13e2d-290">Olá exemplo a seguir retorna `false`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="13e2d-291">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="13e2d-292">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="13e2d-293">analisar</span><span class="sxs-lookup"><span data-stu-id="13e2d-293">parse</span></span>
<span data-ttu-id="13e2d-294">Converte tipo nativo do hello parâmetro tooa.</span><span class="sxs-lookup"><span data-stu-id="13e2d-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="13e2d-295">Em outras palavras, essa função é o inverso da saudação `string()`.</span><span class="sxs-lookup"><span data-stu-id="13e2d-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="13e2d-296">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="13e2d-297">Olá exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="13e2d-298">Olá exemplo a seguir retorna `true`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="13e2d-299">Olá exemplo a seguir retorna `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="13e2d-300">Olá exemplo a seguir retorna `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="13e2d-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="13e2d-301">encodeBase64</span></span>
<span data-ttu-id="13e2d-302">Codifica Olá parâmetro tooa base 64 cadeia de caracteres codificada.</span><span class="sxs-lookup"><span data-stu-id="13e2d-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="13e2d-303">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="13e2d-304">Olá exemplo a seguir retorna `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="13e2d-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="13e2d-305">decodeBase64</span></span>
<span data-ttu-id="13e2d-306">Decodifica o parâmetro hello de uma cadeia de caracteres codificada de base 64.</span><span class="sxs-lookup"><span data-stu-id="13e2d-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="13e2d-307">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="13e2d-308">Olá exemplo a seguir retorna `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="13e2d-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="13e2d-309">encodeUriComponent</span></span>
<span data-ttu-id="13e2d-310">Codifica a cadeia de caracteres codificados de URL tooa de parâmetro de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="13e2d-311">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="13e2d-312">Olá exemplo a seguir retorna `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="13e2d-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="13e2d-313">decodeUriComponent</span></span>
<span data-ttu-id="13e2d-314">Decodifica o parâmetro hello de uma cadeia de caracteres codificados de URL.</span><span class="sxs-lookup"><span data-stu-id="13e2d-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="13e2d-315">Essa função dá suporte apenas a parâmetros do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="13e2d-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="13e2d-316">Olá exemplo a seguir retorna `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="13e2d-317">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="13e2d-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="13e2d-318">adicionar</span><span class="sxs-lookup"><span data-stu-id="13e2d-318">add</span></span>
<span data-ttu-id="13e2d-319">Adiciona dois números e retorna o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="13e2d-320">Olá exemplo a seguir retorna `3`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="13e2d-321">sub</span><span class="sxs-lookup"><span data-stu-id="13e2d-321">sub</span></span>
<span data-ttu-id="13e2d-322">Subtrai o segundo o número do primeiro número de Olá Olá e retorna o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="13e2d-323">Olá exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="13e2d-324">mul</span><span class="sxs-lookup"><span data-stu-id="13e2d-324">mul</span></span>
<span data-ttu-id="13e2d-325">Multiplica dois números e retorna o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="13e2d-326">Olá exemplo a seguir retorna `6`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="13e2d-327">div</span><span class="sxs-lookup"><span data-stu-id="13e2d-327">div</span></span>
<span data-ttu-id="13e2d-328">Divide o número de primeira Olá por segundo hello e retorna o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="13e2d-329">resultado de saudação sempre é um inteiro.</span><span class="sxs-lookup"><span data-stu-id="13e2d-329">hello result is always an integer.</span></span>

<span data-ttu-id="13e2d-330">Olá exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="13e2d-331">mod</span><span class="sxs-lookup"><span data-stu-id="13e2d-331">mod</span></span>
<span data-ttu-id="13e2d-332">Divide o número de primeira Olá por segundo hello e retorna o resto de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="13e2d-333">Olá exemplo a seguir retorna `0`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="13e2d-334">Olá exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="13e2d-335">Min</span><span class="sxs-lookup"><span data-stu-id="13e2d-335">min</span></span>
<span data-ttu-id="13e2d-336">Retorna Olá pequeno de números de saudação dois.</span><span class="sxs-lookup"><span data-stu-id="13e2d-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="13e2d-337">Olá exemplo a seguir retorna `1`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="13e2d-338">max</span><span class="sxs-lookup"><span data-stu-id="13e2d-338">max</span></span>
<span data-ttu-id="13e2d-339">Olá retorna mais de dois números de saudação.</span><span class="sxs-lookup"><span data-stu-id="13e2d-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="13e2d-340">Olá exemplo a seguir retorna `2`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="13e2d-341">range</span><span class="sxs-lookup"><span data-stu-id="13e2d-341">range</span></span>
<span data-ttu-id="13e2d-342">Gera uma sequência de integral números em Olá o intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="13e2d-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="13e2d-343">Olá exemplo a seguir retorna `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="13e2d-344">rand</span><span class="sxs-lookup"><span data-stu-id="13e2d-344">rand</span></span>
<span data-ttu-id="13e2d-345">Retorna um aleatório número integral em Olá o intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="13e2d-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="13e2d-346">Essa função não gera números aleatórios criptograficamente seguros.</span><span class="sxs-lookup"><span data-stu-id="13e2d-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="13e2d-347">Olá exemplo a seguir poderia retornar `42`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="13e2d-348">floor</span><span class="sxs-lookup"><span data-stu-id="13e2d-348">floor</span></span>
<span data-ttu-id="13e2d-349">Retorna o hello maior inteiro menor ou igual toohello no número especificado.</span><span class="sxs-lookup"><span data-stu-id="13e2d-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="13e2d-350">Olá exemplo a seguir retorna `3`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="13e2d-351">ceil</span><span class="sxs-lookup"><span data-stu-id="13e2d-351">ceil</span></span>
<span data-ttu-id="13e2d-352">Retorna Olá maior número inteiro maior ou igual toohello no número especificado.</span><span class="sxs-lookup"><span data-stu-id="13e2d-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="13e2d-353">Olá exemplo a seguir retorna `4`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="13e2d-354">Funções de data</span><span class="sxs-lookup"><span data-stu-id="13e2d-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="13e2d-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="13e2d-355">utcNow</span></span>
<span data-ttu-id="13e2d-356">Retorna uma cadeia de caracteres no formato ISO 8601 de saudação data e hora no computador local Olá atuais.</span><span class="sxs-lookup"><span data-stu-id="13e2d-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="13e2d-357">Olá exemplo a seguir poderia retornar `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="13e2d-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="13e2d-358">addSeconds</span></span>
<span data-ttu-id="13e2d-359">Adiciona um número integral de toohello de segundos especificado timestamp.</span><span class="sxs-lookup"><span data-stu-id="13e2d-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="13e2d-360">Olá exemplo a seguir retorna `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="13e2d-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="13e2d-361">addMinutes</span></span>
<span data-ttu-id="13e2d-362">Adiciona um número integral de toohello de minutos especificado timestamp.</span><span class="sxs-lookup"><span data-stu-id="13e2d-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="13e2d-363">Olá exemplo a seguir retorna `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="13e2d-364">addHours</span><span class="sxs-lookup"><span data-stu-id="13e2d-364">addHours</span></span>
<span data-ttu-id="13e2d-365">Adiciona um número integral de toohello de horas especificado timestamp.</span><span class="sxs-lookup"><span data-stu-id="13e2d-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="13e2d-366">Olá exemplo a seguir retorna `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="13e2d-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="13e2d-367">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13e2d-367">Next steps</span></span>
* <span data-ttu-id="13e2d-368">Para uma introdução tooAzure Gerenciador de recursos, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13e2d-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

