---
title: "Operações assíncronas do Azure | Microsoft Docs"
description: "Descreve como rastrear operações assíncronas no Azure."
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
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="63f46-103">Rastrear operações assíncronas no Azure</span><span class="sxs-lookup"><span data-stu-id="63f46-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="63f46-104">Algumas operações REST do Azure são executadas de forma assíncrona porque a operação não pode ser concluída com rapidez.</span><span class="sxs-lookup"><span data-stu-id="63f46-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="63f46-105">Este tópico descreve como controlar o status das operações assíncronas por meio de valores retornados na resposta.</span><span class="sxs-lookup"><span data-stu-id="63f46-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="63f46-106">Códigos de status de operações assíncronas</span><span class="sxs-lookup"><span data-stu-id="63f46-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="63f46-107">Uma operação assíncrona inicialmente retorna um dos seguintes códigos de status HTTP:</span><span class="sxs-lookup"><span data-stu-id="63f46-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="63f46-108">201 (Criado)</span><span class="sxs-lookup"><span data-stu-id="63f46-108">201 (Created)</span></span>
* <span data-ttu-id="63f46-109">202 (Aceito)</span><span class="sxs-lookup"><span data-stu-id="63f46-109">202 (Accepted)</span></span> 

<span data-ttu-id="63f46-110">Quando a operação for concluída com êxito, ela retorna um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="63f46-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="63f46-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="63f46-111">200 (OK)</span></span>
* <span data-ttu-id="63f46-112">204 (Sem Conteúdo)</span><span class="sxs-lookup"><span data-stu-id="63f46-112">204 (No Content)</span></span> 

<span data-ttu-id="63f46-113">Consulte a [Documentação da API REST](/rest/api/) para ver as respostas para a operação que você está executando.</span><span class="sxs-lookup"><span data-stu-id="63f46-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="63f46-114">Monitorar o status da operação</span><span class="sxs-lookup"><span data-stu-id="63f46-114">Monitor status of operation</span></span>
<span data-ttu-id="63f46-115">As operações REST assíncronas retornam valores de cabeçalho, que você pode usar para determinar o status da operação.</span><span class="sxs-lookup"><span data-stu-id="63f46-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="63f46-116">Há potencialmente três valores de cabeçalho a examinar:</span><span class="sxs-lookup"><span data-stu-id="63f46-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="63f46-117">`Azure-AsyncOperation` ‑ A URL para verificar o status da operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="63f46-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="63f46-118">Se a operação retornar esse valor, sempre o use (em vez de Location) para acompanhar o status da operação.</span><span class="sxs-lookup"><span data-stu-id="63f46-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="63f46-119">`Location` ‑ A URL para determinar quando uma operação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="63f46-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="63f46-120">Use esse valor somente quando Azure-AsyncOperation não é retornado.</span><span class="sxs-lookup"><span data-stu-id="63f46-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="63f46-121">`Retry-After` ‑ O número de segundos de espera antes de verificar o status da operação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="63f46-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="63f46-122">No entanto, nem toda operação assíncrona retorna todos esses valores.</span><span class="sxs-lookup"><span data-stu-id="63f46-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="63f46-123">Por exemplo, você precisará avaliar o valor do cabeçalho Azure-AsyncOperation para uma operação e o valor do cabeçalho Location para outra operação.</span><span class="sxs-lookup"><span data-stu-id="63f46-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="63f46-124">Recupere os valores de cabeçalho da mesma forma que faria com qualquer valor de cabeçalho para uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="63f46-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="63f46-125">Por exemplo, em C#, recupere o valor de cabeçalho de um objeto `HttpWebResponse` chamado `response` com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="63f46-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="63f46-126">Solicitação e resposta de Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="63f46-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="63f46-127">Para obter o status da operação assíncrona, envie uma solicitação GET para a URL no valor do cabeçalho Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="63f46-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="63f46-128">O corpo da resposta dessa operação contém informações sobre a operação.</span><span class="sxs-lookup"><span data-stu-id="63f46-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="63f46-129">O exemplo a seguir mostra os possíveis valores retornados da operação:</span><span class="sxs-lookup"><span data-stu-id="63f46-129">The following example shows the possible values returned from the operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="63f46-130">Somente `status` é retornado para todas as respostas.</span><span class="sxs-lookup"><span data-stu-id="63f46-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="63f46-131">O objeto de erro é retornado quando o status é Falha ou Cancelado.</span><span class="sxs-lookup"><span data-stu-id="63f46-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="63f46-132">Todos os outros valores são opcionais, portanto, a resposta recebida pode parecer diferente do exemplo.</span><span class="sxs-lookup"><span data-stu-id="63f46-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="63f46-133">Valores de provisioningState</span><span class="sxs-lookup"><span data-stu-id="63f46-133">provisioningState values</span></span>

