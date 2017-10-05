---
title: "Modelo de dados do Azure Application Insights Telemetry – telemetria de exceções | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria de exceções"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="277ae-103">Telemetria de exceções: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="277ae-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="277ae-104">Um [Application Insights](app-insights-overview.md), uma instância da exceção representa uma exceção tratada ou sem tratamento que ocorreu durante a execução do aplicativo monitorado.</span><span class="sxs-lookup"><span data-stu-id="277ae-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="277ae-105">ID do Problema</span><span class="sxs-lookup"><span data-stu-id="277ae-105">Problem Id</span></span>

<span data-ttu-id="277ae-106">Identificador do local em que a exceção foi lançada no código.</span><span class="sxs-lookup"><span data-stu-id="277ae-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="277ae-107">Usada para agrupamento de exceções.</span><span class="sxs-lookup"><span data-stu-id="277ae-107">Used for exceptions grouping.</span></span> <span data-ttu-id="277ae-108">Normalmente, é uma combinação do tipo de exceção e uma função da pilha de chamadas.</span><span class="sxs-lookup"><span data-stu-id="277ae-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="277ae-109">Comprimento máximo: 1.024 caracteres</span><span class="sxs-lookup"><span data-stu-id="277ae-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="277ae-110">Nível de severidade</span><span class="sxs-lookup"><span data-stu-id="277ae-110">Severity level</span></span>

<span data-ttu-id="277ae-111">Nível de severidade de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="277ae-111">Trace severity level.</span></span> <span data-ttu-id="277ae-112">O valor pode ser `Verbose`, `Information`, `Warning`, `Error` ou `Critical`.</span><span class="sxs-lookup"><span data-stu-id="277ae-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="277ae-113">Detalhes da exceção</span><span class="sxs-lookup"><span data-stu-id="277ae-113">Exception details</span></span>

<span data-ttu-id="277ae-114">(A ser estendido)</span><span class="sxs-lookup"><span data-stu-id="277ae-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="277ae-115">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="277ae-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="277ae-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="277ae-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="277ae-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="277ae-117">Next steps</span></span>

- <span data-ttu-id="277ae-118">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="277ae-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="277ae-119">Aprenda a [diagnosticar exceções em seus aplicativos Web com o Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="277ae-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="277ae-120">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="277ae-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
