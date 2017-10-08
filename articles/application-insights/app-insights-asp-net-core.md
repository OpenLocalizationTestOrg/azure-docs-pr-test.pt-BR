---
title: aaaAzure Application Insights para ASP.NET Core | Microsoft Docs
description: Monitorar aplicativos web de disponibilidade, desempenho e uso.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>Application Insights para ASP.NET Core
O [Application Insights](app-insights-overview.md) permite que você monitore seu aplicativo Web quanto à disponibilidade, desempenho e uso. Feedback Olá que obter sobre desempenho hello e a eficácia do seu aplicativo em Olá curinga, você pode fazer escolhas informadas sobre a direção de saudação do design de saudação em cada ciclo de vida de desenvolvimento.

![Exemplo](./media/app-insights-asp-net-core/sample.png)

Precisa de uma assinatura do [Microsoft Azure](http://azure.com). Entre com uma conta da Microsoft, que você pode ter para o Windows, XBox Live ou outros serviços de nuvem da Microsoft. Sua equipe pode ter uma assinatura organizacional tooAzure: peça Olá proprietário tooadd tooit usando sua conta da Microsoft.

## <a name="getting-started"></a>Introdução

* No Gerenciador de Soluções do Visual Studio, clique com o botão direito do mouse no projeto e selecione **Configurar Application Insights** ou **Adicionar > Application Insights**. [Saiba mais](app-insights-asp-net.md).
* Se você não vir os comandos de menu, siga Olá [manual guia de Introdução ao obter](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Talvez você precise toodo isso se seu projeto foi criado com uma versão do Visual Studio antes de 2017.

## <a name="using-application-insights"></a>Usando o Application Insights
O logon no hello [portal do Microsoft Azure](https://portal.azure.com), selecione **todos os recursos** ou **Application Insights**e, em seguida, selecione o recurso de saudação criado toomonitor seu aplicativo.

Em uma janela separada do navegador, use seu aplicativo por algum tempo. Você verá os dados que aparecem nos gráficos do Application Insights hello. (Talvez seja necessário tooclick atualização). Haverá uma pequena quantidade de dados enquanto você estiver desenvolvendo, mas estes gráficos realmente ganharão vida quando você publicar seu aplicativo e tiver muitos usuários. 

página de visão geral de saudação mostra gráficos de desempenho principais: tempo de resposta do servidor, tempo de carregamento de página e as contagens de solicitações com falha. Clique em qualquer toosee gráfico mais gráficos e dados.

Modos de exibição no portal de saudação se enquadram em três categorias principais:

* [Do Metrics Explorer](app-insights-metrics-explorer.md) mostra gráficos e tabelas de métricas e contagens, como tempos de resposta, taxas de falha ou métricas criados por você com hello [API](app-insights-api-custom-events-metrics.md). Filtrar e segmento de dados de saudação por tooget de valores de propriedade, uma melhor compreensão sobre seu aplicativo e seus usuários.
* [Pesquisar Gerenciador](app-insights-diagnostic-search.md) lista os eventos individuais, como solicitações específicas, exceções, rastreamentos de log ou eventos que você criou por conta própria com hello [API](app-insights-api-custom-events-metrics.md). Filtrar e pesquisar eventos hello e navegar em problemas de tooinvestigate eventos relacionados.
* [Análise](app-insights-analytics.md) permite que você execute consultas SQL em sua telemetria e é uma poderosa ferramenta de análise e de diagnóstico.

## <a name="alerts"></a>Alertas
* Você obtém automaticamente [alertas proativos de diagnóstico](app-insights-proactive-diagnostics.md) que informam sobre alterações anômalas em taxas de falha e outras métricas.
* Configurar [testes de disponibilidade](app-insights-monitor-web-app-availability.md) tootest emails em seu site continuamente em locais em todo o mundo e get, assim como qualquer teste falhar.
* Configurar [alertas métricas](app-insights-monitor-web-app-availability.md) tooknow se métricas, como tempos de resposta ou taxas de exceção ficarem fora dos limites aceitáveis.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Código-fonte aberto
[Ler e contribuir toohello código](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Próximas etapas
* [Adicionar páginas da web a telemetria tooyour](app-insights-javascript.md) toomonitor página desempenho e uso.
* [Monitorar dependências](app-insights-asp-net-dependencies.md) toosee se REST, SQL ou outros recursos externos são lentidão você.
* [Use a API de saudação](app-insights-api-custom-events-metrics.md) toosend seus próprios eventos e métricas para uma exibição mais detalhada de uso e desempenho do seu aplicativo.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) Verifique seu aplicativo constantemente do mundo hello. 

