---
title: "aaaSmart detecção no Azure Application Insights | Microsoft Docs"
description: "O Application Insights executa uma análise automática profunda de telemetria do seu aplicativo e o avisará sobre possíveis problemas de desempenho."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Detecção Inteligente no Application Insights
 A Detecção Inteligente avisa automaticamente sobre possíveis problemas de desempenho no seu aplicativo Web. Ele executa análise proativa de telemetria Olá que seu aplicativo envia muito[Application Insights](app-insights-overview.md). Se houver um aumento repentino nas taxas de falha ou nos padrões anormais de desempenho de cliente ou de servidor, você receberá um alerta. Esse recurso não precisa de nenhuma configuração. Ela funciona se o seu aplicativo envia telemetria suficiente.

Você pode acessar alertas de detecção inteligente de emails de saudação recebidos e na folha de detecção inteligente hello.

## <a name="review-your-smart-detections"></a>Revise suas detecções inteligentes
É possível descobrir as detecções de duas maneiras:

* **Você recebe um email** do Application Insights. Aqui está um exemplo típico:
  
    ![Alerta de email](./media/app-insights-proactive-diagnostics/03.png)
  
    Clique em Olá grande botão tooopen mais detalhes no portal de saudação.
* **bloco de detecção inteligente Olá** na visão geral do aplicativo folha mostra uma contagem de alertas recentes. Clique em Olá bloco toosee uma lista dos alertas recentes.

![Exibir detecções recentes](./media/app-insights-proactive-diagnostics/04.png)

Selecione um alerta toosee seus detalhes.

## <a name="what-problems-are-detected"></a>Quais problemas foram detectados?
Há três tipos de detecção:

* [Detecção inteligente - anomalias de falha](app-insights-proactive-failure-diagnostics.md). Podemos usar o aprendizado de máquina tooset taxa de saudação esperada de solicitações com falha para seu aplicativo, correlacionando com carga e outros fatores. Se a taxa de falha Olá ficar fora envelope esperado hello, podemos enviar um alerta.
* [Detecção inteligente - anomalias de desempenho](app-insights-proactive-performance-diagnostics.md). Você receberá notificações se o tempo de resposta de uma duração da operação ou dependência está diminuindo toohistorical em comparação com linha de base ou se é identificar um padrão anormal no tempo de resposta ou tempo de carregamento de página.   
* [Detecção inteligente - problemas do Serviço em Nuvem do Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Você obterá alertas se seu aplicativo estiver hospedado nos Serviços de Nuvem do Azure e se uma instância de função tiver falhas de inicialização, reciclagem frequente ou falhas no tempo de execução.

(links de ajuda de saudação em cada notificação levam artigos relevantes toohello.)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Próximas etapas
Essas ferramentas de diagnóstico ajudam a inspecionar a telemetria de saudação do seu aplicativo:

* [Metrics explorer](app-insights-metrics-explorer.md)
* [Gerenciador de pesquisas](app-insights-diagnostic-search.md)
* [Analytics - linguagem de consulta poderosa](app-insights-analytics-tour.md)

A Detecção Inteligente é totalmente automática. Mas você queria tooset alguns alertas mais?

* [Alertas de métrica configurados manualmente](app-insights-alerts.md)
* [Testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md) 

