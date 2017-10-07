---
title: "aaaAzure modelo de dados de telemetria do Application Insights - telemetria de dependência | Microsoft Docs"
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
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="4dac5-103">Telemetria de dependências: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4dac5-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="4dac5-104">Telemetria de dependência (em [Application Insights](app-insights-overview.md)) representa uma interação de componente Olá monitorado com um componente remoto, como SQL ou um ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="4dac5-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="4dac5-105">Nome</span><span class="sxs-lookup"><span data-stu-id="4dac5-105">Name</span></span>

<span data-ttu-id="4dac5-106">Nome do comando Olá iniciado com essa chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="4dac5-107">Valor de baixa cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="4dac5-107">Low cardinality value.</span></span> <span data-ttu-id="4dac5-108">Os exemplos são o nome do procedimento armazenado e o modelo do caminho da URL.</span><span class="sxs-lookup"><span data-stu-id="4dac5-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="4dac5-109">ID</span><span class="sxs-lookup"><span data-stu-id="4dac5-109">ID</span></span>

<span data-ttu-id="4dac5-110">Identificador de uma instância de chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="4dac5-111">Usado para correlação com o item de telemetria de solicitação Olá correspondente toothis chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="4dac5-112">Para obter mais informações, consulte a página de [correlação](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="4dac5-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="4dac5-113">Dados</span><span class="sxs-lookup"><span data-stu-id="4dac5-113">Data</span></span>

<span data-ttu-id="4dac5-114">Comando iniciado por essa chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="4dac5-115">Exemplos são a instrução SQL e a URL HTTP com todos os parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="4dac5-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="4dac5-116">Tipo</span><span class="sxs-lookup"><span data-stu-id="4dac5-116">Type</span></span>

<span data-ttu-id="4dac5-117">Nome do tipo de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-117">Dependency type name.</span></span> <span data-ttu-id="4dac5-118">Valor de baixa cardinalidade para agrupamento lógico de dependências e a interpretação de outros campos como commandName e resultCode.</span><span class="sxs-lookup"><span data-stu-id="4dac5-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="4dac5-119">Exemplos são HTTP, tabela do Azure e SQL.</span><span class="sxs-lookup"><span data-stu-id="4dac5-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="4dac5-120">Destino</span><span class="sxs-lookup"><span data-stu-id="4dac5-120">Target</span></span>

<span data-ttu-id="4dac5-121">Site de destino de uma chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-121">Target site of a dependency call.</span></span> <span data-ttu-id="4dac5-122">Os exemplos são o nome do servidor e o endereço do host.</span><span class="sxs-lookup"><span data-stu-id="4dac5-122">Examples are server name, host address.</span></span> <span data-ttu-id="4dac5-123">Para obter mais informações, consulte a página de [correlação](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="4dac5-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="4dac5-124">Duração</span><span class="sxs-lookup"><span data-stu-id="4dac5-124">Duration</span></span>

<span data-ttu-id="4dac5-125">Duração da solicitação no formato: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="4dac5-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="4dac5-126">Deve ser menor que `1000` dias.</span><span class="sxs-lookup"><span data-stu-id="4dac5-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="4dac5-127">Código de resultado</span><span class="sxs-lookup"><span data-stu-id="4dac5-127">Result code</span></span>

<span data-ttu-id="4dac5-128">Código de resultado de uma chamada de dependência.</span><span class="sxs-lookup"><span data-stu-id="4dac5-128">Result code of a dependency call.</span></span> <span data-ttu-id="4dac5-129">Os exemplos são o código de erro do SQL e o código de status HTTP.</span><span class="sxs-lookup"><span data-stu-id="4dac5-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="4dac5-130">Sucesso</span><span class="sxs-lookup"><span data-stu-id="4dac5-130">Success</span></span>

<span data-ttu-id="4dac5-131">Indicação de chamada bem-sucedida ou malsucedida.</span><span class="sxs-lookup"><span data-stu-id="4dac5-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="4dac5-132">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="4dac5-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="4dac5-133">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="4dac5-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="4dac5-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4dac5-134">Next steps</span></span>

- <span data-ttu-id="4dac5-135">Configurar o acompanhamento de dependência para [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="4dac5-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="4dac5-136">Configurar o acompanhamento de dependência para [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="4dac5-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="4dac5-137">Escrever telemetria de dependência personalizada</span><span class="sxs-lookup"><span data-stu-id="4dac5-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="4dac5-138">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4dac5-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="4dac5-139">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4dac5-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
