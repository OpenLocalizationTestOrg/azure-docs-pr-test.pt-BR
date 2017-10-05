---
title: "Modelo de dados do Azure Application Insights Telemetry – telemetria de eventos | Microsoft Docs"
description: Modelo de dados do Application Insights para telemetria de eventos
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
ms.openlocfilehash: 422e193ae10938954602a6ef8c49fd47f473bc01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="9962b-103">Telemetria de eventos: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="9962b-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="9962b-104">Você pode criar itens de telemetria do evento (em [Application Insights](app-insights-overview.md)) para representar um evento que ocorreu em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9962b-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span></span> <span data-ttu-id="9962b-105">Geralmente trata-se de uma interação do usuário como um clique de botão ou finalização de compra.</span><span class="sxs-lookup"><span data-stu-id="9962b-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="9962b-106">Também pode ser um evento de ciclo de vida do aplicativo como a inicialização ou atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="9962b-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="9962b-107">Semanticamente, eventos podem ou não ser correlacionados às solicitações.</span><span class="sxs-lookup"><span data-stu-id="9962b-107">Semantically, events may or may not be correlated to requests.</span></span> <span data-ttu-id="9962b-108">No entanto, se usada corretamente, a telemetria de eventos é mais importante que solicitações ou rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="9962b-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="9962b-109">Os eventos representam a telemetria de negócios e devem estar sujeitos a uma [amostragem](app-insights-api-filtering-sampling.md) separada, menos agressiva.</span><span class="sxs-lookup"><span data-stu-id="9962b-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="9962b-110">Nome</span><span class="sxs-lookup"><span data-stu-id="9962b-110">Name</span></span>

<span data-ttu-id="9962b-111">Nome do evento.</span><span class="sxs-lookup"><span data-stu-id="9962b-111">Event name.</span></span> <span data-ttu-id="9962b-112">Para permitir o agrupamento adequado e métricas úteis, restrinja seu aplicativo de maneira que ele gere um pequeno número de nomes de eventos separados.</span><span class="sxs-lookup"><span data-stu-id="9962b-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="9962b-113">Por exemplo, não use um nome à parte para cada instância gerado de um evento.</span><span class="sxs-lookup"><span data-stu-id="9962b-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="9962b-114">Comprimento máximo: 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="9962b-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="9962b-115">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="9962b-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="9962b-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="9962b-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="9962b-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9962b-117">Next steps</span></span>

- <span data-ttu-id="9962b-118">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9962b-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="9962b-119">Escrever telemetria do evento personalizada</span><span class="sxs-lookup"><span data-stu-id="9962b-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="9962b-120">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9962b-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
