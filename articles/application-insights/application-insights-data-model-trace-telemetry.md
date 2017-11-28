---
title: aaaAzure modelo de dados de telemetria do Application Insights - telemetria de rastreamento | Microsoft Docs
description: Modelo de dados do Application Insights para telemetria de rastreamento
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="db254-103">Telemetria de rastreamento: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="db254-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="db254-104">A telemetria de rastreamento (em [Application Insights](app-insights-overview.md)) representa instruções de rastreamento de estilo `printf` pesquisadas por texto.</span><span class="sxs-lookup"><span data-stu-id="db254-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="db254-105">`Log4Net`, `NLog` e outras entradas do arquivo de log baseadas em texto são convertidas em instâncias desse tipo.</span><span class="sxs-lookup"><span data-stu-id="db254-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="db254-106">rastreamento de saudação não tem medidas como uma extensibilidade.</span><span class="sxs-lookup"><span data-stu-id="db254-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="db254-107">Mensagem</span><span class="sxs-lookup"><span data-stu-id="db254-107">Message</span></span>

<span data-ttu-id="db254-108">Mensagem de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="db254-108">Trace message.</span></span>

<span data-ttu-id="db254-109">Comprimento máximo: 32.768 caracteres</span><span class="sxs-lookup"><span data-stu-id="db254-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="db254-110">Nível de severidade</span><span class="sxs-lookup"><span data-stu-id="db254-110">Severity level</span></span>

<span data-ttu-id="db254-111">Nível de severidade de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="db254-111">Trace severity level.</span></span> <span data-ttu-id="db254-112">O valor pode ser `Verbose`, `Information`, `Warning`, `Error` ou `Critical`.</span><span class="sxs-lookup"><span data-stu-id="db254-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="db254-113">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="db254-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="db254-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db254-114">Next steps</span></span>

- <span data-ttu-id="db254-115">[Explore os logs de rastreamento do .NET no Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="db254-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="db254-116">[Explore os logs de rastreamento de Java no Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="db254-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="db254-117">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="db254-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="db254-118">Escrever telemetria personalizada de rastreamento</span><span class="sxs-lookup"><span data-stu-id="db254-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="db254-119">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="db254-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
