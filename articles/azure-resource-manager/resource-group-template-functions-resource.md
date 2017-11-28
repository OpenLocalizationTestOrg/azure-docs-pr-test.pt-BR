---
title: "funções de modelo do Gerenciador de recursos aaaAzure - recursos | Microsoft Docs"
description: "Descreve Olá toouse de funções em valores do Azure Resource Manager modelo tooretrieve sobre os recursos."
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
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="7a69e-103">Funções de recursos para modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a69e-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="7a69e-104">Gerenciador de recursos fornece Olá funções para obter valores de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="7a69e-105">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="7a69e-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="7a69e-106">providers</span><span class="sxs-lookup"><span data-stu-id="7a69e-106">providers</span></span>](#providers)
* [<span data-ttu-id="7a69e-107">reference</span><span class="sxs-lookup"><span data-stu-id="7a69e-107">reference</span></span>](#reference)
* [<span data-ttu-id="7a69e-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7a69e-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="7a69e-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="7a69e-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="7a69e-110">subscription</span><span class="sxs-lookup"><span data-stu-id="7a69e-110">subscription</span></span>](#subscription)

<span data-ttu-id="7a69e-111">tooget valores de parâmetros, variáveis ou implantação atual do hello, consulte [funções com valor de implantação](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7a69e-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="7a69e-112">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="7a69e-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="7a69e-113">Retorna Olá valores para qualquer tipo de recurso que dá suporte à operação de lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="7a69e-114">Olá o uso mais comum é `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="7a69e-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7a69e-115">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7a69e-115">Parameters</span></span>

| <span data-ttu-id="7a69e-116">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="7a69e-116">Parameter</span></span> | <span data-ttu-id="7a69e-117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7a69e-117">Required</span></span> | <span data-ttu-id="7a69e-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="7a69e-118">Type</span></span> | <span data-ttu-id="7a69e-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="7a69e-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7a69e-120">resourceName ou resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="7a69e-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7a69e-121">Sim</span><span class="sxs-lookup"><span data-stu-id="7a69e-121">Yes</span></span> |<span data-ttu-id="7a69e-122">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-122">string</span></span> |<span data-ttu-id="7a69e-123">Identificador exclusivo para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="7a69e-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7a69e-124">apiVersion</span></span> |<span data-ttu-id="7a69e-125">Sim</span><span class="sxs-lookup"><span data-stu-id="7a69e-125">Yes</span></span> |<span data-ttu-id="7a69e-126">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-126">string</span></span> |<span data-ttu-id="7a69e-127">Versão de API do estado de tempo de execução do recurso.</span><span class="sxs-lookup"><span data-stu-id="7a69e-127">API version of resource runtime state.</span></span> <span data-ttu-id="7a69e-128">Normalmente, no formato de saudação **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="7a69e-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7a69e-129">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7a69e-129">Return value</span></span>

<span data-ttu-id="7a69e-130">Olá retornou objeto do listkeys do tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-130">hello returned object from listKeys has hello following format:</span></span>

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

<span data-ttu-id="7a69e-131">Outras funções de lista têm formatos diferentes de retorno.</span><span class="sxs-lookup"><span data-stu-id="7a69e-131">Other list functions have different return formats.</span></span> <span data-ttu-id="7a69e-132">formato de saudação toosee de uma função, incluí-lo na seção de saídas Olá conforme mostrado no modelo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7a69e-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="7a69e-133">Comentários</span><span class="sxs-lookup"><span data-stu-id="7a69e-133">Remarks</span></span>

<span data-ttu-id="7a69e-134">Qualquer operação que começa com **list** pode ser usada como uma função no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="7a69e-135">Olá, as operações disponíveis incluem não só listkeys do, mas também operações como `list`, `listAdminKeys`, e `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="7a69e-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="7a69e-136">No entanto, você não pode usar **lista** as operações que exigem valores hello corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="7a69e-137">Por exemplo, Olá [SAS de conta da lista](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operação requer parâmetros de corpo de solicitação como *signedExpiry*, portanto, você não pode usá-lo em um modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="7a69e-138">toodetermine quais tipos de recursos tem uma operação de lista, você tem Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="7a69e-139">Saudação de exibição [operações da API REST](/rest/api/) para um provedor de recursos e procure por operações de lista.</span><span class="sxs-lookup"><span data-stu-id="7a69e-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="7a69e-140">Por exemplo, contas de armazenamento tem Olá [operação do listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="7a69e-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="7a69e-141">Saudação de uso [AzureRmProviderOperation Get](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a69e-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="7a69e-142">Olá, exemplo a seguir obtém todas as operações de lista de contas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="7a69e-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="7a69e-143">Use Olá comando CLI do Azure toofilter Olá somente operações de lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="7a69e-144">Especificar recursos hello usando qualquer Olá [função resourceId](#resourceid), ou o formato de saudação `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="7a69e-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="7a69e-145">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7a69e-145">Example</span></span>

<span data-ttu-id="7a69e-146">Olá exemplo a seguir mostra como tooreturn Olá primários e secundários as chaves de conta de armazenamento no hello saídas de seção.</span><span class="sxs-lookup"><span data-stu-id="7a69e-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="7a69e-147">providers</span><span class="sxs-lookup"><span data-stu-id="7a69e-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="7a69e-148">Retorna informações sobre um provedor de recursos e seus tipos de recursos com suporte.</span><span class="sxs-lookup"><span data-stu-id="7a69e-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="7a69e-149">Se você não fornecer um tipo de recurso, a função hello retorna todos os tipos de Olá com suporte para provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a69e-150">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7a69e-150">Parameters</span></span>

| <span data-ttu-id="7a69e-151">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="7a69e-151">Parameter</span></span> | <span data-ttu-id="7a69e-152">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7a69e-152">Required</span></span> | <span data-ttu-id="7a69e-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="7a69e-153">Type</span></span> | <span data-ttu-id="7a69e-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="7a69e-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7a69e-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="7a69e-155">providerNamespace</span></span> |<span data-ttu-id="7a69e-156">Sim</span><span class="sxs-lookup"><span data-stu-id="7a69e-156">Yes</span></span> |<span data-ttu-id="7a69e-157">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-157">string</span></span> |<span data-ttu-id="7a69e-158">Namespace do provedor de saudação</span><span class="sxs-lookup"><span data-stu-id="7a69e-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="7a69e-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="7a69e-159">resourceType</span></span> |<span data-ttu-id="7a69e-160">Não</span><span class="sxs-lookup"><span data-stu-id="7a69e-160">No</span></span> |<span data-ttu-id="7a69e-161">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-161">string</span></span> |<span data-ttu-id="7a69e-162">tipo de saudação do recurso na saudação especificado namespace.</span><span class="sxs-lookup"><span data-stu-id="7a69e-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7a69e-163">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7a69e-163">Return value</span></span>

<span data-ttu-id="7a69e-164">Cada tipo com suporte é retornado no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="7a69e-165">Ordenação de matriz de saudação retornado valores não é garantida.</span><span class="sxs-lookup"><span data-stu-id="7a69e-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="7a69e-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7a69e-166">Example</span></span>

<span data-ttu-id="7a69e-167">saudação de exemplo a seguir mostra como toouse Olá a função do provedor:</span><span class="sxs-lookup"><span data-stu-id="7a69e-167">hello following example shows how toouse hello provider function:</span></span>

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

<span data-ttu-id="7a69e-168">Olá exemplo anterior retorna um objeto no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-168">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="7a69e-169">reference</span><span class="sxs-lookup"><span data-stu-id="7a69e-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="7a69e-170">Retorna um objeto que representa o estado de tempo de execução de um recurso.</span><span class="sxs-lookup"><span data-stu-id="7a69e-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a69e-171">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7a69e-171">Parameters</span></span>

| <span data-ttu-id="7a69e-172">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="7a69e-172">Parameter</span></span> | <span data-ttu-id="7a69e-173">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7a69e-173">Required</span></span> | <span data-ttu-id="7a69e-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="7a69e-174">Type</span></span> | <span data-ttu-id="7a69e-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="7a69e-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7a69e-176">resourceName ou resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="7a69e-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7a69e-177">Sim</span><span class="sxs-lookup"><span data-stu-id="7a69e-177">Yes</span></span> |<span data-ttu-id="7a69e-178">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-178">string</span></span> |<span data-ttu-id="7a69e-179">Nome ou identificador exclusivo de um recurso.</span><span class="sxs-lookup"><span data-stu-id="7a69e-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="7a69e-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7a69e-180">apiVersion</span></span> |<span data-ttu-id="7a69e-181">Não</span><span class="sxs-lookup"><span data-stu-id="7a69e-181">No</span></span> |<span data-ttu-id="7a69e-182">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-182">string</span></span> |<span data-ttu-id="7a69e-183">Versão de API do hello o recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="7a69e-183">API version of hello specified resource.</span></span> <span data-ttu-id="7a69e-184">Inclua esse parâmetro quando o recurso de saudação não está provisionado no mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="7a69e-185">Normalmente, no formato de saudação **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="7a69e-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7a69e-186">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7a69e-186">Return value</span></span>

<span data-ttu-id="7a69e-187">Cada tipo de recurso retorna propriedades diferentes para a função de referência de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="7a69e-188">função Hello não retorna um único formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="7a69e-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="7a69e-189">Propriedades de saudação toosee para um tipo de recurso, retornar objeto Olá Olá gera seção conforme mostrado no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7a69e-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="7a69e-190">Comentários</span><span class="sxs-lookup"><span data-stu-id="7a69e-190">Remarks</span></span>

<span data-ttu-id="7a69e-191">função de referência Olá deriva seu valor de um estado de tempo de execução e, portanto, não pode ser usada na seção de variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="7a69e-192">Ela pode ser usada na seção de saídas de um modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="7a69e-193">Usando a função de referência hello, você implicitamente declarar que um recurso depende de outro recurso se o recurso Olá referenciado é provisionado no mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="7a69e-194">Propriedade do tooalso use Olá dependsOn não é necessário.</span><span class="sxs-lookup"><span data-stu-id="7a69e-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="7a69e-195">Olá função não será avaliada até hello recurso referenciado tiver concluído a implantação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="7a69e-196">toosee Olá nomes e valores de um tipo de recurso, criar um modelo que retorna o objeto de Olá Olá saídas de seção.</span><span class="sxs-lookup"><span data-stu-id="7a69e-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="7a69e-197">Se você tiver um recurso existente do mesmo tipo, o modelo retorna objeto Olá sem implantar os novos recursos.</span><span class="sxs-lookup"><span data-stu-id="7a69e-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="7a69e-198">Normalmente, você usa Olá **referência** função tooreturn um valor específico de um objeto, como o ponto de extremidade de blob de saudação URI ou o nome de domínio totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="7a69e-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="7a69e-199">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7a69e-199">Example</span></span>

<span data-ttu-id="7a69e-200">toodeploy e referência de recurso de saudação em Olá mesmo modelo, use:</span><span class="sxs-lookup"><span data-stu-id="7a69e-200">toodeploy and reference hello resource in hello same template, use:</span></span>

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

<span data-ttu-id="7a69e-201">Olá exemplo anterior retorna um objeto no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-201">hello preceding example returns an object in hello following format:</span></span>

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

<span data-ttu-id="7a69e-202">Olá exemplo a seguir faz referência a uma conta de armazenamento que não foi implantada nesse modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="7a69e-203">Olá conta de armazenamento já existe no hello mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7a69e-203">hello storage account already exists within hello same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="7a69e-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7a69e-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="7a69e-205">Retorna um objeto que representa o grupo de recursos atual hello.</span><span class="sxs-lookup"><span data-stu-id="7a69e-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7a69e-206">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7a69e-206">Return value</span></span>

<span data-ttu-id="7a69e-207">Olá retornou objeto está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-207">hello returned object is in hello following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="7a69e-208">Comentários</span><span class="sxs-lookup"><span data-stu-id="7a69e-208">Remarks</span></span>

<span data-ttu-id="7a69e-209">Um uso comum da função de resourceGroup Olá é toocreate recursos Olá mesmo local que o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a69e-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="7a69e-210">Olá exemplo a seguir usa Olá recurso grupo tooassign Olá local para um site da web.</span><span class="sxs-lookup"><span data-stu-id="7a69e-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="7a69e-211">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7a69e-211">Example</span></span>

<span data-ttu-id="7a69e-212">Olá modelo a seguir retorna propriedades de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7a69e-212">hello following template returns hello properties of hello resource group.</span></span>

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

<span data-ttu-id="7a69e-213">Olá exemplo anterior retorna um objeto no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-213">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="7a69e-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="7a69e-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="7a69e-215">Retorna Olá identificador exclusivo de um recurso.</span><span class="sxs-lookup"><span data-stu-id="7a69e-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="7a69e-216">Usar essa função quando o nome do recurso de saudação é ambíguo ou não provisionado em Olá mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7a69e-217">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7a69e-217">Parameters</span></span>

| <span data-ttu-id="7a69e-218">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="7a69e-218">Parameter</span></span> | <span data-ttu-id="7a69e-219">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7a69e-219">Required</span></span> | <span data-ttu-id="7a69e-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="7a69e-220">Type</span></span> | <span data-ttu-id="7a69e-221">Descrição</span><span class="sxs-lookup"><span data-stu-id="7a69e-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7a69e-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7a69e-222">subscriptionId</span></span> |<span data-ttu-id="7a69e-223">Não</span><span class="sxs-lookup"><span data-stu-id="7a69e-223">No</span></span> |<span data-ttu-id="7a69e-224">string (no formato GUID)</span><span class="sxs-lookup"><span data-stu-id="7a69e-224">string (In GUID format)</span></span> |<span data-ttu-id="7a69e-225">Valor padrão é assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="7a69e-225">Default value is hello current subscription.</span></span> <span data-ttu-id="7a69e-226">Especifique esse valor quando precisar tooretrieve um recurso em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="7a69e-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="7a69e-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="7a69e-227">resourceGroupName</span></span> |<span data-ttu-id="7a69e-228">Não</span><span class="sxs-lookup"><span data-stu-id="7a69e-228">No</span></span> |<span data-ttu-id="7a69e-229">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-229">string</span></span> |<span data-ttu-id="7a69e-230">O valor padrão é o grupo de recursos atual.</span><span class="sxs-lookup"><span data-stu-id="7a69e-230">Default value is current resource group.</span></span> <span data-ttu-id="7a69e-231">Especifique esse valor quando precisar tooretrieve um recurso em outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7a69e-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="7a69e-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="7a69e-232">resourceType</span></span> |<span data-ttu-id="7a69e-233">Sim</span><span class="sxs-lookup"><span data-stu-id="7a69e-233">Yes</span></span> |<span data-ttu-id="7a69e-234">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-234">string</span></span> |<span data-ttu-id="7a69e-235">Tipo de recurso, incluindo o namespace do provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="7a69e-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="7a69e-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="7a69e-236">resourceName1</span></span> |<span data-ttu-id="7a69e-237">Sim</span><span class="sxs-lookup"><span data-stu-id="7a69e-237">Yes</span></span> |<span data-ttu-id="7a69e-238">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-238">string</span></span> |<span data-ttu-id="7a69e-239">Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="7a69e-239">Name of resource.</span></span> |
| <span data-ttu-id="7a69e-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="7a69e-240">resourceName2</span></span> |<span data-ttu-id="7a69e-241">Não</span><span class="sxs-lookup"><span data-stu-id="7a69e-241">No</span></span> |<span data-ttu-id="7a69e-242">string</span><span class="sxs-lookup"><span data-stu-id="7a69e-242">string</span></span> |<span data-ttu-id="7a69e-243">Próximo segmento de nome do recurso se o recurso está aninhado.</span><span class="sxs-lookup"><span data-stu-id="7a69e-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7a69e-244">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7a69e-244">Return value</span></span>

<span data-ttu-id="7a69e-245">Identificador de saudação é retornado no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="7a69e-246">Comentários</span><span class="sxs-lookup"><span data-stu-id="7a69e-246">Remarks</span></span>

<span data-ttu-id="7a69e-247">Olá valores de parâmetro especificados dependem se o recurso de saudação é em hello mesmo grupo de assinatura e o recurso de implantação atual hello.</span><span class="sxs-lookup"><span data-stu-id="7a69e-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="7a69e-248">ID de recurso de saudação tooget para uma conta de armazenamento Olá mesmo assinatura e grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="7a69e-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7a69e-249">ID de recurso Olá tooget para uma conta de armazenamento Olá mesma assinatura, mas um grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="7a69e-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7a69e-250">ID do recurso Olá tooget para uma conta de armazenamento em uma assinatura diferente e o grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="7a69e-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7a69e-251">ID do recurso Olá tooget para um banco de dados em um grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="7a69e-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="7a69e-252">Geralmente, é necessário toouse essa função ao usar uma conta de armazenamento ou a rede virtual em um grupo de recurso alternativo.</span><span class="sxs-lookup"><span data-stu-id="7a69e-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="7a69e-253">Olá exemplo a seguir mostra como um recurso de um grupo de recursos externos pode ser facilmente usado:</span><span class="sxs-lookup"><span data-stu-id="7a69e-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="7a69e-254">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7a69e-254">Example</span></span>

<span data-ttu-id="7a69e-255">Olá exemplo a seguir retorna ID de recurso Olá para uma conta de armazenamento no grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7a69e-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

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

<span data-ttu-id="7a69e-256">saudação de saída de saudação anterior exemplo com valores padrão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="7a69e-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7a69e-257">Nome</span><span class="sxs-lookup"><span data-stu-id="7a69e-257">Name</span></span> | <span data-ttu-id="7a69e-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="7a69e-258">Type</span></span> | <span data-ttu-id="7a69e-259">Valor</span><span class="sxs-lookup"><span data-stu-id="7a69e-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7a69e-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="7a69e-260">sameRGOutput</span></span> | <span data-ttu-id="7a69e-261">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7a69e-261">String</span></span> | <span data-ttu-id="7a69e-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7a69e-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7a69e-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="7a69e-263">differentRGOutput</span></span> | <span data-ttu-id="7a69e-264">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7a69e-264">String</span></span> | <span data-ttu-id="7a69e-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7a69e-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7a69e-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="7a69e-266">differentSubOutput</span></span> | <span data-ttu-id="7a69e-267">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7a69e-267">String</span></span> | <span data-ttu-id="7a69e-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7a69e-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7a69e-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="7a69e-269">nestedResourceOutput</span></span> | <span data-ttu-id="7a69e-270">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7a69e-270">String</span></span> | <span data-ttu-id="7a69e-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="7a69e-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="7a69e-272">subscription</span><span class="sxs-lookup"><span data-stu-id="7a69e-272">subscription</span></span>
`subscription()`

<span data-ttu-id="7a69e-273">Retorna detalhes sobre assinatura Olá para implantação de saudação atual.</span><span class="sxs-lookup"><span data-stu-id="7a69e-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7a69e-274">Valor de retorno</span><span class="sxs-lookup"><span data-stu-id="7a69e-274">Return value</span></span>

<span data-ttu-id="7a69e-275">função Hello retorna Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a69e-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="7a69e-276">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7a69e-276">Example</span></span>

<span data-ttu-id="7a69e-277">Olá exemplo a seguir mostra função de assinatura hello chamada hello saídas de seção.</span><span class="sxs-lookup"><span data-stu-id="7a69e-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="7a69e-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a69e-278">Next steps</span></span>
* <span data-ttu-id="7a69e-279">Para obter uma descrição das seções de saudação em um modelo do Gerenciador de recursos do Azure, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7a69e-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7a69e-280">toomerge vários modelos, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7a69e-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="7a69e-281">tooiterate um número de vezes especificado durante a criação de um tipo de recurso, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7a69e-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="7a69e-282">toosee como modelo de saudação toodeploy que você criou, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7a69e-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

