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
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="d38a4-103">Funções de matriz e objeto para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d38a4-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="d38a4-104">O Resource Manager fornece diversas funções para trabalhar com matrizes e objetos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="d38a4-105">array</span><span class="sxs-lookup"><span data-stu-id="d38a4-105">array</span></span>](#array)
* [<span data-ttu-id="d38a4-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="d38a4-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="d38a4-107">concat</span><span class="sxs-lookup"><span data-stu-id="d38a4-107">concat</span></span>](#concat)
* [<span data-ttu-id="d38a4-108">contains</span><span class="sxs-lookup"><span data-stu-id="d38a4-108">contains</span></span>](#contains)
* [<span data-ttu-id="d38a4-109">createArray</span><span class="sxs-lookup"><span data-stu-id="d38a4-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="d38a4-110">empty</span><span class="sxs-lookup"><span data-stu-id="d38a4-110">empty</span></span>](#empty)
* [<span data-ttu-id="d38a4-111">first</span><span class="sxs-lookup"><span data-stu-id="d38a4-111">first</span></span>](#first)
* [<span data-ttu-id="d38a4-112">intersection</span><span class="sxs-lookup"><span data-stu-id="d38a4-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="d38a4-113">json</span><span class="sxs-lookup"><span data-stu-id="d38a4-113">json</span></span>](#json)
* [<span data-ttu-id="d38a4-114">last</span><span class="sxs-lookup"><span data-stu-id="d38a4-114">last</span></span>](#last)
* [<span data-ttu-id="d38a4-115">length</span><span class="sxs-lookup"><span data-stu-id="d38a4-115">length</span></span>](#length)
* [<span data-ttu-id="d38a4-116">min</span><span class="sxs-lookup"><span data-stu-id="d38a4-116">min</span></span>](#min)
* [<span data-ttu-id="d38a4-117">max</span><span class="sxs-lookup"><span data-stu-id="d38a4-117">max</span></span>](#max)
* [<span data-ttu-id="d38a4-118">range</span><span class="sxs-lookup"><span data-stu-id="d38a4-118">range</span></span>](#range)
* [<span data-ttu-id="d38a4-119">skip</span><span class="sxs-lookup"><span data-stu-id="d38a4-119">skip</span></span>](#skip)
* [<span data-ttu-id="d38a4-120">take</span><span class="sxs-lookup"><span data-stu-id="d38a4-120">take</span></span>](#take)
* [<span data-ttu-id="d38a4-121">union</span><span class="sxs-lookup"><span data-stu-id="d38a4-121">union</span></span>](#union)

<span data-ttu-id="d38a4-122">tooget uma matriz de valores de cadeia de caracteres delimitada por um valor, consulte [dividir](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="d38a4-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="d38a4-123">array</span><span class="sxs-lookup"><span data-stu-id="d38a4-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="d38a4-124">Converte Olá valor tooan matriz.</span><span class="sxs-lookup"><span data-stu-id="d38a4-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-125">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-125">Parameters</span></span>

| <span data-ttu-id="d38a4-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-126">Parameter</span></span> | <span data-ttu-id="d38a4-127">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-127">Required</span></span> | <span data-ttu-id="d38a4-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-128">Type</span></span> | <span data-ttu-id="d38a4-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="d38a4-130">convertToArray</span></span> |<span data-ttu-id="d38a4-131">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-131">Yes</span></span> |<span data-ttu-id="d38a4-132">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="d38a4-132">int, string, array, or object</span></span> |<span data-ttu-id="d38a4-133">matriz de tooan tooconvert do valor Hello.</span><span class="sxs-lookup"><span data-stu-id="d38a4-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-134">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-134">Return value</span></span>

<span data-ttu-id="d38a4-135">Uma matriz.</span><span class="sxs-lookup"><span data-stu-id="d38a4-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-136">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-136">Example</span></span>

<span data-ttu-id="d38a4-137">Olá exemplo a seguir mostra como toouse Olá a função de matriz com tipos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d38a4-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="d38a4-138">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-139">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-139">Name</span></span> | <span data-ttu-id="d38a4-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-140">Type</span></span> | <span data-ttu-id="d38a4-141">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-142">intOutput</span></span> | <span data-ttu-id="d38a4-143">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-143">Array</span></span> | <span data-ttu-id="d38a4-144">[1]</span><span class="sxs-lookup"><span data-stu-id="d38a4-144">[1]</span></span> |
| <span data-ttu-id="d38a4-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-145">stringOutput</span></span> | <span data-ttu-id="d38a4-146">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-146">Array</span></span> | <span data-ttu-id="d38a4-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-147">["a"]</span></span> |
| <span data-ttu-id="d38a4-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-148">objectOutput</span></span> | <span data-ttu-id="d38a4-149">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-149">Array</span></span> | <span data-ttu-id="d38a4-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="d38a4-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="d38a4-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="d38a4-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="d38a4-152">Retorna o primeiro valor não nulo de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="d38a4-153">Cadeias de caracteres vazias, matrizes vazias e objetos vazios não são nulos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-154">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-154">Parameters</span></span>

| <span data-ttu-id="d38a4-155">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-155">Parameter</span></span> | <span data-ttu-id="d38a4-156">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-156">Required</span></span> | <span data-ttu-id="d38a4-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-157">Type</span></span> | <span data-ttu-id="d38a4-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-159">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-159">arg1</span></span> |<span data-ttu-id="d38a4-160">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-160">Yes</span></span> |<span data-ttu-id="d38a4-161">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="d38a4-161">int, string, array, or object</span></span> |<span data-ttu-id="d38a4-162">Olá primeiro tootest de valor para null.</span><span class="sxs-lookup"><span data-stu-id="d38a4-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="d38a4-163">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="d38a4-163">additional args</span></span> |<span data-ttu-id="d38a4-164">Não</span><span class="sxs-lookup"><span data-stu-id="d38a4-164">No</span></span> |<span data-ttu-id="d38a4-165">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="d38a4-165">int, string, array, or object</span></span> |<span data-ttu-id="d38a4-166">Tootest valores adicionais para null.</span><span class="sxs-lookup"><span data-stu-id="d38a4-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-167">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-167">Return value</span></span>

<span data-ttu-id="d38a4-168">valor de saudação do hello primeiro parâmetros não nulos, que pode ser uma cadeia de caracteres, int, matriz ou objeto.</span><span class="sxs-lookup"><span data-stu-id="d38a4-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="d38a4-169">Null se todos os parâmetros forem nulos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="d38a4-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-170">Example</span></span>

<span data-ttu-id="d38a4-171">Olá, exemplo a seguir mostra saída Olá usa diferentes de adesão.</span><span class="sxs-lookup"><span data-stu-id="d38a4-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="d38a4-172">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-173">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-173">Name</span></span> | <span data-ttu-id="d38a4-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-174">Type</span></span> | <span data-ttu-id="d38a4-175">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-176">stringOutput</span></span> | <span data-ttu-id="d38a4-177">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-177">String</span></span> | <span data-ttu-id="d38a4-178">padrão</span><span class="sxs-lookup"><span data-stu-id="d38a4-178">default</span></span> |
| <span data-ttu-id="d38a4-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-179">intOutput</span></span> | <span data-ttu-id="d38a4-180">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-180">Int</span></span> | <span data-ttu-id="d38a4-181">1</span><span class="sxs-lookup"><span data-stu-id="d38a4-181">1</span></span> |
| <span data-ttu-id="d38a4-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-182">objectOutput</span></span> | <span data-ttu-id="d38a4-183">Objeto</span><span class="sxs-lookup"><span data-stu-id="d38a4-183">Object</span></span> | <span data-ttu-id="d38a4-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="d38a4-184">{"first": "default"}</span></span> |
| <span data-ttu-id="d38a4-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-185">arrayOutput</span></span> | <span data-ttu-id="d38a4-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-186">Array</span></span> | <span data-ttu-id="d38a4-187">[1]</span><span class="sxs-lookup"><span data-stu-id="d38a4-187">[1]</span></span> |
| <span data-ttu-id="d38a4-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-188">emptyOutput</span></span> | <span data-ttu-id="d38a4-189">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-189">Bool</span></span> | <span data-ttu-id="d38a4-190">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="d38a4-191">concat</span><span class="sxs-lookup"><span data-stu-id="d38a4-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="d38a4-192">Combina vários conjuntos e retorna Olá concatenado matriz, ou combina vários valores de cadeia de caracteres e retorna a cadeia de caracteres hello concatenado.</span><span class="sxs-lookup"><span data-stu-id="d38a4-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="d38a4-193">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-193">Parameters</span></span>

| <span data-ttu-id="d38a4-194">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-194">Parameter</span></span> | <span data-ttu-id="d38a4-195">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-195">Required</span></span> | <span data-ttu-id="d38a4-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-196">Type</span></span> | <span data-ttu-id="d38a4-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-198">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-198">arg1</span></span> |<span data-ttu-id="d38a4-199">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-199">Yes</span></span> |<span data-ttu-id="d38a4-200">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-200">array or string</span></span> |<span data-ttu-id="d38a4-201">Olá primeira matriz ou cadeia de caracteres para concatenação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="d38a4-202">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="d38a4-202">additional arguments</span></span> |<span data-ttu-id="d38a4-203">Não</span><span class="sxs-lookup"><span data-stu-id="d38a4-203">No</span></span> |<span data-ttu-id="d38a4-204">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-204">array or string</span></span> |<span data-ttu-id="d38a4-205">Matrizes ou cadeias de caractere adicionais em ordem sequencial para concatenação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="d38a4-206">Essa função pode conter qualquer número de argumentos e pode aceitar cadeias de caracteres ou matrizes de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="d38a4-207">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-207">Return value</span></span>
<span data-ttu-id="d38a4-208">Uma cadeia de caracteres ou matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="d38a4-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-209">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-209">Example</span></span>

<span data-ttu-id="d38a4-210">saudação de exemplo a seguir mostra como toocombine duas matrizes.</span><span class="sxs-lookup"><span data-stu-id="d38a4-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="d38a4-211">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-212">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-212">Name</span></span> | <span data-ttu-id="d38a4-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-213">Type</span></span> | <span data-ttu-id="d38a4-214">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-215">retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-215">return</span></span> | <span data-ttu-id="d38a4-216">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-216">Array</span></span> | <span data-ttu-id="d38a4-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="d38a4-218">saudação de exemplo a seguir mostra como toocombine dois valores de cadeia de caracteres e retorna uma cadeia de caracteres concatenada.</span><span class="sxs-lookup"><span data-stu-id="d38a4-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="d38a4-219">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-220">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-220">Name</span></span> | <span data-ttu-id="d38a4-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-221">Type</span></span> | <span data-ttu-id="d38a4-222">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-223">concatOutput</span></span> | <span data-ttu-id="d38a4-224">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-224">String</span></span> | <span data-ttu-id="d38a4-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="d38a4-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="d38a4-226">contains</span><span class="sxs-lookup"><span data-stu-id="d38a4-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="d38a4-227">Verifica se uma matriz contém um valor, um objeto contém uma chave ou uma cadeia de caracteres contém uma subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-228">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-228">Parameters</span></span>

| <span data-ttu-id="d38a4-229">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-229">Parameter</span></span> | <span data-ttu-id="d38a4-230">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-230">Required</span></span> | <span data-ttu-id="d38a4-231">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-231">Type</span></span> | <span data-ttu-id="d38a4-232">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-233">contêiner</span><span class="sxs-lookup"><span data-stu-id="d38a4-233">container</span></span> |<span data-ttu-id="d38a4-234">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-234">Yes</span></span> |<span data-ttu-id="d38a4-235">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-235">array, object, or string</span></span> |<span data-ttu-id="d38a4-236">valor de saudação que contém Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d38a4-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="d38a4-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="d38a4-237">itemToFind</span></span> |<span data-ttu-id="d38a4-238">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-238">Yes</span></span> |<span data-ttu-id="d38a4-239">string ou int</span><span class="sxs-lookup"><span data-stu-id="d38a4-239">string or int</span></span> |<span data-ttu-id="d38a4-240">Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d38a4-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-241">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-241">Return value</span></span>

<span data-ttu-id="d38a4-242">**True** se o item de saudação for encontrado; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="d38a4-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-243">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-243">Example</span></span>

<span data-ttu-id="d38a4-244">Olá exemplo a seguir mostra como toouse contém com tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="d38a4-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="d38a4-245">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-246">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-246">Name</span></span> | <span data-ttu-id="d38a4-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-247">Type</span></span> | <span data-ttu-id="d38a4-248">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="d38a4-249">stringTrue</span></span> | <span data-ttu-id="d38a4-250">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-250">Bool</span></span> | <span data-ttu-id="d38a4-251">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-251">True</span></span> |
| <span data-ttu-id="d38a4-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="d38a4-252">stringFalse</span></span> | <span data-ttu-id="d38a4-253">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-253">Bool</span></span> | <span data-ttu-id="d38a4-254">Falso</span><span class="sxs-lookup"><span data-stu-id="d38a4-254">False</span></span> |
| <span data-ttu-id="d38a4-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="d38a4-255">objectTrue</span></span> | <span data-ttu-id="d38a4-256">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-256">Bool</span></span> | <span data-ttu-id="d38a4-257">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-257">True</span></span> |
| <span data-ttu-id="d38a4-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="d38a4-258">objectFalse</span></span> | <span data-ttu-id="d38a4-259">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-259">Bool</span></span> | <span data-ttu-id="d38a4-260">Falso</span><span class="sxs-lookup"><span data-stu-id="d38a4-260">False</span></span> |
| <span data-ttu-id="d38a4-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="d38a4-261">arrayTrue</span></span> | <span data-ttu-id="d38a4-262">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-262">Bool</span></span> | <span data-ttu-id="d38a4-263">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-263">True</span></span> |
| <span data-ttu-id="d38a4-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="d38a4-264">arrayFalse</span></span> | <span data-ttu-id="d38a4-265">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-265">Bool</span></span> | <span data-ttu-id="d38a4-266">Falso</span><span class="sxs-lookup"><span data-stu-id="d38a4-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="d38a4-267">createarray</span><span class="sxs-lookup"><span data-stu-id="d38a4-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="d38a4-268">Cria uma matriz de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-269">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-269">Parameters</span></span>

| <span data-ttu-id="d38a4-270">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-270">Parameter</span></span> | <span data-ttu-id="d38a4-271">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-271">Required</span></span> | <span data-ttu-id="d38a4-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-272">Type</span></span> | <span data-ttu-id="d38a4-273">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-274">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-274">arg1</span></span> |<span data-ttu-id="d38a4-275">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-275">Yes</span></span> |<span data-ttu-id="d38a4-276">String, Inteiro, Matriz ou Objeto</span><span class="sxs-lookup"><span data-stu-id="d38a4-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="d38a4-277">primeiro valor na matriz Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="d38a4-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="d38a4-278">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="d38a4-278">additional arguments</span></span> |<span data-ttu-id="d38a4-279">Não</span><span class="sxs-lookup"><span data-stu-id="d38a4-279">No</span></span> |<span data-ttu-id="d38a4-280">String, Inteiro, Matriz ou Objeto</span><span class="sxs-lookup"><span data-stu-id="d38a4-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="d38a4-281">Valores adicionais na matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-282">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-282">Return value</span></span>

<span data-ttu-id="d38a4-283">Uma matriz.</span><span class="sxs-lookup"><span data-stu-id="d38a4-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-284">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-284">Example</span></span>

<span data-ttu-id="d38a4-285">Olá mostrado no exemplo a seguir como toouse createArray com tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="d38a4-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="d38a4-286">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-287">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-287">Name</span></span> | <span data-ttu-id="d38a4-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-288">Type</span></span> | <span data-ttu-id="d38a4-289">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="d38a4-290">stringArray</span></span> | <span data-ttu-id="d38a4-291">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-291">Array</span></span> | <span data-ttu-id="d38a4-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="d38a4-293">intArray</span><span class="sxs-lookup"><span data-stu-id="d38a4-293">intArray</span></span> | <span data-ttu-id="d38a4-294">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-294">Array</span></span> | <span data-ttu-id="d38a4-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="d38a4-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="d38a4-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="d38a4-296">objectArray</span></span> | <span data-ttu-id="d38a4-297">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-297">Array</span></span> | <span data-ttu-id="d38a4-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="d38a4-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="d38a4-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="d38a4-299">arrayArray</span></span> | <span data-ttu-id="d38a4-300">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-300">Array</span></span> | <span data-ttu-id="d38a4-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="d38a4-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="d38a4-302">empty</span><span class="sxs-lookup"><span data-stu-id="d38a4-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="d38a4-303">Determina se uma matriz, objeto ou uma cadeia de caracteres está vazio.</span><span class="sxs-lookup"><span data-stu-id="d38a4-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-304">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-304">Parameters</span></span>

| <span data-ttu-id="d38a4-305">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-305">Parameter</span></span> | <span data-ttu-id="d38a4-306">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-306">Required</span></span> | <span data-ttu-id="d38a4-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-307">Type</span></span> | <span data-ttu-id="d38a4-308">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="d38a4-309">itemToTest</span></span> |<span data-ttu-id="d38a4-310">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-310">Yes</span></span> |<span data-ttu-id="d38a4-311">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-311">array, object, or string</span></span> |<span data-ttu-id="d38a4-312">Olá toocheck valor se ele estiver vazio.</span><span class="sxs-lookup"><span data-stu-id="d38a4-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-313">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-313">Return value</span></span>

<span data-ttu-id="d38a4-314">Retorna **True** se o valor de saudação está vazio; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="d38a4-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-315">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-315">Example</span></span>

<span data-ttu-id="d38a4-316">saudação de exemplo a seguir verifica se uma matriz, objeto e a cadeia de caracteres estão vazios.</span><span class="sxs-lookup"><span data-stu-id="d38a4-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="d38a4-317">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-318">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-318">Name</span></span> | <span data-ttu-id="d38a4-319">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-319">Type</span></span> | <span data-ttu-id="d38a4-320">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="d38a4-321">arrayEmpty</span></span> | <span data-ttu-id="d38a4-322">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-322">Bool</span></span> | <span data-ttu-id="d38a4-323">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-323">True</span></span> |
| <span data-ttu-id="d38a4-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="d38a4-324">objectEmpty</span></span> | <span data-ttu-id="d38a4-325">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-325">Bool</span></span> | <span data-ttu-id="d38a4-326">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-326">True</span></span> |
| <span data-ttu-id="d38a4-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="d38a4-327">stringEmpty</span></span> | <span data-ttu-id="d38a4-328">Bool</span><span class="sxs-lookup"><span data-stu-id="d38a4-328">Bool</span></span> | <span data-ttu-id="d38a4-329">True </span><span class="sxs-lookup"><span data-stu-id="d38a4-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="d38a4-330">first</span><span class="sxs-lookup"><span data-stu-id="d38a4-330">first</span></span>
`first(arg1)`

<span data-ttu-id="d38a4-331">Retorna Olá primeiro elemento da matriz de saudação ou o primeiro caractere da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-332">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-332">Parameters</span></span>

| <span data-ttu-id="d38a4-333">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-333">Parameter</span></span> | <span data-ttu-id="d38a4-334">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-334">Required</span></span> | <span data-ttu-id="d38a4-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-335">Type</span></span> | <span data-ttu-id="d38a4-336">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-337">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-337">arg1</span></span> |<span data-ttu-id="d38a4-338">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-338">Yes</span></span> |<span data-ttu-id="d38a4-339">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-339">array or string</span></span> |<span data-ttu-id="d38a4-340">Olá valor tooretrieve Olá primeiro elemento ou um caractere.</span><span class="sxs-lookup"><span data-stu-id="d38a4-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-341">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-341">Return value</span></span>

<span data-ttu-id="d38a4-342">tipo de saudação (string, int, matriz ou objeto) do primeiro elemento Olá em uma matriz, ou o primeiro caractere de saudação de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-343">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-343">Example</span></span>

<span data-ttu-id="d38a4-344">Olá exemplo a seguir mostra como toouse Olá primeira função com uma matriz e a cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="d38a4-345">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-346">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-346">Name</span></span> | <span data-ttu-id="d38a4-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-347">Type</span></span> | <span data-ttu-id="d38a4-348">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-349">arrayOutput</span></span> | <span data-ttu-id="d38a4-350">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-350">String</span></span> | <span data-ttu-id="d38a4-351">one</span><span class="sxs-lookup"><span data-stu-id="d38a4-351">one</span></span> |
| <span data-ttu-id="d38a4-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-352">stringOutput</span></span> | <span data-ttu-id="d38a4-353">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-353">String</span></span> | <span data-ttu-id="d38a4-354">O</span><span class="sxs-lookup"><span data-stu-id="d38a4-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="d38a4-355">interseção</span><span class="sxs-lookup"><span data-stu-id="d38a4-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="d38a4-356">Retorna uma matriz ou objeto com elementos comuns Olá de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-357">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-357">Parameters</span></span>

| <span data-ttu-id="d38a4-358">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-358">Parameter</span></span> | <span data-ttu-id="d38a4-359">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-359">Required</span></span> | <span data-ttu-id="d38a4-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-360">Type</span></span> | <span data-ttu-id="d38a4-361">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-362">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-362">arg1</span></span> |<span data-ttu-id="d38a4-363">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-363">Yes</span></span> |<span data-ttu-id="d38a4-364">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-364">array or object</span></span> |<span data-ttu-id="d38a4-365">Olá primeiro toouse de valor para a localização de elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="d38a4-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="d38a4-366">arg2</span><span class="sxs-lookup"><span data-stu-id="d38a4-366">arg2</span></span> |<span data-ttu-id="d38a4-367">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-367">Yes</span></span> |<span data-ttu-id="d38a4-368">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-368">array or object</span></span> |<span data-ttu-id="d38a4-369">Olá segundo toouse de valor para a localização de elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="d38a4-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="d38a4-370">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="d38a4-370">additional arguments</span></span> |<span data-ttu-id="d38a4-371">Não</span><span class="sxs-lookup"><span data-stu-id="d38a4-371">No</span></span> |<span data-ttu-id="d38a4-372">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-372">array or object</span></span> |<span data-ttu-id="d38a4-373">Toouse valores adicionais para a localização de elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="d38a4-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-374">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-374">Return value</span></span>

<span data-ttu-id="d38a4-375">Uma matriz ou objeto com elementos comuns hello.</span><span class="sxs-lookup"><span data-stu-id="d38a4-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-376">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-376">Example</span></span>

<span data-ttu-id="d38a4-377">saudação de exemplo a seguir mostra como a interseção de toouse com matrizes e objetos:</span><span class="sxs-lookup"><span data-stu-id="d38a4-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="d38a4-378">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-379">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-379">Name</span></span> | <span data-ttu-id="d38a4-380">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-380">Type</span></span> | <span data-ttu-id="d38a4-381">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-382">objectOutput</span></span> | <span data-ttu-id="d38a4-383">Objeto</span><span class="sxs-lookup"><span data-stu-id="d38a4-383">Object</span></span> | <span data-ttu-id="d38a4-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="d38a4-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="d38a4-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-385">arrayOutput</span></span> | <span data-ttu-id="d38a4-386">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-386">Array</span></span> | <span data-ttu-id="d38a4-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="d38a4-388">json</span><span class="sxs-lookup"><span data-stu-id="d38a4-388">json</span></span>
`json(arg1)`

<span data-ttu-id="d38a4-389">Retorna um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="d38a4-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-390">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-390">Parameters</span></span>

| <span data-ttu-id="d38a4-391">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-391">Parameter</span></span> | <span data-ttu-id="d38a4-392">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-392">Required</span></span> | <span data-ttu-id="d38a4-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-393">Type</span></span> | <span data-ttu-id="d38a4-394">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-395">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-395">arg1</span></span> |<span data-ttu-id="d38a4-396">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-396">Yes</span></span> |<span data-ttu-id="d38a4-397">string</span><span class="sxs-lookup"><span data-stu-id="d38a4-397">string</span></span> |<span data-ttu-id="d38a4-398">Olá valor tooconvert tooJSON.</span><span class="sxs-lookup"><span data-stu-id="d38a4-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="d38a4-399">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-399">Return value</span></span>

<span data-ttu-id="d38a4-400">objeto JSON de saudação do hello especificado a cadeia de caracteres ou um objeto vazio quando **nulo** for especificado.</span><span class="sxs-lookup"><span data-stu-id="d38a4-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-401">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-401">Example</span></span>

<span data-ttu-id="d38a4-402">saudação de exemplo a seguir mostra como a interseção de toouse com matrizes e objetos:</span><span class="sxs-lookup"><span data-stu-id="d38a4-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="d38a4-403">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-404">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-404">Name</span></span> | <span data-ttu-id="d38a4-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-405">Type</span></span> | <span data-ttu-id="d38a4-406">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-407">jsonOutput</span></span> | <span data-ttu-id="d38a4-408">Objeto</span><span class="sxs-lookup"><span data-stu-id="d38a4-408">Object</span></span> | <span data-ttu-id="d38a4-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="d38a4-409">{"a": "b"}</span></span> |
| <span data-ttu-id="d38a4-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-410">nullOutput</span></span> | <span data-ttu-id="d38a4-411">Booliano</span><span class="sxs-lookup"><span data-stu-id="d38a4-411">Boolean</span></span> | <span data-ttu-id="d38a4-412">True</span><span class="sxs-lookup"><span data-stu-id="d38a4-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="d38a4-413">last</span><span class="sxs-lookup"><span data-stu-id="d38a4-413">last</span></span>
`last (arg1)`

<span data-ttu-id="d38a4-414">Retorna Olá último elemento da matriz de saudação ou o último caractere da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-415">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-415">Parameters</span></span>

| <span data-ttu-id="d38a4-416">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-416">Parameter</span></span> | <span data-ttu-id="d38a4-417">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-417">Required</span></span> | <span data-ttu-id="d38a4-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-418">Type</span></span> | <span data-ttu-id="d38a4-419">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-420">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-420">arg1</span></span> |<span data-ttu-id="d38a4-421">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-421">Yes</span></span> |<span data-ttu-id="d38a4-422">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-422">array or string</span></span> |<span data-ttu-id="d38a4-423">Olá valor tooretrieve Olá último elemento ou um caractere.</span><span class="sxs-lookup"><span data-stu-id="d38a4-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-424">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-424">Return value</span></span>

<span data-ttu-id="d38a4-425">tipo de saudação (string, int, matriz ou objeto) do hello último elemento em uma matriz, ou o último caractere saudação de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-426">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-426">Example</span></span>

<span data-ttu-id="d38a4-427">Olá exemplo a seguir mostra como toouse Olá última função com uma matriz e a cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="d38a4-428">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-429">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-429">Name</span></span> | <span data-ttu-id="d38a4-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-430">Type</span></span> | <span data-ttu-id="d38a4-431">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-432">arrayOutput</span></span> | <span data-ttu-id="d38a4-433">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-433">String</span></span> | <span data-ttu-id="d38a4-434">três</span><span class="sxs-lookup"><span data-stu-id="d38a4-434">three</span></span> |
| <span data-ttu-id="d38a4-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-435">stringOutput</span></span> | <span data-ttu-id="d38a4-436">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-436">String</span></span> | <span data-ttu-id="d38a4-437">e</span><span class="sxs-lookup"><span data-stu-id="d38a4-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="d38a4-438">length</span><span class="sxs-lookup"><span data-stu-id="d38a4-438">length</span></span>
`length(arg1)`

<span data-ttu-id="d38a4-439">Retorna o número de saudação de elementos em uma matriz ou uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-440">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-440">Parameters</span></span>

| <span data-ttu-id="d38a4-441">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-441">Parameter</span></span> | <span data-ttu-id="d38a4-442">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-442">Required</span></span> | <span data-ttu-id="d38a4-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-443">Type</span></span> | <span data-ttu-id="d38a4-444">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-445">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-445">arg1</span></span> |<span data-ttu-id="d38a4-446">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-446">Yes</span></span> |<span data-ttu-id="d38a4-447">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-447">array or string</span></span> |<span data-ttu-id="d38a4-448">Olá toouse de matriz para obter o número de saudação de elementos ou Olá toouse de cadeia de caracteres para obter o número de saudação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-449">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-449">Return value</span></span>

<span data-ttu-id="d38a4-450">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="d38a4-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="d38a4-451">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-451">Example</span></span>

<span data-ttu-id="d38a4-452">Olá mostrado no exemplo a seguir como comprimento toouse com uma matriz e a cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="d38a4-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="d38a4-453">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-454">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-454">Name</span></span> | <span data-ttu-id="d38a4-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-455">Type</span></span> | <span data-ttu-id="d38a4-456">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="d38a4-457">arrayLength</span></span> | <span data-ttu-id="d38a4-458">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-458">Int</span></span> | <span data-ttu-id="d38a4-459">3</span><span class="sxs-lookup"><span data-stu-id="d38a4-459">3</span></span> |
| <span data-ttu-id="d38a4-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="d38a4-460">stringLength</span></span> | <span data-ttu-id="d38a4-461">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-461">Int</span></span> | <span data-ttu-id="d38a4-462">13</span><span class="sxs-lookup"><span data-stu-id="d38a4-462">13</span></span> |

<span data-ttu-id="d38a4-463">Você pode usar essa função com um número de saudação do toospecify de matriz de iterações ao criar recursos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="d38a4-464">Em Olá exemplo a seguir, Olá parâmetro **siteNames** faz referência a matriz de tooan de toouse nomes durante a criação de sites da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="d38a4-465">Para saber mais sobre como usar essa função com uma matriz, confira [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d38a4-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="d38a4-466">Min</span><span class="sxs-lookup"><span data-stu-id="d38a4-466">min</span></span>
`min(arg1)`

<span data-ttu-id="d38a4-467">Retorna Olá valor mínimo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.</span><span class="sxs-lookup"><span data-stu-id="d38a4-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-468">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-468">Parameters</span></span>

| <span data-ttu-id="d38a4-469">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-469">Parameter</span></span> | <span data-ttu-id="d38a4-470">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-470">Required</span></span> | <span data-ttu-id="d38a4-471">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-471">Type</span></span> | <span data-ttu-id="d38a4-472">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-473">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-473">arg1</span></span> |<span data-ttu-id="d38a4-474">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-474">Yes</span></span> |<span data-ttu-id="d38a4-475">matriz de inteiros ou lista de inteiros separados por vírgulas</span><span class="sxs-lookup"><span data-stu-id="d38a4-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="d38a4-476">Olá coleção tooget Olá valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="d38a4-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-477">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-477">Return value</span></span>

<span data-ttu-id="d38a4-478">Um inteiro que representa o valor mínimo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-479">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-479">Example</span></span>

<span data-ttu-id="d38a4-480">Olá mostrado no exemplo a seguir como min toouse com uma matriz e uma lista de números inteiros:</span><span class="sxs-lookup"><span data-stu-id="d38a4-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="d38a4-481">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-482">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-482">Name</span></span> | <span data-ttu-id="d38a4-483">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-483">Type</span></span> | <span data-ttu-id="d38a4-484">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-485">arrayOutput</span></span> | <span data-ttu-id="d38a4-486">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-486">Int</span></span> | <span data-ttu-id="d38a4-487">0</span><span class="sxs-lookup"><span data-stu-id="d38a4-487">0</span></span> |
| <span data-ttu-id="d38a4-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-488">intOutput</span></span> | <span data-ttu-id="d38a4-489">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-489">Int</span></span> | <span data-ttu-id="d38a4-490">0</span><span class="sxs-lookup"><span data-stu-id="d38a4-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="d38a4-491">max</span><span class="sxs-lookup"><span data-stu-id="d38a4-491">max</span></span>
`max(arg1)`

<span data-ttu-id="d38a4-492">Retorna Olá valor máximo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.</span><span class="sxs-lookup"><span data-stu-id="d38a4-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-493">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-493">Parameters</span></span>

| <span data-ttu-id="d38a4-494">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-494">Parameter</span></span> | <span data-ttu-id="d38a4-495">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-495">Required</span></span> | <span data-ttu-id="d38a4-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-496">Type</span></span> | <span data-ttu-id="d38a4-497">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-498">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-498">arg1</span></span> |<span data-ttu-id="d38a4-499">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-499">Yes</span></span> |<span data-ttu-id="d38a4-500">matriz de inteiros ou lista de inteiros separados por vírgulas</span><span class="sxs-lookup"><span data-stu-id="d38a4-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="d38a4-501">Olá coleção tooget Olá valor máximo.</span><span class="sxs-lookup"><span data-stu-id="d38a4-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-502">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-502">Return value</span></span>

<span data-ttu-id="d38a4-503">Um inteiro que representa o valor máximo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-504">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-504">Example</span></span>

<span data-ttu-id="d38a4-505">Olá mostrado no exemplo a seguir como toouse max com uma matriz e uma lista de números inteiros:</span><span class="sxs-lookup"><span data-stu-id="d38a4-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="d38a4-506">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-507">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-507">Name</span></span> | <span data-ttu-id="d38a4-508">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-508">Type</span></span> | <span data-ttu-id="d38a4-509">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-510">arrayOutput</span></span> | <span data-ttu-id="d38a4-511">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-511">Int</span></span> | <span data-ttu-id="d38a4-512">5</span><span class="sxs-lookup"><span data-stu-id="d38a4-512">5</span></span> |
| <span data-ttu-id="d38a4-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-513">intOutput</span></span> | <span data-ttu-id="d38a4-514">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-514">Int</span></span> | <span data-ttu-id="d38a4-515">5</span><span class="sxs-lookup"><span data-stu-id="d38a4-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="d38a4-516">range</span><span class="sxs-lookup"><span data-stu-id="d38a4-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="d38a4-517">Cria uma matriz de inteiros a partir de um inteiro inicial e contendo um número de itens.</span><span class="sxs-lookup"><span data-stu-id="d38a4-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-518">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-518">Parameters</span></span>

| <span data-ttu-id="d38a4-519">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-519">Parameter</span></span> | <span data-ttu-id="d38a4-520">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-520">Required</span></span> | <span data-ttu-id="d38a4-521">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-521">Type</span></span> | <span data-ttu-id="d38a4-522">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="d38a4-523">startingInteger</span></span> |<span data-ttu-id="d38a4-524">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-524">Yes</span></span> |<span data-ttu-id="d38a4-525">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-525">int</span></span> |<span data-ttu-id="d38a4-526">primeiro inteiro na matriz Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="d38a4-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="d38a4-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="d38a4-527">numberofElements</span></span> |<span data-ttu-id="d38a4-528">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-528">Yes</span></span> |<span data-ttu-id="d38a4-529">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-529">int</span></span> |<span data-ttu-id="d38a4-530">número de saudação de inteiros na matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-531">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-531">Return value</span></span>

<span data-ttu-id="d38a4-532">Uma matriz de inteiros.</span><span class="sxs-lookup"><span data-stu-id="d38a4-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-533">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-533">Example</span></span>

<span data-ttu-id="d38a4-534">saudação de exemplo a seguir mostra como toouse Olá função range:</span><span class="sxs-lookup"><span data-stu-id="d38a4-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="d38a4-535">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-536">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-536">Name</span></span> | <span data-ttu-id="d38a4-537">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-537">Type</span></span> | <span data-ttu-id="d38a4-538">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-539">rangeOutput</span></span> | <span data-ttu-id="d38a4-540">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-540">Array</span></span> | <span data-ttu-id="d38a4-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="d38a4-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="d38a4-542">skip</span><span class="sxs-lookup"><span data-stu-id="d38a4-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="d38a4-543">Retorna uma matriz com todos os elementos de saudação depois Olá número especificado na matriz hello, ou retorna uma cadeia de caracteres com todos os caracteres de saudação depois Olá número especificado na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-544">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-544">Parameters</span></span>

| <span data-ttu-id="d38a4-545">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-545">Parameter</span></span> | <span data-ttu-id="d38a4-546">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-546">Required</span></span> | <span data-ttu-id="d38a4-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-547">Type</span></span> | <span data-ttu-id="d38a4-548">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="d38a4-549">originalValue</span></span> |<span data-ttu-id="d38a4-550">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-550">Yes</span></span> |<span data-ttu-id="d38a4-551">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-551">array or string</span></span> |<span data-ttu-id="d38a4-552">Olá toouse matriz ou cadeia de caracteres para ignorar.</span><span class="sxs-lookup"><span data-stu-id="d38a4-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="d38a4-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="d38a4-553">numberToSkip</span></span> |<span data-ttu-id="d38a4-554">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-554">Yes</span></span> |<span data-ttu-id="d38a4-555">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-555">int</span></span> |<span data-ttu-id="d38a4-556">número de saudação de elementos ou caracteres tooskip.</span><span class="sxs-lookup"><span data-stu-id="d38a4-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="d38a4-557">Se esse valor for 0 ou menos, todos os elementos de hello ou caracteres no valor de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="d38a4-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="d38a4-558">Se for maior do que o tamanho de cadeia de caracteres ou matriz Olá Olá, uma matriz vazia ou cadeia de caracteres é retornada.</span><span class="sxs-lookup"><span data-stu-id="d38a4-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-559">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-559">Return value</span></span>

<span data-ttu-id="d38a4-560">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-561">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-561">Example</span></span>

<span data-ttu-id="d38a4-562">Olá seguindo o exemplo ignora Olá número especificado de elementos na matriz de saudação e Olá número especificado de caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="d38a4-563">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-564">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-564">Name</span></span> | <span data-ttu-id="d38a4-565">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-565">Type</span></span> | <span data-ttu-id="d38a4-566">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-567">arrayOutput</span></span> | <span data-ttu-id="d38a4-568">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-568">Array</span></span> | <span data-ttu-id="d38a4-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-569">["three"]</span></span> |
| <span data-ttu-id="d38a4-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-570">stringOutput</span></span> | <span data-ttu-id="d38a4-571">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-571">String</span></span> | <span data-ttu-id="d38a4-572">two three</span><span class="sxs-lookup"><span data-stu-id="d38a4-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="d38a4-573">take</span><span class="sxs-lookup"><span data-stu-id="d38a4-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="d38a4-574">Retorna uma matriz com hello número especificado de elementos de Olá início da matriz hello, ou uma cadeia de caracteres com hello número especificado de caracteres do início de saudação de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-575">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-575">Parameters</span></span>

| <span data-ttu-id="d38a4-576">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-576">Parameter</span></span> | <span data-ttu-id="d38a4-577">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-577">Required</span></span> | <span data-ttu-id="d38a4-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-578">Type</span></span> | <span data-ttu-id="d38a4-579">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="d38a4-580">originalValue</span></span> |<span data-ttu-id="d38a4-581">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-581">Yes</span></span> |<span data-ttu-id="d38a4-582">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-582">array or string</span></span> |<span data-ttu-id="d38a4-583">Olá cadeia ou matriz de elementos de saudação tootake do.</span><span class="sxs-lookup"><span data-stu-id="d38a4-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="d38a4-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="d38a4-584">numberToTake</span></span> |<span data-ttu-id="d38a4-585">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-585">Yes</span></span> |<span data-ttu-id="d38a4-586">int</span><span class="sxs-lookup"><span data-stu-id="d38a4-586">int</span></span> |<span data-ttu-id="d38a4-587">número de saudação de elementos ou caracteres tootake.</span><span class="sxs-lookup"><span data-stu-id="d38a4-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="d38a4-588">Se esse valor for 0 ou menos, uma matriz ou cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="d38a4-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="d38a4-589">Se for maior do que o comprimento de saudação do hello considerando a cadeia de caracteres ou matriz, todos os elementos de saudação na cadeia de caracteres ou matriz hello serão retornados.</span><span class="sxs-lookup"><span data-stu-id="d38a4-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-590">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-590">Return value</span></span>

<span data-ttu-id="d38a4-591">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-592">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-592">Example</span></span>

<span data-ttu-id="d38a4-593">Olá seguindo o exemplo usa Olá número especificado de elementos da matriz hello e caracteres de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d38a4-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="d38a4-594">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-595">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-595">Name</span></span> | <span data-ttu-id="d38a4-596">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-596">Type</span></span> | <span data-ttu-id="d38a4-597">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-598">arrayOutput</span></span> | <span data-ttu-id="d38a4-599">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-599">Array</span></span> | <span data-ttu-id="d38a4-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-600">["one", "two"]</span></span> |
| <span data-ttu-id="d38a4-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-601">stringOutput</span></span> | <span data-ttu-id="d38a4-602">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d38a4-602">String</span></span> | <span data-ttu-id="d38a4-603">em</span><span class="sxs-lookup"><span data-stu-id="d38a4-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="d38a4-604">union</span><span class="sxs-lookup"><span data-stu-id="d38a4-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="d38a4-605">Retorna uma matriz ou objeto com todos os elementos de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38a4-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="d38a4-606">Valores duplicados ou chaves só são incluídos uma vez.</span><span class="sxs-lookup"><span data-stu-id="d38a4-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="d38a4-607">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d38a4-607">Parameters</span></span>

| <span data-ttu-id="d38a4-608">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d38a4-608">Parameter</span></span> | <span data-ttu-id="d38a4-609">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d38a4-609">Required</span></span> | <span data-ttu-id="d38a4-610">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-610">Type</span></span> | <span data-ttu-id="d38a4-611">Descrição</span><span class="sxs-lookup"><span data-stu-id="d38a4-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d38a4-612">arg1</span><span class="sxs-lookup"><span data-stu-id="d38a4-612">arg1</span></span> |<span data-ttu-id="d38a4-613">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-613">Yes</span></span> |<span data-ttu-id="d38a4-614">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-614">array or object</span></span> |<span data-ttu-id="d38a4-615">Olá toouse valor primeiro para ingressar em elementos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="d38a4-616">arg2</span><span class="sxs-lookup"><span data-stu-id="d38a4-616">arg2</span></span> |<span data-ttu-id="d38a4-617">Sim</span><span class="sxs-lookup"><span data-stu-id="d38a4-617">Yes</span></span> |<span data-ttu-id="d38a4-618">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-618">array or object</span></span> |<span data-ttu-id="d38a4-619">Olá toouse valor segundo para ingressar em elementos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="d38a4-620">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="d38a4-620">additional arguments</span></span> |<span data-ttu-id="d38a4-621">Não</span><span class="sxs-lookup"><span data-stu-id="d38a4-621">No</span></span> |<span data-ttu-id="d38a4-622">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-622">array or object</span></span> |<span data-ttu-id="d38a4-623">Toouse valores adicionais para ingressar em elementos.</span><span class="sxs-lookup"><span data-stu-id="d38a4-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d38a4-624">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="d38a4-624">Return value</span></span>

<span data-ttu-id="d38a4-625">Uma matriz ou objeto.</span><span class="sxs-lookup"><span data-stu-id="d38a4-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="d38a4-626">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d38a4-626">Example</span></span>

<span data-ttu-id="d38a4-627">saudação de exemplo a seguir mostra como união toouse com matrizes e objetos:</span><span class="sxs-lookup"><span data-stu-id="d38a4-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="d38a4-628">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d38a4-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d38a4-629">Nome</span><span class="sxs-lookup"><span data-stu-id="d38a4-629">Name</span></span> | <span data-ttu-id="d38a4-630">Tipo</span><span class="sxs-lookup"><span data-stu-id="d38a4-630">Type</span></span> | <span data-ttu-id="d38a4-631">Valor</span><span class="sxs-lookup"><span data-stu-id="d38a4-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d38a4-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-632">objectOutput</span></span> | <span data-ttu-id="d38a4-633">Objeto</span><span class="sxs-lookup"><span data-stu-id="d38a4-633">Object</span></span> | <span data-ttu-id="d38a4-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="d38a4-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="d38a4-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d38a4-635">arrayOutput</span></span> | <span data-ttu-id="d38a4-636">Matriz</span><span class="sxs-lookup"><span data-stu-id="d38a4-636">Array</span></span> | <span data-ttu-id="d38a4-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="d38a4-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d38a4-638">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d38a4-638">Next steps</span></span>
* <span data-ttu-id="d38a4-639">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d38a4-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d38a4-640">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d38a4-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="d38a4-641">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d38a4-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="d38a4-642">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d38a4-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

