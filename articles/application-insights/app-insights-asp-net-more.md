---
title: aaaGet mais ideias de aplicativo do Azure | Microsoft Docs
description: "Depois de guia de Introdução ao Application Insights, aqui está um resumo dos recursos de saudação, que você pode explorar."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>Mais telemetria do Application Insights
Depois de ter [adicionado código do Application Insights tooyour ASP.NET](app-insights-asp-net.md), há algumas coisas que você pode fazer tooget ainda mais a telemetria. 

| Ação | O que você ganha|
|---|---|
|(Servidores IIS) [Instale o Monitor de Status](http://go.microsoft.com/fwlink/?LinkId=506648) em cada máquina do servidor.<br/>(Aplicativos da web do azure) No painel de controle do Azure de saudação do aplicativo web de hello, abra a folha de Application Insights de saudação.| [**Contadores de desempenho**](app-insights-performance-counters.md)<br/>[**Exceções**](app-insights-asp-net-exceptions.md) - rastreamentos de pilha detalhados<br/>[**Dependências**](app-insights-asp-net-dependencies.md)|
|[Adicionar páginas da web do hello JavaScript trecho tooyour](app-insights-javascript.md)|[Desempenho da página](app-insights-web-track-usage.md), exceções do navegador, desempenho do AJAX. Telemetria personalizada do lado do cliente.|
|[Criar testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md)|Obter alertas se o seu site ficar indisponível|
|[Certificar-se de que buildinfo.config](https://msdn.microsoft.com/library/dn449058.aspx) seja gerado pelo MSBuild|[Criar anotações em gráficos de métricas](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/)
|[Gravar eventos e métricas personalizadas](app-insights-api-custom-events-metrics.md)|Contagem de métricas e eventos de negócios, acompanhar o uso detalhado e muito mais.|
|[Perfil de seu site ativo](https://aka.ms/AIProfilerPreview)|Intervalos de função detalhada de seu aplicativo Web ativo|






