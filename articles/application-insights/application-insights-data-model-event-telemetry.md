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
# <a name="event-telemetry-application-insights-data-model"></a>Telemetria de eventos: modelo de dados do Application Insights

Você pode criar itens de telemetria evento (em [Application Insights](app-insights-overview.md)) toorepresent um evento ocorrido em seu aplicativo. Geralmente trata-se de uma interação do usuário como um clique de botão ou finalização de compra. Também pode ser um evento de ciclo de vida do aplicativo como a inicialização ou atualização de configuração. 

Semanticamente, eventos podem ou não ser toorequests correlacionados. No entanto, se usada corretamente, a telemetria de eventos é mais importante que solicitações ou rastreamentos. Eventos representam telemetria dos negócios e deve ser um tooseparate de assunto, menos agressiva [amostragem](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Nome

Nome do evento. agrupamento adequado tooallow e métricas úteis, restringir seu aplicativo para que ele gera um pequeno número de nomes de evento separado. Por exemplo, não use um nome à parte para cada instância gerado de um evento.

Comprimento máximo: 512 caracteres

## <a name="custom-properties"></a>Propriedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Próximas etapas

- Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.
- [Escrever telemetria do evento personalizada](app-insights-api-custom-events-metrics.md#trackevent)
- Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.
