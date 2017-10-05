---
title: "APIs Enterprise de cobrança do Azure | Microsoft Docs"
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
ms.openlocfilehash: e3a5f9bcd6b54a51c29df649f1ae8ac185b153a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="0e3c6-103">Visão geral das APIs de Relatórios para clientes Enterprise</span><span class="sxs-lookup"><span data-stu-id="0e3c6-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="0e3c6-104">As APIs de Relatórios permitem que clientes Enterprise do Azure efetuem pull de modo programático dos dados de consumo e cobrança nas ferramentas preferidas de análise de dados.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="0e3c6-105">Habilitando o acesso a dados para a API</span><span class="sxs-lookup"><span data-stu-id="0e3c6-105">Enabling data access to the API</span></span>
* <span data-ttu-id="0e3c6-106">**Gerar ou recuperar a chave de API** – faça logon no Enterprise Portal e siga o tutorial em Ajuda – APIs de Relatório.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-106">**Generate or retrieve the API key** - Log in to the Enterprise portal and follow the tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="0e3c6-107">A primeira seção neste artigo explica como gerar ou recuperar a chave de API do registro especificado.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-107">The first section under this help article explains how to generate or retrieve the API key for the specified enrollment.</span></span>
* <span data-ttu-id="0e3c6-108">**Passando chaves na API**: a chave de API precisa ser passada para cada chamada de Autenticação e Autorização.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-108">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="0e3c6-109">A propriedade a seguir precisa ser para os cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="0e3c6-109">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="0e3c6-110">Chave de cabeçalho da solicitação</span><span class="sxs-lookup"><span data-stu-id="0e3c6-110">Request Header Key</span></span> | <span data-ttu-id="0e3c6-111">Valor</span><span class="sxs-lookup"><span data-stu-id="0e3c6-111">Value</span></span>|
|-|-|
|<span data-ttu-id="0e3c6-112">Autorização</span><span class="sxs-lookup"><span data-stu-id="0e3c6-112">Authorization</span></span>| <span data-ttu-id="0e3c6-113">Especifique o valor neste formato: **portador {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="0e3c6-113">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="0e3c6-114">Exemplo: portador e... 09</span><span class="sxs-lookup"><span data-stu-id="0e3c6-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="0e3c6-115">APIs de consumo</span><span class="sxs-lookup"><span data-stu-id="0e3c6-115">Consumption APIs</span></span>
<span data-ttu-id="0e3c6-116">Um ponto de extremidade Swagger está disponível [aqui](https://consumption.azure.com/swagger/ui/index) para as APIs descritas abaixo, que devem permitir a fácil introspecção da API e a capacidade de gerar SDKs de cliente usando [AutoRest](https://github.com/Azure/AutoRest) ou [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="0e3c6-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="0e3c6-117">Os dados a partir de 1º de maio de 2014 estão disponíveis por essa API.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="0e3c6-118">**Saldo e Resumo**: a [API Saldo e Resumo](billing-enterprise-api-balance-summary.md) oferece um resumo mensal de informações sobre saldos, novas compras, encargos de serviço do Azure Marketplace, ajustes e encargos de excedente.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-118">**Balance and Summary** - The [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="0e3c6-119">**Detalhes de Uso**: a [API Detalhes de Uso](billing-enterprise-api-usage-detail.md) oferece um detalhamento diário das quantidades consumidas e de encargos estimados por um registro.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-119">**Usage Details** - The [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="0e3c6-120">O resultado também inclui informações sobre instâncias, medidores e departamentos.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-120">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="0e3c6-121">A API pode ser consultada por período de cobrança ou por uma data de início e de término especificada.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-121">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="0e3c6-122">**Encargo de Repositório do Marketplace**: a [API Encargo de Repositório do Marketplace](billing-enterprise-api-marketplace-storecharge.md) retorna o detalhamento dos encargos do marketplace com base no uso por dia para o Período de Cobrança especificado ou as datas de início e término (taxas avulsas não estão incluídas).</span><span class="sxs-lookup"><span data-stu-id="0e3c6-122">**Marketplace Store Charge** - The [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="0e3c6-123">**Tabela de Preços**: a [API Tabela de Preços](billing-enterprise-api-pricesheet.md) fornece a taxa aplicável de cada Medidor para o Registro e o Período de Cobrança determinados.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-123">**Price Sheet** - The [Price Sheet API](billing-enterprise-api-pricesheet.md) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="0e3c6-124">APIs auxiliares</span><span class="sxs-lookup"><span data-stu-id="0e3c6-124">Helper APIs</span></span>
 <span data-ttu-id="0e3c6-125">**Listar Períodos de Cobrança**: a [API Períodos de Cobrança](billing-enterprise-api-billing-periods.md) retorna uma lista de períodos de cobrança que têm dados de consumo para o Registro especificado em ordem cronológica inversa.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-125">**List Billing Periods** - The [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="0e3c6-126">Cada período contém uma propriedade que aponta para a rota da API dos quatro conjuntos de dados: BalanceSummary, UsageDetails, Encargos do Marketplace e Price Sheet.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-126">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="0e3c6-127">Códigos de resposta da API</span><span class="sxs-lookup"><span data-stu-id="0e3c6-127">API Response Codes</span></span>  
|<span data-ttu-id="0e3c6-128">Código de status de resposta</span><span class="sxs-lookup"><span data-stu-id="0e3c6-128">Response Status Code</span></span>|<span data-ttu-id="0e3c6-129">Mensagem</span><span class="sxs-lookup"><span data-stu-id="0e3c6-129">Message</span></span>|<span data-ttu-id="0e3c6-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="0e3c6-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="0e3c6-131">200</span><span class="sxs-lookup"><span data-stu-id="0e3c6-131">200</span></span>| <span data-ttu-id="0e3c6-132">OK</span><span class="sxs-lookup"><span data-stu-id="0e3c6-132">OK</span></span>|<span data-ttu-id="0e3c6-133">Nenhum erro</span><span class="sxs-lookup"><span data-stu-id="0e3c6-133">No error</span></span>|
|<span data-ttu-id="0e3c6-134">401</span><span class="sxs-lookup"><span data-stu-id="0e3c6-134">401</span></span>| <span data-ttu-id="0e3c6-135">Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="0e3c6-135">Unauthorized</span></span>| <span data-ttu-id="0e3c6-136">Chave de API não encontrada, inválida, expirada, etc.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="0e3c6-137">404</span><span class="sxs-lookup"><span data-stu-id="0e3c6-137">404</span></span>| <span data-ttu-id="0e3c6-138">Indisponível</span><span class="sxs-lookup"><span data-stu-id="0e3c6-138">Unavailable</span></span>| <span data-ttu-id="0e3c6-139">Ponto de extremidade de relatório não encontrado</span><span class="sxs-lookup"><span data-stu-id="0e3c6-139">Report endpoint not found</span></span>|
|<span data-ttu-id="0e3c6-140">400</span><span class="sxs-lookup"><span data-stu-id="0e3c6-140">400</span></span>| <span data-ttu-id="0e3c6-141">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="0e3c6-141">Bad Request</span></span>| <span data-ttu-id="0e3c6-142">Parâmetros inválidos – intervalos de datas, números de EA, etc.</span><span class="sxs-lookup"><span data-stu-id="0e3c6-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="0e3c6-143">500</span><span class="sxs-lookup"><span data-stu-id="0e3c6-143">500</span></span>| <span data-ttu-id="0e3c6-144">Erro de servidor</span><span class="sxs-lookup"><span data-stu-id="0e3c6-144">Server Error</span></span>| <span data-ttu-id="0e3c6-145">Solicitação de processamento de erro inesperada</span><span class="sxs-lookup"><span data-stu-id="0e3c6-145">Unexoected error processing request</span></span>| 









