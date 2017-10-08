---
title: "aaaAzure modelo de dados de telemetria do Application Insights - telemetria de exceção | Microsoft Docs"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a>Telemetria de exceções: modelo de dados do Application Insights

Em [Application Insights](app-insights-overview.md), uma instância de exceção representa uma exceção de tratada ou não tratada que ocorreu durante a execução do aplicativo hello monitorado.

## <a name="problem-id"></a>ID do Problema

Identificador de onde a exceção de saudação foi gerada no código. Usada para agrupamento de exceções. Normalmente, uma combinação de tipo de exceção e uma função da pilha de chamadas de saudação.

Comprimento máximo: 1.024 caracteres

## <a name="severity-level"></a>Nível de severidade

Nível de severidade de rastreamento. O valor pode ser `Verbose`, `Information`, `Warning`, `Error` ou `Critical`.

## <a name="exception-details"></a>Detalhes da exceção

(toobe estendido)

## <a name="custom-properties"></a>Propriedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Próximas etapas

- Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.
- Saiba como muito[diagnosticar exceções em seus aplicativos web com o Application Insights](app-insights-asp-net-exceptions.md).
- Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.
