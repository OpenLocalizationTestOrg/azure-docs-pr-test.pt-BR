---
title: "aaaAzure cobrança Enterprise APIs - períodos de cobrança | Microsoft Docs"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="c6e16-103">APIs de Relatórios para clientes Enterprise – Períodos de Cobrança</span><span class="sxs-lookup"><span data-stu-id="c6e16-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="c6e16-104">Olá cobrança períodos API retorna uma lista de cobrança períodos com dados de consumo para Olá especificado registro em ordem cronológica inversa.</span><span class="sxs-lookup"><span data-stu-id="c6e16-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="c6e16-105">Cada período contém uma propriedade apontando toohello rota de API para Olá quatro conjuntos de dados - BalanceSummary, UsageDetails, Marktplace encargos e PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="c6e16-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="c6e16-106">Se o período de saudação não tiver dados, propriedade correspondente Olá é nula.</span><span class="sxs-lookup"><span data-stu-id="c6e16-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="c6e16-107">Solicitação</span><span class="sxs-lookup"><span data-stu-id="c6e16-107">Request</span></span> 
<span data-ttu-id="c6e16-108">Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="c6e16-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="c6e16-109">Método</span><span class="sxs-lookup"><span data-stu-id="c6e16-109">Method</span></span> | <span data-ttu-id="c6e16-110">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="c6e16-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="c6e16-111">GET</span><span class="sxs-lookup"><span data-stu-id="c6e16-111">GET</span></span>| <span data-ttu-id="c6e16-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="c6e16-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="c6e16-113">versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.</span><span class="sxs-lookup"><span data-stu-id="c6e16-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="c6e16-114">Resposta</span><span class="sxs-lookup"><span data-stu-id="c6e16-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="c6e16-115">**Definições da propriedade de resposta**</span><span class="sxs-lookup"><span data-stu-id="c6e16-115">**Response property definitions**</span></span>

|<span data-ttu-id="c6e16-116">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="c6e16-116">Property Name</span></span>| <span data-ttu-id="c6e16-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="c6e16-117">Type</span></span>| <span data-ttu-id="c6e16-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="c6e16-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="c6e16-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="c6e16-119">billingPeriodId</span></span>| <span data-ttu-id="c6e16-120">string</span><span class="sxs-lookup"><span data-stu-id="c6e16-120">string</span></span>| <span data-ttu-id="c6e16-121">Olá Id exclusiva que representa um determinado período de cobrança</span><span class="sxs-lookup"><span data-stu-id="c6e16-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="c6e16-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="c6e16-122">billingStart</span></span>| <span data-ttu-id="c6e16-123">datetime</span><span class="sxs-lookup"><span data-stu-id="c6e16-123">datetime</span></span>| <span data-ttu-id="c6e16-124">Cadeia de caracteres ISO 8601 que representa a data de início do período de saudação</span><span class="sxs-lookup"><span data-stu-id="c6e16-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="c6e16-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="c6e16-125">billingEnd</span></span>| <span data-ttu-id="c6e16-126">datetime</span><span class="sxs-lookup"><span data-stu-id="c6e16-126">datetime</span></span>| <span data-ttu-id="c6e16-127">Cadeia de caracteres ISO 8601 que representa a data de término do período de saudação</span><span class="sxs-lookup"><span data-stu-id="c6e16-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="c6e16-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="c6e16-128">balanceSummary</span></span>| <span data-ttu-id="c6e16-129">string</span><span class="sxs-lookup"><span data-stu-id="c6e16-129">string</span></span>| <span data-ttu-id="c6e16-130">caminho de URL de saudação que encaminha os dados de resumo de saldo de toohello para esse período</span><span class="sxs-lookup"><span data-stu-id="c6e16-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="c6e16-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="c6e16-131">usageDetails</span></span>| <span data-ttu-id="c6e16-132">string</span><span class="sxs-lookup"><span data-stu-id="c6e16-132">string</span></span>| <span data-ttu-id="c6e16-133">caminho de URL de saudação que roteia toohello dados de detalhes de uso para esse período</span><span class="sxs-lookup"><span data-stu-id="c6e16-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="c6e16-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="c6e16-134">marketplaceCharges</span></span>| <span data-ttu-id="c6e16-135">string</span><span class="sxs-lookup"><span data-stu-id="c6e16-135">string</span></span>| <span data-ttu-id="c6e16-136">caminho da URL Olá que encaminha dados de encargos do Marketplace toohello para esse período</span><span class="sxs-lookup"><span data-stu-id="c6e16-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="c6e16-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="c6e16-137">priceSheet</span></span>| <span data-ttu-id="c6e16-138">string</span><span class="sxs-lookup"><span data-stu-id="c6e16-138">string</span></span>| <span data-ttu-id="c6e16-139">caminho de URL de saudação que roteia toohello PriceSheet dados para esse período</span><span class="sxs-lookup"><span data-stu-id="c6e16-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="c6e16-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c6e16-140">See also</span></span>

* [<span data-ttu-id="c6e16-141">API de saldo e resumo</span><span class="sxs-lookup"><span data-stu-id="c6e16-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="c6e16-142">API de detalhes do uso</span><span class="sxs-lookup"><span data-stu-id="c6e16-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="c6e16-143">API do custo de armazenamento do Marketplace</span><span class="sxs-lookup"><span data-stu-id="c6e16-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="c6e16-144">API da folha de preço</span><span class="sxs-lookup"><span data-stu-id="c6e16-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)