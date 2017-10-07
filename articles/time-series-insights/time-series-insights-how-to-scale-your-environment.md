---
title: "aaaHow tooscale seu ambiente do Azure Insights de série de tempo | Microsoft Docs"
description: "Este tutorial aborda como tooscale seu ambiente do Azure Insights de série de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Como tooscale seu ambiente de informações da série de tempo

Este tutorial aborda como tooscale seu ambiente de informações da série de tempo.

> [!NOTE]
> Escalar verticalmente os tipos de sku não é permitido. Um ambiente com um Sku S1 não pode ser convertido em um ambiente de S2.

## <a name="s1-sku-ingress-rates-and-capacities"></a>As taxas e as capacidades de entrada de SKU S1

| Capacidade de SKU S1 | Taxa de entrada | Capacidade de armazenamento máxima
| --- | --- | --- |
| 1 | 1 GB (1 milhão de eventos) | 30 GB (30 milhões de eventos) por mês |
| 10 | 10 GB (10 milhões de eventos) | 300 GB (300 milhões de eventos) por mês |

## <a name="s2-sku-ingress-rates-and-capacities"></a>As taxas e as capacidades de entrada de SKU S2

| Capacidade de SKU S2 | Taxa de entrada | Capacidade de armazenamento máxima
| --- | --- | --- |
| 1 | 10 GB (10 milhões de eventos) | 300 GB (300 milhões de eventos) por mês |
| 10 | 100 GB (100 milhões de eventos) | 3 TB (3 bilhões de eventos) por mês |

As capacidades são dimensionadas linearmente, portanto, uma sku S1 com capacidade 2 dá suporte a 2 GB (2 milhões) de eventos por taxa de entrada por dia e 60 GB (60 milhões de eventos) por mês.

## <a name="changing-hello-capacity-of-your-environment"></a>Alterando a capacidade de saudação do seu ambiente

1. No portal do Azure de Olá, selecione Olá ambiente cuja capacidade deseja toochange.
1. Em Configurações, clique em Configurar.
1. Use Olá capacidade controle deslizante tooselect Olá capacidade que atenda aos requisitos de saudação para suas taxas de entrada e a capacidade de armazenamento.

## <a name="next-steps"></a>Próximas etapas

* Verifique se que a nova capacidade de saudação é suficiente tooprevent limitação. Para obter mais detalhes, consulte Olá *seu ambiente pode ser ser limitado* seção [aqui](time-series-insights-diagnose-and-solve-problems.md).
