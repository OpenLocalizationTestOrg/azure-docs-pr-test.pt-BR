---
title: "operações assíncronas aaaAzure | Microsoft Docs"
description: "Descreve como as operações assíncronas tootrack no Azure."
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
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="e2dd9-103">Rastrear operações assíncronas no Azure</span><span class="sxs-lookup"><span data-stu-id="e2dd9-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="e2dd9-104">Algumas operações REST do Azure executados de forma assíncrona porque a operação de saudação não pode ser concluída rapidamente.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="e2dd9-105">Este tópico descreve como o status de saudação tootrack das operações assíncronas por valores retornado na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="e2dd9-106">Códigos de status de operações assíncronas</span><span class="sxs-lookup"><span data-stu-id="e2dd9-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="e2dd9-107">Uma operação assíncrona inicialmente retorna um dos seguintes códigos de status HTTP:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="e2dd9-108">201 (Criado)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-108">201 (Created)</span></span>
* <span data-ttu-id="e2dd9-109">202 (Aceito)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-109">202 (Accepted)</span></span> 

<span data-ttu-id="e2dd9-110">Quando a operação de saudação for concluída com êxito, ele retorna um:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="e2dd9-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-111">200 (OK)</span></span>
* <span data-ttu-id="e2dd9-112">204 (Sem Conteúdo)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-112">204 (No Content)</span></span> 

<span data-ttu-id="e2dd9-113">Consulte toohello [documentação da API REST](/rest/api/) toosee respostas de saudação para operação Olá estão em execução.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="e2dd9-114">Monitorar o status da operação</span><span class="sxs-lookup"><span data-stu-id="e2dd9-114">Monitor status of operation</span></span>
<span data-ttu-id="e2dd9-115">Olá assíncrona REST operações retornar valores de cabeçalho, que você usar toodetermine Olá status de hello a operação.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="e2dd9-116">Potencialmente, existem tooexamine do cabeçalho de três valores:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="e2dd9-117">`Azure-AsyncOperation`-URL para verificar o status de saudação em andamento da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="e2dd9-118">Se a operação retorna esse valor, sempre use o status de saudação do tootrack de TI (em vez de local) da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="e2dd9-119">`Location` ‑ A URL para determinar quando uma operação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="e2dd9-120">Use esse valor somente quando Azure-AsyncOperation não é retornado.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="e2dd9-121">`Retry-After`-Olá o número de segundos toowait antes de verificar o status de saudação de operação assíncrona hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="e2dd9-122">No entanto, nem toda operação assíncrona retorna todos esses valores.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="e2dd9-123">Por exemplo, o valor do cabeçalho tooevaluate hello Azure AsyncOperation talvez seja necessário para uma operação e o valor de cabeçalho de local Olá para outra operação.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="e2dd9-124">Recuperar valores de cabeçalho hello como recuperaria qualquer valor de cabeçalho de uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="e2dd9-125">Por exemplo, no c#, você recuperar valor de cabeçalho de saudação de um `HttpWebResponse` objeto chamado `response` com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="e2dd9-126">Solicitação e resposta de Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="e2dd9-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="e2dd9-127">status de saudação de tooget de operação assíncrona do hello, enviar uma URL de toohello solicitação GET no valor do cabeçalho do Azure AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="e2dd9-128">corpo de Olá de resposta de saudação desta operação contém informações sobre a operação hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="e2dd9-129">Olá, exemplo a seguir mostra os valores possíveis Olá retornados da operação de saudação:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="e2dd9-130">Somente `status` é retornado para todas as respostas.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="e2dd9-131">objeto de erro de saudação é retornado quando o status de saudação é falha ou cancelada.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="e2dd9-132">Todos os outros valores são opcionais. Portanto, resposta Olá que recebe pode ser diferente do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="e2dd9-133">Valores de provisioningState</span><span class="sxs-lookup"><span data-stu-id="e2dd9-133">provisioningState values</span></span>

