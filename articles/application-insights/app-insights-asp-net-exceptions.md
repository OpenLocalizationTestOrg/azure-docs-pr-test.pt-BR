---
title: "Diagnosticar falhas e exceções em aplicativos Web com o Azure Application Insights | Microsoft Docs"
description: "Capture exceções de aplicativos do ASP.NET junto com a telemetria de solicitação."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="f2555-103">Diagnosticar exceções em seus aplicativos Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="f2555-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="f2555-104">Exceções em seu aplicativo Web ao vivo são relatadas pelo [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2555-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f2555-105">Você pode correlacionar solicitações com falha com exceções e outros eventos no cliente e no servidor, para poder diagnosticar as causas rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f2555-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="f2555-106">Configurar os relatórios de exceção</span><span class="sxs-lookup"><span data-stu-id="f2555-106">Set up exception reporting</span></span>
* <span data-ttu-id="f2555-107">Para que as exceções sejam relatadas em seu aplicativo de servidor:</span><span class="sxs-lookup"><span data-stu-id="f2555-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="f2555-108">Instale o[ SDK do Application Insights](app-insights-asp-net.md) no aplicativo ou</span><span class="sxs-lookup"><span data-stu-id="f2555-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="f2555-109">Servidores Web IIS: executar o [Agente do Application Insights](app-insights-monitor-performance-live-website-now.md) ou</span><span class="sxs-lookup"><span data-stu-id="f2555-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="f2555-110">Aplicativos Web do Azure: adicionar a [extensão do Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="f2555-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="f2555-111">Aplicativos Web Java: instalar o [Agente Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="f2555-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="f2555-112">Instale o [trecho de JavaScript](app-insights-javascript.md) em suas páginas da Web para capturar exceções de navegador.</span><span class="sxs-lookup"><span data-stu-id="f2555-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="f2555-113">Em algumas estruturas de aplicativo ou com algumas configurações, você precisa executar algumas etapas adicionais para capturar mais exceções:</span><span class="sxs-lookup"><span data-stu-id="f2555-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="f2555-114">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="f2555-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="f2555-115">MVC</span><span class="sxs-lookup"><span data-stu-id="f2555-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="f2555-116">API Web 1.*</span><span class="sxs-lookup"><span data-stu-id="f2555-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="f2555-117">API Web 2.*</span><span class="sxs-lookup"><span data-stu-id="f2555-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="f2555-118">WCF</span><span class="sxs-lookup"><span data-stu-id="f2555-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="f2555-119">Diagnosticar exceções usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2555-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="f2555-120">Abra a solução do aplicativo no Visual Studio para ajudar com a depuração.</span><span class="sxs-lookup"><span data-stu-id="f2555-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="f2555-121">Execute o aplicativo, em seu servidor ou na máquina de desenvolvimento, usando F5.</span><span class="sxs-lookup"><span data-stu-id="f2555-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="f2555-122">Abra a janela Pesquisa do Application Insights no Visual Studio e configure-a para exibir eventos de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2555-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="f2555-123">Durante a depuração, você pode fazer isso clicando no botão Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f2555-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Clique com o botão direito no projeto e escolha Application Insights, Abrir.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="f2555-125">Observe que você pode filtrar o relatório para mostrar apenas as exceções.</span><span class="sxs-lookup"><span data-stu-id="f2555-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="f2555-126">*Nenhuma exceção mostrando? Consulte [Capturar exceções](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="f2555-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="f2555-127">Clique em um relatório de exceções para mostrar o rastreamento de pilha.</span><span class="sxs-lookup"><span data-stu-id="f2555-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="f2555-128">Clique em uma referência de linha no rastreamento de pilha para abrir o arquivo de código relevante.</span><span class="sxs-lookup"><span data-stu-id="f2555-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="f2555-129">No código, observe que o CodeLens mostra dados sobre as exceções:</span><span class="sxs-lookup"><span data-stu-id="f2555-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![Notificação de exceções do CodeLens.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="f2555-131">Como diagnosticar falhas usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f2555-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="f2555-132">Na visão geral do Application Insights de seu aplicativo, o bloco Falhas mostra gráficos de exceções e solicitações HTTP, juntamente com uma lista da solicitação com falha URLs que causam as falhas mais frequentes.</span><span class="sxs-lookup"><span data-stu-id="f2555-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Escolha Configurações, Falhas.](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="f2555-134">Clique em um dos tipos de exceção com falha na lista para obter as ocorrências individuais da exceção, em que é possível ver os detalhes e o rastreamento de pilha:</span><span class="sxs-lookup"><span data-stu-id="f2555-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Selecione uma instância de uma solicitação com falha e, em detalhes da exceção, obtenha a instâncias da exceção.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="f2555-136">**Como alternativa,** você pode começar na lista de solicitações e encontrar exceções relacionadas a ela.</span><span class="sxs-lookup"><span data-stu-id="f2555-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="f2555-137">*Nenhuma exceção mostrando? Consulte [Capturar exceções](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="f2555-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="f2555-138">Dados personalizados de rastreamento e log</span><span class="sxs-lookup"><span data-stu-id="f2555-138">Custom tracing and log data</span></span>
<span data-ttu-id="f2555-139">Para obter dados de diagnóstico específicos do aplicativo, você pode inserir código para enviar seus próprios dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="f2555-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="f2555-140">Eles são exibidos na pesquisa de diagnóstico junto com a solicitação, exibição de página e outros dados coletados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f2555-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="f2555-141">Você tem várias opções:</span><span class="sxs-lookup"><span data-stu-id="f2555-141">You have several options:</span></span>

* <span data-ttu-id="f2555-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) normalmente é usado para monitorar padrões de uso, mas os dados que ele envia também aparecem em Eventos Personalizados na pesquisa de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f2555-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="f2555-143">Os eventos são nomeados e podem conter propriedades de cadeia de caracteres e métricas numéricas nas quais é possível [filtrar pesquisas de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="f2555-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="f2555-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) permite que você envie dados mais longos, como informações POST.</span><span class="sxs-lookup"><span data-stu-id="f2555-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="f2555-145">[TrackException()](#exceptions) envia rastreamentos de pilha.</span><span class="sxs-lookup"><span data-stu-id="f2555-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="f2555-146">[Mais sobre exceções](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="f2555-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="f2555-147">Se você já usa uma estrutura de registros, como Log4Net ou NLog poderá [capturar esses logs](app-insights-asp-net-trace-logs.md) e vê-los na pesquisa de diagnóstico junto com os dados de solicitação e exceção.</span><span class="sxs-lookup"><span data-stu-id="f2555-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="f2555-148">Para ver esses eventos, abra [Pesquisar](app-insights-diagnostic-search.md), abra Filtrar e escolha Evento Personalizado, Rastreamento ou Exceção.</span><span class="sxs-lookup"><span data-stu-id="f2555-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Drill-through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="f2555-150">Se o seu aplicativo gerar muita telemetria, o módulo de amostragem adaptável reduzirá automaticamente o volume enviado ao portal, enviando apenas uma fração representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="f2555-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="f2555-151">Os eventos que fazem parte da mesma operação serão selecionados ou desmarcados como um grupo, para que você possa navegar entre os eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f2555-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="f2555-152">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="f2555-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="f2555-153">Como consultar dados POST de solicitação</span><span class="sxs-lookup"><span data-stu-id="f2555-153">How to see request POST data</span></span>
<span data-ttu-id="f2555-154">Os detalhes da solicitação não incluem os dados enviados ao seu aplicativo em uma chamada POST.</span><span class="sxs-lookup"><span data-stu-id="f2555-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="f2555-155">Para que esses dados sejam relatados:</span><span class="sxs-lookup"><span data-stu-id="f2555-155">To have this data reported:</span></span>

* <span data-ttu-id="f2555-156">[Instale o SDK](app-insights-asp-net.md) no projeto do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2555-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="f2555-157">Insira o código no seu aplicativo para chamar [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="f2555-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="f2555-158">Envie os dados de POST no parâmetro de mensagem.</span><span class="sxs-lookup"><span data-stu-id="f2555-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="f2555-159">Há um limite para o tamanho permitido, portanto você deve tentar enviar somente os dados essenciais.</span><span class="sxs-lookup"><span data-stu-id="f2555-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="f2555-160">Quando você investiga uma solicitação com falha, localize os rastreamentos associados.</span><span class="sxs-lookup"><span data-stu-id="f2555-160">When you investigate a failed request, find the associated traces.</span></span>  

![Drill-through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="f2555-162"><a name="exceptions"></a> Capturando exceções e dados de diagnóstico relacionados</span><span class="sxs-lookup"><span data-stu-id="f2555-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="f2555-163">No início você não verá no portal todas as exceções que causam falhas em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2555-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="f2555-164">Você verá quaisquer exceções do navegador (se você estiver usando o [SDK do JavaScript](app-insights-javascript.md) nas páginas da Web).</span><span class="sxs-lookup"><span data-stu-id="f2555-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="f2555-165">Mas a maioria das exceções de servidor são capturados pelo IIS e é preciso escrever um pouco de código para vê-los.</span><span class="sxs-lookup"><span data-stu-id="f2555-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="f2555-166">Você pode:</span><span class="sxs-lookup"><span data-stu-id="f2555-166">You can:</span></span>

* <span data-ttu-id="f2555-167">**Registrar as exceções explicitamente** inserindo código em manipuladores de exceção para relatar as exceções.</span><span class="sxs-lookup"><span data-stu-id="f2555-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="f2555-168">**Capturar exceções automaticamente** configurando sua estrutura do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f2555-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="f2555-169">As inclusões necessárias são diferentes para diferentes tipos de estrutura.</span><span class="sxs-lookup"><span data-stu-id="f2555-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="f2555-170">Relatar exceções explicitamente</span><span class="sxs-lookup"><span data-stu-id="f2555-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="f2555-171">A maneira mais simples é inserir uma chamada a TrackException() em um manipulador de exceção.</span><span class="sxs-lookup"><span data-stu-id="f2555-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="f2555-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f2555-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="f2555-173">C#</span><span class="sxs-lookup"><span data-stu-id="f2555-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="f2555-174">VB</span><span class="sxs-lookup"><span data-stu-id="f2555-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="f2555-175">Os parâmetros de medidas e propriedades são opcionais, mas são úteis para [filtrar e adicionar](app-insights-diagnostic-search.md) informações extras.</span><span class="sxs-lookup"><span data-stu-id="f2555-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="f2555-176">Por exemplo, se você tiver um aplicativo que pode executar vários jogos, será possível localizar todos os relatórios de exceção relacionados a um jogo específico.</span><span class="sxs-lookup"><span data-stu-id="f2555-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="f2555-177">Você pode adicionar quantos itens desejar a cada dicionário.</span><span class="sxs-lookup"><span data-stu-id="f2555-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="f2555-178">Exceções de navegador</span><span class="sxs-lookup"><span data-stu-id="f2555-178">Browser exceptions</span></span>
<span data-ttu-id="f2555-179">A maioria das exceções de navegador são relatados.</span><span class="sxs-lookup"><span data-stu-id="f2555-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="f2555-180">Se sua página da web inclui arquivos de script de redes de distribuição de conteúdo ou de outros domínios, certifique-se de sua marca de script com o atributo ```crossorigin="anonymous"``` e que o servidor envia [cabeçalhos CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="f2555-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="f2555-181">Isso permitirá que você obtenha um rastreamento de pilha e detalhes de exceções sem tratamento JavaScript desses recursos.</span><span class="sxs-lookup"><span data-stu-id="f2555-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="f2555-182">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="f2555-182">Web forms</span></span>
<span data-ttu-id="f2555-183">Para formulários da web, o módulo HTTP poderá coletar as exceções quando não houver nenhum redirecionamento configurado com CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="f2555-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="f2555-184">Mas se você tiver redirecionamentos ativos, adicione as seguintes linhas para a função Application_Error em Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="f2555-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="f2555-185">(Adicionar um arquivo Global.asax se você ainda não tiver um).</span><span class="sxs-lookup"><span data-stu-id="f2555-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="f2555-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="f2555-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="f2555-187">MVC</span><span class="sxs-lookup"><span data-stu-id="f2555-187">MVC</span></span>
<span data-ttu-id="f2555-188">Se a configuração do [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) é `Off`, as exceções estarão disponíveis para o [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) coletar.</span><span class="sxs-lookup"><span data-stu-id="f2555-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="f2555-189">No entanto, se for `RemoteOnly` (padrão), ou `On`, a exceção será desmarcada e não está disponível para o Application Insights coletar automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f2555-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="f2555-190">Você pode corrigir isso substituindo a classe [System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx) e aplicando a classe substituída conforme mostrado para as diferentes versões do MVC abaixo ([fonte do github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="f2555-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report the exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="f2555-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="f2555-191">MVC 2</span></span>
<span data-ttu-id="f2555-192">Substitua o atributo HandleError pelo novo atributo em seus controladores.</span><span class="sxs-lookup"><span data-stu-id="f2555-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="f2555-193">Amostra</span><span class="sxs-lookup"><span data-stu-id="f2555-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="f2555-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="f2555-194">MVC 3</span></span>
<span data-ttu-id="f2555-195">Registrar `AiHandleErrorAttribute` como um filtro global em Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="f2555-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="f2555-196">Amostra</span><span class="sxs-lookup"><span data-stu-id="f2555-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="f2555-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="f2555-197">MVC 4, MVC5</span></span>
<span data-ttu-id="f2555-198">Registre AiHandleErrorAttribute como um filtro global em FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="f2555-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="f2555-199">Amostra</span><span class="sxs-lookup"><span data-stu-id="f2555-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="f2555-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="f2555-200">Web API 1.x</span></span>
<span data-ttu-id="f2555-201">Substitua System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="f2555-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="f2555-202">Você pode adicionar esse atributo substituído para controladores específicos ou adicioná-lo na configuração de filtros globais na classe WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="f2555-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="f2555-203">Amostra</span><span class="sxs-lookup"><span data-stu-id="f2555-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="f2555-204">Há um número de casos que não podem lidar com os filtros de exceção.</span><span class="sxs-lookup"><span data-stu-id="f2555-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="f2555-205">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f2555-205">For example:</span></span>

* <span data-ttu-id="f2555-206">Exceções geradas por construtores de controlador.</span><span class="sxs-lookup"><span data-stu-id="f2555-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="f2555-207">Exceções geradas por manipuladores de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f2555-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="f2555-208">Exceções geradas durante o roteamento.</span><span class="sxs-lookup"><span data-stu-id="f2555-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="f2555-209">Exceções geradas durante a serialização de conteúdo da resposta.</span><span class="sxs-lookup"><span data-stu-id="f2555-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="f2555-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="f2555-210">Web API 2.x</span></span>
<span data-ttu-id="f2555-211">Adicione uma implementação de IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="f2555-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="f2555-212">Adicione isso aos serviços no WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="f2555-212">Add this to the services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="f2555-213">}</span><span class="sxs-lookup"><span data-stu-id="f2555-213">}</span></span>

[<span data-ttu-id="f2555-214">Amostra</span><span class="sxs-lookup"><span data-stu-id="f2555-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="f2555-215">Como alternativas, você pode:</span><span class="sxs-lookup"><span data-stu-id="f2555-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="f2555-216">Substituir o ExceptionHandler apenas por uma implementação personalizada de IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="f2555-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="f2555-217">Isso é chamado apenas quando a estrutura ainda é capaz de escolher a mensagem de resposta para enviar (não quando a conexão é anulada, por exemplo)</span><span class="sxs-lookup"><span data-stu-id="f2555-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="f2555-218">Filtros de Exceção (como descrito na seção controladores acima da API Web 1.x) - não são chamados em todos os casos.</span><span class="sxs-lookup"><span data-stu-id="f2555-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="f2555-219">WCF</span><span class="sxs-lookup"><span data-stu-id="f2555-219">WCF</span></span>
<span data-ttu-id="f2555-220">Adicione uma classe que estende o atributo e implementa IErrorHandler e IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="f2555-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="f2555-221">Adicione o atributo para as implementações de serviço:</span><span class="sxs-lookup"><span data-stu-id="f2555-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="f2555-222">Amostra</span><span class="sxs-lookup"><span data-stu-id="f2555-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="f2555-223">Contadores de desempenho de exceção</span><span class="sxs-lookup"><span data-stu-id="f2555-223">Exception performance counters</span></span>
<span data-ttu-id="f2555-224">Se você [instalou o Agente do Application Insights](app-insights-monitor-performance-live-website-now.md) no seu servidor, poderá obter um gráfico da taxa de exceções, medida pelo .NET.</span><span class="sxs-lookup"><span data-stu-id="f2555-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="f2555-225">Isso inclui exceções .NET tradas e sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="f2555-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="f2555-226">Abra uma folha do Metrics Explorer, adicione um novo gráfico e selecione **Taxa de exceção**, listada em Contadores de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="f2555-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="f2555-227">O .NET Framework calcula a taxa contando o número de exceções em um intervalo e dividindo pelo comprimento do intervalo.</span><span class="sxs-lookup"><span data-stu-id="f2555-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="f2555-228">Observe que ela será diferente da contagem 'Exceções' calculada pelo portal do Application Insights contando relatórios TrackException.</span><span class="sxs-lookup"><span data-stu-id="f2555-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="f2555-229">Os intervalos de amostragem são diferentes, e o SDK não envia relatórios TrackException a todas as exceções tratadas e sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="f2555-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="f2555-230">Vídeo</span><span class="sxs-lookup"><span data-stu-id="f2555-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="f2555-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2555-231">Next steps</span></span>
* [<span data-ttu-id="f2555-232">Monitorar REST, SQL e outras chamadas para dependências</span><span class="sxs-lookup"><span data-stu-id="f2555-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="f2555-233">Monitorar tempos de carregamento de página, exceções de navegador e chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="f2555-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="f2555-234">Monitorar contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="f2555-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
