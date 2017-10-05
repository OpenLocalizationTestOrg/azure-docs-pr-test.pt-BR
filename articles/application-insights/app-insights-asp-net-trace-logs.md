---
title: Explorar os logs de rastreamento do .NET no Application Insights
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
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="69db5-103">Explorar os logs de rastreamento do .NET no Application Insights</span><span class="sxs-lookup"><span data-stu-id="69db5-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="69db5-104">Se você usar NLog, log4Net ou System.Diagnostics.Trace para o rastreamento de diagnóstico em seu aplicativo ASP.NET, os logs poderão ser enviados ao [Azure Application Insights][start], onde será possível explorá-los e pesquisá-los.</span><span class="sxs-lookup"><span data-stu-id="69db5-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="69db5-105">Os logs serão mesclados à outra telemetria proveniente de seu aplicativo para que você possa identificar os rastreamentos associados ao atendimento de cada solicitação de usuário e correlacioná-los com outros relatórios de eventos e exceções.</span><span class="sxs-lookup"><span data-stu-id="69db5-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="69db5-106">Você precisa do módulo de captura de log?</span><span class="sxs-lookup"><span data-stu-id="69db5-106">Do you need the log capture module?</span></span> <span data-ttu-id="69db5-107">É um adaptador útil para agentes de terceiros, mas se você ainda não usa o NLog, log4Net ou System.Diagnostics.Trace, convém chamar apenas o [TrackTrace() do Application Insights](app-insights-api-custom-events-metrics.md#tracktrace) diretamente.</span><span class="sxs-lookup"><span data-stu-id="69db5-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="69db5-108">Instalar o log no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="69db5-108">Install logging on your app</span></span>
<span data-ttu-id="69db5-109">Instale a estrutura de registros escolhida no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="69db5-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="69db5-110">Isso deve resultar em uma entrada no app.config ou web.config.</span><span class="sxs-lookup"><span data-stu-id="69db5-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="69db5-111">Se você estiver usando System.Diagnostics.Trace, precisará adicionar uma entrada ao web.config:</span><span class="sxs-lookup"><span data-stu-id="69db5-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

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
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="69db5-112">Configurar o Application Insights para coletar logs</span><span class="sxs-lookup"><span data-stu-id="69db5-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="69db5-113">**[Adicione o Application Insights ao seu projeto](app-insights-asp-net.md)** se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="69db5-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="69db5-114">Você verá uma opção para incluir o coletor de logs.</span><span class="sxs-lookup"><span data-stu-id="69db5-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="69db5-115">Ou então **Configure o Application Insights** clicando com o botão direito no seu projeto no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="69db5-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="69db5-116">Selecione a opção **Configurar a coleta de rastreamento**.</span><span class="sxs-lookup"><span data-stu-id="69db5-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="69db5-117">*Não consegue ver o menu do Application Insights nem a opção de coletor de logs?*</span><span class="sxs-lookup"><span data-stu-id="69db5-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="69db5-118">Experimente [Solucionar problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="69db5-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="69db5-119">Instalação manual</span><span class="sxs-lookup"><span data-stu-id="69db5-119">Manual installation</span></span>
<span data-ttu-id="69db5-120">Use este método se o tipo de projeto não tiver suporte no instalador do Application Insights (por exemplo, um projeto de Área de Trabalho do Windows).</span><span class="sxs-lookup"><span data-stu-id="69db5-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="69db5-121">Se você planeja usar o log4Net ou NLog, instale-o em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="69db5-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="69db5-122">No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="69db5-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="69db5-123">Pesquise “Application Insights”</span><span class="sxs-lookup"><span data-stu-id="69db5-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="69db5-124">Selecione o pacote apropriado entre:</span><span class="sxs-lookup"><span data-stu-id="69db5-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="69db5-125">Microsoft.ApplicationInsights.TraceListener (para capturar chamadas do System.Diagnostics.Trace)</span><span class="sxs-lookup"><span data-stu-id="69db5-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="69db5-126">Microsoft.ApplicationInsights.EventSourceListener (para capturar EventSource)</span><span class="sxs-lookup"><span data-stu-id="69db5-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="69db5-127">Microsoft.ApplicationInsights.EtwListener (para capturar eventos ETW)</span><span class="sxs-lookup"><span data-stu-id="69db5-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="69db5-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="69db5-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="69db5-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="69db5-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="69db5-130">O pacote NuGet instala os assemblies necessários e também modifica o app.config ou web.config.</span><span class="sxs-lookup"><span data-stu-id="69db5-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="69db5-131">Inserir chamadas de log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="69db5-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="69db5-132">Se você usa System.Diagnostics.Trace, uma chamada típica é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="69db5-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="69db5-133">Se você preferir log4net ou NLog:</span><span class="sxs-lookup"><span data-stu-id="69db5-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="69db5-134">Usando eventos EventSource</span><span class="sxs-lookup"><span data-stu-id="69db5-134">Using EventSource events</span></span>
<span data-ttu-id="69db5-135">É possível configurar eventos [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) para que eles sejam enviados para o Application Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="69db5-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="69db5-136">Primeiro, instale o pacote NuGet `Microsoft.ApplicationInsights.EventSourceListener`.</span><span class="sxs-lookup"><span data-stu-id="69db5-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="69db5-137">Depois, edite a seção `TelemetryModules` do arquivo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="69db5-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="69db5-138">Para cada fonte, você pode definir os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="69db5-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="69db5-139">`Name` especifica o nome do EventSource a ser coletado.</span><span class="sxs-lookup"><span data-stu-id="69db5-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="69db5-140">`Level` especifica o nível de registro em log a ser coletado.</span><span class="sxs-lookup"><span data-stu-id="69db5-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="69db5-141">Pode ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` ou `Warning`.</span><span class="sxs-lookup"><span data-stu-id="69db5-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="69db5-142">`Keywords` (opcional) especifica o valor inteiro das combinações de palavras-chave a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="69db5-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="69db5-143">Usando eventos DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="69db5-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="69db5-144">É possível configurar eventos [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) para que eles sejam enviados para o Application Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="69db5-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="69db5-145">Primeiro, instale o pacote NuGet [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener).</span><span class="sxs-lookup"><span data-stu-id="69db5-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="69db5-146">Depois, edite a seção `TelemetryModules` do arquivo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="69db5-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="69db5-147">Para cada DiagnosticSource que você deseja rastrear, adicione uma entrada com o atributo `Name` definido como o nome do seu DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="69db5-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="69db5-148">Usando eventos ETW</span><span class="sxs-lookup"><span data-stu-id="69db5-148">Using ETW events</span></span>
<span data-ttu-id="69db5-149">É possível configurar os eventos ETW a serem enviados ao Application Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="69db5-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="69db5-150">Primeiro, instale o pacote NuGet `Microsoft.ApplicationInsights.EtwCollector`.</span><span class="sxs-lookup"><span data-stu-id="69db5-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="69db5-151">Depois, edite a seção `TelemetryModules` do arquivo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="69db5-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="69db5-152">Eventos ETW só podem ser coletados se o processo que hospeda o SDK estiver em execução em uma identidade que é membro dos administradores ou "Usuários de log de desempenho".</span><span class="sxs-lookup"><span data-stu-id="69db5-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="69db5-153">Para cada fonte, você pode definir os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="69db5-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="69db5-154">`ProviderName` é o nome do provedor de ETW a ser coletado.</span><span class="sxs-lookup"><span data-stu-id="69db5-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="69db5-155">`ProviderGuid` especifica o GUID do provedor de ETW a ser coletado, pode ser usado em vez de `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="69db5-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="69db5-156">`Level` define o nível de registro em log a ser coletado.</span><span class="sxs-lookup"><span data-stu-id="69db5-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="69db5-157">Pode ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` ou `Warning`.</span><span class="sxs-lookup"><span data-stu-id="69db5-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="69db5-158">`Keywords` (opcional) define o valor inteiro das combinações de palavras-chave a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="69db5-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="69db5-159">Usando a API de rastreamento diretamente</span><span class="sxs-lookup"><span data-stu-id="69db5-159">Using the Trace API directly</span></span>
<span data-ttu-id="69db5-160">Você pode chamar a API de rastreamento do Application Insights diretamente.</span><span class="sxs-lookup"><span data-stu-id="69db5-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="69db5-161">Os adaptadores de log usam essa API.</span><span class="sxs-lookup"><span data-stu-id="69db5-161">The logging adapters use this API.</span></span>

<span data-ttu-id="69db5-162">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="69db5-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="69db5-163">Uma vantagem de TrackTrace é que você pode colocar dados relativamente compridos na mensagem.</span><span class="sxs-lookup"><span data-stu-id="69db5-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="69db5-164">Por exemplo, você pode codificar dados POST.</span><span class="sxs-lookup"><span data-stu-id="69db5-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="69db5-165">Além disso, você pode adicionar um nível de severidade à mensagem.</span><span class="sxs-lookup"><span data-stu-id="69db5-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="69db5-166">E, como ocorre com outros casos de telemetria, você pode adicionar valores de propriedade que podem ser usados para ajudar a filtrar ou a pesquisar diferentes conjuntos de rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="69db5-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="69db5-167">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="69db5-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="69db5-168">Isso permite que você filtre facilmente todas as mensagens de um nível de severidade específico relacionadas a determinado banco de dados na [Pesquisa][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="69db5-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="69db5-169">Explorar seus logs</span><span class="sxs-lookup"><span data-stu-id="69db5-169">Explore your logs</span></span>
<span data-ttu-id="69db5-170">Execute o aplicativo no modo de depuração ou implante-o dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="69db5-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="69db5-171">Na folha de visão geral do aplicativo, no [portal do Application Insights][portal], escolha [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="69db5-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![No Application Insights, escolha Pesquisar](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Pesquisa](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="69db5-174">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="69db5-174">You can, for example:</span></span>

* <span data-ttu-id="69db5-175">Filtrar rastreamentos de log ou itens com propriedades específicas</span><span class="sxs-lookup"><span data-stu-id="69db5-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="69db5-176">Inspecionar um item específico em detalhes.</span><span class="sxs-lookup"><span data-stu-id="69db5-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="69db5-177">Localizar outra telemetria relacionada à mesma solicitação de usuário (ou seja, com o mesmo OperationId)</span><span class="sxs-lookup"><span data-stu-id="69db5-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="69db5-178">Salvar a configuração dessa página como um favorito</span><span class="sxs-lookup"><span data-stu-id="69db5-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="69db5-179">**Amostragem.**</span><span class="sxs-lookup"><span data-stu-id="69db5-179">**Sampling.**</span></span> <span data-ttu-id="69db5-180">Se o aplicativo enviar muitos dados e se você estiver usando o SDK do Application Insights para o ASP.NET versão 2.0.0-beta3 ou posterior, o recurso de amostragem adaptável poderá operar e enviar apenas uma porcentagem de sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="69db5-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="69db5-181">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="69db5-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="69db5-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69db5-182">Next steps</span></span>
<span data-ttu-id="69db5-183">[Diagnosticar falhas e exceções no ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="69db5-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="69db5-184">[Saiba mais sobre o Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="69db5-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="69db5-185">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="69db5-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="69db5-186">Como faço isso no Java?</span><span class="sxs-lookup"><span data-stu-id="69db5-186">How do I do this for Java?</span></span>
<span data-ttu-id="69db5-187">Use os [adaptadores de log Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="69db5-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="69db5-188">Não há nenhuma opção do Application Insights no menu de contexto do projeto</span><span class="sxs-lookup"><span data-stu-id="69db5-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="69db5-189">Verifique se as ferramentas do Application Insights estão instaladas neste computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="69db5-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="69db5-190">No menu Ferramentas do Visual Studio, em Extensões e Atualizações, procure pelas Ferramentas do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="69db5-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="69db5-191">Se não estiver na aba Instalado, abra a guia Online e instale-as.</span><span class="sxs-lookup"><span data-stu-id="69db5-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="69db5-192">Este pode ser um tipo de projeto sem suporte pelas ferramentas do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="69db5-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="69db5-193">Use a [instalação manual](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="69db5-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="69db5-194">Não há nenhuma opção de adaptador de log na ferramenta de configuração</span><span class="sxs-lookup"><span data-stu-id="69db5-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="69db5-195">Você precisa instalar primeiro a estrutura de registros.</span><span class="sxs-lookup"><span data-stu-id="69db5-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="69db5-196">Se estiver usando System.Diagnostics.Trace, verifique se você o [configurou no `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="69db5-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="69db5-197">Você tem a versão mais recente do Application Insights?</span><span class="sxs-lookup"><span data-stu-id="69db5-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="69db5-198">No menu **Ferramentas** do Visual Studio, escolha **Extensões e Atualizações** e abra a guia **Atualizações**. Se as ferramentas de Análise do Desenvolvedor estiverem presentes, clique para atualizá-las.</span><span class="sxs-lookup"><span data-stu-id="69db5-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="69db5-199"><a name="emptykey"></a>Recebo um erro "Chave de instrumentação não pode ser vazio"</span><span class="sxs-lookup"><span data-stu-id="69db5-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="69db5-200">Parece que você instalou o pacote de Nuget de adaptador para registro em log sem instalar o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="69db5-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="69db5-201">No Gerenciador de Soluções, clique com o botão direito do mouse em `ApplicationInsights.config` e escolha **Atualizar o Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="69db5-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="69db5-202">Você obterá uma caixa de diálogo que solicita que você entre no Azure e crie um recurso de Application Insights, ou então reutilize um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="69db5-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="69db5-203">Isso deve corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="69db5-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="69db5-204">Posso ver rastreamentos na pesquisa de diagnóstico, mas não os outros eventos</span><span class="sxs-lookup"><span data-stu-id="69db5-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="69db5-205">Às vezes, pode levar algum tempo para que todos os eventos e solicitações percorram o pipeline.</span><span class="sxs-lookup"><span data-stu-id="69db5-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="69db5-206"><a name="limits"></a>Que quantidade de dados é mantida?</span><span class="sxs-lookup"><span data-stu-id="69db5-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="69db5-207">Vários fatores afetam a quantidade de dados retidos.</span><span class="sxs-lookup"><span data-stu-id="69db5-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="69db5-208">Veja a seção de [limites](app-insights-api-custom-events-metrics.md#limits) da página de métricas de eventos do cliente para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="69db5-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="69db5-209">Não estou vendo algumas das entradas de log que eu esperava</span><span class="sxs-lookup"><span data-stu-id="69db5-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="69db5-210">Se o aplicativo enviar muitos dados e se você estiver usando o SDK do Application Insights para o ASP.NET versão 2.0.0-beta3 ou posterior, o recurso de amostragem adaptável poderá operar e enviar apenas uma porcentagem de sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="69db5-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="69db5-211">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="69db5-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="69db5-212"><a name="add"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69db5-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="69db5-213">[Configurar testes de disponibilidade e capacidade de resposta][availability]</span><span class="sxs-lookup"><span data-stu-id="69db5-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="69db5-214">[Solução de problemas][qna]</span><span class="sxs-lookup"><span data-stu-id="69db5-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
