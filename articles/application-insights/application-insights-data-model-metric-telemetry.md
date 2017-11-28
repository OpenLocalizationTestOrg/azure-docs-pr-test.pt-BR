---
title: "aaaAzure modelo de dados de telemetria do Application Insights - telemetria de métrica | Microsoft Docs"
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
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="fd6e2-103">Telemetria de métricas: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="fd6e2-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="fd6e2-104">Há dois tipos de telemetria de métricas com suporte do [Application Insights](app-insights-overview.md): medida única e métrica agregada previamente.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="fd6e2-105">A medida única é apenas um nome e valor.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="fd6e2-106">Métrica agregada previamente Especifica o valor mínimo e máximo da métrica de saudação no intervalo de agregação de saudação e desvio padrão dele.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="fd6e2-107">A telemetria de métrica agregada previamente supõe que esse período de agregação foi de um minuto.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="fd6e2-108">Há vários nomes de métrica conhecidos com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="fd6e2-109">Métrica representando os contadores de processo e de sistema:</span><span class="sxs-lookup"><span data-stu-id="fd6e2-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="fd6e2-110">**Nome do .NET**</span><span class="sxs-lookup"><span data-stu-id="fd6e2-110">**.NET name**</span></span>             | <span data-ttu-id="fd6e2-111">**Nome independente de plataforma**</span><span class="sxs-lookup"><span data-stu-id="fd6e2-111">**Platform agnostic name**</span></span> | <span data-ttu-id="fd6e2-112">**Nome da API REST**</span><span class="sxs-lookup"><span data-stu-id="fd6e2-112">**REST API name**</span></span> | <span data-ttu-id="fd6e2-113">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="fd6e2-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="fd6e2-114">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-114">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="fd6e2-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="fd6e2-116">total de CPU do computador</span><span class="sxs-lookup"><span data-stu-id="fd6e2-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="fd6e2-117">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-117">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="fd6e2-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="fd6e2-119">memória disponível em disco</span><span class="sxs-lookup"><span data-stu-id="fd6e2-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="fd6e2-120">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-120">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="fd6e2-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="fd6e2-122">CPU do processo de saudação hospedando o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="fd6e2-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="fd6e2-123">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-123">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="fd6e2-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="fd6e2-125">memória usada pelo processo de saudação hospedando o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="fd6e2-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="fd6e2-126">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-126">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="fd6e2-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="fd6e2-128">taxa de operações de e/s é executado pelo processo que hospeda o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="fd6e2-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="fd6e2-129">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-129">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="fd6e2-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="fd6e2-131">taxa de solicitações processadas por aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd6e2-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="fd6e2-132">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-132">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="fd6e2-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="fd6e2-134">taxa de exceções geradas por aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd6e2-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="fd6e2-135">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-135">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="fd6e2-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="fd6e2-137">tempo médio de execução de solicitações</span><span class="sxs-lookup"><span data-stu-id="fd6e2-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="fd6e2-138">Trabalho em andamento...</span><span class="sxs-lookup"><span data-stu-id="fd6e2-138">Work in progress...</span></span> | [<span data-ttu-id="fd6e2-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="fd6e2-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="fd6e2-140">número de solicitações aguardando em uma fila de processamento de saudação</span><span class="sxs-lookup"><span data-stu-id="fd6e2-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="fd6e2-141">Nome</span><span class="sxs-lookup"><span data-stu-id="fd6e2-141">Name</span></span>

<span data-ttu-id="fd6e2-142">Nome da métrica Olá você gostaria que toosee no portal do Application Insights e interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="fd6e2-143">Valor</span><span class="sxs-lookup"><span data-stu-id="fd6e2-143">Value</span></span>

<span data-ttu-id="fd6e2-144">Valor único para medida.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-144">Single value for measurement.</span></span> <span data-ttu-id="fd6e2-145">Soma de medidas individuais para agregação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="fd6e2-146">Contagem</span><span class="sxs-lookup"><span data-stu-id="fd6e2-146">Count</span></span>

<span data-ttu-id="fd6e2-147">Peso da métrica de métrica Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="fd6e2-148">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="fd6e2-149">Min</span><span class="sxs-lookup"><span data-stu-id="fd6e2-149">Min</span></span>

<span data-ttu-id="fd6e2-150">Valor mínimo da métrica Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="fd6e2-151">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="fd6e2-152">max</span><span class="sxs-lookup"><span data-stu-id="fd6e2-152">Max</span></span>

<span data-ttu-id="fd6e2-153">Valor máximo da métrica Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="fd6e2-154">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="fd6e2-155">Desvio padrão</span><span class="sxs-lookup"><span data-stu-id="fd6e2-155">Standard deviation</span></span>

<span data-ttu-id="fd6e2-156">Desvio padrão de métrica Olá agregado.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="fd6e2-157">Não deve ser definido para uma medida.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="fd6e2-158">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="fd6e2-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="fd6e2-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd6e2-159">Next steps</span></span>

- <span data-ttu-id="fd6e2-160">Saiba como toouse [API do Application Insights para métricas e eventos personalizados](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="fd6e2-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="fd6e2-161">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="fd6e2-162">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd6e2-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
