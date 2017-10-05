---
title: "Live Metrics Stream com métricas personalizadas e diagnósticos no Azure Application Insights | Microsoft Docs"
description: "Monitore seu aplicativo Web em tempo real usando métrica personalizada e diagnostique problemas com um feed em tempo real de falhas, rastreamentos e eventos."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="c1595-103">Live Metrics Stream: monitorar e diagnosticar com latência de um segundo</span><span class="sxs-lookup"><span data-stu-id="c1595-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="c1595-104">Teste a pulsação do aplicativo Web ao vivo em produção usando o Live Metrics Stream do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1595-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="c1595-105">Selecione e filtre os contadores de desempenho e as métricas para observar em tempo real, sem qualquer perturbação para o serviço.</span><span class="sxs-lookup"><span data-stu-id="c1595-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="c1595-106">Inspecione os rastreamentos de pilha de exceções e solicitações de amostra com falha.</span><span class="sxs-lookup"><span data-stu-id="c1595-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="c1595-107">Juntamente com [Criador de perfil](app-insights-profiler.md), [Depurador de instantâneo](app-insights-snapshot-debugger.md) e [testes de desempenho](app-insights-monitor-web-app-availability.md#performance-tests), o Live Metrics Stream fornece uma ferramenta de diagnóstico poderosa e não invasiva para seu site ao vivo.</span><span class="sxs-lookup"><span data-stu-id="c1595-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="c1595-108">Com o Live Metrics Stream, você pode:</span><span class="sxs-lookup"><span data-stu-id="c1595-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="c1595-109">Valide uma correção enquanto ela é liberado, observando as contagens de falha e desempenho.</span><span class="sxs-lookup"><span data-stu-id="c1595-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="c1595-110">Observe o efeito de cargas de teste e diagnostique problemas em tempo real.</span><span class="sxs-lookup"><span data-stu-id="c1595-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="c1595-111">Concentre-se em sessões de teste específicas ou filtre os problemas conhecidos, selecionando e filtrando as métricas que você deseja inspecionar.</span><span class="sxs-lookup"><span data-stu-id="c1595-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="c1595-112">Obter rastreamentos de exceção quando eles ocorrerem.</span><span class="sxs-lookup"><span data-stu-id="c1595-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="c1595-113">Experimente os filtros para localizar os KPIs mais relevantes.</span><span class="sxs-lookup"><span data-stu-id="c1595-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="c1595-114">Monitore qualquer contador de desempenho do Windows em tempo real.</span><span class="sxs-lookup"><span data-stu-id="c1595-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="c1595-115">Identifique com facilidade um servidor que está apresentando problemas e filtre todo o KPI/feed em tempo real para apenas aquele servidor.</span><span class="sxs-lookup"><span data-stu-id="c1595-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="c1595-116">[![Vídeo do Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="c1595-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="c1595-117">O Live Metrics Stream está disponível em aplicativos ASP.NET executados localmente ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c1595-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="c1595-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="c1595-118">Get started</span></span>

1. <span data-ttu-id="c1595-119">Se você ainda não [instalou o Application Insights](app-insights-asp-net.md) no aplicativo Web ASP.NET ou [aplicativo do Windows Server](app-insights-windows-services.md), faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="c1595-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="c1595-120">**Atualização para a última versão** do pacote do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c1595-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="c1595-121">No Visual Studio, clique com o botão direito do mouse em seu projeto e escolha **Gerenciar pacotes Nuget**.</span><span class="sxs-lookup"><span data-stu-id="c1595-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="c1595-122">Abra a guia **Atualizações**, marque **Incluir pré-lançamento** e selecione todos os pacotes Microsoft.ApplicationInsights.*.</span><span class="sxs-lookup"><span data-stu-id="c1595-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="c1595-123">Reimplante o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c1595-123">Redeploy your app.</span></span>

3. <span data-ttu-id="c1595-124">No [Portal do Azure](https://portal.azure.com), abra o recurso Application Insights para o aplicativo e abra o Live Stream.</span><span class="sxs-lookup"><span data-stu-id="c1595-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="c1595-125">[Proteja o canal de controle](#secure-the-control-channel) se você puder usar dados confidenciais, como nomes de clientes, em seus filtros.</span><span class="sxs-lookup"><span data-stu-id="c1595-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Na folha Visão Geral, clique em Live Stream](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="c1595-127">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="c1595-127">No data?</span></span> <span data-ttu-id="c1595-128">Verificar o firewall de servidor</span><span class="sxs-lookup"><span data-stu-id="c1595-128">Check your server firewall</span></span>

<span data-ttu-id="c1595-129">Verifique se as [portas de saída para o Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) estão abertas no firewall dos servidores.</span><span class="sxs-lookup"><span data-stu-id="c1595-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="c1595-130">Como o Live Metrics Stream difere do Metrics Explorer e Analytics?</span><span class="sxs-lookup"><span data-stu-id="c1595-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="c1595-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="c1595-131">Live Stream</span></span> | <span data-ttu-id="c1595-132">Metrics Explorer e Analytics</span><span class="sxs-lookup"><span data-stu-id="c1595-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="c1595-133">Latência</span><span class="sxs-lookup"><span data-stu-id="c1595-133">Latency</span></span>|<span data-ttu-id="c1595-134">Dados exibidos em um segundo</span><span class="sxs-lookup"><span data-stu-id="c1595-134">Data displayed within one second</span></span>|<span data-ttu-id="c1595-135">Agregado ao longo de minutos</span><span class="sxs-lookup"><span data-stu-id="c1595-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="c1595-136">Nenhuma retenção</span><span class="sxs-lookup"><span data-stu-id="c1595-136">No retention</span></span>|<span data-ttu-id="c1595-137">Os dados persistem enquanto estão no gráfico e depois são descartados</span><span class="sxs-lookup"><span data-stu-id="c1595-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="c1595-138">Dados retidos por 90 dias</span><span class="sxs-lookup"><span data-stu-id="c1595-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="c1595-139">Sob demanda</span><span class="sxs-lookup"><span data-stu-id="c1595-139">On demand</span></span>|<span data-ttu-id="c1595-140">Os dados são transmitidos enquanto você abre o Live Metrics</span><span class="sxs-lookup"><span data-stu-id="c1595-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="c1595-141">Os dados são enviados sempre que o SDK está instalado e habilitado</span><span class="sxs-lookup"><span data-stu-id="c1595-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="c1595-142">Grátis</span><span class="sxs-lookup"><span data-stu-id="c1595-142">Free</span></span>|<span data-ttu-id="c1595-143">Não há nenhum custo para dados do Live Stream</span><span class="sxs-lookup"><span data-stu-id="c1595-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="c1595-144">Sujeito a [preços](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="c1595-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="c1595-145">Amostragem</span><span class="sxs-lookup"><span data-stu-id="c1595-145">Sampling</span></span>|<span data-ttu-id="c1595-146">Todas as métricas e os contadores selecionados são transmitidos.</span><span class="sxs-lookup"><span data-stu-id="c1595-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="c1595-147">Há amostras de falhas e rastreamentos de pilha.</span><span class="sxs-lookup"><span data-stu-id="c1595-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="c1595-148">TelemetryProcessors não são aplicados.</span><span class="sxs-lookup"><span data-stu-id="c1595-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="c1595-149">Os eventos podem ter [amostras](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="c1595-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="c1595-150">Canal de controle</span><span class="sxs-lookup"><span data-stu-id="c1595-150">Control channel</span></span>|<span data-ttu-id="c1595-151">Os sinais de controle de filtro são enviados ao SDK.</span><span class="sxs-lookup"><span data-stu-id="c1595-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="c1595-152">Recomendamos que você [proteja este canal](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="c1595-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="c1595-153">A comunicação é unidirecional para o portal</span><span class="sxs-lookup"><span data-stu-id="c1595-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="c1595-154">Selecionar e filtrar suas métricas</span><span class="sxs-lookup"><span data-stu-id="c1595-154">Select and filter your metrics</span></span>

<span data-ttu-id="c1595-155">(Disponível em aplicativos ASP.NET clássicos com o SDK mais recente).</span><span class="sxs-lookup"><span data-stu-id="c1595-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="c1595-156">Você pode monitorar o KPI personalizado em tempo real aplicando filtros arbitrários a qualquer Application Insights Telemetry no portal.</span><span class="sxs-lookup"><span data-stu-id="c1595-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="c1595-157">Clique no controle de filtro que é exibido quando você passa o mouse sobre qualquer um dos gráficos.</span><span class="sxs-lookup"><span data-stu-id="c1595-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="c1595-158">O gráfico a seguir plota um KPI personalizado de contagem de solicitações com filtros nos atributos de URL e a duração.</span><span class="sxs-lookup"><span data-stu-id="c1595-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="c1595-159">Valide seus filtros com a seção Versão Prévia do Fluxo, que mostra um feed em tempo real da telemetria que corresponde aos critérios que você especificou em qualquer ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="c1595-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![KPI de solicitação personalizado](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="c1595-161">Você pode monitorar um valor diferente da Contagem.</span><span class="sxs-lookup"><span data-stu-id="c1595-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="c1595-162">As opções dependem do tipo de fluxo, que poderia ser qualquer Application Insights Telemetry: solicitações, dependências, exceções, rastreamentos, eventos ou métricas.</span><span class="sxs-lookup"><span data-stu-id="c1595-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="c1595-163">Ela pode ser sua própria [medida personalizada](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="c1595-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Opções de valor](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="c1595-165">Além da Application Insights Telemetry, você também pode monitorar qualquer contador de desempenho do Windows selecionando entre as opções de fluxo e fornecendo o nome do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="c1595-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="c1595-166">Métricas em tempo real são agregadas em dois pontos: localmente em cada servidor e, em seguida, em todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="c1595-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="c1595-167">Você pode alterar o padrão de ambos selecionando outras opções nos respectivos menus suspensos.</span><span class="sxs-lookup"><span data-stu-id="c1595-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="c1595-168">Telemetria de exemplo: eventos de diagnóstico em tempo real personalizados</span><span class="sxs-lookup"><span data-stu-id="c1595-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="c1595-169">Por padrão, o feed de eventos em tempo real mostra exemplos de solicitações com falha e chamadas de dependência, exceções, eventos e rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="c1595-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="c1595-170">Clique no ícone do filtro para ver os critérios aplicados em qualquer ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="c1595-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![Feed em tempo real padrão](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="c1595-172">Assim como acontece com as métricas, você pode especificar qualquer critério arbitrário para qualquer um dos tipos de Application Insights Telemetry.</span><span class="sxs-lookup"><span data-stu-id="c1595-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="c1595-173">Neste exemplo, estamos selecionando falhas, rastreamentos e eventos de solicitação específicos.</span><span class="sxs-lookup"><span data-stu-id="c1595-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="c1595-174">Também estamos selecionando todas as exceções e falhas de dependência.</span><span class="sxs-lookup"><span data-stu-id="c1595-174">We are also selecting all exceptions and dependency failures.</span></span>

![Feed em tempo real personalizado](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="c1595-176">Observação: no momento, para critérios baseados em mensagens de exceção, use a mensagem de exceção mais externa.</span><span class="sxs-lookup"><span data-stu-id="c1595-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="c1595-177">No exemplo anterior, para filtrar a exceção benigna com a mensagem de exceção interna (segue o delimitador "< –") "O cliente se desconectou.",</span><span class="sxs-lookup"><span data-stu-id="c1595-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="c1595-178">use um critério de que a mensagem não contém "Erro ao ler o conteúdo da solicitação".</span><span class="sxs-lookup"><span data-stu-id="c1595-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="c1595-179">Consulte os detalhes de um item no feed em tempo real clicando nele.</span><span class="sxs-lookup"><span data-stu-id="c1595-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="c1595-180">Você pode pausar o feed clicando em **Pausar** ou simplesmente rolando para baixo ou clicando em um item.</span><span class="sxs-lookup"><span data-stu-id="c1595-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="c1595-181">O feed em tempo real será retomado quando você rolar de volta para o início ou clicando no contador de itens coletados enquanto ele estava em pausa.</span><span class="sxs-lookup"><span data-stu-id="c1595-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![Amostra de falhas em tempo real](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="c1595-183">Filtrar por instância do servidor</span><span class="sxs-lookup"><span data-stu-id="c1595-183">Filter by server instance</span></span>

<span data-ttu-id="c1595-184">Se você quiser monitorar uma instância de função de servidor específico, filtre por servidor.</span><span class="sxs-lookup"><span data-stu-id="c1595-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Amostra de falhas em tempo real](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="c1595-186">Requisitos do SDK</span><span class="sxs-lookup"><span data-stu-id="c1595-186">SDK Requirements</span></span>
<span data-ttu-id="c1595-187">O Fluxo de métricas em tempo real personalizado está disponível com a versão 2.4.0-beta2 ou mais recente do [SDK do Application Insights para Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="c1595-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="c1595-188">Lembre-se de selecionar a opção "Incluir pré-lançamento" no gerenciador de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1595-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="c1595-189">Proteger o canal de controle</span><span class="sxs-lookup"><span data-stu-id="c1595-189">Secure the control channel</span></span>
<span data-ttu-id="c1595-190">Os critérios de filtro personalizados especificados são enviados para o componente de Métricas em tempo real no SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c1595-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="c1595-191">Os filtros podem conter informações confidenciais, como customerIDs.</span><span class="sxs-lookup"><span data-stu-id="c1595-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="c1595-192">Você pode proteger o canal com uma chave de API secreta além da chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="c1595-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="c1595-193">Criar uma chave de API</span><span class="sxs-lookup"><span data-stu-id="c1595-193">Create an API Key</span></span>

![Criar chave de API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="c1595-195">Adicionar chave de API à configuração</span><span class="sxs-lookup"><span data-stu-id="c1595-195">Add API key to Configuration</span></span>
<span data-ttu-id="c1595-196">No arquivo applicationinsights.config, adicione AuthenticationApiKey a QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="c1595-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="c1595-197">Ou, no código, defina-a no QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="c1595-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="c1595-198">No entanto, caso reconheça e confie em todos os servidores conectados, você pode testar os filtros personalizados sem o canal autenticado.</span><span class="sxs-lookup"><span data-stu-id="c1595-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="c1595-199">Essa opção está disponível por seis meses.</span><span class="sxs-lookup"><span data-stu-id="c1595-199">This option is available for six months.</span></span> <span data-ttu-id="c1595-200">Essa substituição é necessária uma vez a cada nova sessão ou quando um novo servidor ficar online.</span><span class="sxs-lookup"><span data-stu-id="c1595-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opções de autenticação das métricas em tempo real](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="c1595-202">É altamente recomendável que você configure o canal autenticado antes de inserir informações potencialmente confidenciais, como CustomerIDs, nos critérios de filtro.</span><span class="sxs-lookup"><span data-stu-id="c1595-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="c1595-203">Geração de uma carga de teste de desempenho</span><span class="sxs-lookup"><span data-stu-id="c1595-203">Generating a performance test load</span></span>

<span data-ttu-id="c1595-204">Se você quiser observar o efeito de um aumento de carga, use a folha de Teste de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="c1595-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="c1595-205">Ele simula solicitações de vários usuários simultâneos.</span><span class="sxs-lookup"><span data-stu-id="c1595-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="c1595-206">Ele pode executar "testes manuais" (testes de ping) de uma única URL ou pode executar um [teste de desempenho da Web de várias etapas](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que você carrega (da mesma forma como um teste de disponibilidade).</span><span class="sxs-lookup"><span data-stu-id="c1595-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="c1595-207">Depois de criar o teste de desempenho, abra o teste e a folha do Live Stream em janelas separadas.</span><span class="sxs-lookup"><span data-stu-id="c1595-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="c1595-208">Você pode ver quando o teste de desempenho na fila é iniciado e assistir à transmissão ao vivo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="c1595-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="c1595-209">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="c1595-209">Troubleshooting</span></span>

<span data-ttu-id="c1595-210">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="c1595-210">No data?</span></span> <span data-ttu-id="c1595-211">Se seu aplicativo estiver em uma rede protegida: o Fluxo de métricas em tempo real usará endereços IP diferentes de outras Application Insights Telemetries.</span><span class="sxs-lookup"><span data-stu-id="c1595-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="c1595-212">Certifique-se de que [esses endereços IP](app-insights-ip-addresses.md) estejam abertos em seu firewall.</span><span class="sxs-lookup"><span data-stu-id="c1595-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c1595-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1595-213">Next steps</span></span>
* [<span data-ttu-id="c1595-214">Monitorando o uso com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="c1595-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="c1595-215">Usando a Pesquisa de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c1595-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="c1595-216">Criador de perfil</span><span class="sxs-lookup"><span data-stu-id="c1595-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="c1595-217">Depurador instantâneo</span><span class="sxs-lookup"><span data-stu-id="c1595-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