<span data-ttu-id="63f46-134">Operações que criam, atualizam ou excluem (PUT, PATCH, DELETE) um recurso geralmente retornam um valor `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="63f46-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="63f46-135">Quando uma operação for concluída, um dos três valores a seguir será retornado:</span><span class="sxs-lookup"><span data-stu-id="63f46-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="63f46-136">Bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="63f46-136">Succeeded</span></span>
* <span data-ttu-id="63f46-137">Falha</span><span class="sxs-lookup"><span data-stu-id="63f46-137">Failed</span></span>
* <span data-ttu-id="63f46-138">Cancelado</span><span class="sxs-lookup"><span data-stu-id="63f46-138">Canceled</span></span>

<span data-ttu-id="63f46-139">Todos os outros valores indicam que a operação ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="63f46-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="63f46-140">O provedor de recursos pode retornar um valor personalizado que indica o estado.</span><span class="sxs-lookup"><span data-stu-id="63f46-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="63f46-141">Por exemplo, você pode receber **Aceito** quando a solicitação é recebida e está em execução.</span><span class="sxs-lookup"><span data-stu-id="63f46-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="63f46-142">Exemplo de solicitações e respostas</span><span class="sxs-lookup"><span data-stu-id="63f46-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="63f46-143">Iniciar a máquina virtual (202 com Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="63f46-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="63f46-144">Este exemplo mostra como determinar o status da operação **start** para máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="63f46-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="63f46-145">A solicitação inicial está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="63f46-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="63f46-146">Ele retorna um código de status 202.</span><span class="sxs-lookup"><span data-stu-id="63f46-146">It returns status code 202.</span></span> <span data-ttu-id="63f46-147">Entre os valores de cabeçalho, você verá:</span><span class="sxs-lookup"><span data-stu-id="63f46-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="63f46-148">Para verificar o status da operação assíncrona, envie outra solicitação para a URL.</span><span class="sxs-lookup"><span data-stu-id="63f46-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="63f46-149">O corpo da resposta contém o status da operação:</span><span class="sxs-lookup"><span data-stu-id="63f46-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="63f46-150">Implantar recursos (201 com Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="63f46-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="63f46-151">Este exemplo mostra como determinar o status da operação **deployments** para implantação de recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="63f46-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="63f46-152">A solicitação inicial está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="63f46-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="63f46-153">Ele retorna um código de status 201.</span><span class="sxs-lookup"><span data-stu-id="63f46-153">It returns status code 201.</span></span> <span data-ttu-id="63f46-154">O corpo da resposta inclui:</span><span class="sxs-lookup"><span data-stu-id="63f46-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="63f46-155">Entre os valores de cabeçalho, você verá:</span><span class="sxs-lookup"><span data-stu-id="63f46-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="63f46-156">Para verificar o status da operação assíncrona, envie outra solicitação para a URL.</span><span class="sxs-lookup"><span data-stu-id="63f46-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="63f46-157">O corpo da resposta contém o status da operação:</span><span class="sxs-lookup"><span data-stu-id="63f46-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="63f46-158">Quando a implantação for concluída, a resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="63f46-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="63f46-159">Criar conta de armazenamento (202 com Location e Retry-After)</span><span class="sxs-lookup"><span data-stu-id="63f46-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="63f46-160">Este exemplo mostra como determinar o status da operação **create** para contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="63f46-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="63f46-161">A solicitação inicial está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="63f46-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="63f46-162">E o corpo da solicitação contém as propriedades da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="63f46-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="63f46-163">Ele retorna um código de status 202.</span><span class="sxs-lookup"><span data-stu-id="63f46-163">It returns status code 202.</span></span> <span data-ttu-id="63f46-164">Entre os valores de cabeçalho, você verá os dois valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="63f46-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="63f46-165">Depois de aguardar o número de segundos especificado em Retry-After, verifique o status da operação assíncrona enviando outra solicitação para a URL.</span><span class="sxs-lookup"><span data-stu-id="63f46-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="63f46-166">Se a solicitação ainda estiver em execução, você receberá um código de status 202.</span><span class="sxs-lookup"><span data-stu-id="63f46-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="63f46-167">Se a solicitação tiver sido concluída, você receberá um código de status 200 e o corpo da resposta conterá as propriedades da conta de armazenamento que foi criada.</span><span class="sxs-lookup"><span data-stu-id="63f46-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63f46-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63f46-168">Next steps</span></span>

* <span data-ttu-id="63f46-169">Para ver a documentação sobre cada operação REST, consulte [Documentação da API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="63f46-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="63f46-170">Para obter informações sobre como gerenciar recursos por meio da API REST do Resource Manager, consulte [Usando a API REST do Resource Manager](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="63f46-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="63f46-171">Para obter informações sobre a implantação de modelos por meio da API REST do Resource Manager, consulte [Deploy resources with Resource Manager templates and Resource Manager REST API (Implantar recursos com modelos do Resource Manager e a API REST do Resource Manager)](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="63f46-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>