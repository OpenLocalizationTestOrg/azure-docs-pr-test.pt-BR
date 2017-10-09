---
title: "aaaApplication aplicativos que já estão em tempo real de web do Insights para Java"
description: "Comece a monitorar um aplicativo Web que já esteja em execução no servidor"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights para aplicativos Web Java que já estão em modo dinâmico


Se você tiver um aplicativo web que já está em execução no servidor J2EE, você pode iniciar o monitoramento com [Application Insights](app-insights-overview.md) sem Olá necessário toomake alterações de código ou recompile seu projeto. Com essa opção, é possível obter informações sobre solicitações HTTP enviadas tooyour servidor, exceções sem tratamento e contadores de desempenho.

Você terá uma assinatura muito[Microsoft Azure](https://azure.com).

> [!NOTE]
> procedimento de saudação nesta página adiciona Olá SDK tooyour web aplicativo em tempo de execução. A instrumentação de tempo de execução é útil se você não deseja tooupdate ou recriar seu código-fonte. Mas, se possível, recomendamos que você [adicionar código-fonte SDK Olá toohello](app-insights-java-get-started.md) em vez disso. Que fornece a você mais opções de como escrever código tootrack usuário atividade.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Obter uma chave de instrumentação do Application Insights
1. Entrar toohello [portal do Microsoft Azure](https://portal.azure.com)
2. Criar um novo recurso do Application Insights e defina o aplicativo de web tooJava do tipo de aplicativo hello.
   
    ![Preencha um nome, escolha o aplicativo Java da Web e clique em Criar](./media/app-insights-java-live/02-create.png)

    Olá recurso é criado em alguns segundos.

4. Abra o novo recurso de saudação e obter sua chave de instrumentação. Você precisará toopaste essa chave em seu projeto de código em breve.
   
    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Baixe o SDK de saudação
1. Baixar Olá [SDK do Application Insights para Java](https://aka.ms/aijavasdk). 
2. No servidor, extrai diretório Olá SDK conteúdo toohello do qual seus binários de projeto são carregados. Se você estiver usando o Tomcat, esse diretório normalmente estará em `webapps/<your_app_name>/WEB-INF/lib`

Observe que você precisa toorepeat isso em cada instância de servidor e para cada aplicativo.

## <a name="3-add-an-application-insights-xml-file"></a>3. Adicione um arquivo xml do Application Insights
Crie ApplicationInsights.xml na pasta Olá no qual você adicionou Olá SDK. Colocar nele Olá XML a seguir.

Substitua a chave de instrumentação Olá que você obteve Olá portal do Azure.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* chave de instrumentação de saudação enviada juntamente com todos os itens de telemetria e informa ao Application Insights toodisplay-lo em seu recurso.
* Olá componente de solicitação HTTP é opcional. Ele envia automaticamente telemetria sobre solicitações e o portal de toohello de tempos de resposta.
* Correlação de eventos é um componente de solicitação HTTP de toohello de adição. Ele atribui uma solicitação de tooeach identificador recebida pelo servidor de saudação e adiciona esse identificador como um item de tooevery de propriedade de telemetria como propriedade Olá 'Operation.Id'. Ele permite toocorrelate telemetria de saudação associada com cada solicitação, definindo um filtro no [pesquisa diagnóstica](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Adicionar um filtro HTTP
Localize e abra o arquivo Web. XML de saudação em seu projeto e saudação de mesclagem após o trecho de código no nó de aplicativo web hello, onde os filtros de aplicativo estão configurados.

resultados mais precisos tooget hello, filtro Olá devem ser mapeados antes de todos os outros filtros.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a>5. Verificar exceções do firewall
Talvez seja necessário muito[definir exceções dados de saída toosend](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Reiniciar seu aplicativo Web
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Exibir sua telemetria no Application Insights
Retornar recurso Application Insights tooyour [portal do Microsoft Azure](https://portal.azure.com).

Telemetria sobre solicitações HTTP é exibida na folha de visão geral de saudação. (Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)

![dados de exemplo](./media/app-insights-java-live/5-results.png)

Clique em por meio de qualquer gráfico toosee métricas mais detalhadas. 

![](./media/app-insights-java-live/6-barchart.png)

E, ao exibir as propriedades de saudação de uma solicitação, você pode ver eventos de telemetria Olá associados a ele, como solicitações e exceções.

![](./media/app-insights-java-live/7-instance.png)

[Saiba mais sobre métricas.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Próximas etapas
* [Adicionar páginas da web a telemetria tooyour](app-insights-javascript.md) toomonitor página exibições e métricas de usuário.
* [Configurar testes da web](app-insights-monitor-web-app-availability.md) toomake-se de que seu aplicativo permanece em tempo real e responsivo.
* [Capturar rastreamentos de log](app-insights-java-trace-logs.md)
* [Pesquisar eventos e logs](app-insights-diagnostic-search.md) toohelp diagnosticar problemas.

