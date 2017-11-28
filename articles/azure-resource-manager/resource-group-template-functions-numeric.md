---
title: "funções de modelo Gerenciador de recursos aaaAzure - numéricas | Microsoft Docs"
description: "Descreve Olá toouse de funções em um toowork de modelo do Gerenciador de recursos do Azure com números."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="a834b-103">Funções numéricas para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a834b-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="a834b-104">Gerenciador de recursos fornece Olá seguintes funções para trabalhar com números inteiros:</span><span class="sxs-lookup"><span data-stu-id="a834b-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="a834b-105">adicionar</span><span class="sxs-lookup"><span data-stu-id="a834b-105">add</span></span>](#add)
* [<span data-ttu-id="a834b-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="a834b-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="a834b-107">div</span><span class="sxs-lookup"><span data-stu-id="a834b-107">div</span></span>](#div)
* [<span data-ttu-id="a834b-108">float</span><span class="sxs-lookup"><span data-stu-id="a834b-108">float</span></span>](#float)
* [<span data-ttu-id="a834b-109">int</span><span class="sxs-lookup"><span data-stu-id="a834b-109">int</span></span>](#int)
* [<span data-ttu-id="a834b-110">min</span><span class="sxs-lookup"><span data-stu-id="a834b-110">min</span></span>](#min)
* [<span data-ttu-id="a834b-111">max</span><span class="sxs-lookup"><span data-stu-id="a834b-111">max</span></span>](#max)
* [<span data-ttu-id="a834b-112">mod</span><span class="sxs-lookup"><span data-stu-id="a834b-112">mod</span></span>](#mod)
* [<span data-ttu-id="a834b-113">mul</span><span class="sxs-lookup"><span data-stu-id="a834b-113">mul</span></span>](#mul)
* [<span data-ttu-id="a834b-114">sub</span><span class="sxs-lookup"><span data-stu-id="a834b-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="a834b-115">adicionar</span><span class="sxs-lookup"><span data-stu-id="a834b-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="a834b-116">Retorna Olá soma de números inteiros de fornecido hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-117">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-117">Parameters</span></span>

| <span data-ttu-id="a834b-118">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-118">Parameter</span></span> | <span data-ttu-id="a834b-119">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-119">Required</span></span> | <span data-ttu-id="a834b-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-120">Type</span></span> | <span data-ttu-id="a834b-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="a834b-122">operand1</span><span class="sxs-lookup"><span data-stu-id="a834b-122">operand1</span></span> |<span data-ttu-id="a834b-123">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-123">Yes</span></span> |<span data-ttu-id="a834b-124">int</span><span class="sxs-lookup"><span data-stu-id="a834b-124">int</span></span> |<span data-ttu-id="a834b-125">Primeiro número tooadd.</span><span class="sxs-lookup"><span data-stu-id="a834b-125">First number tooadd.</span></span> |
|<span data-ttu-id="a834b-126">operand2</span><span class="sxs-lookup"><span data-stu-id="a834b-126">operand2</span></span> |<span data-ttu-id="a834b-127">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-127">Yes</span></span> |<span data-ttu-id="a834b-128">int</span><span class="sxs-lookup"><span data-stu-id="a834b-128">int</span></span> |<span data-ttu-id="a834b-129">Segundo tooadd número.</span><span class="sxs-lookup"><span data-stu-id="a834b-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-130">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-130">Return value</span></span>

<span data-ttu-id="a834b-131">Um inteiro que contém a soma de saudação de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="a834b-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-132">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-132">Example</span></span>

<span data-ttu-id="a834b-133">saudação de exemplo a seguir adiciona dois parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a834b-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="a834b-134">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-135">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-135">Name</span></span> | <span data-ttu-id="a834b-136">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-136">Type</span></span> | <span data-ttu-id="a834b-137">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-138">addResult</span><span class="sxs-lookup"><span data-stu-id="a834b-138">addResult</span></span> | <span data-ttu-id="a834b-139">int</span><span class="sxs-lookup"><span data-stu-id="a834b-139">Int</span></span> | <span data-ttu-id="a834b-140">8</span><span class="sxs-lookup"><span data-stu-id="a834b-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="a834b-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="a834b-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="a834b-142">Retorna Olá índice de um loop de iteração.</span><span class="sxs-lookup"><span data-stu-id="a834b-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="a834b-143">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-143">Parameters</span></span>

| <span data-ttu-id="a834b-144">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-144">Parameter</span></span> | <span data-ttu-id="a834b-145">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-145">Required</span></span> | <span data-ttu-id="a834b-146">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-146">Type</span></span> | <span data-ttu-id="a834b-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-148">loopName</span><span class="sxs-lookup"><span data-stu-id="a834b-148">loopName</span></span> | <span data-ttu-id="a834b-149">Não</span><span class="sxs-lookup"><span data-stu-id="a834b-149">No</span></span> | <span data-ttu-id="a834b-150">string</span><span class="sxs-lookup"><span data-stu-id="a834b-150">string</span></span> | <span data-ttu-id="a834b-151">nome de saudação de loop Olá para obtenção de iteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="a834b-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="a834b-152">deslocamento</span><span class="sxs-lookup"><span data-stu-id="a834b-152">offset</span></span> |<span data-ttu-id="a834b-153">Não</span><span class="sxs-lookup"><span data-stu-id="a834b-153">No</span></span> |<span data-ttu-id="a834b-154">int</span><span class="sxs-lookup"><span data-stu-id="a834b-154">int</span></span> |<span data-ttu-id="a834b-155">Olá valor numérico de tooadd toohello iteração com base em zero.</span><span class="sxs-lookup"><span data-stu-id="a834b-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="a834b-156">Comentários</span><span class="sxs-lookup"><span data-stu-id="a834b-156">Remarks</span></span>

<span data-ttu-id="a834b-157">Essa função é sempre usada com um objeto **copy** .</span><span class="sxs-lookup"><span data-stu-id="a834b-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="a834b-158">Se nenhum valor for fornecido para **deslocamento**, o valor de iteração atual Olá é retornado.</span><span class="sxs-lookup"><span data-stu-id="a834b-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="a834b-159">valor de iteração Olá começa em zero.</span><span class="sxs-lookup"><span data-stu-id="a834b-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="a834b-160">Olá **loopName** propriedade permite que você toospecify se copyIndex se refere a iteração de recurso tooa ou iteração de propriedade.</span><span class="sxs-lookup"><span data-stu-id="a834b-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="a834b-161">Se nenhum valor for fornecido para **loopName**, Olá atual iteração de tipo de recurso é usada.</span><span class="sxs-lookup"><span data-stu-id="a834b-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="a834b-162">Forneça um valor para **loopName** durante a iteração em uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="a834b-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="a834b-163">Para obter uma descrição completa de como usar **copyIndex**, confira [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a834b-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="a834b-164">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-164">Example</span></span>

<span data-ttu-id="a834b-165">Olá exemplo a seguir mostra um loop e hello índice valor cópia incluído no nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="a834b-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="a834b-166">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-166">Return value</span></span>

<span data-ttu-id="a834b-167">Um inteiro que representa o índice de iteração Olá atual hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="a834b-168">div</span><span class="sxs-lookup"><span data-stu-id="a834b-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="a834b-169">Retorna Olá divisão de dois inteiros de fornecido hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-170">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-170">Parameters</span></span>

| <span data-ttu-id="a834b-171">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-171">Parameter</span></span> | <span data-ttu-id="a834b-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-172">Required</span></span> | <span data-ttu-id="a834b-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-173">Type</span></span> | <span data-ttu-id="a834b-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-175">operand1</span><span class="sxs-lookup"><span data-stu-id="a834b-175">operand1</span></span> |<span data-ttu-id="a834b-176">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-176">Yes</span></span> |<span data-ttu-id="a834b-177">int</span><span class="sxs-lookup"><span data-stu-id="a834b-177">int</span></span> |<span data-ttu-id="a834b-178">número de Hello está sendo dividido.</span><span class="sxs-lookup"><span data-stu-id="a834b-178">hello number being divided.</span></span> |
| <span data-ttu-id="a834b-179">operand2</span><span class="sxs-lookup"><span data-stu-id="a834b-179">operand2</span></span> |<span data-ttu-id="a834b-180">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-180">Yes</span></span> |<span data-ttu-id="a834b-181">int</span><span class="sxs-lookup"><span data-stu-id="a834b-181">int</span></span> |<span data-ttu-id="a834b-182">Olá número toodivide usado.</span><span class="sxs-lookup"><span data-stu-id="a834b-182">hello number that is used toodivide.</span></span> <span data-ttu-id="a834b-183">Não pode ser 0.</span><span class="sxs-lookup"><span data-stu-id="a834b-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-184">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-184">Return value</span></span>

<span data-ttu-id="a834b-185">Divisão de saudação representando um inteiro.</span><span class="sxs-lookup"><span data-stu-id="a834b-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-186">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-186">Example</span></span>

<span data-ttu-id="a834b-187">saudação de exemplo a seguir divide um parâmetro por outro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a834b-187">hello following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="a834b-188">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-189">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-189">Name</span></span> | <span data-ttu-id="a834b-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-190">Type</span></span> | <span data-ttu-id="a834b-191">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-192">divResult</span><span class="sxs-lookup"><span data-stu-id="a834b-192">divResult</span></span> | <span data-ttu-id="a834b-193">int</span><span class="sxs-lookup"><span data-stu-id="a834b-193">Int</span></span> | <span data-ttu-id="a834b-194">2</span><span class="sxs-lookup"><span data-stu-id="a834b-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="a834b-195">flutuante</span><span class="sxs-lookup"><span data-stu-id="a834b-195">float</span></span>
`float(arg1)`

<span data-ttu-id="a834b-196">Converte Olá valor tooa número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="a834b-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="a834b-197">Você só usar essa função ao passar parâmetros personalizados tooan aplicativo, como um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a834b-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-198">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-198">Parameters</span></span>

| <span data-ttu-id="a834b-199">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-199">Parameter</span></span> | <span data-ttu-id="a834b-200">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-200">Required</span></span> | <span data-ttu-id="a834b-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-201">Type</span></span> | <span data-ttu-id="a834b-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-203">arg1</span><span class="sxs-lookup"><span data-stu-id="a834b-203">arg1</span></span> |<span data-ttu-id="a834b-204">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-204">Yes</span></span> |<span data-ttu-id="a834b-205">string ou int</span><span class="sxs-lookup"><span data-stu-id="a834b-205">string or int</span></span> |<span data-ttu-id="a834b-206">Olá valor tooconvert tooa número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="a834b-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-207">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-207">Return value</span></span>
<span data-ttu-id="a834b-208">Um número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="a834b-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-209">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-209">Example</span></span>

<span data-ttu-id="a834b-210">saudação de exemplo a seguir mostra como toouse float toopass parâmetros tooa lógica de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="a834b-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="a834b-211">int</span><span class="sxs-lookup"><span data-stu-id="a834b-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="a834b-212">Converte o inteiro de tooan Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="a834b-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-213">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-213">Parameters</span></span>

| <span data-ttu-id="a834b-214">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-214">Parameter</span></span> | <span data-ttu-id="a834b-215">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-215">Required</span></span> | <span data-ttu-id="a834b-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-216">Type</span></span> | <span data-ttu-id="a834b-217">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="a834b-218">valueToConvert</span></span> |<span data-ttu-id="a834b-219">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-219">Yes</span></span> |<span data-ttu-id="a834b-220">string ou int</span><span class="sxs-lookup"><span data-stu-id="a834b-220">string or int</span></span> |<span data-ttu-id="a834b-221">inteiro de tooan tooconvert do valor Hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-222">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-222">Return value</span></span>

<span data-ttu-id="a834b-223">Um inteiro de valor Olá convertido.</span><span class="sxs-lookup"><span data-stu-id="a834b-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-224">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-224">Example</span></span>

<span data-ttu-id="a834b-225">Olá, exemplo a seguir converte Olá toointeger de valor de parâmetro fornecido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="a834b-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="a834b-226">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-227">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-227">Name</span></span> | <span data-ttu-id="a834b-228">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-228">Type</span></span> | <span data-ttu-id="a834b-229">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-230">intResult</span><span class="sxs-lookup"><span data-stu-id="a834b-230">intResult</span></span> | <span data-ttu-id="a834b-231">int</span><span class="sxs-lookup"><span data-stu-id="a834b-231">Int</span></span> | <span data-ttu-id="a834b-232">4</span><span class="sxs-lookup"><span data-stu-id="a834b-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="a834b-233">Min</span><span class="sxs-lookup"><span data-stu-id="a834b-233">min</span></span>
`min (arg1)`

<span data-ttu-id="a834b-234">Retorna Olá valor mínimo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.</span><span class="sxs-lookup"><span data-stu-id="a834b-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-235">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-235">Parameters</span></span>

| <span data-ttu-id="a834b-236">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-236">Parameter</span></span> | <span data-ttu-id="a834b-237">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-237">Required</span></span> | <span data-ttu-id="a834b-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-238">Type</span></span> | <span data-ttu-id="a834b-239">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-240">arg1</span><span class="sxs-lookup"><span data-stu-id="a834b-240">arg1</span></span> |<span data-ttu-id="a834b-241">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-241">Yes</span></span> |<span data-ttu-id="a834b-242">matriz de inteiros ou lista de inteiros separados por vírgulas</span><span class="sxs-lookup"><span data-stu-id="a834b-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="a834b-243">Olá coleção tooget Olá valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="a834b-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-244">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-244">Return value</span></span>

<span data-ttu-id="a834b-245">Um inteiro que representa o valor mínimo da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="a834b-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-246">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-246">Example</span></span>

<span data-ttu-id="a834b-247">Olá mostrado no exemplo a seguir como min toouse com uma matriz e uma lista de números inteiros:</span><span class="sxs-lookup"><span data-stu-id="a834b-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="a834b-248">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-249">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-249">Name</span></span> | <span data-ttu-id="a834b-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-250">Type</span></span> | <span data-ttu-id="a834b-251">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a834b-252">arrayOutput</span></span> | <span data-ttu-id="a834b-253">int</span><span class="sxs-lookup"><span data-stu-id="a834b-253">Int</span></span> | <span data-ttu-id="a834b-254">0</span><span class="sxs-lookup"><span data-stu-id="a834b-254">0</span></span> |
| <span data-ttu-id="a834b-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="a834b-255">intOutput</span></span> | <span data-ttu-id="a834b-256">int</span><span class="sxs-lookup"><span data-stu-id="a834b-256">Int</span></span> | <span data-ttu-id="a834b-257">0</span><span class="sxs-lookup"><span data-stu-id="a834b-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="a834b-258">max</span><span class="sxs-lookup"><span data-stu-id="a834b-258">max</span></span>
`max (arg1)`

<span data-ttu-id="a834b-259">Retorna Olá valor máximo de uma matriz de inteiros ou uma lista separada por vírgulas de números inteiros.</span><span class="sxs-lookup"><span data-stu-id="a834b-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-260">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-260">Parameters</span></span>

| <span data-ttu-id="a834b-261">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-261">Parameter</span></span> | <span data-ttu-id="a834b-262">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-262">Required</span></span> | <span data-ttu-id="a834b-263">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-263">Type</span></span> | <span data-ttu-id="a834b-264">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-265">arg1</span><span class="sxs-lookup"><span data-stu-id="a834b-265">arg1</span></span> |<span data-ttu-id="a834b-266">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-266">Yes</span></span> |<span data-ttu-id="a834b-267">matriz de inteiros ou lista de inteiros separados por vírgulas</span><span class="sxs-lookup"><span data-stu-id="a834b-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="a834b-268">Olá coleção tooget Olá valor máximo.</span><span class="sxs-lookup"><span data-stu-id="a834b-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-269">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-269">Return value</span></span>

<span data-ttu-id="a834b-270">Um inteiro que representa o valor máximo de saudação da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="a834b-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-271">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-271">Example</span></span>

<span data-ttu-id="a834b-272">Olá mostrado no exemplo a seguir como toouse max com uma matriz e uma lista de números inteiros:</span><span class="sxs-lookup"><span data-stu-id="a834b-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="a834b-273">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-274">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-274">Name</span></span> | <span data-ttu-id="a834b-275">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-275">Type</span></span> | <span data-ttu-id="a834b-276">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a834b-277">arrayOutput</span></span> | <span data-ttu-id="a834b-278">int</span><span class="sxs-lookup"><span data-stu-id="a834b-278">Int</span></span> | <span data-ttu-id="a834b-279">5</span><span class="sxs-lookup"><span data-stu-id="a834b-279">5</span></span> |
| <span data-ttu-id="a834b-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="a834b-280">intOutput</span></span> | <span data-ttu-id="a834b-281">int</span><span class="sxs-lookup"><span data-stu-id="a834b-281">Int</span></span> | <span data-ttu-id="a834b-282">5</span><span class="sxs-lookup"><span data-stu-id="a834b-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="a834b-283">mod</span><span class="sxs-lookup"><span data-stu-id="a834b-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="a834b-284">Retorna o resto de saudação de divisão hello usando números inteiros de fornecido hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-285">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-285">Parameters</span></span>

| <span data-ttu-id="a834b-286">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-286">Parameter</span></span> | <span data-ttu-id="a834b-287">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-287">Required</span></span> | <span data-ttu-id="a834b-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-288">Type</span></span> | <span data-ttu-id="a834b-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-290">operand1</span><span class="sxs-lookup"><span data-stu-id="a834b-290">operand1</span></span> |<span data-ttu-id="a834b-291">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-291">Yes</span></span> |<span data-ttu-id="a834b-292">int</span><span class="sxs-lookup"><span data-stu-id="a834b-292">int</span></span> |<span data-ttu-id="a834b-293">número de Hello está sendo dividido.</span><span class="sxs-lookup"><span data-stu-id="a834b-293">hello number being divided.</span></span> |
| <span data-ttu-id="a834b-294">operand2</span><span class="sxs-lookup"><span data-stu-id="a834b-294">operand2</span></span> |<span data-ttu-id="a834b-295">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-295">Yes</span></span> |<span data-ttu-id="a834b-296">int</span><span class="sxs-lookup"><span data-stu-id="a834b-296">int</span></span> |<span data-ttu-id="a834b-297">número de saudação toodivide usado, não pode ser 0.</span><span class="sxs-lookup"><span data-stu-id="a834b-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-298">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-298">Return value</span></span>
<span data-ttu-id="a834b-299">Um resto Olá representando inteiro.</span><span class="sxs-lookup"><span data-stu-id="a834b-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-300">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-300">Example</span></span>

<span data-ttu-id="a834b-301">Olá, exemplo a seguir retorna Olá resto da divisão de um parâmetro por outro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a834b-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="a834b-302">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-303">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-303">Name</span></span> | <span data-ttu-id="a834b-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-304">Type</span></span> | <span data-ttu-id="a834b-305">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-306">modResult</span><span class="sxs-lookup"><span data-stu-id="a834b-306">modResult</span></span> | <span data-ttu-id="a834b-307">int</span><span class="sxs-lookup"><span data-stu-id="a834b-307">Int</span></span> | <span data-ttu-id="a834b-308">1</span><span class="sxs-lookup"><span data-stu-id="a834b-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="a834b-309">mul</span><span class="sxs-lookup"><span data-stu-id="a834b-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="a834b-310">Retorna Olá multiplicação de dois inteiros de fornecido hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-311">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-311">Parameters</span></span>

| <span data-ttu-id="a834b-312">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-312">Parameter</span></span> | <span data-ttu-id="a834b-313">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-313">Required</span></span> | <span data-ttu-id="a834b-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-314">Type</span></span> | <span data-ttu-id="a834b-315">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-316">operand1</span><span class="sxs-lookup"><span data-stu-id="a834b-316">operand1</span></span> |<span data-ttu-id="a834b-317">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-317">Yes</span></span> |<span data-ttu-id="a834b-318">int</span><span class="sxs-lookup"><span data-stu-id="a834b-318">int</span></span> |<span data-ttu-id="a834b-319">Primeiro número toomultiply.</span><span class="sxs-lookup"><span data-stu-id="a834b-319">First number toomultiply.</span></span> |
| <span data-ttu-id="a834b-320">operand2</span><span class="sxs-lookup"><span data-stu-id="a834b-320">operand2</span></span> |<span data-ttu-id="a834b-321">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-321">Yes</span></span> |<span data-ttu-id="a834b-322">int</span><span class="sxs-lookup"><span data-stu-id="a834b-322">int</span></span> |<span data-ttu-id="a834b-323">Segundo toomultiply número.</span><span class="sxs-lookup"><span data-stu-id="a834b-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-324">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-324">Return value</span></span>

<span data-ttu-id="a834b-325">Multiplicação de saudação representando um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="a834b-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-326">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-326">Example</span></span>

<span data-ttu-id="a834b-327">saudação de exemplo a seguir multiplica um parâmetro por outro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a834b-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="a834b-328">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-329">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-329">Name</span></span> | <span data-ttu-id="a834b-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-330">Type</span></span> | <span data-ttu-id="a834b-331">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="a834b-332">mulResult</span></span> | <span data-ttu-id="a834b-333">int</span><span class="sxs-lookup"><span data-stu-id="a834b-333">Int</span></span> | <span data-ttu-id="a834b-334">15</span><span class="sxs-lookup"><span data-stu-id="a834b-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="a834b-335">sub</span><span class="sxs-lookup"><span data-stu-id="a834b-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="a834b-336">Retorna Olá subtração dos números inteiros de fornecido hello.</span><span class="sxs-lookup"><span data-stu-id="a834b-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a834b-337">parâmetros</span><span class="sxs-lookup"><span data-stu-id="a834b-337">Parameters</span></span>

| <span data-ttu-id="a834b-338">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a834b-338">Parameter</span></span> | <span data-ttu-id="a834b-339">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a834b-339">Required</span></span> | <span data-ttu-id="a834b-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-340">Type</span></span> | <span data-ttu-id="a834b-341">Descrição</span><span class="sxs-lookup"><span data-stu-id="a834b-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a834b-342">operand1</span><span class="sxs-lookup"><span data-stu-id="a834b-342">operand1</span></span> |<span data-ttu-id="a834b-343">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-343">Yes</span></span> |<span data-ttu-id="a834b-344">int</span><span class="sxs-lookup"><span data-stu-id="a834b-344">int</span></span> |<span data-ttu-id="a834b-345">número de saudação que é subtraído.</span><span class="sxs-lookup"><span data-stu-id="a834b-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="a834b-346">operand2</span><span class="sxs-lookup"><span data-stu-id="a834b-346">operand2</span></span> |<span data-ttu-id="a834b-347">Sim</span><span class="sxs-lookup"><span data-stu-id="a834b-347">Yes</span></span> |<span data-ttu-id="a834b-348">int</span><span class="sxs-lookup"><span data-stu-id="a834b-348">int</span></span> |<span data-ttu-id="a834b-349">número de saudação que é subtraído.</span><span class="sxs-lookup"><span data-stu-id="a834b-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a834b-350">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="a834b-350">Return value</span></span>
<span data-ttu-id="a834b-351">Subtração de saudação representando um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="a834b-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="a834b-352">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a834b-352">Example</span></span>

<span data-ttu-id="a834b-353">saudação de exemplo a seguir subtrai um parâmetro de outro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a834b-353">hello following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="a834b-354">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="a834b-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a834b-355">Nome</span><span class="sxs-lookup"><span data-stu-id="a834b-355">Name</span></span> | <span data-ttu-id="a834b-356">Tipo</span><span class="sxs-lookup"><span data-stu-id="a834b-356">Type</span></span> | <span data-ttu-id="a834b-357">Valor</span><span class="sxs-lookup"><span data-stu-id="a834b-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a834b-358">subResult</span><span class="sxs-lookup"><span data-stu-id="a834b-358">subResult</span></span> | <span data-ttu-id="a834b-359">int</span><span class="sxs-lookup"><span data-stu-id="a834b-359">Int</span></span> | <span data-ttu-id="a834b-360">4</span><span class="sxs-lookup"><span data-stu-id="a834b-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a834b-361">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a834b-361">Next steps</span></span>
* <span data-ttu-id="a834b-362">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a834b-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a834b-363">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a834b-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="a834b-364">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a834b-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="a834b-365">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a834b-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

