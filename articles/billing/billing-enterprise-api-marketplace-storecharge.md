---
title: "APIs Enterprise de cobrança do Azure – cobranças do Marketplace| Microsoft Docs"
description: "Saiba mais sobre as APIs de Relatório que permitem a clientes Enterprise do Azure efetuar pull dos dados de consumo de modo programático."
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
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="68f99-103">APIs de Relatórios para clientes Enterprise – Custos de Armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="68f99-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="68f99-104">A API Encargo de Repositório do Marketplace retorna o detalhamento dos encargos do marketplace com base no uso por dia para o Período de Cobrança especificado ou as datas de início e término (taxas avulsas não estão incluídas).</span><span class="sxs-lookup"><span data-stu-id="68f99-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="68f99-105">Solicitação</span><span class="sxs-lookup"><span data-stu-id="68f99-105">Request</span></span> 
<span data-ttu-id="68f99-106">As propriedades de cabeçalho comuns que precisam ser adicionadas são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="68f99-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="68f99-107">Se um período de cobrança não for especificado, os dados do período de cobrança atual serão retornados.</span><span class="sxs-lookup"><span data-stu-id="68f99-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="68f99-108">Os intervalos de tempo personalizados podem ser especificados com os parâmetros das datas de início e término no formato aaaa-MM-dd, o intervalo de tempo compatível máximo é de 36 meses.</span><span class="sxs-lookup"><span data-stu-id="68f99-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="68f99-109">Método</span><span class="sxs-lookup"><span data-stu-id="68f99-109">Method</span></span> | <span data-ttu-id="68f99-110">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="68f99-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="68f99-111">GET</span><span class="sxs-lookup"><span data-stu-id="68f99-111">GET</span></span>|<span data-ttu-id="68f99-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="68f99-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="68f99-113">GET</span><span class="sxs-lookup"><span data-stu-id="68f99-113">GET</span></span>|<span data-ttu-id="68f99-114">https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/billingPeriods/{períododeCobrança}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="68f99-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="68f99-115">GET</span><span class="sxs-lookup"><span data-stu-id="68f99-115">GET</span></span>|<span data-ttu-id="68f99-116">https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="68f99-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="68f99-117">Para usar a versão de visualização da API, substitua a v2 pela v1 na URL anterior.</span><span class="sxs-lookup"><span data-stu-id="68f99-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="68f99-118">Resposta</span><span class="sxs-lookup"><span data-stu-id="68f99-118">Response</span></span>
 
    
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
    

<span data-ttu-id="68f99-119">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="68f99-119">**Response property definitions**</span></span>

