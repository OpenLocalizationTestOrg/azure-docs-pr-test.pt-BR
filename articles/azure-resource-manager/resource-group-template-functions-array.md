---
title: "Funções de modelo do Azure Resource Manager – matrizes e objetos | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Azure Resource Manager para trabalhar com matrizes e objetos."
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
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="67fc2-103">Funções de matriz e objeto para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67fc2-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="67fc2-104">O Resource Manager fornece diversas funções para trabalhar com matrizes e objetos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="67fc2-105">array</span><span class="sxs-lookup"><span data-stu-id="67fc2-105">array</span></span>](#array)
* [<span data-ttu-id="67fc2-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="67fc2-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="67fc2-107">concat</span><span class="sxs-lookup"><span data-stu-id="67fc2-107">concat</span></span>](#concat)
* [<span data-ttu-id="67fc2-108">contains</span><span class="sxs-lookup"><span data-stu-id="67fc2-108">contains</span></span>](#contains)
* [<span data-ttu-id="67fc2-109">createArray</span><span class="sxs-lookup"><span data-stu-id="67fc2-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="67fc2-110">empty</span><span class="sxs-lookup"><span data-stu-id="67fc2-110">empty</span></span>](#empty)
* [<span data-ttu-id="67fc2-111">first</span><span class="sxs-lookup"><span data-stu-id="67fc2-111">first</span></span>](#first)
* [<span data-ttu-id="67fc2-112">intersection</span><span class="sxs-lookup"><span data-stu-id="67fc2-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="67fc2-113">json</span><span class="sxs-lookup"><span data-stu-id="67fc2-113">json</span></span>](#json)
* [<span data-ttu-id="67fc2-114">last</span><span class="sxs-lookup"><span data-stu-id="67fc2-114">last</span></span>](#last)
* [<span data-ttu-id="67fc2-115">length</span><span class="sxs-lookup"><span data-stu-id="67fc2-115">length</span></span>](#length)
* [<span data-ttu-id="67fc2-116">min</span><span class="sxs-lookup"><span data-stu-id="67fc2-116">min</span></span>](#min)
* [<span data-ttu-id="67fc2-117">max</span><span class="sxs-lookup"><span data-stu-id="67fc2-117">max</span></span>](#max)
* [<span data-ttu-id="67fc2-118">range</span><span class="sxs-lookup"><span data-stu-id="67fc2-118">range</span></span>](#range)
* [<span data-ttu-id="67fc2-119">skip</span><span class="sxs-lookup"><span data-stu-id="67fc2-119">skip</span></span>](#skip)
* [<span data-ttu-id="67fc2-120">take</span><span class="sxs-lookup"><span data-stu-id="67fc2-120">take</span></span>](#take)
* [<span data-ttu-id="67fc2-121">union</span><span class="sxs-lookup"><span data-stu-id="67fc2-121">union</span></span>](#union)

<span data-ttu-id="67fc2-122">Para obter uma matriz de valores de cadeia de caracteres delimitada por um valor, confira [split](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="67fc2-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="67fc2-123">matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="67fc2-124">Converte o valor em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-125">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-125">Parameters</span></span>

| <span data-ttu-id="67fc2-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-126">Parameter</span></span> | <span data-ttu-id="67fc2-127">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-127">Required</span></span> | <span data-ttu-id="67fc2-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-128">Type</span></span> | <span data-ttu-id="67fc2-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="67fc2-130">convertToArray</span></span> |<span data-ttu-id="67fc2-131">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-131">Yes</span></span> |<span data-ttu-id="67fc2-132">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="67fc2-132">int, string, array, or object</span></span> |<span data-ttu-id="67fc2-133">O valor a ser convertido em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-134">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-134">Return value</span></span>

<span data-ttu-id="67fc2-135">Uma matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-136">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-136">Example</span></span>

<span data-ttu-id="67fc2-137">O seguinte exemplo mostra como usar a função array com tipos diferentes.</span><span class="sxs-lookup"><span data-stu-id="67fc2-137">The following example shows how to use the array function with different types.</span></span>

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

<span data-ttu-id="67fc2-138">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-139">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-139">Name</span></span> | <span data-ttu-id="67fc2-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-140">Type</span></span> | <span data-ttu-id="67fc2-141">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-142">intOutput</span></span> | <span data-ttu-id="67fc2-143">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-143">Array</span></span> | <span data-ttu-id="67fc2-144">[1]</span><span class="sxs-lookup"><span data-stu-id="67fc2-144">[1]</span></span> |
| <span data-ttu-id="67fc2-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-145">stringOutput</span></span> | <span data-ttu-id="67fc2-146">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-146">Array</span></span> | <span data-ttu-id="67fc2-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-147">["a"]</span></span> |
| <span data-ttu-id="67fc2-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-148">objectOutput</span></span> | <span data-ttu-id="67fc2-149">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-149">Array</span></span> | <span data-ttu-id="67fc2-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="67fc2-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="67fc2-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="67fc2-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="67fc2-152">Retorna o primeiro valor não nulo dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="67fc2-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="67fc2-153">Cadeias de caracteres vazias, matrizes vazias e objetos vazios não são nulos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-154">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-154">Parameters</span></span>

| <span data-ttu-id="67fc2-155">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-155">Parameter</span></span> | <span data-ttu-id="67fc2-156">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-156">Required</span></span> | <span data-ttu-id="67fc2-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-157">Type</span></span> | <span data-ttu-id="67fc2-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-159">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-159">arg1</span></span> |<span data-ttu-id="67fc2-160">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-160">Yes</span></span> |<span data-ttu-id="67fc2-161">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="67fc2-161">int, string, array, or object</span></span> |<span data-ttu-id="67fc2-162">O primeiro valor para testar se é nulo.</span><span class="sxs-lookup"><span data-stu-id="67fc2-162">The first value to test for null.</span></span> |
| <span data-ttu-id="67fc2-163">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="67fc2-163">additional args</span></span> |<span data-ttu-id="67fc2-164">Não</span><span class="sxs-lookup"><span data-stu-id="67fc2-164">No</span></span> |<span data-ttu-id="67fc2-165">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="67fc2-165">int, string, array, or object</span></span> |<span data-ttu-id="67fc2-166">Valores adicionais para testar se são nulos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-167">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-167">Return value</span></span>

<span data-ttu-id="67fc2-168">O valor dos primeiros parâmetros não nulos, que pode ser uma cadeia de caracteres, inteiro, matriz ou objeto.</span><span class="sxs-lookup"><span data-stu-id="67fc2-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="67fc2-169">Null se todos os parâmetros forem nulos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="67fc2-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-170">Example</span></span>

<span data-ttu-id="67fc2-171">O exemplo a seguir mostra a saída de diferentes usos de coalesce.</span><span class="sxs-lookup"><span data-stu-id="67fc2-171">The following example shows the output from different uses of coalesce.</span></span>

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

<span data-ttu-id="67fc2-172">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-173">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-173">Name</span></span> | <span data-ttu-id="67fc2-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-174">Type</span></span> | <span data-ttu-id="67fc2-175">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-176">stringOutput</span></span> | <span data-ttu-id="67fc2-177">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-177">String</span></span> | <span data-ttu-id="67fc2-178">padrão</span><span class="sxs-lookup"><span data-stu-id="67fc2-178">default</span></span> |
| <span data-ttu-id="67fc2-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-179">intOutput</span></span> | <span data-ttu-id="67fc2-180">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-180">Int</span></span> | <span data-ttu-id="67fc2-181">1</span><span class="sxs-lookup"><span data-stu-id="67fc2-181">1</span></span> |
| <span data-ttu-id="67fc2-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-182">objectOutput</span></span> | <span data-ttu-id="67fc2-183">Objeto</span><span class="sxs-lookup"><span data-stu-id="67fc2-183">Object</span></span> | <span data-ttu-id="67fc2-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="67fc2-184">{"first": "default"}</span></span> |
| <span data-ttu-id="67fc2-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-185">arrayOutput</span></span> | <span data-ttu-id="67fc2-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-186">Array</span></span> | <span data-ttu-id="67fc2-187">[1]</span><span class="sxs-lookup"><span data-stu-id="67fc2-187">[1]</span></span> |
| <span data-ttu-id="67fc2-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-188">emptyOutput</span></span> | <span data-ttu-id="67fc2-189">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-189">Bool</span></span> | <span data-ttu-id="67fc2-190">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="67fc2-191">concat</span><span class="sxs-lookup"><span data-stu-id="67fc2-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="67fc2-192">Combina várias matrizes e retorna a matriz concatenada, ou combina vários valores de cadeia de caracteres e retorna a matriz concatenada.</span><span class="sxs-lookup"><span data-stu-id="67fc2-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="67fc2-193">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-193">Parameters</span></span>

| <span data-ttu-id="67fc2-194">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-194">Parameter</span></span> | <span data-ttu-id="67fc2-195">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-195">Required</span></span> | <span data-ttu-id="67fc2-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-196">Type</span></span> | <span data-ttu-id="67fc2-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-198">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-198">arg1</span></span> |<span data-ttu-id="67fc2-199">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-199">Yes</span></span> |<span data-ttu-id="67fc2-200">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-200">array or string</span></span> |<span data-ttu-id="67fc2-201">A primeira matriz ou cadeia de caracteres para concatenação.</span><span class="sxs-lookup"><span data-stu-id="67fc2-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="67fc2-202">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="67fc2-202">additional arguments</span></span> |<span data-ttu-id="67fc2-203">Não</span><span class="sxs-lookup"><span data-stu-id="67fc2-203">No</span></span> |<span data-ttu-id="67fc2-204">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-204">array or string</span></span> |<span data-ttu-id="67fc2-205">Matrizes ou cadeias de caractere adicionais em ordem sequencial para concatenação.</span><span class="sxs-lookup"><span data-stu-id="67fc2-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="67fc2-206">Essa função pode conter qualquer número de argumentos e pode aceitar cadeias de caracteres ou matrizes como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="67fc2-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="67fc2-207">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-207">Return value</span></span>
<span data-ttu-id="67fc2-208">Uma cadeia de caracteres ou matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="67fc2-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-209">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-209">Example</span></span>

<span data-ttu-id="67fc2-210">O próximo exemplo mostra como combinar duas matrizes.</span><span class="sxs-lookup"><span data-stu-id="67fc2-210">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="67fc2-211">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-212">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-212">Name</span></span> | <span data-ttu-id="67fc2-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-213">Type</span></span> | <span data-ttu-id="67fc2-214">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-215">retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-215">return</span></span> | <span data-ttu-id="67fc2-216">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-216">Array</span></span> | <span data-ttu-id="67fc2-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="67fc2-218">O exemplo a seguir mostra como combinar dois valores de cadeia de caracteres e retornar uma cadeia de caracteres concatenada.</span><span class="sxs-lookup"><span data-stu-id="67fc2-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="67fc2-219">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-220">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-220">Name</span></span> | <span data-ttu-id="67fc2-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-221">Type</span></span> | <span data-ttu-id="67fc2-222">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-223">concatOutput</span></span> | <span data-ttu-id="67fc2-224">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-224">String</span></span> | <span data-ttu-id="67fc2-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="67fc2-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="67fc2-226">contains</span><span class="sxs-lookup"><span data-stu-id="67fc2-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="67fc2-227">Verifica se uma matriz contém um valor, um objeto contém uma chave ou uma cadeia de caracteres contém uma subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-228">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-228">Parameters</span></span>

| <span data-ttu-id="67fc2-229">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-229">Parameter</span></span> | <span data-ttu-id="67fc2-230">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-230">Required</span></span> | <span data-ttu-id="67fc2-231">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-231">Type</span></span> | <span data-ttu-id="67fc2-232">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-233">contêiner</span><span class="sxs-lookup"><span data-stu-id="67fc2-233">container</span></span> |<span data-ttu-id="67fc2-234">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-234">Yes</span></span> |<span data-ttu-id="67fc2-235">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-235">array, object, or string</span></span> |<span data-ttu-id="67fc2-236">O valor que contém o valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="67fc2-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="67fc2-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="67fc2-237">itemToFind</span></span> |<span data-ttu-id="67fc2-238">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-238">Yes</span></span> |<span data-ttu-id="67fc2-239">string ou int</span><span class="sxs-lookup"><span data-stu-id="67fc2-239">string or int</span></span> |<span data-ttu-id="67fc2-240">O valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="67fc2-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-241">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-241">Return value</span></span>

<span data-ttu-id="67fc2-242">**True** se o item for encontrado; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="67fc2-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-243">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-243">Example</span></span>

<span data-ttu-id="67fc2-244">O seguinte exemplo mostra como usar contains com tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="67fc2-244">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="67fc2-245">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-246">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-246">Name</span></span> | <span data-ttu-id="67fc2-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-247">Type</span></span> | <span data-ttu-id="67fc2-248">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="67fc2-249">stringTrue</span></span> | <span data-ttu-id="67fc2-250">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-250">Bool</span></span> | <span data-ttu-id="67fc2-251">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-251">True</span></span> |
| <span data-ttu-id="67fc2-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="67fc2-252">stringFalse</span></span> | <span data-ttu-id="67fc2-253">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-253">Bool</span></span> | <span data-ttu-id="67fc2-254">Falso</span><span class="sxs-lookup"><span data-stu-id="67fc2-254">False</span></span> |
| <span data-ttu-id="67fc2-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="67fc2-255">objectTrue</span></span> | <span data-ttu-id="67fc2-256">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-256">Bool</span></span> | <span data-ttu-id="67fc2-257">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-257">True</span></span> |
| <span data-ttu-id="67fc2-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="67fc2-258">objectFalse</span></span> | <span data-ttu-id="67fc2-259">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-259">Bool</span></span> | <span data-ttu-id="67fc2-260">Falso</span><span class="sxs-lookup"><span data-stu-id="67fc2-260">False</span></span> |
| <span data-ttu-id="67fc2-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="67fc2-261">arrayTrue</span></span> | <span data-ttu-id="67fc2-262">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-262">Bool</span></span> | <span data-ttu-id="67fc2-263">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-263">True</span></span> |
| <span data-ttu-id="67fc2-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="67fc2-264">arrayFalse</span></span> | <span data-ttu-id="67fc2-265">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-265">Bool</span></span> | <span data-ttu-id="67fc2-266">Falso</span><span class="sxs-lookup"><span data-stu-id="67fc2-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="67fc2-267">createarray</span><span class="sxs-lookup"><span data-stu-id="67fc2-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="67fc2-268">Cria uma matriz de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="67fc2-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-269">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-269">Parameters</span></span>

| <span data-ttu-id="67fc2-270">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-270">Parameter</span></span> | <span data-ttu-id="67fc2-271">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-271">Required</span></span> | <span data-ttu-id="67fc2-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-272">Type</span></span> | <span data-ttu-id="67fc2-273">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-274">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-274">arg1</span></span> |<span data-ttu-id="67fc2-275">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-275">Yes</span></span> |<span data-ttu-id="67fc2-276">String, Inteiro, Matriz ou Objeto</span><span class="sxs-lookup"><span data-stu-id="67fc2-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="67fc2-277">O primeiro valor na matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-277">The first value in the array.</span></span> |
| <span data-ttu-id="67fc2-278">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="67fc2-278">additional arguments</span></span> |<span data-ttu-id="67fc2-279">Não</span><span class="sxs-lookup"><span data-stu-id="67fc2-279">No</span></span> |<span data-ttu-id="67fc2-280">String, Inteiro, Matriz ou Objeto</span><span class="sxs-lookup"><span data-stu-id="67fc2-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="67fc2-281">Valores adicionais na matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-282">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-282">Return value</span></span>

<span data-ttu-id="67fc2-283">Uma matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-284">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-284">Example</span></span>

<span data-ttu-id="67fc2-285">O seguinte exemplo mostra como usar createArray com tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="67fc2-285">The following example shows how to use createArray with different types:</span></span>

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

<span data-ttu-id="67fc2-286">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-287">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-287">Name</span></span> | <span data-ttu-id="67fc2-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-288">Type</span></span> | <span data-ttu-id="67fc2-289">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="67fc2-290">stringArray</span></span> | <span data-ttu-id="67fc2-291">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-291">Array</span></span> | <span data-ttu-id="67fc2-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="67fc2-293">intArray</span><span class="sxs-lookup"><span data-stu-id="67fc2-293">intArray</span></span> | <span data-ttu-id="67fc2-294">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-294">Array</span></span> | <span data-ttu-id="67fc2-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="67fc2-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="67fc2-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="67fc2-296">objectArray</span></span> | <span data-ttu-id="67fc2-297">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-297">Array</span></span> | <span data-ttu-id="67fc2-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="67fc2-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="67fc2-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="67fc2-299">arrayArray</span></span> | <span data-ttu-id="67fc2-300">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-300">Array</span></span> | <span data-ttu-id="67fc2-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="67fc2-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="67fc2-302">empty</span><span class="sxs-lookup"><span data-stu-id="67fc2-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="67fc2-303">Determina se uma matriz, objeto ou uma cadeia de caracteres está vazio.</span><span class="sxs-lookup"><span data-stu-id="67fc2-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-304">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-304">Parameters</span></span>

| <span data-ttu-id="67fc2-305">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-305">Parameter</span></span> | <span data-ttu-id="67fc2-306">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-306">Required</span></span> | <span data-ttu-id="67fc2-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-307">Type</span></span> | <span data-ttu-id="67fc2-308">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="67fc2-309">itemToTest</span></span> |<span data-ttu-id="67fc2-310">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-310">Yes</span></span> |<span data-ttu-id="67fc2-311">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-311">array, object, or string</span></span> |<span data-ttu-id="67fc2-312">O valor a ser verificado, caso esteja vazio.</span><span class="sxs-lookup"><span data-stu-id="67fc2-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-313">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-313">Return value</span></span>

<span data-ttu-id="67fc2-314">Retorna **True** se o valor é vazio; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="67fc2-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-315">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-315">Example</span></span>

<span data-ttu-id="67fc2-316">O exemplo a seguir verifica se uma matriz, um objeto e uma cadeia de caracteres estão vazios.</span><span class="sxs-lookup"><span data-stu-id="67fc2-316">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="67fc2-317">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-318">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-318">Name</span></span> | <span data-ttu-id="67fc2-319">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-319">Type</span></span> | <span data-ttu-id="67fc2-320">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="67fc2-321">arrayEmpty</span></span> | <span data-ttu-id="67fc2-322">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-322">Bool</span></span> | <span data-ttu-id="67fc2-323">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-323">True</span></span> |
| <span data-ttu-id="67fc2-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="67fc2-324">objectEmpty</span></span> | <span data-ttu-id="67fc2-325">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-325">Bool</span></span> | <span data-ttu-id="67fc2-326">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-326">True</span></span> |
| <span data-ttu-id="67fc2-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="67fc2-327">stringEmpty</span></span> | <span data-ttu-id="67fc2-328">Bool</span><span class="sxs-lookup"><span data-stu-id="67fc2-328">Bool</span></span> | <span data-ttu-id="67fc2-329">True </span><span class="sxs-lookup"><span data-stu-id="67fc2-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="67fc2-330">first</span><span class="sxs-lookup"><span data-stu-id="67fc2-330">first</span></span>
`first(arg1)`

<span data-ttu-id="67fc2-331">Retorna o primeiro elemento da matriz ou o primeiro caractere da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-332">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-332">Parameters</span></span>

| <span data-ttu-id="67fc2-333">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-333">Parameter</span></span> | <span data-ttu-id="67fc2-334">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-334">Required</span></span> | <span data-ttu-id="67fc2-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-335">Type</span></span> | <span data-ttu-id="67fc2-336">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-337">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-337">arg1</span></span> |<span data-ttu-id="67fc2-338">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-338">Yes</span></span> |<span data-ttu-id="67fc2-339">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-339">array or string</span></span> |<span data-ttu-id="67fc2-340">O valor para recuperar o primeiro elemento ou caractere.</span><span class="sxs-lookup"><span data-stu-id="67fc2-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-341">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-341">Return value</span></span>

<span data-ttu-id="67fc2-342">O tipo (cadeia de caracteres, inteiro, matriz ou objeto) do primeiro elemento em uma matriz ou o primeiro caractere de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-343">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-343">Example</span></span>

<span data-ttu-id="67fc2-344">O exemplo a seguir mostra como usar a primeira função com uma matriz e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-344">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="67fc2-345">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-346">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-346">Name</span></span> | <span data-ttu-id="67fc2-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-347">Type</span></span> | <span data-ttu-id="67fc2-348">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-349">arrayOutput</span></span> | <span data-ttu-id="67fc2-350">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-350">String</span></span> | <span data-ttu-id="67fc2-351">one</span><span class="sxs-lookup"><span data-stu-id="67fc2-351">one</span></span> |
| <span data-ttu-id="67fc2-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-352">stringOutput</span></span> | <span data-ttu-id="67fc2-353">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-353">String</span></span> | <span data-ttu-id="67fc2-354">O</span><span class="sxs-lookup"><span data-stu-id="67fc2-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="67fc2-355">interseção</span><span class="sxs-lookup"><span data-stu-id="67fc2-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="67fc2-356">Retorna uma única matriz ou objeto com os elementos comuns dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="67fc2-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-357">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-357">Parameters</span></span>

| <span data-ttu-id="67fc2-358">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-358">Parameter</span></span> | <span data-ttu-id="67fc2-359">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-359">Required</span></span> | <span data-ttu-id="67fc2-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-360">Type</span></span> | <span data-ttu-id="67fc2-361">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-362">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-362">arg1</span></span> |<span data-ttu-id="67fc2-363">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-363">Yes</span></span> |<span data-ttu-id="67fc2-364">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-364">array or object</span></span> |<span data-ttu-id="67fc2-365">O primeiro valor a ser usado para localizar elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="67fc2-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="67fc2-366">arg2</span><span class="sxs-lookup"><span data-stu-id="67fc2-366">arg2</span></span> |<span data-ttu-id="67fc2-367">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-367">Yes</span></span> |<span data-ttu-id="67fc2-368">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-368">array or object</span></span> |<span data-ttu-id="67fc2-369">O segundo valor a ser usado para localizar elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="67fc2-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="67fc2-370">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="67fc2-370">additional arguments</span></span> |<span data-ttu-id="67fc2-371">Não</span><span class="sxs-lookup"><span data-stu-id="67fc2-371">No</span></span> |<span data-ttu-id="67fc2-372">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-372">array or object</span></span> |<span data-ttu-id="67fc2-373">Os valores adicionais a serem usados para localizar elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="67fc2-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-374">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-374">Return value</span></span>

<span data-ttu-id="67fc2-375">Uma matriz ou objeto com os elementos comuns.</span><span class="sxs-lookup"><span data-stu-id="67fc2-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-376">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-376">Example</span></span>

<span data-ttu-id="67fc2-377">O exemplo a seguir mostra como usar a interseção com matrizes e objetos:</span><span class="sxs-lookup"><span data-stu-id="67fc2-377">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="67fc2-378">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-379">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-379">Name</span></span> | <span data-ttu-id="67fc2-380">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-380">Type</span></span> | <span data-ttu-id="67fc2-381">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-382">objectOutput</span></span> | <span data-ttu-id="67fc2-383">Objeto</span><span class="sxs-lookup"><span data-stu-id="67fc2-383">Object</span></span> | <span data-ttu-id="67fc2-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="67fc2-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="67fc2-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-385">arrayOutput</span></span> | <span data-ttu-id="67fc2-386">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-386">Array</span></span> | <span data-ttu-id="67fc2-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="67fc2-388">json</span><span class="sxs-lookup"><span data-stu-id="67fc2-388">json</span></span>
`json(arg1)`

<span data-ttu-id="67fc2-389">Retorna um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="67fc2-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-390">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-390">Parameters</span></span>

| <span data-ttu-id="67fc2-391">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-391">Parameter</span></span> | <span data-ttu-id="67fc2-392">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-392">Required</span></span> | <span data-ttu-id="67fc2-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-393">Type</span></span> | <span data-ttu-id="67fc2-394">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-395">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-395">arg1</span></span> |<span data-ttu-id="67fc2-396">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-396">Yes</span></span> |<span data-ttu-id="67fc2-397">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-397">string</span></span> |<span data-ttu-id="67fc2-398">O valor a ser convertido para JSON.</span><span class="sxs-lookup"><span data-stu-id="67fc2-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="67fc2-399">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-399">Return value</span></span>

<span data-ttu-id="67fc2-400">O objeto JSON de cadeia de caracteres especificada, ou um objeto vazio quando **nulo** for especificado.</span><span class="sxs-lookup"><span data-stu-id="67fc2-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-401">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-401">Example</span></span>

<span data-ttu-id="67fc2-402">O exemplo a seguir mostra como usar a interseção com matrizes e objetos:</span><span class="sxs-lookup"><span data-stu-id="67fc2-402">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="67fc2-403">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-404">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-404">Name</span></span> | <span data-ttu-id="67fc2-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-405">Type</span></span> | <span data-ttu-id="67fc2-406">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-407">jsonOutput</span></span> | <span data-ttu-id="67fc2-408">Objeto</span><span class="sxs-lookup"><span data-stu-id="67fc2-408">Object</span></span> | <span data-ttu-id="67fc2-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="67fc2-409">{"a": "b"}</span></span> |
| <span data-ttu-id="67fc2-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-410">nullOutput</span></span> | <span data-ttu-id="67fc2-411">Booliano</span><span class="sxs-lookup"><span data-stu-id="67fc2-411">Boolean</span></span> | <span data-ttu-id="67fc2-412">True</span><span class="sxs-lookup"><span data-stu-id="67fc2-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="67fc2-413">last</span><span class="sxs-lookup"><span data-stu-id="67fc2-413">last</span></span>
`last (arg1)`

<span data-ttu-id="67fc2-414">Retorna o último elemento da matriz ou o último caractere da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-415">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-415">Parameters</span></span>

| <span data-ttu-id="67fc2-416">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-416">Parameter</span></span> | <span data-ttu-id="67fc2-417">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-417">Required</span></span> | <span data-ttu-id="67fc2-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-418">Type</span></span> | <span data-ttu-id="67fc2-419">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-420">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-420">arg1</span></span> |<span data-ttu-id="67fc2-421">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-421">Yes</span></span> |<span data-ttu-id="67fc2-422">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-422">array or string</span></span> |<span data-ttu-id="67fc2-423">O valor para recuperar o último elemento ou caractere.</span><span class="sxs-lookup"><span data-stu-id="67fc2-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-424">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-424">Return value</span></span>

<span data-ttu-id="67fc2-425">O tipo (cadeia de caracteres, inteiro, matriz ou objeto) do último elemento em uma matriz ou o último caractere de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-426">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-426">Example</span></span>

<span data-ttu-id="67fc2-427">O exemplo a seguir mostra como usar a última função com uma matriz e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-427">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="67fc2-428">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-429">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-429">Name</span></span> | <span data-ttu-id="67fc2-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-430">Type</span></span> | <span data-ttu-id="67fc2-431">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-432">arrayOutput</span></span> | <span data-ttu-id="67fc2-433">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-433">String</span></span> | <span data-ttu-id="67fc2-434">três</span><span class="sxs-lookup"><span data-stu-id="67fc2-434">three</span></span> |
| <span data-ttu-id="67fc2-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-435">stringOutput</span></span> | <span data-ttu-id="67fc2-436">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-436">String</span></span> | <span data-ttu-id="67fc2-437">e</span><span class="sxs-lookup"><span data-stu-id="67fc2-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="67fc2-438">length</span><span class="sxs-lookup"><span data-stu-id="67fc2-438">length</span></span>
`length(arg1)`

<span data-ttu-id="67fc2-439">Retorna o número de elementos em uma matriz ou os caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-440">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-440">Parameters</span></span>

| <span data-ttu-id="67fc2-441">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-441">Parameter</span></span> | <span data-ttu-id="67fc2-442">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-442">Required</span></span> | <span data-ttu-id="67fc2-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-443">Type</span></span> | <span data-ttu-id="67fc2-444">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-445">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-445">arg1</span></span> |<span data-ttu-id="67fc2-446">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-446">Yes</span></span> |<span data-ttu-id="67fc2-447">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-447">array or string</span></span> |<span data-ttu-id="67fc2-448">A matriz a ser usada para obter o número de elementos ou a cadeia de caracteres a ser usada para obter o número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-449">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-449">Return value</span></span>

<span data-ttu-id="67fc2-450">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="67fc2-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="67fc2-451">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-451">Example</span></span>

<span data-ttu-id="67fc2-452">O seguinte exemplo mostra como usar length com uma matriz e cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="67fc2-452">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="67fc2-453">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-454">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-454">Name</span></span> | <span data-ttu-id="67fc2-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-455">Type</span></span> | <span data-ttu-id="67fc2-456">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="67fc2-457">arrayLength</span></span> | <span data-ttu-id="67fc2-458">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-458">Int</span></span> | <span data-ttu-id="67fc2-459">3</span><span class="sxs-lookup"><span data-stu-id="67fc2-459">3</span></span> |
| <span data-ttu-id="67fc2-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="67fc2-460">stringLength</span></span> | <span data-ttu-id="67fc2-461">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-461">Int</span></span> | <span data-ttu-id="67fc2-462">13</span><span class="sxs-lookup"><span data-stu-id="67fc2-462">13</span></span> |

<span data-ttu-id="67fc2-463">Essa função pode ser usada com uma matriz para especificar o número de iterações durante a criação de recursos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="67fc2-464">No exemplo a seguir, o parâmetro **siteNames** faz referência a uma matriz de nomes a serem usados durante a criação de sites da web.</span><span class="sxs-lookup"><span data-stu-id="67fc2-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="67fc2-465">Para saber mais sobre como usar essa função com uma matriz, confira [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="67fc2-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="67fc2-466">Min</span><span class="sxs-lookup"><span data-stu-id="67fc2-466">min</span></span>
`min(arg1)`

<span data-ttu-id="67fc2-467">Retorna o valor mínimo de uma matriz de inteiros ou uma lista de inteiros separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="67fc2-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-468">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-468">Parameters</span></span>

| <span data-ttu-id="67fc2-469">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-469">Parameter</span></span> | <span data-ttu-id="67fc2-470">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-470">Required</span></span> | <span data-ttu-id="67fc2-471">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-471">Type</span></span> | <span data-ttu-id="67fc2-472">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-473">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-473">arg1</span></span> |<span data-ttu-id="67fc2-474">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-474">Yes</span></span> |<span data-ttu-id="67fc2-475">matriz de inteiros ou lista de inteiros separados por vírgulas</span><span class="sxs-lookup"><span data-stu-id="67fc2-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="67fc2-476">A coleção para obtenção do valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="67fc2-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-477">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-477">Return value</span></span>

<span data-ttu-id="67fc2-478">Um inteiro que representa o valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="67fc2-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-479">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-479">Example</span></span>

<span data-ttu-id="67fc2-480">O seguinte exemplo mostra como usar min com uma matriz e uma lista de inteiros:</span><span class="sxs-lookup"><span data-stu-id="67fc2-480">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="67fc2-481">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-482">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-482">Name</span></span> | <span data-ttu-id="67fc2-483">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-483">Type</span></span> | <span data-ttu-id="67fc2-484">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-485">arrayOutput</span></span> | <span data-ttu-id="67fc2-486">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-486">Int</span></span> | <span data-ttu-id="67fc2-487">0</span><span class="sxs-lookup"><span data-stu-id="67fc2-487">0</span></span> |
| <span data-ttu-id="67fc2-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-488">intOutput</span></span> | <span data-ttu-id="67fc2-489">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-489">Int</span></span> | <span data-ttu-id="67fc2-490">0</span><span class="sxs-lookup"><span data-stu-id="67fc2-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="67fc2-491">max</span><span class="sxs-lookup"><span data-stu-id="67fc2-491">max</span></span>
`max(arg1)`

<span data-ttu-id="67fc2-492">Retorna o valor máximo de uma matriz de inteiros ou uma lista de inteiros separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="67fc2-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-493">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-493">Parameters</span></span>

| <span data-ttu-id="67fc2-494">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-494">Parameter</span></span> | <span data-ttu-id="67fc2-495">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-495">Required</span></span> | <span data-ttu-id="67fc2-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-496">Type</span></span> | <span data-ttu-id="67fc2-497">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-498">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-498">arg1</span></span> |<span data-ttu-id="67fc2-499">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-499">Yes</span></span> |<span data-ttu-id="67fc2-500">matriz de inteiros ou lista de inteiros separados por vírgulas</span><span class="sxs-lookup"><span data-stu-id="67fc2-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="67fc2-501">A coleção para obtenção do valor máximo.</span><span class="sxs-lookup"><span data-stu-id="67fc2-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-502">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-502">Return value</span></span>

<span data-ttu-id="67fc2-503">Um inteiro que representa o valor máximo.</span><span class="sxs-lookup"><span data-stu-id="67fc2-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-504">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-504">Example</span></span>

<span data-ttu-id="67fc2-505">O seguinte exemplo mostra como usar max com uma matriz e uma lista de inteiros:</span><span class="sxs-lookup"><span data-stu-id="67fc2-505">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="67fc2-506">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-507">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-507">Name</span></span> | <span data-ttu-id="67fc2-508">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-508">Type</span></span> | <span data-ttu-id="67fc2-509">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-510">arrayOutput</span></span> | <span data-ttu-id="67fc2-511">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-511">Int</span></span> | <span data-ttu-id="67fc2-512">5</span><span class="sxs-lookup"><span data-stu-id="67fc2-512">5</span></span> |
| <span data-ttu-id="67fc2-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-513">intOutput</span></span> | <span data-ttu-id="67fc2-514">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-514">Int</span></span> | <span data-ttu-id="67fc2-515">5</span><span class="sxs-lookup"><span data-stu-id="67fc2-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="67fc2-516">range</span><span class="sxs-lookup"><span data-stu-id="67fc2-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="67fc2-517">Cria uma matriz de inteiros a partir de um inteiro inicial e contendo um número de itens.</span><span class="sxs-lookup"><span data-stu-id="67fc2-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-518">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-518">Parameters</span></span>

| <span data-ttu-id="67fc2-519">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-519">Parameter</span></span> | <span data-ttu-id="67fc2-520">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-520">Required</span></span> | <span data-ttu-id="67fc2-521">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-521">Type</span></span> | <span data-ttu-id="67fc2-522">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="67fc2-523">startingInteger</span></span> |<span data-ttu-id="67fc2-524">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-524">Yes</span></span> |<span data-ttu-id="67fc2-525">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-525">int</span></span> |<span data-ttu-id="67fc2-526">O primeiro inteiro na matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-526">The first integer in the array.</span></span> |
| <span data-ttu-id="67fc2-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="67fc2-527">numberofElements</span></span> |<span data-ttu-id="67fc2-528">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-528">Yes</span></span> |<span data-ttu-id="67fc2-529">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-529">int</span></span> |<span data-ttu-id="67fc2-530">O número de inteiros na matriz.</span><span class="sxs-lookup"><span data-stu-id="67fc2-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-531">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-531">Return value</span></span>

<span data-ttu-id="67fc2-532">Uma matriz de inteiros.</span><span class="sxs-lookup"><span data-stu-id="67fc2-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-533">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-533">Example</span></span>

<span data-ttu-id="67fc2-534">O exemplo a seguir mostra como usar a função range:</span><span class="sxs-lookup"><span data-stu-id="67fc2-534">The following example shows how to use the range function:</span></span>

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

<span data-ttu-id="67fc2-535">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-536">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-536">Name</span></span> | <span data-ttu-id="67fc2-537">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-537">Type</span></span> | <span data-ttu-id="67fc2-538">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-539">rangeOutput</span></span> | <span data-ttu-id="67fc2-540">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-540">Array</span></span> | <span data-ttu-id="67fc2-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="67fc2-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="67fc2-542">skip</span><span class="sxs-lookup"><span data-stu-id="67fc2-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="67fc2-543">Retorna uma matriz com todos os elementos após o número especificado na matriz, ou retorna uma cadeia de caracteres com todos os caracteres após o número especificado na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-544">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-544">Parameters</span></span>

| <span data-ttu-id="67fc2-545">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-545">Parameter</span></span> | <span data-ttu-id="67fc2-546">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-546">Required</span></span> | <span data-ttu-id="67fc2-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-547">Type</span></span> | <span data-ttu-id="67fc2-548">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="67fc2-549">originalValue</span></span> |<span data-ttu-id="67fc2-550">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-550">Yes</span></span> |<span data-ttu-id="67fc2-551">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-551">array or string</span></span> |<span data-ttu-id="67fc2-552">A matriz ou cadeia de caracteres a ser usada para ignorar.</span><span class="sxs-lookup"><span data-stu-id="67fc2-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="67fc2-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="67fc2-553">numberToSkip</span></span> |<span data-ttu-id="67fc2-554">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-554">Yes</span></span> |<span data-ttu-id="67fc2-555">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-555">int</span></span> |<span data-ttu-id="67fc2-556">O número de elementos ou caracteres a ser ignorado.</span><span class="sxs-lookup"><span data-stu-id="67fc2-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="67fc2-557">Se esse valor for 0 ou menos, todos os elementos ou caracteres no valor serão retornados.</span><span class="sxs-lookup"><span data-stu-id="67fc2-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="67fc2-558">Se for maior que o tamanho da matriz ou cadeia de caracteres, uma matriz ou cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="67fc2-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-559">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-559">Return value</span></span>

<span data-ttu-id="67fc2-560">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-561">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-561">Example</span></span>

<span data-ttu-id="67fc2-562">O exemplo a seguir ignora o número especificado de elementos na matriz e o número especificado de caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="67fc2-563">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-564">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-564">Name</span></span> | <span data-ttu-id="67fc2-565">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-565">Type</span></span> | <span data-ttu-id="67fc2-566">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-567">arrayOutput</span></span> | <span data-ttu-id="67fc2-568">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-568">Array</span></span> | <span data-ttu-id="67fc2-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-569">["three"]</span></span> |
| <span data-ttu-id="67fc2-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-570">stringOutput</span></span> | <span data-ttu-id="67fc2-571">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-571">String</span></span> | <span data-ttu-id="67fc2-572">two three</span><span class="sxs-lookup"><span data-stu-id="67fc2-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="67fc2-573">take</span><span class="sxs-lookup"><span data-stu-id="67fc2-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="67fc2-574">Retorna uma matriz com o número especificado de elementos desde o início da matriz, ou uma cadeia de caracteres com o número especificado de caracteres desde o início da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-575">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-575">Parameters</span></span>

| <span data-ttu-id="67fc2-576">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-576">Parameter</span></span> | <span data-ttu-id="67fc2-577">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-577">Required</span></span> | <span data-ttu-id="67fc2-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-578">Type</span></span> | <span data-ttu-id="67fc2-579">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="67fc2-580">originalValue</span></span> |<span data-ttu-id="67fc2-581">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-581">Yes</span></span> |<span data-ttu-id="67fc2-582">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-582">array or string</span></span> |<span data-ttu-id="67fc2-583">A matriz ou cadeia de caracteres da qual extrair os elementos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="67fc2-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="67fc2-584">numberToTake</span></span> |<span data-ttu-id="67fc2-585">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-585">Yes</span></span> |<span data-ttu-id="67fc2-586">int</span><span class="sxs-lookup"><span data-stu-id="67fc2-586">int</span></span> |<span data-ttu-id="67fc2-587">O número de elementos ou caracteres a ser extraído.</span><span class="sxs-lookup"><span data-stu-id="67fc2-587">The number of elements or characters to take.</span></span> <span data-ttu-id="67fc2-588">Se esse valor for 0 ou menos, uma matriz ou cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="67fc2-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="67fc2-589">Se for maior que o tamanho da matriz ou cadeia de caracteres especificada, todos os elementos da matriz ou cadeia de caracteres serão retornados.</span><span class="sxs-lookup"><span data-stu-id="67fc2-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-590">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-590">Return value</span></span>

<span data-ttu-id="67fc2-591">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-592">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-592">Example</span></span>

<span data-ttu-id="67fc2-593">O exemplo a seguir extrai o número especificado de elementos da matriz e de caracteres de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="67fc2-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="67fc2-594">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-595">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-595">Name</span></span> | <span data-ttu-id="67fc2-596">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-596">Type</span></span> | <span data-ttu-id="67fc2-597">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-598">arrayOutput</span></span> | <span data-ttu-id="67fc2-599">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-599">Array</span></span> | <span data-ttu-id="67fc2-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-600">["one", "two"]</span></span> |
| <span data-ttu-id="67fc2-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-601">stringOutput</span></span> | <span data-ttu-id="67fc2-602">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="67fc2-602">String</span></span> | <span data-ttu-id="67fc2-603">em</span><span class="sxs-lookup"><span data-stu-id="67fc2-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="67fc2-604">union</span><span class="sxs-lookup"><span data-stu-id="67fc2-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="67fc2-605">Retorna uma única matriz ou objeto com todos os elementos dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="67fc2-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="67fc2-606">Valores duplicados ou chaves só são incluídos uma vez.</span><span class="sxs-lookup"><span data-stu-id="67fc2-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="67fc2-607">parâmetros</span><span class="sxs-lookup"><span data-stu-id="67fc2-607">Parameters</span></span>

| <span data-ttu-id="67fc2-608">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="67fc2-608">Parameter</span></span> | <span data-ttu-id="67fc2-609">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="67fc2-609">Required</span></span> | <span data-ttu-id="67fc2-610">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-610">Type</span></span> | <span data-ttu-id="67fc2-611">Descrição</span><span class="sxs-lookup"><span data-stu-id="67fc2-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67fc2-612">arg1</span><span class="sxs-lookup"><span data-stu-id="67fc2-612">arg1</span></span> |<span data-ttu-id="67fc2-613">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-613">Yes</span></span> |<span data-ttu-id="67fc2-614">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-614">array or object</span></span> |<span data-ttu-id="67fc2-615">O primeiro valor a ser usado para unir elementos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="67fc2-616">arg2</span><span class="sxs-lookup"><span data-stu-id="67fc2-616">arg2</span></span> |<span data-ttu-id="67fc2-617">Sim</span><span class="sxs-lookup"><span data-stu-id="67fc2-617">Yes</span></span> |<span data-ttu-id="67fc2-618">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-618">array or object</span></span> |<span data-ttu-id="67fc2-619">O segundo valor a ser usado para unir elementos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="67fc2-620">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="67fc2-620">additional arguments</span></span> |<span data-ttu-id="67fc2-621">Não</span><span class="sxs-lookup"><span data-stu-id="67fc2-621">No</span></span> |<span data-ttu-id="67fc2-622">objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-622">array or object</span></span> |<span data-ttu-id="67fc2-623">Valores adicionais a serem usados para unir elementos.</span><span class="sxs-lookup"><span data-stu-id="67fc2-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67fc2-624">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="67fc2-624">Return value</span></span>

<span data-ttu-id="67fc2-625">Uma matriz ou objeto.</span><span class="sxs-lookup"><span data-stu-id="67fc2-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="67fc2-626">Exemplo</span><span class="sxs-lookup"><span data-stu-id="67fc2-626">Example</span></span>

<span data-ttu-id="67fc2-627">O exemplo a seguir mostra como usar a union com matrizes e objetos:</span><span class="sxs-lookup"><span data-stu-id="67fc2-627">The following example shows how to use union with arrays and objects:</span></span>

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

<span data-ttu-id="67fc2-628">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="67fc2-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67fc2-629">Nome</span><span class="sxs-lookup"><span data-stu-id="67fc2-629">Name</span></span> | <span data-ttu-id="67fc2-630">Tipo</span><span class="sxs-lookup"><span data-stu-id="67fc2-630">Type</span></span> | <span data-ttu-id="67fc2-631">Valor</span><span class="sxs-lookup"><span data-stu-id="67fc2-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67fc2-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-632">objectOutput</span></span> | <span data-ttu-id="67fc2-633">Objeto</span><span class="sxs-lookup"><span data-stu-id="67fc2-633">Object</span></span> | <span data-ttu-id="67fc2-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="67fc2-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="67fc2-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67fc2-635">arrayOutput</span></span> | <span data-ttu-id="67fc2-636">Matriz</span><span class="sxs-lookup"><span data-stu-id="67fc2-636">Array</span></span> | <span data-ttu-id="67fc2-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="67fc2-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67fc2-638">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67fc2-638">Next steps</span></span>
* <span data-ttu-id="67fc2-639">Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67fc2-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="67fc2-640">Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67fc2-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="67fc2-641">Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="67fc2-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="67fc2-642">Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="67fc2-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

