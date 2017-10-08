---
title: aaaMonitor o desempenho do aplicativo web do Azure | Microsoft Docs
description: "Monitoramento do desempenho do aplicativo de para aplicativos Web do Azure. Tempo de resposta e de carga, informações de dependência e alertas definidos sobre o desempenho do gráfico."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Monitorar o desempenho do aplicativo Web do Azure
Em Olá [Portal do Azure](https://portal.azure.com) você pode configurar o monitoramento de desempenho do aplicativo para o [aplicativos web do Azure](../app-service-web/app-service-web-overview.md). [Informações de aplicativo do Azure](app-insights-overview.md) instrumenta telemetria do toosend seu aplicativo sobre seu toohello atividades serviço Application Insights, onde é armazenado e analisado. Lá, os gráficos de métricas e ferramentas de pesquisa podem ser usadas toohelp diagnosticar problemas, melhorar o desempenho e avaliar o uso.

## <a name="run-time-or-build-time"></a>Tempo de execução ou tempo de compilação
Você pode configurar o monitoramento por instrumentação aplicativo hello em qualquer uma das duas maneiras:

* **Tempo de execução** - você pode selecionar um desempenho extensão de monitoramento quando seu aplicativo Web já está ativo. Ele não é necessário toorebuild ou reinstale o aplicativo. Obtenha um conjunto padrão de pacotes que monitoram os tempos de resposta, taxas de êxito, exceções, dependências e assim por diante. 
* **Tempo de compilação** - você pode instalar um pacote em seu aplicativo em desenvolvimento. Essa opção é mais versátil. Em adição toohello mesmo pacotes padrão, você pode escrever telemetria de saudação do código toocustomize ou toosend sua telemetria. Você pode registrar eventos de registro de acordo com a semântica toohello do seu domínio de aplicativo ou de atividades específicas. 

## <a name="run-time-instrumentation-with-application-insights"></a>Execute a instrumentação de tempo com o Application Insights
Se você já estiver executando um aplicativo Web no Azure, então já está sendo monitorado: taxas de erro e de solicitação. Adicione Application Insights tooget mais, como tempos de resposta, monitoramento toodependencies de chamadas, detecção inteligente e poderosa linguagem de consulta de análise de Log hello. 

1. **Selecione o Application Insights** no painel de controle do Azure de saudação para seu aplicativo web.
   
    ![Em Monitoramento, selecione Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Escolha toocreate um novo recurso, a menos que você configurou um recurso do Application Insights para esse aplicativo por outra rota.
2. **Instrumente seu aplicativo Web** após a instalação do Application Insights. 
   
    ![Instrumentar seu aplicativo Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Habilite o monitoramento do lado do cliente** para telemetria de usuário e exibição de página.

   * Selecione Configurações > Configurações do Aplicativo
   * Em configurações do aplicativo, adicione um novo par de chave/valor: 
   
    Chave: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valor: `true`
   * **Salvar** Olá configurações e **reiniciar** seu aplicativo.
3. **Monitore o seu aplicativo**.  [Dados de saudação Expore](#explore-the-data).

Posteriormente, você pode criar aplicativo hello com o Application Insights se desejar.

*Como remover o Application Insights, ou alternar toosending tooanother recurso?*

* No Azure, folha de controle de aplicativo de web hello aberta e em ferramentas de desenvolvimento, abra **extensões**. Exclua extensão do Application Insights hello. Em seguida, em monitoramento, escolha Application Insights e crie ou selecione recurso Olá desejado.

## <a name="build-hello-app-with-application-insights"></a>Criar aplicativo hello com o Application Insights
O Application Insights pode fornecer dados de telemetria mais detalhados instalando um SDK em seu aplicativo. Em particular, você pode coletar logs de rastreamento, [escrever telemetria personalizada](app-insights-api-custom-events-metrics.md) e obter relatórios de exceção mais detalhados.

1. **No Visual Studio** (2013 atualização 2 ou posterior), adicione o Application Insights ao seu projeto.

    Clique com botão direito Olá web e selecione **Adicionar > Application Insights** ou **configurar o Application Insights**.
   
    ![Clique com botão direito Olá web e escolha Adicionar ou configurar o Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    Se você for questionado toosign em, use credenciais de saudação para sua conta do Azure.
   
    operação de saudação tem dois efeitos:
   
   1. Cria um recurso do Application Insights no Azure, onde a telemetria é armazenada, analisada e exibida.
   2. Adiciona a saudação do Application Insights NuGet tooyour código de pacote (se ele não estiver lá já) e o configura toosend telemetria toohello recursos do Azure.
2. **Testar a telemetria Olá** pelo aplicativo hello em execução no computador de desenvolvimento (F5).
3. **Publicar o aplicativo hello** tooAzure em Olá maneira normal. 

*Como alternar o recurso de diferentes do Application Insights toosending tooa?*

* No Visual Studio, o projeto de Olá do botão direito do mouse, escolha **configurar o Application Insights** e escolha Olá recurso desejado. Você obtém Olá opção toocreate um novo recurso. Recompilar e reimplantar.

## <a name="explore-hello-data"></a>Explorar dados Olá
1. Na folha do Application Insights saudação do painel de controle de aplicativo web, você visualiza em métricas em tempo real, que mostra a falhas e solicitações em um segundo ou dois deles ocorrendo. É muito útil exibir quando você estiver republicando seu aplicativo – você poderá ver todos os problemas imediatamente.
2. Clique em toohello completo de recursos do Application Insights.

    ![Clique para o](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    Você também pode ir lá diretamente da navegação de recursos do Azure.

1. Clique nas tooget qualquer gráfico mais detalhes:
   
    ![Na folha de visão geral do Application Insights hello, clique em um gráfico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    Você pode [personalizar folhas de métricas](app-insights-metrics-explorer.md).
2. Clique nas mais toosee eventos individuais e suas propriedades:
   
    ![Clique em um tooopen de tipo de evento filtrada de uma pesquisa no tipo](./media/app-insights-azure-web-apps/08-requests.png)
   
    Observe que "…" hello link tooopen todas as propriedades.
   
    Você pode [personalizar pesquisas](app-insights-diagnostic-search.md).

Para pesquisas mais eficientes em sua telemetria, use Olá [linguagem de consulta de análise de Log](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Mais telemetria

* [Carregar dados da página da Web](app-insights-javascript.md)
* [Telemetria personalizada](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Próximas etapas
* [Executar o criador de perfil de saudação em seu live app](app-insights-profiler.md).
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) – monitorar o Azure Functions com o Application Insights
* [Habilitar o diagnóstico do Azure](app-insights-azure-diagnostics.md) tooApplication toobe enviado Insights.
* [Monitorar as métricas de integridade do serviço](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
* [Receba notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) sempre que ocorrerem eventos operacionais ou métricas ultrapassarem um limite.
* Use [Application Insights para páginas da web e aplicativos JavaScript](app-insights-javascript.md) tooget telemetria de cliente de navegadores Olá que visita uma página da web.
* [Configurar testes da web de disponibilidade](app-insights-monitor-web-app-availability.md) toobe alertado se seu site está inativo.

