---
title: "aaaApplication Insights API para eventos personalizados e métricas | Microsoft Docs"
description: "Insira algumas linhas de código em seu uso tootrack dispositivo ou aplicativo de área de trabalho, página da Web ou serviço e diagnosticar problemas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="99aa3-103">API do Application Insights para métricas e eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="99aa3-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="99aa3-104">Insira algumas linhas de código no seu toofind aplicativo out que os usuários estão fazendo com que ele ou toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="99aa3-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="99aa3-105">Você pode enviar telemetria de aplicativos da área de trabalho e de dispositivo, clientes Web e servidores Web.</span><span class="sxs-lookup"><span data-stu-id="99aa3-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="99aa3-106">Saudação de uso [Azure Application Insights](app-insights-overview.md) principais eventos personalizados do API de telemetria toosend e métricas e suas próprias versões da telemetria padrão.</span><span class="sxs-lookup"><span data-stu-id="99aa3-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="99aa3-107">Essa API é Olá mesma API esse padrão Olá usam os coletores de dados do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="99aa3-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="99aa3-108">Resumo da API</span><span class="sxs-lookup"><span data-stu-id="99aa3-108">API summary</span></span>
<span data-ttu-id="99aa3-109">Olá API é uniforme em todas as plataformas, além de algumas pequenas variações.</span><span class="sxs-lookup"><span data-stu-id="99aa3-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="99aa3-110">Método</span><span class="sxs-lookup"><span data-stu-id="99aa3-110">Method</span></span> | <span data-ttu-id="99aa3-111">Usado para</span><span class="sxs-lookup"><span data-stu-id="99aa3-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="99aa3-112">Páginas, telas, folhas ou formulários.</span><span class="sxs-lookup"><span data-stu-id="99aa3-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="99aa3-113">Ações de usuário e outros eventos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-113">User actions and other events.</span></span> <span data-ttu-id="99aa3-114">Usado tootrack desempenho de comportamento ou toomonitor do usuário.</span><span class="sxs-lookup"><span data-stu-id="99aa3-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="99aa3-115">Medidas de desempenho, como comprimentos de fila de eventos de toospecific não relacionados.</span><span class="sxs-lookup"><span data-stu-id="99aa3-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="99aa3-116">Registrar em log as exceções para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="99aa3-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="99aa3-117">Rastreamento onde eles ocorrem em eventos de tooother de relação e examine os rastreamentos de pilha.</span><span class="sxs-lookup"><span data-stu-id="99aa3-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="99aa3-118">Registro em log frequência hello e duração de solicitações de servidor para análise de desempenho.</span><span class="sxs-lookup"><span data-stu-id="99aa3-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="99aa3-119">Mensagens de log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="99aa3-119">Diagnostic log messages.</span></span> <span data-ttu-id="99aa3-120">Você também pode capturar logs de terceiros.</span><span class="sxs-lookup"><span data-stu-id="99aa3-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="99aa3-121">Duração de saudação do registro e a frequência de componentes de tooexternal de chamadas que seu aplicativo depende.</span><span class="sxs-lookup"><span data-stu-id="99aa3-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="99aa3-122">Você pode [anexar propriedades e métricas](#properties) toomost dessas chamadas de telemetria.</span><span class="sxs-lookup"><span data-stu-id="99aa3-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="99aa3-123"><a name="prep"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="99aa3-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="99aa3-124">Se você ainda não tem uma referência no SDK do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="99aa3-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="99aa3-125">Adicione projeto de tooyour do SDK do Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="99aa3-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="99aa3-126">Projeto do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99aa3-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="99aa3-127">Projeto Java</span><span class="sxs-lookup"><span data-stu-id="99aa3-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="99aa3-128">JavaScript em cada página da Web</span><span class="sxs-lookup"><span data-stu-id="99aa3-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="99aa3-129">Em seu código de servidor Web ou dispositivo, inclua:</span><span class="sxs-lookup"><span data-stu-id="99aa3-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="99aa3-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="99aa3-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="99aa3-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="99aa3-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="99aa3-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="99aa3-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="99aa3-133">Construção de uma instância de TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="99aa3-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="99aa3-134">Construa uma instância de `TelemetryClient` (exceto em JavaScript nas páginas da Web):</span><span class="sxs-lookup"><span data-stu-id="99aa3-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="99aa3-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="99aa3-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="99aa3-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="99aa3-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="99aa3-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="99aa3-138">TelemetryClient é thread-safe.</span><span class="sxs-lookup"><span data-stu-id="99aa3-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="99aa3-139">É recomendável usar uma instância de TelemetryClient para cada módulo do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="99aa3-140">Por exemplo, você pode ter uma instância de TelemetryClient em seu web service tooreport solicitações HTTP de entrada e outro em eventos de lógica de negócios um middleware classe tooreport.</span><span class="sxs-lookup"><span data-stu-id="99aa3-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="99aa3-141">Você pode definir propriedades, como `TelemetryClient.Context.User.Id` tootrack usuários e sessões, ou `TelemetryClient.Context.Device.Id` tooidentify máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="99aa3-142">Essas informações são eventos anexados tooall Olá envios de instância.</span><span class="sxs-lookup"><span data-stu-id="99aa3-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="99aa3-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="99aa3-143">TrackEvent</span></span>
<span data-ttu-id="99aa3-144">No Application Insights, um *evento personalizado* é um ponto de dados que você pode exibir no [Metrics Explorer](app-insights-metrics-explorer.md) como uma contagem agregada e na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md) como ocorrências individuais.</span><span class="sxs-lookup"><span data-stu-id="99aa3-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="99aa3-145">(Não é relacionado tooMVC ou outros framework "eventos".)</span><span class="sxs-lookup"><span data-stu-id="99aa3-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="99aa3-146">Inserir `TrackEvent` chamadas em seu código toocount vários eventos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="99aa3-147">Com que frequência os usuários escolhem um determinado recurso, com que frequência eles atingem metas específicas ou talvez com que frequência cometem tipos de erro específicos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="99aa3-148">Por exemplo, em um aplicativo de jogo, envie um evento sempre que um usuário wins jogo hello:</span><span class="sxs-lookup"><span data-stu-id="99aa3-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="99aa3-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="99aa3-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="99aa3-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="99aa3-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="99aa3-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="99aa3-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="99aa3-153">Exibir os eventos no portal do Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="99aa3-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="99aa3-154">toosee uma contagem de seus eventos, abra um [Metrics Explorer](app-insights-metrics-explorer.md) folha, adicionar um novo gráfico e selecione **eventos**.</span><span class="sxs-lookup"><span data-stu-id="99aa3-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Ver uma contagem de eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="99aa3-156">contagens de saudação toocompare eventos diferentes, definir o tipo de gráfico de saudação muito**grade**e de grupo pelo nome do evento:</span><span class="sxs-lookup"><span data-stu-id="99aa3-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Defina o tipo de gráfico de saudação e agrupamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="99aa3-158">Na grade de hello, clique em um nome toosee individuais as ocorrências de eventos que o evento.</span><span class="sxs-lookup"><span data-stu-id="99aa3-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="99aa3-159">toosee mais detalham - clique em qualquer ocorrência na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-159">toosee more detail - click any occurrence in hello list.</span></span>

