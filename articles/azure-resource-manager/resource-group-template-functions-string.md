---
title: "a cadeia de caracteres de funções de modelo do Gerenciador de recursos de aaaAzure - | Microsoft Docs"
description: "Descreve Olá toouse de funções em um toowork de modelo do Gerenciador de recursos do Azure com cadeias de caracteres."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="b573f-103">Funções de cadeia de caracteres para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b573f-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="b573f-104">Gerenciador de recursos fornece Olá funções para trabalhar com cadeias de caracteres a seguir:</span><span class="sxs-lookup"><span data-stu-id="b573f-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="b573f-105">base64</span><span class="sxs-lookup"><span data-stu-id="b573f-105">base64</span></span>](#base64)
* [<span data-ttu-id="b573f-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="b573f-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="b573f-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="b573f-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="b573f-108">concat</span><span class="sxs-lookup"><span data-stu-id="b573f-108">concat</span></span>](#concat)
* [<span data-ttu-id="b573f-109">contains</span><span class="sxs-lookup"><span data-stu-id="b573f-109">contains</span></span>](#contains)
* [<span data-ttu-id="b573f-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="b573f-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="b573f-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="b573f-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="b573f-112">empty</span><span class="sxs-lookup"><span data-stu-id="b573f-112">empty</span></span>](#empty)
* [<span data-ttu-id="b573f-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="b573f-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="b573f-114">first</span><span class="sxs-lookup"><span data-stu-id="b573f-114">first</span></span>](#first)
* [<span data-ttu-id="b573f-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="b573f-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="b573f-116">last</span><span class="sxs-lookup"><span data-stu-id="b573f-116">last</span></span>](#last)
* [<span data-ttu-id="b573f-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="b573f-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="b573f-118">length</span><span class="sxs-lookup"><span data-stu-id="b573f-118">length</span></span>](#length)
* [<span data-ttu-id="b573f-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="b573f-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="b573f-120">substitui</span><span class="sxs-lookup"><span data-stu-id="b573f-120">replace</span></span>](#replace)
* [<span data-ttu-id="b573f-121">skip</span><span class="sxs-lookup"><span data-stu-id="b573f-121">skip</span></span>](#skip)
* [<span data-ttu-id="b573f-122">split</span><span class="sxs-lookup"><span data-stu-id="b573f-122">split</span></span>](#split)
* [<span data-ttu-id="b573f-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="b573f-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="b573f-124">string</span><span class="sxs-lookup"><span data-stu-id="b573f-124">string</span></span>](#string)
* [<span data-ttu-id="b573f-125">substring</span><span class="sxs-lookup"><span data-stu-id="b573f-125">substring</span></span>](#substring)
* [<span data-ttu-id="b573f-126">take</span><span class="sxs-lookup"><span data-stu-id="b573f-126">take</span></span>](#take)
* [<span data-ttu-id="b573f-127">toLower</span><span class="sxs-lookup"><span data-stu-id="b573f-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="b573f-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="b573f-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="b573f-129">cortar</span><span class="sxs-lookup"><span data-stu-id="b573f-129">trim</span></span>](#trim)
* [<span data-ttu-id="b573f-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="b573f-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="b573f-131">uri</span><span class="sxs-lookup"><span data-stu-id="b573f-131">uri</span></span>](#uri)
* [<span data-ttu-id="b573f-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="b573f-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="b573f-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="b573f-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="b573f-134">base64</span><span class="sxs-lookup"><span data-stu-id="b573f-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="b573f-135">Retorna Olá representação de cadeia de caracteres de entrada hello base 64.</span><span class="sxs-lookup"><span data-stu-id="b573f-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-136">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-136">Parameters</span></span>

| <span data-ttu-id="b573f-137">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-137">Parameter</span></span> | <span data-ttu-id="b573f-138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-138">Required</span></span> | <span data-ttu-id="b573f-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-139">Type</span></span> | <span data-ttu-id="b573f-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-141">inputString</span><span class="sxs-lookup"><span data-stu-id="b573f-141">inputString</span></span> |<span data-ttu-id="b573f-142">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-142">Yes</span></span> |<span data-ttu-id="b573f-143">string</span><span class="sxs-lookup"><span data-stu-id="b573f-143">string</span></span> |<span data-ttu-id="b573f-144">Olá tooreturn valor como uma representação em base64.</span><span class="sxs-lookup"><span data-stu-id="b573f-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-145">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-145">Return value</span></span>

<span data-ttu-id="b573f-146">Uma cadeia de caracteres que contém a representação de base64 hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-147">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-147">Examples</span></span>

<span data-ttu-id="b573f-148">saudação de exemplo a seguir mostra como toouse Olá função base64.</span><span class="sxs-lookup"><span data-stu-id="b573f-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="b573f-149">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-150">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-150">Name</span></span> | <span data-ttu-id="b573f-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-151">Type</span></span> | <span data-ttu-id="b573f-152">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="b573f-153">base64Output</span></span> | <span data-ttu-id="b573f-154">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-154">String</span></span> | <span data-ttu-id="b573f-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="b573f-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="b573f-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-156">toStringOutput</span></span> | <span data-ttu-id="b573f-157">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-157">String</span></span> | <span data-ttu-id="b573f-158">um, dois, três</span><span class="sxs-lookup"><span data-stu-id="b573f-158">one, two, three</span></span> |
| <span data-ttu-id="b573f-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-159">toJsonOutput</span></span> | <span data-ttu-id="b573f-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="b573f-160">Object</span></span> | <span data-ttu-id="b573f-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="b573f-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="b573f-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="b573f-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="b573f-163">Converte um objeto JSON de tooa de representação de base64.</span><span class="sxs-lookup"><span data-stu-id="b573f-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-164">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-164">Parameters</span></span>

| <span data-ttu-id="b573f-165">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-165">Parameter</span></span> | <span data-ttu-id="b573f-166">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-166">Required</span></span> | <span data-ttu-id="b573f-167">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-167">Type</span></span> | <span data-ttu-id="b573f-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="b573f-169">base64Value</span></span> |<span data-ttu-id="b573f-170">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-170">Yes</span></span> |<span data-ttu-id="b573f-171">string</span><span class="sxs-lookup"><span data-stu-id="b573f-171">string</span></span> |<span data-ttu-id="b573f-172">objeto Olá base64 representação tooconvert tooa JSON.</span><span class="sxs-lookup"><span data-stu-id="b573f-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-173">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-173">Return value</span></span>

<span data-ttu-id="b573f-174">Um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="b573f-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-175">Examples</span></span>

<span data-ttu-id="b573f-176">Olá, exemplo a seguir usa Olá base64ToJson função tooconvert um valor base64:</span><span class="sxs-lookup"><span data-stu-id="b573f-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="b573f-177">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-178">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-178">Name</span></span> | <span data-ttu-id="b573f-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-179">Type</span></span> | <span data-ttu-id="b573f-180">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="b573f-181">base64Output</span></span> | <span data-ttu-id="b573f-182">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-182">String</span></span> | <span data-ttu-id="b573f-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="b573f-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="b573f-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-184">toStringOutput</span></span> | <span data-ttu-id="b573f-185">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-185">String</span></span> | <span data-ttu-id="b573f-186">um, dois, três</span><span class="sxs-lookup"><span data-stu-id="b573f-186">one, two, three</span></span> |
| <span data-ttu-id="b573f-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-187">toJsonOutput</span></span> | <span data-ttu-id="b573f-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="b573f-188">Object</span></span> | <span data-ttu-id="b573f-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="b573f-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="b573f-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="b573f-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="b573f-191">Converte uma cadeia de caracteres base64 representação tooa.</span><span class="sxs-lookup"><span data-stu-id="b573f-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-192">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-192">Parameters</span></span>

| <span data-ttu-id="b573f-193">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-193">Parameter</span></span> | <span data-ttu-id="b573f-194">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-194">Required</span></span> | <span data-ttu-id="b573f-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-195">Type</span></span> | <span data-ttu-id="b573f-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="b573f-197">base64Value</span></span> |<span data-ttu-id="b573f-198">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-198">Yes</span></span> |<span data-ttu-id="b573f-199">string</span><span class="sxs-lookup"><span data-stu-id="b573f-199">string</span></span> |<span data-ttu-id="b573f-200">cadeia de caracteres do Hello base64 representação tooconvert tooa.</span><span class="sxs-lookup"><span data-stu-id="b573f-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-201">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-201">Return value</span></span>

<span data-ttu-id="b573f-202">Uma cadeia de caracteres de saudação convertido valor base64.</span><span class="sxs-lookup"><span data-stu-id="b573f-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-203">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-203">Examples</span></span>

<span data-ttu-id="b573f-204">Olá, exemplo a seguir usa Olá base64ToString função tooconvert um valor base64:</span><span class="sxs-lookup"><span data-stu-id="b573f-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="b573f-205">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-206">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-206">Name</span></span> | <span data-ttu-id="b573f-207">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-207">Type</span></span> | <span data-ttu-id="b573f-208">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="b573f-209">base64Output</span></span> | <span data-ttu-id="b573f-210">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-210">String</span></span> | <span data-ttu-id="b573f-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="b573f-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="b573f-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-212">toStringOutput</span></span> | <span data-ttu-id="b573f-213">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-213">String</span></span> | <span data-ttu-id="b573f-214">um, dois, três</span><span class="sxs-lookup"><span data-stu-id="b573f-214">one, two, three</span></span> |
| <span data-ttu-id="b573f-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-215">toJsonOutput</span></span> | <span data-ttu-id="b573f-216">Objeto</span><span class="sxs-lookup"><span data-stu-id="b573f-216">Object</span></span> | <span data-ttu-id="b573f-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="b573f-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="b573f-218">concat</span><span class="sxs-lookup"><span data-stu-id="b573f-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="b573f-219">Combina vários valores de cadeia de caracteres e retorna a cadeia de caracteres hello concatenado, ou combina vários conjuntos e retorna a matriz Olá concatenado.</span><span class="sxs-lookup"><span data-stu-id="b573f-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-220">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-220">Parameters</span></span>

| <span data-ttu-id="b573f-221">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-221">Parameter</span></span> | <span data-ttu-id="b573f-222">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-222">Required</span></span> | <span data-ttu-id="b573f-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-223">Type</span></span> | <span data-ttu-id="b573f-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-225">arg1</span><span class="sxs-lookup"><span data-stu-id="b573f-225">arg1</span></span> |<span data-ttu-id="b573f-226">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-226">Yes</span></span> |<span data-ttu-id="b573f-227">cadeia de caracteres ou matriz</span><span class="sxs-lookup"><span data-stu-id="b573f-227">string or array</span></span> |<span data-ttu-id="b573f-228">primeiro valor de concatenação Hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="b573f-229">argumentos adicionais</span><span class="sxs-lookup"><span data-stu-id="b573f-229">additional arguments</span></span> |<span data-ttu-id="b573f-230">Não</span><span class="sxs-lookup"><span data-stu-id="b573f-230">No</span></span> |<span data-ttu-id="b573f-231">string</span><span class="sxs-lookup"><span data-stu-id="b573f-231">string</span></span> |<span data-ttu-id="b573f-232">Valores adicionais em ordem sequencial para concatenação.</span><span class="sxs-lookup"><span data-stu-id="b573f-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-233">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-233">Return value</span></span>
<span data-ttu-id="b573f-234">Uma cadeia de caracteres ou matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="b573f-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-235">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-235">Examples</span></span>

<span data-ttu-id="b573f-236">saudação de exemplo a seguir mostra como toocombine dois valores de cadeia de caracteres e retorna uma cadeia de caracteres concatenada.</span><span class="sxs-lookup"><span data-stu-id="b573f-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="b573f-237">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-238">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-238">Name</span></span> | <span data-ttu-id="b573f-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-239">Type</span></span> | <span data-ttu-id="b573f-240">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-241">concatOutput</span></span> | <span data-ttu-id="b573f-242">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-242">String</span></span> | <span data-ttu-id="b573f-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="b573f-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="b573f-244">saudação de exemplo a seguir mostra como toocombine duas matrizes.</span><span class="sxs-lookup"><span data-stu-id="b573f-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="b573f-245">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-246">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-246">Name</span></span> | <span data-ttu-id="b573f-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-247">Type</span></span> | <span data-ttu-id="b573f-248">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-249">retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-249">return</span></span> | <span data-ttu-id="b573f-250">Matriz</span><span class="sxs-lookup"><span data-stu-id="b573f-250">Array</span></span> | <span data-ttu-id="b573f-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="b573f-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="b573f-252">contains</span><span class="sxs-lookup"><span data-stu-id="b573f-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="b573f-253">Verifica se uma matriz contém um valor, um objeto contém uma chave ou uma cadeia de caracteres contém uma subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-254">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-254">Parameters</span></span>

| <span data-ttu-id="b573f-255">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-255">Parameter</span></span> | <span data-ttu-id="b573f-256">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-256">Required</span></span> | <span data-ttu-id="b573f-257">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-257">Type</span></span> | <span data-ttu-id="b573f-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-259">contêiner</span><span class="sxs-lookup"><span data-stu-id="b573f-259">container</span></span> |<span data-ttu-id="b573f-260">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-260">Yes</span></span> |<span data-ttu-id="b573f-261">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-261">array, object, or string</span></span> |<span data-ttu-id="b573f-262">valor de saudação que contém Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="b573f-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="b573f-263">itemToFind</span></span> |<span data-ttu-id="b573f-264">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-264">Yes</span></span> |<span data-ttu-id="b573f-265">string ou int</span><span class="sxs-lookup"><span data-stu-id="b573f-265">string or int</span></span> |<span data-ttu-id="b573f-266">Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-267">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-267">Return value</span></span>

<span data-ttu-id="b573f-268">**True** se o item de saudação for encontrado; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="b573f-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-269">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-269">Examples</span></span>

<span data-ttu-id="b573f-270">Olá exemplo a seguir mostra como toouse contém com tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="b573f-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="b573f-271">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-272">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-272">Name</span></span> | <span data-ttu-id="b573f-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-273">Type</span></span> | <span data-ttu-id="b573f-274">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-275">stringTrue</span></span> | <span data-ttu-id="b573f-276">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-276">Bool</span></span> | <span data-ttu-id="b573f-277">True </span><span class="sxs-lookup"><span data-stu-id="b573f-277">True</span></span> |
| <span data-ttu-id="b573f-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-278">stringFalse</span></span> | <span data-ttu-id="b573f-279">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-279">Bool</span></span> | <span data-ttu-id="b573f-280">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-280">False</span></span> |
| <span data-ttu-id="b573f-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-281">objectTrue</span></span> | <span data-ttu-id="b573f-282">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-282">Bool</span></span> | <span data-ttu-id="b573f-283">True </span><span class="sxs-lookup"><span data-stu-id="b573f-283">True</span></span> |
| <span data-ttu-id="b573f-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-284">objectFalse</span></span> | <span data-ttu-id="b573f-285">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-285">Bool</span></span> | <span data-ttu-id="b573f-286">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-286">False</span></span> |
| <span data-ttu-id="b573f-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-287">arrayTrue</span></span> | <span data-ttu-id="b573f-288">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-288">Bool</span></span> | <span data-ttu-id="b573f-289">True </span><span class="sxs-lookup"><span data-stu-id="b573f-289">True</span></span> |
| <span data-ttu-id="b573f-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-290">arrayFalse</span></span> | <span data-ttu-id="b573f-291">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-291">Bool</span></span> | <span data-ttu-id="b573f-292">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="b573f-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="b573f-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="b573f-294">Converte um dado do valor tooa URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-295">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-295">Parameters</span></span>

| <span data-ttu-id="b573f-296">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-296">Parameter</span></span> | <span data-ttu-id="b573f-297">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-297">Required</span></span> | <span data-ttu-id="b573f-298">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-298">Type</span></span> | <span data-ttu-id="b573f-299">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="b573f-300">stringToConvert</span></span> |<span data-ttu-id="b573f-301">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-301">Yes</span></span> |<span data-ttu-id="b573f-302">string</span><span class="sxs-lookup"><span data-stu-id="b573f-302">string</span></span> |<span data-ttu-id="b573f-303">Olá tooconvert tooa dados de valor URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-304">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-304">Return value</span></span>

<span data-ttu-id="b573f-305">Uma cadeia de caracteres formatada como um URI de dados.</span><span class="sxs-lookup"><span data-stu-id="b573f-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-306">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-306">Examples</span></span>

<span data-ttu-id="b573f-307">saudação de exemplo a seguir converte um dado do valor tooa URI e converte uma cadeia de caracteres do URI tooa de dados:</span><span class="sxs-lookup"><span data-stu-id="b573f-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="b573f-308">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-309">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-309">Name</span></span> | <span data-ttu-id="b573f-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-310">Type</span></span> | <span data-ttu-id="b573f-311">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-312">dataUriOutput</span></span> | <span data-ttu-id="b573f-313">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-313">String</span></span> | <span data-ttu-id="b573f-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="b573f-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="b573f-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-315">toStringOutput</span></span> | <span data-ttu-id="b573f-316">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-316">String</span></span> | <span data-ttu-id="b573f-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="b573f-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="b573f-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="b573f-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="b573f-319">Converte um URI de dados formatados de cadeia de caracteres do valor tooa.</span><span class="sxs-lookup"><span data-stu-id="b573f-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-320">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-320">Parameters</span></span>

| <span data-ttu-id="b573f-321">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-321">Parameter</span></span> | <span data-ttu-id="b573f-322">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-322">Required</span></span> | <span data-ttu-id="b573f-323">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-323">Type</span></span> | <span data-ttu-id="b573f-324">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="b573f-325">dataUriToConvert</span></span> |<span data-ttu-id="b573f-326">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-326">Yes</span></span> |<span data-ttu-id="b573f-327">string</span><span class="sxs-lookup"><span data-stu-id="b573f-327">string</span></span> |<span data-ttu-id="b573f-328">dados de saudação tooconvert de valor do URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-329">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-329">Return value</span></span>

<span data-ttu-id="b573f-330">Uma cadeia de caracteres que contém a saudação convertido valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-331">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-331">Examples</span></span>

<span data-ttu-id="b573f-332">saudação de exemplo a seguir converte um dado do valor tooa URI e converte uma cadeia de caracteres do URI tooa de dados:</span><span class="sxs-lookup"><span data-stu-id="b573f-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="b573f-333">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-334">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-334">Name</span></span> | <span data-ttu-id="b573f-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-335">Type</span></span> | <span data-ttu-id="b573f-336">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-337">dataUriOutput</span></span> | <span data-ttu-id="b573f-338">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-338">String</span></span> | <span data-ttu-id="b573f-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="b573f-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="b573f-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-340">toStringOutput</span></span> | <span data-ttu-id="b573f-341">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-341">String</span></span> | <span data-ttu-id="b573f-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="b573f-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="b573f-343">empty</span><span class="sxs-lookup"><span data-stu-id="b573f-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="b573f-344">Determina se uma matriz, objeto ou uma cadeia de caracteres está vazio.</span><span class="sxs-lookup"><span data-stu-id="b573f-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-345">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-345">Parameters</span></span>

| <span data-ttu-id="b573f-346">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-346">Parameter</span></span> | <span data-ttu-id="b573f-347">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-347">Required</span></span> | <span data-ttu-id="b573f-348">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-348">Type</span></span> | <span data-ttu-id="b573f-349">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="b573f-350">itemToTest</span></span> |<span data-ttu-id="b573f-351">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-351">Yes</span></span> |<span data-ttu-id="b573f-352">matriz, objeto ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-352">array, object, or string</span></span> |<span data-ttu-id="b573f-353">Olá toocheck valor se ele estiver vazio.</span><span class="sxs-lookup"><span data-stu-id="b573f-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-354">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-354">Return value</span></span>

<span data-ttu-id="b573f-355">Retorna **True** se o valor de saudação está vazio; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="b573f-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-356">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-356">Examples</span></span>

<span data-ttu-id="b573f-357">saudação de exemplo a seguir verifica se uma matriz, objeto e a cadeia de caracteres estão vazios.</span><span class="sxs-lookup"><span data-stu-id="b573f-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="b573f-358">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-359">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-359">Name</span></span> | <span data-ttu-id="b573f-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-360">Type</span></span> | <span data-ttu-id="b573f-361">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="b573f-362">arrayEmpty</span></span> | <span data-ttu-id="b573f-363">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-363">Bool</span></span> | <span data-ttu-id="b573f-364">True </span><span class="sxs-lookup"><span data-stu-id="b573f-364">True</span></span> |
| <span data-ttu-id="b573f-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="b573f-365">objectEmpty</span></span> | <span data-ttu-id="b573f-366">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-366">Bool</span></span> | <span data-ttu-id="b573f-367">True </span><span class="sxs-lookup"><span data-stu-id="b573f-367">True</span></span> |
| <span data-ttu-id="b573f-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="b573f-368">stringEmpty</span></span> | <span data-ttu-id="b573f-369">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-369">Bool</span></span> | <span data-ttu-id="b573f-370">True </span><span class="sxs-lookup"><span data-stu-id="b573f-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="b573f-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="b573f-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="b573f-372">Determina se uma cadeia de caracteres termina com um valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="b573f-373">comparação de saudação diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b573f-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-374">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-374">Parameters</span></span>

| <span data-ttu-id="b573f-375">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-375">Parameter</span></span> | <span data-ttu-id="b573f-376">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-376">Required</span></span> | <span data-ttu-id="b573f-377">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-377">Type</span></span> | <span data-ttu-id="b573f-378">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b573f-379">stringToSearch</span></span> |<span data-ttu-id="b573f-380">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-380">Yes</span></span> |<span data-ttu-id="b573f-381">string</span><span class="sxs-lookup"><span data-stu-id="b573f-381">string</span></span> |<span data-ttu-id="b573f-382">valor de saudação que contém Olá toofind de item.</span><span class="sxs-lookup"><span data-stu-id="b573f-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b573f-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b573f-383">stringToFind</span></span> |<span data-ttu-id="b573f-384">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-384">Yes</span></span> |<span data-ttu-id="b573f-385">string</span><span class="sxs-lookup"><span data-stu-id="b573f-385">string</span></span> |<span data-ttu-id="b573f-386">Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-387">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-387">Return value</span></span>

<span data-ttu-id="b573f-388">**True** se Olá último ou mais caracteres de cadeia de caracteres hello corresponder ao valor de saudação; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="b573f-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-389">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-389">Examples</span></span>

<span data-ttu-id="b573f-390">saudação de exemplo a seguir mostra como toouse Olá startsWith e endsWith funções:</span><span class="sxs-lookup"><span data-stu-id="b573f-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="b573f-391">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-392">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-392">Name</span></span> | <span data-ttu-id="b573f-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-393">Type</span></span> | <span data-ttu-id="b573f-394">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-395">startsTrue</span></span> | <span data-ttu-id="b573f-396">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-396">Bool</span></span> | <span data-ttu-id="b573f-397">True </span><span class="sxs-lookup"><span data-stu-id="b573f-397">True</span></span> |
| <span data-ttu-id="b573f-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-398">startsCapTrue</span></span> | <span data-ttu-id="b573f-399">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-399">Bool</span></span> | <span data-ttu-id="b573f-400">True </span><span class="sxs-lookup"><span data-stu-id="b573f-400">True</span></span> |
| <span data-ttu-id="b573f-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-401">startsFalse</span></span> | <span data-ttu-id="b573f-402">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-402">Bool</span></span> | <span data-ttu-id="b573f-403">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-403">False</span></span> |
| <span data-ttu-id="b573f-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-404">endsTrue</span></span> | <span data-ttu-id="b573f-405">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-405">Bool</span></span> | <span data-ttu-id="b573f-406">True </span><span class="sxs-lookup"><span data-stu-id="b573f-406">True</span></span> |
| <span data-ttu-id="b573f-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-407">endsCapTrue</span></span> | <span data-ttu-id="b573f-408">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-408">Bool</span></span> | <span data-ttu-id="b573f-409">True </span><span class="sxs-lookup"><span data-stu-id="b573f-409">True</span></span> |
| <span data-ttu-id="b573f-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-410">endsFalse</span></span> | <span data-ttu-id="b573f-411">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-411">Bool</span></span> | <span data-ttu-id="b573f-412">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="b573f-413">first</span><span class="sxs-lookup"><span data-stu-id="b573f-413">first</span></span>
`first(arg1)`

<span data-ttu-id="b573f-414">Retorna Olá primeiro caractere da cadeia de caracteres de saudação ou o primeiro elemento da matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-415">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-415">Parameters</span></span>

| <span data-ttu-id="b573f-416">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-416">Parameter</span></span> | <span data-ttu-id="b573f-417">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-417">Required</span></span> | <span data-ttu-id="b573f-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-418">Type</span></span> | <span data-ttu-id="b573f-419">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-420">arg1</span><span class="sxs-lookup"><span data-stu-id="b573f-420">arg1</span></span> |<span data-ttu-id="b573f-421">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-421">Yes</span></span> |<span data-ttu-id="b573f-422">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-422">array or string</span></span> |<span data-ttu-id="b573f-423">Olá valor tooretrieve Olá primeiro elemento ou um caractere.</span><span class="sxs-lookup"><span data-stu-id="b573f-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-424">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-424">Return value</span></span>

<span data-ttu-id="b573f-425">Uma cadeia de caracteres primeiro hello, ou tipo hello (string, int, matriz ou objeto) do primeiro elemento Olá em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="b573f-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-426">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-426">Examples</span></span>

<span data-ttu-id="b573f-427">Olá exemplo a seguir mostra como toouse Olá primeira função com uma matriz e a cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="b573f-428">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-429">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-429">Name</span></span> | <span data-ttu-id="b573f-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-430">Type</span></span> | <span data-ttu-id="b573f-431">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-432">arrayOutput</span></span> | <span data-ttu-id="b573f-433">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-433">String</span></span> | <span data-ttu-id="b573f-434">one</span><span class="sxs-lookup"><span data-stu-id="b573f-434">one</span></span> |
| <span data-ttu-id="b573f-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-435">stringOutput</span></span> | <span data-ttu-id="b573f-436">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-436">String</span></span> | <span data-ttu-id="b573f-437">O</span><span class="sxs-lookup"><span data-stu-id="b573f-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="b573f-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="b573f-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="b573f-439">Retorna Olá primeira posição de um valor em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="b573f-440">comparação de saudação diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b573f-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-441">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-441">Parameters</span></span>

| <span data-ttu-id="b573f-442">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-442">Parameter</span></span> | <span data-ttu-id="b573f-443">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-443">Required</span></span> | <span data-ttu-id="b573f-444">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-444">Type</span></span> | <span data-ttu-id="b573f-445">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b573f-446">stringToSearch</span></span> |<span data-ttu-id="b573f-447">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-447">Yes</span></span> |<span data-ttu-id="b573f-448">string</span><span class="sxs-lookup"><span data-stu-id="b573f-448">string</span></span> |<span data-ttu-id="b573f-449">valor de saudação que contém Olá toofind de item.</span><span class="sxs-lookup"><span data-stu-id="b573f-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b573f-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b573f-450">stringToFind</span></span> |<span data-ttu-id="b573f-451">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-451">Yes</span></span> |<span data-ttu-id="b573f-452">string</span><span class="sxs-lookup"><span data-stu-id="b573f-452">string</span></span> |<span data-ttu-id="b573f-453">Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-454">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-454">Return value</span></span>

<span data-ttu-id="b573f-455">Um inteiro que representa a posição de saudação do hello toofind de item.</span><span class="sxs-lookup"><span data-stu-id="b573f-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="b573f-456">valor de saudação é baseado em zero.</span><span class="sxs-lookup"><span data-stu-id="b573f-456">hello value is zero-based.</span></span> <span data-ttu-id="b573f-457">Se o item de saudação não for encontrado, -1 será retornado.</span><span class="sxs-lookup"><span data-stu-id="b573f-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-458">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-458">Examples</span></span>

<span data-ttu-id="b573f-459">saudação de exemplo a seguir mostra como toouse Olá indexOf e lastIndexOf funções:</span><span class="sxs-lookup"><span data-stu-id="b573f-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="b573f-460">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-461">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-461">Name</span></span> | <span data-ttu-id="b573f-462">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-462">Type</span></span> | <span data-ttu-id="b573f-463">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-464">firstT</span><span class="sxs-lookup"><span data-stu-id="b573f-464">firstT</span></span> | <span data-ttu-id="b573f-465">int</span><span class="sxs-lookup"><span data-stu-id="b573f-465">Int</span></span> | <span data-ttu-id="b573f-466">0</span><span class="sxs-lookup"><span data-stu-id="b573f-466">0</span></span> |
| <span data-ttu-id="b573f-467">lastT</span><span class="sxs-lookup"><span data-stu-id="b573f-467">lastT</span></span> | <span data-ttu-id="b573f-468">int</span><span class="sxs-lookup"><span data-stu-id="b573f-468">Int</span></span> | <span data-ttu-id="b573f-469">3</span><span class="sxs-lookup"><span data-stu-id="b573f-469">3</span></span> |
| <span data-ttu-id="b573f-470">firstString</span><span class="sxs-lookup"><span data-stu-id="b573f-470">firstString</span></span> | <span data-ttu-id="b573f-471">int</span><span class="sxs-lookup"><span data-stu-id="b573f-471">Int</span></span> | <span data-ttu-id="b573f-472">2</span><span class="sxs-lookup"><span data-stu-id="b573f-472">2</span></span> |
| <span data-ttu-id="b573f-473">lastString</span><span class="sxs-lookup"><span data-stu-id="b573f-473">lastString</span></span> | <span data-ttu-id="b573f-474">int</span><span class="sxs-lookup"><span data-stu-id="b573f-474">Int</span></span> | <span data-ttu-id="b573f-475">0</span><span class="sxs-lookup"><span data-stu-id="b573f-475">0</span></span> |
| <span data-ttu-id="b573f-476">NotFound</span><span class="sxs-lookup"><span data-stu-id="b573f-476">notFound</span></span> | <span data-ttu-id="b573f-477">int</span><span class="sxs-lookup"><span data-stu-id="b573f-477">Int</span></span> | <span data-ttu-id="b573f-478">-1</span><span class="sxs-lookup"><span data-stu-id="b573f-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="b573f-479">last</span><span class="sxs-lookup"><span data-stu-id="b573f-479">last</span></span>
`last (arg1)`

<span data-ttu-id="b573f-480">Retorna a última caractere da cadeia de caracteres de saudação ou último elemento Olá da matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-481">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-481">Parameters</span></span>

| <span data-ttu-id="b573f-482">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-482">Parameter</span></span> | <span data-ttu-id="b573f-483">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-483">Required</span></span> | <span data-ttu-id="b573f-484">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-484">Type</span></span> | <span data-ttu-id="b573f-485">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-486">arg1</span><span class="sxs-lookup"><span data-stu-id="b573f-486">arg1</span></span> |<span data-ttu-id="b573f-487">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-487">Yes</span></span> |<span data-ttu-id="b573f-488">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-488">array or string</span></span> |<span data-ttu-id="b573f-489">Olá valor tooretrieve Olá último elemento ou um caractere.</span><span class="sxs-lookup"><span data-stu-id="b573f-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-490">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-490">Return value</span></span>

<span data-ttu-id="b573f-491">Uma cadeia de caracteres última hello ou tipo de saudação (string, int, matriz ou objeto) do hello último elemento em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="b573f-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-492">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-492">Examples</span></span>

<span data-ttu-id="b573f-493">Olá exemplo a seguir mostra como toouse Olá última função com uma matriz e a cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="b573f-494">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-495">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-495">Name</span></span> | <span data-ttu-id="b573f-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-496">Type</span></span> | <span data-ttu-id="b573f-497">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-498">arrayOutput</span></span> | <span data-ttu-id="b573f-499">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-499">String</span></span> | <span data-ttu-id="b573f-500">três</span><span class="sxs-lookup"><span data-stu-id="b573f-500">three</span></span> |
| <span data-ttu-id="b573f-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-501">stringOutput</span></span> | <span data-ttu-id="b573f-502">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-502">String</span></span> | <span data-ttu-id="b573f-503">e</span><span class="sxs-lookup"><span data-stu-id="b573f-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="b573f-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="b573f-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="b573f-505">Retorna Olá última posição de um valor em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="b573f-506">comparação de saudação diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b573f-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-507">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-507">Parameters</span></span>

| <span data-ttu-id="b573f-508">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-508">Parameter</span></span> | <span data-ttu-id="b573f-509">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-509">Required</span></span> | <span data-ttu-id="b573f-510">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-510">Type</span></span> | <span data-ttu-id="b573f-511">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b573f-512">stringToSearch</span></span> |<span data-ttu-id="b573f-513">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-513">Yes</span></span> |<span data-ttu-id="b573f-514">string</span><span class="sxs-lookup"><span data-stu-id="b573f-514">string</span></span> |<span data-ttu-id="b573f-515">valor de saudação que contém Olá toofind de item.</span><span class="sxs-lookup"><span data-stu-id="b573f-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b573f-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b573f-516">stringToFind</span></span> |<span data-ttu-id="b573f-517">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-517">Yes</span></span> |<span data-ttu-id="b573f-518">string</span><span class="sxs-lookup"><span data-stu-id="b573f-518">string</span></span> |<span data-ttu-id="b573f-519">Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-520">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-520">Return value</span></span>

<span data-ttu-id="b573f-521">Um inteiro que representa a última posição Olá da saudação toofind de item.</span><span class="sxs-lookup"><span data-stu-id="b573f-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="b573f-522">valor de saudação é baseado em zero.</span><span class="sxs-lookup"><span data-stu-id="b573f-522">hello value is zero-based.</span></span> <span data-ttu-id="b573f-523">Se o item de saudação não for encontrado, -1 será retornado.</span><span class="sxs-lookup"><span data-stu-id="b573f-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-524">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-524">Examples</span></span>

<span data-ttu-id="b573f-525">saudação de exemplo a seguir mostra como toouse Olá indexOf e lastIndexOf funções:</span><span class="sxs-lookup"><span data-stu-id="b573f-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="b573f-526">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-527">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-527">Name</span></span> | <span data-ttu-id="b573f-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-528">Type</span></span> | <span data-ttu-id="b573f-529">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-530">firstT</span><span class="sxs-lookup"><span data-stu-id="b573f-530">firstT</span></span> | <span data-ttu-id="b573f-531">int</span><span class="sxs-lookup"><span data-stu-id="b573f-531">Int</span></span> | <span data-ttu-id="b573f-532">0</span><span class="sxs-lookup"><span data-stu-id="b573f-532">0</span></span> |
| <span data-ttu-id="b573f-533">lastT</span><span class="sxs-lookup"><span data-stu-id="b573f-533">lastT</span></span> | <span data-ttu-id="b573f-534">int</span><span class="sxs-lookup"><span data-stu-id="b573f-534">Int</span></span> | <span data-ttu-id="b573f-535">3</span><span class="sxs-lookup"><span data-stu-id="b573f-535">3</span></span> |
| <span data-ttu-id="b573f-536">firstString</span><span class="sxs-lookup"><span data-stu-id="b573f-536">firstString</span></span> | <span data-ttu-id="b573f-537">int</span><span class="sxs-lookup"><span data-stu-id="b573f-537">Int</span></span> | <span data-ttu-id="b573f-538">2</span><span class="sxs-lookup"><span data-stu-id="b573f-538">2</span></span> |
| <span data-ttu-id="b573f-539">lastString</span><span class="sxs-lookup"><span data-stu-id="b573f-539">lastString</span></span> | <span data-ttu-id="b573f-540">int</span><span class="sxs-lookup"><span data-stu-id="b573f-540">Int</span></span> | <span data-ttu-id="b573f-541">0</span><span class="sxs-lookup"><span data-stu-id="b573f-541">0</span></span> |
| <span data-ttu-id="b573f-542">NotFound</span><span class="sxs-lookup"><span data-stu-id="b573f-542">notFound</span></span> | <span data-ttu-id="b573f-543">int</span><span class="sxs-lookup"><span data-stu-id="b573f-543">Int</span></span> | <span data-ttu-id="b573f-544">-1</span><span class="sxs-lookup"><span data-stu-id="b573f-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="b573f-545">length</span><span class="sxs-lookup"><span data-stu-id="b573f-545">length</span></span>
`length(string)`

<span data-ttu-id="b573f-546">Retorna o número de saudação de caracteres em uma cadeia de caracteres ou elementos em uma matriz.</span><span class="sxs-lookup"><span data-stu-id="b573f-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-547">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-547">Parameters</span></span>

| <span data-ttu-id="b573f-548">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-548">Parameter</span></span> | <span data-ttu-id="b573f-549">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-549">Required</span></span> | <span data-ttu-id="b573f-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-550">Type</span></span> | <span data-ttu-id="b573f-551">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-552">arg1</span><span class="sxs-lookup"><span data-stu-id="b573f-552">arg1</span></span> |<span data-ttu-id="b573f-553">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-553">Yes</span></span> |<span data-ttu-id="b573f-554">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-554">array or string</span></span> |<span data-ttu-id="b573f-555">Olá toouse de matriz para obter o número de saudação de elementos ou Olá toouse de cadeia de caracteres para obter o número de saudação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-556">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-556">Return value</span></span>

<span data-ttu-id="b573f-557">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="b573f-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="b573f-558">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-558">Examples</span></span>

<span data-ttu-id="b573f-559">Olá mostrado no exemplo a seguir como comprimento toouse com uma matriz e a cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="b573f-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="b573f-560">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-561">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-561">Name</span></span> | <span data-ttu-id="b573f-562">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-562">Type</span></span> | <span data-ttu-id="b573f-563">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="b573f-564">arrayLength</span></span> | <span data-ttu-id="b573f-565">int</span><span class="sxs-lookup"><span data-stu-id="b573f-565">Int</span></span> | <span data-ttu-id="b573f-566">3</span><span class="sxs-lookup"><span data-stu-id="b573f-566">3</span></span> |
| <span data-ttu-id="b573f-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="b573f-567">stringLength</span></span> | <span data-ttu-id="b573f-568">int</span><span class="sxs-lookup"><span data-stu-id="b573f-568">Int</span></span> | <span data-ttu-id="b573f-569">13</span><span class="sxs-lookup"><span data-stu-id="b573f-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="b573f-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="b573f-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="b573f-571">Retorna uma cadeia de caracteres alinhada à direita, adicionando caracteres toohello esquerda até atingir o comprimento especificado total hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-572">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-572">Parameters</span></span>

| <span data-ttu-id="b573f-573">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-573">Parameter</span></span> | <span data-ttu-id="b573f-574">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-574">Required</span></span> | <span data-ttu-id="b573f-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-575">Type</span></span> | <span data-ttu-id="b573f-576">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="b573f-577">valueToPad</span></span> |<span data-ttu-id="b573f-578">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-578">Yes</span></span> |<span data-ttu-id="b573f-579">string ou int</span><span class="sxs-lookup"><span data-stu-id="b573f-579">string or int</span></span> |<span data-ttu-id="b573f-580">Olá valor tooright-alinhar.</span><span class="sxs-lookup"><span data-stu-id="b573f-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="b573f-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="b573f-581">totalLength</span></span> |<span data-ttu-id="b573f-582">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-582">Yes</span></span> |<span data-ttu-id="b573f-583">int</span><span class="sxs-lookup"><span data-stu-id="b573f-583">int</span></span> |<span data-ttu-id="b573f-584">número total de saudação de caracteres em Olá retornou uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="b573f-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="b573f-585">paddingCharacter</span></span> |<span data-ttu-id="b573f-586">Não</span><span class="sxs-lookup"><span data-stu-id="b573f-586">No</span></span> |<span data-ttu-id="b573f-587">caractere único</span><span class="sxs-lookup"><span data-stu-id="b573f-587">single character</span></span> |<span data-ttu-id="b573f-588">Olá toouse de caractere para o preenchimento à esquerda até que o comprimento total Olá seja atingido.</span><span class="sxs-lookup"><span data-stu-id="b573f-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="b573f-589">valor padrão de saudação é um espaço.</span><span class="sxs-lookup"><span data-stu-id="b573f-589">hello default value is a space.</span></span> |

<span data-ttu-id="b573f-590">Se a cadeia de caracteres original Olá for maior que o número de saudação do toopad caracteres, caracteres não é adicionado.</span><span class="sxs-lookup"><span data-stu-id="b573f-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="b573f-591">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-591">Return value</span></span>

<span data-ttu-id="b573f-592">Uma cadeia de caracteres pelo menos Olá número de caracteres especificado.</span><span class="sxs-lookup"><span data-stu-id="b573f-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-593">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-593">Examples</span></span>

<span data-ttu-id="b573f-594">saudação de exemplo a seguir mostra como toopad Olá valor de parâmetro fornecido pelo usuário, adicionando Olá caractere zero até atingir o número total de saudação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="b573f-595">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-596">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-596">Name</span></span> | <span data-ttu-id="b573f-597">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-597">Type</span></span> | <span data-ttu-id="b573f-598">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-599">stringOutput</span></span> | <span data-ttu-id="b573f-600">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-600">String</span></span> | <span data-ttu-id="b573f-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="b573f-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="b573f-602">substituir</span><span class="sxs-lookup"><span data-stu-id="b573f-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="b573f-603">Retorna uma nova cadeia de caracteres com todas as instâncias de uma cadeia de caracteres substituídas por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-604">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-604">Parameters</span></span>

| <span data-ttu-id="b573f-605">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-605">Parameter</span></span> | <span data-ttu-id="b573f-606">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-606">Required</span></span> | <span data-ttu-id="b573f-607">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-607">Type</span></span> | <span data-ttu-id="b573f-608">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-609">originalString</span><span class="sxs-lookup"><span data-stu-id="b573f-609">originalString</span></span> |<span data-ttu-id="b573f-610">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-610">Yes</span></span> |<span data-ttu-id="b573f-611">string</span><span class="sxs-lookup"><span data-stu-id="b573f-611">string</span></span> |<span data-ttu-id="b573f-612">valor de saudação que tem todas as instâncias de uma cadeia de caracteres substituídas por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="b573f-613">oldString</span><span class="sxs-lookup"><span data-stu-id="b573f-613">oldString</span></span> |<span data-ttu-id="b573f-614">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-614">Yes</span></span> |<span data-ttu-id="b573f-615">string</span><span class="sxs-lookup"><span data-stu-id="b573f-615">string</span></span> |<span data-ttu-id="b573f-616">cadeia de caracteres de saudação toobe removida da cadeia de caracteres original hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="b573f-617">newString</span><span class="sxs-lookup"><span data-stu-id="b573f-617">newString</span></span> |<span data-ttu-id="b573f-618">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-618">Yes</span></span> |<span data-ttu-id="b573f-619">string</span><span class="sxs-lookup"><span data-stu-id="b573f-619">string</span></span> |<span data-ttu-id="b573f-620">Olá tooadd de cadeia de caracteres em vez da saudação removido cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-621">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-621">Return value</span></span>

<span data-ttu-id="b573f-622">Uma cadeia de caracteres com hello caracteres foram substituídos.</span><span class="sxs-lookup"><span data-stu-id="b573f-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-623">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-623">Examples</span></span>

<span data-ttu-id="b573f-624">saudação de exemplo a seguir mostra como tooremove todos os traços de cadeia de caracteres fornecida pelo usuário hello e como parte de tooreplace de saudação cadeia de caracteres com outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="b573f-625">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-626">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-626">Name</span></span> | <span data-ttu-id="b573f-627">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-627">Type</span></span> | <span data-ttu-id="b573f-628">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-629">firstOutput</span></span> | <span data-ttu-id="b573f-630">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-630">String</span></span> | <span data-ttu-id="b573f-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="b573f-631">1231231234</span></span> |
| <span data-ttu-id="b573f-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-632">secodeOutput</span></span> | <span data-ttu-id="b573f-633">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-633">String</span></span> | <span data-ttu-id="b573f-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="b573f-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="b573f-635">skip</span><span class="sxs-lookup"><span data-stu-id="b573f-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="b573f-636">Retorna uma cadeia de caracteres com todos os caracteres de saudação depois Olá número especificado de caracteres ou uma matriz com todos os elementos de saudação depois Olá número especificado de elementos.</span><span class="sxs-lookup"><span data-stu-id="b573f-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-637">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-637">Parameters</span></span>

| <span data-ttu-id="b573f-638">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-638">Parameter</span></span> | <span data-ttu-id="b573f-639">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-639">Required</span></span> | <span data-ttu-id="b573f-640">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-640">Type</span></span> | <span data-ttu-id="b573f-641">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="b573f-642">originalValue</span></span> |<span data-ttu-id="b573f-643">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-643">Yes</span></span> |<span data-ttu-id="b573f-644">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-644">array or string</span></span> |<span data-ttu-id="b573f-645">Olá toouse matriz ou cadeia de caracteres para ignorar.</span><span class="sxs-lookup"><span data-stu-id="b573f-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="b573f-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="b573f-646">numberToSkip</span></span> |<span data-ttu-id="b573f-647">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-647">Yes</span></span> |<span data-ttu-id="b573f-648">int</span><span class="sxs-lookup"><span data-stu-id="b573f-648">int</span></span> |<span data-ttu-id="b573f-649">número de saudação de elementos ou caracteres tooskip.</span><span class="sxs-lookup"><span data-stu-id="b573f-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="b573f-650">Se esse valor for 0 ou menos, todos os elementos de hello ou caracteres no valor de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="b573f-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="b573f-651">Se for maior do que o tamanho de cadeia de caracteres ou matriz Olá Olá, uma matriz vazia ou cadeia de caracteres é retornada.</span><span class="sxs-lookup"><span data-stu-id="b573f-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-652">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-652">Return value</span></span>

<span data-ttu-id="b573f-653">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-654">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-654">Examples</span></span>

<span data-ttu-id="b573f-655">Olá seguindo o exemplo ignora Olá número especificado de elementos na matriz de saudação e Olá número especificado de caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="b573f-656">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-657">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-657">Name</span></span> | <span data-ttu-id="b573f-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-658">Type</span></span> | <span data-ttu-id="b573f-659">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-660">arrayOutput</span></span> | <span data-ttu-id="b573f-661">Matriz</span><span class="sxs-lookup"><span data-stu-id="b573f-661">Array</span></span> | <span data-ttu-id="b573f-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="b573f-662">["three"]</span></span> |
| <span data-ttu-id="b573f-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-663">stringOutput</span></span> | <span data-ttu-id="b573f-664">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-664">String</span></span> | <span data-ttu-id="b573f-665">dois três</span><span class="sxs-lookup"><span data-stu-id="b573f-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="b573f-666">split</span><span class="sxs-lookup"><span data-stu-id="b573f-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="b573f-667">Retorna uma matriz de cadeias de caracteres que contém as subcadeias de caracteres de saudação do hello cadeia de caracteres de entrada que é delimitadas por Olá especificado delimitadores.</span><span class="sxs-lookup"><span data-stu-id="b573f-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-668">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-668">Parameters</span></span>

| <span data-ttu-id="b573f-669">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-669">Parameter</span></span> | <span data-ttu-id="b573f-670">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-670">Required</span></span> | <span data-ttu-id="b573f-671">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-671">Type</span></span> | <span data-ttu-id="b573f-672">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-673">inputString</span><span class="sxs-lookup"><span data-stu-id="b573f-673">inputString</span></span> |<span data-ttu-id="b573f-674">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-674">Yes</span></span> |<span data-ttu-id="b573f-675">string</span><span class="sxs-lookup"><span data-stu-id="b573f-675">string</span></span> |<span data-ttu-id="b573f-676">Olá toosplit de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-676">hello string toosplit.</span></span> |
| <span data-ttu-id="b573f-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="b573f-677">delimiter</span></span> |<span data-ttu-id="b573f-678">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-678">Yes</span></span> |<span data-ttu-id="b573f-679">cadeia de caracteres ou matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-679">string or array of strings</span></span> |<span data-ttu-id="b573f-680">Olá toouse delimitador para a divisão de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-681">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-681">Return value</span></span>

<span data-ttu-id="b573f-682">Uma matriz de cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-683">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-683">Examples</span></span>

<span data-ttu-id="b573f-684">Olá exemplo a seguir divide Olá entrada cadeia de caracteres com uma vírgula e com uma vírgula ou ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="b573f-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="b573f-685">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-686">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-686">Name</span></span> | <span data-ttu-id="b573f-687">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-687">Type</span></span> | <span data-ttu-id="b573f-688">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-689">firstOutput</span></span> | <span data-ttu-id="b573f-690">Matriz</span><span class="sxs-lookup"><span data-stu-id="b573f-690">Array</span></span> | <span data-ttu-id="b573f-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="b573f-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="b573f-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-692">secondOutput</span></span> | <span data-ttu-id="b573f-693">Matriz</span><span class="sxs-lookup"><span data-stu-id="b573f-693">Array</span></span> | <span data-ttu-id="b573f-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="b573f-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="b573f-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="b573f-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="b573f-696">Determina se uma cadeia de caracteres começa com um valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="b573f-697">comparação de saudação diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b573f-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-698">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-698">Parameters</span></span>

| <span data-ttu-id="b573f-699">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-699">Parameter</span></span> | <span data-ttu-id="b573f-700">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-700">Required</span></span> | <span data-ttu-id="b573f-701">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-701">Type</span></span> | <span data-ttu-id="b573f-702">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b573f-703">stringToSearch</span></span> |<span data-ttu-id="b573f-704">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-704">Yes</span></span> |<span data-ttu-id="b573f-705">string</span><span class="sxs-lookup"><span data-stu-id="b573f-705">string</span></span> |<span data-ttu-id="b573f-706">valor de saudação que contém Olá toofind de item.</span><span class="sxs-lookup"><span data-stu-id="b573f-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b573f-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b573f-707">stringToFind</span></span> |<span data-ttu-id="b573f-708">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-708">Yes</span></span> |<span data-ttu-id="b573f-709">string</span><span class="sxs-lookup"><span data-stu-id="b573f-709">string</span></span> |<span data-ttu-id="b573f-710">Olá toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-711">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-711">Return value</span></span>

<span data-ttu-id="b573f-712">**True** se Olá primeiro caractere ou caracteres de cadeia de caracteres hello corresponder ao valor de saudação; caso contrário, **False**.</span><span class="sxs-lookup"><span data-stu-id="b573f-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-713">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-713">Examples</span></span>

<span data-ttu-id="b573f-714">saudação de exemplo a seguir mostra como toouse Olá startsWith e endsWith funções:</span><span class="sxs-lookup"><span data-stu-id="b573f-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="b573f-715">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-716">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-716">Name</span></span> | <span data-ttu-id="b573f-717">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-717">Type</span></span> | <span data-ttu-id="b573f-718">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-719">startsTrue</span></span> | <span data-ttu-id="b573f-720">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-720">Bool</span></span> | <span data-ttu-id="b573f-721">True </span><span class="sxs-lookup"><span data-stu-id="b573f-721">True</span></span> |
| <span data-ttu-id="b573f-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-722">startsCapTrue</span></span> | <span data-ttu-id="b573f-723">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-723">Bool</span></span> | <span data-ttu-id="b573f-724">True </span><span class="sxs-lookup"><span data-stu-id="b573f-724">True</span></span> |
| <span data-ttu-id="b573f-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-725">startsFalse</span></span> | <span data-ttu-id="b573f-726">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-726">Bool</span></span> | <span data-ttu-id="b573f-727">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-727">False</span></span> |
| <span data-ttu-id="b573f-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-728">endsTrue</span></span> | <span data-ttu-id="b573f-729">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-729">Bool</span></span> | <span data-ttu-id="b573f-730">True </span><span class="sxs-lookup"><span data-stu-id="b573f-730">True</span></span> |
| <span data-ttu-id="b573f-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b573f-731">endsCapTrue</span></span> | <span data-ttu-id="b573f-732">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-732">Bool</span></span> | <span data-ttu-id="b573f-733">True </span><span class="sxs-lookup"><span data-stu-id="b573f-733">True</span></span> |
| <span data-ttu-id="b573f-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="b573f-734">endsFalse</span></span> | <span data-ttu-id="b573f-735">Bool</span><span class="sxs-lookup"><span data-stu-id="b573f-735">Bool</span></span> | <span data-ttu-id="b573f-736">Falso</span><span class="sxs-lookup"><span data-stu-id="b573f-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="b573f-737">string</span><span class="sxs-lookup"><span data-stu-id="b573f-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="b573f-738">Converte Olá especificado a cadeia de caracteres do valor tooa.</span><span class="sxs-lookup"><span data-stu-id="b573f-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-739">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-739">Parameters</span></span>

| <span data-ttu-id="b573f-740">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-740">Parameter</span></span> | <span data-ttu-id="b573f-741">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-741">Required</span></span> | <span data-ttu-id="b573f-742">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-742">Type</span></span> | <span data-ttu-id="b573f-743">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="b573f-744">valueToConvert</span></span> |<span data-ttu-id="b573f-745">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-745">Yes</span></span> | <span data-ttu-id="b573f-746">Qualquer</span><span class="sxs-lookup"><span data-stu-id="b573f-746">Any</span></span> |<span data-ttu-id="b573f-747">Olá valor tooconvert toostring.</span><span class="sxs-lookup"><span data-stu-id="b573f-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="b573f-748">Qualquer tipo de valor pode ser convertido, incluindo objetos e matrizes.</span><span class="sxs-lookup"><span data-stu-id="b573f-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-749">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-749">Return value</span></span>

<span data-ttu-id="b573f-750">Uma cadeia de caracteres do valor de saudação convertida.</span><span class="sxs-lookup"><span data-stu-id="b573f-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-751">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-751">Examples</span></span>

<span data-ttu-id="b573f-752">saudação de exemplo a seguir mostra como tooconvert diferentes tipos de valores toostrings:</span><span class="sxs-lookup"><span data-stu-id="b573f-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="b573f-753">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-754">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-754">Name</span></span> | <span data-ttu-id="b573f-755">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-755">Type</span></span> | <span data-ttu-id="b573f-756">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-757">objectOutput</span></span> | <span data-ttu-id="b573f-758">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-758">String</span></span> | <span data-ttu-id="b573f-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="b573f-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="b573f-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-760">arrayOutput</span></span> | <span data-ttu-id="b573f-761">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-761">String</span></span> | <span data-ttu-id="b573f-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="b573f-762">["a","b","c"]</span></span> |
| <span data-ttu-id="b573f-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-763">intOutput</span></span> | <span data-ttu-id="b573f-764">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-764">String</span></span> | <span data-ttu-id="b573f-765">5</span><span class="sxs-lookup"><span data-stu-id="b573f-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="b573f-766">substring</span><span class="sxs-lookup"><span data-stu-id="b573f-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="b573f-767">Retorna uma subcadeia de caracteres que começa no hello especificado posição de caracteres e contém Olá número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-768">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-768">Parameters</span></span>

| <span data-ttu-id="b573f-769">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-769">Parameter</span></span> | <span data-ttu-id="b573f-770">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-770">Required</span></span> | <span data-ttu-id="b573f-771">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-771">Type</span></span> | <span data-ttu-id="b573f-772">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="b573f-773">stringToParse</span></span> |<span data-ttu-id="b573f-774">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-774">Yes</span></span> |<span data-ttu-id="b573f-775">string</span><span class="sxs-lookup"><span data-stu-id="b573f-775">string</span></span> |<span data-ttu-id="b573f-776">Olá cadeia de caracteres original do qual Olá subcadeia de caracteres é extraída.</span><span class="sxs-lookup"><span data-stu-id="b573f-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="b573f-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="b573f-777">startIndex</span></span> |<span data-ttu-id="b573f-778">Não</span><span class="sxs-lookup"><span data-stu-id="b573f-778">No</span></span> |<span data-ttu-id="b573f-779">int</span><span class="sxs-lookup"><span data-stu-id="b573f-779">int</span></span> |<span data-ttu-id="b573f-780">Olá com base em zero posição de caractere inicial de subcadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="b573f-781">length</span><span class="sxs-lookup"><span data-stu-id="b573f-781">length</span></span> |<span data-ttu-id="b573f-782">Não</span><span class="sxs-lookup"><span data-stu-id="b573f-782">No</span></span> |<span data-ttu-id="b573f-783">int</span><span class="sxs-lookup"><span data-stu-id="b573f-783">int</span></span> |<span data-ttu-id="b573f-784">número de saudação de caracteres de subcadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="b573f-785">Deve se referir tooa local dentro da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-786">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-786">Return value</span></span>

<span data-ttu-id="b573f-787">subcadeia de caracteres Hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="b573f-788">Comentários</span><span class="sxs-lookup"><span data-stu-id="b573f-788">Remarks</span></span>

<span data-ttu-id="b573f-789">função Hello falha quando a subcadeia de caracteres hello ultrapassa a fim de saudação da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="b573f-790">saudação de exemplo a seguir falhará com hello erro "parâmetros de índice e o comprimento da saudação devem se referir tooa local dentro da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="b573f-791">Olá parâmetro de índice: '0' hello parâmetro de comprimento: Olá '11', comprimento do parâmetro de cadeia de caracteres hello: '10'. ".</span><span class="sxs-lookup"><span data-stu-id="b573f-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="b573f-792">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-792">Examples</span></span>

<span data-ttu-id="b573f-793">saudação de exemplo a seguir extrai uma subcadeia de caracteres de um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b573f-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="b573f-794">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-795">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-795">Name</span></span> | <span data-ttu-id="b573f-796">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-796">Type</span></span> | <span data-ttu-id="b573f-797">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-798">substringOutput</span></span> | <span data-ttu-id="b573f-799">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-799">String</span></span> | <span data-ttu-id="b573f-800">dois</span><span class="sxs-lookup"><span data-stu-id="b573f-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="b573f-801">take</span><span class="sxs-lookup"><span data-stu-id="b573f-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="b573f-802">Retorna uma cadeia de caracteres com hello número especificado de caracteres do início de saudação do hello cadeia de caracteres ou uma matriz com hello número especificado de elementos do início de saudação da matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-803">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-803">Parameters</span></span>

| <span data-ttu-id="b573f-804">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-804">Parameter</span></span> | <span data-ttu-id="b573f-805">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-805">Required</span></span> | <span data-ttu-id="b573f-806">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-806">Type</span></span> | <span data-ttu-id="b573f-807">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="b573f-808">originalValue</span></span> |<span data-ttu-id="b573f-809">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-809">Yes</span></span> |<span data-ttu-id="b573f-810">matriz ou cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-810">array or string</span></span> |<span data-ttu-id="b573f-811">Olá cadeia ou matriz de elementos de saudação tootake do.</span><span class="sxs-lookup"><span data-stu-id="b573f-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="b573f-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="b573f-812">numberToTake</span></span> |<span data-ttu-id="b573f-813">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-813">Yes</span></span> |<span data-ttu-id="b573f-814">int</span><span class="sxs-lookup"><span data-stu-id="b573f-814">int</span></span> |<span data-ttu-id="b573f-815">número de saudação de elementos ou caracteres tootake.</span><span class="sxs-lookup"><span data-stu-id="b573f-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="b573f-816">Se esse valor for 0 ou menos, uma matriz ou cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="b573f-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="b573f-817">Se for maior do que o comprimento de saudação do hello considerando a cadeia de caracteres ou matriz, todos os elementos de saudação na cadeia de caracteres ou matriz hello serão retornados.</span><span class="sxs-lookup"><span data-stu-id="b573f-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-818">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-818">Return value</span></span>

<span data-ttu-id="b573f-819">Uma matriz ou cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-820">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-820">Examples</span></span>

<span data-ttu-id="b573f-821">Olá seguindo o exemplo usa Olá número especificado de elementos da matriz hello e caracteres de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="b573f-822">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-823">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-823">Name</span></span> | <span data-ttu-id="b573f-824">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-824">Type</span></span> | <span data-ttu-id="b573f-825">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-826">arrayOutput</span></span> | <span data-ttu-id="b573f-827">Matriz</span><span class="sxs-lookup"><span data-stu-id="b573f-827">Array</span></span> | <span data-ttu-id="b573f-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="b573f-828">["one", "two"]</span></span> |
| <span data-ttu-id="b573f-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-829">stringOutput</span></span> | <span data-ttu-id="b573f-830">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-830">String</span></span> | <span data-ttu-id="b573f-831">em</span><span class="sxs-lookup"><span data-stu-id="b573f-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="b573f-832">toLower</span><span class="sxs-lookup"><span data-stu-id="b573f-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="b573f-833">Converte Olá especificado caso toolower de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-834">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-834">Parameters</span></span>

| <span data-ttu-id="b573f-835">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-835">Parameter</span></span> | <span data-ttu-id="b573f-836">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-836">Required</span></span> | <span data-ttu-id="b573f-837">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-837">Type</span></span> | <span data-ttu-id="b573f-838">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="b573f-839">stringToChange</span></span> |<span data-ttu-id="b573f-840">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-840">Yes</span></span> |<span data-ttu-id="b573f-841">string</span><span class="sxs-lookup"><span data-stu-id="b573f-841">string</span></span> |<span data-ttu-id="b573f-842">Olá valor tooconvert toolower maiusculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b573f-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-843">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-843">Return value</span></span>

<span data-ttu-id="b573f-844">cadeia de caracteres de saudação convertida toolower caso.</span><span class="sxs-lookup"><span data-stu-id="b573f-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-845">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-845">Examples</span></span>

<span data-ttu-id="b573f-846">saudação de exemplo a seguir converte um caso de toolower de valor de parâmetro e tooupper caso.</span><span class="sxs-lookup"><span data-stu-id="b573f-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="b573f-847">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-848">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-848">Name</span></span> | <span data-ttu-id="b573f-849">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-849">Type</span></span> | <span data-ttu-id="b573f-850">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-851">toLowerOutput</span></span> | <span data-ttu-id="b573f-852">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-852">String</span></span> | <span data-ttu-id="b573f-853">um dois três</span><span class="sxs-lookup"><span data-stu-id="b573f-853">one two three</span></span> |
| <span data-ttu-id="b573f-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-854">toUpperOutput</span></span> | <span data-ttu-id="b573f-855">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-855">String</span></span> | <span data-ttu-id="b573f-856">UM DOIS TRÊS</span><span class="sxs-lookup"><span data-stu-id="b573f-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="b573f-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="b573f-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="b573f-858">Converte Olá especificado caso tooupper de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-859">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-859">Parameters</span></span>

| <span data-ttu-id="b573f-860">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-860">Parameter</span></span> | <span data-ttu-id="b573f-861">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-861">Required</span></span> | <span data-ttu-id="b573f-862">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-862">Type</span></span> | <span data-ttu-id="b573f-863">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="b573f-864">stringToChange</span></span> |<span data-ttu-id="b573f-865">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-865">Yes</span></span> |<span data-ttu-id="b573f-866">string</span><span class="sxs-lookup"><span data-stu-id="b573f-866">string</span></span> |<span data-ttu-id="b573f-867">Olá valor tooconvert tooupper maiusculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b573f-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-868">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-868">Return value</span></span>

<span data-ttu-id="b573f-869">cadeia de caracteres de saudação convertida tooupper caso.</span><span class="sxs-lookup"><span data-stu-id="b573f-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-870">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-870">Examples</span></span>

<span data-ttu-id="b573f-871">saudação de exemplo a seguir converte um caso de toolower de valor de parâmetro e tooupper caso.</span><span class="sxs-lookup"><span data-stu-id="b573f-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="b573f-872">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-873">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-873">Name</span></span> | <span data-ttu-id="b573f-874">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-874">Type</span></span> | <span data-ttu-id="b573f-875">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-876">toLowerOutput</span></span> | <span data-ttu-id="b573f-877">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-877">String</span></span> | <span data-ttu-id="b573f-878">um dois três</span><span class="sxs-lookup"><span data-stu-id="b573f-878">one two three</span></span> |
| <span data-ttu-id="b573f-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-879">toUpperOutput</span></span> | <span data-ttu-id="b573f-880">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-880">String</span></span> | <span data-ttu-id="b573f-881">UM DOIS TRÊS</span><span class="sxs-lookup"><span data-stu-id="b573f-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="b573f-882">cortar</span><span class="sxs-lookup"><span data-stu-id="b573f-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="b573f-883">Remove todos os principais e caracteres de espaço em branco da saudação especificado cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-884">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-884">Parameters</span></span>

| <span data-ttu-id="b573f-885">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-885">Parameter</span></span> | <span data-ttu-id="b573f-886">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-886">Required</span></span> | <span data-ttu-id="b573f-887">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-887">Type</span></span> | <span data-ttu-id="b573f-888">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="b573f-889">stringToTrim</span></span> |<span data-ttu-id="b573f-890">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-890">Yes</span></span> |<span data-ttu-id="b573f-891">string</span><span class="sxs-lookup"><span data-stu-id="b573f-891">string</span></span> |<span data-ttu-id="b573f-892">Olá tootrim de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-893">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-893">Return value</span></span>

<span data-ttu-id="b573f-894">cadeia de caracteres de saudação sem à esquerda e caracteres de espaço em branco à direita.</span><span class="sxs-lookup"><span data-stu-id="b573f-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-895">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-895">Examples</span></span>

<span data-ttu-id="b573f-896">Olá, exemplo a seguir remove caracteres de espaço em branco de saudação do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="b573f-897">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-898">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-898">Name</span></span> | <span data-ttu-id="b573f-899">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-899">Type</span></span> | <span data-ttu-id="b573f-900">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-901">retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-901">return</span></span> | <span data-ttu-id="b573f-902">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-902">String</span></span> | <span data-ttu-id="b573f-903">um dois três</span><span class="sxs-lookup"><span data-stu-id="b573f-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="b573f-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="b573f-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="b573f-905">Cria uma cadeia de caracteres de hash determinística com base nos valores hello fornecidos como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b573f-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="b573f-906">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-906">Parameters</span></span>

| <span data-ttu-id="b573f-907">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-907">Parameter</span></span> | <span data-ttu-id="b573f-908">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-908">Required</span></span> | <span data-ttu-id="b573f-909">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-909">Type</span></span> | <span data-ttu-id="b573f-910">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-911">baseString</span><span class="sxs-lookup"><span data-stu-id="b573f-911">baseString</span></span> |<span data-ttu-id="b573f-912">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-912">Yes</span></span> |<span data-ttu-id="b573f-913">string</span><span class="sxs-lookup"><span data-stu-id="b573f-913">string</span></span> |<span data-ttu-id="b573f-914">valor de saudação usado na toocreate de função de hash Olá uma cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="b573f-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="b573f-915">parâmetros extras conforme necessário</span><span class="sxs-lookup"><span data-stu-id="b573f-915">additional parameters as needed</span></span> |<span data-ttu-id="b573f-916">Não</span><span class="sxs-lookup"><span data-stu-id="b573f-916">No</span></span> |<span data-ttu-id="b573f-917">string</span><span class="sxs-lookup"><span data-stu-id="b573f-917">string</span></span> |<span data-ttu-id="b573f-918">Você pode adicionar quantas cadeias de caracteres como valor de saudação toocreate necessário que especifica o nível de saudação de exclusividade.</span><span class="sxs-lookup"><span data-stu-id="b573f-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="b573f-919">Comentários</span><span class="sxs-lookup"><span data-stu-id="b573f-919">Remarks</span></span>

<span data-ttu-id="b573f-920">Essa função é útil quando você precisa toocreate um nome exclusivo para um recurso.</span><span class="sxs-lookup"><span data-stu-id="b573f-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="b573f-921">Você fornecer valores de parâmetro para limitam o escopo de saudação de exclusividade para o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="b573f-922">Você pode especificar se o nome da saudação é exclusivo para baixo toosubscription, no grupo de recursos ou implantação.</span><span class="sxs-lookup"><span data-stu-id="b573f-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="b573f-923">Olá retornou o valor não é uma cadeia de caracteres aleatória, mas em vez disso, Olá resultado de uma função de hash.</span><span class="sxs-lookup"><span data-stu-id="b573f-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="b573f-924">Olá retornou o valor é 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="b573f-925">Não é globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="b573f-925">It is not globally unique.</span></span> <span data-ttu-id="b573f-926">Talvez você queira toocombine valor de saudação com um prefixo de seu toocreate de convenção de nomenclatura um nome que seja significativo.</span><span class="sxs-lookup"><span data-stu-id="b573f-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="b573f-927">Olá, exemplo a seguir mostra formato Olá Olá retornada o valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="b573f-928">valor real Olá varia de acordo com hello parâmetros fornecido.</span><span class="sxs-lookup"><span data-stu-id="b573f-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="b573f-929">Olá exemplos a seguir mostra como toouse uniqueString toocreate um único valor para comumente usados níveis.</span><span class="sxs-lookup"><span data-stu-id="b573f-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="b573f-930">Toosubscription escopo exclusivo</span><span class="sxs-lookup"><span data-stu-id="b573f-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="b573f-931">Exclusivo tooresource no escopo de grupo</span><span class="sxs-lookup"><span data-stu-id="b573f-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="b573f-932">Exclusivo toodeployment com escopo definido para um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b573f-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="b573f-933">saudação de exemplo a seguir mostra como toocreate um nome exclusivo para uma conta de armazenamento com base em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b573f-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="b573f-934">Dentro do grupo de recursos Olá, nome de saudação não é exclusivo se construída Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="b573f-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="b573f-935">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-935">Return value</span></span>

<span data-ttu-id="b573f-936">Uma cadeia de caracteres que contém 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-937">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-937">Examples</span></span>

<span data-ttu-id="b573f-938">saudação de exemplo a seguir retorna os resultados da uniquestring:</span><span class="sxs-lookup"><span data-stu-id="b573f-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="b573f-939">uri</span><span class="sxs-lookup"><span data-stu-id="b573f-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="b573f-940">Cria um URI absoluto combinando Olá baseUri e cadeia de caracteres hello Uri_relativo.</span><span class="sxs-lookup"><span data-stu-id="b573f-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-941">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-941">Parameters</span></span>

| <span data-ttu-id="b573f-942">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-942">Parameter</span></span> | <span data-ttu-id="b573f-943">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-943">Required</span></span> | <span data-ttu-id="b573f-944">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-944">Type</span></span> | <span data-ttu-id="b573f-945">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="b573f-946">baseUri</span></span> |<span data-ttu-id="b573f-947">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-947">Yes</span></span> |<span data-ttu-id="b573f-948">string</span><span class="sxs-lookup"><span data-stu-id="b573f-948">string</span></span> |<span data-ttu-id="b573f-949">Olá a cadeia de caracteres de uri de base.</span><span class="sxs-lookup"><span data-stu-id="b573f-949">hello base uri string.</span></span> |
| <span data-ttu-id="b573f-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="b573f-950">relativeUri</span></span> |<span data-ttu-id="b573f-951">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-951">Yes</span></span> |<span data-ttu-id="b573f-952">string</span><span class="sxs-lookup"><span data-stu-id="b573f-952">string</span></span> |<span data-ttu-id="b573f-953">Olá uri relativo cadeia de caracteres tooadd toohello uri base cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b573f-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="b573f-954">Olá valor Olá **baseUri** parâmetro pode incluir um arquivo específico, mas somente caminho base Olá é usado ao construir Olá URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="b573f-955">Por exemplo, passar `http://contoso.com/resources/azuredeploy.json` como resultados de parâmetro hello baseUri em um URI de base de `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="b573f-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="b573f-956">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-956">Return value</span></span>

<span data-ttu-id="b573f-957">Uma cadeia de caracteres que representa Olá URI absoluto para valores de base e relativo hello.</span><span class="sxs-lookup"><span data-stu-id="b573f-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-958">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-958">Examples</span></span>

<span data-ttu-id="b573f-959">saudação de exemplo a seguir mostra como tooconstruct um modelo aninhado do link tooa com base no valor de saudação do modelo pai a saudação.</span><span class="sxs-lookup"><span data-stu-id="b573f-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="b573f-960">Olá mostrado no exemplo a seguir como uri toouse, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="b573f-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="b573f-961">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-962">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-962">Name</span></span> | <span data-ttu-id="b573f-963">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-963">Type</span></span> | <span data-ttu-id="b573f-964">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-965">uriOutput</span></span> | <span data-ttu-id="b573f-966">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-966">String</span></span> | <span data-ttu-id="b573f-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="b573f-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-968">componentOutput</span></span> | <span data-ttu-id="b573f-969">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-969">String</span></span> | <span data-ttu-id="b573f-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="b573f-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-971">toStringOutput</span></span> | <span data-ttu-id="b573f-972">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-972">String</span></span> | <span data-ttu-id="b573f-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="b573f-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="b573f-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="b573f-975">Codifica um URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-976">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-976">Parameters</span></span>

| <span data-ttu-id="b573f-977">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-977">Parameter</span></span> | <span data-ttu-id="b573f-978">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-978">Required</span></span> | <span data-ttu-id="b573f-979">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-979">Type</span></span> | <span data-ttu-id="b573f-980">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="b573f-981">stringToEncode</span></span> |<span data-ttu-id="b573f-982">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-982">Yes</span></span> |<span data-ttu-id="b573f-983">string</span><span class="sxs-lookup"><span data-stu-id="b573f-983">string</span></span> |<span data-ttu-id="b573f-984">Olá tooencode de valor.</span><span class="sxs-lookup"><span data-stu-id="b573f-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-985">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-985">Return value</span></span>

<span data-ttu-id="b573f-986">Uma cadeia de caracteres de saudação URI valor codificado.</span><span class="sxs-lookup"><span data-stu-id="b573f-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-987">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-987">Examples</span></span>

<span data-ttu-id="b573f-988">Olá mostrado no exemplo a seguir como uri toouse, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="b573f-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="b573f-989">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-990">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-990">Name</span></span> | <span data-ttu-id="b573f-991">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-991">Type</span></span> | <span data-ttu-id="b573f-992">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-993">uriOutput</span></span> | <span data-ttu-id="b573f-994">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-994">String</span></span> | <span data-ttu-id="b573f-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="b573f-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-996">componentOutput</span></span> | <span data-ttu-id="b573f-997">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-997">String</span></span> | <span data-ttu-id="b573f-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="b573f-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-999">toStringOutput</span></span> | <span data-ttu-id="b573f-1000">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-1000">String</span></span> | <span data-ttu-id="b573f-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="b573f-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="b573f-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="b573f-1003">Retorna uma cadeia de caracteres de um valor codificado em URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="b573f-1004">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b573f-1004">Parameters</span></span>

| <span data-ttu-id="b573f-1005">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b573f-1005">Parameter</span></span> | <span data-ttu-id="b573f-1006">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b573f-1006">Required</span></span> | <span data-ttu-id="b573f-1007">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-1007">Type</span></span> | <span data-ttu-id="b573f-1008">Descrição</span><span class="sxs-lookup"><span data-stu-id="b573f-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b573f-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="b573f-1009">uriEncodedString</span></span> |<span data-ttu-id="b573f-1010">Sim</span><span class="sxs-lookup"><span data-stu-id="b573f-1010">Yes</span></span> |<span data-ttu-id="b573f-1011">string</span><span class="sxs-lookup"><span data-stu-id="b573f-1011">string</span></span> |<span data-ttu-id="b573f-1012">Olá URI codificado em cadeia de caracteres do valor tooconvert tooa.</span><span class="sxs-lookup"><span data-stu-id="b573f-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b573f-1013">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="b573f-1013">Return value</span></span>

<span data-ttu-id="b573f-1014">Uma cadeia de caracteres decodificada de valores codificados em URI.</span><span class="sxs-lookup"><span data-stu-id="b573f-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="b573f-1015">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b573f-1015">Examples</span></span>

<span data-ttu-id="b573f-1016">Olá mostrado no exemplo a seguir como uri toouse, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="b573f-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="b573f-1017">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="b573f-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b573f-1018">Nome</span><span class="sxs-lookup"><span data-stu-id="b573f-1018">Name</span></span> | <span data-ttu-id="b573f-1019">Tipo</span><span class="sxs-lookup"><span data-stu-id="b573f-1019">Type</span></span> | <span data-ttu-id="b573f-1020">Valor</span><span class="sxs-lookup"><span data-stu-id="b573f-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b573f-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-1021">uriOutput</span></span> | <span data-ttu-id="b573f-1022">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-1022">String</span></span> | <span data-ttu-id="b573f-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="b573f-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-1024">componentOutput</span></span> | <span data-ttu-id="b573f-1025">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-1025">String</span></span> | <span data-ttu-id="b573f-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="b573f-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b573f-1027">toStringOutput</span></span> | <span data-ttu-id="b573f-1028">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b573f-1028">String</span></span> | <span data-ttu-id="b573f-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b573f-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b573f-1030">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b573f-1030">Next steps</span></span>
* <span data-ttu-id="b573f-1031">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b573f-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b573f-1032">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b573f-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="b573f-1033">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b573f-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="b573f-1034">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b573f-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

