---
title: "Funções do modelo do Azure Resource Manager – cadeia de caracteres | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Azure Resource Manager para trabalhar com cadeias de caracteres."
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="1a45f-103">Funções de cadeia de caracteres para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a45f-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="1a45f-104">O Gerenciador de Recursos fornece as seguintes funções para trabalhar com cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="1a45f-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="1a45f-105">base64</span><span class="sxs-lookup"><span data-stu-id="1a45f-105">base64</span></span>](#base64)
* [<span data-ttu-id="1a45f-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="1a45f-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="1a45f-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="1a45f-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="1a45f-108">concat</span><span class="sxs-lookup"><span data-stu-id="1a45f-108">concat</span></span>](#concat)
* [<span data-ttu-id="1a45f-109">contains</span><span class="sxs-lookup"><span data-stu-id="1a45f-109">contains</span></span>](#contains)
* [<span data-ttu-id="1a45f-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="1a45f-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="1a45f-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="1a45f-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="1a45f-112">empty</span><span class="sxs-lookup"><span data-stu-id="1a45f-112">empty</span></span>](#empty)
* [<span data-ttu-id="1a45f-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="1a45f-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="1a45f-114">first</span><span class="sxs-lookup"><span data-stu-id="1a45f-114">first</span></span>](#first)
* [<span data-ttu-id="1a45f-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="1a45f-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="1a45f-116">last</span><span class="sxs-lookup"><span data-stu-id="1a45f-116">last</span></span>](#last)
* [<span data-ttu-id="1a45f-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="1a45f-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="1a45f-118">length</span><span class="sxs-lookup"><span data-stu-id="1a45f-118">length</span></span>](#length)
* [<span data-ttu-id="1a45f-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="1a45f-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="1a45f-120">substitui</span><span class="sxs-lookup"><span data-stu-id="1a45f-120">replace</span></span>](#replace)
* [<span data-ttu-id="1a45f-121">skip</span><span class="sxs-lookup"><span data-stu-id="1a45f-121">skip</span></span>](#skip)
* [<span data-ttu-id="1a45f-122">split</span><span class="sxs-lookup"><span data-stu-id="1a45f-122">split</span></span>](#split)
* [<span data-ttu-id="1a45f-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="1a45f-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="1a45f-124">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-124">string</span></span>](#string)
* [<span data-ttu-id="1a45f-125">substring</span><span class="sxs-lookup"><span data-stu-id="1a45f-125">substring</span></span>](#substring)
* [<span data-ttu-id="1a45f-126">take</span><span class="sxs-lookup"><span data-stu-id="1a45f-126">take</span></span>](#take)
* [<span data-ttu-id="1a45f-127">toLower</span><span class="sxs-lookup"><span data-stu-id="1a45f-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="1a45f-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="1a45f-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="1a45f-129">cortar</span><span class="sxs-lookup"><span data-stu-id="1a45f-129">trim</span></span>](#trim)
* [<span data-ttu-id="1a45f-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="1a45f-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="1a45f-131">uri</span><span class="sxs-lookup"><span data-stu-id="1a45f-131">uri</span></span>](#uri)
* [<span data-ttu-id="1a45f-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="1a45f-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="1a45f-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="1a45f-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="1a45f-134">base64</span><span class="sxs-lookup"><span data-stu-id="1a45f-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="1a45f-135">Retorna a representação base64 da cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-136">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-136">Parameters</span></span>

| <span data-ttu-id="1a45f-137">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-137">Parameter</span></span> | <span data-ttu-id="1a45f-138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-138">Required</span></span> | <span data-ttu-id="1a45f-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-139">Type</span></span> | <span data-ttu-id="1a45f-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-141">inputString</span><span class="sxs-lookup"><span data-stu-id="1a45f-141">inputString</span></span> |<span data-ttu-id="1a45f-142">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-142">Yes</span></span> |<span data-ttu-id="1a45f-143">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-143">string</span></span> |<span data-ttu-id="1a45f-144">O valor a retornar como uma representação base64.</span><span class="sxs-lookup"><span data-stu-id="1a45f-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-145">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-145">Return value</span></span>

<span data-ttu-id="1a45f-146">Uma cadeia de caracteres que contém a representação base64.</span><span class="sxs-lookup"><span data-stu-id="1a45f-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-147">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-147">Examples</span></span>

<span data-ttu-id="1a45f-148">O exemplo a seguir mostra como usar a função base64.</span><span class="sxs-lookup"><span data-stu-id="1a45f-148">The following example shows how to use the base64 function.</span></span>

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

<span data-ttu-id="1a45f-149">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-150">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-150">Name</span></span> | <span data-ttu-id="1a45f-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-151">Type</span></span> | <span data-ttu-id="1a45f-152">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="1a45f-153">base64Output</span></span> | <span data-ttu-id="1a45f-154">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-154">String</span></span> | <span data-ttu-id="1a45f-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="1a45f-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="1a45f-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-156">toStringOutput</span></span> | <span data-ttu-id="1a45f-157">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-157">String</span></span> | <span data-ttu-id="1a45f-158">um, dois, três</span><span class="sxs-lookup"><span data-stu-id="1a45f-158">one, two, three</span></span> |
| <span data-ttu-id="1a45f-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-159">toJsonOutput</span></span> | <span data-ttu-id="1a45f-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="1a45f-160">Object</span></span> | <span data-ttu-id="1a45f-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="1a45f-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="1a45f-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="1a45f-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="1a45f-163">Converte uma representação base64 em um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="1a45f-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-164">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-164">Parameters</span></span>

| <span data-ttu-id="1a45f-165">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-165">Parameter</span></span> | <span data-ttu-id="1a45f-166">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-166">Required</span></span> | <span data-ttu-id="1a45f-167">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-167">Type</span></span> | <span data-ttu-id="1a45f-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="1a45f-169">base64Value</span></span> |<span data-ttu-id="1a45f-170">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-170">Yes</span></span> |<span data-ttu-id="1a45f-171">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-171">string</span></span> |<span data-ttu-id="1a45f-172">A representação base64 a ser convertida em um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="1a45f-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-173">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-173">Return value</span></span>

<span data-ttu-id="1a45f-174">Um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="1a45f-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-175">Examples</span></span>

<span data-ttu-id="1a45f-176">O seguinte exemplo usa a função base64ToJson para converter um valor base64:</span><span class="sxs-lookup"><span data-stu-id="1a45f-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

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

<span data-ttu-id="1a45f-177">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-178">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-178">Name</span></span> | <span data-ttu-id="1a45f-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-179">Type</span></span> | <span data-ttu-id="1a45f-180">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="1a45f-181">base64Output</span></span> | <span data-ttu-id="1a45f-182">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-182">String</span></span> | <span data-ttu-id="1a45f-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="1a45f-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="1a45f-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-184">toStringOutput</span></span> | <span data-ttu-id="1a45f-185">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-185">String</span></span> | <span data-ttu-id="1a45f-186">um, dois, três</span><span class="sxs-lookup"><span data-stu-id="1a45f-186">one, two, three</span></span> |
| <span data-ttu-id="1a45f-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-187">toJsonOutput</span></span> | <span data-ttu-id="1a45f-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="1a45f-188">Object</span></span> | <span data-ttu-id="1a45f-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="1a45f-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="1a45f-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="1a45f-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="1a45f-191">Converte uma representação base64 em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-192">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-192">Parameters</span></span>

| <span data-ttu-id="1a45f-193">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-193">Parameter</span></span> | <span data-ttu-id="1a45f-194">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-194">Required</span></span> | <span data-ttu-id="1a45f-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-195">Type</span></span> | <span data-ttu-id="1a45f-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="1a45f-197">base64Value</span></span> |<span data-ttu-id="1a45f-198">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-198">Yes</span></span> |<span data-ttu-id="1a45f-199">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-199">string</span></span> |<span data-ttu-id="1a45f-200">A representação base64 a ser convertida em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-201">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-201">Return value</span></span>

<span data-ttu-id="1a45f-202">Uma cadeia de caracteres do valor base64 convertido.</span><span class="sxs-lookup"><span data-stu-id="1a45f-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-203">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-203">Examples</span></span>

<span data-ttu-id="1a45f-204">O seguinte exemplo usa a função base64ToString para converter um valor base64:</span><span class="sxs-lookup"><span data-stu-id="1a45f-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

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

<span data-ttu-id="1a45f-205">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-206">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-206">Name</span></span> | <span data-ttu-id="1a45f-207">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-207">Type</span></span> | <span data-ttu-id="1a45f-208">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="1a45f-209">base64Output</span></span> | <span data-ttu-id="1a45f-210">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-210">String</span></span> | <span data-ttu-id="1a45f-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="1a45f-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="1a45f-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-212">toStringOutput</span></span> | <span data-ttu-id="1a45f-213">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-213">String</span></span> | <span data-ttu-id="1a45f-214">um, dois, três</span><span class="sxs-lookup"><span data-stu-id="1a45f-214">one, two, three</span></span> |
| <span data-ttu-id="1a45f-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-215">toJsonOutput</span></span> | <span data-ttu-id="1a45f-216">Objeto</span><span class="sxs-lookup"><span data-stu-id="1a45f-216">Object</span></span> | <span data-ttu-id="1a45f-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="1a45f-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="1a45f-218">concat</span><span class="sxs-lookup"><span data-stu-id="1a45f-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="1a45f-219">Combina vários valores de cadeia de caracteres e retorna a cadeia de caracteres concatenada ou combina várias matrizes e retorna a matriz concatenada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-220">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-220">Parameters</span></span>

| <span data-ttu-id="1a45f-221">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-221">Parameter</span></span> | <span data-ttu-id="1a45f-222">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-222">Required</span></span> | <span data-ttu-id="1a45f-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-223">Type</span></span> | <span data-ttu-id="1a45f-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-225">arg1</span><span class="sxs-lookup"><span data-stu-id="1a45f-225">arg1</span></span> |<span data-ttu-id="1a45f-226">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-226">Yes</span></span> |<span data-ttu-id="1a45f-227">cadeia de caracteres ou matriz</span><span class="sxs-lookup"><span data-stu-id="1a45f-227">string or array</span></span> |<span data-ttu-id="1a45f-228">O primeiro valor de concatenação.</span><span class="sxs-lookup"><span data-stu-id="1a45f-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="1a45f-229">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="1a45f-229">additional arguments</span></span> |<span data-ttu-id="1a45f-230">Não</span><span class="sxs-lookup"><span data-stu-id="1a45f-230">No</span></span> |<span data-ttu-id="1a45f-231">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-231">string</span></span> |<span data-ttu-id="1a45f-232">Valores adicionais em ordem sequencial para concatenação.</span><span class="sxs-lookup"><span data-stu-id="1a45f-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-233">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-233">Return value</span></span>
<span data-ttu-id="1a45f-234">Uma cadeia de caracteres ou matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-235">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-235">Examples</span></span>

<span data-ttu-id="1a45f-236">O exemplo a seguir mostra como combinar dois valores de cadeia de caracteres e retornar uma cadeia de caracteres concatenada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="1a45f-237">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-238">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-238">Name</span></span> | <span data-ttu-id="1a45f-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-239">Type</span></span> | <span data-ttu-id="1a45f-240">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-241">concatOutput</span></span> | <span data-ttu-id="1a45f-242">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-242">String</span></span> | <span data-ttu-id="1a45f-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="1a45f-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="1a45f-244">O próximo exemplo mostra como combinar duas matrizes.</span><span class="sxs-lookup"><span data-stu-id="1a45f-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="1a45f-245">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-246">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-246">Name</span></span> | <span data-ttu-id="1a45f-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-247">Type</span></span> | <span data-ttu-id="1a45f-248">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-249">retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-249">return</span></span> | <span data-ttu-id="1a45f-250">Matriz</span><span class="sxs-lookup"><span data-stu-id="1a45f-250">Array</span></span> | <span data-ttu-id="1a45f-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="1a45f-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="1a45f-252">contains</span><span class="sxs-lookup"><span data-stu-id="1a45f-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="1a45f-253">Verifica se uma matriz contém um valor, um objeto contém uma chave ou uma cadeia de caracteres contém uma subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-254">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-254">Parameters</span></span>

| <span data-ttu-id="1a45f-255">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-255">Parameter</span></span> | <span data-ttu-id="1a45f-256">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-256">Required</span></span> | <span data-ttu-id="1a45f-257">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-257">Type</span></span> | <span data-ttu-id="1a45f-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-259">contêiner</span><span class="sxs-lookup"><span data-stu-id="1a45f-259">container</span></span> |<span data-ttu-id="1a45f-260">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-260">Yes</span></span> |<span data-ttu-id="1a45f-261">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-261">array, object, or string</span></span> |<span data-ttu-id="1a45f-262">O valor que contém o valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="1a45f-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="1a45f-263">itemToFind</span></span> |<span data-ttu-id="1a45f-264">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-264">Yes</span></span> |<span data-ttu-id="1a45f-265">string ou int</span><span class="sxs-lookup"><span data-stu-id="1a45f-265">string or int</span></span> |<span data-ttu-id="1a45f-266">O valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-267">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-267">Return value</span></span>

<span data-ttu-id="1a45f-268">**True** se o item for encontrado; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="1a45f-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-269">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-269">Examples</span></span>

<span data-ttu-id="1a45f-270">O seguinte exemplo mostra como usar contains com tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="1a45f-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="1a45f-271">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-272">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-272">Name</span></span> | <span data-ttu-id="1a45f-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-273">Type</span></span> | <span data-ttu-id="1a45f-274">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-275">stringTrue</span></span> | <span data-ttu-id="1a45f-276">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-276">Bool</span></span> | <span data-ttu-id="1a45f-277">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-277">True</span></span> |
| <span data-ttu-id="1a45f-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-278">stringFalse</span></span> | <span data-ttu-id="1a45f-279">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-279">Bool</span></span> | <span data-ttu-id="1a45f-280">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-280">False</span></span> |
| <span data-ttu-id="1a45f-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-281">objectTrue</span></span> | <span data-ttu-id="1a45f-282">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-282">Bool</span></span> | <span data-ttu-id="1a45f-283">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-283">True</span></span> |
| <span data-ttu-id="1a45f-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-284">objectFalse</span></span> | <span data-ttu-id="1a45f-285">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-285">Bool</span></span> | <span data-ttu-id="1a45f-286">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-286">False</span></span> |
| <span data-ttu-id="1a45f-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-287">arrayTrue</span></span> | <span data-ttu-id="1a45f-288">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-288">Bool</span></span> | <span data-ttu-id="1a45f-289">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-289">True</span></span> |
| <span data-ttu-id="1a45f-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-290">arrayFalse</span></span> | <span data-ttu-id="1a45f-291">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-291">Bool</span></span> | <span data-ttu-id="1a45f-292">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="1a45f-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="1a45f-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="1a45f-294">Converte um valor em um URI de dados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-295">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-295">Parameters</span></span>

| <span data-ttu-id="1a45f-296">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-296">Parameter</span></span> | <span data-ttu-id="1a45f-297">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-297">Required</span></span> | <span data-ttu-id="1a45f-298">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-298">Type</span></span> | <span data-ttu-id="1a45f-299">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="1a45f-300">stringToConvert</span></span> |<span data-ttu-id="1a45f-301">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-301">Yes</span></span> |<span data-ttu-id="1a45f-302">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-302">string</span></span> |<span data-ttu-id="1a45f-303">O valor a ser convertido em um URI de dados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-304">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-304">Return value</span></span>

<span data-ttu-id="1a45f-305">Uma cadeia de caracteres formatada como um URI de dados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-306">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-306">Examples</span></span>

<span data-ttu-id="1a45f-307">O seguinte exemplo converte um valor em um URI de dados e um URI de dados em uma cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="1a45f-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="1a45f-308">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-309">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-309">Name</span></span> | <span data-ttu-id="1a45f-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-310">Type</span></span> | <span data-ttu-id="1a45f-311">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-312">dataUriOutput</span></span> | <span data-ttu-id="1a45f-313">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-313">String</span></span> | <span data-ttu-id="1a45f-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="1a45f-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="1a45f-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-315">toStringOutput</span></span> | <span data-ttu-id="1a45f-316">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-316">String</span></span> | <span data-ttu-id="1a45f-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="1a45f-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="1a45f-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="1a45f-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="1a45f-319">Converte um valor formatado como um URI de dados em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-320">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-320">Parameters</span></span>

| <span data-ttu-id="1a45f-321">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-321">Parameter</span></span> | <span data-ttu-id="1a45f-322">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-322">Required</span></span> | <span data-ttu-id="1a45f-323">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-323">Type</span></span> | <span data-ttu-id="1a45f-324">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="1a45f-325">dataUriToConvert</span></span> |<span data-ttu-id="1a45f-326">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-326">Yes</span></span> |<span data-ttu-id="1a45f-327">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-327">string</span></span> |<span data-ttu-id="1a45f-328">Os valor de URI de dados a ser convertido.</span><span class="sxs-lookup"><span data-stu-id="1a45f-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-329">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-329">Return value</span></span>

<span data-ttu-id="1a45f-330">Uma cadeia de caracteres que contém o valor convertido.</span><span class="sxs-lookup"><span data-stu-id="1a45f-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-331">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-331">Examples</span></span>

<span data-ttu-id="1a45f-332">O seguinte exemplo converte um valor em um URI de dados e um URI de dados em uma cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="1a45f-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="1a45f-333">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-334">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-334">Name</span></span> | <span data-ttu-id="1a45f-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-335">Type</span></span> | <span data-ttu-id="1a45f-336">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-337">dataUriOutput</span></span> | <span data-ttu-id="1a45f-338">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-338">String</span></span> | <span data-ttu-id="1a45f-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="1a45f-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="1a45f-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-340">toStringOutput</span></span> | <span data-ttu-id="1a45f-341">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-341">String</span></span> | <span data-ttu-id="1a45f-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="1a45f-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="1a45f-343">empty</span><span class="sxs-lookup"><span data-stu-id="1a45f-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="1a45f-344">Determina se uma matriz, objeto ou uma cadeia de caracteres está vazio.</span><span class="sxs-lookup"><span data-stu-id="1a45f-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-345">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-345">Parameters</span></span>

| <span data-ttu-id="1a45f-346">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-346">Parameter</span></span> | <span data-ttu-id="1a45f-347">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-347">Required</span></span> | <span data-ttu-id="1a45f-348">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-348">Type</span></span> | <span data-ttu-id="1a45f-349">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="1a45f-350">itemToTest</span></span> |<span data-ttu-id="1a45f-351">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-351">Yes</span></span> |<span data-ttu-id="1a45f-352">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-352">array, object, or string</span></span> |<span data-ttu-id="1a45f-353">O valor a ser verificado, caso esteja vazio.</span><span class="sxs-lookup"><span data-stu-id="1a45f-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-354">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-354">Return value</span></span>

<span data-ttu-id="1a45f-355">Retorna **True** se o valor é vazio; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="1a45f-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-356">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-356">Examples</span></span>

<span data-ttu-id="1a45f-357">O exemplo a seguir verifica se uma matriz, um objeto e uma cadeia de caracteres estão vazios.</span><span class="sxs-lookup"><span data-stu-id="1a45f-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="1a45f-358">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-359">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-359">Name</span></span> | <span data-ttu-id="1a45f-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-360">Type</span></span> | <span data-ttu-id="1a45f-361">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="1a45f-362">arrayEmpty</span></span> | <span data-ttu-id="1a45f-363">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-363">Bool</span></span> | <span data-ttu-id="1a45f-364">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-364">True</span></span> |
| <span data-ttu-id="1a45f-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="1a45f-365">objectEmpty</span></span> | <span data-ttu-id="1a45f-366">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-366">Bool</span></span> | <span data-ttu-id="1a45f-367">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-367">True</span></span> |
| <span data-ttu-id="1a45f-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="1a45f-368">stringEmpty</span></span> | <span data-ttu-id="1a45f-369">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-369">Bool</span></span> | <span data-ttu-id="1a45f-370">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="1a45f-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="1a45f-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="1a45f-372">Determina se uma cadeia de caracteres termina com um valor.</span><span class="sxs-lookup"><span data-stu-id="1a45f-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="1a45f-373">A comparação não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-374">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-374">Parameters</span></span>

| <span data-ttu-id="1a45f-375">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-375">Parameter</span></span> | <span data-ttu-id="1a45f-376">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-376">Required</span></span> | <span data-ttu-id="1a45f-377">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-377">Type</span></span> | <span data-ttu-id="1a45f-378">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1a45f-379">stringToSearch</span></span> |<span data-ttu-id="1a45f-380">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-380">Yes</span></span> |<span data-ttu-id="1a45f-381">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-381">string</span></span> |<span data-ttu-id="1a45f-382">O valor que contém o item a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1a45f-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1a45f-383">stringToFind</span></span> |<span data-ttu-id="1a45f-384">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-384">Yes</span></span> |<span data-ttu-id="1a45f-385">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-385">string</span></span> |<span data-ttu-id="1a45f-386">O valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-387">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-387">Return value</span></span>

<span data-ttu-id="1a45f-388">**True** se o último caractere ou caracteres da cadeia de caracteres corresponderem ao valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="1a45f-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-389">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-389">Examples</span></span>

<span data-ttu-id="1a45f-390">O seguinte exemplo mostra como usar as funções startsWith e endsWith:</span><span class="sxs-lookup"><span data-stu-id="1a45f-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="1a45f-391">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-392">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-392">Name</span></span> | <span data-ttu-id="1a45f-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-393">Type</span></span> | <span data-ttu-id="1a45f-394">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-395">startsTrue</span></span> | <span data-ttu-id="1a45f-396">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-396">Bool</span></span> | <span data-ttu-id="1a45f-397">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-397">True</span></span> |
| <span data-ttu-id="1a45f-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-398">startsCapTrue</span></span> | <span data-ttu-id="1a45f-399">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-399">Bool</span></span> | <span data-ttu-id="1a45f-400">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-400">True</span></span> |
| <span data-ttu-id="1a45f-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-401">startsFalse</span></span> | <span data-ttu-id="1a45f-402">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-402">Bool</span></span> | <span data-ttu-id="1a45f-403">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-403">False</span></span> |
| <span data-ttu-id="1a45f-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-404">endsTrue</span></span> | <span data-ttu-id="1a45f-405">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-405">Bool</span></span> | <span data-ttu-id="1a45f-406">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-406">True</span></span> |
| <span data-ttu-id="1a45f-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-407">endsCapTrue</span></span> | <span data-ttu-id="1a45f-408">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-408">Bool</span></span> | <span data-ttu-id="1a45f-409">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-409">True</span></span> |
| <span data-ttu-id="1a45f-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-410">endsFalse</span></span> | <span data-ttu-id="1a45f-411">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-411">Bool</span></span> | <span data-ttu-id="1a45f-412">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="1a45f-413">first</span><span class="sxs-lookup"><span data-stu-id="1a45f-413">first</span></span>
`first(arg1)`

<span data-ttu-id="1a45f-414">Retorna o primeiro caractere da cadeia de caracteres ou o primeiro elemento da matriz.</span><span class="sxs-lookup"><span data-stu-id="1a45f-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-415">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-415">Parameters</span></span>

| <span data-ttu-id="1a45f-416">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-416">Parameter</span></span> | <span data-ttu-id="1a45f-417">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-417">Required</span></span> | <span data-ttu-id="1a45f-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-418">Type</span></span> | <span data-ttu-id="1a45f-419">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-420">arg1</span><span class="sxs-lookup"><span data-stu-id="1a45f-420">arg1</span></span> |<span data-ttu-id="1a45f-421">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-421">Yes</span></span> |<span data-ttu-id="1a45f-422">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-422">array or string</span></span> |<span data-ttu-id="1a45f-423">O valor para recuperar o primeiro elemento ou caractere.</span><span class="sxs-lookup"><span data-stu-id="1a45f-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-424">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-424">Return value</span></span>

<span data-ttu-id="1a45f-425">Uma cadeia de caracteres do primeiro caractere ou o tipo (cadeia de caracteres, inteiro, matriz ou objeto) do primeiro elemento em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="1a45f-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-426">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-426">Examples</span></span>

<span data-ttu-id="1a45f-427">O exemplo a seguir mostra como usar a primeira função com uma matriz e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="1a45f-428">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-429">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-429">Name</span></span> | <span data-ttu-id="1a45f-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-430">Type</span></span> | <span data-ttu-id="1a45f-431">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-432">arrayOutput</span></span> | <span data-ttu-id="1a45f-433">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-433">String</span></span> | <span data-ttu-id="1a45f-434">one</span><span class="sxs-lookup"><span data-stu-id="1a45f-434">one</span></span> |
| <span data-ttu-id="1a45f-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-435">stringOutput</span></span> | <span data-ttu-id="1a45f-436">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-436">String</span></span> | <span data-ttu-id="1a45f-437">O</span><span class="sxs-lookup"><span data-stu-id="1a45f-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="1a45f-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="1a45f-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="1a45f-439">Retorna a primeira posição de um valor em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="1a45f-440">A comparação não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-441">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-441">Parameters</span></span>

| <span data-ttu-id="1a45f-442">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-442">Parameter</span></span> | <span data-ttu-id="1a45f-443">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-443">Required</span></span> | <span data-ttu-id="1a45f-444">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-444">Type</span></span> | <span data-ttu-id="1a45f-445">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1a45f-446">stringToSearch</span></span> |<span data-ttu-id="1a45f-447">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-447">Yes</span></span> |<span data-ttu-id="1a45f-448">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-448">string</span></span> |<span data-ttu-id="1a45f-449">O valor que contém o item a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1a45f-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1a45f-450">stringToFind</span></span> |<span data-ttu-id="1a45f-451">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-451">Yes</span></span> |<span data-ttu-id="1a45f-452">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-452">string</span></span> |<span data-ttu-id="1a45f-453">O valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-454">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-454">Return value</span></span>

<span data-ttu-id="1a45f-455">Um inteiro que representa a posição do item a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="1a45f-456">O valor é baseado em zero.</span><span class="sxs-lookup"><span data-stu-id="1a45f-456">The value is zero-based.</span></span> <span data-ttu-id="1a45f-457">Se o item não for encontrado, -1 será retornado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-458">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-458">Examples</span></span>

<span data-ttu-id="1a45f-459">O seguinte exemplo mostra como usar as funções indexOf e lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="1a45f-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="1a45f-460">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-461">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-461">Name</span></span> | <span data-ttu-id="1a45f-462">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-462">Type</span></span> | <span data-ttu-id="1a45f-463">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-464">firstT</span><span class="sxs-lookup"><span data-stu-id="1a45f-464">firstT</span></span> | <span data-ttu-id="1a45f-465">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-465">Int</span></span> | <span data-ttu-id="1a45f-466">0</span><span class="sxs-lookup"><span data-stu-id="1a45f-466">0</span></span> |
| <span data-ttu-id="1a45f-467">lastT</span><span class="sxs-lookup"><span data-stu-id="1a45f-467">lastT</span></span> | <span data-ttu-id="1a45f-468">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-468">Int</span></span> | <span data-ttu-id="1a45f-469">3</span><span class="sxs-lookup"><span data-stu-id="1a45f-469">3</span></span> |
| <span data-ttu-id="1a45f-470">firstString</span><span class="sxs-lookup"><span data-stu-id="1a45f-470">firstString</span></span> | <span data-ttu-id="1a45f-471">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-471">Int</span></span> | <span data-ttu-id="1a45f-472">2</span><span class="sxs-lookup"><span data-stu-id="1a45f-472">2</span></span> |
| <span data-ttu-id="1a45f-473">lastString</span><span class="sxs-lookup"><span data-stu-id="1a45f-473">lastString</span></span> | <span data-ttu-id="1a45f-474">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-474">Int</span></span> | <span data-ttu-id="1a45f-475">0</span><span class="sxs-lookup"><span data-stu-id="1a45f-475">0</span></span> |
| <span data-ttu-id="1a45f-476">NotFound</span><span class="sxs-lookup"><span data-stu-id="1a45f-476">notFound</span></span> | <span data-ttu-id="1a45f-477">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-477">Int</span></span> | <span data-ttu-id="1a45f-478">-1</span><span class="sxs-lookup"><span data-stu-id="1a45f-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="1a45f-479">last</span><span class="sxs-lookup"><span data-stu-id="1a45f-479">last</span></span>
`last (arg1)`

<span data-ttu-id="1a45f-480">Retorna o último caractere da cadeia de caracteres ou o último elemento da matriz.</span><span class="sxs-lookup"><span data-stu-id="1a45f-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-481">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-481">Parameters</span></span>

| <span data-ttu-id="1a45f-482">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-482">Parameter</span></span> | <span data-ttu-id="1a45f-483">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-483">Required</span></span> | <span data-ttu-id="1a45f-484">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-484">Type</span></span> | <span data-ttu-id="1a45f-485">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-486">arg1</span><span class="sxs-lookup"><span data-stu-id="1a45f-486">arg1</span></span> |<span data-ttu-id="1a45f-487">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-487">Yes</span></span> |<span data-ttu-id="1a45f-488">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-488">array or string</span></span> |<span data-ttu-id="1a45f-489">O valor para recuperar o último elemento ou caractere.</span><span class="sxs-lookup"><span data-stu-id="1a45f-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-490">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-490">Return value</span></span>

<span data-ttu-id="1a45f-491">Uma cadeia de caracteres do último caractere ou o tipo (cadeia de caracteres, inteiro, matriz ou objeto) do último elemento em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="1a45f-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-492">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-492">Examples</span></span>

<span data-ttu-id="1a45f-493">O exemplo a seguir mostra como usar a última função com uma matriz e cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="1a45f-494">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-495">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-495">Name</span></span> | <span data-ttu-id="1a45f-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-496">Type</span></span> | <span data-ttu-id="1a45f-497">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-498">arrayOutput</span></span> | <span data-ttu-id="1a45f-499">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-499">String</span></span> | <span data-ttu-id="1a45f-500">três</span><span class="sxs-lookup"><span data-stu-id="1a45f-500">three</span></span> |
| <span data-ttu-id="1a45f-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-501">stringOutput</span></span> | <span data-ttu-id="1a45f-502">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-502">String</span></span> | <span data-ttu-id="1a45f-503">e</span><span class="sxs-lookup"><span data-stu-id="1a45f-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="1a45f-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="1a45f-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="1a45f-505">Retorna a última posição de um valor em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="1a45f-506">A comparação não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-507">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-507">Parameters</span></span>

| <span data-ttu-id="1a45f-508">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-508">Parameter</span></span> | <span data-ttu-id="1a45f-509">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-509">Required</span></span> | <span data-ttu-id="1a45f-510">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-510">Type</span></span> | <span data-ttu-id="1a45f-511">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1a45f-512">stringToSearch</span></span> |<span data-ttu-id="1a45f-513">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-513">Yes</span></span> |<span data-ttu-id="1a45f-514">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-514">string</span></span> |<span data-ttu-id="1a45f-515">O valor que contém o item a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1a45f-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1a45f-516">stringToFind</span></span> |<span data-ttu-id="1a45f-517">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-517">Yes</span></span> |<span data-ttu-id="1a45f-518">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-518">string</span></span> |<span data-ttu-id="1a45f-519">O valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-520">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-520">Return value</span></span>

<span data-ttu-id="1a45f-521">Um inteiro que representa a última posição do item a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="1a45f-522">O valor é baseado em zero.</span><span class="sxs-lookup"><span data-stu-id="1a45f-522">The value is zero-based.</span></span> <span data-ttu-id="1a45f-523">Se o item não for encontrado, -1 será retornado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-524">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-524">Examples</span></span>

<span data-ttu-id="1a45f-525">O seguinte exemplo mostra como usar as funções indexOf e lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="1a45f-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="1a45f-526">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-527">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-527">Name</span></span> | <span data-ttu-id="1a45f-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-528">Type</span></span> | <span data-ttu-id="1a45f-529">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-530">firstT</span><span class="sxs-lookup"><span data-stu-id="1a45f-530">firstT</span></span> | <span data-ttu-id="1a45f-531">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-531">Int</span></span> | <span data-ttu-id="1a45f-532">0</span><span class="sxs-lookup"><span data-stu-id="1a45f-532">0</span></span> |
| <span data-ttu-id="1a45f-533">lastT</span><span class="sxs-lookup"><span data-stu-id="1a45f-533">lastT</span></span> | <span data-ttu-id="1a45f-534">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-534">Int</span></span> | <span data-ttu-id="1a45f-535">3</span><span class="sxs-lookup"><span data-stu-id="1a45f-535">3</span></span> |
| <span data-ttu-id="1a45f-536">firstString</span><span class="sxs-lookup"><span data-stu-id="1a45f-536">firstString</span></span> | <span data-ttu-id="1a45f-537">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-537">Int</span></span> | <span data-ttu-id="1a45f-538">2</span><span class="sxs-lookup"><span data-stu-id="1a45f-538">2</span></span> |
| <span data-ttu-id="1a45f-539">lastString</span><span class="sxs-lookup"><span data-stu-id="1a45f-539">lastString</span></span> | <span data-ttu-id="1a45f-540">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-540">Int</span></span> | <span data-ttu-id="1a45f-541">0</span><span class="sxs-lookup"><span data-stu-id="1a45f-541">0</span></span> |
| <span data-ttu-id="1a45f-542">NotFound</span><span class="sxs-lookup"><span data-stu-id="1a45f-542">notFound</span></span> | <span data-ttu-id="1a45f-543">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-543">Int</span></span> | <span data-ttu-id="1a45f-544">-1</span><span class="sxs-lookup"><span data-stu-id="1a45f-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="1a45f-545">length</span><span class="sxs-lookup"><span data-stu-id="1a45f-545">length</span></span>
`length(string)`

<span data-ttu-id="1a45f-546">Retorna o número de caracteres em uma cadeia de caracteres ou de elementos em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="1a45f-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-547">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-547">Parameters</span></span>

| <span data-ttu-id="1a45f-548">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-548">Parameter</span></span> | <span data-ttu-id="1a45f-549">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-549">Required</span></span> | <span data-ttu-id="1a45f-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-550">Type</span></span> | <span data-ttu-id="1a45f-551">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-552">arg1</span><span class="sxs-lookup"><span data-stu-id="1a45f-552">arg1</span></span> |<span data-ttu-id="1a45f-553">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-553">Yes</span></span> |<span data-ttu-id="1a45f-554">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-554">array or string</span></span> |<span data-ttu-id="1a45f-555">A matriz a ser usada para obter o número de elementos ou a cadeia de caracteres a ser usada para obter o número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-556">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-556">Return value</span></span>

<span data-ttu-id="1a45f-557">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="1a45f-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="1a45f-558">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-558">Examples</span></span>

<span data-ttu-id="1a45f-559">O seguinte exemplo mostra como usar length com uma matriz e cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="1a45f-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="1a45f-560">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-561">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-561">Name</span></span> | <span data-ttu-id="1a45f-562">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-562">Type</span></span> | <span data-ttu-id="1a45f-563">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="1a45f-564">arrayLength</span></span> | <span data-ttu-id="1a45f-565">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-565">Int</span></span> | <span data-ttu-id="1a45f-566">3</span><span class="sxs-lookup"><span data-stu-id="1a45f-566">3</span></span> |
| <span data-ttu-id="1a45f-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="1a45f-567">stringLength</span></span> | <span data-ttu-id="1a45f-568">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-568">Int</span></span> | <span data-ttu-id="1a45f-569">13</span><span class="sxs-lookup"><span data-stu-id="1a45f-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="1a45f-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="1a45f-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="1a45f-571">Retorna uma cadeia de caracteres alinhada à direita adicionando caracteres à esquerda até alcançar o comprimento total especificado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-572">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-572">Parameters</span></span>

| <span data-ttu-id="1a45f-573">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-573">Parameter</span></span> | <span data-ttu-id="1a45f-574">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-574">Required</span></span> | <span data-ttu-id="1a45f-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-575">Type</span></span> | <span data-ttu-id="1a45f-576">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="1a45f-577">valueToPad</span></span> |<span data-ttu-id="1a45f-578">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-578">Yes</span></span> |<span data-ttu-id="1a45f-579">cadeia de caracteres ou inteiro</span><span class="sxs-lookup"><span data-stu-id="1a45f-579">string or int</span></span> |<span data-ttu-id="1a45f-580">O valor para alinhar à direita.</span><span class="sxs-lookup"><span data-stu-id="1a45f-580">The value to right-align.</span></span> |
| <span data-ttu-id="1a45f-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="1a45f-581">totalLength</span></span> |<span data-ttu-id="1a45f-582">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-582">Yes</span></span> |<span data-ttu-id="1a45f-583">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-583">int</span></span> |<span data-ttu-id="1a45f-584">O número total de caracteres na cadeia de caracteres retornada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="1a45f-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="1a45f-585">paddingCharacter</span></span> |<span data-ttu-id="1a45f-586">Não</span><span class="sxs-lookup"><span data-stu-id="1a45f-586">No</span></span> |<span data-ttu-id="1a45f-587">caractere único</span><span class="sxs-lookup"><span data-stu-id="1a45f-587">single character</span></span> |<span data-ttu-id="1a45f-588">O caractere a ser usado para o preenchimento à esquerda até que o tamanho total seja atingido.</span><span class="sxs-lookup"><span data-stu-id="1a45f-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="1a45f-589">O valor padrão é um espaço.</span><span class="sxs-lookup"><span data-stu-id="1a45f-589">The default value is a space.</span></span> |

<span data-ttu-id="1a45f-590">Se a cadeia de caracteres original for mais longa que o número de caracteres a ser preenchido, nenhum caractere será adicionado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="1a45f-591">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-591">Return value</span></span>

<span data-ttu-id="1a45f-592">Uma cadeia de caracteres com, pelo menos, o número de caracteres especificado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-593">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-593">Examples</span></span>

<span data-ttu-id="1a45f-594">O exemplo a seguir mostra como preencher o valor de parâmetro fornecido pelo usuário adicionando o caractere zero até que ele atinja o número total de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

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

<span data-ttu-id="1a45f-595">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-596">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-596">Name</span></span> | <span data-ttu-id="1a45f-597">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-597">Type</span></span> | <span data-ttu-id="1a45f-598">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-599">stringOutput</span></span> | <span data-ttu-id="1a45f-600">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-600">String</span></span> | <span data-ttu-id="1a45f-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="1a45f-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="1a45f-602">substituir</span><span class="sxs-lookup"><span data-stu-id="1a45f-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="1a45f-603">Retorna uma nova cadeia de caracteres com todas as instâncias de uma cadeia de caracteres substituídas por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-604">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-604">Parameters</span></span>

| <span data-ttu-id="1a45f-605">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-605">Parameter</span></span> | <span data-ttu-id="1a45f-606">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-606">Required</span></span> | <span data-ttu-id="1a45f-607">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-607">Type</span></span> | <span data-ttu-id="1a45f-608">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-609">originalString</span><span class="sxs-lookup"><span data-stu-id="1a45f-609">originalString</span></span> |<span data-ttu-id="1a45f-610">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-610">Yes</span></span> |<span data-ttu-id="1a45f-611">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-611">string</span></span> |<span data-ttu-id="1a45f-612">O valor que tem todas as instâncias de uma cadeia de caracteres substituídas por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="1a45f-613">oldString</span><span class="sxs-lookup"><span data-stu-id="1a45f-613">oldString</span></span> |<span data-ttu-id="1a45f-614">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-614">Yes</span></span> |<span data-ttu-id="1a45f-615">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-615">string</span></span> |<span data-ttu-id="1a45f-616">A cadeia de caractere a ser removida da cadeia de caracteres original.</span><span class="sxs-lookup"><span data-stu-id="1a45f-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="1a45f-617">newString</span><span class="sxs-lookup"><span data-stu-id="1a45f-617">newString</span></span> |<span data-ttu-id="1a45f-618">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-618">Yes</span></span> |<span data-ttu-id="1a45f-619">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-619">string</span></span> |<span data-ttu-id="1a45f-620">A cadeia de caracteres a ser adicionada no lugar da cadeia removida.</span><span class="sxs-lookup"><span data-stu-id="1a45f-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-621">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-621">Return value</span></span>

<span data-ttu-id="1a45f-622">Uma cadeia de caracteres com os caracteres substituídos.</span><span class="sxs-lookup"><span data-stu-id="1a45f-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-623">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-623">Examples</span></span>

<span data-ttu-id="1a45f-624">O exemplo a seguir mostra como remover todos os traços da cadeia de caracteres fornecida pelo usuário e como substituir parte da cadeia de caracteres por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

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

<span data-ttu-id="1a45f-625">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-626">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-626">Name</span></span> | <span data-ttu-id="1a45f-627">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-627">Type</span></span> | <span data-ttu-id="1a45f-628">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-629">firstOutput</span></span> | <span data-ttu-id="1a45f-630">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-630">String</span></span> | <span data-ttu-id="1a45f-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="1a45f-631">1231231234</span></span> |
| <span data-ttu-id="1a45f-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-632">secodeOutput</span></span> | <span data-ttu-id="1a45f-633">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-633">String</span></span> | <span data-ttu-id="1a45f-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="1a45f-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="1a45f-635">skip</span><span class="sxs-lookup"><span data-stu-id="1a45f-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="1a45f-636">Retorna uma cadeia de caracteres com todos os caracteres após o número especificado de caracteres ou uma matriz com todos os elementos após o número especificado de elementos.</span><span class="sxs-lookup"><span data-stu-id="1a45f-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-637">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-637">Parameters</span></span>

| <span data-ttu-id="1a45f-638">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-638">Parameter</span></span> | <span data-ttu-id="1a45f-639">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-639">Required</span></span> | <span data-ttu-id="1a45f-640">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-640">Type</span></span> | <span data-ttu-id="1a45f-641">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="1a45f-642">originalValue</span></span> |<span data-ttu-id="1a45f-643">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-643">Yes</span></span> |<span data-ttu-id="1a45f-644">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-644">array or string</span></span> |<span data-ttu-id="1a45f-645">A matriz ou cadeia de caracteres a ser usada para ignorar.</span><span class="sxs-lookup"><span data-stu-id="1a45f-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="1a45f-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="1a45f-646">numberToSkip</span></span> |<span data-ttu-id="1a45f-647">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-647">Yes</span></span> |<span data-ttu-id="1a45f-648">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-648">int</span></span> |<span data-ttu-id="1a45f-649">O número de elementos ou caracteres a ser ignorado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="1a45f-650">Se esse valor for 0 ou menos, todos os elementos ou caracteres no valor serão retornados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="1a45f-651">Se for maior que o tamanho da matriz ou cadeia de caracteres, uma matriz ou cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-652">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-652">Return value</span></span>

<span data-ttu-id="1a45f-653">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-654">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-654">Examples</span></span>

<span data-ttu-id="1a45f-655">O exemplo a seguir ignora o número especificado de elementos na matriz e o número especificado de caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="1a45f-656">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-657">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-657">Name</span></span> | <span data-ttu-id="1a45f-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-658">Type</span></span> | <span data-ttu-id="1a45f-659">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-660">arrayOutput</span></span> | <span data-ttu-id="1a45f-661">Matriz</span><span class="sxs-lookup"><span data-stu-id="1a45f-661">Array</span></span> | <span data-ttu-id="1a45f-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="1a45f-662">["three"]</span></span> |
| <span data-ttu-id="1a45f-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-663">stringOutput</span></span> | <span data-ttu-id="1a45f-664">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-664">String</span></span> | <span data-ttu-id="1a45f-665">dois três</span><span class="sxs-lookup"><span data-stu-id="1a45f-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="1a45f-666">split</span><span class="sxs-lookup"><span data-stu-id="1a45f-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="1a45f-667">Retorna uma matriz de cadeias de caracteres que contém as subcadeias de caracteres da cadeia de caracteres de entrada que são delimitadas por delimitadores especificados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-668">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-668">Parameters</span></span>

| <span data-ttu-id="1a45f-669">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-669">Parameter</span></span> | <span data-ttu-id="1a45f-670">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-670">Required</span></span> | <span data-ttu-id="1a45f-671">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-671">Type</span></span> | <span data-ttu-id="1a45f-672">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-673">inputString</span><span class="sxs-lookup"><span data-stu-id="1a45f-673">inputString</span></span> |<span data-ttu-id="1a45f-674">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-674">Yes</span></span> |<span data-ttu-id="1a45f-675">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-675">string</span></span> |<span data-ttu-id="1a45f-676">A cadeia de caracteres a dividir.</span><span class="sxs-lookup"><span data-stu-id="1a45f-676">The string to split.</span></span> |
| <span data-ttu-id="1a45f-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="1a45f-677">delimiter</span></span> |<span data-ttu-id="1a45f-678">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-678">Yes</span></span> |<span data-ttu-id="1a45f-679">cadeia de caracteres ou matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-679">string or array of strings</span></span> |<span data-ttu-id="1a45f-680">O delimitador a ser usado para dividir a cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-681">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-681">Return value</span></span>

<span data-ttu-id="1a45f-682">Uma matriz de cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-683">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-683">Examples</span></span>

<span data-ttu-id="1a45f-684">O exemplo a seguir divide a cadeia de caracteres de entrada com uma vírgula e com uma vírgula ou um ponto-e-vírgula.</span><span class="sxs-lookup"><span data-stu-id="1a45f-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="1a45f-685">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-686">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-686">Name</span></span> | <span data-ttu-id="1a45f-687">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-687">Type</span></span> | <span data-ttu-id="1a45f-688">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-689">firstOutput</span></span> | <span data-ttu-id="1a45f-690">Matriz</span><span class="sxs-lookup"><span data-stu-id="1a45f-690">Array</span></span> | <span data-ttu-id="1a45f-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="1a45f-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="1a45f-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-692">secondOutput</span></span> | <span data-ttu-id="1a45f-693">Matriz</span><span class="sxs-lookup"><span data-stu-id="1a45f-693">Array</span></span> | <span data-ttu-id="1a45f-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="1a45f-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="1a45f-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="1a45f-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="1a45f-696">Determina se uma cadeia de caracteres começa com um valor.</span><span class="sxs-lookup"><span data-stu-id="1a45f-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="1a45f-697">A comparação não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-698">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-698">Parameters</span></span>

| <span data-ttu-id="1a45f-699">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-699">Parameter</span></span> | <span data-ttu-id="1a45f-700">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-700">Required</span></span> | <span data-ttu-id="1a45f-701">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-701">Type</span></span> | <span data-ttu-id="1a45f-702">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1a45f-703">stringToSearch</span></span> |<span data-ttu-id="1a45f-704">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-704">Yes</span></span> |<span data-ttu-id="1a45f-705">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-705">string</span></span> |<span data-ttu-id="1a45f-706">O valor que contém o item a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1a45f-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1a45f-707">stringToFind</span></span> |<span data-ttu-id="1a45f-708">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-708">Yes</span></span> |<span data-ttu-id="1a45f-709">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-709">string</span></span> |<span data-ttu-id="1a45f-710">O valor a ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-711">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-711">Return value</span></span>

<span data-ttu-id="1a45f-712">**True** se o primeiro caractere ou caracteres da cadeia de caracteres corresponderem ao valor; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="1a45f-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-713">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-713">Examples</span></span>

<span data-ttu-id="1a45f-714">O seguinte exemplo mostra como usar as funções startsWith e endsWith:</span><span class="sxs-lookup"><span data-stu-id="1a45f-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="1a45f-715">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-716">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-716">Name</span></span> | <span data-ttu-id="1a45f-717">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-717">Type</span></span> | <span data-ttu-id="1a45f-718">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-719">startsTrue</span></span> | <span data-ttu-id="1a45f-720">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-720">Bool</span></span> | <span data-ttu-id="1a45f-721">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-721">True</span></span> |
| <span data-ttu-id="1a45f-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-722">startsCapTrue</span></span> | <span data-ttu-id="1a45f-723">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-723">Bool</span></span> | <span data-ttu-id="1a45f-724">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-724">True</span></span> |
| <span data-ttu-id="1a45f-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-725">startsFalse</span></span> | <span data-ttu-id="1a45f-726">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-726">Bool</span></span> | <span data-ttu-id="1a45f-727">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-727">False</span></span> |
| <span data-ttu-id="1a45f-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-728">endsTrue</span></span> | <span data-ttu-id="1a45f-729">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-729">Bool</span></span> | <span data-ttu-id="1a45f-730">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-730">True</span></span> |
| <span data-ttu-id="1a45f-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1a45f-731">endsCapTrue</span></span> | <span data-ttu-id="1a45f-732">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-732">Bool</span></span> | <span data-ttu-id="1a45f-733">True </span><span class="sxs-lookup"><span data-stu-id="1a45f-733">True</span></span> |
| <span data-ttu-id="1a45f-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="1a45f-734">endsFalse</span></span> | <span data-ttu-id="1a45f-735">Bool</span><span class="sxs-lookup"><span data-stu-id="1a45f-735">Bool</span></span> | <span data-ttu-id="1a45f-736">Falso</span><span class="sxs-lookup"><span data-stu-id="1a45f-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="1a45f-737">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="1a45f-738">Converte o valor especificado em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-739">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-739">Parameters</span></span>

| <span data-ttu-id="1a45f-740">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-740">Parameter</span></span> | <span data-ttu-id="1a45f-741">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-741">Required</span></span> | <span data-ttu-id="1a45f-742">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-742">Type</span></span> | <span data-ttu-id="1a45f-743">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="1a45f-744">valueToConvert</span></span> |<span data-ttu-id="1a45f-745">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-745">Yes</span></span> | <span data-ttu-id="1a45f-746">Qualquer</span><span class="sxs-lookup"><span data-stu-id="1a45f-746">Any</span></span> |<span data-ttu-id="1a45f-747">O valor a ser convertido em cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-747">The value to convert to string.</span></span> <span data-ttu-id="1a45f-748">Qualquer tipo de valor pode ser convertido, incluindo objetos e matrizes.</span><span class="sxs-lookup"><span data-stu-id="1a45f-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-749">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-749">Return value</span></span>

<span data-ttu-id="1a45f-750">Uma cadeia de caracteres do valor convertido.</span><span class="sxs-lookup"><span data-stu-id="1a45f-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-751">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-751">Examples</span></span>

<span data-ttu-id="1a45f-752">O seguinte exemplo mostra como converter diferentes tipos de valores em cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="1a45f-752">The following example shows how to convert different types of values to strings:</span></span>

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

<span data-ttu-id="1a45f-753">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-754">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-754">Name</span></span> | <span data-ttu-id="1a45f-755">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-755">Type</span></span> | <span data-ttu-id="1a45f-756">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-757">objectOutput</span></span> | <span data-ttu-id="1a45f-758">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-758">String</span></span> | <span data-ttu-id="1a45f-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="1a45f-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="1a45f-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-760">arrayOutput</span></span> | <span data-ttu-id="1a45f-761">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-761">String</span></span> | <span data-ttu-id="1a45f-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="1a45f-762">["a","b","c"]</span></span> |
| <span data-ttu-id="1a45f-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-763">intOutput</span></span> | <span data-ttu-id="1a45f-764">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-764">String</span></span> | <span data-ttu-id="1a45f-765">5</span><span class="sxs-lookup"><span data-stu-id="1a45f-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="1a45f-766">substring</span><span class="sxs-lookup"><span data-stu-id="1a45f-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="1a45f-767">Retorna uma subcadeia de caraceteres que começa na posição do caractere especificado e contém o número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-768">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-768">Parameters</span></span>

| <span data-ttu-id="1a45f-769">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-769">Parameter</span></span> | <span data-ttu-id="1a45f-770">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-770">Required</span></span> | <span data-ttu-id="1a45f-771">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-771">Type</span></span> | <span data-ttu-id="1a45f-772">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="1a45f-773">stringToParse</span></span> |<span data-ttu-id="1a45f-774">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-774">Yes</span></span> |<span data-ttu-id="1a45f-775">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-775">string</span></span> |<span data-ttu-id="1a45f-776">A cadeia original da qual a subcadeia de caracteres é extraída.</span><span class="sxs-lookup"><span data-stu-id="1a45f-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="1a45f-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="1a45f-777">startIndex</span></span> |<span data-ttu-id="1a45f-778">Não</span><span class="sxs-lookup"><span data-stu-id="1a45f-778">No</span></span> |<span data-ttu-id="1a45f-779">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-779">int</span></span> |<span data-ttu-id="1a45f-780">A posição inicial do caractere baseada em zero para a subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="1a45f-781">length</span><span class="sxs-lookup"><span data-stu-id="1a45f-781">length</span></span> |<span data-ttu-id="1a45f-782">Não</span><span class="sxs-lookup"><span data-stu-id="1a45f-782">No</span></span> |<span data-ttu-id="1a45f-783">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-783">int</span></span> |<span data-ttu-id="1a45f-784">O número de caracteres para a subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-784">The number of characters for the substring.</span></span> <span data-ttu-id="1a45f-785">Deve se referir a uma localização dentro da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-786">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-786">Return value</span></span>

<span data-ttu-id="1a45f-787">A subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="1a45f-788">Comentários</span><span class="sxs-lookup"><span data-stu-id="1a45f-788">Remarks</span></span>

<span data-ttu-id="1a45f-789">A função falhará quando a subcadeia de caracteres ultrapassar o final da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="1a45f-790">O exemplo a seguir falha com o erro “Os parâmetros de índice e de tamanho devem se referir a uma localização na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="1a45f-791">O parâmetro de índice: '0', o parâmetro de comprimento: '11', o comprimento do parâmetro de cadeia de caracteres: '10'”.</span><span class="sxs-lookup"><span data-stu-id="1a45f-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="1a45f-792">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-792">Examples</span></span>

<span data-ttu-id="1a45f-793">O exemplo a seguir extrai uma subcadeia de caracteres de um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1a45f-793">The following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="1a45f-794">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-795">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-795">Name</span></span> | <span data-ttu-id="1a45f-796">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-796">Type</span></span> | <span data-ttu-id="1a45f-797">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-798">substringOutput</span></span> | <span data-ttu-id="1a45f-799">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-799">String</span></span> | <span data-ttu-id="1a45f-800">dois</span><span class="sxs-lookup"><span data-stu-id="1a45f-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="1a45f-801">take</span><span class="sxs-lookup"><span data-stu-id="1a45f-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="1a45f-802">Retorna uma cadeia de caracteres com o número especificado de caracteres desde o início da cadeia de caracteres ou uma matriz com o número especificado de elementos desde o início da matriz.</span><span class="sxs-lookup"><span data-stu-id="1a45f-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-803">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-803">Parameters</span></span>

| <span data-ttu-id="1a45f-804">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-804">Parameter</span></span> | <span data-ttu-id="1a45f-805">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-805">Required</span></span> | <span data-ttu-id="1a45f-806">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-806">Type</span></span> | <span data-ttu-id="1a45f-807">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="1a45f-808">originalValue</span></span> |<span data-ttu-id="1a45f-809">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-809">Yes</span></span> |<span data-ttu-id="1a45f-810">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-810">array or string</span></span> |<span data-ttu-id="1a45f-811">A matriz ou cadeia de caracteres da qual extrair os elementos.</span><span class="sxs-lookup"><span data-stu-id="1a45f-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="1a45f-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="1a45f-812">numberToTake</span></span> |<span data-ttu-id="1a45f-813">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-813">Yes</span></span> |<span data-ttu-id="1a45f-814">int</span><span class="sxs-lookup"><span data-stu-id="1a45f-814">int</span></span> |<span data-ttu-id="1a45f-815">O número de elementos ou caracteres a ser extraído.</span><span class="sxs-lookup"><span data-stu-id="1a45f-815">The number of elements or characters to take.</span></span> <span data-ttu-id="1a45f-816">Se esse valor for 0 ou menos, uma matriz ou cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="1a45f-817">Se for maior que o tamanho da matriz ou cadeia de caracteres especificada, todos os elementos da matriz ou cadeia de caracteres serão retornados.</span><span class="sxs-lookup"><span data-stu-id="1a45f-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-818">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-818">Return value</span></span>

<span data-ttu-id="1a45f-819">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-820">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-820">Examples</span></span>

<span data-ttu-id="1a45f-821">O exemplo a seguir extrai o número especificado de elementos da matriz e de caracteres de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="1a45f-822">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-823">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-823">Name</span></span> | <span data-ttu-id="1a45f-824">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-824">Type</span></span> | <span data-ttu-id="1a45f-825">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-826">arrayOutput</span></span> | <span data-ttu-id="1a45f-827">Matriz</span><span class="sxs-lookup"><span data-stu-id="1a45f-827">Array</span></span> | <span data-ttu-id="1a45f-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="1a45f-828">["one", "two"]</span></span> |
| <span data-ttu-id="1a45f-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-829">stringOutput</span></span> | <span data-ttu-id="1a45f-830">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-830">String</span></span> | <span data-ttu-id="1a45f-831">em</span><span class="sxs-lookup"><span data-stu-id="1a45f-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="1a45f-832">toLower</span><span class="sxs-lookup"><span data-stu-id="1a45f-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="1a45f-833">Converte a cadeia de caracteres especificada em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-834">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-834">Parameters</span></span>

| <span data-ttu-id="1a45f-835">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-835">Parameter</span></span> | <span data-ttu-id="1a45f-836">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-836">Required</span></span> | <span data-ttu-id="1a45f-837">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-837">Type</span></span> | <span data-ttu-id="1a45f-838">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="1a45f-839">stringToChange</span></span> |<span data-ttu-id="1a45f-840">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-840">Yes</span></span> |<span data-ttu-id="1a45f-841">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-841">string</span></span> |<span data-ttu-id="1a45f-842">O valor a ser convertido em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-843">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-843">Return value</span></span>

<span data-ttu-id="1a45f-844">A cadeia de caracteres convertida em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-845">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-845">Examples</span></span>

<span data-ttu-id="1a45f-846">O exemplo a seguir converte um valor de parâmetro em letras minúsculas e maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-846">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="1a45f-847">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-848">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-848">Name</span></span> | <span data-ttu-id="1a45f-849">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-849">Type</span></span> | <span data-ttu-id="1a45f-850">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-851">toLowerOutput</span></span> | <span data-ttu-id="1a45f-852">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-852">String</span></span> | <span data-ttu-id="1a45f-853">um dois três</span><span class="sxs-lookup"><span data-stu-id="1a45f-853">one two three</span></span> |
| <span data-ttu-id="1a45f-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-854">toUpperOutput</span></span> | <span data-ttu-id="1a45f-855">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-855">String</span></span> | <span data-ttu-id="1a45f-856">UM DOIS TRÊS</span><span class="sxs-lookup"><span data-stu-id="1a45f-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="1a45f-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="1a45f-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="1a45f-858">Converte a cadeia de caracteres especificada em maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-859">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-859">Parameters</span></span>

| <span data-ttu-id="1a45f-860">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-860">Parameter</span></span> | <span data-ttu-id="1a45f-861">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-861">Required</span></span> | <span data-ttu-id="1a45f-862">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-862">Type</span></span> | <span data-ttu-id="1a45f-863">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="1a45f-864">stringToChange</span></span> |<span data-ttu-id="1a45f-865">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-865">Yes</span></span> |<span data-ttu-id="1a45f-866">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-866">string</span></span> |<span data-ttu-id="1a45f-867">O valor a ser convertido em letras maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-868">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-868">Return value</span></span>

<span data-ttu-id="1a45f-869">A cadeia de caracteres convertida em maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-870">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-870">Examples</span></span>

<span data-ttu-id="1a45f-871">O exemplo a seguir converte um valor de parâmetro em letras minúsculas e maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="1a45f-871">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="1a45f-872">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-873">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-873">Name</span></span> | <span data-ttu-id="1a45f-874">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-874">Type</span></span> | <span data-ttu-id="1a45f-875">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-876">toLowerOutput</span></span> | <span data-ttu-id="1a45f-877">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-877">String</span></span> | <span data-ttu-id="1a45f-878">um dois três</span><span class="sxs-lookup"><span data-stu-id="1a45f-878">one two three</span></span> |
| <span data-ttu-id="1a45f-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-879">toUpperOutput</span></span> | <span data-ttu-id="1a45f-880">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-880">String</span></span> | <span data-ttu-id="1a45f-881">UM DOIS TRÊS</span><span class="sxs-lookup"><span data-stu-id="1a45f-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="1a45f-882">cortar</span><span class="sxs-lookup"><span data-stu-id="1a45f-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="1a45f-883">Remove todos os caracteres de espaço em branco à esquerda e à direita da cadeia de caracteres especificada.</span><span class="sxs-lookup"><span data-stu-id="1a45f-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-884">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-884">Parameters</span></span>

| <span data-ttu-id="1a45f-885">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-885">Parameter</span></span> | <span data-ttu-id="1a45f-886">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-886">Required</span></span> | <span data-ttu-id="1a45f-887">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-887">Type</span></span> | <span data-ttu-id="1a45f-888">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="1a45f-889">stringToTrim</span></span> |<span data-ttu-id="1a45f-890">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-890">Yes</span></span> |<span data-ttu-id="1a45f-891">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-891">string</span></span> |<span data-ttu-id="1a45f-892">O valor de corte.</span><span class="sxs-lookup"><span data-stu-id="1a45f-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-893">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-893">Return value</span></span>

<span data-ttu-id="1a45f-894">A cadeia de caracteres sem caracteres de espaço em branco à esquerda e à direita.</span><span class="sxs-lookup"><span data-stu-id="1a45f-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-895">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-895">Examples</span></span>

<span data-ttu-id="1a45f-896">O exemplo a seguir remove os caracteres de espaço em branco do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1a45f-896">The following example trims the white-space characters from the parameter.</span></span>

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

<span data-ttu-id="1a45f-897">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-898">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-898">Name</span></span> | <span data-ttu-id="1a45f-899">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-899">Type</span></span> | <span data-ttu-id="1a45f-900">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-901">retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-901">return</span></span> | <span data-ttu-id="1a45f-902">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-902">String</span></span> | <span data-ttu-id="1a45f-903">um dois três</span><span class="sxs-lookup"><span data-stu-id="1a45f-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="1a45f-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="1a45f-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="1a45f-905">Cria uma cadeia de caracteres de hash determinístico com base nos valores fornecidos como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1a45f-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="1a45f-906">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-906">Parameters</span></span>

| <span data-ttu-id="1a45f-907">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-907">Parameter</span></span> | <span data-ttu-id="1a45f-908">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-908">Required</span></span> | <span data-ttu-id="1a45f-909">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-909">Type</span></span> | <span data-ttu-id="1a45f-910">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-911">baseString</span><span class="sxs-lookup"><span data-stu-id="1a45f-911">baseString</span></span> |<span data-ttu-id="1a45f-912">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-912">Yes</span></span> |<span data-ttu-id="1a45f-913">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-913">string</span></span> |<span data-ttu-id="1a45f-914">O valor usado na função de hash para criar uma cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="1a45f-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="1a45f-915">parâmetros extras conforme necessário</span><span class="sxs-lookup"><span data-stu-id="1a45f-915">additional parameters as needed</span></span> |<span data-ttu-id="1a45f-916">Não</span><span class="sxs-lookup"><span data-stu-id="1a45f-916">No</span></span> |<span data-ttu-id="1a45f-917">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-917">string</span></span> |<span data-ttu-id="1a45f-918">Você pode adicionar quantas cadeias de caracteres forem necessárias para criar o valor que especifica o nível de exclusividade.</span><span class="sxs-lookup"><span data-stu-id="1a45f-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="1a45f-919">Comentários</span><span class="sxs-lookup"><span data-stu-id="1a45f-919">Remarks</span></span>

<span data-ttu-id="1a45f-920">Essa função é útil quando você precisa criar um nome exclusivo para um recurso.</span><span class="sxs-lookup"><span data-stu-id="1a45f-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="1a45f-921">Você fornece valores de parâmetros que limitam o escopo de exclusividade para o resultado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="1a45f-922">Você pode especificar se o nome é exclusivo para a assinatura, grupo de recursos ou implantação.</span><span class="sxs-lookup"><span data-stu-id="1a45f-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="1a45f-923">O valor retornado não é uma cadeia de caracteres aleatória, mas sim o resultado de uma função de hash.</span><span class="sxs-lookup"><span data-stu-id="1a45f-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="1a45f-924">O valor retornado tem 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="1a45f-925">Não é globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="1a45f-925">It is not globally unique.</span></span> <span data-ttu-id="1a45f-926">Você talvez queira combinar o valor com um prefixo de sua convenção de nomenclatura para criar um nome significativo.</span><span class="sxs-lookup"><span data-stu-id="1a45f-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="1a45f-927">O exemplo a seguir mostra o formato do valor retornado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="1a45f-928">O valor real poderá variar de acordo com os parâmetros fornecidos.</span><span class="sxs-lookup"><span data-stu-id="1a45f-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="1a45f-929">Os exemplos a seguir mostram como usar uniqueString para criar um valor exclusivo para níveis usados com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="1a45f-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="1a45f-930">Escopo exclusivo para a assinatura</span><span class="sxs-lookup"><span data-stu-id="1a45f-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="1a45f-931">Escopo exclusivo para o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1a45f-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="1a45f-932">Escopo exclusivo para a implantação de um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1a45f-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="1a45f-933">O exemplo a seguir mostra como criar um nome exclusivo para uma conta de armazenamento com base em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1a45f-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="1a45f-934">Dentro do grupo de recursos, o nome não é exclusivo se for construído da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="1a45f-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="1a45f-935">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-935">Return value</span></span>

<span data-ttu-id="1a45f-936">Uma cadeia de caracteres que contém 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-937">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-937">Examples</span></span>

<span data-ttu-id="1a45f-938">O exemplo abaixo retorna os resultados de uniquestring:</span><span class="sxs-lookup"><span data-stu-id="1a45f-938">The following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="1a45f-939">uri</span><span class="sxs-lookup"><span data-stu-id="1a45f-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="1a45f-940">Cria um URI absoluto, combinando o baseUri e a cadeia de caracteres relativeUri.</span><span class="sxs-lookup"><span data-stu-id="1a45f-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-941">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-941">Parameters</span></span>

| <span data-ttu-id="1a45f-942">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-942">Parameter</span></span> | <span data-ttu-id="1a45f-943">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-943">Required</span></span> | <span data-ttu-id="1a45f-944">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-944">Type</span></span> | <span data-ttu-id="1a45f-945">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="1a45f-946">baseUri</span></span> |<span data-ttu-id="1a45f-947">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-947">Yes</span></span> |<span data-ttu-id="1a45f-948">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-948">string</span></span> |<span data-ttu-id="1a45f-949">Cadeia de caracteres do URI de base.</span><span class="sxs-lookup"><span data-stu-id="1a45f-949">The base uri string.</span></span> |
| <span data-ttu-id="1a45f-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="1a45f-950">relativeUri</span></span> |<span data-ttu-id="1a45f-951">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-951">Yes</span></span> |<span data-ttu-id="1a45f-952">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-952">string</span></span> |<span data-ttu-id="1a45f-953">Cadeia de caracteres de uri relativo para adicionar a cadeia de caracteres do uri de base.</span><span class="sxs-lookup"><span data-stu-id="1a45f-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="1a45f-954">O valor para o parâmetro **baseUri** pode incluir um arquivo específico, mas apenas o caminho base é usado ao construir a URI.</span><span class="sxs-lookup"><span data-stu-id="1a45f-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="1a45f-955">Por exemplo, transmitir `http://contoso.com/resources/azuredeploy.json` como parâmetro baseUri resultará em uma URI base de `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="1a45f-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="1a45f-956">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-956">Return value</span></span>

<span data-ttu-id="1a45f-957">Uma cadeia de caracteres que representa o URI absoluto dos valores base e relativos.</span><span class="sxs-lookup"><span data-stu-id="1a45f-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-958">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-958">Examples</span></span>

<span data-ttu-id="1a45f-959">O exemplo a seguir mostra como criar um link para um modelo aninhado com base no valor do modelo pai.</span><span class="sxs-lookup"><span data-stu-id="1a45f-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="1a45f-960">O seguinte exemplo mostra como usar uri, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="1a45f-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="1a45f-961">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-962">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-962">Name</span></span> | <span data-ttu-id="1a45f-963">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-963">Type</span></span> | <span data-ttu-id="1a45f-964">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-965">uriOutput</span></span> | <span data-ttu-id="1a45f-966">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-966">String</span></span> | <span data-ttu-id="1a45f-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="1a45f-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-968">componentOutput</span></span> | <span data-ttu-id="1a45f-969">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-969">String</span></span> | <span data-ttu-id="1a45f-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="1a45f-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-971">toStringOutput</span></span> | <span data-ttu-id="1a45f-972">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-972">String</span></span> | <span data-ttu-id="1a45f-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="1a45f-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="1a45f-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="1a45f-975">Codifica um URI.</span><span class="sxs-lookup"><span data-stu-id="1a45f-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-976">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-976">Parameters</span></span>

| <span data-ttu-id="1a45f-977">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-977">Parameter</span></span> | <span data-ttu-id="1a45f-978">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-978">Required</span></span> | <span data-ttu-id="1a45f-979">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-979">Type</span></span> | <span data-ttu-id="1a45f-980">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="1a45f-981">stringToEncode</span></span> |<span data-ttu-id="1a45f-982">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-982">Yes</span></span> |<span data-ttu-id="1a45f-983">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-983">string</span></span> |<span data-ttu-id="1a45f-984">O valor a ser codificado.</span><span class="sxs-lookup"><span data-stu-id="1a45f-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-985">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-985">Return value</span></span>

<span data-ttu-id="1a45f-986">Uma cadeia de caracteres do valor codificado em URI.</span><span class="sxs-lookup"><span data-stu-id="1a45f-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-987">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-987">Examples</span></span>

<span data-ttu-id="1a45f-988">O seguinte exemplo mostra como usar uri, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="1a45f-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="1a45f-989">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-990">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-990">Name</span></span> | <span data-ttu-id="1a45f-991">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-991">Type</span></span> | <span data-ttu-id="1a45f-992">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-993">uriOutput</span></span> | <span data-ttu-id="1a45f-994">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-994">String</span></span> | <span data-ttu-id="1a45f-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="1a45f-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-996">componentOutput</span></span> | <span data-ttu-id="1a45f-997">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-997">String</span></span> | <span data-ttu-id="1a45f-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="1a45f-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-999">toStringOutput</span></span> | <span data-ttu-id="1a45f-1000">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-1000">String</span></span> | <span data-ttu-id="1a45f-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="1a45f-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="1a45f-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="1a45f-1003">Retorna uma cadeia de caracteres de um valor codificado em URI.</span><span class="sxs-lookup"><span data-stu-id="1a45f-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a45f-1004">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a45f-1004">Parameters</span></span>

| <span data-ttu-id="1a45f-1005">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a45f-1005">Parameter</span></span> | <span data-ttu-id="1a45f-1006">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a45f-1006">Required</span></span> | <span data-ttu-id="1a45f-1007">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-1007">Type</span></span> | <span data-ttu-id="1a45f-1008">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a45f-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1a45f-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="1a45f-1009">uriEncodedString</span></span> |<span data-ttu-id="1a45f-1010">Sim</span><span class="sxs-lookup"><span data-stu-id="1a45f-1010">Yes</span></span> |<span data-ttu-id="1a45f-1011">string</span><span class="sxs-lookup"><span data-stu-id="1a45f-1011">string</span></span> |<span data-ttu-id="1a45f-1012">O valor codificado em URI a ser convertido em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1a45f-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1a45f-1013">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="1a45f-1013">Return value</span></span>

<span data-ttu-id="1a45f-1014">Uma cadeia de caracteres decodificada de valores codificados em URI.</span><span class="sxs-lookup"><span data-stu-id="1a45f-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="1a45f-1015">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a45f-1015">Examples</span></span>

<span data-ttu-id="1a45f-1016">O seguinte exemplo mostra como usar uri, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="1a45f-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="1a45f-1017">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="1a45f-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1a45f-1018">Nome</span><span class="sxs-lookup"><span data-stu-id="1a45f-1018">Name</span></span> | <span data-ttu-id="1a45f-1019">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a45f-1019">Type</span></span> | <span data-ttu-id="1a45f-1020">Valor</span><span class="sxs-lookup"><span data-stu-id="1a45f-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1a45f-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-1021">uriOutput</span></span> | <span data-ttu-id="1a45f-1022">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-1022">String</span></span> | <span data-ttu-id="1a45f-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="1a45f-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-1024">componentOutput</span></span> | <span data-ttu-id="1a45f-1025">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-1025">String</span></span> | <span data-ttu-id="1a45f-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="1a45f-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1a45f-1027">toStringOutput</span></span> | <span data-ttu-id="1a45f-1028">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1a45f-1028">String</span></span> | <span data-ttu-id="1a45f-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a45f-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1a45f-1030">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a45f-1030">Next steps</span></span>
* <span data-ttu-id="1a45f-1031">Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1a45f-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="1a45f-1032">Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1a45f-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="1a45f-1033">Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1a45f-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="1a45f-1034">Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1a45f-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

