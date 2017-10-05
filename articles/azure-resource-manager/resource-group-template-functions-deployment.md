---
title: "Funções de modelo do Azure Resource Manager – implantação | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Resource Manager para recuperar informações sobre implantação."
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
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="fc0fc-103">Funções de implantação para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc0fc-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="fc0fc-104">O Gerenciador de Recursos fornece as seguintes funções para obter os valores de seções do modelo e os valores relacionados à implantação:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="fc0fc-105">implantação</span><span class="sxs-lookup"><span data-stu-id="fc0fc-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="fc0fc-106">parâmetros</span><span class="sxs-lookup"><span data-stu-id="fc0fc-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="fc0fc-107">variáveis</span><span class="sxs-lookup"><span data-stu-id="fc0fc-107">variables</span></span>](#variables)

<span data-ttu-id="fc0fc-108">Para obter valores de recursos, de grupos de recursos ou de assinaturas, veja [Funções de recurso](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="fc0fc-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="fc0fc-109">implantação</span><span class="sxs-lookup"><span data-stu-id="fc0fc-109">deployment</span></span>
`deployment()`

<span data-ttu-id="fc0fc-110">Retorna informações sobre a operação de implantação atual.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="fc0fc-111">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="fc0fc-111">Return value</span></span>

<span data-ttu-id="fc0fc-112">Essa função retorna o objeto que é passado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="fc0fc-113">As propriedades no objeto retornado vão variar dependendo se o objeto de implantação for transmitido como um link ou como um objeto na linha.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="fc0fc-114">Quando o objeto de implantação é passado na linha, como ao usar o parâmetro **-TemplateFile** no Azure PowerShell para apontar para um arquivo local, o objeto retornado tem no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="fc0fc-115">Quando o objeto é transmitido como um link, como ao usar o parâmetro **- TemplateUri** para apontar para um objeto remoto, o objeto é retornado no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="fc0fc-116">Comentários</span><span class="sxs-lookup"><span data-stu-id="fc0fc-116">Remarks</span></span>

<span data-ttu-id="fc0fc-117">Você pode usar a implantação() para vincular a outro modelo com base no URI do modelo pai.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="fc0fc-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-118">Example</span></span>

<span data-ttu-id="fc0fc-119">O exemplo a seguir retorna o objeto de implantação:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-119">The following example returns the deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="fc0fc-120">O exemplo anterior retorna o seguinte objeto:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-120">The preceding example returns the following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="fc0fc-121">parameters</span><span class="sxs-lookup"><span data-stu-id="fc0fc-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="fc0fc-122">Retorna um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-122">Returns a parameter value.</span></span> <span data-ttu-id="fc0fc-123">O nome do parâmetro especificado deve ser definido na seção de parâmetros do modelo.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="fc0fc-124">parâmetros</span><span class="sxs-lookup"><span data-stu-id="fc0fc-124">Parameters</span></span>

| <span data-ttu-id="fc0fc-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="fc0fc-125">Parameter</span></span> | <span data-ttu-id="fc0fc-126">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fc0fc-126">Required</span></span> | <span data-ttu-id="fc0fc-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-127">Type</span></span> | <span data-ttu-id="fc0fc-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc0fc-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fc0fc-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="fc0fc-129">parameterName</span></span> |<span data-ttu-id="fc0fc-130">Sim</span><span class="sxs-lookup"><span data-stu-id="fc0fc-130">Yes</span></span> |<span data-ttu-id="fc0fc-131">string</span><span class="sxs-lookup"><span data-stu-id="fc0fc-131">string</span></span> |<span data-ttu-id="fc0fc-132">O nome do parâmetro a retornar.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fc0fc-133">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="fc0fc-133">Return value</span></span>

<span data-ttu-id="fc0fc-134">O valor do parâmetro especificado.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="fc0fc-135">Comentários</span><span class="sxs-lookup"><span data-stu-id="fc0fc-135">Remarks</span></span>

<span data-ttu-id="fc0fc-136">Normalmente, você usa parâmetros para definir valores de recursos.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="fc0fc-137">O exemplo a seguir define o nome do site para o valor do parâmetro passado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="fc0fc-138">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-138">Example</span></span>

<span data-ttu-id="fc0fc-139">O exemplo a seguir mostra um uso simplificado da função parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-139">The following example shows a simplified use of the parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="fc0fc-140">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fc0fc-141">Nome</span><span class="sxs-lookup"><span data-stu-id="fc0fc-141">Name</span></span> | <span data-ttu-id="fc0fc-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-142">Type</span></span> | <span data-ttu-id="fc0fc-143">Valor</span><span class="sxs-lookup"><span data-stu-id="fc0fc-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fc0fc-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fc0fc-144">stringOutput</span></span> | <span data-ttu-id="fc0fc-145">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fc0fc-145">String</span></span> | <span data-ttu-id="fc0fc-146">opção 1</span><span class="sxs-lookup"><span data-stu-id="fc0fc-146">option 1</span></span> |
| <span data-ttu-id="fc0fc-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="fc0fc-147">intOutput</span></span> | <span data-ttu-id="fc0fc-148">int</span><span class="sxs-lookup"><span data-stu-id="fc0fc-148">Int</span></span> | <span data-ttu-id="fc0fc-149">1</span><span class="sxs-lookup"><span data-stu-id="fc0fc-149">1</span></span> |
| <span data-ttu-id="fc0fc-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="fc0fc-150">objectOutput</span></span> | <span data-ttu-id="fc0fc-151">Objeto</span><span class="sxs-lookup"><span data-stu-id="fc0fc-151">Object</span></span> | <span data-ttu-id="fc0fc-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="fc0fc-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="fc0fc-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fc0fc-153">arrayOutput</span></span> | <span data-ttu-id="fc0fc-154">Matriz</span><span class="sxs-lookup"><span data-stu-id="fc0fc-154">Array</span></span> | <span data-ttu-id="fc0fc-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="fc0fc-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="fc0fc-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="fc0fc-156">crossOutput</span></span> | <span data-ttu-id="fc0fc-157">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fc0fc-157">String</span></span> | <span data-ttu-id="fc0fc-158">opção 1</span><span class="sxs-lookup"><span data-stu-id="fc0fc-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="fc0fc-159">variáveis</span><span class="sxs-lookup"><span data-stu-id="fc0fc-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="fc0fc-160">Retorna o valor da variável.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-160">Returns the value of variable.</span></span> <span data-ttu-id="fc0fc-161">O nome do parâmetro especificado deve ser definido na seção variáveis do modelo.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="fc0fc-162">parâmetros</span><span class="sxs-lookup"><span data-stu-id="fc0fc-162">Parameters</span></span>

| <span data-ttu-id="fc0fc-163">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="fc0fc-163">Parameter</span></span> | <span data-ttu-id="fc0fc-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fc0fc-164">Required</span></span> | <span data-ttu-id="fc0fc-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-165">Type</span></span> | <span data-ttu-id="fc0fc-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc0fc-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fc0fc-167">variableName</span><span class="sxs-lookup"><span data-stu-id="fc0fc-167">variableName</span></span> |<span data-ttu-id="fc0fc-168">Sim</span><span class="sxs-lookup"><span data-stu-id="fc0fc-168">Yes</span></span> |<span data-ttu-id="fc0fc-169">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fc0fc-169">String</span></span> |<span data-ttu-id="fc0fc-170">O nome da variável a retornar.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fc0fc-171">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="fc0fc-171">Return value</span></span>

<span data-ttu-id="fc0fc-172">O valor da variável especificada.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="fc0fc-173">Comentários</span><span class="sxs-lookup"><span data-stu-id="fc0fc-173">Remarks</span></span>

<span data-ttu-id="fc0fc-174">Normalmente, você usa variáveis para simplificar seu modelo criando valores complexos apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="fc0fc-175">O exemplo a seguir constrói um nome exclusivo para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-175">The following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="fc0fc-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-176">Example</span></span>

<span data-ttu-id="fc0fc-177">O modelo de exemplo retorna valores de variáveis diferentes.</span><span class="sxs-lookup"><span data-stu-id="fc0fc-177">The example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="fc0fc-178">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="fc0fc-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fc0fc-179">Nome</span><span class="sxs-lookup"><span data-stu-id="fc0fc-179">Name</span></span> | <span data-ttu-id="fc0fc-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="fc0fc-180">Type</span></span> | <span data-ttu-id="fc0fc-181">Valor</span><span class="sxs-lookup"><span data-stu-id="fc0fc-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fc0fc-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="fc0fc-182">exampleOutput1</span></span> | <span data-ttu-id="fc0fc-183">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fc0fc-183">String</span></span> | <span data-ttu-id="fc0fc-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="fc0fc-184">myVariable</span></span> |
| <span data-ttu-id="fc0fc-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="fc0fc-185">exampleOutput2</span></span> | <span data-ttu-id="fc0fc-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="fc0fc-186">Array</span></span> | <span data-ttu-id="fc0fc-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="fc0fc-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="fc0fc-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="fc0fc-188">exampleOutput3</span></span> | <span data-ttu-id="fc0fc-189">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fc0fc-189">String</span></span> | <span data-ttu-id="fc0fc-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="fc0fc-190">myVariable</span></span> |
| <span data-ttu-id="fc0fc-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="fc0fc-191">exampleOutput4</span></span> |  <span data-ttu-id="fc0fc-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="fc0fc-192">Object</span></span> | <span data-ttu-id="fc0fc-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="fc0fc-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc0fc-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc0fc-194">Next steps</span></span>
* <span data-ttu-id="fc0fc-195">Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fc0fc-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fc0fc-196">Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fc0fc-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="fc0fc-197">Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fc0fc-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="fc0fc-198">Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fc0fc-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

