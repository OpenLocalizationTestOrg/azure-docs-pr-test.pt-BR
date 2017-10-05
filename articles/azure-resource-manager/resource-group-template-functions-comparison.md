---
title: "Funções de modelo do Azure Resource Manager – comparação | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Resource Manager para comparar valores."
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="73af2-103">Funções de comparação para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="73af2-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="73af2-104">O Resource Manager fornece várias funções para fazer comparações em seus modelos.</span><span class="sxs-lookup"><span data-stu-id="73af2-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="73af2-105">equals</span><span class="sxs-lookup"><span data-stu-id="73af2-105">equals</span></span>](#equals)
* [<span data-ttu-id="73af2-106">greater</span><span class="sxs-lookup"><span data-stu-id="73af2-106">greater</span></span>](#greater)
* [<span data-ttu-id="73af2-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="73af2-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="73af2-108">less</span><span class="sxs-lookup"><span data-stu-id="73af2-108">less</span></span>](#less)
* [<span data-ttu-id="73af2-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="73af2-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="73af2-110">equals</span><span class="sxs-lookup"><span data-stu-id="73af2-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="73af2-111">Verifica se dois valores são iguais entre si.</span><span class="sxs-lookup"><span data-stu-id="73af2-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="73af2-112">parâmetros</span><span class="sxs-lookup"><span data-stu-id="73af2-112">Parameters</span></span>

| <span data-ttu-id="73af2-113">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="73af2-113">Parameter</span></span> | <span data-ttu-id="73af2-114">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="73af2-114">Required</span></span> | <span data-ttu-id="73af2-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-115">Type</span></span> | <span data-ttu-id="73af2-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="73af2-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="73af2-117">arg1</span><span class="sxs-lookup"><span data-stu-id="73af2-117">arg1</span></span> |<span data-ttu-id="73af2-118">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-118">Yes</span></span> |<span data-ttu-id="73af2-119">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="73af2-119">int, string, array, or object</span></span> |<span data-ttu-id="73af2-120">O primeiro valor para verificar a igualdade.</span><span class="sxs-lookup"><span data-stu-id="73af2-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="73af2-121">arg2</span><span class="sxs-lookup"><span data-stu-id="73af2-121">arg2</span></span> |<span data-ttu-id="73af2-122">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-122">Yes</span></span> |<span data-ttu-id="73af2-123">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="73af2-123">int, string, array, or object</span></span> |<span data-ttu-id="73af2-124">O segundo valor para verificar a igualdade.</span><span class="sxs-lookup"><span data-stu-id="73af2-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="73af2-125">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="73af2-125">Return value</span></span>

<span data-ttu-id="73af2-126">Retorna **True** se os valores são iguais; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="73af2-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="73af2-127">Comentários</span><span class="sxs-lookup"><span data-stu-id="73af2-127">Remarks</span></span>

<span data-ttu-id="73af2-128">A função equals é frequentemente usada com o elemento `condition` para testar se um recurso está implantado.</span><span class="sxs-lookup"><span data-stu-id="73af2-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="73af2-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="73af2-129">Example</span></span>

<span data-ttu-id="73af2-130">O modelo de exemplo verifica os diferentes tipos de valores para igualdade.</span><span class="sxs-lookup"><span data-stu-id="73af2-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="73af2-131">Todos os valores padrão retornam True.</span><span class="sxs-lookup"><span data-stu-id="73af2-131">All the default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="73af2-132">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="73af2-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="73af2-133">Nome</span><span class="sxs-lookup"><span data-stu-id="73af2-133">Name</span></span> | <span data-ttu-id="73af2-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-134">Type</span></span> | <span data-ttu-id="73af2-135">Valor</span><span class="sxs-lookup"><span data-stu-id="73af2-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="73af2-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="73af2-136">checkInts</span></span> | <span data-ttu-id="73af2-137">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-137">Bool</span></span> | <span data-ttu-id="73af2-138">True </span><span class="sxs-lookup"><span data-stu-id="73af2-138">True</span></span> |
| <span data-ttu-id="73af2-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="73af2-139">checkStrings</span></span> | <span data-ttu-id="73af2-140">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-140">Bool</span></span> | <span data-ttu-id="73af2-141">True </span><span class="sxs-lookup"><span data-stu-id="73af2-141">True</span></span> |
| <span data-ttu-id="73af2-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="73af2-142">checkArrays</span></span> | <span data-ttu-id="73af2-143">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-143">Bool</span></span> | <span data-ttu-id="73af2-144">True </span><span class="sxs-lookup"><span data-stu-id="73af2-144">True</span></span> |
| <span data-ttu-id="73af2-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="73af2-145">checkObjects</span></span> | <span data-ttu-id="73af2-146">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-146">Bool</span></span> | <span data-ttu-id="73af2-147">True</span><span class="sxs-lookup"><span data-stu-id="73af2-147">True</span></span> |


<span data-ttu-id="73af2-148">O exemplo a seguir usa [não](resource-group-template-functions-logical.md#not) com **é igual a**.</span><span class="sxs-lookup"><span data-stu-id="73af2-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="73af2-149">O resultado do exemplo anterior é:</span><span class="sxs-lookup"><span data-stu-id="73af2-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="73af2-150">Nome</span><span class="sxs-lookup"><span data-stu-id="73af2-150">Name</span></span> | <span data-ttu-id="73af2-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-151">Type</span></span> | <span data-ttu-id="73af2-152">Valor</span><span class="sxs-lookup"><span data-stu-id="73af2-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="73af2-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="73af2-153">checkNotEquals</span></span> | <span data-ttu-id="73af2-154">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-154">Bool</span></span> | <span data-ttu-id="73af2-155">True</span><span class="sxs-lookup"><span data-stu-id="73af2-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="73af2-156">greater</span><span class="sxs-lookup"><span data-stu-id="73af2-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="73af2-157">Verifica se o primeiro valor é maior que o segundo valor.</span><span class="sxs-lookup"><span data-stu-id="73af2-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="73af2-158">parâmetros</span><span class="sxs-lookup"><span data-stu-id="73af2-158">Parameters</span></span>

| <span data-ttu-id="73af2-159">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="73af2-159">Parameter</span></span> | <span data-ttu-id="73af2-160">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="73af2-160">Required</span></span> | <span data-ttu-id="73af2-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-161">Type</span></span> | <span data-ttu-id="73af2-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="73af2-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="73af2-163">arg1</span><span class="sxs-lookup"><span data-stu-id="73af2-163">arg1</span></span> |<span data-ttu-id="73af2-164">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-164">Yes</span></span> |<span data-ttu-id="73af2-165">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-165">int or string</span></span> |<span data-ttu-id="73af2-166">O primeiro valor da comparação de maior que.</span><span class="sxs-lookup"><span data-stu-id="73af2-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="73af2-167">arg2</span><span class="sxs-lookup"><span data-stu-id="73af2-167">arg2</span></span> |<span data-ttu-id="73af2-168">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-168">Yes</span></span> |<span data-ttu-id="73af2-169">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-169">int or string</span></span> |<span data-ttu-id="73af2-170">O segundo valor da comparação de maior que.</span><span class="sxs-lookup"><span data-stu-id="73af2-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="73af2-171">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="73af2-171">Return value</span></span>

<span data-ttu-id="73af2-172">Retorna **True** se o primeiro valor é maior que o segundo valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="73af2-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="73af2-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="73af2-173">Example</span></span>

<span data-ttu-id="73af2-174">O modelo de exemplo verifica se um valor é maior que o outro.</span><span class="sxs-lookup"><span data-stu-id="73af2-174">The example template checks whether the one value is greater than the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="73af2-175">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="73af2-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="73af2-176">Nome</span><span class="sxs-lookup"><span data-stu-id="73af2-176">Name</span></span> | <span data-ttu-id="73af2-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-177">Type</span></span> | <span data-ttu-id="73af2-178">Valor</span><span class="sxs-lookup"><span data-stu-id="73af2-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="73af2-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="73af2-179">checkInts</span></span> | <span data-ttu-id="73af2-180">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-180">Bool</span></span> | <span data-ttu-id="73af2-181">Falso</span><span class="sxs-lookup"><span data-stu-id="73af2-181">False</span></span> |
| <span data-ttu-id="73af2-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="73af2-182">checkStrings</span></span> | <span data-ttu-id="73af2-183">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-183">Bool</span></span> | <span data-ttu-id="73af2-184">True </span><span class="sxs-lookup"><span data-stu-id="73af2-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="73af2-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="73af2-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="73af2-186">Verifica se o primeiro valor é maior que ou igual ao segundo valor.</span><span class="sxs-lookup"><span data-stu-id="73af2-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="73af2-187">parâmetros</span><span class="sxs-lookup"><span data-stu-id="73af2-187">Parameters</span></span>

| <span data-ttu-id="73af2-188">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="73af2-188">Parameter</span></span> | <span data-ttu-id="73af2-189">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="73af2-189">Required</span></span> | <span data-ttu-id="73af2-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-190">Type</span></span> | <span data-ttu-id="73af2-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="73af2-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="73af2-192">arg1</span><span class="sxs-lookup"><span data-stu-id="73af2-192">arg1</span></span> |<span data-ttu-id="73af2-193">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-193">Yes</span></span> |<span data-ttu-id="73af2-194">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-194">int or string</span></span> |<span data-ttu-id="73af2-195">O primeiro valor da comparação de maior que ou igual a.</span><span class="sxs-lookup"><span data-stu-id="73af2-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="73af2-196">arg2</span><span class="sxs-lookup"><span data-stu-id="73af2-196">arg2</span></span> |<span data-ttu-id="73af2-197">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-197">Yes</span></span> |<span data-ttu-id="73af2-198">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-198">int or string</span></span> |<span data-ttu-id="73af2-199">O segundo valor da comparação de maior que ou igual a.</span><span class="sxs-lookup"><span data-stu-id="73af2-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="73af2-200">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="73af2-200">Return value</span></span>

<span data-ttu-id="73af2-201">Retorna **True** se o primeiro valor é maior que ou igual ao segundo valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="73af2-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="73af2-202">Exemplo</span><span class="sxs-lookup"><span data-stu-id="73af2-202">Example</span></span>

<span data-ttu-id="73af2-203">O modelo de exemplo verifica se um valor é maior que ou igual ao outro.</span><span class="sxs-lookup"><span data-stu-id="73af2-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="73af2-204">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="73af2-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="73af2-205">Nome</span><span class="sxs-lookup"><span data-stu-id="73af2-205">Name</span></span> | <span data-ttu-id="73af2-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-206">Type</span></span> | <span data-ttu-id="73af2-207">Valor</span><span class="sxs-lookup"><span data-stu-id="73af2-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="73af2-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="73af2-208">checkInts</span></span> | <span data-ttu-id="73af2-209">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-209">Bool</span></span> | <span data-ttu-id="73af2-210">Falso</span><span class="sxs-lookup"><span data-stu-id="73af2-210">False</span></span> |
| <span data-ttu-id="73af2-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="73af2-211">checkStrings</span></span> | <span data-ttu-id="73af2-212">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-212">Bool</span></span> | <span data-ttu-id="73af2-213">True </span><span class="sxs-lookup"><span data-stu-id="73af2-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="73af2-214">less</span><span class="sxs-lookup"><span data-stu-id="73af2-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="73af2-215">Verifica se o primeiro valor é menor que o segundo valor.</span><span class="sxs-lookup"><span data-stu-id="73af2-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="73af2-216">parâmetros</span><span class="sxs-lookup"><span data-stu-id="73af2-216">Parameters</span></span>

| <span data-ttu-id="73af2-217">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="73af2-217">Parameter</span></span> | <span data-ttu-id="73af2-218">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="73af2-218">Required</span></span> | <span data-ttu-id="73af2-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-219">Type</span></span> | <span data-ttu-id="73af2-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="73af2-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="73af2-221">arg1</span><span class="sxs-lookup"><span data-stu-id="73af2-221">arg1</span></span> |<span data-ttu-id="73af2-222">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-222">Yes</span></span> |<span data-ttu-id="73af2-223">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-223">int or string</span></span> |<span data-ttu-id="73af2-224">O primeiro valor da comparação de menor que.</span><span class="sxs-lookup"><span data-stu-id="73af2-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="73af2-225">arg2</span><span class="sxs-lookup"><span data-stu-id="73af2-225">arg2</span></span> |<span data-ttu-id="73af2-226">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-226">Yes</span></span> |<span data-ttu-id="73af2-227">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-227">int or string</span></span> |<span data-ttu-id="73af2-228">O segundo valor da comparação de menor que.</span><span class="sxs-lookup"><span data-stu-id="73af2-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="73af2-229">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="73af2-229">Return value</span></span>

<span data-ttu-id="73af2-230">Retorna **True** se o primeiro valor é menor que o segundo valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="73af2-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="73af2-231">Exemplo</span><span class="sxs-lookup"><span data-stu-id="73af2-231">Example</span></span>

<span data-ttu-id="73af2-232">O modelo de exemplo verifica se um valor é menor que o outro.</span><span class="sxs-lookup"><span data-stu-id="73af2-232">The example template checks whether the one value is less than the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="73af2-233">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="73af2-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="73af2-234">Nome</span><span class="sxs-lookup"><span data-stu-id="73af2-234">Name</span></span> | <span data-ttu-id="73af2-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-235">Type</span></span> | <span data-ttu-id="73af2-236">Valor</span><span class="sxs-lookup"><span data-stu-id="73af2-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="73af2-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="73af2-237">checkInts</span></span> | <span data-ttu-id="73af2-238">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-238">Bool</span></span> | <span data-ttu-id="73af2-239">True </span><span class="sxs-lookup"><span data-stu-id="73af2-239">True</span></span> |
| <span data-ttu-id="73af2-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="73af2-240">checkStrings</span></span> | <span data-ttu-id="73af2-241">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-241">Bool</span></span> | <span data-ttu-id="73af2-242">Falso</span><span class="sxs-lookup"><span data-stu-id="73af2-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="73af2-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="73af2-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="73af2-244">Verifica se o primeiro valor é menor que ou igual ao segundo valor.</span><span class="sxs-lookup"><span data-stu-id="73af2-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="73af2-245">parâmetros</span><span class="sxs-lookup"><span data-stu-id="73af2-245">Parameters</span></span>

| <span data-ttu-id="73af2-246">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="73af2-246">Parameter</span></span> | <span data-ttu-id="73af2-247">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="73af2-247">Required</span></span> | <span data-ttu-id="73af2-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-248">Type</span></span> | <span data-ttu-id="73af2-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="73af2-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="73af2-250">arg1</span><span class="sxs-lookup"><span data-stu-id="73af2-250">arg1</span></span> |<span data-ttu-id="73af2-251">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-251">Yes</span></span> |<span data-ttu-id="73af2-252">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-252">int or string</span></span> |<span data-ttu-id="73af2-253">O primeiro valor da comparação de menor que ou igual a.</span><span class="sxs-lookup"><span data-stu-id="73af2-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="73af2-254">arg2</span><span class="sxs-lookup"><span data-stu-id="73af2-254">arg2</span></span> |<span data-ttu-id="73af2-255">Sim</span><span class="sxs-lookup"><span data-stu-id="73af2-255">Yes</span></span> |<span data-ttu-id="73af2-256">int ou string</span><span class="sxs-lookup"><span data-stu-id="73af2-256">int or string</span></span> |<span data-ttu-id="73af2-257">O segundo valor da comparação de menor que ou igual a.</span><span class="sxs-lookup"><span data-stu-id="73af2-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="73af2-258">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="73af2-258">Return value</span></span>

<span data-ttu-id="73af2-259">Retorna **True** se o primeiro valor é menor que ou igual ao segundo valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="73af2-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="73af2-260">Exemplo</span><span class="sxs-lookup"><span data-stu-id="73af2-260">Example</span></span>

<span data-ttu-id="73af2-261">O modelo de exemplo verifica se um valor é menor que ou igual ao outro.</span><span class="sxs-lookup"><span data-stu-id="73af2-261">The example template checks whether the one value is less than or equal to the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="73af2-262">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="73af2-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="73af2-263">Nome</span><span class="sxs-lookup"><span data-stu-id="73af2-263">Name</span></span> | <span data-ttu-id="73af2-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="73af2-264">Type</span></span> | <span data-ttu-id="73af2-265">Valor</span><span class="sxs-lookup"><span data-stu-id="73af2-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="73af2-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="73af2-266">checkInts</span></span> | <span data-ttu-id="73af2-267">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-267">Bool</span></span> | <span data-ttu-id="73af2-268">True </span><span class="sxs-lookup"><span data-stu-id="73af2-268">True</span></span> |
| <span data-ttu-id="73af2-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="73af2-269">checkStrings</span></span> | <span data-ttu-id="73af2-270">Bool</span><span class="sxs-lookup"><span data-stu-id="73af2-270">Bool</span></span> | <span data-ttu-id="73af2-271">Falso</span><span class="sxs-lookup"><span data-stu-id="73af2-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="73af2-272">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73af2-272">Next steps</span></span>
* <span data-ttu-id="73af2-273">Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73af2-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="73af2-274">Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73af2-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="73af2-275">Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="73af2-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="73af2-276">Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="73af2-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

