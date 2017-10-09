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
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="81851-103">Funções lógicas para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="81851-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="81851-104">O Resource Manager fornece várias funções para fazer comparações em seus modelos.</span><span class="sxs-lookup"><span data-stu-id="81851-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="81851-105">and</span><span class="sxs-lookup"><span data-stu-id="81851-105">and</span></span>](#and)
* [<span data-ttu-id="81851-106">bool</span><span class="sxs-lookup"><span data-stu-id="81851-106">bool</span></span>](#bool)
* [<span data-ttu-id="81851-107">if</span><span class="sxs-lookup"><span data-stu-id="81851-107">if</span></span>](#if)
* [<span data-ttu-id="81851-108">not</span><span class="sxs-lookup"><span data-stu-id="81851-108">not</span></span>](#not)
* [<span data-ttu-id="81851-109">or</span><span class="sxs-lookup"><span data-stu-id="81851-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="81851-110">e</span><span class="sxs-lookup"><span data-stu-id="81851-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="81851-111">Verifica se os dois valores de parâmetro são verdadeiros.</span><span class="sxs-lookup"><span data-stu-id="81851-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="81851-112">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="81851-112">Parameters</span></span>

| <span data-ttu-id="81851-113">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81851-113">Parameter</span></span> | <span data-ttu-id="81851-114">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="81851-114">Required</span></span> | <span data-ttu-id="81851-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-115">Type</span></span> | <span data-ttu-id="81851-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="81851-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="81851-117">arg1</span><span class="sxs-lookup"><span data-stu-id="81851-117">arg1</span></span> |<span data-ttu-id="81851-118">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-118">Yes</span></span> |<span data-ttu-id="81851-119">Booliano</span><span class="sxs-lookup"><span data-stu-id="81851-119">boolean</span></span> |<span data-ttu-id="81851-120">Olá primeiro toocheck de valor se for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="81851-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="81851-121">arg2</span><span class="sxs-lookup"><span data-stu-id="81851-121">arg2</span></span> |<span data-ttu-id="81851-122">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-122">Yes</span></span> |<span data-ttu-id="81851-123">Booliano</span><span class="sxs-lookup"><span data-stu-id="81851-123">boolean</span></span> |<span data-ttu-id="81851-124">Olá toocheck do segundo valor se for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="81851-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="81851-125">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="81851-125">Return value</span></span>

<span data-ttu-id="81851-126">Retorna **True** se os dois valores forem verdadeiros; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="81851-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="81851-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="81851-127">Examples</span></span>

<span data-ttu-id="81851-128">Olá mostrado no exemplo a seguir como toouse as funções lógicas.</span><span class="sxs-lookup"><span data-stu-id="81851-128">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="81851-129">saída Olá Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="81851-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="81851-130">Nome</span><span class="sxs-lookup"><span data-stu-id="81851-130">Name</span></span> | <span data-ttu-id="81851-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-131">Type</span></span> | <span data-ttu-id="81851-132">Valor</span><span class="sxs-lookup"><span data-stu-id="81851-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="81851-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-133">andExampleOutput</span></span> | <span data-ttu-id="81851-134">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-134">Bool</span></span> | <span data-ttu-id="81851-135">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-135">False</span></span> |
| <span data-ttu-id="81851-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-136">orExampleOutput</span></span> | <span data-ttu-id="81851-137">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-137">Bool</span></span> | <span data-ttu-id="81851-138">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="81851-138">True</span></span> |
| <span data-ttu-id="81851-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-139">notExampleOutput</span></span> | <span data-ttu-id="81851-140">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-140">Bool</span></span> | <span data-ttu-id="81851-141">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="81851-142">bool</span><span class="sxs-lookup"><span data-stu-id="81851-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="81851-143">Converte Olá tooa parâmetro booliano.</span><span class="sxs-lookup"><span data-stu-id="81851-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="81851-144">parâmetros</span><span class="sxs-lookup"><span data-stu-id="81851-144">Parameters</span></span>

| <span data-ttu-id="81851-145">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81851-145">Parameter</span></span> | <span data-ttu-id="81851-146">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="81851-146">Required</span></span> | <span data-ttu-id="81851-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-147">Type</span></span> | <span data-ttu-id="81851-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="81851-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="81851-149">arg1</span><span class="sxs-lookup"><span data-stu-id="81851-149">arg1</span></span> |<span data-ttu-id="81851-150">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-150">Yes</span></span> |<span data-ttu-id="81851-151">string ou int</span><span class="sxs-lookup"><span data-stu-id="81851-151">string or int</span></span> |<span data-ttu-id="81851-152">Olá tooa de tooconvert de valor booliano.</span><span class="sxs-lookup"><span data-stu-id="81851-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="81851-153">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="81851-153">Return value</span></span>
<span data-ttu-id="81851-154">Um valor booleano da saudação converter valor.</span><span class="sxs-lookup"><span data-stu-id="81851-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="81851-155">Exemplos</span><span class="sxs-lookup"><span data-stu-id="81851-155">Examples</span></span>

<span data-ttu-id="81851-156">Olá mostrado no exemplo a seguir como toouse bool com uma cadeia de caracteres ou um inteiro.</span><span class="sxs-lookup"><span data-stu-id="81851-156">hello following example shows how toouse bool with a string or integer.</span></span>

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

<span data-ttu-id="81851-157">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="81851-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="81851-158">Nome</span><span class="sxs-lookup"><span data-stu-id="81851-158">Name</span></span> | <span data-ttu-id="81851-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-159">Type</span></span> | <span data-ttu-id="81851-160">Valor</span><span class="sxs-lookup"><span data-stu-id="81851-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="81851-161">trueString</span><span class="sxs-lookup"><span data-stu-id="81851-161">trueString</span></span> | <span data-ttu-id="81851-162">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-162">Bool</span></span> | <span data-ttu-id="81851-163">True </span><span class="sxs-lookup"><span data-stu-id="81851-163">True</span></span> |
| <span data-ttu-id="81851-164">falseString</span><span class="sxs-lookup"><span data-stu-id="81851-164">falseString</span></span> | <span data-ttu-id="81851-165">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-165">Bool</span></span> | <span data-ttu-id="81851-166">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-166">False</span></span> |
| <span data-ttu-id="81851-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="81851-167">trueInt</span></span> | <span data-ttu-id="81851-168">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-168">Bool</span></span> | <span data-ttu-id="81851-169">True </span><span class="sxs-lookup"><span data-stu-id="81851-169">True</span></span> |
| <span data-ttu-id="81851-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="81851-170">falseInt</span></span> | <span data-ttu-id="81851-171">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-171">Bool</span></span> | <span data-ttu-id="81851-172">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="81851-173">if</span><span class="sxs-lookup"><span data-stu-id="81851-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="81851-174">Retorna um valor com base em se uma condição é verdadeira ou falsa.</span><span class="sxs-lookup"><span data-stu-id="81851-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="81851-175">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="81851-175">Parameters</span></span>

| <span data-ttu-id="81851-176">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81851-176">Parameter</span></span> | <span data-ttu-id="81851-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="81851-177">Required</span></span> | <span data-ttu-id="81851-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-178">Type</span></span> | <span data-ttu-id="81851-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="81851-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="81851-180">condition</span><span class="sxs-lookup"><span data-stu-id="81851-180">condition</span></span> |<span data-ttu-id="81851-181">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-181">Yes</span></span> |<span data-ttu-id="81851-182">Booliano</span><span class="sxs-lookup"><span data-stu-id="81851-182">boolean</span></span> |<span data-ttu-id="81851-183">Olá toocheck valor se for verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="81851-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="81851-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="81851-184">trueValue</span></span> |<span data-ttu-id="81851-185">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-185">Yes</span></span> | <span data-ttu-id="81851-186">cadeia de caracteres, inteiro, objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="81851-186">string, int, object, or array</span></span> |<span data-ttu-id="81851-187">Olá valor tooreturn quando Olá condição for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="81851-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="81851-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="81851-188">falseValue</span></span> |<span data-ttu-id="81851-189">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-189">Yes</span></span> | <span data-ttu-id="81851-190">cadeia de caracteres, inteiro, objeto ou matriz</span><span class="sxs-lookup"><span data-stu-id="81851-190">string, int, object, or array</span></span> |<span data-ttu-id="81851-191">Olá valor tooreturn quando Olá condição for falsa.</span><span class="sxs-lookup"><span data-stu-id="81851-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="81851-192">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="81851-192">Return value</span></span>

<span data-ttu-id="81851-193">Retorna o segundo parâmetro quando o primeiro parâmetro é **True**; caso contrário, retorna o terceiro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="81851-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="81851-194">Comentários</span><span class="sxs-lookup"><span data-stu-id="81851-194">Remarks</span></span>

<span data-ttu-id="81851-195">Você pode usar esse conjunto de tooconditionally de função uma propriedade de recurso.</span><span class="sxs-lookup"><span data-stu-id="81851-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="81851-196">Olá exemplo a seguir não é um modelo completo, mas ele mostra as partes relevantes de saudação para definir o conjunto de disponibilidade Olá condicionalmente.</span><span class="sxs-lookup"><span data-stu-id="81851-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="81851-197">Exemplos</span><span class="sxs-lookup"><span data-stu-id="81851-197">Examples</span></span>

<span data-ttu-id="81851-198">Olá mostrado no exemplo a seguir como toouse Olá `if` função.</span><span class="sxs-lookup"><span data-stu-id="81851-198">hello following example shows how toouse hello `if` function.</span></span>

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

<span data-ttu-id="81851-199">saída Olá Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="81851-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="81851-200">Nome</span><span class="sxs-lookup"><span data-stu-id="81851-200">Name</span></span> | <span data-ttu-id="81851-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-201">Type</span></span> | <span data-ttu-id="81851-202">Valor</span><span class="sxs-lookup"><span data-stu-id="81851-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="81851-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="81851-203">yesOutput</span></span> | <span data-ttu-id="81851-204">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="81851-204">String</span></span> | <span data-ttu-id="81851-205">sim</span><span class="sxs-lookup"><span data-stu-id="81851-205">yes</span></span> |
| <span data-ttu-id="81851-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="81851-206">noOutput</span></span> | <span data-ttu-id="81851-207">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="81851-207">String</span></span> | <span data-ttu-id="81851-208">não</span><span class="sxs-lookup"><span data-stu-id="81851-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="81851-209">não</span><span class="sxs-lookup"><span data-stu-id="81851-209">not</span></span>
`not(arg1)`

<span data-ttu-id="81851-210">Converte o valor booliano tooits oposta valor.</span><span class="sxs-lookup"><span data-stu-id="81851-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="81851-211">parâmetros</span><span class="sxs-lookup"><span data-stu-id="81851-211">Parameters</span></span>

| <span data-ttu-id="81851-212">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81851-212">Parameter</span></span> | <span data-ttu-id="81851-213">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="81851-213">Required</span></span> | <span data-ttu-id="81851-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-214">Type</span></span> | <span data-ttu-id="81851-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="81851-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="81851-216">arg1</span><span class="sxs-lookup"><span data-stu-id="81851-216">arg1</span></span> |<span data-ttu-id="81851-217">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-217">Yes</span></span> |<span data-ttu-id="81851-218">Booliano</span><span class="sxs-lookup"><span data-stu-id="81851-218">boolean</span></span> |<span data-ttu-id="81851-219">Olá tooconvert de valor.</span><span class="sxs-lookup"><span data-stu-id="81851-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="81851-220">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="81851-220">Return value</span></span>

<span data-ttu-id="81851-221">Retorna **True** quando o parâmetro é **False**.</span><span class="sxs-lookup"><span data-stu-id="81851-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="81851-222">Retorna **False** quando o parâmetro é **True**.</span><span class="sxs-lookup"><span data-stu-id="81851-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="81851-223">Exemplos</span><span class="sxs-lookup"><span data-stu-id="81851-223">Examples</span></span>

<span data-ttu-id="81851-224">Olá mostrado no exemplo a seguir como toouse as funções lógicas.</span><span class="sxs-lookup"><span data-stu-id="81851-224">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="81851-225">saída Olá Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="81851-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="81851-226">Nome</span><span class="sxs-lookup"><span data-stu-id="81851-226">Name</span></span> | <span data-ttu-id="81851-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-227">Type</span></span> | <span data-ttu-id="81851-228">Valor</span><span class="sxs-lookup"><span data-stu-id="81851-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="81851-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-229">andExampleOutput</span></span> | <span data-ttu-id="81851-230">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-230">Bool</span></span> | <span data-ttu-id="81851-231">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-231">False</span></span> |
| <span data-ttu-id="81851-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-232">orExampleOutput</span></span> | <span data-ttu-id="81851-233">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-233">Bool</span></span> | <span data-ttu-id="81851-234">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="81851-234">True</span></span> |
| <span data-ttu-id="81851-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-235">notExampleOutput</span></span> | <span data-ttu-id="81851-236">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-236">Bool</span></span> | <span data-ttu-id="81851-237">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-237">False</span></span> |

<span data-ttu-id="81851-238">Olá exemplo a seguir usa **não** com [é igual a](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="81851-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="81851-239">saída Olá Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="81851-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="81851-240">Nome</span><span class="sxs-lookup"><span data-stu-id="81851-240">Name</span></span> | <span data-ttu-id="81851-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-241">Type</span></span> | <span data-ttu-id="81851-242">Valor</span><span class="sxs-lookup"><span data-stu-id="81851-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="81851-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="81851-243">checkNotEquals</span></span> | <span data-ttu-id="81851-244">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-244">Bool</span></span> | <span data-ttu-id="81851-245">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="81851-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="81851-246">ou o</span><span class="sxs-lookup"><span data-stu-id="81851-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="81851-247">Verifica se o valor do parâmetro é true.</span><span class="sxs-lookup"><span data-stu-id="81851-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="81851-248">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="81851-248">Parameters</span></span>

| <span data-ttu-id="81851-249">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81851-249">Parameter</span></span> | <span data-ttu-id="81851-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="81851-250">Required</span></span> | <span data-ttu-id="81851-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-251">Type</span></span> | <span data-ttu-id="81851-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="81851-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="81851-253">arg1</span><span class="sxs-lookup"><span data-stu-id="81851-253">arg1</span></span> |<span data-ttu-id="81851-254">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-254">Yes</span></span> |<span data-ttu-id="81851-255">Booliano</span><span class="sxs-lookup"><span data-stu-id="81851-255">boolean</span></span> |<span data-ttu-id="81851-256">Olá primeiro toocheck de valor se for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="81851-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="81851-257">arg2</span><span class="sxs-lookup"><span data-stu-id="81851-257">arg2</span></span> |<span data-ttu-id="81851-258">Sim</span><span class="sxs-lookup"><span data-stu-id="81851-258">Yes</span></span> |<span data-ttu-id="81851-259">Booliano</span><span class="sxs-lookup"><span data-stu-id="81851-259">boolean</span></span> |<span data-ttu-id="81851-260">Olá toocheck do segundo valor se for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="81851-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="81851-261">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="81851-261">Return value</span></span>

<span data-ttu-id="81851-262">Retorna **True** se qualquer valor é verdadeiro; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="81851-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="81851-263">Exemplos</span><span class="sxs-lookup"><span data-stu-id="81851-263">Examples</span></span>

<span data-ttu-id="81851-264">Olá mostrado no exemplo a seguir como toouse as funções lógicas.</span><span class="sxs-lookup"><span data-stu-id="81851-264">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="81851-265">saída Olá Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="81851-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="81851-266">Nome</span><span class="sxs-lookup"><span data-stu-id="81851-266">Name</span></span> | <span data-ttu-id="81851-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="81851-267">Type</span></span> | <span data-ttu-id="81851-268">Valor</span><span class="sxs-lookup"><span data-stu-id="81851-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="81851-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-269">andExampleOutput</span></span> | <span data-ttu-id="81851-270">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-270">Bool</span></span> | <span data-ttu-id="81851-271">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-271">False</span></span> |
| <span data-ttu-id="81851-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-272">orExampleOutput</span></span> | <span data-ttu-id="81851-273">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-273">Bool</span></span> | <span data-ttu-id="81851-274">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="81851-274">True</span></span> |
| <span data-ttu-id="81851-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="81851-275">notExampleOutput</span></span> | <span data-ttu-id="81851-276">Bool</span><span class="sxs-lookup"><span data-stu-id="81851-276">Bool</span></span> | <span data-ttu-id="81851-277">Falso</span><span class="sxs-lookup"><span data-stu-id="81851-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="81851-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81851-278">Next steps</span></span>
* <span data-ttu-id="81851-279">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="81851-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="81851-280">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="81851-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="81851-281">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="81851-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="81851-282">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="81851-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

