---
title: "aaaResource Gerenciador de funções de modelo | Microsoft Docs"
description: "Descreve Olá toouse de funções em valores de tooretrieve um modelo do Azure Resource Manager, trabalhar com cadeias de caracteres e valores numéricos e recuperar informações de implantação."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="16ff9-103">Funções do modelo do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="16ff9-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="16ff9-104">Este tópico descreve todas as funções hello, que você pode usar em um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="16ff9-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="16ff9-105">Você adiciona funções aos seus modelos colocando-as entre colchetes: `[` e `]`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="16ff9-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="16ff9-106">Olá expressão é avaliada durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="16ff9-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="16ff9-107">Enquanto gravado como uma cadeia de caracteres literal, o resultado de saudação da avaliação de expressão Olá pode ser de um tipo diferente de JSON, como uma matriz, objeto ou inteiro.</span><span class="sxs-lookup"><span data-stu-id="16ff9-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="16ff9-108">Assim como no JavaScript, as chamadas de função são formatadas como `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="16ff9-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="16ff9-109">Você pode referenciar propriedades usando os operadores de ponto e [index] hello.</span><span class="sxs-lookup"><span data-stu-id="16ff9-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="16ff9-110">Uma expressão de modelo não pode exceder 24.576 caracteres.</span><span class="sxs-lookup"><span data-stu-id="16ff9-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="16ff9-111">As funções do modelo e seus parâmetros não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="16ff9-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="16ff9-112">Por exemplo, o Gerenciador de recursos resolve **variables('var1')** e **VARIABLES('VAR1')** como Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="16ff9-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="16ff9-113">Quando avaliada, a menos que a função hello expressamente modifica caso (como toUpper ou toLower), a função hello preserva caso hello.</span><span class="sxs-lookup"><span data-stu-id="16ff9-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="16ff9-114">Determinados tipos de recursos podem ter requisitos de maiúsculas e minúsculas independentemente de como as funções são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="16ff9-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="16ff9-115">Funções de objeto e matriz</span><span class="sxs-lookup"><span data-stu-id="16ff9-115">Array and object functions</span></span>
<span data-ttu-id="16ff9-116">O Resource Manager fornece diversas funções para trabalhar com matrizes e objetos.</span><span class="sxs-lookup"><span data-stu-id="16ff9-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="16ff9-117">array</span><span class="sxs-lookup"><span data-stu-id="16ff9-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="16ff9-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="16ff9-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="16ff9-119">concat</span><span class="sxs-lookup"><span data-stu-id="16ff9-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="16ff9-120">contains</span><span class="sxs-lookup"><span data-stu-id="16ff9-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="16ff9-121">createArray</span><span class="sxs-lookup"><span data-stu-id="16ff9-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="16ff9-122">empty</span><span class="sxs-lookup"><span data-stu-id="16ff9-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="16ff9-123">first</span><span class="sxs-lookup"><span data-stu-id="16ff9-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="16ff9-124">intersection</span><span class="sxs-lookup"><span data-stu-id="16ff9-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="16ff9-125">json</span><span class="sxs-lookup"><span data-stu-id="16ff9-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="16ff9-126">last</span><span class="sxs-lookup"><span data-stu-id="16ff9-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="16ff9-127">length</span><span class="sxs-lookup"><span data-stu-id="16ff9-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="16ff9-128">min</span><span class="sxs-lookup"><span data-stu-id="16ff9-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="16ff9-129">max</span><span class="sxs-lookup"><span data-stu-id="16ff9-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="16ff9-130">range</span><span class="sxs-lookup"><span data-stu-id="16ff9-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="16ff9-131">skip</span><span class="sxs-lookup"><span data-stu-id="16ff9-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="16ff9-132">take</span><span class="sxs-lookup"><span data-stu-id="16ff9-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="16ff9-133">union</span><span class="sxs-lookup"><span data-stu-id="16ff9-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="16ff9-134">Funções de comparação</span><span class="sxs-lookup"><span data-stu-id="16ff9-134">Comparison functions</span></span>
<span data-ttu-id="16ff9-135">O Resource Manager fornece várias funções para fazer comparações em seus modelos.</span><span class="sxs-lookup"><span data-stu-id="16ff9-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="16ff9-136">equals</span><span class="sxs-lookup"><span data-stu-id="16ff9-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="16ff9-137">less</span><span class="sxs-lookup"><span data-stu-id="16ff9-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="16ff9-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="16ff9-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="16ff9-139">greater</span><span class="sxs-lookup"><span data-stu-id="16ff9-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="16ff9-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="16ff9-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="16ff9-141">Funções de valor de implantação</span><span class="sxs-lookup"><span data-stu-id="16ff9-141">Deployment value functions</span></span>
<span data-ttu-id="16ff9-142">Gerenciador de recursos fornece a seguinte Olá funções para obter valores de seções do modelo de saudação e valores relacionados toohello implantação:</span><span class="sxs-lookup"><span data-stu-id="16ff9-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="16ff9-143">implantação</span><span class="sxs-lookup"><span data-stu-id="16ff9-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="16ff9-144">parâmetros</span><span class="sxs-lookup"><span data-stu-id="16ff9-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="16ff9-145">variáveis</span><span class="sxs-lookup"><span data-stu-id="16ff9-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="16ff9-146">Funções lógicas</span><span class="sxs-lookup"><span data-stu-id="16ff9-146">Logical functions</span></span>
<span data-ttu-id="16ff9-147">Gerenciador de recursos fornece Olá funções para trabalhar com condições lógicas a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ff9-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="16ff9-148">and</span><span class="sxs-lookup"><span data-stu-id="16ff9-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="16ff9-149">bool</span><span class="sxs-lookup"><span data-stu-id="16ff9-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="16ff9-150">if</span><span class="sxs-lookup"><span data-stu-id="16ff9-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="16ff9-151">not</span><span class="sxs-lookup"><span data-stu-id="16ff9-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="16ff9-152">ou</span><span class="sxs-lookup"><span data-stu-id="16ff9-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="16ff9-153">Funções numéricas</span><span class="sxs-lookup"><span data-stu-id="16ff9-153">Numeric functions</span></span>
<span data-ttu-id="16ff9-154">Gerenciador de recursos fornece Olá seguintes funções para trabalhar com números inteiros:</span><span class="sxs-lookup"><span data-stu-id="16ff9-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="16ff9-155">adicionar</span><span class="sxs-lookup"><span data-stu-id="16ff9-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="16ff9-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="16ff9-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="16ff9-157">div</span><span class="sxs-lookup"><span data-stu-id="16ff9-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="16ff9-158">float</span><span class="sxs-lookup"><span data-stu-id="16ff9-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="16ff9-159">int</span><span class="sxs-lookup"><span data-stu-id="16ff9-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="16ff9-160">min</span><span class="sxs-lookup"><span data-stu-id="16ff9-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="16ff9-161">max</span><span class="sxs-lookup"><span data-stu-id="16ff9-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="16ff9-162">mod</span><span class="sxs-lookup"><span data-stu-id="16ff9-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="16ff9-163">mul</span><span class="sxs-lookup"><span data-stu-id="16ff9-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="16ff9-164">sub</span><span class="sxs-lookup"><span data-stu-id="16ff9-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="16ff9-165">Funções de recurso</span><span class="sxs-lookup"><span data-stu-id="16ff9-165">Resource functions</span></span>
<span data-ttu-id="16ff9-166">Gerenciador de recursos fornece Olá funções para obter valores de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ff9-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="16ff9-167">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="16ff9-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="16ff9-168">providers</span><span class="sxs-lookup"><span data-stu-id="16ff9-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="16ff9-169">reference</span><span class="sxs-lookup"><span data-stu-id="16ff9-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="16ff9-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="16ff9-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="16ff9-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="16ff9-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="16ff9-172">subscription</span><span class="sxs-lookup"><span data-stu-id="16ff9-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="16ff9-173">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="16ff9-173">String functions</span></span>
<span data-ttu-id="16ff9-174">Gerenciador de recursos fornece Olá funções para trabalhar com cadeias de caracteres a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ff9-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="16ff9-175">base64</span><span class="sxs-lookup"><span data-stu-id="16ff9-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="16ff9-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="16ff9-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="16ff9-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="16ff9-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="16ff9-178">concat</span><span class="sxs-lookup"><span data-stu-id="16ff9-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="16ff9-179">contains</span><span class="sxs-lookup"><span data-stu-id="16ff9-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="16ff9-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="16ff9-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="16ff9-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="16ff9-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="16ff9-182">empty</span><span class="sxs-lookup"><span data-stu-id="16ff9-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="16ff9-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="16ff9-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="16ff9-184">first</span><span class="sxs-lookup"><span data-stu-id="16ff9-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="16ff9-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="16ff9-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="16ff9-186">last</span><span class="sxs-lookup"><span data-stu-id="16ff9-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="16ff9-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="16ff9-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="16ff9-188">length</span><span class="sxs-lookup"><span data-stu-id="16ff9-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="16ff9-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="16ff9-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="16ff9-190">substitui</span><span class="sxs-lookup"><span data-stu-id="16ff9-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="16ff9-191">skip</span><span class="sxs-lookup"><span data-stu-id="16ff9-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="16ff9-192">split</span><span class="sxs-lookup"><span data-stu-id="16ff9-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="16ff9-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="16ff9-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="16ff9-194">string</span><span class="sxs-lookup"><span data-stu-id="16ff9-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="16ff9-195">substring</span><span class="sxs-lookup"><span data-stu-id="16ff9-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="16ff9-196">take</span><span class="sxs-lookup"><span data-stu-id="16ff9-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="16ff9-197">toLower</span><span class="sxs-lookup"><span data-stu-id="16ff9-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="16ff9-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="16ff9-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="16ff9-199">cortar</span><span class="sxs-lookup"><span data-stu-id="16ff9-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="16ff9-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="16ff9-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="16ff9-201">uri</span><span class="sxs-lookup"><span data-stu-id="16ff9-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="16ff9-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="16ff9-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="16ff9-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="16ff9-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="16ff9-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16ff9-204">Next steps</span></span>
* <span data-ttu-id="16ff9-205">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="16ff9-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="16ff9-206">toomerge vários modelos, consulte [usando modelos vinculados com o Gerenciador de recursos do Azure](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="16ff9-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="16ff9-207">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="16ff9-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="16ff9-208">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Gerenciador de recursos do Azure](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="16ff9-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

