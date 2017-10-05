---
title: "Funções do modelo do Resource Manager | Microsoft Docs"
description: "Descreve as funções a serem usadas no modelo do Gerenciador de Recursos do Azure para recuperar valores, trabalhar com cadeias de caracteres e numéricos e recuperar informações de implantação."
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
ms.openlocfilehash: 1324bed07e991e9d84cb6832afe78bdb2d3348fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="57441-103">Funções do modelo do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="57441-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="57441-104">Este tópico descreve todas as funções que você pode usar em um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57441-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="57441-105">Você adiciona funções aos seus modelos colocando-as entre colchetes: `[` e `]`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="57441-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="57441-106">A expressão é avaliada durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="57441-106">The expression is evaluated during deployment.</span></span> <span data-ttu-id="57441-107">Embora escrito como um literal de cadeia de caracteres, o resultado da avaliação da expressão pode ser de um tipo JSON diferente, como uma matriz, um objeto ou um inteiro.</span><span class="sxs-lookup"><span data-stu-id="57441-107">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="57441-108">Assim como no JavaScript, as chamadas de função são formatadas como `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="57441-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="57441-109">Você faz referência às propriedades usando os operadores dot e [index].</span><span class="sxs-lookup"><span data-stu-id="57441-109">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="57441-110">Uma expressão de modelo não pode exceder 24.576 caracteres.</span><span class="sxs-lookup"><span data-stu-id="57441-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="57441-111">As funções do modelo e seus parâmetros não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="57441-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="57441-112">Por exemplo, o Resource Manager resolve **variables('var1')** e **VARIABLES('VAR1')** da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="57441-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="57441-113">Quando avaliada, a função preservará as maiúsculas e minúsculas, a menos que a função modifique-as expressamente (como toUpper ou toLower).</span><span class="sxs-lookup"><span data-stu-id="57441-113">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="57441-114">Determinados tipos de recursos podem ter requisitos de maiúsculas e minúsculas independentemente de como as funções são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="57441-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

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

## <a name="array-and-object-functions"></a><span data-ttu-id="57441-115">Funções de objeto e matriz</span><span class="sxs-lookup"><span data-stu-id="57441-115">Array and object functions</span></span>
<span data-ttu-id="57441-116">O Resource Manager fornece diversas funções para trabalhar com matrizes e objetos.</span><span class="sxs-lookup"><span data-stu-id="57441-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="57441-117">array</span><span class="sxs-lookup"><span data-stu-id="57441-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="57441-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="57441-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="57441-119">concat</span><span class="sxs-lookup"><span data-stu-id="57441-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="57441-120">contains</span><span class="sxs-lookup"><span data-stu-id="57441-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="57441-121">createArray</span><span class="sxs-lookup"><span data-stu-id="57441-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="57441-122">empty</span><span class="sxs-lookup"><span data-stu-id="57441-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="57441-123">first</span><span class="sxs-lookup"><span data-stu-id="57441-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="57441-124">intersection</span><span class="sxs-lookup"><span data-stu-id="57441-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="57441-125">json</span><span class="sxs-lookup"><span data-stu-id="57441-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="57441-126">last</span><span class="sxs-lookup"><span data-stu-id="57441-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="57441-127">length</span><span class="sxs-lookup"><span data-stu-id="57441-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="57441-128">min</span><span class="sxs-lookup"><span data-stu-id="57441-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="57441-129">max</span><span class="sxs-lookup"><span data-stu-id="57441-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="57441-130">range</span><span class="sxs-lookup"><span data-stu-id="57441-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="57441-131">skip</span><span class="sxs-lookup"><span data-stu-id="57441-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="57441-132">take</span><span class="sxs-lookup"><span data-stu-id="57441-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="57441-133">union</span><span class="sxs-lookup"><span data-stu-id="57441-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="57441-134">Funções de comparação</span><span class="sxs-lookup"><span data-stu-id="57441-134">Comparison functions</span></span>
<span data-ttu-id="57441-135">O Resource Manager fornece várias funções para fazer comparações em seus modelos.</span><span class="sxs-lookup"><span data-stu-id="57441-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="57441-136">equals</span><span class="sxs-lookup"><span data-stu-id="57441-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="57441-137">less</span><span class="sxs-lookup"><span data-stu-id="57441-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="57441-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="57441-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="57441-139">greater</span><span class="sxs-lookup"><span data-stu-id="57441-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="57441-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="57441-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="57441-141">Funções de valor de implantação</span><span class="sxs-lookup"><span data-stu-id="57441-141">Deployment value functions</span></span>
<span data-ttu-id="57441-142">O Gerenciador de Recursos fornece as seguintes funções para obter os valores de seções do modelo e os valores relacionados à implantação:</span><span class="sxs-lookup"><span data-stu-id="57441-142">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="57441-143">implantação</span><span class="sxs-lookup"><span data-stu-id="57441-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="57441-144">parâmetros</span><span class="sxs-lookup"><span data-stu-id="57441-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="57441-145">variáveis</span><span class="sxs-lookup"><span data-stu-id="57441-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a><span data-ttu-id="57441-146">Funções lógicas</span><span class="sxs-lookup"><span data-stu-id="57441-146">Logical functions</span></span>
<span data-ttu-id="57441-147">O Gerenciador de Recursos fornece as seguintes funções para trabalhar com condições lógicas:</span><span class="sxs-lookup"><span data-stu-id="57441-147">Resource Manager provides the following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="57441-148">e</span><span class="sxs-lookup"><span data-stu-id="57441-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="57441-149">bool</span><span class="sxs-lookup"><span data-stu-id="57441-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="57441-150">if</span><span class="sxs-lookup"><span data-stu-id="57441-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="57441-151">not</span><span class="sxs-lookup"><span data-stu-id="57441-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="57441-152">ou</span><span class="sxs-lookup"><span data-stu-id="57441-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="57441-153">Funções numéricas</span><span class="sxs-lookup"><span data-stu-id="57441-153">Numeric functions</span></span>
<span data-ttu-id="57441-154">O Gerenciador de Recursos fornece as seguintes funções para trabalhar com números inteiros:</span><span class="sxs-lookup"><span data-stu-id="57441-154">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="57441-155">adicionar</span><span class="sxs-lookup"><span data-stu-id="57441-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="57441-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="57441-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="57441-157">div</span><span class="sxs-lookup"><span data-stu-id="57441-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="57441-158">float</span><span class="sxs-lookup"><span data-stu-id="57441-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="57441-159">int</span><span class="sxs-lookup"><span data-stu-id="57441-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="57441-160">min</span><span class="sxs-lookup"><span data-stu-id="57441-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="57441-161">max</span><span class="sxs-lookup"><span data-stu-id="57441-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="57441-162">mod</span><span class="sxs-lookup"><span data-stu-id="57441-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="57441-163">mul</span><span class="sxs-lookup"><span data-stu-id="57441-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="57441-164">sub</span><span class="sxs-lookup"><span data-stu-id="57441-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="57441-165">Funções de recurso</span><span class="sxs-lookup"><span data-stu-id="57441-165">Resource functions</span></span>
<span data-ttu-id="57441-166">O Gerenciador de Recursos fornece as seguintes funções para obter valores de recurso:</span><span class="sxs-lookup"><span data-stu-id="57441-166">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="57441-167">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="57441-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="57441-168">providers</span><span class="sxs-lookup"><span data-stu-id="57441-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="57441-169">reference</span><span class="sxs-lookup"><span data-stu-id="57441-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="57441-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="57441-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="57441-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="57441-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="57441-172">subscription</span><span class="sxs-lookup"><span data-stu-id="57441-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a><span data-ttu-id="57441-173">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="57441-173">String functions</span></span>
<span data-ttu-id="57441-174">O Gerenciador de Recursos fornece as seguintes funções para trabalhar com cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="57441-174">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="57441-175">base64</span><span class="sxs-lookup"><span data-stu-id="57441-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="57441-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="57441-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="57441-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="57441-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="57441-178">concat</span><span class="sxs-lookup"><span data-stu-id="57441-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="57441-179">contains</span><span class="sxs-lookup"><span data-stu-id="57441-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="57441-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="57441-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="57441-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="57441-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="57441-182">empty</span><span class="sxs-lookup"><span data-stu-id="57441-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="57441-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="57441-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="57441-184">first</span><span class="sxs-lookup"><span data-stu-id="57441-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="57441-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="57441-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="57441-186">last</span><span class="sxs-lookup"><span data-stu-id="57441-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="57441-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="57441-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="57441-188">length</span><span class="sxs-lookup"><span data-stu-id="57441-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="57441-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="57441-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="57441-190">substitui</span><span class="sxs-lookup"><span data-stu-id="57441-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="57441-191">skip</span><span class="sxs-lookup"><span data-stu-id="57441-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="57441-192">split</span><span class="sxs-lookup"><span data-stu-id="57441-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="57441-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="57441-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="57441-194">string</span><span class="sxs-lookup"><span data-stu-id="57441-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="57441-195">substring</span><span class="sxs-lookup"><span data-stu-id="57441-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="57441-196">take</span><span class="sxs-lookup"><span data-stu-id="57441-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="57441-197">toLower</span><span class="sxs-lookup"><span data-stu-id="57441-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="57441-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="57441-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="57441-199">cortar</span><span class="sxs-lookup"><span data-stu-id="57441-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="57441-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="57441-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="57441-201">uri</span><span class="sxs-lookup"><span data-stu-id="57441-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="57441-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="57441-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="57441-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="57441-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="57441-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57441-204">Next steps</span></span>
* <span data-ttu-id="57441-205">Para obter uma descrição das seções de um modelo do Gerenciador de Recursos do Azure, veja a seção [Criando modelos do Gerenciador de Recursos do Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="57441-205">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="57441-206">Para mesclar diversos modelos, confira a seção [Como usar modelos vinculados com o Gerenciador de Recursos do Azure](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="57441-206">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="57441-207">Para iterar um número de vezes especificado ao criar um tipo de recurso, confira [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="57441-207">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="57441-208">Para ver como implantar o modelo que você criou, consulte [Implantar um aplicativo com o Modelo do Gerenciador de Recursos do Azure](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="57441-208">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

