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
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="cad22-103">Application Insights para aplicativos Web Java que já estão em modo dinâmico</span><span class="sxs-lookup"><span data-stu-id="cad22-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="cad22-104">Se você tiver um aplicativo web que já está em execução no servidor J2EE, você pode iniciar o monitoramento com [Application Insights](app-insights-overview.md) sem Olá necessário toomake alterações de código ou recompile seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cad22-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="cad22-105">Com essa opção, é possível obter informações sobre solicitações HTTP enviadas tooyour servidor, exceções sem tratamento e contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="cad22-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="cad22-106">Você terá uma assinatura muito[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="cad22-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="cad22-107">procedimento de saudação nesta página adiciona Olá SDK tooyour web aplicativo em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cad22-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="cad22-108">A instrumentação de tempo de execução é útil se você não deseja tooupdate ou recriar seu código-fonte.</span><span class="sxs-lookup"><span data-stu-id="cad22-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="cad22-109">Mas, se possível, recomendamos que você [adicionar código-fonte SDK Olá toohello](app-insights-java-get-started.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="cad22-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="cad22-110">Que fornece a você mais opções de como escrever código tootrack usuário atividade.</span><span class="sxs-lookup"><span data-stu-id="cad22-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="cad22-111">1. Obter uma chave de instrumentação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="cad22-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="cad22-112">Entrar toohello [portal do Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="cad22-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="cad22-113">Criar um novo recurso do Application Insights e defina o aplicativo de web tooJava do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cad22-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Preencha um nome, escolha o aplicativo Java da Web e clique em Criar](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="cad22-115">Olá recurso é criado em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="cad22-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="cad22-116">Abra o novo recurso de saudação e obter sua chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="cad22-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="cad22-117">Você precisará toopaste essa chave em seu projeto de código em breve.</span><span class="sxs-lookup"><span data-stu-id="cad22-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="cad22-119">2. Baixe o SDK de saudação</span><span class="sxs-lookup"><span data-stu-id="cad22-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="cad22-120">Baixar Olá [SDK do Application Insights para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="cad22-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="cad22-121">No servidor, extrai diretório Olá SDK conteúdo toohello do qual seus binários de projeto são carregados.</span><span class="sxs-lookup"><span data-stu-id="cad22-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="cad22-122">Se você estiver usando o Tomcat, esse diretório normalmente estará em `webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="cad22-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="cad22-123">Observe que você precisa toorepeat isso em cada instância de servidor e para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cad22-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="cad22-124">3. Adicione um arquivo xml do Application Insights</span><span class="sxs-lookup"><span data-stu-id="cad22-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="cad22-125">Crie ApplicationInsights.xml na pasta Olá no qual você adicionou Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="cad22-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="cad22-126">Colocar nele Olá XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="cad22-126">Put into it hello following XML.</span></span>

<span data-ttu-id="cad22-127">Substitua a chave de instrumentação Olá que você obteve Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cad22-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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

* <span data-ttu-id="cad22-128">chave de instrumentação de saudação enviada juntamente com todos os itens de telemetria e informa ao Application Insights toodisplay-lo em seu recurso.</span><span class="sxs-lookup"><span data-stu-id="cad22-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="cad22-129">Olá componente de solicitação HTTP é opcional.</span><span class="sxs-lookup"><span data-stu-id="cad22-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="cad22-130">Ele envia automaticamente telemetria sobre solicitações e o portal de toohello de tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="cad22-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="cad22-131">Correlação de eventos é um componente de solicitação HTTP de toohello de adição.</span><span class="sxs-lookup"><span data-stu-id="cad22-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="cad22-132">Ele atribui uma solicitação de tooeach identificador recebida pelo servidor de saudação e adiciona esse identificador como um item de tooevery de propriedade de telemetria como propriedade Olá 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="cad22-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="cad22-133">Ele permite toocorrelate telemetria de saudação associada com cada solicitação, definindo um filtro no [pesquisa diagnóstica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="cad22-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="cad22-134">4. Adicionar um filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="cad22-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="cad22-135">Localize e abra o arquivo Web. XML de saudação em seu projeto e saudação de mesclagem após o trecho de código no nó de aplicativo web hello, onde os filtros de aplicativo estão configurados.</span><span class="sxs-lookup"><span data-stu-id="cad22-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="cad22-136">resultados mais precisos tooget hello, filtro Olá devem ser mapeados antes de todos os outros filtros.</span><span class="sxs-lookup"><span data-stu-id="cad22-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="cad22-137">5. Verificar exceções do firewall</span><span class="sxs-lookup"><span data-stu-id="cad22-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="cad22-138">Talvez seja necessário muito[definir exceções dados de saída toosend](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="cad22-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="cad22-139">6. Reiniciar seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="cad22-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="cad22-140">7. Exibir sua telemetria no Application Insights</span><span class="sxs-lookup"><span data-stu-id="cad22-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="cad22-141">Retornar recurso Application Insights tooyour [portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cad22-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="cad22-142">Telemetria sobre solicitações HTTP é exibida na folha de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="cad22-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="cad22-143">(Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)</span><span class="sxs-lookup"><span data-stu-id="cad22-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dados de exemplo](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="cad22-145">Clique em por meio de qualquer gráfico toosee métricas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cad22-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="cad22-146">E, ao exibir as propriedades de saudação de uma solicitação, você pode ver eventos de telemetria Olá associados a ele, como solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="cad22-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="cad22-147">Saiba mais sobre métricas.</span><span class="sxs-lookup"><span data-stu-id="cad22-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="cad22-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cad22-148">Next steps</span></span>
* <span data-ttu-id="cad22-149">[Adicionar páginas da web a telemetria tooyour](app-insights-javascript.md) toomonitor página exibições e métricas de usuário.</span><span class="sxs-lookup"><span data-stu-id="cad22-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="cad22-150">[Configurar testes da web](app-insights-monitor-web-app-availability.md) toomake-se de que seu aplicativo permanece em tempo real e responsivo.</span><span class="sxs-lookup"><span data-stu-id="cad22-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="cad22-151">Capturar rastreamentos de log</span><span class="sxs-lookup"><span data-stu-id="cad22-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="cad22-152">[Pesquisar eventos e logs](app-insights-diagnostic-search.md) toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="cad22-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

