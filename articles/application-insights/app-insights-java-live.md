---
title: "Application Insights para aplicativos Web Java que já estão em modo dinâmico"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="44fc3-103">Application Insights para aplicativos Web Java que já estão em modo dinâmico</span><span class="sxs-lookup"><span data-stu-id="44fc3-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="44fc3-104">Se tiver um aplicativo Web já em execução no servidor J2EE, você poderá começar a monitorá-lo com o [Application Insights](app-insights-overview.md) sem a necessidade de fazer alterações de código ou recompilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="44fc3-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="44fc3-105">Com essa opção, você obtém informações sobre solicitações HTTP enviadas ao seu servidor, exceções sem tratamento e contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="44fc3-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="44fc3-106">Você precisará de uma assinatura do [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="44fc3-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="44fc3-107">O procedimento nesta página adiciona o SDK ao seu aplicativo Web no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="44fc3-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="44fc3-108">Essa instrumentação de tempo de execução será útil se você não quiser atualizar nem recompilar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="44fc3-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="44fc3-109">Mas, se possível, recomendamos que você [adicione o SDK para o código-fonte](app-insights-java-get-started.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="44fc3-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="44fc3-110">Isso dá mais opções, como escrever o código para rastrear a atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="44fc3-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="44fc3-111">1. Obter uma chave de instrumentação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="44fc3-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="44fc3-112">Entre no [Portal do Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="44fc3-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="44fc3-113">Crie um novo recurso do Application Insights e defina o tipo de aplicativo para aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="44fc3-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Preencha um nome, escolha o aplicativo Java da Web e clique em Criar](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="44fc3-115">O recurso é criado em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="44fc3-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="44fc3-116">Abr o novo recurso e obtenha sua chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="44fc3-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="44fc3-117">Você precisará colar essa chave no código de seu projeto em breve.</span><span class="sxs-lookup"><span data-stu-id="44fc3-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![Na visão geral do novo recurso, clique em Propriedades e copie a chave de instrumentação](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="44fc3-119">2. Baixar o SDK</span><span class="sxs-lookup"><span data-stu-id="44fc3-119">2. Download the SDK</span></span>
1. <span data-ttu-id="44fc3-120">Baixe o [SDK do Application Insights para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="44fc3-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="44fc3-121">No servidor, extraia o conteúdo do SDK para o diretório por meio do qual os binários do projeto são carregados.</span><span class="sxs-lookup"><span data-stu-id="44fc3-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="44fc3-122">Se você estiver usando o Tomcat, esse diretório normalmente estará em `webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="44fc3-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="44fc3-123">Observe que você precisa repetir isso em cada instância do servidor e para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44fc3-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="44fc3-124">3. Adicione um arquivo xml do Application Insights</span><span class="sxs-lookup"><span data-stu-id="44fc3-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="44fc3-125">Crie o ApplicationInsights.xml na pasta em que você adicionou o SDK.</span><span class="sxs-lookup"><span data-stu-id="44fc3-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="44fc3-126">Coloque dentro dela o XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="44fc3-126">Put into it the following XML.</span></span>

<span data-ttu-id="44fc3-127">Substitua a chave de instrumentação que você obteve no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44fc3-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="44fc3-128">A chave de instrumentação é enviada junto com todos os itens de telemetria e orienta o Application Insights a exibi-los em seu recurso.</span><span class="sxs-lookup"><span data-stu-id="44fc3-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="44fc3-129">O componente de solicitação HTTP é opcional.</span><span class="sxs-lookup"><span data-stu-id="44fc3-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="44fc3-130">Ele envia automaticamente a telemetria sobre solicitações e tempos de resposta para o portal.</span><span class="sxs-lookup"><span data-stu-id="44fc3-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="44fc3-131">A correlação de eventos é uma adição ao componente de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="44fc3-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="44fc3-132">Ele atribui um identificador a cada solicitação recebida pelo servidor e adiciona esse identificador como uma propriedade para cada item de telemetria, como a propriedade “Operation.Id”.</span><span class="sxs-lookup"><span data-stu-id="44fc3-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="44fc3-133">Ele permite que você correlacione a telemetria associada com cada solicitação, definindo um filtro na [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="44fc3-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="44fc3-134">4. Adicionar um filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="44fc3-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="44fc3-135">Localize e abra o arquivo web.xml em seu projeto, então mescle o trecho de código a seguir sob o nó do aplicativo Web, no qual seus filtros de aplicativo estão configurados.</span><span class="sxs-lookup"><span data-stu-id="44fc3-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="44fc3-136">Para obter os resultados mais precisos, o filtro deve ser mapeado antes de todos os outros filtros.</span><span class="sxs-lookup"><span data-stu-id="44fc3-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="44fc3-137">5. Verificar exceções do firewall</span><span class="sxs-lookup"><span data-stu-id="44fc3-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="44fc3-138">Talvez você precise [definir exceções de firewall para enviar dados de saída](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="44fc3-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="44fc3-139">6. Reiniciar seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="44fc3-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="44fc3-140">7. Exibir sua telemetria no Application Insights</span><span class="sxs-lookup"><span data-stu-id="44fc3-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="44fc3-141">Retorne para seu recurso do Application Insights no [Portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44fc3-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="44fc3-142">A telemetria de solicitações HTTP é exibida na folha de visão geral.</span><span class="sxs-lookup"><span data-stu-id="44fc3-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="44fc3-143">(Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)</span><span class="sxs-lookup"><span data-stu-id="44fc3-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dados de exemplo](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="44fc3-145">Clique em qualquer gráfico para ver métricas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="44fc3-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="44fc3-146">Ao exibir as propriedades de uma solicitação, você pode ver os eventos de telemetria associados a ela, como solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="44fc3-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="44fc3-147">Saiba mais sobre métricas.</span><span class="sxs-lookup"><span data-stu-id="44fc3-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="44fc3-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44fc3-148">Next steps</span></span>
* <span data-ttu-id="44fc3-149">[Adicione telemetria às suas páginas da Web](app-insights-javascript.md) para monitorar exibições de página e métricas de usuário.</span><span class="sxs-lookup"><span data-stu-id="44fc3-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="44fc3-150">[Configure os testes da Web](app-insights-monitor-web-app-availability.md) para certificar-se de manter seu aplicativo operante e responsivo.</span><span class="sxs-lookup"><span data-stu-id="44fc3-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="44fc3-151">Capturar rastreamentos de log</span><span class="sxs-lookup"><span data-stu-id="44fc3-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="44fc3-152">[Pesquise eventos e logs](app-insights-diagnostic-search.md) para ajudar a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="44fc3-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

