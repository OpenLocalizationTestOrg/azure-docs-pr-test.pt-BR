---
title: "aaaAzure cobrança Enterprise APIs - saldo e resumo | Microsoft Docs"
description: "Saiba mais sobre o uso de cobrança do Azure e APIs RateCard, que são insights tooprovide usados para consumo de recursos do Azure e tendências."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="b316e-103">APIs de Relatórios para clientes Enterprise – Saldo e Resumo</span><span class="sxs-lookup"><span data-stu-id="b316e-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="b316e-104">Olá equilíbrio e a API de resumo oferece um resumo mensal de informações sobre saldos, novas aquisições, tarifas do serviço Azure Marketplace, ajustes e encargos de excedentes.</span><span class="sxs-lookup"><span data-stu-id="b316e-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="b316e-105">Solicitação</span><span class="sxs-lookup"><span data-stu-id="b316e-105">Request</span></span> 
<span data-ttu-id="b316e-106">Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="b316e-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="b316e-107">Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados.</span><span class="sxs-lookup"><span data-stu-id="b316e-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="b316e-108">Método</span><span class="sxs-lookup"><span data-stu-id="b316e-108">Method</span></span> | <span data-ttu-id="b316e-109">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="b316e-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="b316e-110">GET</span><span class="sxs-lookup"><span data-stu-id="b316e-110">GET</span></span>| <span data-ttu-id="b316e-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="b316e-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="b316e-112">GET</span><span class="sxs-lookup"><span data-stu-id="b316e-112">GET</span></span>| <span data-ttu-id="b316e-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="b316e-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="b316e-114">versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.</span><span class="sxs-lookup"><span data-stu-id="b316e-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="b316e-115">Resposta</span><span class="sxs-lookup"><span data-stu-id="b316e-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="b316e-116">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="b316e-116">**Response property definitions**</span></span>

|<span data-ttu-id="b316e-117">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="b316e-117">Property Name</span></span>| <span data-ttu-id="b316e-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="b316e-118">Type</span></span>| <span data-ttu-id="b316e-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="b316e-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="b316e-120">ID</span><span class="sxs-lookup"><span data-stu-id="b316e-120">id</span></span>|<span data-ttu-id="b316e-121">string</span><span class="sxs-lookup"><span data-stu-id="b316e-121">string</span></span>|<span data-ttu-id="b316e-122">Olá Id exclusiva para um determinado período de cobrança e registro</span><span class="sxs-lookup"><span data-stu-id="b316e-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="b316e-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="b316e-123">billingPeriodId</span></span>|<span data-ttu-id="b316e-124">string</span><span class="sxs-lookup"><span data-stu-id="b316e-124">string</span></span> |<span data-ttu-id="b316e-125">Olá Id do período de cobrança</span><span class="sxs-lookup"><span data-stu-id="b316e-125">hello billing period Id</span></span>|
|<span data-ttu-id="b316e-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="b316e-126">currencyCode</span></span>|<span data-ttu-id="b316e-127">string</span><span class="sxs-lookup"><span data-stu-id="b316e-127">string</span></span> |<span data-ttu-id="b316e-128">código de moeda Olá</span><span class="sxs-lookup"><span data-stu-id="b316e-128">hello currency code</span></span>|
|<span data-ttu-id="b316e-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="b316e-129">beginningBalance</span></span>|<span data-ttu-id="b316e-130">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-130">decimal</span></span>| <span data-ttu-id="b316e-131">saldo inicial de Olá Olá período de faturamento</span><span class="sxs-lookup"><span data-stu-id="b316e-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="b316e-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="b316e-132">endingBalance</span></span>|<span data-ttu-id="b316e-133">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-133">decimal</span></span>| <span data-ttu-id="b316e-134">Olá saldo final para o período de cobrança hello (para períodos abertos que isso será atualizado diariamente)</span><span class="sxs-lookup"><span data-stu-id="b316e-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="b316e-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="b316e-135">newPurchases</span></span>|<span data-ttu-id="b316e-136">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-136">decimal</span></span>| <span data-ttu-id="b316e-137">Valor total da nova compra</span><span class="sxs-lookup"><span data-stu-id="b316e-137">Total new purchase amount</span></span>|
|<span data-ttu-id="b316e-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="b316e-138">adjustments</span></span>|<span data-ttu-id="b316e-139">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-139">decimal</span></span>| <span data-ttu-id="b316e-140">Valor total do ajuste</span><span class="sxs-lookup"><span data-stu-id="b316e-140">Total adjustment amount</span></span>|
|<span data-ttu-id="b316e-141">utilized</span><span class="sxs-lookup"><span data-stu-id="b316e-141">utilized</span></span>|<span data-ttu-id="b316e-142">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-142">decimal</span></span>| <span data-ttu-id="b316e-143">Uso total do compromisso</span><span class="sxs-lookup"><span data-stu-id="b316e-143">Total Commitment usage</span></span>|
|<span data-ttu-id="b316e-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="b316e-144">serviceOverage</span></span>|<span data-ttu-id="b316e-145">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-145">decimal</span></span>| <span data-ttu-id="b316e-146">Excedente dos serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="b316e-146">Overage for Azure services</span></span>|
|<span data-ttu-id="b316e-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="b316e-147">chargesBilledSeparately</span></span>|<span data-ttu-id="b316e-148">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-148">decimal</span></span>| <span data-ttu-id="b316e-149">Encargos cobrados separadamente</span><span class="sxs-lookup"><span data-stu-id="b316e-149">Charges Billed separately</span></span>|
|<span data-ttu-id="b316e-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="b316e-150">totalOverage</span></span>|<span data-ttu-id="b316e-151">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-151">decimal</span></span>| <span data-ttu-id="b316e-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="b316e-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="b316e-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="b316e-153">totalUsage</span></span>|<span data-ttu-id="b316e-154">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-154">decimal</span></span>| <span data-ttu-id="b316e-155">Compromisso do serviço do Azure + excedente total</span><span class="sxs-lookup"><span data-stu-id="b316e-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="b316e-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="b316e-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="b316e-157">decimal</span><span class="sxs-lookup"><span data-stu-id="b316e-157">decimal</span></span>| <span data-ttu-id="b316e-158">Total de encargos do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="b316e-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="b316e-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="b316e-159">newPurchasesDetails</span></span>|<span data-ttu-id="b316e-160">Matriz de cadeias de caracteres JSON de pares de nome e valor</span><span class="sxs-lookup"><span data-stu-id="b316e-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="b316e-161">Lista de novas compras</span><span class="sxs-lookup"><span data-stu-id="b316e-161">List of new purchases</span></span>|
|<span data-ttu-id="b316e-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="b316e-162">adjustmentDetails</span></span>|<span data-ttu-id="b316e-163">Matriz de cadeias de caracteres JSON de pares de nome e valor</span><span class="sxs-lookup"><span data-stu-id="b316e-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="b316e-164">Lista de ajustes (crédito de promoção, crédito SIE etc.)</span><span class="sxs-lookup"><span data-stu-id="b316e-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="b316e-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b316e-165">See also</span></span>

* [<span data-ttu-id="b316e-166">API dos períodos de cobrança</span><span class="sxs-lookup"><span data-stu-id="b316e-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="b316e-167">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="b316e-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="b316e-168">API do custo de armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="b316e-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="b316e-169">API da folha de preço</span><span class="sxs-lookup"><span data-stu-id="b316e-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)