<span data-ttu-id="e2dd9-134">Operações que criam, atualizam ou excluem (PUT, PATCH, DELETE) um recurso geralmente retornam um valor `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="e2dd9-135">Quando uma operação for concluída, um dos três valores a seguir será retornado:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="e2dd9-136">Bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="e2dd9-136">Succeeded</span></span>
* <span data-ttu-id="e2dd9-137">Falha</span><span class="sxs-lookup"><span data-stu-id="e2dd9-137">Failed</span></span>
* <span data-ttu-id="e2dd9-138">Cancelado</span><span class="sxs-lookup"><span data-stu-id="e2dd9-138">Canceled</span></span>

<span data-ttu-id="e2dd9-139">Todos os outros valores indicam a operação Olá ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="e2dd9-140">provedor de recursos de saudação pode retornar um valor que indica o estado.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="e2dd9-141">Por exemplo, você pode receber **aceito** quando a solicitação de saudação é recebida e em execução.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="e2dd9-142">Exemplo de solicitações e respostas</span><span class="sxs-lookup"><span data-stu-id="e2dd9-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="e2dd9-143">Iniciar a máquina virtual (202 com Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="e2dd9-144">Este exemplo mostra como toodetermine Olá status de **iniciar** operação para máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="e2dd9-145">solicitação de saudação inicial está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="e2dd9-146">Ele retorna um código de status 202.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-146">It returns status code 202.</span></span> <span data-ttu-id="e2dd9-147">Entre os valores de cabeçalho hello, consulte:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="e2dd9-148">status de saudação toocheck da operação assíncrona do hello, enviar outra solicitação toothat URL.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="e2dd9-149">corpo da resposta Olá contém status de saudação da operação de saudação:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="e2dd9-150">Implantar recursos (201 com Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="e2dd9-151">Este exemplo mostra como toodetermine Olá status de **implantações** operação para implantar recursos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="e2dd9-152">solicitação de saudação inicial está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="e2dd9-153">Ele retorna um código de status 201.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-153">It returns status code 201.</span></span> <span data-ttu-id="e2dd9-154">saudação de corpo de resposta de saudação inclui:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="e2dd9-155">Entre os valores de cabeçalho hello, consulte:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="e2dd9-156">status de saudação toocheck da operação assíncrona do hello, enviar outra solicitação toothat URL.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="e2dd9-157">corpo da resposta Olá contém status de saudação da operação de saudação:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="e2dd9-158">Quando Olá implantação for concluída, a resposta de saudação contém:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="e2dd9-159">Criar conta de armazenamento (202 com Location e Retry-After)</span><span class="sxs-lookup"><span data-stu-id="e2dd9-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="e2dd9-160">Este exemplo mostra como toodetermine Olá status de saudação **criar** operação para contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="e2dd9-161">solicitação de saudação inicial está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="e2dd9-162">E o corpo da solicitação Olá contém propriedades da conta de armazenamento hello:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="e2dd9-163">Ele retorna um código de status 202.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-163">It returns status code 202.</span></span> <span data-ttu-id="e2dd9-164">Entre os valores de cabeçalho hello, você verá Olá dois valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2dd9-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="e2dd9-165">Depois de aguardar por número de segundos especificado em Retry-After, verifique o status de saudação de operação assíncrona Olá enviando outra solicitação toothat URL.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="e2dd9-166">Se a solicitação Olá ainda está em execução, você receberá um código de status 202.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="e2dd9-167">Se a solicitação de saudação for concluída, a receber um código de status 200 e corpo de saudação da resposta Olá contém propriedades de Olá Olá da conta de armazenamento que foi criado.</span><span class="sxs-lookup"><span data-stu-id="e2dd9-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2dd9-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2dd9-168">Next steps</span></span>

* <span data-ttu-id="e2dd9-169">Para ver a documentação sobre cada operação REST, consulte [Documentação da API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="e2dd9-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="e2dd9-170">Para obter informações sobre o gerenciamento de recursos por meio de saudação REST API do Gerenciador de recursos, consulte [hello usando REST API do Gerenciador de recursos](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="e2dd9-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="e2dd9-171">Para obter informações sobre a implantação de modelos por meio de saudação REST API do Gerenciador de recursos, consulte [implantar recursos com modelos do Gerenciador de recursos e a API de REST do Gerenciador de recursos](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="e2dd9-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
