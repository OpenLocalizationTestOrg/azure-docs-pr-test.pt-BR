---
title: "Funções de modelo do Azure Resource Manager – recursos | Microsoft Docs"
description: "Descreve as funções a serem usadas em um modelo do Azure Resource Manager para recuperar valores sobre recursos."
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
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="9e536-103">Funções de recursos para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e536-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="9e536-104">O Gerenciador de Recursos fornece as seguintes funções para obter valores de recurso:</span><span class="sxs-lookup"><span data-stu-id="9e536-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="9e536-105">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="9e536-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="9e536-106">providers</span><span class="sxs-lookup"><span data-stu-id="9e536-106">providers</span></span>](#providers)
* [<span data-ttu-id="9e536-107">reference</span><span class="sxs-lookup"><span data-stu-id="9e536-107">reference</span></span>](#reference)
* [<span data-ttu-id="9e536-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e536-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="9e536-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="9e536-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="9e536-110">subscription</span><span class="sxs-lookup"><span data-stu-id="9e536-110">subscription</span></span>](#subscription)

<span data-ttu-id="9e536-111">Para obter valores de parâmetros, de variáveis ou da implantação atual, veja [Funções de valor de implantação](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="9e536-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="9e536-112">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="9e536-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="9e536-113">Retorna os valores para qualquer tipo de recurso que ofereça suporte à operação de lista.</span><span class="sxs-lookup"><span data-stu-id="9e536-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="9e536-114">O uso mais comum é `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="9e536-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="9e536-115">parâmetros</span><span class="sxs-lookup"><span data-stu-id="9e536-115">Parameters</span></span>

| <span data-ttu-id="9e536-116">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="9e536-116">Parameter</span></span> | <span data-ttu-id="9e536-117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9e536-117">Required</span></span> | <span data-ttu-id="9e536-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e536-118">Type</span></span> | <span data-ttu-id="9e536-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="9e536-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9e536-120">resourceName ou resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="9e536-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="9e536-121">Sim</span><span class="sxs-lookup"><span data-stu-id="9e536-121">Yes</span></span> |<span data-ttu-id="9e536-122">string</span><span class="sxs-lookup"><span data-stu-id="9e536-122">string</span></span> |<span data-ttu-id="9e536-123">Identificador exclusivo para o recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="9e536-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9e536-124">apiVersion</span></span> |<span data-ttu-id="9e536-125">Sim</span><span class="sxs-lookup"><span data-stu-id="9e536-125">Yes</span></span> |<span data-ttu-id="9e536-126">string</span><span class="sxs-lookup"><span data-stu-id="9e536-126">string</span></span> |<span data-ttu-id="9e536-127">Versão de API do estado de tempo de execução do recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-127">API version of resource runtime state.</span></span> <span data-ttu-id="9e536-128">Normalmente, no formato **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="9e536-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9e536-129">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="9e536-129">Return value</span></span>

<span data-ttu-id="9e536-130">O objeto retornado de listKeys tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-130">The returned object from listKeys has the following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="9e536-131">Outras funções de lista têm formatos diferentes de retorno.</span><span class="sxs-lookup"><span data-stu-id="9e536-131">Other list functions have different return formats.</span></span> <span data-ttu-id="9e536-132">Para ver o formato de uma função, inclua-a na seção de saídas, conforme mostra o exemplo de modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="9e536-133">Comentários</span><span class="sxs-lookup"><span data-stu-id="9e536-133">Remarks</span></span>

<span data-ttu-id="9e536-134">Qualquer operação que começa com **list** pode ser usada como uma função no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="9e536-135">As operações disponíveis não incluem apenas listKeys, mas também operações como `list`, `listAdminKeys` e `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="9e536-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="9e536-136">No entanto, você não pode usar **lista** as operações que exigem valores no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9e536-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="9e536-137">Por exemplo, o [lista conta SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operação requer parâmetros de corpo de solicitação como *signedExpiry*, portanto, você não pode usá-lo em um modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="9e536-138">Para determinar quais tipos de recursos têm uma operação de lista, use as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="9e536-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="9e536-139">Veja as [operações da API REST](/rest/api/) de um provedor de recursos e procure por operações de lista.</span><span class="sxs-lookup"><span data-stu-id="9e536-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="9e536-140">Por exemplo, as contas de armazenamento têm a [operação listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="9e536-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="9e536-141">Use o cmdlet do PowerShell [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation).</span><span class="sxs-lookup"><span data-stu-id="9e536-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="9e536-142">O exemplo a seguir obtém todas as operações de lista de contas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="9e536-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="9e536-143">Use o seguinte comando da CLI do Azure para filtrar apenas as operações de lista:</span><span class="sxs-lookup"><span data-stu-id="9e536-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="9e536-144">Especifique o recurso usando a [função resourceId](#resourceid) ou o formato `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="9e536-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="9e536-145">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9e536-145">Example</span></span>

<span data-ttu-id="9e536-146">O exemplo a seguir mostra como retornar as chaves primárias e secundárias de uma conta de armazenamento na seção de saídas.</span><span class="sxs-lookup"><span data-stu-id="9e536-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="9e536-147">providers</span><span class="sxs-lookup"><span data-stu-id="9e536-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="9e536-148">Retorna informações sobre um provedor de recursos e seus tipos de recursos com suporte.</span><span class="sxs-lookup"><span data-stu-id="9e536-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="9e536-149">Se você não fornecer um tipo de recurso, a função retornará todos os tipos com suporte para o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e536-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="9e536-150">parâmetros</span><span class="sxs-lookup"><span data-stu-id="9e536-150">Parameters</span></span>

| <span data-ttu-id="9e536-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="9e536-151">Parameter</span></span> | <span data-ttu-id="9e536-152">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9e536-152">Required</span></span> | <span data-ttu-id="9e536-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e536-153">Type</span></span> | <span data-ttu-id="9e536-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="9e536-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9e536-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="9e536-155">providerNamespace</span></span> |<span data-ttu-id="9e536-156">Sim</span><span class="sxs-lookup"><span data-stu-id="9e536-156">Yes</span></span> |<span data-ttu-id="9e536-157">string</span><span class="sxs-lookup"><span data-stu-id="9e536-157">string</span></span> |<span data-ttu-id="9e536-158">Namespace do provedor</span><span class="sxs-lookup"><span data-stu-id="9e536-158">Namespace of the provider</span></span> |
| <span data-ttu-id="9e536-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="9e536-159">resourceType</span></span> |<span data-ttu-id="9e536-160">Não</span><span class="sxs-lookup"><span data-stu-id="9e536-160">No</span></span> |<span data-ttu-id="9e536-161">string</span><span class="sxs-lookup"><span data-stu-id="9e536-161">string</span></span> |<span data-ttu-id="9e536-162">O tipo de recurso no namespace especificado.</span><span class="sxs-lookup"><span data-stu-id="9e536-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9e536-163">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="9e536-163">Return value</span></span>

<span data-ttu-id="9e536-164">Cada tipo com suporte é retornado no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="9e536-165">A ordenação de matriz dos valores retornados não é garantida.</span><span class="sxs-lookup"><span data-stu-id="9e536-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="9e536-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9e536-166">Example</span></span>

<span data-ttu-id="9e536-167">O exemplo a seguir mostra como usar a função provider:</span><span class="sxs-lookup"><span data-stu-id="9e536-167">The following example shows how to use the provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="9e536-168">O exemplo anterior retorna um objeto no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-168">The preceding example returns an object in the following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="9e536-169">reference</span><span class="sxs-lookup"><span data-stu-id="9e536-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="9e536-170">Retorna um objeto que representa o estado de tempo de execução de um recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="9e536-171">parâmetros</span><span class="sxs-lookup"><span data-stu-id="9e536-171">Parameters</span></span>

| <span data-ttu-id="9e536-172">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="9e536-172">Parameter</span></span> | <span data-ttu-id="9e536-173">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9e536-173">Required</span></span> | <span data-ttu-id="9e536-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e536-174">Type</span></span> | <span data-ttu-id="9e536-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="9e536-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9e536-176">resourceName ou resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="9e536-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="9e536-177">Sim</span><span class="sxs-lookup"><span data-stu-id="9e536-177">Yes</span></span> |<span data-ttu-id="9e536-178">string</span><span class="sxs-lookup"><span data-stu-id="9e536-178">string</span></span> |<span data-ttu-id="9e536-179">Nome ou identificador exclusivo de um recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="9e536-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9e536-180">apiVersion</span></span> |<span data-ttu-id="9e536-181">Não</span><span class="sxs-lookup"><span data-stu-id="9e536-181">No</span></span> |<span data-ttu-id="9e536-182">string</span><span class="sxs-lookup"><span data-stu-id="9e536-182">string</span></span> |<span data-ttu-id="9e536-183">Versão da API do recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="9e536-183">API version of the specified resource.</span></span> <span data-ttu-id="9e536-184">Inclua esse parâmetro quando o recurso não estiver provisionado no mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="9e536-185">Normalmente, no formato **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="9e536-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9e536-186">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="9e536-186">Return value</span></span>

<span data-ttu-id="9e536-187">Cada tipo de recurso retorna propriedades diferentes para a função de referência.</span><span class="sxs-lookup"><span data-stu-id="9e536-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="9e536-188">A função não retorna um único formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="9e536-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="9e536-189">Para ver as propriedades de um tipo de recurso, retorne o objeto na seção de saída, conforme mostra o exemplo.</span><span class="sxs-lookup"><span data-stu-id="9e536-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="9e536-190">Comentários</span><span class="sxs-lookup"><span data-stu-id="9e536-190">Remarks</span></span>

<span data-ttu-id="9e536-191">A função de referência deriva seu valor de um estado de tempo de execução e, portanto, não pode ser usada na seção de variáveis.</span><span class="sxs-lookup"><span data-stu-id="9e536-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="9e536-192">Ela pode ser usada na seção de saídas de um modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="9e536-193">Usando a função de referência, você declara implicitamente que um recurso depende de outro recurso se o recurso referenciado é provisionado no mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="9e536-194">Você não precisa usar a propriedade dependsOn também.</span><span class="sxs-lookup"><span data-stu-id="9e536-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="9e536-195">A função não é avaliada até que o recurso referenciado conclua a implantação.</span><span class="sxs-lookup"><span data-stu-id="9e536-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="9e536-196">Para ver os valores e nomes de propriedade para um tipo de recurso, crie um modelo que retorne o objeto na seção de saídas .</span><span class="sxs-lookup"><span data-stu-id="9e536-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="9e536-197">Se você tiver um recurso existente desse tipo, o modelo retornará o objeto sem implantar qualquer recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="9e536-198">Normalmente, você usa a função **reference** para retornar um valor específico de um objeto, como o URI do ponto de extremidade de blob ou o nome de domínio totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="9e536-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="9e536-199">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9e536-199">Example</span></span>

<span data-ttu-id="9e536-200">Para implantar e fazer referência ao recurso no mesmo modelo, use:</span><span class="sxs-lookup"><span data-stu-id="9e536-200">To deploy and reference the resource in the same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="9e536-201">O exemplo anterior retorna um objeto no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-201">The preceding example returns an object in the following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="9e536-202">O exemplo a seguir faz referência a uma conta de armazenamento implantada nesse modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="9e536-203">A conta de armazenamento já existe dentro do mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e536-203">The storage account already exists within the same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="9e536-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e536-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="9e536-205">Retorna um objeto que representa o grupo de recursos atual.</span><span class="sxs-lookup"><span data-stu-id="9e536-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="9e536-206">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="9e536-206">Return value</span></span>

<span data-ttu-id="9e536-207">O objeto retornado está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-207">The returned object is in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="9e536-208">Comentários</span><span class="sxs-lookup"><span data-stu-id="9e536-208">Remarks</span></span>

<span data-ttu-id="9e536-209">Um uso comum da função resourceGroup é criar recursos no mesmo local que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e536-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="9e536-210">O exemplo a seguir usa o local do grupo de recursos para atribuir o local de um site Web.</span><span class="sxs-lookup"><span data-stu-id="9e536-210">The following example uses the resource group location to assign the location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="9e536-211">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9e536-211">Example</span></span>

<span data-ttu-id="9e536-212">O modelo a seguir retorna as propriedades do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e536-212">The following template returns the properties of the resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="9e536-213">O exemplo anterior retorna um objeto no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-213">The preceding example returns an object in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="9e536-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="9e536-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="9e536-215">Retorna o identificador exclusivo de um recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="9e536-216">Você pode usar essa função quando o nome do recurso é ambíguo ou não provisionado no mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="9e536-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="9e536-217">parâmetros</span><span class="sxs-lookup"><span data-stu-id="9e536-217">Parameters</span></span>

| <span data-ttu-id="9e536-218">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="9e536-218">Parameter</span></span> | <span data-ttu-id="9e536-219">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9e536-219">Required</span></span> | <span data-ttu-id="9e536-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e536-220">Type</span></span> | <span data-ttu-id="9e536-221">Descrição</span><span class="sxs-lookup"><span data-stu-id="9e536-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9e536-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="9e536-222">subscriptionId</span></span> |<span data-ttu-id="9e536-223">Não</span><span class="sxs-lookup"><span data-stu-id="9e536-223">No</span></span> |<span data-ttu-id="9e536-224">string (no formato GUID)</span><span class="sxs-lookup"><span data-stu-id="9e536-224">string (In GUID format)</span></span> |<span data-ttu-id="9e536-225">O valor padrão é a assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="9e536-225">Default value is the current subscription.</span></span> <span data-ttu-id="9e536-226">Especifique esse valor quando você precisar recuperar um recurso em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="9e536-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="9e536-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="9e536-227">resourceGroupName</span></span> |<span data-ttu-id="9e536-228">Não</span><span class="sxs-lookup"><span data-stu-id="9e536-228">No</span></span> |<span data-ttu-id="9e536-229">string</span><span class="sxs-lookup"><span data-stu-id="9e536-229">string</span></span> |<span data-ttu-id="9e536-230">O valor padrão é o grupo de recursos atual.</span><span class="sxs-lookup"><span data-stu-id="9e536-230">Default value is current resource group.</span></span> <span data-ttu-id="9e536-231">Especifique esse valor quando você precisar recuperar um recurso em outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e536-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="9e536-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="9e536-232">resourceType</span></span> |<span data-ttu-id="9e536-233">Sim</span><span class="sxs-lookup"><span data-stu-id="9e536-233">Yes</span></span> |<span data-ttu-id="9e536-234">string</span><span class="sxs-lookup"><span data-stu-id="9e536-234">string</span></span> |<span data-ttu-id="9e536-235">Tipo de recurso, incluindo o namespace do provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e536-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="9e536-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="9e536-236">resourceName1</span></span> |<span data-ttu-id="9e536-237">Sim</span><span class="sxs-lookup"><span data-stu-id="9e536-237">Yes</span></span> |<span data-ttu-id="9e536-238">string</span><span class="sxs-lookup"><span data-stu-id="9e536-238">string</span></span> |<span data-ttu-id="9e536-239">Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="9e536-239">Name of resource.</span></span> |
| <span data-ttu-id="9e536-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="9e536-240">resourceName2</span></span> |<span data-ttu-id="9e536-241">Não</span><span class="sxs-lookup"><span data-stu-id="9e536-241">No</span></span> |<span data-ttu-id="9e536-242">string</span><span class="sxs-lookup"><span data-stu-id="9e536-242">string</span></span> |<span data-ttu-id="9e536-243">Próximo segmento de nome do recurso se o recurso está aninhado.</span><span class="sxs-lookup"><span data-stu-id="9e536-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9e536-244">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="9e536-244">Return value</span></span>

<span data-ttu-id="9e536-245">O identificador é retornado no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="9e536-246">Comentários</span><span class="sxs-lookup"><span data-stu-id="9e536-246">Remarks</span></span>

<span data-ttu-id="9e536-247">Os valores de parâmetro que você especifica dependem se o recurso está na mesma assinatura e grupo de recursos que a implantação atual.</span><span class="sxs-lookup"><span data-stu-id="9e536-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="9e536-248">Para obter a ID de recurso de uma conta de armazenamento na mesma assinatura e grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="9e536-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="9e536-249">Para obter a ID de recurso de uma conta de armazenamento na mesma assinatura, mas em um grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="9e536-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="9e536-250">Para obter a ID de recurso de uma conta de armazenamento em uma assinatura e grupo de recursos diferentes, use:</span><span class="sxs-lookup"><span data-stu-id="9e536-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="9e536-251">Para obter a ID de recurso para um banco de dados em um grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="9e536-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="9e536-252">Frequentemente, você precisa usar essa função ao usar uma conta de armazenamento ou rede virtual em um grupo de recursos alternativo.</span><span class="sxs-lookup"><span data-stu-id="9e536-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="9e536-253">O exemplo a seguir mostra como um recurso de um grupo de recursos externo pode ser facilmente usado:</span><span class="sxs-lookup"><span data-stu-id="9e536-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="9e536-254">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9e536-254">Example</span></span>

<span data-ttu-id="9e536-255">O exemplo a seguir retorna a ID de recurso de uma conta de armazenamento no grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="9e536-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="9e536-256">A saída do exemplo anterior com os valores padrão é:</span><span class="sxs-lookup"><span data-stu-id="9e536-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="9e536-257">Nome</span><span class="sxs-lookup"><span data-stu-id="9e536-257">Name</span></span> | <span data-ttu-id="9e536-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e536-258">Type</span></span> | <span data-ttu-id="9e536-259">Valor</span><span class="sxs-lookup"><span data-stu-id="9e536-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9e536-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="9e536-260">sameRGOutput</span></span> | <span data-ttu-id="9e536-261">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9e536-261">String</span></span> | <span data-ttu-id="9e536-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="9e536-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="9e536-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="9e536-263">differentRGOutput</span></span> | <span data-ttu-id="9e536-264">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9e536-264">String</span></span> | <span data-ttu-id="9e536-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="9e536-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="9e536-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="9e536-266">differentSubOutput</span></span> | <span data-ttu-id="9e536-267">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9e536-267">String</span></span> | <span data-ttu-id="9e536-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="9e536-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="9e536-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="9e536-269">nestedResourceOutput</span></span> | <span data-ttu-id="9e536-270">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9e536-270">String</span></span> | <span data-ttu-id="9e536-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="9e536-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="9e536-272">subscription</span><span class="sxs-lookup"><span data-stu-id="9e536-272">subscription</span></span>
`subscription()`

<span data-ttu-id="9e536-273">Retorna detalhes sobre a assinatura da implantação atual.</span><span class="sxs-lookup"><span data-stu-id="9e536-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="9e536-274">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="9e536-274">Return value</span></span>

<span data-ttu-id="9e536-275">A função retorna o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9e536-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="9e536-276">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9e536-276">Example</span></span>

<span data-ttu-id="9e536-277">O exemplo a seguir mostra a função de assinatura chamada na seção de saídas.</span><span class="sxs-lookup"><span data-stu-id="9e536-277">The following example shows the subscription function called in the outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="9e536-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e536-278">Next steps</span></span>
* <span data-ttu-id="9e536-279">Para obter uma descrição das seções de um modelo do Azure Resource Manager, veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e536-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9e536-280">Para mesclar vários modelos, veja [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e536-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="9e536-281">Para iterar um número de vezes especificado ao criar um tipo de recurso, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="9e536-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="9e536-282">Para ver como implantar o modelo que você criou, veja [Implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9e536-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

