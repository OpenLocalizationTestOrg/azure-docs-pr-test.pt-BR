---
title: "aaaAzure cobrança Enterprise APIs | Microsoft Docs"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="9315f-103">Visão geral das APIs de Relatórios para clientes Enterprise</span><span class="sxs-lookup"><span data-stu-id="9315f-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="9315f-104">Olá Reporting APIs permitem que o consumo do Azure Enterprise clientes tooprogrammatically pull e dados de cobrança em ferramentas de análise de dados preferencial.</span><span class="sxs-lookup"><span data-stu-id="9315f-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="9315f-105">Habilitando a API toohello de acesso a dados</span><span class="sxs-lookup"><span data-stu-id="9315f-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="9315f-106">**Gerar ou recuperar a chave de API de saudação** - Log toohello Enterprise portal e siga Olá tutorial em Ajuda - APIs de relatórios.</span><span class="sxs-lookup"><span data-stu-id="9315f-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="9315f-107">a primeira seção Olá sob este artigo ajuda explica como toogenerate ou recuperar chave Olá API Olá especificado registro.</span><span class="sxs-lookup"><span data-stu-id="9315f-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="9315f-108">**Passando chaves Olá API** -chave de API de saudação deve toobe passado para cada chamada para autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="9315f-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="9315f-109">propriedade a seguir Hello precisa toobe toohello HTTP cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="9315f-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="9315f-110">Chave de cabeçalho da solicitação</span><span class="sxs-lookup"><span data-stu-id="9315f-110">Request Header Key</span></span> | <span data-ttu-id="9315f-111">Valor</span><span class="sxs-lookup"><span data-stu-id="9315f-111">Value</span></span>|
|-|-|
|<span data-ttu-id="9315f-112">Autorização</span><span class="sxs-lookup"><span data-stu-id="9315f-112">Authorization</span></span>| <span data-ttu-id="9315f-113">Especifique o valor de saudação neste formato: **portador {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="9315f-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="9315f-114">Exemplo: portador e... 09</span><span class="sxs-lookup"><span data-stu-id="9315f-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="9315f-115">APIs de consumo</span><span class="sxs-lookup"><span data-stu-id="9315f-115">Consumption APIs</span></span>
<span data-ttu-id="9315f-116">Há um ponto de extremidade de Swagger [aqui](https://consumption.azure.com/swagger/ui/index) para Olá APIs descritas abaixo do qual deve introspecção fácil de habilitar da API de saudação e cliente toogenerate da capacidade Olá SDKs usando [AutoRest](https://github.com/Azure/AutoRest) ou [ Gerador de código de swagger](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="9315f-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="9315f-117">Os dados a partir de 1º de maio de 2014 estão disponíveis por essa API.</span><span class="sxs-lookup"><span data-stu-id="9315f-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="9315f-118">**Saldo e resumo** - Olá [equilíbrio e a API de resumo](billing-enterprise-api-balance-summary.md) oferece um resumo mensal de informações sobre saldos, novas aquisições, taxas de serviço do Azure Marketplace, ajustes e encargos excedentes.</span><span class="sxs-lookup"><span data-stu-id="9315f-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="9315f-119">**Detalhes de uso** - Olá [API de detalhes de uso](billing-enterprise-api-usage-detail.md) oferece um detalhamento diário das quantidades consumidas e encargos estimados por um registro.</span><span class="sxs-lookup"><span data-stu-id="9315f-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="9315f-120">resultado de saudação também inclui informações sobre instâncias, medidores e departamentos.</span><span class="sxs-lookup"><span data-stu-id="9315f-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="9315f-121">Olá API pode ser consultada por período de cobrança ou de início especificado e a data de término.</span><span class="sxs-lookup"><span data-stu-id="9315f-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="9315f-122">**Custos de armazenamento do Marketplace** - Olá [API de custos de armazenamento Marketplace](billing-enterprise-api-marketplace-storecharge.md) retorna divisão de encargos do marketplace baseada no uso de Olá por dia para Olá especificado o período de cobrança ou datas de início e término (taxas de uma vez não estão incluídas) .</span><span class="sxs-lookup"><span data-stu-id="9315f-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="9315f-123">**Tabela de preços** - Olá [API de folha de preço](billing-enterprise-api-pricesheet.md) fornece taxa aplicável Olá para cada medidor para Olá dado registro e o período de cobrança.</span><span class="sxs-lookup"><span data-stu-id="9315f-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="9315f-124">APIs auxiliares</span><span class="sxs-lookup"><span data-stu-id="9315f-124">Helper APIs</span></span>
 <span data-ttu-id="9315f-125">**Lista os períodos de cobrança** - Olá [API de períodos de cobrança](billing-enterprise-api-billing-periods.md) retorna uma lista de períodos que têm dados de consumo de saudação especificada registro em ordem cronológica inversa de cobrança.</span><span class="sxs-lookup"><span data-stu-id="9315f-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="9315f-126">Cada período contém uma propriedade apontando toohello rota de API para Olá quatro conjuntos de dados - BalanceSummary, UsageDetails, encargos do Marketplace e tabela de preços.</span><span class="sxs-lookup"><span data-stu-id="9315f-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="9315f-127">Códigos de resposta da API</span><span class="sxs-lookup"><span data-stu-id="9315f-127">API Response Codes</span></span>  
|<span data-ttu-id="9315f-128">Código de status de resposta</span><span class="sxs-lookup"><span data-stu-id="9315f-128">Response Status Code</span></span>|<span data-ttu-id="9315f-129">Mensagem</span><span class="sxs-lookup"><span data-stu-id="9315f-129">Message</span></span>|<span data-ttu-id="9315f-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="9315f-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="9315f-131">200</span><span class="sxs-lookup"><span data-stu-id="9315f-131">200</span></span>| <span data-ttu-id="9315f-132">OK</span><span class="sxs-lookup"><span data-stu-id="9315f-132">OK</span></span>|<span data-ttu-id="9315f-133">Nenhum erro</span><span class="sxs-lookup"><span data-stu-id="9315f-133">No error</span></span>|
|<span data-ttu-id="9315f-134">401</span><span class="sxs-lookup"><span data-stu-id="9315f-134">401</span></span>| <span data-ttu-id="9315f-135">Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="9315f-135">Unauthorized</span></span>| <span data-ttu-id="9315f-136">Chave de API não encontrada, inválida, expirada, etc.</span><span class="sxs-lookup"><span data-stu-id="9315f-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="9315f-137">404</span><span class="sxs-lookup"><span data-stu-id="9315f-137">404</span></span>| <span data-ttu-id="9315f-138">Indisponível</span><span class="sxs-lookup"><span data-stu-id="9315f-138">Unavailable</span></span>| <span data-ttu-id="9315f-139">Ponto de extremidade de relatório não encontrado</span><span class="sxs-lookup"><span data-stu-id="9315f-139">Report endpoint not found</span></span>|
|<span data-ttu-id="9315f-140">400</span><span class="sxs-lookup"><span data-stu-id="9315f-140">400</span></span>| <span data-ttu-id="9315f-141">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="9315f-141">Bad Request</span></span>| <span data-ttu-id="9315f-142">Parâmetros inválidos – intervalos de datas, números de EA, etc.</span><span class="sxs-lookup"><span data-stu-id="9315f-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="9315f-143">500</span><span class="sxs-lookup"><span data-stu-id="9315f-143">500</span></span>| <span data-ttu-id="9315f-144">Erro de servidor</span><span class="sxs-lookup"><span data-stu-id="9315f-144">Server Error</span></span>| <span data-ttu-id="9315f-145">Solicitação de processamento de erro inesperada</span><span class="sxs-lookup"><span data-stu-id="9315f-145">Unexoected error processing request</span></span>| 









