---
title: "Limites de solicitação do Azure Resource Manager | Microsoft Docs"
description: "Descreve como usar a limitação com solicitações Azure Resource Manager quando os limites de assinatura tiverem sido atingidos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="71d90-103">Restrição de solicitações do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71d90-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="71d90-104">Para cada assinatura e locatário, os limites do Resource Manager limita as solicitações de leitura para 15.000 por hora e solicitações de gravação para 1.200 por hora.</span><span class="sxs-lookup"><span data-stu-id="71d90-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="71d90-105">Esses limites se aplicam a cada instância do Azure Resource Manager. Há várias instâncias em todas as regiões do Azure e o Azure Resource Manager é implantado em todas as regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="71d90-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="71d90-106">Portanto, na prática, os limites são efetivamente muito maiores do que aqueles listados acima, pois as solicitações do usuário são geralmente atendidas por muitas instâncias diferentes.</span><span class="sxs-lookup"><span data-stu-id="71d90-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="71d90-107">Se seu aplicativo ou script atingir esses limites, será necessário restringir suas solicitações.</span><span class="sxs-lookup"><span data-stu-id="71d90-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="71d90-108">Este tópico mostra como determinar as solicitações restantes que você tem antes de atingir o limite e como responder quando você tiver atingido o limite.</span><span class="sxs-lookup"><span data-stu-id="71d90-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="71d90-109">Quando você alcança o limite, recebe o código de status HTTP **429 Excesso de solicitações**.</span><span class="sxs-lookup"><span data-stu-id="71d90-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="71d90-110">O número de solicitações é no escopo da sua assinatura ou de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="71d90-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="71d90-111">Se você tiver vários aplicativos simultâneos fazendo solicitações em sua assinatura, as solicitações desses aplicativos serão adicionadas juntas para determinar o número de solicitações restantes.</span><span class="sxs-lookup"><span data-stu-id="71d90-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="71d90-112">As solicitações no escopo da assinatura são aquelas que envolvem a passagem da ID de assinatura, assim como a recuperação dos grupos de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="71d90-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="71d90-113">Solicitações no escopo do locatário não incluem sua ID de assinatura, assim como a recuperação de locais do Azure válidos.</span><span class="sxs-lookup"><span data-stu-id="71d90-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="71d90-114">Solicitações restantes</span><span class="sxs-lookup"><span data-stu-id="71d90-114">Remaining requests</span></span>
<span data-ttu-id="71d90-115">Você pode determinar o número de solicitações restantes ao examinar cabeçalhos de resposta.</span><span class="sxs-lookup"><span data-stu-id="71d90-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="71d90-116">Cada solicitação inclui os valores para o número de solicitações de leitura e gravação restantes.</span><span class="sxs-lookup"><span data-stu-id="71d90-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="71d90-117">A tabela a seguir descreve os cabeçalhos de resposta que você pode examinar em busca desses valores:</span><span class="sxs-lookup"><span data-stu-id="71d90-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="71d90-118">Cabeçalho de resposta</span><span class="sxs-lookup"><span data-stu-id="71d90-118">Response header</span></span> | <span data-ttu-id="71d90-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="71d90-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71d90-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="71d90-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="71d90-121">Leituras no escopo da assinatura restantes</span><span class="sxs-lookup"><span data-stu-id="71d90-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="71d90-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="71d90-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="71d90-123">Gravações no escopo da assinatura restantes</span><span class="sxs-lookup"><span data-stu-id="71d90-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="71d90-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="71d90-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="71d90-125">Leituras no escopo do locatário restantes</span><span class="sxs-lookup"><span data-stu-id="71d90-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="71d90-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="71d90-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="71d90-127">Gravações no escopo do locatário restantes</span><span class="sxs-lookup"><span data-stu-id="71d90-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="71d90-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="71d90-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="71d90-129">Solicitações de tipo de recurso no escopo da assinatura restantes.</span><span class="sxs-lookup"><span data-stu-id="71d90-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="71d90-130">Esse valor de cabeçalho só será retornado se um serviço tiver substituído o limite padrão.</span><span class="sxs-lookup"><span data-stu-id="71d90-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="71d90-131">O Resource Manager adiciona esse valor em vez das leituras ou gravações da assinatura.</span><span class="sxs-lookup"><span data-stu-id="71d90-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="71d90-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="71d90-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="71d90-133">Solicitações de coletas de tipo de recurso no escopo da assinatura restantes.</span><span class="sxs-lookup"><span data-stu-id="71d90-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="71d90-134">Esse valor de cabeçalho só será retornado se um serviço tiver substituído o limite padrão.</span><span class="sxs-lookup"><span data-stu-id="71d90-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="71d90-135">Esse valor fornece o número de solicitações de coleta restantes (listar recursos).</span><span class="sxs-lookup"><span data-stu-id="71d90-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="71d90-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="71d90-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="71d90-137">Solicitações de tipo de recurso no escopo do locatário restantes.</span><span class="sxs-lookup"><span data-stu-id="71d90-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="71d90-138">Esse cabeçalho será adicionado somente para solicitações em nível de locatário e somente se um serviço tiver substituído o limite padrão.</span><span class="sxs-lookup"><span data-stu-id="71d90-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="71d90-139">O Resource Manager adiciona esse valor em vez das leituras ou gravações do locatário.</span><span class="sxs-lookup"><span data-stu-id="71d90-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="71d90-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="71d90-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="71d90-141">Solicitações de coletas de tipo de recurso no escopo do locatário restantes.</span><span class="sxs-lookup"><span data-stu-id="71d90-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="71d90-142">Esse cabeçalho será adicionado somente para solicitações em nível de locatário e somente se um serviço tiver substituído o limite padrão.</span><span class="sxs-lookup"><span data-stu-id="71d90-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="71d90-143">Recuperar os valores de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="71d90-143">Retrieving the header values</span></span>
<span data-ttu-id="71d90-144">Recuperar esses valores de cabeçalho no seu código ou script não é diferente de recuperar um outro valor de cabeçalho qualquer.</span><span class="sxs-lookup"><span data-stu-id="71d90-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="71d90-145">Por exemplo, em **C#**, recupere o valor de cabeçalho de um objeto **HttpWebResponse** chamado **response** com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="71d90-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="71d90-146">No **PowerShell**, você recupera o valor de cabeçalho de uma operação Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="71d90-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="71d90-147">Ou, se quiser ver as solicitações restantes para depuração, você pode fornecer o parâmetro **-Debug** em seu cmdlet **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="71d90-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="71d90-148">Que retorna muitos valores, incluindo o seguinte valor de resposta:</span><span class="sxs-lookup"><span data-stu-id="71d90-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="71d90-149">Na **CLI do Azure**, você recupera o valor do cabeçalho usando a opção mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="71d90-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="71d90-150">Que retorna muitos valores, incluindo o seguinte objeto:</span><span class="sxs-lookup"><span data-stu-id="71d90-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="71d90-151">Aguardando antes de enviar a próxima solicitação</span><span class="sxs-lookup"><span data-stu-id="71d90-151">Waiting before sending next request</span></span>
<span data-ttu-id="71d90-152">Quando você alcançar o limite de solicitação, o Resource Manager retorna o código de status HTTP **429** e um valor **Retry-After** no cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="71d90-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="71d90-153">O valor **Retry-After** especifica o número de segundos que o aplicativo deve aguardar (ou ficar suspenso) antes de enviar a próxima solicitação.</span><span class="sxs-lookup"><span data-stu-id="71d90-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="71d90-154">Se você enviar uma solicitação antes que o valor de repetição tenha decorrido, sua solicitação não será processada e um novo valor de repetição será retornado.</span><span class="sxs-lookup"><span data-stu-id="71d90-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71d90-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71d90-155">Next steps</span></span>

* <span data-ttu-id="71d90-156">Para obter mais informações sobre limites e cotas, confira [Assinatura do Azure e limite de serviços, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="71d90-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="71d90-157">Para saber mais sobre como lidar com solicitações assíncronas de REST, confira [Track asynchronous Azure operations](resource-manager-async-operations.md) (Rastrear operações assíncronas do Azure).</span><span class="sxs-lookup"><span data-stu-id="71d90-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
