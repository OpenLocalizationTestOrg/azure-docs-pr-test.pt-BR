---
title: "APIs Enterprise de cobrança do Azure – saldo e resumo | Microsoft Docs"
description: "Aprenda sobre as APIs RateCard e de Uso de Cobrança do Azure, que são usadas para fornecer informações sobre o consumo de recursos e as tendências do Azure."
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="0b889-103">APIs de Relatórios para clientes Enterprise – Saldo e Resumo</span><span class="sxs-lookup"><span data-stu-id="0b889-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="0b889-104">A API Saldo e Resumo oferece um resumo mensal de informações sobre saldos, novas compras, encargos de serviço do Azure Marketplace, ajustes e encargos de excedente.</span><span class="sxs-lookup"><span data-stu-id="0b889-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="0b889-105">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0b889-105">Request</span></span> 
<span data-ttu-id="0b889-106">As propriedades de cabeçalho comuns que precisam ser adicionadas são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="0b889-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="0b889-107">Se um período de cobrança não for especificado, os dados do período de cobrança atual serão retornados.</span><span class="sxs-lookup"><span data-stu-id="0b889-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="0b889-108">Método</span><span class="sxs-lookup"><span data-stu-id="0b889-108">Method</span></span> | <span data-ttu-id="0b889-109">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="0b889-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="0b889-110">GET</span><span class="sxs-lookup"><span data-stu-id="0b889-110">GET</span></span>| <span data-ttu-id="0b889-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="0b889-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="0b889-112">GET</span><span class="sxs-lookup"><span data-stu-id="0b889-112">GET</span></span>| <span data-ttu-id="0b889-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="0b889-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="0b889-114">Para usar a versão de visualização da API, substitua a v2 pela v1 na URL anterior.</span><span class="sxs-lookup"><span data-stu-id="0b889-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="0b889-115">Resposta</span><span class="sxs-lookup"><span data-stu-id="0b889-115">Response</span></span>

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


<span data-ttu-id="0b889-116">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="0b889-116">**Response property definitions**</span></span>

|<span data-ttu-id="0b889-117">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="0b889-117">Property Name</span></span>| <span data-ttu-id="0b889-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b889-118">Type</span></span>| <span data-ttu-id="0b889-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b889-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="0b889-120">ID</span><span class="sxs-lookup"><span data-stu-id="0b889-120">id</span></span>|<span data-ttu-id="0b889-121">string</span><span class="sxs-lookup"><span data-stu-id="0b889-121">string</span></span>|<span data-ttu-id="0b889-122">A ID exclusiva de um determinado período de cobrança e registro</span><span class="sxs-lookup"><span data-stu-id="0b889-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="0b889-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="0b889-123">billingPeriodId</span></span>|<span data-ttu-id="0b889-124">string</span><span class="sxs-lookup"><span data-stu-id="0b889-124">string</span></span> |<span data-ttu-id="0b889-125">A ID do período de cobrança</span><span class="sxs-lookup"><span data-stu-id="0b889-125">The billing period Id</span></span>|
|<span data-ttu-id="0b889-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="0b889-126">currencyCode</span></span>|<span data-ttu-id="0b889-127">string</span><span class="sxs-lookup"><span data-stu-id="0b889-127">string</span></span> |<span data-ttu-id="0b889-128">O código da moeda</span><span class="sxs-lookup"><span data-stu-id="0b889-128">The currency code</span></span>|
|<span data-ttu-id="0b889-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="0b889-129">beginningBalance</span></span>|<span data-ttu-id="0b889-130">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-130">decimal</span></span>| <span data-ttu-id="0b889-131">O saldo inicial para o período de cobrança</span><span class="sxs-lookup"><span data-stu-id="0b889-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="0b889-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="0b889-132">endingBalance</span></span>|<span data-ttu-id="0b889-133">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-133">decimal</span></span>| <span data-ttu-id="0b889-134">O saldo final do período de cobrança (para períodos abertos ele será atualizado diariamente)</span><span class="sxs-lookup"><span data-stu-id="0b889-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="0b889-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="0b889-135">newPurchases</span></span>|<span data-ttu-id="0b889-136">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-136">decimal</span></span>| <span data-ttu-id="0b889-137">Valor total da nova compra</span><span class="sxs-lookup"><span data-stu-id="0b889-137">Total new purchase amount</span></span>|
|<span data-ttu-id="0b889-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="0b889-138">adjustments</span></span>|<span data-ttu-id="0b889-139">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-139">decimal</span></span>| <span data-ttu-id="0b889-140">Valor total do ajuste</span><span class="sxs-lookup"><span data-stu-id="0b889-140">Total adjustment amount</span></span>|
|<span data-ttu-id="0b889-141">utilized</span><span class="sxs-lookup"><span data-stu-id="0b889-141">utilized</span></span>|<span data-ttu-id="0b889-142">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-142">decimal</span></span>| <span data-ttu-id="0b889-143">Uso total do compromisso</span><span class="sxs-lookup"><span data-stu-id="0b889-143">Total Commitment usage</span></span>|
|<span data-ttu-id="0b889-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="0b889-144">serviceOverage</span></span>|<span data-ttu-id="0b889-145">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-145">decimal</span></span>| <span data-ttu-id="0b889-146">Excedente dos serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="0b889-146">Overage for Azure services</span></span>|
|<span data-ttu-id="0b889-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="0b889-147">chargesBilledSeparately</span></span>|<span data-ttu-id="0b889-148">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-148">decimal</span></span>| <span data-ttu-id="0b889-149">Encargos cobrados separadamente</span><span class="sxs-lookup"><span data-stu-id="0b889-149">Charges Billed separately</span></span>|
|<span data-ttu-id="0b889-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="0b889-150">totalOverage</span></span>|<span data-ttu-id="0b889-151">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-151">decimal</span></span>| <span data-ttu-id="0b889-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="0b889-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="0b889-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="0b889-153">totalUsage</span></span>|<span data-ttu-id="0b889-154">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-154">decimal</span></span>| <span data-ttu-id="0b889-155">Compromisso do serviço do Azure + excedente total</span><span class="sxs-lookup"><span data-stu-id="0b889-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="0b889-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="0b889-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="0b889-157">decimal</span><span class="sxs-lookup"><span data-stu-id="0b889-157">decimal</span></span>| <span data-ttu-id="0b889-158">Total de encargos do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="0b889-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="0b889-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="0b889-159">newPurchasesDetails</span></span>|<span data-ttu-id="0b889-160">Matriz de cadeias de caracteres JSON de pares de nome e valor</span><span class="sxs-lookup"><span data-stu-id="0b889-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="0b889-161">Lista de novas compras</span><span class="sxs-lookup"><span data-stu-id="0b889-161">List of new purchases</span></span>|
|<span data-ttu-id="0b889-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="0b889-162">adjustmentDetails</span></span>|<span data-ttu-id="0b889-163">Matriz de cadeias de caracteres JSON de pares de nome e valor</span><span class="sxs-lookup"><span data-stu-id="0b889-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="0b889-164">Lista de ajustes (crédito de promoção, crédito SIE etc.)</span><span class="sxs-lookup"><span data-stu-id="0b889-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="0b889-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="0b889-165">See also</span></span>

* [<span data-ttu-id="0b889-166">API dos períodos de cobrança</span><span class="sxs-lookup"><span data-stu-id="0b889-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="0b889-167">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="0b889-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="0b889-168">API do custo de armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="0b889-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="0b889-169">API da folha de preço</span><span class="sxs-lookup"><span data-stu-id="0b889-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)