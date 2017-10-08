---
title: aaaAzure Gerenciador de recursos de estrutura de modelo e a sintaxe | Microsoft Docs
description: "Descreve a estrutura de saudação e propriedades de modelos do Gerenciador de recursos do Azure usando a sintaxe JSON declarativa."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="7f0ae-103">Entender a estrutura de saudação e a sintaxe de modelos do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="7f0ae-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="7f0ae-104">Este tópico descreve a estrutura de saudação de um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="7f0ae-105">Ele apresenta seções diferentes de saudação de um modelo e hello propriedades disponíveis nessas seções.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="7f0ae-106">Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="7f0ae-107">Para ver um tutorial passo a passo sobre como criar um modelo, confira [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="7f0ae-108">Formato de modelo</span><span class="sxs-lookup"><span data-stu-id="7f0ae-108">Template format</span></span>
<span data-ttu-id="7f0ae-109">Em sua estrutura mais simples, um modelo contém Olá elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-109">In its simplest structure, a template contains hello following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="7f0ae-110">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="7f0ae-110">Element name</span></span> | <span data-ttu-id="7f0ae-111">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7f0ae-111">Required</span></span> | <span data-ttu-id="7f0ae-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f0ae-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f0ae-113">$schema</span><span class="sxs-lookup"><span data-stu-id="7f0ae-113">$schema</span></span> |<span data-ttu-id="7f0ae-114">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-114">Yes</span></span> |<span data-ttu-id="7f0ae-115">Local do arquivo de esquema do hello JSON que descreve a versão de saudação do idioma do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="7f0ae-116">Use URL Olá mostrada a saudação anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="7f0ae-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="7f0ae-117">contentVersion</span></span> |<span data-ttu-id="7f0ae-118">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-118">Yes</span></span> |<span data-ttu-id="7f0ae-119">Versão do modelo de saudação (por exemplo, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="7f0ae-120">Você pode fornecer qualquer valor para esse elemento.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-120">You can provide any value for this element.</span></span> <span data-ttu-id="7f0ae-121">Durante a implantação de recursos usando o modelo de hello, esse valor pode ser usado toomake-se de que o modelo certo hello está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="7f0ae-122">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7f0ae-122">parameters</span></span> |<span data-ttu-id="7f0ae-123">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-123">No</span></span> |<span data-ttu-id="7f0ae-124">Valores que são fornecidos quando a implantação é executado toocustomize implantação de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="7f0ae-125">variáveis</span><span class="sxs-lookup"><span data-stu-id="7f0ae-125">variables</span></span> |<span data-ttu-id="7f0ae-126">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-126">No</span></span> |<span data-ttu-id="7f0ae-127">Valores que são usados como fragmentos JSON em expressões de idioma Olá modelo toosimplify modelo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="7f0ae-128">recursos</span><span class="sxs-lookup"><span data-stu-id="7f0ae-128">resources</span></span> |<span data-ttu-id="7f0ae-129">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-129">Yes</span></span> |<span data-ttu-id="7f0ae-130">Tipos de recursos que são implantados ou atualizados em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="7f0ae-131">outputs</span><span class="sxs-lookup"><span data-stu-id="7f0ae-131">outputs</span></span> |<span data-ttu-id="7f0ae-132">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-132">No</span></span> |<span data-ttu-id="7f0ae-133">Valores que são retornados após a implantação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="7f0ae-134">Cada elemento contém propriedades que você pode definir.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-134">Each element contains properties you can set.</span></span> <span data-ttu-id="7f0ae-135">saudação de exemplo a seguir contém a sintaxe completa Olá para um modelo:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-135">hello following example contains hello full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="7f0ae-136">Podemos examinar seções de saudação do modelo de saudação em maiores detalhes posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="7f0ae-137">Expressões e funções</span><span class="sxs-lookup"><span data-stu-id="7f0ae-137">Expressions and functions</span></span>
<span data-ttu-id="7f0ae-138">sintaxe básica de saudação do modelo de saudação é JSON.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="7f0ae-139">No entanto, expressões e funções estendem valores JSON de saudação disponíveis no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="7f0ae-140">As expressões são escritas em literais de cadeia de caracteres JSON cujo primeiro e último caracteres são colchetes Olá: `[` e `]`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="7f0ae-141">valor de saudação da expressão de saudação é avaliado quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="7f0ae-142">Enquanto gravado como uma cadeia de caracteres literal, o resultado de saudação da avaliação de expressão Olá pode ser de um tipo diferente de JSON, como uma matriz ou um número inteiro, dependendo da expressão real hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="7f0ae-143">toohave uma cadeia de caracteres literal começar com um colchete `[`, mas não que ele seja interpretado como uma expressão, adicionar uma cadeia de caracteres do colchete extra toostart Olá com `[[`.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="7f0ae-144">Normalmente, você deve usar expressões com operações de tooperform de funções para a configuração de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="7f0ae-145">Assim como no JavaScript, as chamadas de função são formatadas como `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="7f0ae-146">Você pode referenciar propriedades usando os operadores de ponto e [index] hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="7f0ae-147">saudação de exemplo a seguir mostra como toouse várias funções ao construir valores:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="7f0ae-148">Para Olá a lista completa de funções de modelo, consulte [funções de modelo do Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="7f0ae-149">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7f0ae-149">Parameters</span></span>
<span data-ttu-id="7f0ae-150">Na seção de parâmetros de saudação do modelo hello, você especificar os valores que você pode inserir ao implantar Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="7f0ae-151">Esses valores de parâmetro habilite a implantação de saudação toocustomize fornecendo os valores que são adaptados para um ambiente específico (como desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="7f0ae-152">Você não tem parâmetros tooprovide em seu modelo, mas sem parâmetros seu modelo sempre implanta Olá mesmos recursos com hello mesmo nomes, locais e propriedades.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="7f0ae-153">Você pode definir parâmetros com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-153">You define parameters with hello following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="7f0ae-154">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="7f0ae-154">Element name</span></span> | <span data-ttu-id="7f0ae-155">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7f0ae-155">Required</span></span> | <span data-ttu-id="7f0ae-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f0ae-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f0ae-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="7f0ae-157">parameterName</span></span> |<span data-ttu-id="7f0ae-158">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-158">Yes</span></span> |<span data-ttu-id="7f0ae-159">Nome do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-159">Name of hello parameter.</span></span> <span data-ttu-id="7f0ae-160">Deve ser um identificador JavaScript válido.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="7f0ae-161">type</span><span class="sxs-lookup"><span data-stu-id="7f0ae-161">type</span></span> |<span data-ttu-id="7f0ae-162">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-162">Yes</span></span> |<span data-ttu-id="7f0ae-163">Tipo de valor de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-163">Type of hello parameter value.</span></span> <span data-ttu-id="7f0ae-164">Consulte a lista de saudação de tipos permitidos depois desta tabela.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="7f0ae-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="7f0ae-165">defaultValue</span></span> |<span data-ttu-id="7f0ae-166">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-166">No</span></span> |<span data-ttu-id="7f0ae-167">Valor padrão para o parâmetro hello, se nenhum valor for fornecido para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="7f0ae-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="7f0ae-168">allowedValues</span></span> |<span data-ttu-id="7f0ae-169">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-169">No</span></span> |<span data-ttu-id="7f0ae-170">Matriz de valores permitidos para Olá parâmetro toomake-se de que o valor de saudação à direita é fornecida.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="7f0ae-171">minValue</span><span class="sxs-lookup"><span data-stu-id="7f0ae-171">minValue</span></span> |<span data-ttu-id="7f0ae-172">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-172">No</span></span> |<span data-ttu-id="7f0ae-173">valor mínimo de saudação para parâmetros de tipo int, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="7f0ae-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="7f0ae-174">maxValue</span></span> |<span data-ttu-id="7f0ae-175">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-175">No</span></span> |<span data-ttu-id="7f0ae-176">valor máximo de saudação para parâmetros de tipo int, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="7f0ae-177">minLength</span><span class="sxs-lookup"><span data-stu-id="7f0ae-177">minLength</span></span> |<span data-ttu-id="7f0ae-178">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-178">No</span></span> |<span data-ttu-id="7f0ae-179">comprimento mínimo de saudação para parâmetros de tipo de matriz de cadeia de caracteres e secureString, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="7f0ae-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="7f0ae-180">maxLength</span></span> |<span data-ttu-id="7f0ae-181">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-181">No</span></span> |<span data-ttu-id="7f0ae-182">tamanho máximo de saudação para parâmetros de tipo de matriz de cadeia de caracteres e secureString, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="7f0ae-183">description</span><span class="sxs-lookup"><span data-stu-id="7f0ae-183">description</span></span> |<span data-ttu-id="7f0ae-184">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-184">No</span></span> |<span data-ttu-id="7f0ae-185">Descrição do parâmetro hello que é exibida toousers por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="7f0ae-186">Olá valores e tipos permitidos são:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="7f0ae-187">**string**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-187">**string**</span></span>
* <span data-ttu-id="7f0ae-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-188">**secureString**</span></span>
* <span data-ttu-id="7f0ae-189">**int**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-189">**int**</span></span>
* <span data-ttu-id="7f0ae-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-190">**bool**</span></span>
* <span data-ttu-id="7f0ae-191">**object**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-191">**object**</span></span> 
* <span data-ttu-id="7f0ae-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-192">**secureObject**</span></span>
* <span data-ttu-id="7f0ae-193">**array**</span><span class="sxs-lookup"><span data-stu-id="7f0ae-193">**array**</span></span>

<span data-ttu-id="7f0ae-194">toospecify um parâmetro como opcional, forneça um valor padrão (pode ser uma cadeia de caracteres vazia).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="7f0ae-195">Se você especificar um nome de parâmetro no modelo que corresponde a um parâmetro no modelo de Olá Olá comando toodeploy, há ambiguidade potencial sobre valores hello fornecidos por você.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="7f0ae-196">Gerenciador de recursos resolve essa confusão, adicionando o sufixo Olá **FromTemplate** toohello parâmetro de modelo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="7f0ae-197">Por exemplo, se você incluir um parâmetro chamado **ResourceGroupName** em seu modelo, ele entra em conflito com hello **ResourceGroupName** parâmetro hello [ Novo AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="7f0ae-198">Durante a implantação, é solicitada tooprovide um valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="7f0ae-199">Em geral, você deve evitar essa confusão ao não nomear parâmetros com o mesmo nome como parâmetros usados para operações de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="7f0ae-200">Todas as senhas, chaves e outros segredos devem usar Olá **secureString** tipo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="7f0ae-201">Se você passar dados confidenciais em um objeto JSON, use Olá **secureObject** tipo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="7f0ae-202">Os parâmetros de modelo com o tipo secureString ou secureObject não podem ser lidos após a implantação de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="7f0ae-203">Por exemplo, hello seguinte entrada no histórico da implantação Olá mostra Olá valor para uma cadeia de caracteres e objeto, mas não para secureString e secureObject.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![mostrar valores de implantação](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="7f0ae-205">Olá mostrado no exemplo a seguir como toodefine parâmetros:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-205">hello following example shows how toodefine parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="7f0ae-206">Para como valores de parâmetro de saudação tooinput durante a implantação, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="7f0ae-207">variáveis</span><span class="sxs-lookup"><span data-stu-id="7f0ae-207">Variables</span></span>
<span data-ttu-id="7f0ae-208">Na seção de variáveis Olá, você pode construir valores que podem ser usados em todo o modelo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="7f0ae-209">Você não precisa toodefine variáveis, mas eles geralmente simplificarem seu modelo, reduzindo expressões complexas.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="7f0ae-210">Você pode definir variáveis com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="7f0ae-211">Olá mostrado no exemplo a seguir como toodefine uma variável que é construída a partir de dois valores de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="7f0ae-212">Olá próximo exemplo mostra uma variável que é um tipo complexo de JSON e variáveis que são construídos a partir de outras variáveis:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="7f0ae-213">Recursos</span><span class="sxs-lookup"><span data-stu-id="7f0ae-213">Resources</span></span>
<span data-ttu-id="7f0ae-214">Na seção de recursos hello, você define os recursos de saudação que são implantados ou atualizados.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="7f0ae-215">Esta seção pode ficar complicada porque você deve entender a saudação tipos que você está implantando os valores corretos do tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="7f0ae-216">Para Olá recurso valores específicos (apiVersion, tipo e propriedades) que você precisa tooset, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="7f0ae-217">Você pode definir recursos com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-217">You define resources with hello following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="7f0ae-218">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="7f0ae-218">Element name</span></span> | <span data-ttu-id="7f0ae-219">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7f0ae-219">Required</span></span> | <span data-ttu-id="7f0ae-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f0ae-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f0ae-221">condition</span><span class="sxs-lookup"><span data-stu-id="7f0ae-221">condition</span></span> | <span data-ttu-id="7f0ae-222">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-222">No</span></span> | <span data-ttu-id="7f0ae-223">Valor booliano que indica se o recurso de saudação está implantado.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="7f0ae-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7f0ae-224">apiVersion</span></span> |<span data-ttu-id="7f0ae-225">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-225">Yes</span></span> |<span data-ttu-id="7f0ae-226">Versão do hello toouse de API REST para criar o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="7f0ae-227">type</span><span class="sxs-lookup"><span data-stu-id="7f0ae-227">type</span></span> |<span data-ttu-id="7f0ae-228">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-228">Yes</span></span> |<span data-ttu-id="7f0ae-229">Tipo de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-229">Type of hello resource.</span></span> <span data-ttu-id="7f0ae-230">Esse valor é uma combinação do namespace de saudação do provedor de recursos de saudação e o tipo de recurso de saudação (como **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="7f0ae-231">name</span><span class="sxs-lookup"><span data-stu-id="7f0ae-231">name</span></span> |<span data-ttu-id="7f0ae-232">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-232">Yes</span></span> |<span data-ttu-id="7f0ae-233">Nome do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-233">Name of hello resource.</span></span> <span data-ttu-id="7f0ae-234">Olá deverá seguir as restrições de componente URI definidas em RFC3986.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="7f0ae-235">Além disso, os serviços do Azure que expõem as partes de toooutside de nome de recurso Olá validar Olá nome toomake se ele não é uma tentativa de toospoof outra identidade.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="7f0ae-236">location</span><span class="sxs-lookup"><span data-stu-id="7f0ae-236">location</span></span> |<span data-ttu-id="7f0ae-237">Varia</span><span class="sxs-lookup"><span data-stu-id="7f0ae-237">Varies</span></span> |<span data-ttu-id="7f0ae-238">Locais geográficos com suporte de saudação fornecido recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="7f0ae-239">Você pode selecionar qualquer um dos locais disponíveis hello, mas geralmente faz sentido toopick aquele tooyour fechar usuários.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="7f0ae-240">Normalmente, isso também faz sentido tooplace recursos que interagem entre si em Olá mesmo região.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="7f0ae-241">A maioria dos tipos de recursos exige um local, mas alguns deles (como uma atribuição de função) não.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="7f0ae-242">Confira [Configure os locais dos recursos de modelos do Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="7f0ae-243">marcas</span><span class="sxs-lookup"><span data-stu-id="7f0ae-243">tags</span></span> |<span data-ttu-id="7f0ae-244">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-244">No</span></span> |<span data-ttu-id="7f0ae-245">Marcas que estão associadas a recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="7f0ae-246">Confira [Marque recursos em modelos do Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="7f0ae-247">comentários</span><span class="sxs-lookup"><span data-stu-id="7f0ae-247">comments</span></span> |<span data-ttu-id="7f0ae-248">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-248">No</span></span> |<span data-ttu-id="7f0ae-249">As anotações para documentar recursos Olá no modelo</span><span class="sxs-lookup"><span data-stu-id="7f0ae-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="7f0ae-250">cópia</span><span class="sxs-lookup"><span data-stu-id="7f0ae-250">copy</span></span> |<span data-ttu-id="7f0ae-251">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-251">No</span></span> |<span data-ttu-id="7f0ae-252">Se for necessário mais de uma instância, Olá inúmeros recursos toocreate.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="7f0ae-253">modo padrão de saudação é paralelo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-253">hello default mode is parallel.</span></span> <span data-ttu-id="7f0ae-254">Especifique o modo serial quando você não deseja que todos ou Olá toodeploy recursos em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="7f0ae-255">Para obter mais informações, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="7f0ae-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="7f0ae-256">dependsOn</span></span> |<span data-ttu-id="7f0ae-257">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-257">No</span></span> |<span data-ttu-id="7f0ae-258">Recursos que devem ser implantados antes deste recurso.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="7f0ae-259">Gerenciador de recursos avalia Olá dependências entre os recursos e implanta-os na ordem correta hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="7f0ae-260">Quando os recursos não dependem uns dos outros, são implantados paralelamente.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="7f0ae-261">Olá valor pode ser uma lista separada por vírgulas de um recurso nomes ou identificadores exclusivos de recurso.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="7f0ae-262">Somente lista recursos que são implantados neste modelo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="7f0ae-263">Recursos que não são definidos neste modelo já devem existir.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="7f0ae-264">Evite adicionar dependências desnecessárias, pois elas podem reduzir sua implantação e criar dependências circulares.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="7f0ae-265">Para obter orientação sobre como configurar as dependências, confira [Definir as dependências nos modelos do Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="7f0ae-266">propriedades</span><span class="sxs-lookup"><span data-stu-id="7f0ae-266">properties</span></span> |<span data-ttu-id="7f0ae-267">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-267">No</span></span> |<span data-ttu-id="7f0ae-268">Definições de configuração específicas do recurso.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="7f0ae-269">valores de saudação para propriedades de saudação são Olá mesmo como valores hello fornecer no corpo da solicitação de Olá Olá API REST operação (método PUT) toocreate Olá recurso.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="7f0ae-270">Você também pode especificar várias instâncias de uma propriedade de um toocreate de matriz de cópia.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="7f0ae-271">Para obter mais informações, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="7f0ae-272">recursos</span><span class="sxs-lookup"><span data-stu-id="7f0ae-272">resources</span></span> |<span data-ttu-id="7f0ae-273">Não</span><span class="sxs-lookup"><span data-stu-id="7f0ae-273">No</span></span> |<span data-ttu-id="7f0ae-274">Recursos filho que dependem do recurso hello está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="7f0ae-275">Forneça somente tipos de recursos que são permitidos pelo esquema de saudação do recurso pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="7f0ae-276">Olá totalmente qualificado do tipo de recurso de filho Olá inclui tipo de recurso Olá pai como **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="7f0ae-277">Dependência no recurso pai, Olá não é sugerida.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="7f0ae-278">Você deve definir explicitamente essa dependência.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="7f0ae-279">seção de recursos Olá contém uma matriz de saudação toodeploy de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="7f0ae-280">Em cada recurso, você também pode definir uma matriz de recursos filhos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="7f0ae-281">Portanto, a seção de recursos pode ter uma estrutura como:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="7f0ae-282">Para saber mais sobre como definir recursos filho, confira [Definir o nome e o tipo do recurso filho no modelo do Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="7f0ae-283">Olá **condição** elemento Especifica se o recurso de saudação é implantado.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="7f0ae-284">valor desse elemento Olá resolve tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="7f0ae-285">Por exemplo, toospecify se uma nova conta de armazenamento é implantada, use:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="7f0ae-286">Para obter um exemplo do uso de um recurso novo ou existente, consulte [Modelo de condição novo ou existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="7f0ae-287">toospecify se uma máquina virtual é implantada com uma senha ou chave SSH, definir duas versões da máquina virtual de saudação em seu modelo e usar **condição** toodifferentiate uso.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="7f0ae-288">Passe um parâmetro que especifica quais toodeploy do cenário.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="7f0ae-289">Para obter um exemplo do uso de uma senha ou a máquina de virtual toodeploy chave SSH, consulte [modelo de condição de nome de usuário ou o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="7f0ae-290">outputs</span><span class="sxs-lookup"><span data-stu-id="7f0ae-290">Outputs</span></span>
<span data-ttu-id="7f0ae-291">Na seção de saídas hello, você deve especificar valores que são retornados da implantação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="7f0ae-292">Por exemplo, você pode retornar Olá URI tooaccess um recurso implantado.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="7f0ae-293">Olá, exemplo a seguir mostra a estrutura de saudação de uma definição de saída:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="7f0ae-294">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="7f0ae-294">Element name</span></span> | <span data-ttu-id="7f0ae-295">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7f0ae-295">Required</span></span> | <span data-ttu-id="7f0ae-296">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f0ae-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f0ae-297">outputName</span><span class="sxs-lookup"><span data-stu-id="7f0ae-297">outputName</span></span> |<span data-ttu-id="7f0ae-298">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-298">Yes</span></span> |<span data-ttu-id="7f0ae-299">Nome do valor de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-299">Name of hello output value.</span></span> <span data-ttu-id="7f0ae-300">Deve ser um identificador JavaScript válido.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="7f0ae-301">type</span><span class="sxs-lookup"><span data-stu-id="7f0ae-301">type</span></span> |<span data-ttu-id="7f0ae-302">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-302">Yes</span></span> |<span data-ttu-id="7f0ae-303">Tipo de saudação do valor de saída.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-303">Type of hello output value.</span></span> <span data-ttu-id="7f0ae-304">Suportam a valores de saída Olá mesmo tipos como parâmetros de entrada do modelo.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="7f0ae-305">valor</span><span class="sxs-lookup"><span data-stu-id="7f0ae-305">value</span></span> |<span data-ttu-id="7f0ae-306">Sim</span><span class="sxs-lookup"><span data-stu-id="7f0ae-306">Yes</span></span> |<span data-ttu-id="7f0ae-307">Expressão de linguagem do modelo avaliada e retornada como valor de saída.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="7f0ae-308">Olá, exemplo a seguir mostra um valor que é retornado na seção de saídas de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="7f0ae-309">Para obter mais informações sobre como trabalhar com a saída, consulte [Compartilhando o estado nos modelos do Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="7f0ae-310">Limites de modelo</span><span class="sxs-lookup"><span data-stu-id="7f0ae-310">Template limits</span></span>

<span data-ttu-id="7f0ae-311">Limitar tamanho de saudação do seu modelo too1 MB e cada parâmetro arquivos too64 KB.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="7f0ae-312">limite de 1 MB de saudação se aplica a toohello o estado final do modelo de saudação depois que ela foi expandida com definições de recursos iterativo e valores para variáveis e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="7f0ae-313">Você também está limitado a:</span><span class="sxs-lookup"><span data-stu-id="7f0ae-313">You are also limited to:</span></span>

* <span data-ttu-id="7f0ae-314">256 parâmetros</span><span class="sxs-lookup"><span data-stu-id="7f0ae-314">256 parameters</span></span>
* <span data-ttu-id="7f0ae-315">256 variáveis</span><span class="sxs-lookup"><span data-stu-id="7f0ae-315">256 variables</span></span>
* <span data-ttu-id="7f0ae-316">800 recursos (incluindo a contagem de cópias)</span><span class="sxs-lookup"><span data-stu-id="7f0ae-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="7f0ae-317">64 valores de saída</span><span class="sxs-lookup"><span data-stu-id="7f0ae-317">64 output values</span></span>
* <span data-ttu-id="7f0ae-318">24.576 caracteres em uma expressão de modelo</span><span class="sxs-lookup"><span data-stu-id="7f0ae-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="7f0ae-319">Você pode exceder alguns limites de modelo usando um modelo aninhado.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="7f0ae-320">Para saber mais, confira [Uso de modelos vinculados ao implantar recursos do Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="7f0ae-321">número de saudação tooreduce de parâmetros, variáveis ou saídas, você pode combinar vários valores em um objeto.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="7f0ae-322">Para saber mais, veja [Objetos como parâmetros](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f0ae-323">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f0ae-323">Next steps</span></span>
* <span data-ttu-id="7f0ae-324">modelos de tooview completa para muitos tipos diferentes de soluções, consulte Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="7f0ae-325">Para obter detalhes sobre as funções hello você pode usar de dentro de um modelo, consulte [funções de modelo do Gerenciador de recursos do Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="7f0ae-326">toocombine vários modelos durante a implantação, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="7f0ae-327">Talvez seja necessário toouse recursos existentes dentro de um grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="7f0ae-328">Essa situação é comum ao trabalhar com contas de armazenamento ou redes virtuais compartilhadas com vários grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f0ae-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="7f0ae-329">Para obter mais informações, consulte Olá [função resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="7f0ae-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
