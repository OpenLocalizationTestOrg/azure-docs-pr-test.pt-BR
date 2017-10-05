---
title: Estrutura e sintaxe do modelo do Azure Resource Manager | Microsoft Docs
description: Descreve a estrutura e as propriedades dos modelos do Azure Resource Manager usando a sintaxe JSON declarativa.
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
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="10a53-103">Noções básicas de estrutura e sintaxe dos modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10a53-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="10a53-104">Este tópico descreve a estrutura de um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10a53-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="10a53-105">Ele apresenta as diferentes seções de um modelo e as propriedades que estão disponíveis nessas seções.</span><span class="sxs-lookup"><span data-stu-id="10a53-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="10a53-106">O modelo consiste em JSON e expressões que podem ser usados na criação de valores para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="10a53-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="10a53-107">Para ver um tutorial passo a passo sobre como criar um modelo, confira [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="10a53-108">Formato de modelo</span><span class="sxs-lookup"><span data-stu-id="10a53-108">Template format</span></span>
<span data-ttu-id="10a53-109">Em sua estrutura mais simples, um modelo contém os seguintes elementos:</span><span class="sxs-lookup"><span data-stu-id="10a53-109">In its simplest structure, a template contains the following elements:</span></span>

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

| <span data-ttu-id="10a53-110">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="10a53-110">Element name</span></span> | <span data-ttu-id="10a53-111">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="10a53-111">Required</span></span> | <span data-ttu-id="10a53-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="10a53-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="10a53-113">$schema</span><span class="sxs-lookup"><span data-stu-id="10a53-113">$schema</span></span> |<span data-ttu-id="10a53-114">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-114">Yes</span></span> |<span data-ttu-id="10a53-115">Local do arquivo de esquema JSON que descreve a versão da linguagem do modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="10a53-116">Use a URL mostrada no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="10a53-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="10a53-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="10a53-117">contentVersion</span></span> |<span data-ttu-id="10a53-118">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-118">Yes</span></span> |<span data-ttu-id="10a53-119">Versão do modelo (como 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="10a53-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="10a53-120">Você pode fornecer qualquer valor para esse elemento.</span><span class="sxs-lookup"><span data-stu-id="10a53-120">You can provide any value for this element.</span></span> <span data-ttu-id="10a53-121">Ao implantar recursos com o modelo, esse valor pode ser usado para garantir que o modelo certo esteja sendo usado.</span><span class="sxs-lookup"><span data-stu-id="10a53-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="10a53-122">parameters</span><span class="sxs-lookup"><span data-stu-id="10a53-122">parameters</span></span> |<span data-ttu-id="10a53-123">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-123">No</span></span> |<span data-ttu-id="10a53-124">Valores que são fornecidos quando a implantação é executada para personalizar a implantação dos recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="10a53-125">variáveis</span><span class="sxs-lookup"><span data-stu-id="10a53-125">variables</span></span> |<span data-ttu-id="10a53-126">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-126">No</span></span> |<span data-ttu-id="10a53-127">Valores que são usados como fragmentos JSON no modelo para simplificar expressões de linguagem do modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="10a53-128">recursos</span><span class="sxs-lookup"><span data-stu-id="10a53-128">resources</span></span> |<span data-ttu-id="10a53-129">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-129">Yes</span></span> |<span data-ttu-id="10a53-130">Tipos de recursos que são implantados ou atualizados em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="10a53-131">outputs</span><span class="sxs-lookup"><span data-stu-id="10a53-131">outputs</span></span> |<span data-ttu-id="10a53-132">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-132">No</span></span> |<span data-ttu-id="10a53-133">Valores que são retornados após a implantação.</span><span class="sxs-lookup"><span data-stu-id="10a53-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="10a53-134">Cada elemento contém propriedades que você pode definir.</span><span class="sxs-lookup"><span data-stu-id="10a53-134">Each element contains properties you can set.</span></span> <span data-ttu-id="10a53-135">O seguinte exemplo contém a sintaxe completa de um modelo:</span><span class="sxs-lookup"><span data-stu-id="10a53-135">The following example contains the full syntax for a template:</span></span>

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
                "description": "<description-of-the parameter>" 
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

<span data-ttu-id="10a53-136">Examinaremos as seções do modelo em detalhes mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="10a53-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="10a53-137">Expressões e funções</span><span class="sxs-lookup"><span data-stu-id="10a53-137">Expressions and functions</span></span>
<span data-ttu-id="10a53-138">A sintaxe básica do modelo é JSON.</span><span class="sxs-lookup"><span data-stu-id="10a53-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="10a53-139">No entanto, as expressões e as funções estendem os valores JSON disponíveis no modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="10a53-140">As expressões são escritas em literais de cadeia de caracteres JSON cujo primeiro e último caracteres são os colchetes: `[` e `]`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="10a53-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="10a53-141">O valor da expressão é avaliado quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="10a53-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="10a53-142">Embora gravado como um literal de cadeia de caracteres, o resultado da avaliação da expressão pode ser de um tipo JSON diferente, como uma matriz ou um inteiro, dependendo da expressão real.</span><span class="sxs-lookup"><span data-stu-id="10a53-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="10a53-143">Para ter uma cadeia de caracteres literal que começa com um colchete `[`, mas que não é interpretada como uma expressão, adicione um colchete extra para iniciar a cadeia de caracteres com `[[`.</span><span class="sxs-lookup"><span data-stu-id="10a53-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="10a53-144">Normalmente, você usa expressões com funções para executar operações e configurar a implantação.</span><span class="sxs-lookup"><span data-stu-id="10a53-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="10a53-145">Assim como no JavaScript, as chamadas de função são formatadas como `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="10a53-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="10a53-146">Você faz referência às propriedades usando os operadores dot e [index].</span><span class="sxs-lookup"><span data-stu-id="10a53-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="10a53-147">O seguinte exemplo mostra como usar várias das funções ao construir valores:</span><span class="sxs-lookup"><span data-stu-id="10a53-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="10a53-148">Para obter a lista completa das funções de modelo, veja [Funções de modelo do Gerenciador de Recursos do Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="10a53-149">parameters</span><span class="sxs-lookup"><span data-stu-id="10a53-149">Parameters</span></span>
<span data-ttu-id="10a53-150">Na seção de parâmetros do modelo, você deve especificar os valores que você pode inserir ao implantar os recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="10a53-151">Esses valores de parâmetro permitem personalizar a implantação fornecendo valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="10a53-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="10a53-152">Você não precisa fornecer parâmetros em seu modelo, mas sem parâmetros o modelo sempre implantaria os mesmos recursos com o mesmo nomes, locais e propriedades.</span><span class="sxs-lookup"><span data-stu-id="10a53-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="10a53-153">Você define parâmetros com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="10a53-153">You define parameters with the following structure:</span></span>

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
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="10a53-154">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="10a53-154">Element name</span></span> | <span data-ttu-id="10a53-155">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="10a53-155">Required</span></span> | <span data-ttu-id="10a53-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="10a53-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="10a53-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="10a53-157">parameterName</span></span> |<span data-ttu-id="10a53-158">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-158">Yes</span></span> |<span data-ttu-id="10a53-159">Nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="10a53-159">Name of the parameter.</span></span> <span data-ttu-id="10a53-160">Deve ser um identificador JavaScript válido.</span><span class="sxs-lookup"><span data-stu-id="10a53-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="10a53-161">type</span><span class="sxs-lookup"><span data-stu-id="10a53-161">type</span></span> |<span data-ttu-id="10a53-162">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-162">Yes</span></span> |<span data-ttu-id="10a53-163">Tipo do valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="10a53-163">Type of the parameter value.</span></span> <span data-ttu-id="10a53-164">Consulte a lista de tipos permitidos após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="10a53-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="10a53-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="10a53-165">defaultValue</span></span> |<span data-ttu-id="10a53-166">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-166">No</span></span> |<span data-ttu-id="10a53-167">Valor padrão do parâmetro, se nenhum valor for fornecido para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="10a53-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="10a53-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="10a53-168">allowedValues</span></span> |<span data-ttu-id="10a53-169">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-169">No</span></span> |<span data-ttu-id="10a53-170">Matriz de valores permitidos para o parâmetro para garantir que o valor correto seja fornecido.</span><span class="sxs-lookup"><span data-stu-id="10a53-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="10a53-171">minValue</span><span class="sxs-lookup"><span data-stu-id="10a53-171">minValue</span></span> |<span data-ttu-id="10a53-172">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-172">No</span></span> |<span data-ttu-id="10a53-173">O valor mínimo para parâmetros de tipo int, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="10a53-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="10a53-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="10a53-174">maxValue</span></span> |<span data-ttu-id="10a53-175">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-175">No</span></span> |<span data-ttu-id="10a53-176">O valor máximo para parâmetros de tipo int, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="10a53-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="10a53-177">minLength</span><span class="sxs-lookup"><span data-stu-id="10a53-177">minLength</span></span> |<span data-ttu-id="10a53-178">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-178">No</span></span> |<span data-ttu-id="10a53-179">O comprimento mínimo para cadeia, secureString e parâmetros do tipo de matriz, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="10a53-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="10a53-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="10a53-180">maxLength</span></span> |<span data-ttu-id="10a53-181">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-181">No</span></span> |<span data-ttu-id="10a53-182">O comprimento máximo para cadeia, secureString e parâmetros do tipo de matriz, esse valor é inclusivo.</span><span class="sxs-lookup"><span data-stu-id="10a53-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="10a53-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="10a53-183">description</span></span> |<span data-ttu-id="10a53-184">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-184">No</span></span> |<span data-ttu-id="10a53-185">Descrição do parâmetro exibido aos usuários pelo portal.</span><span class="sxs-lookup"><span data-stu-id="10a53-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="10a53-186">Os valores e tipos permitidos são:</span><span class="sxs-lookup"><span data-stu-id="10a53-186">The allowed types and values are:</span></span>

* <span data-ttu-id="10a53-187">**string**</span><span class="sxs-lookup"><span data-stu-id="10a53-187">**string**</span></span>
* <span data-ttu-id="10a53-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="10a53-188">**secureString**</span></span>
* <span data-ttu-id="10a53-189">**int**</span><span class="sxs-lookup"><span data-stu-id="10a53-189">**int**</span></span>
* <span data-ttu-id="10a53-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="10a53-190">**bool**</span></span>
* <span data-ttu-id="10a53-191">**object**</span><span class="sxs-lookup"><span data-stu-id="10a53-191">**object**</span></span> 
* <span data-ttu-id="10a53-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="10a53-192">**secureObject**</span></span>
* <span data-ttu-id="10a53-193">**array**</span><span class="sxs-lookup"><span data-stu-id="10a53-193">**array**</span></span>

<span data-ttu-id="10a53-194">Para especificar um parâmetro como opcional, forneça um defaultValue (pode ser uma cadeia de caracteres vazia).</span><span class="sxs-lookup"><span data-stu-id="10a53-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="10a53-195">Se você especificar um nome de parâmetro em seu modelo que corresponda a um parâmetro no comando de implantação do modelo, haverá uma possível ambiguidade nos valores fornecidos.</span><span class="sxs-lookup"><span data-stu-id="10a53-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="10a53-196">O Resource Manager resolve essa confusão adicionando o sufixo **FromTemplate** ao parâmetro do modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="10a53-197">Por exemplo, se você incluir um parâmetro chamado **ResourceGroupName** em seu modelo, ele entrará em conflito com o parâmetro **ResourceGroupName** no cmdlet [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="10a53-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="10a53-198">Durante a implantação, você recebe uma solicitação para fornecer um valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="10a53-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="10a53-199">Em geral, você deve evitar essa confusão não dando aos parâmetros o mesmo nome dos parâmetros usados para operações de implantação.</span><span class="sxs-lookup"><span data-stu-id="10a53-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="10a53-200">Todas as senhas, chaves e outros segredos devem usar o tipo **secureString** .</span><span class="sxs-lookup"><span data-stu-id="10a53-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="10a53-201">Se você passar dados confidenciais em um objeto JSON, use o tipo **secureObject**.</span><span class="sxs-lookup"><span data-stu-id="10a53-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="10a53-202">Os parâmetros de modelo com o tipo secureString ou secureObject não podem ser lidos após a implantação de recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="10a53-203">Por exemplo, a seguinte entrada no histórico de implantação mostra o valor para uma cadeia de caracteres e objeto, mas não para secureString e secureObject.</span><span class="sxs-lookup"><span data-stu-id="10a53-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![mostrar valores de implantação](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="10a53-205">O seguinte exemplo mostra como definir parâmetros:</span><span class="sxs-lookup"><span data-stu-id="10a53-205">The following example shows how to define parameters:</span></span>

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

<span data-ttu-id="10a53-206">Para saber como inserir os valores do parâmetro durante a implantação, consulte [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="10a53-207">variáveis</span><span class="sxs-lookup"><span data-stu-id="10a53-207">Variables</span></span>
<span data-ttu-id="10a53-208">Na seção de variáveis, você constrói valores que podem ser usados em todo o seu modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="10a53-209">Você não precisa definir variáveis, mas normalmente elas simplificam seu modelo reduzindo expressões complexas.</span><span class="sxs-lookup"><span data-stu-id="10a53-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="10a53-210">Você define variáveis com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="10a53-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="10a53-211">O seguinte exemplo mostra como definir uma variável que é construída com base em dois valores de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="10a53-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="10a53-212">O próximo exemplo mostra uma variável que é um tipo JSON complexo e variáveis que são construídas com base em outras variáveis:</span><span class="sxs-lookup"><span data-stu-id="10a53-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="10a53-213">recursos</span><span class="sxs-lookup"><span data-stu-id="10a53-213">Resources</span></span>
<span data-ttu-id="10a53-214">Na seção de recursos, você define os recursos que são implantados ou atualizados.</span><span class="sxs-lookup"><span data-stu-id="10a53-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="10a53-215">Essa seção pode ficar mais complicada, porque você precisa entender os tipos que está implantando para fornecer os valores corretos.</span><span class="sxs-lookup"><span data-stu-id="10a53-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="10a53-216">Para obter os valores específicos de recurso (apiVersion, tipo e propriedades) que é preciso definir, confira [Define resources in Azure Resource Manager templates](/azure/templates/) (Definir recursos nos modelos do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="10a53-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="10a53-217">Você define recursos com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="10a53-217">You define resources with the following structure:</span></span>

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

| <span data-ttu-id="10a53-218">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="10a53-218">Element name</span></span> | <span data-ttu-id="10a53-219">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="10a53-219">Required</span></span> | <span data-ttu-id="10a53-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="10a53-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="10a53-221">condition</span><span class="sxs-lookup"><span data-stu-id="10a53-221">condition</span></span> | <span data-ttu-id="10a53-222">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-222">No</span></span> | <span data-ttu-id="10a53-223">Valor booliano que indica se o recurso está implantado.</span><span class="sxs-lookup"><span data-stu-id="10a53-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="10a53-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="10a53-224">apiVersion</span></span> |<span data-ttu-id="10a53-225">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-225">Yes</span></span> |<span data-ttu-id="10a53-226">Versão da API REST a ser usada para criar o recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="10a53-227">type</span><span class="sxs-lookup"><span data-stu-id="10a53-227">type</span></span> |<span data-ttu-id="10a53-228">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-228">Yes</span></span> |<span data-ttu-id="10a53-229">Tipo do recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-229">Type of the resource.</span></span> <span data-ttu-id="10a53-230">Esse valor é uma combinação do namespace do provedor de recursos e do tipo de recurso (como **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="10a53-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="10a53-231">name</span><span class="sxs-lookup"><span data-stu-id="10a53-231">name</span></span> |<span data-ttu-id="10a53-232">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-232">Yes</span></span> |<span data-ttu-id="10a53-233">Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-233">Name of the resource.</span></span> <span data-ttu-id="10a53-234">O nome deve seguir as restrições de componente URI definidas em RFC3986.</span><span class="sxs-lookup"><span data-stu-id="10a53-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="10a53-235">Além disso, os serviços do Azure que expõem o nome do recurso a terceiros validam o nome para garantir que ele não é uma tentativa de falsificar outra identidade.</span><span class="sxs-lookup"><span data-stu-id="10a53-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="10a53-236">location</span><span class="sxs-lookup"><span data-stu-id="10a53-236">location</span></span> |<span data-ttu-id="10a53-237">Varia</span><span class="sxs-lookup"><span data-stu-id="10a53-237">Varies</span></span> |<span data-ttu-id="10a53-238">Locais geográficos com suporte do recurso fornecido.</span><span class="sxs-lookup"><span data-stu-id="10a53-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="10a53-239">Você pode selecionar qualquer uma das localizações disponíveis, mas geralmente faz sentido escolher um que esteja perto de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="10a53-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="10a53-240">Normalmente, também faz sentido colocar recursos que interagem entre si na mesma região.</span><span class="sxs-lookup"><span data-stu-id="10a53-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="10a53-241">A maioria dos tipos de recursos exige um local, mas alguns deles (como uma atribuição de função) não.</span><span class="sxs-lookup"><span data-stu-id="10a53-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="10a53-242">Confira [Configure os locais dos recursos de modelos do Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="10a53-243">marcas</span><span class="sxs-lookup"><span data-stu-id="10a53-243">tags</span></span> |<span data-ttu-id="10a53-244">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-244">No</span></span> |<span data-ttu-id="10a53-245">Marcas que são associadas ao recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="10a53-246">Confira [Marque recursos em modelos do Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="10a53-247">comentários</span><span class="sxs-lookup"><span data-stu-id="10a53-247">comments</span></span> |<span data-ttu-id="10a53-248">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-248">No</span></span> |<span data-ttu-id="10a53-249">Suas anotações para documentar os recursos em seu modelo</span><span class="sxs-lookup"><span data-stu-id="10a53-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="10a53-250">cópia</span><span class="sxs-lookup"><span data-stu-id="10a53-250">copy</span></span> |<span data-ttu-id="10a53-251">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-251">No</span></span> |<span data-ttu-id="10a53-252">Se mais de uma instância for necessária, o número de recursos a serem criados.</span><span class="sxs-lookup"><span data-stu-id="10a53-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="10a53-253">O modo padrão é paralelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-253">The default mode is parallel.</span></span> <span data-ttu-id="10a53-254">Especifica o modo serial, quando você não deseja que sejam todos ou os recursos para implantação ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="10a53-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="10a53-255">Para obter mais informações, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="10a53-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="10a53-256">dependsOn</span></span> |<span data-ttu-id="10a53-257">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-257">No</span></span> |<span data-ttu-id="10a53-258">Recursos que devem ser implantados antes deste recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="10a53-259">O Gerenciador de Recursos avalia as dependências entre os recursos e os implanta na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="10a53-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="10a53-260">Quando os recursos não dependem uns dos outros, são implantados paralelamente.</span><span class="sxs-lookup"><span data-stu-id="10a53-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="10a53-261">O valor pode ser uma lista separada por vírgulas de nomes de recursos ou identificadores exclusivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="10a53-262">Somente lista recursos que são implantados neste modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="10a53-263">Recursos que não são definidos neste modelo já devem existir.</span><span class="sxs-lookup"><span data-stu-id="10a53-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="10a53-264">Evite adicionar dependências desnecessárias, pois elas podem reduzir sua implantação e criar dependências circulares.</span><span class="sxs-lookup"><span data-stu-id="10a53-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="10a53-265">Para obter orientação sobre como configurar as dependências, confira [Definir as dependências nos modelos do Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="10a53-266">propriedades</span><span class="sxs-lookup"><span data-stu-id="10a53-266">properties</span></span> |<span data-ttu-id="10a53-267">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-267">No</span></span> |<span data-ttu-id="10a53-268">Definições de configuração específicas do recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="10a53-269">Os valores para as propriedades são iguais aos valores que você fornece no corpo da solicitação para a operação da API REST (método PUT) para criar o recurso.</span><span class="sxs-lookup"><span data-stu-id="10a53-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="10a53-270">Você também pode especificar uma matriz de cópia para criar várias instâncias de uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="10a53-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="10a53-271">Para obter mais informações, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="10a53-272">recursos</span><span class="sxs-lookup"><span data-stu-id="10a53-272">resources</span></span> |<span data-ttu-id="10a53-273">Não</span><span class="sxs-lookup"><span data-stu-id="10a53-273">No</span></span> |<span data-ttu-id="10a53-274">Recursos filho que dependem do recurso que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="10a53-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="10a53-275">Forneça apenas os tipos de recurso permitidos pelo esquema do recurso pai.</span><span class="sxs-lookup"><span data-stu-id="10a53-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="10a53-276">O tipo totalmente qualificado do recurso filho inclui o tipo de recurso pai, como **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="10a53-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="10a53-277">A dependência do recurso pai não é implícita.</span><span class="sxs-lookup"><span data-stu-id="10a53-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="10a53-278">Você deve definir explicitamente essa dependência.</span><span class="sxs-lookup"><span data-stu-id="10a53-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="10a53-279">A seção de recursos contém uma matriz dos recursos a serem implantados.</span><span class="sxs-lookup"><span data-stu-id="10a53-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="10a53-280">Em cada recurso, você também pode definir uma matriz de recursos filhos.</span><span class="sxs-lookup"><span data-stu-id="10a53-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="10a53-281">Portanto, a seção de recursos pode ter uma estrutura como:</span><span class="sxs-lookup"><span data-stu-id="10a53-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="10a53-282">Para saber mais sobre como definir recursos filho, confira [Definir o nome e o tipo do recurso filho no modelo do Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="10a53-283">O elemento **condição** especifica se o recurso foi implantado.</span><span class="sxs-lookup"><span data-stu-id="10a53-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="10a53-284">O valor desse elemento é resolvido como verdadeiro ou falso.</span><span class="sxs-lookup"><span data-stu-id="10a53-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="10a53-285">Por exemplo, para especificar se uma nova conta de armazenamento é implantada, use:</span><span class="sxs-lookup"><span data-stu-id="10a53-285">For example, to specify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="10a53-286">Para obter um exemplo do uso de um recurso novo ou existente, consulte [Modelo de condição novo ou existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="10a53-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="10a53-287">Para especificar se uma máquina virtual foi implantada com uma senha ou chave SSH, definir duas versões da máquina virtual em seu modelo e usar **condição** para diferenciar o uso.</span><span class="sxs-lookup"><span data-stu-id="10a53-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="10a53-288">Passe um parâmetro que especifica qual cenário de implantação.</span><span class="sxs-lookup"><span data-stu-id="10a53-288">Pass a parameter that specifies which scenario to deploy.</span></span>

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

<span data-ttu-id="10a53-289">Para obter um exemplo do uso de uma senha ou chave SSH para implantar a máquina virtual, consulte [Modelo de condição de nome de usuário ou o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="10a53-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="10a53-290">Saídas</span><span class="sxs-lookup"><span data-stu-id="10a53-290">Outputs</span></span>
<span data-ttu-id="10a53-291">Na seção de saídas, você especifica valores que são retornados da implantação.</span><span class="sxs-lookup"><span data-stu-id="10a53-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="10a53-292">Por exemplo, é possível retornar o URI para acessar um recurso implantado.</span><span class="sxs-lookup"><span data-stu-id="10a53-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="10a53-293">O exemplo a seguir mostra a estrutura de uma definição de saída:</span><span class="sxs-lookup"><span data-stu-id="10a53-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="10a53-294">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="10a53-294">Element name</span></span> | <span data-ttu-id="10a53-295">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="10a53-295">Required</span></span> | <span data-ttu-id="10a53-296">Descrição</span><span class="sxs-lookup"><span data-stu-id="10a53-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="10a53-297">outputName</span><span class="sxs-lookup"><span data-stu-id="10a53-297">outputName</span></span> |<span data-ttu-id="10a53-298">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-298">Yes</span></span> |<span data-ttu-id="10a53-299">Nome do valor de saída.</span><span class="sxs-lookup"><span data-stu-id="10a53-299">Name of the output value.</span></span> <span data-ttu-id="10a53-300">Deve ser um identificador JavaScript válido.</span><span class="sxs-lookup"><span data-stu-id="10a53-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="10a53-301">type</span><span class="sxs-lookup"><span data-stu-id="10a53-301">type</span></span> |<span data-ttu-id="10a53-302">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-302">Yes</span></span> |<span data-ttu-id="10a53-303">Tipo do valor de saída.</span><span class="sxs-lookup"><span data-stu-id="10a53-303">Type of the output value.</span></span> <span data-ttu-id="10a53-304">Valores de saída oferecem suporte aos mesmos tipos que os parâmetros de entrada do modelo.</span><span class="sxs-lookup"><span data-stu-id="10a53-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="10a53-305">value</span><span class="sxs-lookup"><span data-stu-id="10a53-305">value</span></span> |<span data-ttu-id="10a53-306">Sim</span><span class="sxs-lookup"><span data-stu-id="10a53-306">Yes</span></span> |<span data-ttu-id="10a53-307">Expressão de linguagem do modelo avaliada e retornada como valor de saída.</span><span class="sxs-lookup"><span data-stu-id="10a53-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="10a53-308">O exemplo a seguir mostra um valor que é retornado na seção de saídas.</span><span class="sxs-lookup"><span data-stu-id="10a53-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="10a53-309">Para obter mais informações sobre como trabalhar com a saída, consulte [Compartilhando o estado nos modelos do Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="10a53-310">Limites de modelo</span><span class="sxs-lookup"><span data-stu-id="10a53-310">Template limits</span></span>

<span data-ttu-id="10a53-311">Limite o tamanho de seu modelo em 1 MB e cada arquivo de parâmetro em 64 KB.</span><span class="sxs-lookup"><span data-stu-id="10a53-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="10a53-312">O limite de 1 MB se aplica para o estado final do modelo depois que ele foi expandido com definições de recurso iterativo e valores para variáveis e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="10a53-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="10a53-313">Você também está limitado a:</span><span class="sxs-lookup"><span data-stu-id="10a53-313">You are also limited to:</span></span>

* <span data-ttu-id="10a53-314">256 parâmetros</span><span class="sxs-lookup"><span data-stu-id="10a53-314">256 parameters</span></span>
* <span data-ttu-id="10a53-315">256 variáveis</span><span class="sxs-lookup"><span data-stu-id="10a53-315">256 variables</span></span>
* <span data-ttu-id="10a53-316">800 recursos (incluindo a contagem de cópias)</span><span class="sxs-lookup"><span data-stu-id="10a53-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="10a53-317">64 valores de saída</span><span class="sxs-lookup"><span data-stu-id="10a53-317">64 output values</span></span>
* <span data-ttu-id="10a53-318">24.576 caracteres em uma expressão de modelo</span><span class="sxs-lookup"><span data-stu-id="10a53-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="10a53-319">Você pode exceder alguns limites de modelo usando um modelo aninhado.</span><span class="sxs-lookup"><span data-stu-id="10a53-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="10a53-320">Para saber mais, confira [Uso de modelos vinculados ao implantar recursos do Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="10a53-321">Para reduzir o número de parâmetros, variáveis ou saídas, você pode combinar vários valores em um objeto.</span><span class="sxs-lookup"><span data-stu-id="10a53-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="10a53-322">Para saber mais, veja [Objetos como parâmetros](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10a53-323">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10a53-323">Next steps</span></span>
* <span data-ttu-id="10a53-324">Para exibir modelos completos para muitos tipos diferentes de soluções, consulte os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="10a53-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="10a53-325">Para obter detalhes sobre as funções que podem ser usadas em um modelo, consulte [Funções do Modelo do Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="10a53-326">Para combinar vários modelos durante a implantação, consulte [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="10a53-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="10a53-327">Talvez seja necessário usar recursos que existam em um grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="10a53-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="10a53-328">Essa situação é comum ao trabalhar com contas de armazenamento ou redes virtuais compartilhadas com vários grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="10a53-329">Para obter mais informações, consulte a [função resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="10a53-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
