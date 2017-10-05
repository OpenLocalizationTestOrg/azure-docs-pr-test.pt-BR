---
title: "Funções do modelo do Azure Resource Manager – lógicas | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Resource Manager para determinar valores lógicos."
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
ms.openlocfilehash: 313601ad99cdc12c4b50f5469959d37a9fa70d35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="3d21e-103">Funções lógicas para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d21e-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="3d21e-104">O Resource Manager fornece várias funções para fazer comparações em seus modelos.</span><span class="sxs-lookup"><span data-stu-id="3d21e-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="3d21e-105">and</span><span class="sxs-lookup"><span data-stu-id="3d21e-105">and</span></span>](#and)
* [<span data-ttu-id="3d21e-106">bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-106">bool</span></span>](#bool)
* [<span data-ttu-id="3d21e-107">if</span><span class="sxs-lookup"><span data-stu-id="3d21e-107">if</span></span>](#if)
* [<span data-ttu-id="3d21e-108">not</span><span class="sxs-lookup"><span data-stu-id="3d21e-108">not</span></span>](#not)
* [<span data-ttu-id="3d21e-109">or</span><span class="sxs-lookup"><span data-stu-id="3d21e-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="3d21e-110">e</span><span class="sxs-lookup"><span data-stu-id="3d21e-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="3d21e-111">Verifica se os dois valores de parâmetro são verdadeiros.</span><span class="sxs-lookup"><span data-stu-id="3d21e-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d21e-112">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="3d21e-112">Parameters</span></span>

| <span data-ttu-id="3d21e-113">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3d21e-113">Parameter</span></span> | <span data-ttu-id="3d21e-114">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3d21e-114">Required</span></span> | <span data-ttu-id="3d21e-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-115">Type</span></span> | <span data-ttu-id="3d21e-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="3d21e-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d21e-117">arg1</span><span class="sxs-lookup"><span data-stu-id="3d21e-117">arg1</span></span> |<span data-ttu-id="3d21e-118">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-118">Yes</span></span> |<span data-ttu-id="3d21e-119">Booliano</span><span class="sxs-lookup"><span data-stu-id="3d21e-119">boolean</span></span> |<span data-ttu-id="3d21e-120">O primeiro valor para verificar se é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="3d21e-121">arg2</span><span class="sxs-lookup"><span data-stu-id="3d21e-121">arg2</span></span> |<span data-ttu-id="3d21e-122">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-122">Yes</span></span> |<span data-ttu-id="3d21e-123">Booliano</span><span class="sxs-lookup"><span data-stu-id="3d21e-123">boolean</span></span> |<span data-ttu-id="3d21e-124">O segundo valor para verificar se é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3d21e-125">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="3d21e-125">Return value</span></span>

<span data-ttu-id="3d21e-126">Retorna **True** se os dois valores forem verdadeiros; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="3d21e-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="3d21e-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d21e-127">Examples</span></span>

<span data-ttu-id="3d21e-128">O exemplo a seguir mostra como usar funções lógicas.</span><span class="sxs-lookup"><span data-stu-id="3d21e-128">The following example shows how to use logical functions.</span></span>

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

<span data-ttu-id="3d21e-129">O resultado do exemplo anterior é:</span><span class="sxs-lookup"><span data-stu-id="3d21e-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="3d21e-130">Nome</span><span class="sxs-lookup"><span data-stu-id="3d21e-130">Name</span></span> | <span data-ttu-id="3d21e-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-131">Type</span></span> | <span data-ttu-id="3d21e-132">Valor</span><span class="sxs-lookup"><span data-stu-id="3d21e-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d21e-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-133">andExampleOutput</span></span> | <span data-ttu-id="3d21e-134">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-134">Bool</span></span> | <span data-ttu-id="3d21e-135">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-135">False</span></span> |
| <span data-ttu-id="3d21e-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-136">orExampleOutput</span></span> | <span data-ttu-id="3d21e-137">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-137">Bool</span></span> | <span data-ttu-id="3d21e-138">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="3d21e-138">True</span></span> |
| <span data-ttu-id="3d21e-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-139">notExampleOutput</span></span> | <span data-ttu-id="3d21e-140">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-140">Bool</span></span> | <span data-ttu-id="3d21e-141">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="3d21e-142">bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="3d21e-143">Converte o parâmetro em um booliano.</span><span class="sxs-lookup"><span data-stu-id="3d21e-143">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d21e-144">parâmetros</span><span class="sxs-lookup"><span data-stu-id="3d21e-144">Parameters</span></span>

| <span data-ttu-id="3d21e-145">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3d21e-145">Parameter</span></span> | <span data-ttu-id="3d21e-146">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3d21e-146">Required</span></span> | <span data-ttu-id="3d21e-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-147">Type</span></span> | <span data-ttu-id="3d21e-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="3d21e-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d21e-149">arg1</span><span class="sxs-lookup"><span data-stu-id="3d21e-149">arg1</span></span> |<span data-ttu-id="3d21e-150">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-150">Yes</span></span> |<span data-ttu-id="3d21e-151">cadeia de caracteres ou inteiro</span><span class="sxs-lookup"><span data-stu-id="3d21e-151">string or int</span></span> |<span data-ttu-id="3d21e-152">O valor a ser convertido em um booliano.</span><span class="sxs-lookup"><span data-stu-id="3d21e-152">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3d21e-153">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="3d21e-153">Return value</span></span>
<span data-ttu-id="3d21e-154">Um booliano do valor convertido.</span><span class="sxs-lookup"><span data-stu-id="3d21e-154">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="3d21e-155">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d21e-155">Examples</span></span>

<span data-ttu-id="3d21e-156">O exemplo a seguir mostra como usar um booliano com uma cadeia de caracteres ou um inteiro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-156">The following example shows how to use bool with a string or integer.</span></span>

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

<span data-ttu-id="3d21e-157">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="3d21e-157">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3d21e-158">Nome</span><span class="sxs-lookup"><span data-stu-id="3d21e-158">Name</span></span> | <span data-ttu-id="3d21e-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-159">Type</span></span> | <span data-ttu-id="3d21e-160">Valor</span><span class="sxs-lookup"><span data-stu-id="3d21e-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d21e-161">trueString</span><span class="sxs-lookup"><span data-stu-id="3d21e-161">trueString</span></span> | <span data-ttu-id="3d21e-162">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-162">Bool</span></span> | <span data-ttu-id="3d21e-163">True </span><span class="sxs-lookup"><span data-stu-id="3d21e-163">True</span></span> |
| <span data-ttu-id="3d21e-164">falseString</span><span class="sxs-lookup"><span data-stu-id="3d21e-164">falseString</span></span> | <span data-ttu-id="3d21e-165">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-165">Bool</span></span> | <span data-ttu-id="3d21e-166">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-166">False</span></span> |
| <span data-ttu-id="3d21e-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="3d21e-167">trueInt</span></span> | <span data-ttu-id="3d21e-168">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-168">Bool</span></span> | <span data-ttu-id="3d21e-169">True </span><span class="sxs-lookup"><span data-stu-id="3d21e-169">True</span></span> |
| <span data-ttu-id="3d21e-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="3d21e-170">falseInt</span></span> | <span data-ttu-id="3d21e-171">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-171">Bool</span></span> | <span data-ttu-id="3d21e-172">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="3d21e-173">if</span><span class="sxs-lookup"><span data-stu-id="3d21e-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="3d21e-174">Retorna um valor com base em se uma condição é verdadeira ou falsa.</span><span class="sxs-lookup"><span data-stu-id="3d21e-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d21e-175">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="3d21e-175">Parameters</span></span>

| <span data-ttu-id="3d21e-176">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3d21e-176">Parameter</span></span> | <span data-ttu-id="3d21e-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3d21e-177">Required</span></span> | <span data-ttu-id="3d21e-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-178">Type</span></span> | <span data-ttu-id="3d21e-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="3d21e-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d21e-180">condition</span><span class="sxs-lookup"><span data-stu-id="3d21e-180">condition</span></span> |<span data-ttu-id="3d21e-181">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-181">Yes</span></span> |<span data-ttu-id="3d21e-182">Booliano</span><span class="sxs-lookup"><span data-stu-id="3d21e-182">boolean</span></span> |<span data-ttu-id="3d21e-183">O valor para verificar se é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-183">The value to check whether it is true.</span></span> |
| <span data-ttu-id="3d21e-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="3d21e-184">trueValue</span></span> |<span data-ttu-id="3d21e-185">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-185">Yes</span></span> | <span data-ttu-id="3d21e-186">cadeia de caracteres, inteiro, objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="3d21e-186">string, int, object, or array</span></span> |<span data-ttu-id="3d21e-187">O valor a ser retornado quando a condição é verdadeira.</span><span class="sxs-lookup"><span data-stu-id="3d21e-187">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="3d21e-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="3d21e-188">falseValue</span></span> |<span data-ttu-id="3d21e-189">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-189">Yes</span></span> | <span data-ttu-id="3d21e-190">cadeia de caracteres, inteiro, objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="3d21e-190">string, int, object, or array</span></span> |<span data-ttu-id="3d21e-191">O valor a ser retornado quando a condição é falsa.</span><span class="sxs-lookup"><span data-stu-id="3d21e-191">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3d21e-192">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="3d21e-192">Return value</span></span>

<span data-ttu-id="3d21e-193">Retorna o segundo parâmetro quando o primeiro parâmetro é **True**; caso contrário, retorna o terceiro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="3d21e-194">Comentários</span><span class="sxs-lookup"><span data-stu-id="3d21e-194">Remarks</span></span>

<span data-ttu-id="3d21e-195">Você pode usar essa função definir condicionalmente uma propriedade de recurso.</span><span class="sxs-lookup"><span data-stu-id="3d21e-195">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="3d21e-196">O exemplo a seguir não é um modelo completo, mas ele mostra as partes relevantes para a configuração condicional do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3d21e-196">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="3d21e-197">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d21e-197">Examples</span></span>

<span data-ttu-id="3d21e-198">O exemplo a seguir mostra como usar a função `if`.</span><span class="sxs-lookup"><span data-stu-id="3d21e-198">The following example shows how to use the `if` function.</span></span>

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

<span data-ttu-id="3d21e-199">O resultado do exemplo anterior é:</span><span class="sxs-lookup"><span data-stu-id="3d21e-199">The output from the preceding example is:</span></span>

| <span data-ttu-id="3d21e-200">Nome</span><span class="sxs-lookup"><span data-stu-id="3d21e-200">Name</span></span> | <span data-ttu-id="3d21e-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-201">Type</span></span> | <span data-ttu-id="3d21e-202">Valor</span><span class="sxs-lookup"><span data-stu-id="3d21e-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d21e-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-203">yesOutput</span></span> | <span data-ttu-id="3d21e-204">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3d21e-204">String</span></span> | <span data-ttu-id="3d21e-205">sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-205">yes</span></span> |
| <span data-ttu-id="3d21e-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-206">noOutput</span></span> | <span data-ttu-id="3d21e-207">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3d21e-207">String</span></span> | <span data-ttu-id="3d21e-208">não</span><span class="sxs-lookup"><span data-stu-id="3d21e-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="3d21e-209">não</span><span class="sxs-lookup"><span data-stu-id="3d21e-209">not</span></span>
`not(arg1)`

<span data-ttu-id="3d21e-210">Converte o valor booliano em seu valor oposto.</span><span class="sxs-lookup"><span data-stu-id="3d21e-210">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d21e-211">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="3d21e-211">Parameters</span></span>

| <span data-ttu-id="3d21e-212">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3d21e-212">Parameter</span></span> | <span data-ttu-id="3d21e-213">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3d21e-213">Required</span></span> | <span data-ttu-id="3d21e-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-214">Type</span></span> | <span data-ttu-id="3d21e-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="3d21e-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d21e-216">arg1</span><span class="sxs-lookup"><span data-stu-id="3d21e-216">arg1</span></span> |<span data-ttu-id="3d21e-217">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-217">Yes</span></span> |<span data-ttu-id="3d21e-218">Booliano</span><span class="sxs-lookup"><span data-stu-id="3d21e-218">boolean</span></span> |<span data-ttu-id="3d21e-219">O valor a ser convertido.</span><span class="sxs-lookup"><span data-stu-id="3d21e-219">The value to convert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="3d21e-220">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="3d21e-220">Return value</span></span>

<span data-ttu-id="3d21e-221">Retorna **True** quando o parâmetro é **False**.</span><span class="sxs-lookup"><span data-stu-id="3d21e-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="3d21e-222">Retorna **False** quando o parâmetro é **True**.</span><span class="sxs-lookup"><span data-stu-id="3d21e-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="3d21e-223">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d21e-223">Examples</span></span>

<span data-ttu-id="3d21e-224">O exemplo a seguir mostra como usar funções lógicas.</span><span class="sxs-lookup"><span data-stu-id="3d21e-224">The following example shows how to use logical functions.</span></span>

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

<span data-ttu-id="3d21e-225">O resultado do exemplo anterior é:</span><span class="sxs-lookup"><span data-stu-id="3d21e-225">The output from the preceding example is:</span></span>

| <span data-ttu-id="3d21e-226">Nome</span><span class="sxs-lookup"><span data-stu-id="3d21e-226">Name</span></span> | <span data-ttu-id="3d21e-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-227">Type</span></span> | <span data-ttu-id="3d21e-228">Valor</span><span class="sxs-lookup"><span data-stu-id="3d21e-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d21e-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-229">andExampleOutput</span></span> | <span data-ttu-id="3d21e-230">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-230">Bool</span></span> | <span data-ttu-id="3d21e-231">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-231">False</span></span> |
| <span data-ttu-id="3d21e-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-232">orExampleOutput</span></span> | <span data-ttu-id="3d21e-233">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-233">Bool</span></span> | <span data-ttu-id="3d21e-234">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="3d21e-234">True</span></span> |
| <span data-ttu-id="3d21e-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-235">notExampleOutput</span></span> | <span data-ttu-id="3d21e-236">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-236">Bool</span></span> | <span data-ttu-id="3d21e-237">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-237">False</span></span> |

<span data-ttu-id="3d21e-238">O exemplo a seguir usa **não** com [é igual a](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="3d21e-238">The following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="3d21e-239">O resultado do exemplo anterior é:</span><span class="sxs-lookup"><span data-stu-id="3d21e-239">The output from the preceding example is:</span></span>

| <span data-ttu-id="3d21e-240">Nome</span><span class="sxs-lookup"><span data-stu-id="3d21e-240">Name</span></span> | <span data-ttu-id="3d21e-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-241">Type</span></span> | <span data-ttu-id="3d21e-242">Valor</span><span class="sxs-lookup"><span data-stu-id="3d21e-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d21e-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="3d21e-243">checkNotEquals</span></span> | <span data-ttu-id="3d21e-244">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-244">Bool</span></span> | <span data-ttu-id="3d21e-245">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="3d21e-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="3d21e-246">ou o</span><span class="sxs-lookup"><span data-stu-id="3d21e-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="3d21e-247">Verifica se o valor do parâmetro é true.</span><span class="sxs-lookup"><span data-stu-id="3d21e-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d21e-248">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="3d21e-248">Parameters</span></span>

| <span data-ttu-id="3d21e-249">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3d21e-249">Parameter</span></span> | <span data-ttu-id="3d21e-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3d21e-250">Required</span></span> | <span data-ttu-id="3d21e-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-251">Type</span></span> | <span data-ttu-id="3d21e-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="3d21e-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d21e-253">arg1</span><span class="sxs-lookup"><span data-stu-id="3d21e-253">arg1</span></span> |<span data-ttu-id="3d21e-254">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-254">Yes</span></span> |<span data-ttu-id="3d21e-255">Booliano</span><span class="sxs-lookup"><span data-stu-id="3d21e-255">boolean</span></span> |<span data-ttu-id="3d21e-256">O primeiro valor para verificar se é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-256">The first value to check whether is true.</span></span> |
| <span data-ttu-id="3d21e-257">arg2</span><span class="sxs-lookup"><span data-stu-id="3d21e-257">arg2</span></span> |<span data-ttu-id="3d21e-258">Sim</span><span class="sxs-lookup"><span data-stu-id="3d21e-258">Yes</span></span> |<span data-ttu-id="3d21e-259">Booliano</span><span class="sxs-lookup"><span data-stu-id="3d21e-259">boolean</span></span> |<span data-ttu-id="3d21e-260">O segundo valor para verificar se é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3d21e-260">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3d21e-261">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="3d21e-261">Return value</span></span>

<span data-ttu-id="3d21e-262">Retorna **True** se qualquer valor é verdadeiro; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="3d21e-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="3d21e-263">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d21e-263">Examples</span></span>

<span data-ttu-id="3d21e-264">O exemplo a seguir mostra como usar funções lógicas.</span><span class="sxs-lookup"><span data-stu-id="3d21e-264">The following example shows how to use logical functions.</span></span>

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

<span data-ttu-id="3d21e-265">O resultado do exemplo anterior é:</span><span class="sxs-lookup"><span data-stu-id="3d21e-265">The output from the preceding example is:</span></span>

| <span data-ttu-id="3d21e-266">Nome</span><span class="sxs-lookup"><span data-stu-id="3d21e-266">Name</span></span> | <span data-ttu-id="3d21e-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d21e-267">Type</span></span> | <span data-ttu-id="3d21e-268">Valor</span><span class="sxs-lookup"><span data-stu-id="3d21e-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d21e-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-269">andExampleOutput</span></span> | <span data-ttu-id="3d21e-270">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-270">Bool</span></span> | <span data-ttu-id="3d21e-271">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-271">False</span></span> |
| <span data-ttu-id="3d21e-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-272">orExampleOutput</span></span> | <span data-ttu-id="3d21e-273">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-273">Bool</span></span> | <span data-ttu-id="3d21e-274">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="3d21e-274">True</span></span> |
| <span data-ttu-id="3d21e-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3d21e-275">notExampleOutput</span></span> | <span data-ttu-id="3d21e-276">Bool</span><span class="sxs-lookup"><span data-stu-id="3d21e-276">Bool</span></span> | <span data-ttu-id="3d21e-277">Falso</span><span class="sxs-lookup"><span data-stu-id="3d21e-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3d21e-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d21e-278">Next steps</span></span>
* <span data-ttu-id="3d21e-279">Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3d21e-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3d21e-280">Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3d21e-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="3d21e-281">Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3d21e-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="3d21e-282">Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3d21e-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

