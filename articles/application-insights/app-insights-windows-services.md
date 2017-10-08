---
title: "as funções de servidor e de trabalho de Insights do aplicativo para Windows aaaAzure | Microsoft Docs"
description: Adicione manualmente o desempenho, disponibilidade e uso de tooanalyze de aplicativo hello SDK do Application Insights tooyour ASP.NET.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Configurar manualmente o Application Insights para aplicativos .NET

Você pode configurar [Application Insights](app-insights-overview.md) toomonitor uma ampla variedade de aplicativos ou funções de aplicativo, componentes ou microservices. Para aplicativos Web e serviços, o Visual Studio oferece [configuração em uma etapa](app-insights-asp-net.md). Para outros tipos de aplicativos .NET, como funções de servidor de back-end ou aplicativos de área de trabalho, você pode configurar o Application Insights manualmente.

![Gráficos de exemplo de monitoramento de desempenho](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Antes de começar

Você precisa de:

* Uma assinatura muito[Microsoft Azure](http://azure.com). Se sua equipe ou organização tiver uma assinatura do Azure, Olá proprietário pode adicionar tooit, usando o [conta da Microsoft](http://live.com).
* Visual Studio 2013 ou posterior.

## <a name="add"></a>1. Escolher um recurso Application Insights

Olá 'recurso' é onde os dados são coletados e exibidos no portal do Azure de saudação. Se precisar toodecide toocreate um novo, ou compartilhar uma existente.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Parte de um aplicativo maior: usar o recurso existente

Se seu aplicativo da web tem vários componentes - por exemplo, um aplicativo web front-end e um ou mais serviços de back-end - em seguida, você deve enviar telemetria de todos os toohello de componentes de saudação mesmo recurso. Isso habilitá-las toobe exibido em um mapa de aplicativo único e torná-lo possível tootrace uma solicitação de um componente tooanother.

Portanto, se você já estiver monitorando outros componentes deste aplicativo, em seguida, basta usar Olá mesmo recurso.

Abrir o recurso de saudação em Olá [portal do Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Aplicativo independente: criar um novo recurso

Se aplicativos tooother relacionados Olá novo aplicativo, ele deve ter seu próprio recurso.

Entrar toohello [portal do Azure](https://portal.azure.com/)e criar um novo recurso do Application Insights. Escolha o ASP.NET como o tipo de aplicativo hello.

![Clique em Novo, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

Escolha de saudação do tipo de aplicativo define o conteúdo de padrão de saudação de folhas de recurso hello.

## <a name="2-copy-hello-instrumentation-key"></a>2. Copiar Olá chave de instrumentação
chave de saudação identifica o recurso de saudação. Você vai instalá-lo em breve no hello SDK, no recurso de toohello ordem toodirect dados.

![Clique em propriedades, selecione a chave de saudação e pressione ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Instalar o pacote do Application Insights de saudação em seu aplicativo
Instalando e configurando Olá Application Insights pacote varia dependendo plataforma Olá que você está trabalhando. 

1. No Visual Studio, clique com o botão direito do mouse em seu projeto e escolha **Gerenciar pacotes NuGet**.
   
    ![Clique com botão direito hello e selecione Gerenciar pacotes Nuget](./media/app-insights-windows-services/03-nuget.png)
2. Instalar o pacote do Application Insights Olá para aplicativos do Windows server, "Microsoft.ApplicationInsights.WindowsServer".
   
    ![Pesquise “Application Insights”](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Qual versão?*

    Verificar **incluir pré-lançamento** se você quiser tootry nossos recursos mais recentes. documentos relevantes Hello ou blogs Observe se você precisa de uma versão de pré-lançamento.
    
    *É possível usar outros pacotes?*
   
    Sim. Escolha "Microsoft.ApplicationInsights" se quiser apenas toouse Olá API toosend sua telemetria. pacote do Windows Server Olá inclui Olá API mais um número de outros pacotes, como a coleta do contador de desempenho e monitoramento de dependência. 

### <a name="tooupgrade-toofuture-package-versions"></a>versões do pacote toofuture tooupgrade
Podemos lançar uma nova versão do hello SDK de tootime de tempo.

tooupgrade tooa [nova versão do pacote de saudação](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), abra o Gerenciador de pacotes do NuGet e filtrar pacotes instalados. Selecione **Microsoft.ApplicationInsights.WindowsServer** e **Atualizar**.

Se você fez tooApplicationInsights.config quaisquer personalizações, salve uma cópia dele antes de atualizar e posteriormente mesclar suas alterações na nova versão de hello.

## <a name="4-send-telemetry"></a>4. Enviar telemetria
**Se você instalou somente o pacote hello API:**

* Defina a chave de instrumentação Olá no código, por exemplo `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *sua chave* `";` 
* [Gravar seu próprio telemetria usando a API de saudação](app-insights-api-custom-events-metrics.md#ikey).

**Se você tiver instalado outros pacotes do Application Insights,** você pode usar de se você preferir, chave de instrumentação de Olá Olá. config arquivo tooset:

* Edite applicationinsights. config (que foi adicionado pelo Olá instalar NuGet). Coloque-a antes Olá marca de fechamento:
  
    `<InstrumentationKey>`*chave de instrumentação Olá copiado*`</InstrumentationKey>`
* Certifique-se de que Olá definir propriedades de applicationinsights. config no Solution Explorer são muito**Build Action = conteúdo, cópia tooOutput Directory = copiar**.

É chave de instrumentação Olá tooset úteis no código se você quiser muito[comutador hello chave para as configurações de compilação diferente](app-insights-separate-resources.md). Se você definir a chave de saudação no código, você não tem tooset no hello `.config` arquivo.

## <a name="run"></a> Execute seu projeto
Saudação de uso **F5** toorun seu aplicativo e experimente-o: abrir diferente páginas toogenerate alguns telemetria.

No Visual Studio, você verá uma contagem de eventos de saudação que foram enviadas.

![Contagem de eventos no Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Exibir sua telemetria
Retornar toohello [portal do Azure](https://portal.azure.com/) e procure o recurso do Application Insights tooyour.

Procure dados em gráficos de visão geral de saudação. Primeiro, você apenas verá um ou dois pontos. Por exemplo:

![Clicar em dados toomore](./media/app-insights-windows-services/12-first-perf.png)

Clique em por meio de qualquer gráfico toosee métricas mais detalhadas. [Saiba mais sobre métricas.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Não há dados?
* Use o aplicativo hello, páginas diferentes de abertura para que ele gera algumas telemetria.
* Olá abrir [pesquisa](app-insights-diagnostic-search.md) bloco eventos individuais toosee. Às vezes é preciso eventos tooget um pouco enquanto mais por meio do pipeline de métricas de saudação.
* Aguarde alguns segundos e clique em **Atualizar**. Gráficos de se atualizar periodicamente, mas você pode atualizar manualmente, se você estiver esperando por tooshow alguns dados para cima.
* Consulte [Solucionar problemas](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Publicar seu aplicativo
Agora, implante aplicativos tooyour servidor ou Olá tooAzure e inspecionar dados acumulam.

![Usar o Visual Studio toopublish seu aplicativo](./media/app-insights-windows-services/15-publish.png)

Quando você executa em modo de depuração, telemetria é acelerada por meio do pipeline Olá, para que você deve ver os dados que aparecem dentro de segundos. Quando você implanta seu aplicativo na configuração de Versão, os dados acumulam mais lentamente.

### <a name="no-data-after-you-publish-tooyour-server"></a>Nenhum dado após a publicação de servidor tooyour?
Abra estas portas para tráfego de saída no firewall do servidor. Consulte [essa página](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) para lista de saudação de endereços necessários 

### <a name="trouble-on-your-build-server"></a>Problemas no servidor de compilação?
Consulte [este item de solução de problemas](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Se seu aplicativo gera um lote de telemetria, módulo de amostragem adaptável Olá automaticamente reduzirá o volume Olá enviada toohello portal enviando apenas uma fração representativa de eventos. No entanto, eventos que são relacionada toohello mesma solicitação será marcada ou desmarcada como um grupo, para que você possa navegar entre eventos relacionados. 
> [Saiba mais sobre amostragem](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Próximas etapas
* [Adicionar telemetria mais](app-insights-asp-net-more.md) tooget Olá visão de 360 graus completo do seu aplicativo.

