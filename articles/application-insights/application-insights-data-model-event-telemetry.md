---
title: aaaAzure modelo de dados de telemetria do Application Insights - evento de telemetria | Microsoft Docs
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="94ec7-103">Telemetria de eventos: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="94ec7-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="94ec7-104">Você pode criar itens de telemetria evento (em [Application Insights](app-insights-overview.md)) toorepresent um evento ocorrido em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="94ec7-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="94ec7-105">Geralmente trata-se de uma interação do usuário como um clique de botão ou finalização de compra.</span><span class="sxs-lookup"><span data-stu-id="94ec7-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="94ec7-106">Também pode ser um evento de ciclo de vida do aplicativo como a inicialização ou atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="94ec7-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="94ec7-107">Semanticamente, eventos podem ou não ser toorequests correlacionados.</span><span class="sxs-lookup"><span data-stu-id="94ec7-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="94ec7-108">No entanto, se usada corretamente, a telemetria de eventos é mais importante que solicitações ou rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="94ec7-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="94ec7-109">Eventos representam telemetria dos negócios e deve ser um tooseparate de assunto, menos agressiva [amostragem](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="94ec7-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="94ec7-110">Nome</span><span class="sxs-lookup"><span data-stu-id="94ec7-110">Name</span></span>

<span data-ttu-id="94ec7-111">Nome do evento.</span><span class="sxs-lookup"><span data-stu-id="94ec7-111">Event name.</span></span> <span data-ttu-id="94ec7-112">agrupamento adequado tooallow e métricas úteis, restringir seu aplicativo para que ele gera um pequeno número de nomes de evento separado.</span><span class="sxs-lookup"><span data-stu-id="94ec7-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="94ec7-113">Por exemplo, não use um nome à parte para cada instância gerado de um evento.</span><span class="sxs-lookup"><span data-stu-id="94ec7-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="94ec7-114">Comprimento máximo: 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="94ec7-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="94ec7-115">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="94ec7-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="94ec7-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="94ec7-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="94ec7-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94ec7-117">Next steps</span></span>

- <span data-ttu-id="94ec7-118">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="94ec7-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="94ec7-119">Escrever telemetria do evento personalizada</span><span class="sxs-lookup"><span data-stu-id="94ec7-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="94ec7-120">Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="94ec7-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
