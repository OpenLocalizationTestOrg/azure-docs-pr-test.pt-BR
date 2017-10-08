---
title: "aaaDiagnose falhas e exceções em aplicativos com o Azure Application Insights de web | Microsoft Docs"
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
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="37364-103">Diagnosticar exceções em seus aplicativos Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="37364-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="37364-104">Exceções em seu aplicativo Web ao vivo são relatadas pelo [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37364-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="37364-105">Você pode correlacionar solicitações com falha com exceções e outros eventos no cliente hello e no servidor, para que você pode diagnosticar rapidamente Olá causas.</span><span class="sxs-lookup"><span data-stu-id="37364-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="37364-106">Configurar os relatórios de exceção</span><span class="sxs-lookup"><span data-stu-id="37364-106">Set up exception reporting</span></span>
* <span data-ttu-id="37364-107">exceções de toohave relatadas por meio de seu aplicativo de servidor:</span><span class="sxs-lookup"><span data-stu-id="37364-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="37364-108">Instale o[ SDK do Application Insights](app-insights-asp-net.md) no aplicativo ou</span><span class="sxs-lookup"><span data-stu-id="37364-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="37364-109">Servidores Web IIS: executar o [Agente do Application Insights](app-insights-monitor-performance-live-website-now.md) ou</span><span class="sxs-lookup"><span data-stu-id="37364-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="37364-110">Aplicativos web do Azure: Adicionar Olá [extensão do Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="37364-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="37364-111">Os aplicativos web Java: Install Olá [agente Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="37364-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="37364-112">Instalar Olá [trecho de JavaScript](app-insights-javascript.md) em exceções de navegador de toocatch suas páginas da web.</span><span class="sxs-lookup"><span data-stu-id="37364-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="37364-113">Em algumas estruturas de aplicativo ou com algumas configurações, você precisará tootake toocatch algumas etapas adicionais mais exceções:</span><span class="sxs-lookup"><span data-stu-id="37364-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="37364-114">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="37364-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="37364-115">MVC</span><span class="sxs-lookup"><span data-stu-id="37364-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="37364-116">API Web 1.*</span><span class="sxs-lookup"><span data-stu-id="37364-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="37364-117">API Web 2.*</span><span class="sxs-lookup"><span data-stu-id="37364-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="37364-118">WCF</span><span class="sxs-lookup"><span data-stu-id="37364-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="37364-119">Diagnosticar exceções usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37364-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="37364-120">Abra a solução do aplicativo hello no Visual Studio toohelp com a depuração.</span><span class="sxs-lookup"><span data-stu-id="37364-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="37364-121">Execute o aplicativo hello, no servidor ou no computador de desenvolvimento usando F5.</span><span class="sxs-lookup"><span data-stu-id="37364-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="37364-122">Abra a janela de pesquisa do Application Insights Olá no Visual Studio e defina-toodisplay eventos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37364-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="37364-123">Durante a depuração, você pode fazer isso apenas clicando o botão do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="37364-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Clique com botão direito hello e escolha o Application Insights, aberto.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="37364-125">Observe que você pode filtrar apenas exceções do hello relatório tooshow.</span><span class="sxs-lookup"><span data-stu-id="37364-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="37364-126">*Nenhuma exceção mostrando? Consulte [Capturar exceções](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="37364-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="37364-127">Clique em um tooshow de relatório de exceção do rastreamento de pilha.</span><span class="sxs-lookup"><span data-stu-id="37364-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="37364-128">Clique em uma referência de linha no rastreamento de pilha hello, arquivo de código relevante Olá tooopen.</span><span class="sxs-lookup"><span data-stu-id="37364-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="37364-129">No código de hello, observe que CodeLens mostra dados sobre exceções hello:</span><span class="sxs-lookup"><span data-stu-id="37364-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Notificação de exceções do CodeLens.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="37364-131">Diagnosticar falhas usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37364-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="37364-132">Da visão geral do Application Insights de saudação do seu aplicativo, o bloco de falhas de saudação mostra gráficos de exceções e falha nas solicitações HTTP, junto com uma lista de saudação solicitar URLs que causam falhas mais frequentes hello.</span><span class="sxs-lookup"><span data-stu-id="37364-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Escolha Configurações, Falhas.](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="37364-134">Clique por meio de um Olá falha tipos de exceção em ocorrências de tooindividual Olá lista tooget de exceção hello, onde você pode ver os detalhes de saudação e rastreamento de pilha:</span><span class="sxs-lookup"><span data-stu-id="37364-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Selecione uma instância de uma solicitação com falha e em detalhes da exceção, obter tooinstances da exceção de saudação.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="37364-136">**Como alternativa,** você pode iniciar na lista de saudação de solicitações e localizar tooit relacionados de exceções.</span><span class="sxs-lookup"><span data-stu-id="37364-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="37364-137">*Nenhuma exceção mostrando? Consulte [Capturar exceções](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="37364-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="37364-138">Dados personalizados de rastreamento e log</span><span class="sxs-lookup"><span data-stu-id="37364-138">Custom tracing and log data</span></span>
<span data-ttu-id="37364-139">tooget dados de diagnóstico específicos tooyour aplicativo, você pode inserir código toosend seus próprios dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="37364-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="37364-140">Isso exibidos na pesquisa de diagnóstica junto com a solicitação de hello, exibição de página e outros dados coletados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="37364-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="37364-141">Você tem várias opções:</span><span class="sxs-lookup"><span data-stu-id="37364-141">You have several options:</span></span>

* <span data-ttu-id="37364-142">[Trackevent](app-insights-api-custom-events-metrics.md#trackevent) normalmente é usado para monitorar os padrões de uso, mas Olá dados envia também aparecem em eventos personalizados na pesquisa de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="37364-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="37364-143">Os eventos são nomeados e podem conter propriedades de cadeia de caracteres e métricas numéricas nas quais é possível [filtrar pesquisas de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="37364-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="37364-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) permite que você envie dados mais longos, como informações POST.</span><span class="sxs-lookup"><span data-stu-id="37364-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="37364-145">[TrackException()](#exceptions) envia rastreamentos de pilha.</span><span class="sxs-lookup"><span data-stu-id="37364-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="37364-146">[Mais sobre exceções](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="37364-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="37364-147">Se você já usa uma estrutura de registros, como Log4Net ou NLog poderá [capturar esses logs](app-insights-asp-net-trace-logs.md) e vê-los na pesquisa de diagnóstico junto com os dados de solicitação e exceção.</span><span class="sxs-lookup"><span data-stu-id="37364-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="37364-148">Esses eventos, abra o toosee [pesquisa](app-insights-diagnostic-search.md), abra o filtro e, em seguida, escolha Custom Event, rastreamento ou exceção.</span><span class="sxs-lookup"><span data-stu-id="37364-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Drill-through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="37364-150">Se seu aplicativo gera um lote de telemetria, módulo de amostragem adaptável Olá automaticamente reduzirá o volume Olá enviada toohello portal enviando apenas uma fração representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="37364-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="37364-151">Eventos que fazem parte da saudação mesma operação será marcada ou desmarcada como um grupo, para que você possa navegar entre eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="37364-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="37364-152">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="37364-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="37364-153">Como toosee solicitar dados de POSTAGEM</span><span class="sxs-lookup"><span data-stu-id="37364-153">How toosee request POST data</span></span>
<span data-ttu-id="37364-154">Detalhes da solicitação não incluam dados de saudação enviados tooyour aplicativo em uma chamada POST.</span><span class="sxs-lookup"><span data-stu-id="37364-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="37364-155">toohave esses dados relatados:</span><span class="sxs-lookup"><span data-stu-id="37364-155">toohave this data reported:</span></span>

* <span data-ttu-id="37364-156">[Instalar o SDK do hello](app-insights-asp-net.md) em seu projeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37364-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="37364-157">Inserir o código no seu aplicativo toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="37364-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="37364-158">Envie dados de POSTAGEM Olá no parâmetro de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="37364-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="37364-159">Há um limite de tamanho de toohello permitido, experimente os dados essenciais toosend Olá apenas.</span><span class="sxs-lookup"><span data-stu-id="37364-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="37364-160">Ao investigar uma falha na solicitação, localize rastreamentos Olá associado.</span><span class="sxs-lookup"><span data-stu-id="37364-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Drill-through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="37364-162"><a name="exceptions"></a> Capturando exceções e dados de diagnóstico relacionados</span><span class="sxs-lookup"><span data-stu-id="37364-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="37364-163">Primeiro, você não verá no portal de saudação todas as exceções de saudação que causam falhas em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37364-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="37364-164">Você verá as exceções de navegador (se você estiver usando Olá [SDK de JavaScript](app-insights-javascript.md) nas páginas da web).</span><span class="sxs-lookup"><span data-stu-id="37364-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="37364-165">Mas a maioria das exceções de servidor são detectados pelo IIS e você tiver toowrite um pouco de código toosee-los.</span><span class="sxs-lookup"><span data-stu-id="37364-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="37364-166">Você pode:</span><span class="sxs-lookup"><span data-stu-id="37364-166">You can:</span></span>

* <span data-ttu-id="37364-167">**Registrar exceções explicitamente** inserindo código em exceções de saudação de tooreport de manipuladores de exceção.</span><span class="sxs-lookup"><span data-stu-id="37364-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="37364-168">**Capturar exceções automaticamente** configurando sua estrutura do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="37364-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="37364-169">Olá necessárias forem diferentes para diferentes tipos de estrutura.</span><span class="sxs-lookup"><span data-stu-id="37364-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="37364-170">Relatar exceções explicitamente</span><span class="sxs-lookup"><span data-stu-id="37364-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="37364-171">Olá, a maneira mais simples é tooinsert tooTrackException() uma chamada em um manipulador de exceção.</span><span class="sxs-lookup"><span data-stu-id="37364-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="37364-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="37364-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="37364-173">C#</span><span class="sxs-lookup"><span data-stu-id="37364-173">C#</span></span>

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

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="37364-174">VB</span><span class="sxs-lookup"><span data-stu-id="37364-174">VB</span></span>

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

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="37364-175">Olá as medidas e as propriedades de parâmetros são opcionais, mas são úteis para [filtragem e adição de](app-insights-diagnostic-search.md) informações extras.</span><span class="sxs-lookup"><span data-stu-id="37364-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="37364-176">Por exemplo, se você tiver um aplicativo que pode executar vários jogos, pode encontrar todos os Olá exceção relatórios jogo específico tooa relacionados.</span><span class="sxs-lookup"><span data-stu-id="37364-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="37364-177">Você pode adicionar quantos itens como você como tooeach dicionário.</span><span class="sxs-lookup"><span data-stu-id="37364-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="37364-178">Exceções de navegador</span><span class="sxs-lookup"><span data-stu-id="37364-178">Browser exceptions</span></span>
<span data-ttu-id="37364-179">A maioria das exceções de navegador são relatados.</span><span class="sxs-lookup"><span data-stu-id="37364-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="37364-180">Se sua página da web inclui arquivos de script de redes de fornecimento de conteúdo ou de outros domínios, verifique a marca de script tem atributo Olá ```crossorigin="anonymous"```, e esse servidor de saudação envia [cabeçalhos CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="37364-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="37364-181">Isso permitirá que você tooget um rastreamento de pilha e detalhes de exceções sem tratamento JavaScript desses recursos.</span><span class="sxs-lookup"><span data-stu-id="37364-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="37364-182">Formulários da Web</span><span class="sxs-lookup"><span data-stu-id="37364-182">Web forms</span></span>
<span data-ttu-id="37364-183">Para formulários da web, Olá módulo HTTP será capaz de toocollect exceções de saudação quando não houver nenhum redirecionamentos configurados com CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="37364-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="37364-184">Mas se você tiver redirecionamentos ativos, adicionar Olá linhas toohello Application_Error funcionam em Global.asax.cs a seguir.</span><span class="sxs-lookup"><span data-stu-id="37364-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="37364-185">(Adicionar um arquivo Global.asax se você ainda não tiver um).</span><span class="sxs-lookup"><span data-stu-id="37364-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="37364-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="37364-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="37364-187">MVC</span><span class="sxs-lookup"><span data-stu-id="37364-187">MVC</span></span>
<span data-ttu-id="37364-188">Se hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuração é `Off`, exceções estará disponíveis para Olá [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="37364-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="37364-189">No entanto, se ele for `RemoteOnly` (padrão), ou `On`, exceção Olá será limpo e coletar de tooautomatically não está disponível para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="37364-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="37364-190">Você pode corrigir isso, substituindo Olá [System.Web.Mvc.HandleErrorAttribute classe](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)e aplicar classe Olá substituído, conforme mostrado Olá MVC versões diferentes abaixo ([github origem](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="37364-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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
                //If customError is Off, then AI HTTPModule will report hello exception
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

#### <a name="mvc-2"></a><span data-ttu-id="37364-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="37364-191">MVC 2</span></span>
<span data-ttu-id="37364-192">Substitua o atributo de HandleError de saudação com seu novo atributo em seus controladores.</span><span class="sxs-lookup"><span data-stu-id="37364-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="37364-193">Amostra</span><span class="sxs-lookup"><span data-stu-id="37364-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="37364-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="37364-194">MVC 3</span></span>
<span data-ttu-id="37364-195">Registrar `AiHandleErrorAttribute` como um filtro global em Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="37364-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="37364-196">Amostra</span><span class="sxs-lookup"><span data-stu-id="37364-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="37364-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="37364-197">MVC 4, MVC5</span></span>
<span data-ttu-id="37364-198">Registre AiHandleErrorAttribute como um filtro global em FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="37364-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="37364-199">Amostra</span><span class="sxs-lookup"><span data-stu-id="37364-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="37364-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="37364-200">Web API 1.x</span></span>
<span data-ttu-id="37364-201">Substitua System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="37364-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="37364-202">Você pode adicionar controladores de toospecific este atributo substituído ou adicioná-lo a configuração de filtros globais toohello na classe WebApiConfig de saudação:</span><span class="sxs-lookup"><span data-stu-id="37364-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

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

[<span data-ttu-id="37364-203">Amostra</span><span class="sxs-lookup"><span data-stu-id="37364-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="37364-204">Há um número de casos que não é possível lidar com os filtros de exceção de saudação.</span><span class="sxs-lookup"><span data-stu-id="37364-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="37364-205">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="37364-205">For example:</span></span>

* <span data-ttu-id="37364-206">Exceções geradas por construtores de controlador.</span><span class="sxs-lookup"><span data-stu-id="37364-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="37364-207">Exceções geradas por manipuladores de mensagens.</span><span class="sxs-lookup"><span data-stu-id="37364-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="37364-208">Exceções geradas durante o roteamento.</span><span class="sxs-lookup"><span data-stu-id="37364-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="37364-209">Exceções geradas durante a serialização de conteúdo da resposta.</span><span class="sxs-lookup"><span data-stu-id="37364-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="37364-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="37364-210">Web API 2.x</span></span>
<span data-ttu-id="37364-211">Adicione uma implementação de IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="37364-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="37364-212">Adicione estes serviços toohello WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="37364-212">Add this toohello services in WebApiConfig:</span></span>

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
  <span data-ttu-id="37364-213">}</span><span class="sxs-lookup"><span data-stu-id="37364-213">}</span></span>

[<span data-ttu-id="37364-214">Amostra</span><span class="sxs-lookup"><span data-stu-id="37364-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="37364-215">Como alternativas, você pode:</span><span class="sxs-lookup"><span data-stu-id="37364-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="37364-216">Substituir Olá apenas ExceptionHandler com uma implementação personalizada de IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="37364-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="37364-217">Isso é chamado apenas quando framework hello está ainda poderá toochoose qual resposta de mensagem toosend (e não quando a conexão de saudação é anulada para a instância)</span><span class="sxs-lookup"><span data-stu-id="37364-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="37364-218">Filtros de exceção (conforme descrito na seção de saudação em controladores de 1. x da API da Web acima) - não é chamados em todos os casos.</span><span class="sxs-lookup"><span data-stu-id="37364-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="37364-219">WCF</span><span class="sxs-lookup"><span data-stu-id="37364-219">WCF</span></span>
<span data-ttu-id="37364-220">Adicione uma classe que estende o atributo e implementa IErrorHandler e IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="37364-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="37364-221">Adicione as implementações de serviço Olá atributo toohello:</span><span class="sxs-lookup"><span data-stu-id="37364-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="37364-222">Amostra</span><span class="sxs-lookup"><span data-stu-id="37364-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="37364-223">Contadores de desempenho de exceção</span><span class="sxs-lookup"><span data-stu-id="37364-223">Exception performance counters</span></span>
<span data-ttu-id="37364-224">Se você tiver [instalado Olá Application Insights Agent](app-insights-monitor-performance-live-website-now.md) no seu servidor, você pode obter um gráfico de taxa de exceções hello, medido pelo .NET.</span><span class="sxs-lookup"><span data-stu-id="37364-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="37364-225">Isso inclui exceções .NET tradas e sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="37364-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="37364-226">Abra uma folha do Metrics Explorer, adicione um novo gráfico e selecione **Taxa de exceção**, listada em Contadores de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="37364-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="37364-227">.NET framework do Hello calcula a taxa de saudação contando o número de saudação de exceções em um intervalo e dividindo pelo comprimento de saudação do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="37364-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="37364-228">Observe que ele seja diferente da contagem de 'Exceções' hello calculada pelo portal do Application Insights Olá contando TrackException relatórios.</span><span class="sxs-lookup"><span data-stu-id="37364-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="37364-229">intervalos de amostragem de saudação são diferentes e Olá SDK não envia relatórios de TrackException para todas as exceções manipuladas e não manipuladas.</span><span class="sxs-lookup"><span data-stu-id="37364-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="37364-230">Vídeo</span><span class="sxs-lookup"><span data-stu-id="37364-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="37364-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37364-231">Next steps</span></span>
* [<span data-ttu-id="37364-232">Monitorar REST, SQL e outros toodependencies de chamadas</span><span class="sxs-lookup"><span data-stu-id="37364-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="37364-233">Monitorar tempos de carregamento de página, exceções de navegador e chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="37364-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="37364-234">Monitorar contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="37364-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
