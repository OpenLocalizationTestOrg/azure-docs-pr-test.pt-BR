---
title: "Modelo de dados do Azure Application Insights Telemetry – telemetria de dependências | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria de dependências"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="1f26f-103">Telemetria de dependências: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="1f26f-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="1f26f-104">A telemetria de dependência (em [Application Insights](app-insights-overview.md)) representa uma interação do componente monitorado com um componente remoto como SQL ou um ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="1f26f-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="1f26f-105">Nome</span><span class="sxs-lookup"><span data-stu-id="1f26f-105">Name</span></span>

<span data-ttu-id="1f26f-106">Nome do comando iniciado com esta chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="1f26f-107">Valor de baixa cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="1f26f-107">Low cardinality value.</span></span> <span data-ttu-id="1f26f-108">Os exemplos são o nome do procedimento armazenado e o modelo do caminho da URL.</span><span class="sxs-lookup"><span data-stu-id="1f26f-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="1f26f-109">ID</span><span class="sxs-lookup"><span data-stu-id="1f26f-109">ID</span></span>

<span data-ttu-id="1f26f-110">Identificador de uma instância de chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="1f26f-111">Usado para correlação com o item de telemetria de solicitação correspondente a essa chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="1f26f-112">Para obter mais informações, consulte a página de [correlação](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="1f26f-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="1f26f-113">Dados</span><span class="sxs-lookup"><span data-stu-id="1f26f-113">Data</span></span>

<span data-ttu-id="1f26f-114">Comando iniciado por essa chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="1f26f-115">Exemplos são a instrução SQL e a URL HTTP com todos os parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="1f26f-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="1f26f-116">Tipo</span><span class="sxs-lookup"><span data-stu-id="1f26f-116">Type</span></span>

<span data-ttu-id="1f26f-117">Nome do tipo de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-117">Dependency type name.</span></span> <span data-ttu-id="1f26f-118">Valor de baixa cardinalidade para agrupamento lógico de dependências e a interpretação de outros campos como commandName e resultCode.</span><span class="sxs-lookup"><span data-stu-id="1f26f-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="1f26f-119">Exemplos são HTTP, tabela do Azure e SQL.</span><span class="sxs-lookup"><span data-stu-id="1f26f-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="1f26f-120">Destino</span><span class="sxs-lookup"><span data-stu-id="1f26f-120">Target</span></span>

<span data-ttu-id="1f26f-121">Site de destino de uma chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-121">Target site of a dependency call.</span></span> <span data-ttu-id="1f26f-122">Os exemplos são o nome do servidor e o endereço do host.</span><span class="sxs-lookup"><span data-stu-id="1f26f-122">Examples are server name, host address.</span></span> <span data-ttu-id="1f26f-123">Para obter mais informações, consulte a página de [correlação](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="1f26f-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="1f26f-124">Duração</span><span class="sxs-lookup"><span data-stu-id="1f26f-124">Duration</span></span>

<span data-ttu-id="1f26f-125">Duração da solicitação no formato: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="1f26f-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="1f26f-126">Deve ser menor que `1000` dias.</span><span class="sxs-lookup"><span data-stu-id="1f26f-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="1f26f-127">Código de resultado</span><span class="sxs-lookup"><span data-stu-id="1f26f-127">Result code</span></span>

<span data-ttu-id="1f26f-128">Código de resultado de uma chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="1f26f-128">Result code of a dependency call.</span></span> <span data-ttu-id="1f26f-129">Os exemplos são o código de erro do SQL e o código de status HTTP.</span><span class="sxs-lookup"><span data-stu-id="1f26f-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="1f26f-130">Sucesso</span><span class="sxs-lookup"><span data-stu-id="1f26f-130">Success</span></span>

<span data-ttu-id="1f26f-131">Indicação de chamada bem-sucedida ou malsucedida.</span><span class="sxs-lookup"><span data-stu-id="1f26f-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="1f26f-132">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="1f26f-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="1f26f-133">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="1f26f-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="1f26f-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f26f-134">Next steps</span></span>

- <span data-ttu-id="1f26f-135">Configurar o acompanhamento de dependência para [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="1f26f-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="1f26f-136">Configurar o acompanhamento de dependência para [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="1f26f-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="1f26f-137">Escrever telemetria de dependência personalizada</span><span class="sxs-lookup"><span data-stu-id="1f26f-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="1f26f-138">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1f26f-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="1f26f-139">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1f26f-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
