---
title: "funções de modelo do Gerenciador de recursos aaaAzure - implantação | Microsoft Docs"
description: "Descreve Olá funções toouse um informações de implantação do Azure Resource Manager modelo tooretrieve."
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="da5fe-103">Funções de implantação para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="da5fe-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="da5fe-104">Gerenciador de recursos fornece a seguinte Olá funções para obter valores de seções do modelo de saudação e valores relacionados toohello implantação:</span><span class="sxs-lookup"><span data-stu-id="da5fe-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="da5fe-105">implantação</span><span class="sxs-lookup"><span data-stu-id="da5fe-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="da5fe-106">parâmetros</span><span class="sxs-lookup"><span data-stu-id="da5fe-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="da5fe-107">variáveis</span><span class="sxs-lookup"><span data-stu-id="da5fe-107">variables</span></span>](#variables)

<span data-ttu-id="da5fe-108">tooget valores de recursos, grupos de recursos ou assinaturas, consulte [funções de recurso](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="da5fe-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="da5fe-109">implantação</span><span class="sxs-lookup"><span data-stu-id="da5fe-109">deployment</span></span>
`deployment()`

<span data-ttu-id="da5fe-110">Retorna informações sobre a operação de implantação atual hello.</span><span class="sxs-lookup"><span data-stu-id="da5fe-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="da5fe-111">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="da5fe-111">Return value</span></span>

<span data-ttu-id="da5fe-112">Esta função retorna o objeto Olá passado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="da5fe-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="da5fe-113">propriedades Olá Olá retornada objeto diferem com base em se hello implantação objeto é passado como um link ou como um objeto na linha.</span><span class="sxs-lookup"><span data-stu-id="da5fe-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="da5fe-114">Quando o objeto de implantação de saudação é passado na linha, como ao usar Olá **- TemplateFile** parâmetro no Azure PowerShell toopoint tooa arquivo local, Olá retornou objeto tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="da5fe-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

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

<span data-ttu-id="da5fe-115">Quando o objeto de saudação é passado como um link, como quando usando Olá **- TemplateUri** parâmetro toopoint tooa remoto do objeto, Olá objeto é retornado no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="da5fe-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="da5fe-116">Comentários</span><span class="sxs-lookup"><span data-stu-id="da5fe-116">Remarks</span></span>

<span data-ttu-id="da5fe-117">Você pode usar deployment() toolink tooanother modelo com base em Olá URI do modelo-Olá pai.</span><span class="sxs-lookup"><span data-stu-id="da5fe-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="da5fe-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="da5fe-118">Example</span></span>

<span data-ttu-id="da5fe-119">Olá, exemplo a seguir retorna o objeto de implantação hello:</span><span class="sxs-lookup"><span data-stu-id="da5fe-119">hello following example returns hello deployment object:</span></span>

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

<span data-ttu-id="da5fe-120">Olá, exemplo anterior retorna Olá objeto a seguir:</span><span class="sxs-lookup"><span data-stu-id="da5fe-120">hello preceding example returns hello following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="da5fe-121">parâmetros</span><span class="sxs-lookup"><span data-stu-id="da5fe-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="da5fe-122">Retorna um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="da5fe-122">Returns a parameter value.</span></span> <span data-ttu-id="da5fe-123">nome do parâmetro especificado Olá deve ser definido na seção de parâmetros de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="da5fe-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="da5fe-124">parâmetros</span><span class="sxs-lookup"><span data-stu-id="da5fe-124">Parameters</span></span>

| <span data-ttu-id="da5fe-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="da5fe-125">Parameter</span></span> | <span data-ttu-id="da5fe-126">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="da5fe-126">Required</span></span> | <span data-ttu-id="da5fe-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="da5fe-127">Type</span></span> | <span data-ttu-id="da5fe-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="da5fe-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="da5fe-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="da5fe-129">parameterName</span></span> |<span data-ttu-id="da5fe-130">Sim</span><span class="sxs-lookup"><span data-stu-id="da5fe-130">Yes</span></span> |<span data-ttu-id="da5fe-131">string</span><span class="sxs-lookup"><span data-stu-id="da5fe-131">string</span></span> |<span data-ttu-id="da5fe-132">nome de saudação do hello tooreturn de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="da5fe-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="da5fe-133">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="da5fe-133">Return value</span></span>

<span data-ttu-id="da5fe-134">valor Olá Olá especificado o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="da5fe-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="da5fe-135">Comentários</span><span class="sxs-lookup"><span data-stu-id="da5fe-135">Remarks</span></span>

<span data-ttu-id="da5fe-136">Normalmente, você pode usar valores de parâmetros de recursos tooset.</span><span class="sxs-lookup"><span data-stu-id="da5fe-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="da5fe-137">Olá exemplo a seguir define nome de saudação do valor de parâmetro do site da web toohello passado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="da5fe-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="da5fe-138">Exemplo</span><span class="sxs-lookup"><span data-stu-id="da5fe-138">Example</span></span>

<span data-ttu-id="da5fe-139">Olá, exemplo a seguir mostra um uso simplificado da função de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="da5fe-139">hello following example shows a simplified use of hello parameters function.</span></span>

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

<span data-ttu-id="da5fe-140">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="da5fe-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="da5fe-141">Nome</span><span class="sxs-lookup"><span data-stu-id="da5fe-141">Name</span></span> | <span data-ttu-id="da5fe-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="da5fe-142">Type</span></span> | <span data-ttu-id="da5fe-143">Valor</span><span class="sxs-lookup"><span data-stu-id="da5fe-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="da5fe-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="da5fe-144">stringOutput</span></span> | <span data-ttu-id="da5fe-145">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="da5fe-145">String</span></span> | <span data-ttu-id="da5fe-146">opção 1</span><span class="sxs-lookup"><span data-stu-id="da5fe-146">option 1</span></span> |
| <span data-ttu-id="da5fe-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="da5fe-147">intOutput</span></span> | <span data-ttu-id="da5fe-148">int</span><span class="sxs-lookup"><span data-stu-id="da5fe-148">Int</span></span> | <span data-ttu-id="da5fe-149">1</span><span class="sxs-lookup"><span data-stu-id="da5fe-149">1</span></span> |
| <span data-ttu-id="da5fe-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="da5fe-150">objectOutput</span></span> | <span data-ttu-id="da5fe-151">Objeto</span><span class="sxs-lookup"><span data-stu-id="da5fe-151">Object</span></span> | <span data-ttu-id="da5fe-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="da5fe-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="da5fe-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="da5fe-153">arrayOutput</span></span> | <span data-ttu-id="da5fe-154">Matriz</span><span class="sxs-lookup"><span data-stu-id="da5fe-154">Array</span></span> | <span data-ttu-id="da5fe-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="da5fe-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="da5fe-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="da5fe-156">crossOutput</span></span> | <span data-ttu-id="da5fe-157">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="da5fe-157">String</span></span> | <span data-ttu-id="da5fe-158">opção 1</span><span class="sxs-lookup"><span data-stu-id="da5fe-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="da5fe-159">variáveis</span><span class="sxs-lookup"><span data-stu-id="da5fe-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="da5fe-160">Retorna Olá valor da variável.</span><span class="sxs-lookup"><span data-stu-id="da5fe-160">Returns hello value of variable.</span></span> <span data-ttu-id="da5fe-161">Olá nome de variável especificado deve ser definido na seção de variáveis de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="da5fe-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="da5fe-162">parâmetros</span><span class="sxs-lookup"><span data-stu-id="da5fe-162">Parameters</span></span>

| <span data-ttu-id="da5fe-163">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="da5fe-163">Parameter</span></span> | <span data-ttu-id="da5fe-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="da5fe-164">Required</span></span> | <span data-ttu-id="da5fe-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="da5fe-165">Type</span></span> | <span data-ttu-id="da5fe-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="da5fe-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="da5fe-167">variableName</span><span class="sxs-lookup"><span data-stu-id="da5fe-167">variableName</span></span> |<span data-ttu-id="da5fe-168">Sim</span><span class="sxs-lookup"><span data-stu-id="da5fe-168">Yes</span></span> |<span data-ttu-id="da5fe-169">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="da5fe-169">String</span></span> |<span data-ttu-id="da5fe-170">nome de saudação do tooreturn variável hello.</span><span class="sxs-lookup"><span data-stu-id="da5fe-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="da5fe-171">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="da5fe-171">Return value</span></span>

<span data-ttu-id="da5fe-172">valor Olá Olá especificado variável.</span><span class="sxs-lookup"><span data-stu-id="da5fe-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="da5fe-173">Comentários</span><span class="sxs-lookup"><span data-stu-id="da5fe-173">Remarks</span></span>

<span data-ttu-id="da5fe-174">Normalmente, você usa variáveis toosimplify seu modelo Criando valores complexos, apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="da5fe-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="da5fe-175">Olá, exemplo a seguir constrói um nome exclusivo para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="da5fe-175">hello following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="da5fe-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="da5fe-176">Example</span></span>

<span data-ttu-id="da5fe-177">modelo de exemplo Hello retorna valores de variável diferentes.</span><span class="sxs-lookup"><span data-stu-id="da5fe-177">hello example template returns different variable values.</span></span>

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

<span data-ttu-id="da5fe-178">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="da5fe-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="da5fe-179">Nome</span><span class="sxs-lookup"><span data-stu-id="da5fe-179">Name</span></span> | <span data-ttu-id="da5fe-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="da5fe-180">Type</span></span> | <span data-ttu-id="da5fe-181">Valor</span><span class="sxs-lookup"><span data-stu-id="da5fe-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="da5fe-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="da5fe-182">exampleOutput1</span></span> | <span data-ttu-id="da5fe-183">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="da5fe-183">String</span></span> | <span data-ttu-id="da5fe-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="da5fe-184">myVariable</span></span> |
| <span data-ttu-id="da5fe-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="da5fe-185">exampleOutput2</span></span> | <span data-ttu-id="da5fe-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="da5fe-186">Array</span></span> | <span data-ttu-id="da5fe-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="da5fe-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="da5fe-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="da5fe-188">exampleOutput3</span></span> | <span data-ttu-id="da5fe-189">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="da5fe-189">String</span></span> | <span data-ttu-id="da5fe-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="da5fe-190">myVariable</span></span> |
| <span data-ttu-id="da5fe-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="da5fe-191">exampleOutput4</span></span> |  <span data-ttu-id="da5fe-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="da5fe-192">Object</span></span> | <span data-ttu-id="da5fe-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="da5fe-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="da5fe-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da5fe-194">Next steps</span></span>
* <span data-ttu-id="da5fe-195">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="da5fe-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="da5fe-196">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="da5fe-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="da5fe-197">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="da5fe-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="da5fe-198">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="da5fe-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

