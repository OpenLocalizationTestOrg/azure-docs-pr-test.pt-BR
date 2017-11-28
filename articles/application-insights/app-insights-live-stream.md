---
title: "aaaLive fluxo de métricas com métricas personalizadas e diagnósticos no Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="0499f-103">Live Metrics Stream: monitorar e diagnosticar com latência de um segundo</span><span class="sxs-lookup"><span data-stu-id="0499f-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="0499f-104">Teste o coração de pulsação de saudação do seu aplicativo web em tempo real, em produção usando o fluxo ao vivo de métricas de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0499f-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="0499f-105">Selecionar e filtrar toowatch de contadores de desempenho e métricas em tempo real, sem qualquer serviço de tooyour interferência no.</span><span class="sxs-lookup"><span data-stu-id="0499f-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="0499f-106">Inspecione os rastreamentos de pilha de exceções e solicitações de amostra com falha.</span><span class="sxs-lookup"><span data-stu-id="0499f-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="0499f-107">Juntamente com [Criador de perfil](app-insights-profiler.md), [Depurador de instantâneo](app-insights-snapshot-debugger.md) e [testes de desempenho](app-insights-monitor-web-app-availability.md#performance-tests), o Live Metrics Stream fornece uma ferramenta de diagnóstico poderosa e não invasiva para seu site ao vivo.</span><span class="sxs-lookup"><span data-stu-id="0499f-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="0499f-108">Com o Live Metrics Stream, você pode:</span><span class="sxs-lookup"><span data-stu-id="0499f-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="0499f-109">Valide uma correção enquanto ela é liberado, observando as contagens de falha e desempenho.</span><span class="sxs-lookup"><span data-stu-id="0499f-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="0499f-110">Assista o efeito de saudação de cargas de teste e diagnosticar problemas em tempo real.</span><span class="sxs-lookup"><span data-stu-id="0499f-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="0499f-111">Se concentrar em sessões de teste específica ou filtrar problemas conhecidos, selecionando e métricas Olá deseja toowatch de filtragem.</span><span class="sxs-lookup"><span data-stu-id="0499f-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="0499f-112">Obter rastreamentos de exceção quando eles ocorrerem.</span><span class="sxs-lookup"><span data-stu-id="0499f-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="0499f-113">Experiência com filtros toofind Olá KPIs mais relevantes.</span><span class="sxs-lookup"><span data-stu-id="0499f-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="0499f-114">Monitore qualquer contador de desempenho do Windows em tempo real.</span><span class="sxs-lookup"><span data-stu-id="0499f-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="0499f-115">Facilmente identificar um servidor que está tendo problemas e filtrar todos os Olá KPI/live feed toojust nesse servidor.</span><span class="sxs-lookup"><span data-stu-id="0499f-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="0499f-116">[![Vídeo do Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="0499f-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="0499f-117">Transmissão ao vivo de métricas está disponível em aplicativos ASP.NET executados localmente ou na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0499f-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="0499f-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="0499f-118">Get started</span></span>

1. <span data-ttu-id="0499f-119">Se você ainda não [instalou o Application Insights](app-insights-asp-net.md) no aplicativo Web ASP.NET ou [aplicativo do Windows Server](app-insights-windows-services.md), faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="0499f-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="0499f-120">**Versão mais recente da atualização toohello** do pacote do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="0499f-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="0499f-121">No Visual Studio, clique com o botão direito do mouse em seu projeto e escolha **Gerenciar pacotes Nuget**.</span><span class="sxs-lookup"><span data-stu-id="0499f-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="0499f-122">Olá abrir **atualizações** guia seleção **incluir pré-lançamento**e selecionar todos os pacotes de Microsoft.ApplicationInsights.* hello.</span><span class="sxs-lookup"><span data-stu-id="0499f-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="0499f-123">Reimplante o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0499f-123">Redeploy your app.</span></span>

3. <span data-ttu-id="0499f-124">Em Olá [portal do Azure](https://portal.azure.com), abra o recurso do Application Insights Olá para seu aplicativo e, em seguida, abrir o fluxo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="0499f-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="0499f-125">[Canal de controle seguro Olá](#secure-the-control-channel) se você pode usar dados confidenciais, como nomes de clientes em seus filtros.</span><span class="sxs-lookup"><span data-stu-id="0499f-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Na folha de visão geral de saudação, clique em fluxo ao vivo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="0499f-127">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="0499f-127">No data?</span></span> <span data-ttu-id="0499f-128">Verificar o firewall de servidor</span><span class="sxs-lookup"><span data-stu-id="0499f-128">Check your server firewall</span></span>

<span data-ttu-id="0499f-129">Verificar Olá [portas de saída para transmissão ao vivo de métricas](app-insights-ip-addresses.md#outgoing-ports) estão abertas no firewall Olá dos seus servidores.</span><span class="sxs-lookup"><span data-stu-id="0499f-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="0499f-130">Como o Live Metrics Stream difere do Metrics Explorer e Analytics?</span><span class="sxs-lookup"><span data-stu-id="0499f-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="0499f-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="0499f-131">Live Stream</span></span> | <span data-ttu-id="0499f-132">Metrics Explorer e Analytics</span><span class="sxs-lookup"><span data-stu-id="0499f-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="0499f-133">Latência</span><span class="sxs-lookup"><span data-stu-id="0499f-133">Latency</span></span>|<span data-ttu-id="0499f-134">Dados exibidos em um segundo</span><span class="sxs-lookup"><span data-stu-id="0499f-134">Data displayed within one second</span></span>|<span data-ttu-id="0499f-135">Agregado ao longo de minutos</span><span class="sxs-lookup"><span data-stu-id="0499f-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="0499f-136">Nenhuma retenção</span><span class="sxs-lookup"><span data-stu-id="0499f-136">No retention</span></span>|<span data-ttu-id="0499f-137">Persiste os dados enquanto ele está em um gráfico de saudação e é descartado</span><span class="sxs-lookup"><span data-stu-id="0499f-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="0499f-138">Dados retidos por 90 dias</span><span class="sxs-lookup"><span data-stu-id="0499f-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="0499f-139">Sob demanda</span><span class="sxs-lookup"><span data-stu-id="0499f-139">On demand</span></span>|<span data-ttu-id="0499f-140">Os dados são transmitidos enquanto você abre o Live Metrics</span><span class="sxs-lookup"><span data-stu-id="0499f-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="0499f-141">Os dados são enviados sempre que Olá SDK está instalado e habilitado</span><span class="sxs-lookup"><span data-stu-id="0499f-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="0499f-142">Grátis</span><span class="sxs-lookup"><span data-stu-id="0499f-142">Free</span></span>|<span data-ttu-id="0499f-143">Não há nenhum custo para dados do Live Stream</span><span class="sxs-lookup"><span data-stu-id="0499f-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="0499f-144">Entidade muito[preços](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="0499f-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="0499f-145">amostragem</span><span class="sxs-lookup"><span data-stu-id="0499f-145">Sampling</span></span>|<span data-ttu-id="0499f-146">Todas as métricas e os contadores selecionados são transmitidos.</span><span class="sxs-lookup"><span data-stu-id="0499f-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="0499f-147">Há amostras de falhas e rastreamentos de pilha.</span><span class="sxs-lookup"><span data-stu-id="0499f-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="0499f-148">TelemetryProcessors não são aplicados.</span><span class="sxs-lookup"><span data-stu-id="0499f-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="0499f-149">Os eventos podem ter [amostras](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="0499f-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="0499f-150">Canal de controle</span><span class="sxs-lookup"><span data-stu-id="0499f-150">Control channel</span></span>|<span data-ttu-id="0499f-151">Sinais de controle de filtro são enviados toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="0499f-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="0499f-152">Recomendamos que você [proteja este canal](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="0499f-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="0499f-153">A comunicação é unidirecional toohello portal</span><span class="sxs-lookup"><span data-stu-id="0499f-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="0499f-154">Selecionar e filtrar suas métricas</span><span class="sxs-lookup"><span data-stu-id="0499f-154">Select and filter your metrics</span></span>

<span data-ttu-id="0499f-155">(Disponível em clássico aplicativos ASP.NET com hello SDK mais recente.)</span><span class="sxs-lookup"><span data-stu-id="0499f-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="0499f-156">Você pode monitorar o KPI personalizado ao vivo aplicando filtros arbitrários em qualquer telemetria do Application Insights do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0499f-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="0499f-157">Clique em controle de filtro de saudação que mostra quando você passar o mouse qualquer um dos gráficos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0499f-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="0499f-158">Olá gráfico a seguir é uma contagem de solicitação personalizada KPI com filtros em atributos de URL e a duração de plotagem.</span><span class="sxs-lookup"><span data-stu-id="0499f-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="0499f-159">Valide os filtros com hello seção de visualização de fluxo que mostra um feed de telemetria que corresponde aos critérios de saudação especificado em qualquer ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="0499f-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![KPI de solicitação personalizado](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="0499f-161">Você pode monitorar um valor diferente da Contagem.</span><span class="sxs-lookup"><span data-stu-id="0499f-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="0499f-162">Opções de saudação dependem de tipo de saudação do fluxo, o que pode ser qualquer telemetria do Application Insights: solicitações, dependências, exceções, rastreamentos, eventos ou métricas.</span><span class="sxs-lookup"><span data-stu-id="0499f-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="0499f-163">Ela pode ser sua própria [medida personalizada](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="0499f-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Opções de valor](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="0499f-165">Além disso tooApplication telemetria Insights, você também pode monitorar qualquer contador de desempenho do Windows que a seleção de opções de fluxo de saudação e fornecendo o nome Olá Olá do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0499f-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="0499f-166">Métricas em tempo real são agregadas em dois pontos: localmente em cada servidor e, em seguida, em todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="0499f-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="0499f-167">Você pode alterar o padrão, Olá selecionando outras opções no hello respectivos suspensos.</span><span class="sxs-lookup"><span data-stu-id="0499f-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="0499f-168">Telemetria de exemplo: eventos de diagnóstico em tempo real personalizados</span><span class="sxs-lookup"><span data-stu-id="0499f-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="0499f-169">Por padrão, o feed Olá de eventos mostra exemplos de solicitações com falha e chamadas de dependência, exceções, eventos e rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="0499f-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="0499f-170">Clique em critérios Olá filtro ícone toosee Olá aplicada em qualquer ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="0499f-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Feed em tempo real padrão](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="0499f-172">Como com métricas, você pode especificar qualquer tooany critérios arbitrário de tipos de telemetria do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="0499f-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="0499f-173">Neste exemplo, estamos selecionando falhas, rastreamentos e eventos de solicitação específicos.</span><span class="sxs-lookup"><span data-stu-id="0499f-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="0499f-174">Também estamos selecionando todas as exceções e falhas de dependência.</span><span class="sxs-lookup"><span data-stu-id="0499f-174">We are also selecting all exceptions and dependency failures.</span></span>

![Feed em tempo real personalizado](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="0499f-176">Observação: No momento, para critérios baseada em mensagem de exceção use mensagem de exceção mais externo hello.</span><span class="sxs-lookup"><span data-stu-id="0499f-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="0499f-177">Em Olá anterior como exemplo, toofilter out a exceção benignas Olá com a mensagem de exceção interna (segue hello "< –" delimitador) "cliente de saudação desconectado."</span><span class="sxs-lookup"><span data-stu-id="0499f-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="0499f-178">use um critério de que a mensagem não contém "Erro ao ler o conteúdo da solicitação".</span><span class="sxs-lookup"><span data-stu-id="0499f-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="0499f-179">Consulte os detalhes de saudação de um item no hello live feed clicando nele.</span><span class="sxs-lookup"><span data-stu-id="0499f-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="0499f-180">Você pode pausar Olá feed clicando **pausar** simplesmente rolando para baixo ou clicar em um item.</span><span class="sxs-lookup"><span data-stu-id="0499f-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="0499f-181">Feed dinâmica será retomado quando você rola toohello back superior, ou clicando o contador de saudação de itens coletados enquanto ele estava em pausa.</span><span class="sxs-lookup"><span data-stu-id="0499f-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Amostra de falhas em tempo real](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="0499f-183">Filtrar por instância do servidor</span><span class="sxs-lookup"><span data-stu-id="0499f-183">Filter by server instance</span></span>

<span data-ttu-id="0499f-184">Se você quiser toomonitor uma instância de função de servidor específico, você pode filtrar por servidor.</span><span class="sxs-lookup"><span data-stu-id="0499f-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Amostra de falhas em tempo real](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="0499f-186">Requisitos do SDK</span><span class="sxs-lookup"><span data-stu-id="0499f-186">SDK Requirements</span></span>
<span data-ttu-id="0499f-187">O Fluxo de métricas em tempo real personalizado está disponível com a versão 2.4.0-beta2 ou mais recente do [SDK do Application Insights para Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="0499f-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="0499f-188">Lembre-se a opção de "Incluir pré-lançamento" tooselect do Gerenciador de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0499f-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="0499f-189">Proteger o canal de controle de saudação</span><span class="sxs-lookup"><span data-stu-id="0499f-189">Secure hello control channel</span></span>
<span data-ttu-id="0499f-190">critérios de filtros personalizados Olá especificados são enviados toohello back componente de métricas em tempo real em Olá SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0499f-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="0499f-191">filtros de saudação possam conter informações confidenciais, como customerIDs.</span><span class="sxs-lookup"><span data-stu-id="0499f-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="0499f-192">Você pode fazer com que o canal de saudação seguro com uma chave de segredo de API além toohello chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="0499f-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="0499f-193">Criar uma chave de API</span><span class="sxs-lookup"><span data-stu-id="0499f-193">Create an API Key</span></span>

![Criar chave de API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="0499f-195">Adicionar tooConfiguration de chave de API</span><span class="sxs-lookup"><span data-stu-id="0499f-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="0499f-196">No arquivo applicationinsights. config de hello, adicione Olá AuthenticationApiKey toohello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="0499f-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="0499f-197">Ou, no código, defina-Olá QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="0499f-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="0499f-198">No entanto, se você reconhece e confia em que todos os Olá servidores conectados, você pode tentar filtros personalizados de saudação sem canal Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="0499f-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="0499f-199">Essa opção está disponível por seis meses.</span><span class="sxs-lookup"><span data-stu-id="0499f-199">This option is available for six months.</span></span> <span data-ttu-id="0499f-200">Essa substituição é necessária uma vez a cada nova sessão ou quando um novo servidor ficar online.</span><span class="sxs-lookup"><span data-stu-id="0499f-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opções de autenticação das métricas em tempo real](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="0499f-202">É altamente recomendável que você configure o canal Olá autenticado antes de inserir informações potencialmente confidenciais como CustomerID Olá critérios de filtro.</span><span class="sxs-lookup"><span data-stu-id="0499f-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="0499f-203">Geração de uma carga de teste de desempenho</span><span class="sxs-lookup"><span data-stu-id="0499f-203">Generating a performance test load</span></span>

<span data-ttu-id="0499f-204">Se você quiser toowatch efeito de saudação carga aumentar, folha de teste de desempenho do uso hello.</span><span class="sxs-lookup"><span data-stu-id="0499f-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="0499f-205">Ele simula solicitações de vários usuários simultâneos.</span><span class="sxs-lookup"><span data-stu-id="0499f-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="0499f-206">Ele pode ser executado ou "testes manuais" (ping testes) de uma única URL, ou pode executar um [teste de desempenho web de várias etapas](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que você carregue (em Olá mesma forma como uma disponibilidade de teste).</span><span class="sxs-lookup"><span data-stu-id="0499f-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="0499f-207">Depois de criar o teste de desempenho Olá, abra o teste hello e Olá folha de transmissão ao vivo em janelas separadas.</span><span class="sxs-lookup"><span data-stu-id="0499f-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="0499f-208">Você pode ver quando Olá enfileiradas inicia de teste de desempenho e a transmissão ao vivo inspecionar a saudação simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0499f-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="0499f-209">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="0499f-209">Troubleshooting</span></span>

<span data-ttu-id="0499f-210">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="0499f-210">No data?</span></span> <span data-ttu-id="0499f-211">Se seu aplicativo estiver em uma rede protegida: o Fluxo de métricas em tempo real usará endereços IP diferentes de outras Application Insights Telemetries.</span><span class="sxs-lookup"><span data-stu-id="0499f-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="0499f-212">Certifique-se de que [esses endereços IP](app-insights-ip-addresses.md) estejam abertos em seu firewall.</span><span class="sxs-lookup"><span data-stu-id="0499f-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0499f-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0499f-213">Next steps</span></span>
* [<span data-ttu-id="0499f-214">Monitorando o uso com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0499f-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="0499f-215">Usando a Pesquisa de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0499f-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="0499f-216">Criador de perfil</span><span class="sxs-lookup"><span data-stu-id="0499f-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="0499f-217">Depurador instantâneo</span><span class="sxs-lookup"><span data-stu-id="0499f-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
