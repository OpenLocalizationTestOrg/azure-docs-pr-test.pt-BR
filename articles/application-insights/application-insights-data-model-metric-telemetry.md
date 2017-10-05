---
title: "Modelo de dados do Azure Application Insights Telemetry – telemetria de métricas | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria de métricas"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="926b6-103">Telemetria de métricas: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="926b6-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="926b6-104">Há dois tipos de telemetria de métricas com suporte do [Application Insights](app-insights-overview.md): medida única e métrica agregada previamente.</span><span class="sxs-lookup"><span data-stu-id="926b6-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="926b6-105">A medida única é apenas um nome e valor.</span><span class="sxs-lookup"><span data-stu-id="926b6-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="926b6-106">A métrica agregada previamente especifica os valores mínimo e máximo da métrica no intervalo de agregação e o desvio padrão desses valores.</span><span class="sxs-lookup"><span data-stu-id="926b6-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="926b6-107">A telemetria de métrica agregada previamente supõe que esse período de agregação foi de um minuto.</span><span class="sxs-lookup"><span data-stu-id="926b6-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="926b6-108">Há vários nomes de métrica conhecidos com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="926b6-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="926b6-109">Métrica representando os contadores de processo e de sistema:</span><span class="sxs-lookup"><span data-stu-id="926b6-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="926b6-110">**Nome do .NET**</span><span class="sxs-lookup"><span data-stu-id="926b6-110">**.NET name**</span></span>             | <span data-ttu-id="926b6-111">**Nome independente de plataforma**</span><span class="sxs-lookup"><span data-stu-id="926b6-111">**Platform agnostic name**</span></span> | <span data-ttu-id="926b6-112">**Nome da API REST**</span><span class="sxs-lookup"><span data-stu-id="926b6-112">**REST API name**</span></span> | <span data-ttu-id="926b6-113">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="926b6-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="926b6-114">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-114">Work in progress...</span></span> | [<span data-ttu-id="926b6-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="926b6-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="926b6-116">total de CPU do computador</span><span class="sxs-lookup"><span data-stu-id="926b6-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="926b6-117">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-117">Work in progress...</span></span> | [<span data-ttu-id="926b6-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="926b6-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="926b6-119">memória disponível em disco</span><span class="sxs-lookup"><span data-stu-id="926b6-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="926b6-120">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-120">Work in progress...</span></span> | [<span data-ttu-id="926b6-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="926b6-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="926b6-122">CPU do processo que hospeda o aplicativo</span><span class="sxs-lookup"><span data-stu-id="926b6-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="926b6-123">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-123">Work in progress...</span></span> | [<span data-ttu-id="926b6-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="926b6-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="926b6-125">memória usada pelo processo que hospeda o aplicativo</span><span class="sxs-lookup"><span data-stu-id="926b6-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="926b6-126">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-126">Work in progress...</span></span> | [<span data-ttu-id="926b6-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="926b6-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="926b6-128">taxa de execuções de operações de E/S pelo processo que hospeda o aplicativo</span><span class="sxs-lookup"><span data-stu-id="926b6-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="926b6-129">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-129">Work in progress...</span></span> | [<span data-ttu-id="926b6-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="926b6-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="926b6-131">taxa de solicitações processadas por aplicativo</span><span class="sxs-lookup"><span data-stu-id="926b6-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="926b6-132">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-132">Work in progress...</span></span> | [<span data-ttu-id="926b6-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="926b6-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="926b6-134">taxa de exceções geradas por aplicativo</span><span class="sxs-lookup"><span data-stu-id="926b6-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="926b6-135">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-135">Work in progress...</span></span> | [<span data-ttu-id="926b6-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="926b6-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="926b6-137">tempo médio de execução de solicitações</span><span class="sxs-lookup"><span data-stu-id="926b6-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="926b6-138">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="926b6-138">Work in progress...</span></span> | [<span data-ttu-id="926b6-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="926b6-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="926b6-140">número de solicitações aguardando processamento em uma fila</span><span class="sxs-lookup"><span data-stu-id="926b6-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="926b6-141">Nome</span><span class="sxs-lookup"><span data-stu-id="926b6-141">Name</span></span>

<span data-ttu-id="926b6-142">Nome da métrica que você gostaria de ver na interface do usuário e no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="926b6-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="926b6-143">Valor</span><span class="sxs-lookup"><span data-stu-id="926b6-143">Value</span></span>

<span data-ttu-id="926b6-144">Valor único para medida.</span><span class="sxs-lookup"><span data-stu-id="926b6-144">Single value for measurement.</span></span> <span data-ttu-id="926b6-145">Soma de medidas individuais para a agregação.</span><span class="sxs-lookup"><span data-stu-id="926b6-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="926b6-146">Contagem</span><span class="sxs-lookup"><span data-stu-id="926b6-146">Count</span></span>

<span data-ttu-id="926b6-147">Peso da métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="926b6-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="926b6-148">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="926b6-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="926b6-149">Min</span><span class="sxs-lookup"><span data-stu-id="926b6-149">Min</span></span>

<span data-ttu-id="926b6-150">Valor mínimo da métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="926b6-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="926b6-151">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="926b6-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="926b6-152">max</span><span class="sxs-lookup"><span data-stu-id="926b6-152">Max</span></span>

<span data-ttu-id="926b6-153">Valor máximo da métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="926b6-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="926b6-154">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="926b6-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="926b6-155">Desvio padrão</span><span class="sxs-lookup"><span data-stu-id="926b6-155">Standard deviation</span></span>

<span data-ttu-id="926b6-156">Desvio padrão da métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="926b6-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="926b6-157">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="926b6-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="926b6-158">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="926b6-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="926b6-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="926b6-159">Next steps</span></span>

- <span data-ttu-id="926b6-160">Saiba como usar a [API do Application Insights para métricas e eventos personalizados](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="926b6-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="926b6-161">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="926b6-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="926b6-162">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="926b6-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
