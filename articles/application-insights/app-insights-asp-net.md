---
title: "aaaSet a análise de aplicativo web do ASP.NET com o Azure Application Insights | Microsoft Docs"
description: "Configurar análise de desempenho, disponibilidade e uso para seu site ASP.NET, hospedado no local ou no Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Configurar o Application Insights para seu site ASP.NET

Este procedimento configura o ASP.NET web aplicativo toosend telemetria toohello [Azure Application Insights](app-insights-overview.md) serviço. Ele funciona para aplicativos ASP.NET que estão hospedados em seu próprio servidor IIS ou na nuvem de saudação. Obter gráficos e uma linguagem de consulta eficiente que ajudam você entender o desempenho de saudação do aplicativo e quantas pessoas estão usando mais alertas automáticos falhas ou problemas de desempenho. Muitos desenvolvedores consideram esses recursos excelentes como estão, mas você também pode estender e personalizar a telemetria de saudação se for necessário.

A instalação leva apenas alguns cliques no Visual Studio. Você tem encargos de tooavoid opção Olá limitando volume Olá de telemetria. Isso permite que você tooexperiment e depuração ou toomonitor um site com não muitos usuários. Quando você decidir que deseja toogo em frente e monitorar o seu site de produção, é fácil tooraise limite de hello mais tarde.

## <a name="before-you-start"></a>Antes de começar
Você precisa de:

