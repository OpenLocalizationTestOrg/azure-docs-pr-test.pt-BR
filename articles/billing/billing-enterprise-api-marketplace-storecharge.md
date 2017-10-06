---
title: "aaaAzure cobrança Enterprise APIs - encargos do Marketplace | Microsoft Docs"
description: "Saiba mais sobre Olá APIs de relatórios que permitem que os dados de consumo do Azure Enterprise clientes toopull programaticamente."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="b2b56-103">APIs de Relatórios para clientes Enterprise – Custos de Armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="b2b56-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="b2b56-104">Olá API de custos de armazenamento do Marketplace retorna Olá baseada no uso marketplace encargos divisão por dia para Olá especificado o período de cobrança ou datas de início e término (taxas de uma vez não estão incluídas).</span><span class="sxs-lookup"><span data-stu-id="b2b56-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="b2b56-105">Solicitação</span><span class="sxs-lookup"><span data-stu-id="b2b56-105">Request</span></span> 
<span data-ttu-id="b2b56-106">Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="b2b56-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="b2b56-107">Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados.</span><span class="sxs-lookup"><span data-stu-id="b2b56-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="b2b56-108">Intervalos de tempo personalizado podem ser especificados com o início do hello e terminar parâmetros de data que estão no tempo de saudação formato AAAA-MM-dd, Olá máximo com suporte intervalo é de 36 meses.</span><span class="sxs-lookup"><span data-stu-id="b2b56-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="b2b56-109">Método</span><span class="sxs-lookup"><span data-stu-id="b2b56-109">Method</span></span> | <span data-ttu-id="b2b56-110">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="b2b56-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="b2b56-111">GET</span><span class="sxs-lookup"><span data-stu-id="b2b56-111">GET</span></span>|<span data-ttu-id="b2b56-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b2b56-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="b2b56-113">GET</span><span class="sxs-lookup"><span data-stu-id="b2b56-113">GET</span></span>|<span data-ttu-id="b2b56-114">https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/billingPeriods/{períododeCobrança}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b2b56-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="b2b56-115">GET</span><span class="sxs-lookup"><span data-stu-id="b2b56-115">GET</span></span>|<span data-ttu-id="b2b56-116">https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="b2b56-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="b2b56-117">versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.</span><span class="sxs-lookup"><span data-stu-id="b2b56-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="b2b56-118">Resposta</span><span class="sxs-lookup"><span data-stu-id="b2b56-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="b2b56-119">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="b2b56-119">**Response property definitions**</span></span>