|<span data-ttu-id="68f99-120">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="68f99-120">Property Name</span></span>| <span data-ttu-id="68f99-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="68f99-121">Type</span></span>| <span data-ttu-id="68f99-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="68f99-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="68f99-123">ID</span><span class="sxs-lookup"><span data-stu-id="68f99-123">id</span></span>|<span data-ttu-id="68f99-124">string</span><span class="sxs-lookup"><span data-stu-id="68f99-124">string</span></span>|<span data-ttu-id="68f99-125">ID exclusiva para o item de cobrança do marketplace</span><span class="sxs-lookup"><span data-stu-id="68f99-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="68f99-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="68f99-126">subscriptionGuid</span></span>|<span data-ttu-id="68f99-127">Guid</span><span class="sxs-lookup"><span data-stu-id="68f99-127">Guid</span></span>|<span data-ttu-id="68f99-128">A Guid da assinatura</span><span class="sxs-lookup"><span data-stu-id="68f99-128">The Subscription Guid</span></span>|
|<span data-ttu-id="68f99-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="68f99-129">subscriptionName</span></span>|<span data-ttu-id="68f99-130">string</span><span class="sxs-lookup"><span data-stu-id="68f99-130">string</span></span>|<span data-ttu-id="68f99-131">O nome da assinatura</span><span class="sxs-lookup"><span data-stu-id="68f99-131">The Subscription Name</span></span>|
|<span data-ttu-id="68f99-132">meterId</span><span class="sxs-lookup"><span data-stu-id="68f99-132">meterId</span></span>|<span data-ttu-id="68f99-133">string</span><span class="sxs-lookup"><span data-stu-id="68f99-133">string</span></span>|<span data-ttu-id="68f99-134">ID para o medidor emitido</span><span class="sxs-lookup"><span data-stu-id="68f99-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="68f99-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="68f99-135">usageStartDate</span></span>|<span data-ttu-id="68f99-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="68f99-136">DateTime</span></span>|<span data-ttu-id="68f99-137">Hora de início para o registro de uso</span><span class="sxs-lookup"><span data-stu-id="68f99-137">Start time for the usage record</span></span>|
|<span data-ttu-id="68f99-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="68f99-138">usageEndDate</span></span>|<span data-ttu-id="68f99-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="68f99-139">DateTime</span></span>|<span data-ttu-id="68f99-140">Hora de término para o registro de uso</span><span class="sxs-lookup"><span data-stu-id="68f99-140">End time for the usage record</span></span>|
|<span data-ttu-id="68f99-141">offerName</span><span class="sxs-lookup"><span data-stu-id="68f99-141">offerName</span></span>|<span data-ttu-id="68f99-142">string</span><span class="sxs-lookup"><span data-stu-id="68f99-142">string</span></span>|<span data-ttu-id="68f99-143">O nome da oferta</span><span class="sxs-lookup"><span data-stu-id="68f99-143">The Offer name</span></span>|
|<span data-ttu-id="68f99-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="68f99-144">resourceGroup</span></span>|<span data-ttu-id="68f99-145">string</span><span class="sxs-lookup"><span data-stu-id="68f99-145">string</span></span>|<span data-ttu-id="68f99-146">O grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="68f99-146">The resource Group</span></span>|
|<span data-ttu-id="68f99-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="68f99-147">instanceId</span></span>|<span data-ttu-id="68f99-148">string</span><span class="sxs-lookup"><span data-stu-id="68f99-148">string</span></span>|<span data-ttu-id="68f99-149">ID da instância</span><span class="sxs-lookup"><span data-stu-id="68f99-149">Instance Id</span></span>|
|<span data-ttu-id="68f99-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="68f99-150">additionalInfo</span></span>|<span data-ttu-id="68f99-151">string</span><span class="sxs-lookup"><span data-stu-id="68f99-151">string</span></span>|<span data-ttu-id="68f99-152">Cadeia de caracteres JSON de informações adicionais</span><span class="sxs-lookup"><span data-stu-id="68f99-152">Additional info JSON string</span></span>|
|<span data-ttu-id="68f99-153">marcas</span><span class="sxs-lookup"><span data-stu-id="68f99-153">tags</span></span>|<span data-ttu-id="68f99-154">string</span><span class="sxs-lookup"><span data-stu-id="68f99-154">string</span></span>|<span data-ttu-id="68f99-155">Cadeia de caracteres JSON da marca</span><span class="sxs-lookup"><span data-stu-id="68f99-155">Tag JSON string</span></span>|
|<span data-ttu-id="68f99-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="68f99-156">orderNumber</span></span>|<span data-ttu-id="68f99-157">string</span><span class="sxs-lookup"><span data-stu-id="68f99-157">string</span></span>|<span data-ttu-id="68f99-158">O número da ordem</span><span class="sxs-lookup"><span data-stu-id="68f99-158">The order number</span></span>|
|<span data-ttu-id="68f99-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="68f99-159">unitOfMeasure</span></span>|<span data-ttu-id="68f99-160">string</span><span class="sxs-lookup"><span data-stu-id="68f99-160">string</span></span>|<span data-ttu-id="68f99-161">Unidade de medida para o medidor</span><span class="sxs-lookup"><span data-stu-id="68f99-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="68f99-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="68f99-162">costCenter</span></span>|<span data-ttu-id="68f99-163">string</span><span class="sxs-lookup"><span data-stu-id="68f99-163">string</span></span>|<span data-ttu-id="68f99-164">O centro de custo</span><span class="sxs-lookup"><span data-stu-id="68f99-164">The cost center</span></span>|
|<span data-ttu-id="68f99-165">accountId</span><span class="sxs-lookup"><span data-stu-id="68f99-165">accountId</span></span>|<span data-ttu-id="68f99-166">int</span><span class="sxs-lookup"><span data-stu-id="68f99-166">int</span></span>|<span data-ttu-id="68f99-167">A ID da conta</span><span class="sxs-lookup"><span data-stu-id="68f99-167">The account Id</span></span>|
|<span data-ttu-id="68f99-168">accountName</span><span class="sxs-lookup"><span data-stu-id="68f99-168">accountName</span></span>|<span data-ttu-id="68f99-169">string</span><span class="sxs-lookup"><span data-stu-id="68f99-169">string</span></span> |<span data-ttu-id="68f99-170">O nome da conta</span><span class="sxs-lookup"><span data-stu-id="68f99-170">The Account Name</span></span>|
|<span data-ttu-id="68f99-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="68f99-171">accountOwnerId</span></span>|<span data-ttu-id="68f99-172">string</span><span class="sxs-lookup"><span data-stu-id="68f99-172">string</span></span>|<span data-ttu-id="68f99-173">A ID do proprietário da conta</span><span class="sxs-lookup"><span data-stu-id="68f99-173">The Account Owner Id</span></span>|
|<span data-ttu-id="68f99-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="68f99-174">departmentId</span></span>|<span data-ttu-id="68f99-175">int</span><span class="sxs-lookup"><span data-stu-id="68f99-175">int</span></span>|<span data-ttu-id="68f99-176">A ID do departamento</span><span class="sxs-lookup"><span data-stu-id="68f99-176">The department Id</span></span>|
|<span data-ttu-id="68f99-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="68f99-177">departmentName</span></span>|<span data-ttu-id="68f99-178">string</span><span class="sxs-lookup"><span data-stu-id="68f99-178">string</span></span>|<span data-ttu-id="68f99-179">O nome do departamento</span><span class="sxs-lookup"><span data-stu-id="68f99-179">The department name</span></span>|
|<span data-ttu-id="68f99-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="68f99-180">publisherName</span></span>|<span data-ttu-id="68f99-181">string</span><span class="sxs-lookup"><span data-stu-id="68f99-181">string</span></span>|<span data-ttu-id="68f99-182">O nome do editor</span><span class="sxs-lookup"><span data-stu-id="68f99-182">The publisher name</span></span>|
|<span data-ttu-id="68f99-183">planName</span><span class="sxs-lookup"><span data-stu-id="68f99-183">planName</span></span>|<span data-ttu-id="68f99-184">string</span><span class="sxs-lookup"><span data-stu-id="68f99-184">string</span></span>|<span data-ttu-id="68f99-185">O nome do plano</span><span class="sxs-lookup"><span data-stu-id="68f99-185">The Plan name</span></span>|
|<span data-ttu-id="68f99-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="68f99-186">consumedQuantity</span></span>|<span data-ttu-id="68f99-187">decimal</span><span class="sxs-lookup"><span data-stu-id="68f99-187">decimal</span></span>|<span data-ttu-id="68f99-188">Quantidade consumida durante esse período</span><span class="sxs-lookup"><span data-stu-id="68f99-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="68f99-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="68f99-189">resourceRate</span></span>|<span data-ttu-id="68f99-190">decimal</span><span class="sxs-lookup"><span data-stu-id="68f99-190">decimal</span></span>|<span data-ttu-id="68f99-191">Preço unitário do medidor</span><span class="sxs-lookup"><span data-stu-id="68f99-191">Unit price for the meter</span></span>|
|<span data-ttu-id="68f99-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="68f99-192">extendedCost</span></span>|<span data-ttu-id="68f99-193">decimal</span><span class="sxs-lookup"><span data-stu-id="68f99-193">decimal</span></span>|<span data-ttu-id="68f99-194">Cobrança estimada com base na quantidade consumida e no custo estendido</span><span class="sxs-lookup"><span data-stu-id="68f99-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="68f99-195">Consulte também</span><span class="sxs-lookup"><span data-stu-id="68f99-195">See also</span></span>

* [<span data-ttu-id="68f99-196">API dos períodos de cobrança</span><span class="sxs-lookup"><span data-stu-id="68f99-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="68f99-197">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="68f99-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="68f99-198">API de saldo e resumo</span><span class="sxs-lookup"><span data-stu-id="68f99-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="68f99-199">API da folha de preço</span><span class="sxs-lookup"><span data-stu-id="68f99-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)