---
title: os logs de rastreamento de .NET aaaExplore no Application Insights
description: Pesquise logs gerados com Trace, NLog ou Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="524ab-103">Explorar os logs de rastreamento do .NET no Application Insights</span><span class="sxs-lookup"><span data-stu-id="524ab-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="524ab-104">Se você usar NLog, log4Net ou Trace para rastreamento de diagnóstico em seu aplicativo ASP.NET, você pode ter seus logs enviados muito[Azure Application Insights][start], onde você pode explorar e pesquisar -los.</span><span class="sxs-lookup"><span data-stu-id="524ab-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="524ab-105">Os logs serão mesclados com outros Olá telemetria provenientes de seu aplicativo, para que você possa identificar Olá rastreamentos associados com cada solicitação de usuário de serviço e correlacioná-los com outros eventos e relatórios de exceção.</span><span class="sxs-lookup"><span data-stu-id="524ab-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="524ab-106">Você precisa de módulo de captura de log Olá?</span><span class="sxs-lookup"><span data-stu-id="524ab-106">Do you need hello log capture module?</span></span> <span data-ttu-id="524ab-107">É um adaptador útil para agentes de terceiros, mas se você ainda não usa o NLog, log4Net ou System.Diagnostics.Trace, convém chamar apenas o [TrackTrace() do Application Insights](app-insights-api-custom-events-metrics.md#tracktrace) diretamente.</span><span class="sxs-lookup"><span data-stu-id="524ab-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="524ab-108">Instalar o log no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="524ab-108">Install logging on your app</span></span>
<span data-ttu-id="524ab-109">Instale a estrutura de registros escolhida no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="524ab-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="524ab-110">Isso deve resultar em uma entrada no app.config ou web.config.</span><span class="sxs-lookup"><span data-stu-id="524ab-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="524ab-111">Se você estiver usando o Trace, você precisa tooadd um tooweb.config de entrada:</span><span class="sxs-lookup"><span data-stu-id="524ab-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="524ab-112">Configurar logs de toocollect Application Insights</span><span class="sxs-lookup"><span data-stu-id="524ab-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="524ab-113">**[Adicionar projeto do Application Insights tooyour](app-insights-asp-net.md)**  se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="524ab-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="524ab-114">Você verá um coletor de log opção tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="524ab-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="524ab-115">Ou então **Configure o Application Insights** clicando com o botão direito no seu projeto no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="524ab-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="524ab-116">Selecione a opção de saudação muito**configurar coleta de rastreamento**.</span><span class="sxs-lookup"><span data-stu-id="524ab-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="524ab-117">*Não consegue ver o menu do Application Insights nem a opção de coletor de logs?*</span><span class="sxs-lookup"><span data-stu-id="524ab-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="524ab-118">Experimente [Solucionar problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="524ab-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="524ab-119">Instalação manual</span><span class="sxs-lookup"><span data-stu-id="524ab-119">Manual installation</span></span>
<span data-ttu-id="524ab-120">Use este método se o tipo de projeto não é suportado pelo instalador do Application Insights hello (por exemplo um área de trabalho projeto do Windows).</span><span class="sxs-lookup"><span data-stu-id="524ab-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="524ab-121">Se você planejar toouse log4Net ou NLog, instalá-lo em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="524ab-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="524ab-122">No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="524ab-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="524ab-123">Pesquise “Application Insights”</span><span class="sxs-lookup"><span data-stu-id="524ab-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="524ab-124">Selecione o pacote apropriado Olá - um de:</span><span class="sxs-lookup"><span data-stu-id="524ab-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="524ab-125">Microsoft.ApplicationInsights.TraceListener (toocapture Trace chamadas)</span><span class="sxs-lookup"><span data-stu-id="524ab-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="524ab-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource eventos)</span><span class="sxs-lookup"><span data-stu-id="524ab-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="524ab-127">Microsoft.ApplicationInsights.EtwListener (eventos ETW toocapture)</span><span class="sxs-lookup"><span data-stu-id="524ab-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="524ab-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="524ab-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="524ab-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="524ab-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="524ab-130">pacote do NuGet Olá instala os assemblies necessários hello e modifica Web. config ou App. config.</span><span class="sxs-lookup"><span data-stu-id="524ab-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="524ab-131">Inserir chamadas de log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="524ab-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="524ab-132">Se você usa System.Diagnostics.Trace, uma chamada típica é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="524ab-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="524ab-133">Se você preferir log4net ou NLog:</span><span class="sxs-lookup"><span data-stu-id="524ab-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="524ab-134">Usando eventos EventSource</span><span class="sxs-lookup"><span data-stu-id="524ab-134">Using EventSource events</span></span>
<span data-ttu-id="524ab-135">Você pode configurar [Tracing](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos toobe enviado tooApplication Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="524ab-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="524ab-136">Primeiro, instale Olá `Microsoft.ApplicationInsights.EventSourceListener` pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="524ab-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="524ab-137">Edite `TelemetryModules` seção Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) arquivo.</span><span class="sxs-lookup"><span data-stu-id="524ab-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="524ab-138">Para cada fonte, você pode definir Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="524ab-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="524ab-139">`Name`Especifica o nome de saudação do hello EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="524ab-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="524ab-140">`Level`Especifica a saudação toocollect nível de log.</span><span class="sxs-lookup"><span data-stu-id="524ab-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="524ab-141">Pode ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` ou `Warning`.</span><span class="sxs-lookup"><span data-stu-id="524ab-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="524ab-142">`Keywords`(Opcional) Especifica o valor de inteiro de saudação do toouse de combinações de palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="524ab-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="524ab-143">Usando eventos DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="524ab-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="524ab-144">Você pode configurar [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) eventos toobe enviado tooApplication Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="524ab-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="524ab-145">Primeiro, instale Olá [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="524ab-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="524ab-146">Edite Olá `TelemetryModules` seção Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) arquivo.</span><span class="sxs-lookup"><span data-stu-id="524ab-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="524ab-147">Para cada DiagnosticSource você deseja tootrace, adicione uma entrada com hello `Name` toohello nome do seu DiagnosticSource do conjunto de atributo.</span><span class="sxs-lookup"><span data-stu-id="524ab-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="524ab-148">Usando eventos ETW</span><span class="sxs-lookup"><span data-stu-id="524ab-148">Using ETW events</span></span>
<span data-ttu-id="524ab-149">Você pode configurar toobe de eventos ETW enviado tooApplication Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="524ab-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="524ab-150">Primeiro, instale Olá `Microsoft.ApplicationInsights.EtwCollector` pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="524ab-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="524ab-151">Edite `TelemetryModules` seção Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) arquivo.</span><span class="sxs-lookup"><span data-stu-id="524ab-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="524ab-152">Eventos ETW só podem ser obtidos se Olá Olá de hospedagem de processo SDK está sendo executado sob uma identidade que é um membro de administradores ou "usuários de Log de desempenho".</span><span class="sxs-lookup"><span data-stu-id="524ab-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="524ab-153">Para cada fonte, você pode definir Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="524ab-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="524ab-154">`ProviderName`é o nome de saudação do hello toocollect de provedor ETW.</span><span class="sxs-lookup"><span data-stu-id="524ab-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="524ab-155">`ProviderGuid`Especifica a saudação GUID da saudação toocollect de provedor ETW, pode ser usado em vez de `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="524ab-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="524ab-156">`Level`Define Olá toocollect nível de log.</span><span class="sxs-lookup"><span data-stu-id="524ab-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="524ab-157">Pode ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` ou `Warning`.</span><span class="sxs-lookup"><span data-stu-id="524ab-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="524ab-158">`Keywords`(Opcional) define Olá valor inteiro toouse de combinações de palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="524ab-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="524ab-159">Usando Olá rastreamento API diretamente</span><span class="sxs-lookup"><span data-stu-id="524ab-159">Using hello Trace API directly</span></span>
<span data-ttu-id="524ab-160">Você pode chamar hello Application Insights rastreamento API diretamente.</span><span class="sxs-lookup"><span data-stu-id="524ab-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="524ab-161">adaptadores de registro em log Olá usam essa API.</span><span class="sxs-lookup"><span data-stu-id="524ab-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="524ab-162">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="524ab-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="524ab-163">Uma vantagem de TrackTrace é que você pode colocar dados relativamente longos na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="524ab-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="524ab-164">Por exemplo, você pode codificar dados POST.</span><span class="sxs-lookup"><span data-stu-id="524ab-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="524ab-165">Além disso, você pode adicionar uma mensagem de tooyour nível de severidade.</span><span class="sxs-lookup"><span data-stu-id="524ab-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="524ab-166">E, como outros telemetria, você pode adicionar valores de propriedade que você pode usar o filtro de toohelp ou pesquisa para diferentes conjuntos de rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="524ab-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="524ab-167">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="524ab-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="524ab-168">Isso permitiria que você, em [pesquisa][diagnostic], tooeasily filtrar todas as mensagens de saudação de um nível de severidade específico relacionado tooa determinado banco de dados.</span><span class="sxs-lookup"><span data-stu-id="524ab-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="524ab-169">Explorar seus logs</span><span class="sxs-lookup"><span data-stu-id="524ab-169">Explore your logs</span></span>
<span data-ttu-id="524ab-170">Execute o aplicativo no modo de depuração ou implante-o dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="524ab-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="524ab-171">Na folha de visão geral do aplicativo em [portal do Application Insights Olá][portal], escolha [pesquisa][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="524ab-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![No Application Insights, escolha Pesquisar](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Pesquisa](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="524ab-174">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="524ab-174">You can, for example:</span></span>

* <span data-ttu-id="524ab-175">Filtrar rastreamentos de log ou itens com propriedades específicas</span><span class="sxs-lookup"><span data-stu-id="524ab-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="524ab-176">Inspecionar um item específico em detalhes.</span><span class="sxs-lookup"><span data-stu-id="524ab-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="524ab-177">Localizar outros telemetria relacionados toohello mesma solicitação de usuário (ou seja, com hello mesmo OperationId)</span><span class="sxs-lookup"><span data-stu-id="524ab-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="524ab-178">Salvar configuração de saudação desta página como um favorito</span><span class="sxs-lookup"><span data-stu-id="524ab-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="524ab-179">**Amostragem.**</span><span class="sxs-lookup"><span data-stu-id="524ab-179">**Sampling.**</span></span> <span data-ttu-id="524ab-180">Se seu aplicativo envia um lote de dados e você estiver usando Olá SDK do Application Insights para ASP.NET versão 2.0.0-beta3 ou posterior, o recurso de amostragem adaptável de saudação pode operar e enviar apenas uma porcentagem da sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="524ab-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="524ab-181">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="524ab-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="524ab-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="524ab-182">Next steps</span></span>
<span data-ttu-id="524ab-183">[Diagnosticar falhas e exceções no ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="524ab-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="524ab-184">[Saiba mais sobre o Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="524ab-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="524ab-185">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="524ab-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="524ab-186">Como faço isso no Java?</span><span class="sxs-lookup"><span data-stu-id="524ab-186">How do I do this for Java?</span></span>
<span data-ttu-id="524ab-187">Saudação de uso [adaptadores do log de Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="524ab-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="524ab-188">Não há nenhuma opção Application Insights no menu de contexto do projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="524ab-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="524ab-189">Verifique se as ferramentas do Application Insights estão instaladas neste computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="524ab-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="524ab-190">No menu Ferramentas do Visual Studio, em Extensões e Atualizações, procure pelas Ferramentas do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="524ab-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="524ab-191">Se não estiver na guia do hello instalado, abra Olá Online guia e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="524ab-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="524ab-192">Este pode ser um tipo de projeto sem suporte pelas ferramentas do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="524ab-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="524ab-193">Use a [instalação manual](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="524ab-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="524ab-194">Nenhuma opção de adaptador de log na ferramenta de configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="524ab-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="524ab-195">Você precisa de estrutura de tooinstall Olá log primeiro.</span><span class="sxs-lookup"><span data-stu-id="524ab-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="524ab-196">Se estiver usando System.Diagnostics.Trace, verifique se você o [configurou no `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="524ab-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="524ab-197">Você tem a versão mais recente de saudação do Application Insights?</span><span class="sxs-lookup"><span data-stu-id="524ab-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="524ab-198">No Visual Studio **ferramentas** menu, escolha **extensões e atualizações**e abra hello **atualizações** guia. Se as ferramentas de análise do desenvolvedor está lá, clique em tooupdate-lo.</span><span class="sxs-lookup"><span data-stu-id="524ab-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="524ab-199"><a name="emptykey"></a>Recebo um erro "Chave de instrumentação não pode ser vazio"</span><span class="sxs-lookup"><span data-stu-id="524ab-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="524ab-200">Parece que você instalou Olá log de pacote de Nuget de adaptador sem instalar o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="524ab-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="524ab-201">No Gerenciador de Soluções, clique com o botão direito do mouse em `ApplicationInsights.config` e escolha **Atualizar o Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="524ab-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="524ab-202">Você obterá uma caixa de diálogo que solicita a você toosign no tooAzure e crie um recurso do Application Insights, ou use novamente um existente.</span><span class="sxs-lookup"><span data-stu-id="524ab-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="524ab-203">Isso deve corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="524ab-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="524ab-204">Eu podem ver rastreamentos em busca de diagnóstico, mas não Olá outros eventos</span><span class="sxs-lookup"><span data-stu-id="524ab-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="524ab-205">Às vezes, pode levar algum tempo para que todos os tooget de eventos e solicitações de saudação por meio do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="524ab-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="524ab-206"><a name="limits"></a>Que quantidade de dados é mantida?</span><span class="sxs-lookup"><span data-stu-id="524ab-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="524ab-207">Vários fatores afetam a quantidade de saudação de dados retidos.</span><span class="sxs-lookup"><span data-stu-id="524ab-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="524ab-208">Consulte Olá [limites](app-insights-api-custom-events-metrics.md#limits) seção da página de métricas de evento Olá cliente para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="524ab-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="524ab-209">Não ver algumas das entradas de log Olá esperados</span><span class="sxs-lookup"><span data-stu-id="524ab-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="524ab-210">Se seu aplicativo envia um lote de dados e você estiver usando Olá SDK do Application Insights para ASP.NET versão 2.0.0-beta3 ou posterior, o recurso de amostragem adaptável de saudação pode operar e enviar apenas uma porcentagem da sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="524ab-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="524ab-211">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="524ab-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="524ab-212"><a name="add"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="524ab-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="524ab-213">[Configurar testes de disponibilidade e capacidade de resposta][availability]</span><span class="sxs-lookup"><span data-stu-id="524ab-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="524ab-214">[Solução de problemas][qna]</span><span class="sxs-lookup"><span data-stu-id="524ab-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
