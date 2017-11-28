---
title: "limites de solicitações do Gerenciador de recursos de aaaAzure | Microsoft Docs"
description: "Descreve como toouse limitação com o Azure Resource Manager solicita quando os limites de assinatura foi atingidos."
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="2b255-103">Restrição de solicitações do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2b255-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="2b255-104">Para cada assinatura e de locatário, limites de Gerenciador de recursos too15 de solicitações, 000 por hora de leitura e gravação solicitações too1, 200 por hora.</span><span class="sxs-lookup"><span data-stu-id="2b255-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="2b255-105">Esses limites se aplicam a instância do Gerenciador de recursos do Azure tooeach; Há várias instâncias em todas as regiões do Azure e do Azure Resource Manager é implantado tooall Azure regiões.</span><span class="sxs-lookup"><span data-stu-id="2b255-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="2b255-106">Portanto, na prática, os limites são efetivamente muito maiores do que aqueles listados acima, pois as solicitações do usuário são geralmente atendidas por muitas instâncias diferentes.</span><span class="sxs-lookup"><span data-stu-id="2b255-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="2b255-107">Se seu aplicativo ou script atingir esses limites, você precisa toothrottle suas solicitações.</span><span class="sxs-lookup"><span data-stu-id="2b255-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="2b255-108">Este tópico mostra como Olá toodetermine restantes solicita que você tem antes de atingir o limite de saudação e toorespond quando você atingiu o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="2b255-109">Quando você atingir o limite de saudação, você receberá o código de status HTTP da saudação **muito 429 muitas solicitações**.</span><span class="sxs-lookup"><span data-stu-id="2b255-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="2b255-110">número de solicitações de Olá é tooeither no escopo de sua assinatura ou seu locatário.</span><span class="sxs-lookup"><span data-stu-id="2b255-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="2b255-111">Se você tiver várias, aplicativos simultâneos fazendo solicitações em sua assinatura, Olá solicitações desses aplicativos são adicionados juntos toodetermine número de saudação de solicitações restantes.</span><span class="sxs-lookup"><span data-stu-id="2b255-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="2b255-112">Solicitações de assinatura no escopo são aquelas Olá envolvem passando a id de assinatura, como recuperar grupos de recursos de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="2b255-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="2b255-113">Solicitações no escopo do locatário não incluem sua ID de assinatura, assim como a recuperação de locais do Azure válidos.</span><span class="sxs-lookup"><span data-stu-id="2b255-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="2b255-114">Solicitações restantes</span><span class="sxs-lookup"><span data-stu-id="2b255-114">Remaining requests</span></span>
<span data-ttu-id="2b255-115">Você pode determinar o número de saudação de solicitações restantes, examinando os cabeçalhos de resposta.</span><span class="sxs-lookup"><span data-stu-id="2b255-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="2b255-116">Cada solicitação inclui valores de número de saudação de solicitações de gravação e leitura restante.</span><span class="sxs-lookup"><span data-stu-id="2b255-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="2b255-117">Olá tabela a seguir descreve cabeçalhos de resposta de saudação, que você pode examinar os valores:</span><span class="sxs-lookup"><span data-stu-id="2b255-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="2b255-118">Cabeçalho de resposta</span><span class="sxs-lookup"><span data-stu-id="2b255-118">Response header</span></span> | <span data-ttu-id="2b255-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b255-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b255-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="2b255-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="2b255-121">Leituras no escopo da assinatura restantes</span><span class="sxs-lookup"><span data-stu-id="2b255-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="2b255-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="2b255-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="2b255-123">Gravações no escopo da assinatura restantes</span><span class="sxs-lookup"><span data-stu-id="2b255-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="2b255-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="2b255-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="2b255-125">Leituras no escopo do locatário restantes</span><span class="sxs-lookup"><span data-stu-id="2b255-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="2b255-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="2b255-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="2b255-127">Gravações no escopo do locatário restantes</span><span class="sxs-lookup"><span data-stu-id="2b255-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="2b255-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="2b255-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="2b255-129">Solicitações de tipo de recurso no escopo da assinatura restantes.</span><span class="sxs-lookup"><span data-stu-id="2b255-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="2b255-130">Esse valor de cabeçalho é retornado somente se um serviço tiver substituído o limite padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="2b255-131">Gerenciador de recursos adiciona esse valor em vez da saudação assinatura leituras ou gravações.</span><span class="sxs-lookup"><span data-stu-id="2b255-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="2b255-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="2b255-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="2b255-133">Solicitações de coletas de tipo de recurso no escopo da assinatura restantes.</span><span class="sxs-lookup"><span data-stu-id="2b255-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="2b255-134">Esse valor de cabeçalho é retornado somente se um serviço tiver substituído o limite padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="2b255-135">Esse valor fornece o número de saudação de coleta de solicitações restantes (recursos de lista).</span><span class="sxs-lookup"><span data-stu-id="2b255-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="2b255-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="2b255-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="2b255-137">Solicitações de tipo de recurso no escopo do locatário restantes.</span><span class="sxs-lookup"><span data-stu-id="2b255-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="2b255-138">Esse cabeçalho é adicionado somente para solicitações no nível de locatário, e somente se um serviço tiver substituído o limite padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="2b255-139">Gerenciador de recursos adiciona esse valor em vez da saudação locatário leituras ou gravações.</span><span class="sxs-lookup"><span data-stu-id="2b255-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="2b255-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="2b255-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="2b255-141">Solicitações de coletas de tipo de recurso no escopo do locatário restantes.</span><span class="sxs-lookup"><span data-stu-id="2b255-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="2b255-142">Esse cabeçalho é adicionado somente para solicitações no nível de locatário, e somente se um serviço tiver substituído o limite padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="2b255-143">Recuperando valores de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="2b255-143">Retrieving hello header values</span></span>
<span data-ttu-id="2b255-144">Recuperar esses valores de cabeçalho no seu código ou script não é diferente de recuperar um outro valor de cabeçalho qualquer.</span><span class="sxs-lookup"><span data-stu-id="2b255-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="2b255-145">Por exemplo, em **c#**, recuperar o valor de cabeçalho de saudação de um **HttpWebResponse** objeto chamado **resposta** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b255-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="2b255-146">Em **PowerShell**, recuperar o valor de cabeçalho de saudação de uma operação de Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="2b255-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="2b255-147">Ou, se quiser toosee Olá restantes solicitações de depuração, você pode fornecer Olá **-Debug** parâmetro em sua **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2b255-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="2b255-148">Que retorna vários valores, incluindo o seguinte valor de resposta de saudação:</span><span class="sxs-lookup"><span data-stu-id="2b255-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="2b255-149">Em **CLI do Azure**, recuperar o valor do cabeçalho hello usando Olá opção mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="2b255-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="2b255-150">Que retorna vários valores, incluindo Olá objeto a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b255-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="2b255-151">Aguardando antes de enviar a próxima solicitação</span><span class="sxs-lookup"><span data-stu-id="2b255-151">Waiting before sending next request</span></span>
<span data-ttu-id="2b255-152">Quando você atingir o limite de solicitação de Olá, Gerenciador de recursos retorna Olá **429** código de status HTTP e um **Retry-After** valor no cabeçalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="2b255-153">Olá **Retry-After** valor Especifica o número de saudação de segundos que o aplicativo deve aguardar (ou suspensão) antes de enviar a próxima solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b255-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="2b255-154">Se você enviar uma solicitação antes de decorrido o valor de repetição hello, sua solicitação não será processada e será retornado um novo valor de repetição.</span><span class="sxs-lookup"><span data-stu-id="2b255-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b255-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b255-155">Next steps</span></span>

* <span data-ttu-id="2b255-156">Para obter mais informações sobre limites e cotas, confira [Assinatura do Azure e limite de serviços, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2b255-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="2b255-157">toolearn sobre o tratamento de solicitações REST assíncronas, consulte [controlar operações assíncronas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="2b255-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