|<span data-ttu-id="b2b56-120">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="b2b56-120">Property Name</span></span>| <span data-ttu-id="b2b56-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2b56-121">Type</span></span>| <span data-ttu-id="b2b56-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2b56-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="b2b56-123">ID</span><span class="sxs-lookup"><span data-stu-id="b2b56-123">id</span></span>|<span data-ttu-id="b2b56-124">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-124">string</span></span>|<span data-ttu-id="b2b56-125">Id exclusiva para o item de cobrança do marketplace Olá</span><span class="sxs-lookup"><span data-stu-id="b2b56-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="b2b56-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="b2b56-126">subscriptionGuid</span></span>|<span data-ttu-id="b2b56-127">Guid</span><span class="sxs-lookup"><span data-stu-id="b2b56-127">Guid</span></span>|<span data-ttu-id="b2b56-128">Olá Guid de assinatura</span><span class="sxs-lookup"><span data-stu-id="b2b56-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="b2b56-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="b2b56-129">subscriptionName</span></span>|<span data-ttu-id="b2b56-130">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-130">string</span></span>|<span data-ttu-id="b2b56-131">Olá, nome da assinatura</span><span class="sxs-lookup"><span data-stu-id="b2b56-131">hello Subscription Name</span></span>|
|<span data-ttu-id="b2b56-132">meterId</span><span class="sxs-lookup"><span data-stu-id="b2b56-132">meterId</span></span>|<span data-ttu-id="b2b56-133">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-133">string</span></span>|<span data-ttu-id="b2b56-134">ID de saudação emitido medidor</span><span class="sxs-lookup"><span data-stu-id="b2b56-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="b2b56-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="b2b56-135">usageStartDate</span></span>|<span data-ttu-id="b2b56-136">Datetime</span><span class="sxs-lookup"><span data-stu-id="b2b56-136">DateTime</span></span>|<span data-ttu-id="b2b56-137">Hora de início para o registro de uso de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="b2b56-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="b2b56-138">usageEndDate</span></span>|<span data-ttu-id="b2b56-139">Datetime</span><span class="sxs-lookup"><span data-stu-id="b2b56-139">DateTime</span></span>|<span data-ttu-id="b2b56-140">Hora de término para o registro de uso de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-140">End time for hello usage record</span></span>|
|<span data-ttu-id="b2b56-141">offerName</span><span class="sxs-lookup"><span data-stu-id="b2b56-141">offerName</span></span>|<span data-ttu-id="b2b56-142">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-142">string</span></span>|<span data-ttu-id="b2b56-143">nome da oferta Olá</span><span class="sxs-lookup"><span data-stu-id="b2b56-143">hello Offer name</span></span>|
|<span data-ttu-id="b2b56-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2b56-144">resourceGroup</span></span>|<span data-ttu-id="b2b56-145">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-145">string</span></span>|<span data-ttu-id="b2b56-146">Grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-146">hello resource Group</span></span>|
|<span data-ttu-id="b2b56-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="b2b56-147">instanceId</span></span>|<span data-ttu-id="b2b56-148">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-148">string</span></span>|<span data-ttu-id="b2b56-149">ID da instância</span><span class="sxs-lookup"><span data-stu-id="b2b56-149">Instance Id</span></span>|
|<span data-ttu-id="b2b56-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="b2b56-150">additionalInfo</span></span>|<span data-ttu-id="b2b56-151">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-151">string</span></span>|<span data-ttu-id="b2b56-152">Cadeia de caracteres JSON de informações adicionais</span><span class="sxs-lookup"><span data-stu-id="b2b56-152">Additional info JSON string</span></span>|
|<span data-ttu-id="b2b56-153">marcas</span><span class="sxs-lookup"><span data-stu-id="b2b56-153">tags</span></span>|<span data-ttu-id="b2b56-154">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-154">string</span></span>|<span data-ttu-id="b2b56-155">Cadeia de caracteres JSON da marca</span><span class="sxs-lookup"><span data-stu-id="b2b56-155">Tag JSON string</span></span>|
|<span data-ttu-id="b2b56-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="b2b56-156">orderNumber</span></span>|<span data-ttu-id="b2b56-157">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-157">string</span></span>|<span data-ttu-id="b2b56-158">número de ordem de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-158">hello order number</span></span>|
|<span data-ttu-id="b2b56-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="b2b56-159">unitOfMeasure</span></span>|<span data-ttu-id="b2b56-160">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-160">string</span></span>|<span data-ttu-id="b2b56-161">Unidade de medida para o medidor Olá</span><span class="sxs-lookup"><span data-stu-id="b2b56-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="b2b56-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="b2b56-162">costCenter</span></span>|<span data-ttu-id="b2b56-163">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-163">string</span></span>|<span data-ttu-id="b2b56-164">Centro de custo de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-164">hello cost center</span></span>|
|<span data-ttu-id="b2b56-165">accountId</span><span class="sxs-lookup"><span data-stu-id="b2b56-165">accountId</span></span>|<span data-ttu-id="b2b56-166">int</span><span class="sxs-lookup"><span data-stu-id="b2b56-166">int</span></span>|<span data-ttu-id="b2b56-167">conta de saudação Id</span><span class="sxs-lookup"><span data-stu-id="b2b56-167">hello account Id</span></span>|
|<span data-ttu-id="b2b56-168">accountName</span><span class="sxs-lookup"><span data-stu-id="b2b56-168">accountName</span></span>|<span data-ttu-id="b2b56-169">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-169">string</span></span> |<span data-ttu-id="b2b56-170">Olá, nome da conta</span><span class="sxs-lookup"><span data-stu-id="b2b56-170">hello Account Name</span></span>|
|<span data-ttu-id="b2b56-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="b2b56-171">accountOwnerId</span></span>|<span data-ttu-id="b2b56-172">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-172">string</span></span>|<span data-ttu-id="b2b56-173">Olá Id de proprietário de conta</span><span class="sxs-lookup"><span data-stu-id="b2b56-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="b2b56-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="b2b56-174">departmentId</span></span>|<span data-ttu-id="b2b56-175">int</span><span class="sxs-lookup"><span data-stu-id="b2b56-175">int</span></span>|<span data-ttu-id="b2b56-176">departamento de saudação Id</span><span class="sxs-lookup"><span data-stu-id="b2b56-176">hello department Id</span></span>|
|<span data-ttu-id="b2b56-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="b2b56-177">departmentName</span></span>|<span data-ttu-id="b2b56-178">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-178">string</span></span>|<span data-ttu-id="b2b56-179">nome do departamento de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-179">hello department name</span></span>|
|<span data-ttu-id="b2b56-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="b2b56-180">publisherName</span></span>|<span data-ttu-id="b2b56-181">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-181">string</span></span>|<span data-ttu-id="b2b56-182">nome do publicador Olá</span><span class="sxs-lookup"><span data-stu-id="b2b56-182">hello publisher name</span></span>|
|<span data-ttu-id="b2b56-183">planName</span><span class="sxs-lookup"><span data-stu-id="b2b56-183">planName</span></span>|<span data-ttu-id="b2b56-184">string</span><span class="sxs-lookup"><span data-stu-id="b2b56-184">string</span></span>|<span data-ttu-id="b2b56-185">nome do plano de saudação</span><span class="sxs-lookup"><span data-stu-id="b2b56-185">hello Plan name</span></span>|
|<span data-ttu-id="b2b56-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="b2b56-186">consumedQuantity</span></span>|<span data-ttu-id="b2b56-187">decimal</span><span class="sxs-lookup"><span data-stu-id="b2b56-187">decimal</span></span>|<span data-ttu-id="b2b56-188">Quantidade consumida durante esse período</span><span class="sxs-lookup"><span data-stu-id="b2b56-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="b2b56-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="b2b56-189">resourceRate</span></span>|<span data-ttu-id="b2b56-190">decimal</span><span class="sxs-lookup"><span data-stu-id="b2b56-190">decimal</span></span>|<span data-ttu-id="b2b56-191">Preço unitário medidor Olá</span><span class="sxs-lookup"><span data-stu-id="b2b56-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="b2b56-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="b2b56-192">extendedCost</span></span>|<span data-ttu-id="b2b56-193">decimal</span><span class="sxs-lookup"><span data-stu-id="b2b56-193">decimal</span></span>|<span data-ttu-id="b2b56-194">Cobrança estimada com base na quantidade consumida e no custo estendido</span><span class="sxs-lookup"><span data-stu-id="b2b56-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="b2b56-195">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b2b56-195">See also</span></span>

* [<span data-ttu-id="b2b56-196">API dos períodos de cobrança</span><span class="sxs-lookup"><span data-stu-id="b2b56-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="b2b56-197">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="b2b56-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="b2b56-198">API de saldo e resumo</span><span class="sxs-lookup"><span data-stu-id="b2b56-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="b2b56-199">API da folha de preço</span><span class="sxs-lookup"><span data-stu-id="b2b56-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)