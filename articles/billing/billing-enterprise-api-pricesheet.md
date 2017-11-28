---
title: "aaaAzure cobrança Enterprise APIs - PriceSheet | Microsoft Docs"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="da8d0-103">APIs de Relatórios para clientes Enterprise – PriceSheet</span><span class="sxs-lookup"><span data-stu-id="da8d0-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="da8d0-104">Olá API de folha de preço fornece taxa aplicável Olá para cada medidor para Olá dado registro e o período de cobrança.</span><span class="sxs-lookup"><span data-stu-id="da8d0-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="da8d0-105">Solicitação</span><span class="sxs-lookup"><span data-stu-id="da8d0-105">Request</span></span>
<span data-ttu-id="da8d0-106">Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="da8d0-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="da8d0-107">Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados.</span><span class="sxs-lookup"><span data-stu-id="da8d0-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="da8d0-108">Método</span><span class="sxs-lookup"><span data-stu-id="da8d0-108">Method</span></span> | <span data-ttu-id="da8d0-109">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="da8d0-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="da8d0-110">GET</span><span class="sxs-lookup"><span data-stu-id="da8d0-110">GET</span></span>|<span data-ttu-id="da8d0-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="da8d0-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="da8d0-112">GET</span><span class="sxs-lookup"><span data-stu-id="da8d0-112">GET</span></span>|<span data-ttu-id="da8d0-113">https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/billingPeriods/{períododeCobrança}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="da8d0-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="da8d0-114">versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.</span><span class="sxs-lookup"><span data-stu-id="da8d0-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="da8d0-115">Resposta</span><span class="sxs-lookup"><span data-stu-id="da8d0-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="da8d0-116">Se você estiver usando Olá API da visualização, o campo meterId não está disponível.</span><span class="sxs-lookup"><span data-stu-id="da8d0-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="da8d0-117">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="da8d0-117">**Response property definitions**</span></span>

|<span data-ttu-id="da8d0-118">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="da8d0-118">Property Name</span></span>| <span data-ttu-id="da8d0-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="da8d0-119">Type</span></span>| <span data-ttu-id="da8d0-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="da8d0-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="da8d0-121">ID</span><span class="sxs-lookup"><span data-stu-id="da8d0-121">id</span></span>| <span data-ttu-id="da8d0-122">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-122">string</span></span>| <span data-ttu-id="da8d0-123">Olá Id exclusiva que representa um item específico do PriceSheet (medidor por período de cobrança)</span><span class="sxs-lookup"><span data-stu-id="da8d0-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="da8d0-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="da8d0-124">billingPeriodId</span></span>| <span data-ttu-id="da8d0-125">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-125">string</span></span>| <span data-ttu-id="da8d0-126">Olá Id exclusiva que representa um determinado período de cobrança</span><span class="sxs-lookup"><span data-stu-id="da8d0-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="da8d0-127">meterId</span><span class="sxs-lookup"><span data-stu-id="da8d0-127">meterId</span></span>| <span data-ttu-id="da8d0-128">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-128">string</span></span>| <span data-ttu-id="da8d0-129">Identificador Olá medidor hello.</span><span class="sxs-lookup"><span data-stu-id="da8d0-129">hello identifier for hello meter.</span></span> <span data-ttu-id="da8d0-130">Ele pode ser mapeado toohello meterId de uso.</span><span class="sxs-lookup"><span data-stu-id="da8d0-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="da8d0-131">meterName</span><span class="sxs-lookup"><span data-stu-id="da8d0-131">meterName</span></span>| <span data-ttu-id="da8d0-132">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-132">string</span></span>| <span data-ttu-id="da8d0-133">nome do medidor Olá</span><span class="sxs-lookup"><span data-stu-id="da8d0-133">hello meter name</span></span>|
|<span data-ttu-id="da8d0-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="da8d0-134">unitOfMeasure</span></span>| <span data-ttu-id="da8d0-135">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-135">string</span></span>| <span data-ttu-id="da8d0-136">saudação de unidade de medida para medir o serviço Olá</span><span class="sxs-lookup"><span data-stu-id="da8d0-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="da8d0-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="da8d0-137">includedQuantity</span></span>| <span data-ttu-id="da8d0-138">decimal</span><span class="sxs-lookup"><span data-stu-id="da8d0-138">decimal</span></span>| <span data-ttu-id="da8d0-139">Quantidade incluída</span><span class="sxs-lookup"><span data-stu-id="da8d0-139">Quantity that is included</span></span> |
|<span data-ttu-id="da8d0-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="da8d0-140">partNumber</span></span>| <span data-ttu-id="da8d0-141">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-141">string</span></span>| <span data-ttu-id="da8d0-142">número de peça Olá associado Olá medidor</span><span class="sxs-lookup"><span data-stu-id="da8d0-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="da8d0-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="da8d0-143">unitPrice</span></span>| <span data-ttu-id="da8d0-144">decimal</span><span class="sxs-lookup"><span data-stu-id="da8d0-144">decimal</span></span>| <span data-ttu-id="da8d0-145">preço unitário Olá medidor Olá</span><span class="sxs-lookup"><span data-stu-id="da8d0-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="da8d0-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="da8d0-146">currencyCode</span></span>| <span data-ttu-id="da8d0-147">string</span><span class="sxs-lookup"><span data-stu-id="da8d0-147">string</span></span>| <span data-ttu-id="da8d0-148">código de moeda Olá para unitPrice Olá</span><span class="sxs-lookup"><span data-stu-id="da8d0-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="da8d0-149">Consulte também</span><span class="sxs-lookup"><span data-stu-id="da8d0-149">See also</span></span>

* [<span data-ttu-id="da8d0-150">API dos períodos de cobrança</span><span class="sxs-lookup"><span data-stu-id="da8d0-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="da8d0-151">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="da8d0-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="da8d0-152">API de saldo e resumo</span><span class="sxs-lookup"><span data-stu-id="da8d0-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="da8d0-153">API do custo de armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="da8d0-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
