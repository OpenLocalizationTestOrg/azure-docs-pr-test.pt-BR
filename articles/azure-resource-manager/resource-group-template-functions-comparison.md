---
title: "funções de modelo do Gerenciador de recursos aaaAzure - comparação | Microsoft Docs"
description: "Descreve Olá toouse de funções em valores de toocompare modelo do Azure Resource Manager."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="ddda2-103">Funções de comparação para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ddda2-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="ddda2-104">O Resource Manager fornece várias funções para fazer comparações em seus modelos.</span><span class="sxs-lookup"><span data-stu-id="ddda2-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="ddda2-105">equals</span><span class="sxs-lookup"><span data-stu-id="ddda2-105">equals</span></span>](#equals)
* [<span data-ttu-id="ddda2-106">greater</span><span class="sxs-lookup"><span data-stu-id="ddda2-106">greater</span></span>](#greater)
* [<span data-ttu-id="ddda2-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="ddda2-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="ddda2-108">less</span><span class="sxs-lookup"><span data-stu-id="ddda2-108">less</span></span>](#less)
* [<span data-ttu-id="ddda2-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="ddda2-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="ddda2-110">equals</span><span class="sxs-lookup"><span data-stu-id="ddda2-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="ddda2-111">Verifica se dois valores são iguais entre si.</span><span class="sxs-lookup"><span data-stu-id="ddda2-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="ddda2-112">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ddda2-112">Parameters</span></span>

| <span data-ttu-id="ddda2-113">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ddda2-113">Parameter</span></span> | <span data-ttu-id="ddda2-114">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ddda2-114">Required</span></span> | <span data-ttu-id="ddda2-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-115">Type</span></span> | <span data-ttu-id="ddda2-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="ddda2-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ddda2-117">arg1</span><span class="sxs-lookup"><span data-stu-id="ddda2-117">arg1</span></span> |<span data-ttu-id="ddda2-118">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-118">Yes</span></span> |<span data-ttu-id="ddda2-119">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="ddda2-119">int, string, array, or object</span></span> |<span data-ttu-id="ddda2-120">Olá primeiro toocheck de valor de igualdade.</span><span class="sxs-lookup"><span data-stu-id="ddda2-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="ddda2-121">arg2</span><span class="sxs-lookup"><span data-stu-id="ddda2-121">arg2</span></span> |<span data-ttu-id="ddda2-122">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-122">Yes</span></span> |<span data-ttu-id="ddda2-123">int, string, array ou object</span><span class="sxs-lookup"><span data-stu-id="ddda2-123">int, string, array, or object</span></span> |<span data-ttu-id="ddda2-124">Olá toocheck segundo do valor de igualdade.</span><span class="sxs-lookup"><span data-stu-id="ddda2-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ddda2-125">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="ddda2-125">Return value</span></span>

<span data-ttu-id="ddda2-126">Retorna **True** se valores hello forem iguais; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="ddda2-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="ddda2-127">Comentários</span><span class="sxs-lookup"><span data-stu-id="ddda2-127">Remarks</span></span>

<span data-ttu-id="ddda2-128">Olá igual a função é geralmente usada com hello `condition` elemento tootest se um recurso é implantado.</span><span class="sxs-lookup"><span data-stu-id="ddda2-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="ddda2-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ddda2-129">Example</span></span>

<span data-ttu-id="ddda2-130">modelo de exemplo Hello verifica os diferentes tipos de valores para igualdade.</span><span class="sxs-lookup"><span data-stu-id="ddda2-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="ddda2-131">Todos os valores padrão de saudação retornarem True.</span><span class="sxs-lookup"><span data-stu-id="ddda2-131">All hello default values return True.</span></span>

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

<span data-ttu-id="ddda2-132">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="ddda2-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ddda2-133">Nome</span><span class="sxs-lookup"><span data-stu-id="ddda2-133">Name</span></span> | <span data-ttu-id="ddda2-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-134">Type</span></span> | <span data-ttu-id="ddda2-135">Valor</span><span class="sxs-lookup"><span data-stu-id="ddda2-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ddda2-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="ddda2-136">checkInts</span></span> | <span data-ttu-id="ddda2-137">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-137">Bool</span></span> | <span data-ttu-id="ddda2-138">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-138">True</span></span> |
| <span data-ttu-id="ddda2-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ddda2-139">checkStrings</span></span> | <span data-ttu-id="ddda2-140">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-140">Bool</span></span> | <span data-ttu-id="ddda2-141">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-141">True</span></span> |
| <span data-ttu-id="ddda2-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="ddda2-142">checkArrays</span></span> | <span data-ttu-id="ddda2-143">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-143">Bool</span></span> | <span data-ttu-id="ddda2-144">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-144">True</span></span> |
| <span data-ttu-id="ddda2-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="ddda2-145">checkObjects</span></span> | <span data-ttu-id="ddda2-146">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-146">Bool</span></span> | <span data-ttu-id="ddda2-147">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ddda2-147">True</span></span> |


<span data-ttu-id="ddda2-148">Olá exemplo a seguir usa [não](resource-group-template-functions-logical.md#not) com **é igual a**.</span><span class="sxs-lookup"><span data-stu-id="ddda2-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="ddda2-149">saída Olá Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="ddda2-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ddda2-150">Nome</span><span class="sxs-lookup"><span data-stu-id="ddda2-150">Name</span></span> | <span data-ttu-id="ddda2-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-151">Type</span></span> | <span data-ttu-id="ddda2-152">Valor</span><span class="sxs-lookup"><span data-stu-id="ddda2-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ddda2-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="ddda2-153">checkNotEquals</span></span> | <span data-ttu-id="ddda2-154">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-154">Bool</span></span> | <span data-ttu-id="ddda2-155">True</span><span class="sxs-lookup"><span data-stu-id="ddda2-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="ddda2-156">greater</span><span class="sxs-lookup"><span data-stu-id="ddda2-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="ddda2-157">Verifica se o primeiro valor de saudação é maior que o valor de segundo hello.</span><span class="sxs-lookup"><span data-stu-id="ddda2-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ddda2-158">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ddda2-158">Parameters</span></span>

| <span data-ttu-id="ddda2-159">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ddda2-159">Parameter</span></span> | <span data-ttu-id="ddda2-160">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ddda2-160">Required</span></span> | <span data-ttu-id="ddda2-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-161">Type</span></span> | <span data-ttu-id="ddda2-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="ddda2-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ddda2-163">arg1</span><span class="sxs-lookup"><span data-stu-id="ddda2-163">arg1</span></span> |<span data-ttu-id="ddda2-164">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-164">Yes</span></span> |<span data-ttu-id="ddda2-165">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-165">int or string</span></span> |<span data-ttu-id="ddda2-166">primeiro valor de comparação maior Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="ddda2-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="ddda2-167">arg2</span><span class="sxs-lookup"><span data-stu-id="ddda2-167">arg2</span></span> |<span data-ttu-id="ddda2-168">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-168">Yes</span></span> |<span data-ttu-id="ddda2-169">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-169">int or string</span></span> |<span data-ttu-id="ddda2-170">o segundo valor de comparação maior Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="ddda2-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ddda2-171">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="ddda2-171">Return value</span></span>

<span data-ttu-id="ddda2-172">Retorna **True** se Olá primeiro valor é maior que o valor de segundo Olá; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="ddda2-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ddda2-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ddda2-173">Example</span></span>

<span data-ttu-id="ddda2-174">modelo de exemplo Hello verifica se um valor de saudação é maior do que outros hello.</span><span class="sxs-lookup"><span data-stu-id="ddda2-174">hello example template checks whether hello one value is greater than hello other.</span></span>

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

<span data-ttu-id="ddda2-175">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="ddda2-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ddda2-176">Nome</span><span class="sxs-lookup"><span data-stu-id="ddda2-176">Name</span></span> | <span data-ttu-id="ddda2-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-177">Type</span></span> | <span data-ttu-id="ddda2-178">Valor</span><span class="sxs-lookup"><span data-stu-id="ddda2-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ddda2-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="ddda2-179">checkInts</span></span> | <span data-ttu-id="ddda2-180">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-180">Bool</span></span> | <span data-ttu-id="ddda2-181">Falso</span><span class="sxs-lookup"><span data-stu-id="ddda2-181">False</span></span> |
| <span data-ttu-id="ddda2-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ddda2-182">checkStrings</span></span> | <span data-ttu-id="ddda2-183">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-183">Bool</span></span> | <span data-ttu-id="ddda2-184">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="ddda2-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="ddda2-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="ddda2-186">Verifica se o primeiro valor de saudação é maior que ou igual toohello segundo valor.</span><span class="sxs-lookup"><span data-stu-id="ddda2-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ddda2-187">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ddda2-187">Parameters</span></span>

| <span data-ttu-id="ddda2-188">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ddda2-188">Parameter</span></span> | <span data-ttu-id="ddda2-189">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ddda2-189">Required</span></span> | <span data-ttu-id="ddda2-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-190">Type</span></span> | <span data-ttu-id="ddda2-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="ddda2-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ddda2-192">arg1</span><span class="sxs-lookup"><span data-stu-id="ddda2-192">arg1</span></span> |<span data-ttu-id="ddda2-193">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-193">Yes</span></span> |<span data-ttu-id="ddda2-194">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-194">int or string</span></span> |<span data-ttu-id="ddda2-195">primeiro valor para comparação de maior ou igual Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="ddda2-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="ddda2-196">arg2</span><span class="sxs-lookup"><span data-stu-id="ddda2-196">arg2</span></span> |<span data-ttu-id="ddda2-197">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-197">Yes</span></span> |<span data-ttu-id="ddda2-198">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-198">int or string</span></span> |<span data-ttu-id="ddda2-199">o segundo valor para comparação de maior ou igual Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="ddda2-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ddda2-200">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="ddda2-200">Return value</span></span>

<span data-ttu-id="ddda2-201">Retorna **True** se Olá primeiro valor for maior que ou igual toohello segundo; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="ddda2-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ddda2-202">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ddda2-202">Example</span></span>

<span data-ttu-id="ddda2-203">modelo de exemplo Hello verifica se um valor de saudação é maior ou igual toohello outros.</span><span class="sxs-lookup"><span data-stu-id="ddda2-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

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

<span data-ttu-id="ddda2-204">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="ddda2-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ddda2-205">Nome</span><span class="sxs-lookup"><span data-stu-id="ddda2-205">Name</span></span> | <span data-ttu-id="ddda2-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-206">Type</span></span> | <span data-ttu-id="ddda2-207">Valor</span><span class="sxs-lookup"><span data-stu-id="ddda2-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ddda2-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="ddda2-208">checkInts</span></span> | <span data-ttu-id="ddda2-209">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-209">Bool</span></span> | <span data-ttu-id="ddda2-210">Falso</span><span class="sxs-lookup"><span data-stu-id="ddda2-210">False</span></span> |
| <span data-ttu-id="ddda2-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ddda2-211">checkStrings</span></span> | <span data-ttu-id="ddda2-212">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-212">Bool</span></span> | <span data-ttu-id="ddda2-213">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="ddda2-214">less</span><span class="sxs-lookup"><span data-stu-id="ddda2-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="ddda2-215">Verifica se Olá primeiro valor é menor que Olá segundo valor.</span><span class="sxs-lookup"><span data-stu-id="ddda2-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ddda2-216">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ddda2-216">Parameters</span></span>

| <span data-ttu-id="ddda2-217">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ddda2-217">Parameter</span></span> | <span data-ttu-id="ddda2-218">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ddda2-218">Required</span></span> | <span data-ttu-id="ddda2-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-219">Type</span></span> | <span data-ttu-id="ddda2-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="ddda2-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ddda2-221">arg1</span><span class="sxs-lookup"><span data-stu-id="ddda2-221">arg1</span></span> |<span data-ttu-id="ddda2-222">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-222">Yes</span></span> |<span data-ttu-id="ddda2-223">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-223">int or string</span></span> |<span data-ttu-id="ddda2-224">primeiro valor de saudação menos comparação Hello.</span><span class="sxs-lookup"><span data-stu-id="ddda2-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="ddda2-225">arg2</span><span class="sxs-lookup"><span data-stu-id="ddda2-225">arg2</span></span> |<span data-ttu-id="ddda2-226">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-226">Yes</span></span> |<span data-ttu-id="ddda2-227">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-227">int or string</span></span> |<span data-ttu-id="ddda2-228">o segundo valor para Olá menos comparação Hello.</span><span class="sxs-lookup"><span data-stu-id="ddda2-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ddda2-229">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="ddda2-229">Return value</span></span>

<span data-ttu-id="ddda2-230">Retorna **True** se Olá primeiro valor é menor que Olá segundo valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="ddda2-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ddda2-231">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ddda2-231">Example</span></span>

<span data-ttu-id="ddda2-232">modelo de exemplo Hello verifica se um valor de saudação é menor que Olá outros.</span><span class="sxs-lookup"><span data-stu-id="ddda2-232">hello example template checks whether hello one value is less than hello other.</span></span>

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

<span data-ttu-id="ddda2-233">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="ddda2-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ddda2-234">Nome</span><span class="sxs-lookup"><span data-stu-id="ddda2-234">Name</span></span> | <span data-ttu-id="ddda2-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-235">Type</span></span> | <span data-ttu-id="ddda2-236">Valor</span><span class="sxs-lookup"><span data-stu-id="ddda2-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ddda2-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="ddda2-237">checkInts</span></span> | <span data-ttu-id="ddda2-238">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-238">Bool</span></span> | <span data-ttu-id="ddda2-239">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-239">True</span></span> |
| <span data-ttu-id="ddda2-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ddda2-240">checkStrings</span></span> | <span data-ttu-id="ddda2-241">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-241">Bool</span></span> | <span data-ttu-id="ddda2-242">Falso</span><span class="sxs-lookup"><span data-stu-id="ddda2-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="ddda2-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="ddda2-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="ddda2-244">Verifica se o primeiro valor de saudação é menor ou igual toohello segundo valor.</span><span class="sxs-lookup"><span data-stu-id="ddda2-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ddda2-245">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ddda2-245">Parameters</span></span>

| <span data-ttu-id="ddda2-246">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ddda2-246">Parameter</span></span> | <span data-ttu-id="ddda2-247">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ddda2-247">Required</span></span> | <span data-ttu-id="ddda2-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-248">Type</span></span> | <span data-ttu-id="ddda2-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="ddda2-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ddda2-250">arg1</span><span class="sxs-lookup"><span data-stu-id="ddda2-250">arg1</span></span> |<span data-ttu-id="ddda2-251">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-251">Yes</span></span> |<span data-ttu-id="ddda2-252">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-252">int or string</span></span> |<span data-ttu-id="ddda2-253">Olá Olá primeiro valor menor ou igual a comparação.</span><span class="sxs-lookup"><span data-stu-id="ddda2-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="ddda2-254">arg2</span><span class="sxs-lookup"><span data-stu-id="ddda2-254">arg2</span></span> |<span data-ttu-id="ddda2-255">Sim</span><span class="sxs-lookup"><span data-stu-id="ddda2-255">Yes</span></span> |<span data-ttu-id="ddda2-256">int ou string</span><span class="sxs-lookup"><span data-stu-id="ddda2-256">int or string</span></span> |<span data-ttu-id="ddda2-257">Olá Olá segundo valor menor ou igual a comparação.</span><span class="sxs-lookup"><span data-stu-id="ddda2-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ddda2-258">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="ddda2-258">Return value</span></span>

<span data-ttu-id="ddda2-259">Retorna **True** se Olá primeiro valor é menor ou igual toohello segundo valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="ddda2-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ddda2-260">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ddda2-260">Example</span></span>

<span data-ttu-id="ddda2-261">Olá modelo de exemplo verifica se um valor de saudação é menor ou igual toohello outros.</span><span class="sxs-lookup"><span data-stu-id="ddda2-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

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

<span data-ttu-id="ddda2-262">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="ddda2-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ddda2-263">Nome</span><span class="sxs-lookup"><span data-stu-id="ddda2-263">Name</span></span> | <span data-ttu-id="ddda2-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="ddda2-264">Type</span></span> | <span data-ttu-id="ddda2-265">Valor</span><span class="sxs-lookup"><span data-stu-id="ddda2-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ddda2-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="ddda2-266">checkInts</span></span> | <span data-ttu-id="ddda2-267">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-267">Bool</span></span> | <span data-ttu-id="ddda2-268">True </span><span class="sxs-lookup"><span data-stu-id="ddda2-268">True</span></span> |
| <span data-ttu-id="ddda2-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ddda2-269">checkStrings</span></span> | <span data-ttu-id="ddda2-270">Bool</span><span class="sxs-lookup"><span data-stu-id="ddda2-270">Bool</span></span> | <span data-ttu-id="ddda2-271">Falso</span><span class="sxs-lookup"><span data-stu-id="ddda2-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="ddda2-272">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ddda2-272">Next steps</span></span>
* <span data-ttu-id="ddda2-273">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ddda2-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ddda2-274">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ddda2-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="ddda2-275">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ddda2-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="ddda2-276">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ddda2-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