![Drill-through eventos Olá](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="99aa3-161">toofocus em eventos específicos em pesquisa ou Metrics Explorer filtro toohello nomes de evento do conjunto Olá folha que você estiver interessado em:</span><span class="sxs-lookup"><span data-stu-id="99aa3-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Abra Filtros, expanda o Nome do evento e selecione um ou mais valores](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="99aa3-163">Eventos personalizados na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-163">Custom events in Analytics</span></span>

<span data-ttu-id="99aa3-164">Telemetria Hello está disponível no hello `customEvents` tabela [aplicativo Insights análise](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="99aa3-165">Cada linha representa uma chamada muito`trackEvent(..)` em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="99aa3-166">Se [amostragem](app-insights-sampling.md) está em operação, a propriedade itemCount de saudação mostra um valor maior que 1.</span><span class="sxs-lookup"><span data-stu-id="99aa3-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="99aa3-167">Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackEvent(), processo de amostragem Olá transmitido apenas um deles.</span><span class="sxs-lookup"><span data-stu-id="99aa3-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="99aa3-168">tooget uma contagem correta de eventos personalizados, você deve usar, portanto, usar o código como `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="99aa3-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="99aa3-169">TrackMetric</span></span>

<span data-ttu-id="99aa3-170">Application Insights pode métricas que não estão anexados tooparticular eventos do gráfico.</span><span class="sxs-lookup"><span data-stu-id="99aa3-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="99aa3-171">Por exemplo, você pode monitorar um comprimento de fila em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="99aa3-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="99aa3-172">Com métricas, medidas individuais Olá são menos interessantes que variações hello e tendências e então estatísticos gráficos são úteis.</span><span class="sxs-lookup"><span data-stu-id="99aa3-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="99aa3-173">Em ordem toosend métricas tooApplication Insights, você pode usar o hello `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="99aa3-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="99aa3-174">Há dois toosend de maneiras uma métrica:</span><span class="sxs-lookup"><span data-stu-id="99aa3-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="99aa3-175">Valor único.</span><span class="sxs-lookup"><span data-stu-id="99aa3-175">Single value.</span></span> <span data-ttu-id="99aa3-176">Toda vez que você realiza uma medida em seu aplicativo, você enviar valor correspondente Olá tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="99aa3-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="99aa3-177">Por exemplo, suponha que você tenha uma métrica que descreve o número de saudação de itens em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="99aa3-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="99aa3-178">Durante um período de tempo específico, você primeiro colocar três itens em contêiner hello e, em seguida, remova dois itens.</span><span class="sxs-lookup"><span data-stu-id="99aa3-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="99aa3-179">Da mesma forma, você poderia chamar `TrackMetric` duas vezes: primeiro passar o valor de saudação `3` e, em seguida, Olá valor `-2`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="99aa3-180">O Application Insights armazena os dois valores em seu nome.</span><span class="sxs-lookup"><span data-stu-id="99aa3-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="99aa3-181">Agregação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-181">Aggregation.</span></span> <span data-ttu-id="99aa3-182">Ao trabalhar com as métricas, raramente há interesse em cada medida.</span><span class="sxs-lookup"><span data-stu-id="99aa3-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="99aa3-183">Em vez disso, um resumo do que aconteceu durante um determinado período de tempo é importante.</span><span class="sxs-lookup"><span data-stu-id="99aa3-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="99aa3-184">Esse tipo de resumo é chamado de _agregação_.</span><span class="sxs-lookup"><span data-stu-id="99aa3-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="99aa3-185">Olá, o exemplo acima, Olá métrica soma de agregação daquele período de tempo é `1` e contagem de Olá Olá dos valores das métricas é `2`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="99aa3-186">Ao usar a abordagem de agregação hello, apenas invocar `TrackMetric` uma vez por hora período e enviar Olá valores de agregação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="99aa3-187">Isso é hello abordagem recomendada, pois ele pode reduzir significativamente o custo de saudação e desempenho sobrecarga enviando dados menos pontos tooApplication Insights, enquanto ainda coleta todas as informações relevantes.</span><span class="sxs-lookup"><span data-stu-id="99aa3-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="99aa3-188">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="99aa3-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="99aa3-189">Valores únicos</span><span class="sxs-lookup"><span data-stu-id="99aa3-189">Single values</span></span>

<span data-ttu-id="99aa3-190">toosend um único valor de métrica:</span><span class="sxs-lookup"><span data-stu-id="99aa3-190">toosend a single metric value:</span></span>

<span data-ttu-id="99aa3-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="99aa3-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="99aa3-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="99aa3-193">Métricas de agregação</span><span class="sxs-lookup"><span data-stu-id="99aa3-193">Aggregating metrics</span></span>

<span data-ttu-id="99aa3-194">É recomendável tooaggregate métricas antes de enviá-los do seu aplicativo, largura de banda tooreduce, tooimprove e o custo de desempenho.</span><span class="sxs-lookup"><span data-stu-id="99aa3-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="99aa3-195">Aqui está um exemplo de código de agregação:</span><span class="sxs-lookup"><span data-stu-id="99aa3-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="99aa3-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="99aa3-197">Métricas personalizadas no Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="99aa3-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="99aa3-198">resultados de saudação toosee, abra Metrics Explorer e adicione um novo gráfico.</span><span class="sxs-lookup"><span data-stu-id="99aa3-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="99aa3-199">Edite saudação gráfico tooshow sua métrica.</span><span class="sxs-lookup"><span data-stu-id="99aa3-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="99aa3-200">A métrica personalizada pode levar vários tooappear de minutos na lista de saudação de métricas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="99aa3-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Adicionar um novo gráfico ou escolher um e, em Personalizar, escolher a métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="99aa3-202">Métricas personalizadas no Analytics</span><span class="sxs-lookup"><span data-stu-id="99aa3-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="99aa3-203">Telemetria Hello está disponível no hello `customMetrics` tabela [aplicativo Insights análise](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="99aa3-204">Cada linha representa uma chamada muito`trackMetric(..)` em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="99aa3-205">`valueSum`-Esta é a soma de saudação de medidas de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="99aa3-206">valor médio tooget hello, divisão por `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="99aa3-207">`valueCount`-Olá número de medidas que foram agregados em isso `trackMetric(..)` chamar.</span><span class="sxs-lookup"><span data-stu-id="99aa3-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="99aa3-208">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="99aa3-208">Page views</span></span>
<span data-ttu-id="99aa3-209">Em um aplicativo de página da Web ou dispositivo, a telemetria de exibição de páginas é enviada por padrão quando cada tela ou página é carregada.</span><span class="sxs-lookup"><span data-stu-id="99aa3-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="99aa3-210">Mas você pode alterar modos de exibição de página que tootrack em horários adicionais ou diferentes.</span><span class="sxs-lookup"><span data-stu-id="99aa3-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="99aa3-211">Por exemplo, em um aplicativo que exibe as guias ou em folhas, convém tootrack uma página sempre que o usuário Olá abre uma nova folha.</span><span class="sxs-lookup"><span data-stu-id="99aa3-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Lentes de Utilização na folha Visão geral](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="99aa3-213">Dados de usuário e a sessão são enviados como propriedades junto com os modos de exibição de página, portanto Olá gráficos de usuário e a sessão ficar ativos quando não há telemetria de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="99aa3-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="99aa3-214">Exibições de páginas personalizadas</span><span class="sxs-lookup"><span data-stu-id="99aa3-214">Custom page views</span></span>
<span data-ttu-id="99aa3-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="99aa3-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="99aa3-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="99aa3-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="99aa3-218">Se você tiver várias guias em diferentes páginas HTML, você pode especificar a URL de saudação muito:</span><span class="sxs-lookup"><span data-stu-id="99aa3-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="99aa3-219">Definindo o tempo das exibições de página</span><span class="sxs-lookup"><span data-stu-id="99aa3-219">Timing page views</span></span>
<span data-ttu-id="99aa3-220">Por padrão, os tempos de saudação relatado como **tempo de carregamento da exibição de página** são medidas da quando navegador Olá envia a solicitação de hello, até que o evento de carregamento de página do navegador Olá é chamado.</span><span class="sxs-lookup"><span data-stu-id="99aa3-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="99aa3-221">Em vez disso, é possível:</span><span class="sxs-lookup"><span data-stu-id="99aa3-221">Instead, you can either:</span></span>

* <span data-ttu-id="99aa3-222">Defina uma duração explícita em Olá [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) chamar: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="99aa3-223">Use chamadas de intervalo de exibição de página Olá `startTrackPage` e `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="99aa3-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="99aa3-225">...</span><span class="sxs-lookup"><span data-stu-id="99aa3-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="99aa3-226">Olá nome que você usa como o primeiro parâmetro de saudação associa início hello e parar de chamadas.</span><span class="sxs-lookup"><span data-stu-id="99aa3-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="99aa3-227">O padrão é o nome de página atual toohello.</span><span class="sxs-lookup"><span data-stu-id="99aa3-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="99aa3-228">carregamento de página resultante Olá durações exibidas no Gerenciador de métricas são derivadas do intervalo de saudação entre hello iniciar e parar de chamadas.</span><span class="sxs-lookup"><span data-stu-id="99aa3-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="99aa3-229">É o tooyou o intervalo de tempo realmente.</span><span class="sxs-lookup"><span data-stu-id="99aa3-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="99aa3-230">Telemetria de página na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="99aa3-231">Na [Análise](app-insights-analytics.md), duas tabelas mostram dados das operações do navegador:</span><span class="sxs-lookup"><span data-stu-id="99aa3-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="99aa3-232">Olá `pageViews` tabela contém dados sobre Olá URL e título da página</span><span class="sxs-lookup"><span data-stu-id="99aa3-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="99aa3-233">Olá `browserTimings` tabela contém dados sobre o desempenho do cliente, como tooprocess de tempo gasto Olá Olá os dados de entrada</span><span class="sxs-lookup"><span data-stu-id="99aa3-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="99aa3-234">toofind quanto tempo o navegador Olá leva tooprocess páginas diferentes:</span><span class="sxs-lookup"><span data-stu-id="99aa3-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="99aa3-235">toodiscover popularities de saudação de navegadores diferentes:</span><span class="sxs-lookup"><span data-stu-id="99aa3-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="99aa3-236">chamadas de tooAJAX de modos de exibição de página tooassociate, junção com dependências:</span><span class="sxs-lookup"><span data-stu-id="99aa3-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="99aa3-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="99aa3-237">TrackRequest</span></span>
<span data-ttu-id="99aa3-238">servidor de saudação SDK usa solicitações HTTP toolog TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="99aa3-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="99aa3-239">Você também pode chamá-lo por conta própria se você quiser toosimulate solicitações em um contexto em que você não tem Olá web serviço módulo está em execução.</span><span class="sxs-lookup"><span data-stu-id="99aa3-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="99aa3-240">No entanto, a saudação recomendado telemetria de solicitação do modo toosend é onde a solicitação de saudação atua como um <a href="#operation-context">contexto de operação</a>.</span><span class="sxs-lookup"><span data-stu-id="99aa3-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="99aa3-241">Contexto de operação</span><span class="sxs-lookup"><span data-stu-id="99aa3-241">Operation context</span></span>
<span data-ttu-id="99aa3-242">Você pode associar itens de telemetria juntos anexando toothem uma ID de operação comum.</span><span class="sxs-lookup"><span data-stu-id="99aa3-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="99aa3-243">módulo de rastreamento de solicitação padrão Olá faz isso para exceções e outros eventos que são enviados enquanto uma solicitação HTTP está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="99aa3-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="99aa3-244">Em [pesquisa](app-insights-diagnostic-search.md) e [análise](app-insights-analytics.md), você pode usar todos os eventos associados à solicitação Olá Olá ID tooeasily localizar.</span><span class="sxs-lookup"><span data-stu-id="99aa3-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="99aa3-245">Olá mais fácil maneira tooset Olá ID é tooset um contexto de operação usando esse padrão:</span><span class="sxs-lookup"><span data-stu-id="99aa3-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="99aa3-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="99aa3-247">Junto com a configuração de um contexto de operação, `StartOperation` cria um item de telemetria do tipo hello que você especificar.</span><span class="sxs-lookup"><span data-stu-id="99aa3-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="99aa3-248">Ele envia a telemetria Olá item quando você descartar operação hello, ou se você chamar explicitamente `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="99aa3-249">Se você usar `RequestTelemetry` como tipo de telemetria hello, sua duração é definir o intervalo de toohello atingiu o tempo entre o início e parada.</span><span class="sxs-lookup"><span data-stu-id="99aa3-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="99aa3-250">Contextos de operação não podem ser aninhados.</span><span class="sxs-lookup"><span data-stu-id="99aa3-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="99aa3-251">Se já há um contexto de operação, sua ID é associado a todos os itens de saudação contido, inclusive Olá item criado com `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="99aa3-252">Na pesquisa, o contexto de operação de saudação é Olá toocreate usado **itens relacionados** lista:</span><span class="sxs-lookup"><span data-stu-id="99aa3-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Itens relacionados](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="99aa3-254">Consulte [application-insights-custom-operations-tracking.md] para obter mais informações sobre operações personalizadas de acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="99aa3-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="99aa3-255">Consultas na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-255">Requests in Analytics</span></span> 

<span data-ttu-id="99aa3-256">Em [análises do aplicativo Insights](app-insights-analytics.md), solicitações de mostrar o em Olá `requests` tabela.</span><span class="sxs-lookup"><span data-stu-id="99aa3-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="99aa3-257">Se [amostragem](app-insights-sampling.md) está em operação, propriedade itemCount de saudação mostrará um valor maior que 1.</span><span class="sxs-lookup"><span data-stu-id="99aa3-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="99aa3-258">Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackRequest(), processo de amostragem Olá transmitido apenas um deles.</span><span class="sxs-lookup"><span data-stu-id="99aa3-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="99aa3-259">uma contagem correta das solicitações e duração média de tooget segmentadas por nomes de solicitação, use um código como:</span><span class="sxs-lookup"><span data-stu-id="99aa3-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="99aa3-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="99aa3-260">TrackException</span></span>
<span data-ttu-id="99aa3-261">Envie exceções tooApplication Insights:</span><span class="sxs-lookup"><span data-stu-id="99aa3-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="99aa3-262">muito[contar](app-insights-metrics-explorer.md), como uma indicação de frequência de saudação de um problema.</span><span class="sxs-lookup"><span data-stu-id="99aa3-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="99aa3-263">muito[examinar ocorrências individuais](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="99aa3-264">Olá relatórios incluem rastreamentos de pilha de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="99aa3-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="99aa3-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="99aa3-267">Olá SDKs catch muitas exceções automaticamente, para que você não tenha sempre toocall TrackException explicitamente.</span><span class="sxs-lookup"><span data-stu-id="99aa3-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="99aa3-268">ASP.NET: [escrever código exceções toocatch](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="99aa3-269">J2EE: [as exceções são capturadas automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="99aa3-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="99aa3-270">JavaScript: exceções são capturadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="99aa3-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="99aa3-271">Coleta automática de toodisable, adicione um trecho de código toohello de linha que você inserir em suas páginas da Web:</span><span class="sxs-lookup"><span data-stu-id="99aa3-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="99aa3-272">Exceções na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-272">Exceptions in Analytics</span></span>

<span data-ttu-id="99aa3-273">Em [aplicativo Insights análise](app-insights-analytics.md), exceções aparecem no hello `exceptions` tabela.</span><span class="sxs-lookup"><span data-stu-id="99aa3-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="99aa3-274">Se [amostragem](app-insights-sampling.md) está em operação, hello `itemCount` propriedade mostra um valor maior que 1.</span><span class="sxs-lookup"><span data-stu-id="99aa3-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="99aa3-275">Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackException(), processo de amostragem Olá transmitido apenas um deles.</span><span class="sxs-lookup"><span data-stu-id="99aa3-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="99aa3-276">tooget uma contagem correta de exceções segmentadas por tipo de exceção, use um código como:</span><span class="sxs-lookup"><span data-stu-id="99aa3-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="99aa3-277">A maioria das Olá importante informações de pilha já são extraídas em variáveis separadas, mas você pode extrair Olá separar `details` estrutura tooget mais.</span><span class="sxs-lookup"><span data-stu-id="99aa3-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="99aa3-278">Como essa estrutura é dinâmica, você deve converter o tipo de toohello do hello resultado esperado.</span><span class="sxs-lookup"><span data-stu-id="99aa3-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="99aa3-279">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99aa3-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="99aa3-280">exceções de tooassociate com suas solicitações relacionadas, use uma junção:</span><span class="sxs-lookup"><span data-stu-id="99aa3-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="99aa3-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="99aa3-281">TrackTrace</span></span>
<span data-ttu-id="99aa3-282">Use TrackTrace toohelp diagnosticar problemas enviando um tooApplication "trilha de navegação estrutural" Insights.</span><span class="sxs-lookup"><span data-stu-id="99aa3-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="99aa3-283">Você pode enviar partes de dados de diagnóstico e inspecioná-los na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="99aa3-284">[Adaptadores de log](app-insights-asp-net-trace-logs.md) usar este portal de toohello API toosend logs de terceiros.</span><span class="sxs-lookup"><span data-stu-id="99aa3-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="99aa3-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="99aa3-286">Você pode pesquisar no conteúdo da mensagem, mas (diferentemente de valores de propriedade) não é possível filtrar nele.</span><span class="sxs-lookup"><span data-stu-id="99aa3-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="99aa3-287">limite de tamanho de saudação no `message` é muito maior do que o limite de saudação em Propriedades.</span><span class="sxs-lookup"><span data-stu-id="99aa3-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="99aa3-288">Uma vantagem de TrackTrace é que você pode colocar dados relativamente longos na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="99aa3-289">Por exemplo, você pode codificar dados POST.</span><span class="sxs-lookup"><span data-stu-id="99aa3-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="99aa3-290">Além disso, você pode adicionar uma mensagem de tooyour nível de severidade.</span><span class="sxs-lookup"><span data-stu-id="99aa3-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="99aa3-291">E, como outros telemetria, você pode adicionar toohelp de valores de propriedade que você filtrar ou pesquisar para diferentes conjuntos de rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="99aa3-292">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99aa3-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="99aa3-293">Em [pesquisa](app-insights-diagnostic-search.md), você pode, em seguida, facilmente filtrar todas as mensagens de saudação de um nível de severidade específico que se relacionam tooa determinado banco de dados.</span><span class="sxs-lookup"><span data-stu-id="99aa3-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="99aa3-294">Rastreamentos na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-294">Traces in Analytics</span></span>

<span data-ttu-id="99aa3-295">Em [aplicativo Insights análise](app-insights-analytics.md), chama tooTrackTrace Mostrar em Olá `traces` tabela.</span><span class="sxs-lookup"><span data-stu-id="99aa3-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="99aa3-296">Se [amostragem](app-insights-sampling.md) está em operação, a propriedade itemCount de saudação mostra um valor maior que 1.</span><span class="sxs-lookup"><span data-stu-id="99aa3-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="99aa3-297">Para exemplo itemCount = = 10 significa que de 10 chamadas muito`trackTrace()`, processo de amostragem Olá transmitido apenas um deles.</span><span class="sxs-lookup"><span data-stu-id="99aa3-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="99aa3-298">tooget uma contagem correta de chamadas de rastreamento, você deve usar, portanto, código, como `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="99aa3-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="99aa3-299">TrackDependency</span></span>
<span data-ttu-id="99aa3-300">Olá Use TrackDependency chamar tempos de resposta de saudação tootrack e taxas de sucesso de parte externa de tooan de chamadas do código.</span><span class="sxs-lookup"><span data-stu-id="99aa3-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="99aa3-301">os resultados de saudação aparecem nos gráficos de dependência Olá no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="99aa3-302">Lembre-se de servidor Olá SDKs incluem um [módulo de dependência](app-insights-asp-net-dependencies.md) que detecta e rastreia determinadas chamadas de dependência automaticamente – por exemplo, toodatabases e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="99aa3-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="99aa3-303">Você tem um agente em seu módulo de saudação do servidor toomake de tooinstall trabalhar.</span><span class="sxs-lookup"><span data-stu-id="99aa3-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="99aa3-304">Você usar essa chamada chamadas tootrack Olá controle automatizada não catch, ou se não deseja que o agente de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="99aa3-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="99aa3-305">Editar tooturn fora do módulo de controle de dependência padrão hello, [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) e excluir referência Olá muito`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="99aa3-306">Dependências na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-306">Dependencies in Analytics</span></span>

<span data-ttu-id="99aa3-307">Em [aplicativo Insights análise](app-insights-analytics.md), chamadas trackDependency aparecem no hello `dependencies` tabela.</span><span class="sxs-lookup"><span data-stu-id="99aa3-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="99aa3-308">Se [amostragem](app-insights-sampling.md) está em operação, a propriedade itemCount de saudação mostra um valor maior que 1.</span><span class="sxs-lookup"><span data-stu-id="99aa3-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="99aa3-309">Para exemplo itemCount = = 10 significa que de 10 chamadas tootrackDependency(), processo de amostragem Olá transmitido apenas um deles.</span><span class="sxs-lookup"><span data-stu-id="99aa3-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="99aa3-310">tooget uma contagem correta de dependências segmentadas por componente de destino, use um código como:</span><span class="sxs-lookup"><span data-stu-id="99aa3-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="99aa3-311">dependências de tooassociate com suas solicitações relacionadas, use uma junção:</span><span class="sxs-lookup"><span data-stu-id="99aa3-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="99aa3-312">Liberando dados</span><span class="sxs-lookup"><span data-stu-id="99aa3-312">Flushing data</span></span>
<span data-ttu-id="99aa3-313">Normalmente, Olá SDK envia dados às vezes escolhidos o impacto de saudação toominimize usuário hello.</span><span class="sxs-lookup"><span data-stu-id="99aa3-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="99aa3-314">No entanto, em alguns casos, convém buffer de saudação tooflush – por exemplo, se você estiver usando Olá SDK em um aplicativo que é desligado.</span><span class="sxs-lookup"><span data-stu-id="99aa3-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="99aa3-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="99aa3-316">Observe que a função hello é assíncrona para Olá [canal de telemetria de servidor](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="99aa3-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="99aa3-317">usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="99aa3-317">Authenticated users</span></span>
<span data-ttu-id="99aa3-318">Em um aplicativo Web, os usuários são (por padrão) identificados por cookies.</span><span class="sxs-lookup"><span data-stu-id="99aa3-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="99aa3-319">Um usuário pode ser contado mais de uma vez se ele acessar seu aplicativo de um computador ou navegador diferente, ou se ele excluir cookies.</span><span class="sxs-lookup"><span data-stu-id="99aa3-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="99aa3-320">Se os usuários entrarem no aplicativo tooyour, você pode obter uma contagem mais precisa, definindo Olá autenticado ID de usuário no código de saudação do navegador:</span><span class="sxs-lookup"><span data-stu-id="99aa3-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="99aa3-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="99aa3-322">Em um aplicativo MVC Web ASP.NET, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99aa3-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="99aa3-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="99aa3-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="99aa3-324">Não é necessário toouse Olá nome do usuário real entrar.</span><span class="sxs-lookup"><span data-stu-id="99aa3-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="99aa3-325">Ele só tem toobe uma ID de usuário toothat exclusivo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="99aa3-326">Não é possível incluir espaços ou caracteres de saudação `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="99aa3-327">ID de usuário Olá também é definido em um cookie de sessão e enviado toohello server.</span><span class="sxs-lookup"><span data-stu-id="99aa3-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="99aa3-328">Se o servidor de saudação SDK está instalado, Olá autenticado usuário que ID é enviado como parte das propriedades de contexto de saudação de telemetria de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="99aa3-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="99aa3-329">Assim, você poderá filtrar e pesquisar nele.</span><span class="sxs-lookup"><span data-stu-id="99aa3-329">You can then filter and search on it.</span></span>

<span data-ttu-id="99aa3-330">Se seu aplicativo de grupos de usuários de contas, você também pode passar um identificador para a conta de saudação (com hello mesmo caractere restrições).</span><span class="sxs-lookup"><span data-stu-id="99aa3-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="99aa3-331">No [Metrics Explorer](app-insights-metrics-explorer.md), você pode criar um gráfico que contabiliza **Usuários Autenticados** e **Contas de usuário**.</span><span class="sxs-lookup"><span data-stu-id="99aa3-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="99aa3-332">Você também pode [pesquisar](app-insights-diagnostic-search.md) por pontos de dados do cliente com contas e nomes de usuário específicos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="99aa3-333"><a name="properties"></a>Filtragem, pesquisa e segmentação de dados usando propriedades</span><span class="sxs-lookup"><span data-stu-id="99aa3-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="99aa3-334">Você pode anexar as medidas e propriedades tooyour eventos (e também toometrics, modos de exibição de página, exceções e outros dados de telemetria).</span><span class="sxs-lookup"><span data-stu-id="99aa3-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="99aa3-335">*Propriedades* são valores de cadeia de caracteres que você pode usar toofilter sua telemetria nos relatórios de uso de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="99aa3-336">Por exemplo, se seu aplicativo oferece diversos jogos, pode anexar nome saudação do evento de jogo tooeach Olá para que você possa ver os jogos que são mais populares.</span><span class="sxs-lookup"><span data-stu-id="99aa3-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="99aa3-337">Há um limite de 8192 para o comprimento da cadeia de caracteres hello.</span><span class="sxs-lookup"><span data-stu-id="99aa3-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="99aa3-338">(Se você quiser toosend grandes quantidades de dados, use o parâmetro de mensagem de saudação do [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="99aa3-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="99aa3-339">*Métricas* são valores numéricos que podem ser apresentados graficamente.</span><span class="sxs-lookup"><span data-stu-id="99aa3-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="99aa3-340">Por exemplo, convém toosee se não houver um aumento gradual pontuações de saudação atingir seu jogadores.</span><span class="sxs-lookup"><span data-stu-id="99aa3-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="99aa3-341">gráficos de saudação podem ser segmentados por Olá propriedades que são enviadas com o evento hello, para que você possa obter separam ou empilhados gráficos de jogos diferentes.</span><span class="sxs-lookup"><span data-stu-id="99aa3-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="99aa3-342">Para toobe de valores da métrica exibido corretamente, eles devem ser too0 maior que ou igual.</span><span class="sxs-lookup"><span data-stu-id="99aa3-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="99aa3-343">Há alguns [limites no número de saudação de propriedades, valores de propriedade e métricas](#limits) que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="99aa3-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="99aa3-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="99aa3-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="99aa3-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="99aa3-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="99aa3-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="99aa3-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="99aa3-348">Tome cuidado toolog informações de identificação pessoal em Propriedades.</span><span class="sxs-lookup"><span data-stu-id="99aa3-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="99aa3-349">*Se você usou métricas*, abra Metrics Explorer e selecione a métrica de saudação do hello **personalizado** grupo:</span><span class="sxs-lookup"><span data-stu-id="99aa3-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Abra o Explorer métricas de gráfico selecione Olá e selecione a métrica Olá](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="99aa3-351">Se a métrica não aparecer, ou se hello **personalizado** título não estiver lá, folha de seleção Olá fechar e tente novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="99aa3-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="99aa3-352">As métricas, às vezes, podem levar uma hora toobe agregados por meio do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="99aa3-353">*Se você usou propriedades e métricas*, segmentar métrica Olá pela propriedade hello:</span><span class="sxs-lookup"><span data-stu-id="99aa3-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Definir o agrupamento e, em seguida, selecione a propriedade Olá em Agrupar por](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="99aa3-355">*Na pesquisa de diagnóstico*, você pode exibir as propriedades de saudação e métricas de ocorrências individuais de um evento.</span><span class="sxs-lookup"><span data-stu-id="99aa3-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Selecionar uma instância e, em seguida, "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="99aa3-357">Saudação de uso **pesquisa** campo toosee ocorrências de eventos que têm um valor de propriedade em particular.</span><span class="sxs-lookup"><span data-stu-id="99aa3-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Digite um termo em Pesquisar](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="99aa3-359">[Saiba mais sobre as expressões de pesquisa](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="99aa3-360">Propriedades de tooset de maneira alternativa e métricas</span><span class="sxs-lookup"><span data-stu-id="99aa3-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="99aa3-361">Se for mais conveniente, você pode coletar parâmetros de saudação de um evento em um objeto separado:</span><span class="sxs-lookup"><span data-stu-id="99aa3-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="99aa3-362">Não reutilizar Olá mesma instância de item de telemetria (`event` neste exemplo) toocall Track*() várias vezes.</span><span class="sxs-lookup"><span data-stu-id="99aa3-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="99aa3-363">Isso pode causar toobe telemetria enviada com a configuração incorreta.</span><span class="sxs-lookup"><span data-stu-id="99aa3-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="99aa3-364">Medidas personalizadas e propriedades na Análise</span><span class="sxs-lookup"><span data-stu-id="99aa3-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="99aa3-365">Em [análise](app-insights-analytics.md), métricas personalizadas e propriedades mostram em Olá `customMeasurements` e `customDimensions` atributos de cada registro de telemetria.</span><span class="sxs-lookup"><span data-stu-id="99aa3-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="99aa3-366">Por exemplo, se você adicionou uma propriedade chamada "jogo" tooyour telemetria de solicitação, essa consulta contagens de ocorrências de saudação de valores diferentes de "jogo" e mostrar a média de saudação de saudação métrica personalizada "pontuação":</span><span class="sxs-lookup"><span data-stu-id="99aa3-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="99aa3-367">Observe que:</span><span class="sxs-lookup"><span data-stu-id="99aa3-367">Notice that:</span></span>

* <span data-ttu-id="99aa3-368">Quando você extrai um valor de saudação customDimensions ou customMeasurements JSON, ele tem o tipo dinâmico e portanto você deve converter `tostring` ou `todouble`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="99aa3-369">conta de tootake da possibilidade de saudação do [amostragem](app-insights-sampling.md), você deve usar `sum(itemCount)`, não `count()`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="99aa3-370"><a name="timed"></a> Eventos de tempo</span><span class="sxs-lookup"><span data-stu-id="99aa3-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="99aa3-371">Às vezes, você deseja toochart quanto tempo demora tooperform uma ação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="99aa3-372">Por exemplo, você talvez queira tooknow quanto tempo os usuários tomem tooconsider escolhas em um jogo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="99aa3-373">Você pode usar o parâmetro de medição de saudação para isso.</span><span class="sxs-lookup"><span data-stu-id="99aa3-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="99aa3-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="99aa3-375"><a name="defaults"></a>Propriedades padrão para telemetria personalizada</span><span class="sxs-lookup"><span data-stu-id="99aa3-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="99aa3-376">Se você quiser tooset valores de propriedade de padrão para alguns dos Olá eventos personalizados que você escreve, você pode defini-las em uma instância de TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="99aa3-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="99aa3-377">Eles são anexados tooevery item de telemetria que é enviada do cliente.</span><span class="sxs-lookup"><span data-stu-id="99aa3-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="99aa3-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="99aa3-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="99aa3-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="99aa3-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="99aa3-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="99aa3-381">Chamadas de telemetria individuais podem substituir valores de padrão de Olá nos dicionários de sua propriedade.</span><span class="sxs-lookup"><span data-stu-id="99aa3-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="99aa3-382">*Para clientes Web JavaScript*, [use inicializadores de telemetria JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="99aa3-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="99aa3-383">*Telemetria de tooall propriedades tooadd*, incluindo dados de saudação de módulos de coleção padrão [implementar `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="99aa3-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="99aa3-384">Amostragem, filtragem e processamento da telemetria</span><span class="sxs-lookup"><span data-stu-id="99aa3-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="99aa3-385">Você pode escrever código tooprocess sua telemetria antes do envio de saudação SDK.</span><span class="sxs-lookup"><span data-stu-id="99aa3-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="99aa3-386">processamento de saudação inclui dados que são enviados de módulos de telemetria padrão hello, como coleta de solicitação HTTP e a coleção de dependência.</span><span class="sxs-lookup"><span data-stu-id="99aa3-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="99aa3-387">[Adicionar propriedades](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="99aa3-388">Por exemplo, é possível adicionar números de versão ou valores que são calculados de outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="99aa3-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="99aa3-389">[Filtragem](app-insights-api-filtering-sampling.md#filtering) pode modificar ou descartar telemetria antes do envio de saudação SDK implementando `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="99aa3-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="99aa3-390">Controlar o que é enviado ou descartado, mas tem tooaccount para efeito de saudação em suas métricas.</span><span class="sxs-lookup"><span data-stu-id="99aa3-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="99aa3-391">Dependendo de como você descartar itens, você poderá perder Olá capacidade toonavigate entre itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="99aa3-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="99aa3-392">[Amostragem](app-insights-api-filtering-sampling.md) tooreduce solução Olá do volume dos dados que são enviados de seu portal de toohello do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="99aa3-393">Isso é feito sem afetar as métricas de saudação exibida.</span><span class="sxs-lookup"><span data-stu-id="99aa3-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="99aa3-394">E isso é feito sem afetar os problemas de capacidade toodiagnose navegando entre itens relacionados, como exceções, solicitações e modos de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="99aa3-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="99aa3-395">[Saiba mais](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="99aa3-396">Desabilitando a telemetria</span><span class="sxs-lookup"><span data-stu-id="99aa3-396">Disabling telemetry</span></span>
<span data-ttu-id="99aa3-397">muito*dinamicamente parar e iniciar* Olá coleta e transmissão de telemetria:</span><span class="sxs-lookup"><span data-stu-id="99aa3-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="99aa3-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="99aa3-399">muito*desabilitar os coletores padrão selecionados*– por exemplo, contadores de desempenho, as solicitações HTTP ou dependências – exclua ou comente a linhas relevantes Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Você pode fazer isso, por exemplo, se você quiser toosend seus próprios dados TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="99aa3-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="99aa3-400"><a name="debug"></a>Modo de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="99aa3-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="99aa3-401">Durante a depuração, é útil toohave sua telemetria acelerada por meio do pipeline de saudação para que você possa ver os resultados imediatamente.</span><span class="sxs-lookup"><span data-stu-id="99aa3-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="99aa3-402">Você também obter mensagens adicionais que ajudarão a rastrear problemas com a telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="99aa3-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="99aa3-403">Desative-a na produção, pois isso pode tornar seu aplicativo mais lento.</span><span class="sxs-lookup"><span data-stu-id="99aa3-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="99aa3-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="99aa3-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="99aa3-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="99aa3-406"><a name="ikey"></a>Definindo a chave de instrumentação Olá para telemetria personalizada selecionada</span><span class="sxs-lookup"><span data-stu-id="99aa3-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="99aa3-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="99aa3-408"><a name="dynamic-ikey"></a> Chave de instrumentação dinâmica</span><span class="sxs-lookup"><span data-stu-id="99aa3-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="99aa3-409">tooavoid mistura de telemetria de desenvolvimento, teste e ambientes de produção, você pode [criar recursos do Application Insights separados](app-insights-create-new-resource.md) e altere suas chaves, dependendo do ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="99aa3-410">Em vez de obter a chave de instrumentação Olá Olá do arquivo de configuração, você pode definir no seu código.</span><span class="sxs-lookup"><span data-stu-id="99aa3-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="99aa3-411">Chave de saudação definida em um método de inicialização, como global.aspx.cs em um serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="99aa3-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="99aa3-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="99aa3-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="99aa3-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="99aa3-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="99aa3-414">Em páginas da Web, você pode querer tooset do servidor da web hello estado, em vez de codificá-lo literalmente em script hello.</span><span class="sxs-lookup"><span data-stu-id="99aa3-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="99aa3-415">Por exemplo, em uma página da Web gerada em um aplicativo ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="99aa3-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="99aa3-416">*JavaScript no Razor*</span><span class="sxs-lookup"><span data-stu-id="99aa3-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="99aa3-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="99aa3-417">TelemetryContext</span></span>
<span data-ttu-id="99aa3-418">TelemetryClient tem uma propriedade de Contexto, que contém valores que serão enviadas com todos os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="99aa3-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="99aa3-419">Eles normalmente são definidos pelos módulos de telemetria padrão hello, mas você pode também defini-las por conta própria.</span><span class="sxs-lookup"><span data-stu-id="99aa3-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="99aa3-420">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99aa3-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="99aa3-421">Se você definir esses valores por conta própria, considere remover a linha relevante de saudação do [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), de modo que seus valores e valores padrão de saudação não fiquem confusos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="99aa3-422">**Componente**: Olá aplicativo e sua versão.</span><span class="sxs-lookup"><span data-stu-id="99aa3-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="99aa3-423">**Dispositivo**: dados sobre o dispositivo Olá onde o aplicativo hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="99aa3-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="99aa3-424">(Em aplicativos da web, isso é servidor hello ou dispositivo de cliente enviado da telemetria hello.)</span><span class="sxs-lookup"><span data-stu-id="99aa3-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="99aa3-425">**InstrumentationKey**: Olá recurso do Application Insights no Azure, onde a telemetria Olá aparecem.</span><span class="sxs-lookup"><span data-stu-id="99aa3-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="99aa3-426">Normalmente, escolhido no Applicationinsights.config.</span><span class="sxs-lookup"><span data-stu-id="99aa3-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="99aa3-427">**Local**: Olá localização geográfica do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="99aa3-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="99aa3-428">**Operação**: em aplicativos da web, Olá solicitação HTTP atual.</span><span class="sxs-lookup"><span data-stu-id="99aa3-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="99aa3-429">Em outros tipos de aplicativo, você pode definir essa eventos toogroup juntos.</span><span class="sxs-lookup"><span data-stu-id="99aa3-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="99aa3-430">**ID**: um valor gerado que correlaciona eventos diferentes para que, ao inspecionar qualquer evento na Pesquisa de Diagnóstico, você possa localizar itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="99aa3-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="99aa3-431">**Nome**: um identificador, geralmente Olá URL da solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="99aa3-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="99aa3-432">**SyntheticSource**: se não nula ou vazia, uma cadeia de caracteres que indica que essa fonte Olá da solicitação de saudação foi identificada como um teste da web ou robô.</span><span class="sxs-lookup"><span data-stu-id="99aa3-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="99aa3-433">Por padrão, ela é excluída dos cálculos no Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="99aa3-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="99aa3-434">**Propriedades**: propriedades que são enviadas com todos os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="99aa3-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="99aa3-435">Pode ser substituído nas chamadas individuais de Track*.</span><span class="sxs-lookup"><span data-stu-id="99aa3-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="99aa3-436">**Sessão**: Olá sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="99aa3-436">**Session**: hello user's session.</span></span> <span data-ttu-id="99aa3-437">Olá ID estiver definido como valor tooa gerado, que é alterado quando o usuário Olá não foi ativo por um tempo.</span><span class="sxs-lookup"><span data-stu-id="99aa3-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="99aa3-438">**Usuário**: informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="99aa3-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="99aa3-439">limites</span><span class="sxs-lookup"><span data-stu-id="99aa3-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="99aa3-440">tooavoid atingir o limite de taxa de dados hello, use [amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="99aa3-441">toodetermine como dados long são mantidos, consulte [privacidade e retenção de dados](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="99aa3-442">Documentos de Referência</span><span class="sxs-lookup"><span data-stu-id="99aa3-442">Reference docs</span></span>
* [<span data-ttu-id="99aa3-443">Referência do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99aa3-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="99aa3-444">Referência do Java</span><span class="sxs-lookup"><span data-stu-id="99aa3-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="99aa3-445">Referência do JavaScript</span><span class="sxs-lookup"><span data-stu-id="99aa3-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="99aa3-446">SDK do Android</span><span class="sxs-lookup"><span data-stu-id="99aa3-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="99aa3-447">SDK do iOS</span><span class="sxs-lookup"><span data-stu-id="99aa3-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="99aa3-448">Código do SDK</span><span class="sxs-lookup"><span data-stu-id="99aa3-448">SDK code</span></span>
* [<span data-ttu-id="99aa3-449">SDK de Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99aa3-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="99aa3-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="99aa3-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="99aa3-451">Pacotes do Windows Server</span><span class="sxs-lookup"><span data-stu-id="99aa3-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="99aa3-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="99aa3-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="99aa3-453">SDK do JavaScript</span><span class="sxs-lookup"><span data-stu-id="99aa3-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="99aa3-454">Todas as plataformas</span><span class="sxs-lookup"><span data-stu-id="99aa3-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="99aa3-455">Perguntas</span><span class="sxs-lookup"><span data-stu-id="99aa3-455">Questions</span></span>
* <span data-ttu-id="99aa3-456">*Que exceções podem ser lançadas por chamadas Track_()?*</span><span class="sxs-lookup"><span data-stu-id="99aa3-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="99aa3-457">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="99aa3-457">None.</span></span> <span data-ttu-id="99aa3-458">Você não precisa toowrap-los em cláusulas de try-catch.</span><span class="sxs-lookup"><span data-stu-id="99aa3-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="99aa3-459">Se Olá SDK encontrar problemas, ele registrará em log mensagens na saída de console de depuração de saudação e --se hello mensagens conseguir – em busca de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="99aa3-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="99aa3-460">*Há dados de tooget uma API REST do portal Olá?*</span><span class="sxs-lookup"><span data-stu-id="99aa3-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="99aa3-461">Sim, Olá [API de acesso a dados](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="99aa3-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="99aa3-462">Incluem outros dados de maneiras tooextract [exportar de análise tooPower BI](app-insights-export-power-bi.md) e [a exportação contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="99aa3-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="99aa3-463"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99aa3-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="99aa3-464">Pesquisar eventos e logs</span><span class="sxs-lookup"><span data-stu-id="99aa3-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="99aa3-465">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="99aa3-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