* Atualização 3 ou mais recente do Visual Studio 2013. Mais tarde é melhor.
* Uma assinatura muito[Microsoft Azure](http://azure.com). Se sua equipe ou organização tiver uma assinatura do Azure, Olá proprietário pode adicionar você tooit, usando o [conta da Microsoft](http://live.com).

Há tópicos alternativo toolook em se você estiver interessado em:

* [Instrumentar um aplicativo Web em tempo de execução](app-insights-monitor-performance-live-website-now.md)
* [Serviços de Nuvem do Azure](app-insights-cloudservices.md)

## <a name="ide"></a>Etapa 1: Adicionar Olá SDK do Application Insights

Clique com o botão direito do mouse no projeto de aplicativo Web no Gerenciador de Soluções e escolha **Adicionar** > **Application Insights Telemetry...** ou **Configurar o Application Insights**.

![Captura de tela do Gerenciador de soluções, com adicionar o Application Insights Telemetry realçado](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(No Visual Studio 2015, há também uma opção tooadd Application Insights na caixa de diálogo de novo projeto de saudação.)

Continue a página de configuração do Application Insights toohello:

![Captura de tela de registrar seu aplicativo com o Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Selecione a conta de saudação e assinatura que você use tooaccess do Azure.

**b.** Selecione o recurso de saudação do Azure onde deseja que os dados de saudação toosee de seu aplicativo. Normalmente:

* Use um [único recurso para diferentes componentes](app-insights-monitor-multi-role-apps.md) de um único aplicativo. 
* Crie recursos separados para aplicativos não relacionados.
 
Se você quiser tooset Olá Olá ou grupo local do recurso em que os dados estão armazenados, clique em **configurações**. Grupos de recursos são usados toocontrol toodata de acesso. Por exemplo, se você tiver vários aplicativos que fazem parte do hello mesmo sistema, você pode colocar seus dados do Application Insights hello mesmo grupo de recursos.

**c.** Defina um limite no limite de volume de dados livre hello, tooavoid encargos. O Application Insights é liberar tooa determinados volume de telemetria. Após Olá recurso for criado, você pode alterar sua seleção no portal de saudação abrindo **recursos + preços** > **gerenciamento do volume de dados** > **diário limite de volume**.

**d.** Clique em **registrar** toogo em frente e configurar o Application Insights para seu aplicativo web. Telemetria será enviada toohello [portal do Azure](https://portal.azure.com), durante a depuração e depois de publicar seu aplicativo.

**e.** Se você não quiser portal de toohello de telemetria toosend durante a depuração, basta adicionar Olá SDK do Application Insights tooyour aplicativo mas não configurar um recurso no portal de saudação. Você será capaz de toosee telemetria no Visual Studio enquanto você está depurando. Posteriormente, você pode retornar a página de configuração de toothis ou você pode esperar até depois de implantar seu aplicativo e [ative telemetria em tempo de execução](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a>Etapa 2: Executar seu aplicativo
Execute o aplicativo com F5. Abra páginas diferentes toogenerate alguns telemetria.

No Visual Studio, você vê uma contagem de eventos de saudação que foram registrados.

![Captura de tela do Visual Studio. botão do Application Insights Olá mostra durante a depuração.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Etapa 3: conferir sua telemetria
Você pode ver sua telemetria no Visual Studio ou no portal de web do Application Insights hello. Pesquisar telemetria no Visual Studio toohelp depurar seu aplicativo. Monitorar o desempenho e uso no portal da web de saudação quando o sistema está ativo. 

### <a name="see-your-telemetry-in-visual-studio"></a>Confira sua telemetria no Visual Studio

No Visual Studio, abra a janela do Application Insights Olá. Clique em Olá **Application Insights** botão ou em seu projeto no Gerenciador de soluções, selecione **Application Insights**e, em seguida, clique em **pesquisa Live telemetria**.

Na janela de pesquisa do Visual Studio Application Insights hello, consulte Olá **dados da sessão de depuração** exibição de telemetria gerada no lado do servidor de saudação do seu aplicativo. Fazer experiências com filtros de saudação e clique em qualquer evento toosee mais detalhes.

![Captura de tela de saudação de exibição de dados da sessão de depuração na janela do Application Insights hello.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Se você não vir todos os dados, certifique-se de intervalo de tempo de saudação está correto e clique Olá ícone de pesquisa.

[Saiba mais sobre as ferramentas do Application Insights no Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Conferir telemetria no portal da Web

Você também pode ver a telemetria no portal de web do Application Insights hello (a menos que você escolheu tooinstall somente Olá SDK). portal de saudação tem mais exibições de entre componentes do Visual Studio, ferramentas analíticas e gráficos. portal de saudação também fornece alertas.

Abra seu recurso do Application Insights. O entrar toohello [portal do Azure](https://portal.azure.com/) e localize-lo ou projeto de saudação do botão direito do mouse no Visual Studio e permitir que ele levá-lo lá.

![Captura de tela do Visual Studio, mostrando como tooopen Olá portal do Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Se você receber um erro de acesso: você tem mais de um conjunto de credenciais do Microsoft e você tiver entrado com conjunto errado Olá? No portal de hello, sair e entrar novamente.

portal de saudação é aberto em uma exibição de telemetria de saudação do seu aplicativo.

![Captura de tela da página de visão geral do Application Insights](./media/app-insights-asp-net/66.png)

No portal de hello, clique em qualquer bloco ou gráfico toosee mais detalhes.

[Saiba mais sobre como usar o Application Insights no portal do Azure de saudação](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Etapa 4: Publicar seu aplicativo
Publica seu servidor do IIS do aplicativo tooyour ou tooAzure. Inspecionar [fluxo ao vivo de métricas](app-insights-metrics-explorer.md#live-metrics-stream) toomake-se de que tudo está funcionando normalmente.

A telemetria cria no portal do Application Insights hello, onde você pode monitorar as métricas, pesquisar a telemetria e configurar [painéis](app-insights-dashboards.md). Você também pode usar Olá poderoso [linguagem de consulta de análise de Log](https://docs.loganalytics.io/) tooanalyze uso e desempenho ou toofind eventos específicos.

Você também pode continuar tooanalyze sua telemetria em [Visual Studio](app-insights-visual-studio.md), com ferramentas como pesquisa de diagnóstica e [tendências](app-insights-visual-studio-trends.md).

> [!NOTE]
> Se seu aplicativo envia suficiente Olá tooapproach de telemetria [limitação limites](app-insights-pricing.md#limits-summary)automática [amostragem](app-insights-sampling.md) switches em. Amostragem reduz a quantidade de saudação de telemetria enviada do seu aplicativo, preservando dados correlacionados para fins de diagnóstico.
>
>

## <a name="land"></a> Você está pronto

Parabéns! Você instalou o pacote do Application Insights Olá em seu aplicativo e ele toosend telemetria toohello Application Insights serviço configurado no Azure.

![Diagrama de movimentação de telemetria](./media/app-insights-asp-net/01-scheme.png)

Olá recursos do Azure que recebe a telemetria do aplicativo é identificado por um *chave de instrumentação*. Você encontrará esta chave no arquivo applicationinsights. config de saudação.


## <a name="upgrade-toofuture-sdk-versions"></a>Atualizar versões SDK toofuture
tooupgrade tooa [nova versão do SDK do hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), abra Olá **Gerenciador de pacotes do NuGet** novamente e o filtro de pacotes instalados. Selecione **Microsoft.ApplicationInsights.Web** e escolha **Atualizar**.

Se você fez tooApplicationInsights.config quaisquer personalizações, salve uma cópia dele antes de atualizar. Em seguida, mescle suas alterações na nova versão de hello.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Próximas etapas

### <a name="more-telemetry"></a>Mais telemetria

* **[Navegador e página carregam dados](app-insights-javascript.md)**  -insira um trecho de código em suas páginas da Web.
* **[Obtenha monitoramento de dependência e de exceção mais detalhado](app-insights-monitor-performance-live-website-now.md)**  -instale o Monitor de Status no seu servidor.
* **[Eventos personalizados de código](app-insights-api-custom-events-metrics.md)**  toocount, hora ou medir a ações do usuário.
* **[Obter dados de log](app-insights-asp-net-trace-logs.md)**  - correlacionar dados de log com a telemetria.

### <a name="analysis"></a>Análise

* **[Trabalhar com o Application Insights no Visual Studio](app-insights-visual-studio.md)**<br/>Inclui informações sobre como depurar com a telemetria, pesquisa de diagnóstica e drill-through toocode.
* **[Trabalhando com o portal do Application Insights Olá](app-insights-dashboards.md)**<br/> Inclui informações sobre painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e a exportação de telemetria.
* **[Análise de](app-insights-analytics-tour.md)**  -Olá poderosa linguagem de consulta.

### <a name="alerts"></a>Alertas

* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md): criar testes toomake se seu site está visível na web hello.
* [Inteligente diagnóstico](app-insights-proactive-diagnostics.md): esses testes são executados automaticamente, para que você não tenha toodo nada tooset-los para cima. Eles informam se o aplicativo tem uma taxa incomum de solicitações com falha.
* [Alertas de métrica](app-insights-alerts.md): definir esses toowarn se uma métrica exceder um limite. Você pode defini-los em métricas personalizadas que você codifica em seu aplicativo.

### <a name="automation"></a>Automação

* [Automatizar a criação de um recurso adicional do Application Insights](app-insights-powershell.md)
