---
title: "APIs Enterprise de cobrança do Azure – períodos de cobrança | Microsoft Docs"
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="82dd1-103">APIs de Relatórios para clientes Enterprise – Períodos de Cobrança</span><span class="sxs-lookup"><span data-stu-id="82dd1-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="82dd1-104">A API Períodos de Cobrança retorna uma lista de períodos de cobrança que têm dados de consumo para o Registro especificado em ordem cronológica inversa.</span><span class="sxs-lookup"><span data-stu-id="82dd1-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="82dd1-105">Cada período contém uma propriedade que aponta para a rota da API dos quatro conjuntos de dados: BalanceSummary, UsageDetails, Encargos do Marketplace e PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="82dd1-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="82dd1-106">Se o período não tiver dados, a propriedade correspondente será nula.</span><span class="sxs-lookup"><span data-stu-id="82dd1-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="82dd1-107">Solicitação</span><span class="sxs-lookup"><span data-stu-id="82dd1-107">Request</span></span> 
<span data-ttu-id="82dd1-108">As propriedades de cabeçalho comuns que precisam ser adicionadas são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="82dd1-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="82dd1-109">Método</span><span class="sxs-lookup"><span data-stu-id="82dd1-109">Method</span></span> | <span data-ttu-id="82dd1-110">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="82dd1-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="82dd1-111">GET</span><span class="sxs-lookup"><span data-stu-id="82dd1-111">GET</span></span>| <span data-ttu-id="82dd1-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="82dd1-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="82dd1-113">Para usar a versão de visualização da API, substitua a v2 pela v1 na URL anterior.</span><span class="sxs-lookup"><span data-stu-id="82dd1-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="82dd1-114">Resposta</span><span class="sxs-lookup"><span data-stu-id="82dd1-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="82dd1-115">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="82dd1-115">**Response property definitions**</span></span>

|<span data-ttu-id="82dd1-116">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="82dd1-116">Property Name</span></span>| <span data-ttu-id="82dd1-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="82dd1-117">Type</span></span>| <span data-ttu-id="82dd1-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="82dd1-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="82dd1-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="82dd1-119">billingPeriodId</span></span>| <span data-ttu-id="82dd1-120">string</span><span class="sxs-lookup"><span data-stu-id="82dd1-120">string</span></span>| <span data-ttu-id="82dd1-121">A ID exclusiva que representa um determinado período de cobrança</span><span class="sxs-lookup"><span data-stu-id="82dd1-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="82dd1-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="82dd1-122">billingStart</span></span>| <span data-ttu-id="82dd1-123">datetime</span><span class="sxs-lookup"><span data-stu-id="82dd1-123">datetime</span></span>| <span data-ttu-id="82dd1-124">Cadeia de caracteres ISO 8601 que representa a data de início do período</span><span class="sxs-lookup"><span data-stu-id="82dd1-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="82dd1-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="82dd1-125">billingEnd</span></span>| <span data-ttu-id="82dd1-126">datetime</span><span class="sxs-lookup"><span data-stu-id="82dd1-126">datetime</span></span>| <span data-ttu-id="82dd1-127">Cadeia de caracteres ISO 8601 que representa a data de término do período</span><span class="sxs-lookup"><span data-stu-id="82dd1-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="82dd1-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="82dd1-128">balanceSummary</span></span>| <span data-ttu-id="82dd1-129">string</span><span class="sxs-lookup"><span data-stu-id="82dd1-129">string</span></span>| <span data-ttu-id="82dd1-130">O caminho da URL que encaminha para os dados de resumo de saldo para este período</span><span class="sxs-lookup"><span data-stu-id="82dd1-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="82dd1-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="82dd1-131">usageDetails</span></span>| <span data-ttu-id="82dd1-132">string</span><span class="sxs-lookup"><span data-stu-id="82dd1-132">string</span></span>| <span data-ttu-id="82dd1-133">O caminho da URL que encaminha para os dados de detalhes de uso para este período</span><span class="sxs-lookup"><span data-stu-id="82dd1-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="82dd1-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="82dd1-134">marketplaceCharges</span></span>| <span data-ttu-id="82dd1-135">string</span><span class="sxs-lookup"><span data-stu-id="82dd1-135">string</span></span>| <span data-ttu-id="82dd1-136">O caminho da URL que encaminha para os dados de cobranças do Marketplace para este período</span><span class="sxs-lookup"><span data-stu-id="82dd1-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="82dd1-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="82dd1-137">priceSheet</span></span>| <span data-ttu-id="82dd1-138">string</span><span class="sxs-lookup"><span data-stu-id="82dd1-138">string</span></span>| <span data-ttu-id="82dd1-139">O caminho da URL que encaminha para os dados PriceSheet para este período</span><span class="sxs-lookup"><span data-stu-id="82dd1-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="82dd1-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="82dd1-140">See also</span></span>

* [<span data-ttu-id="82dd1-141">API de saldo e resumo</span><span class="sxs-lookup"><span data-stu-id="82dd1-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="82dd1-142">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="82dd1-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="82dd1-143">API do custo de armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="82dd1-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="82dd1-144">API da folha de preço</span><span class="sxs-lookup"><span data-stu-id="82dd1-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)