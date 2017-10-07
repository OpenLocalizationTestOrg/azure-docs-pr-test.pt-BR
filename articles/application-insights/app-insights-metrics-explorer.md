---
title: "aaaExploring métricas no Azure Application Insights | Microsoft Docs"
description: "Como toointerpret gráficos no explorer métrica e folhas de métrica explorer toocustomize."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="61f90-103">Explorar métricas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="61f90-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="61f90-104">Métricas no [Application Insights][start] são contagens e valores medidos de eventos enviados em telemetria do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61f90-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="61f90-105">Eles ajudam você a detectar problemas de desempenho e observar as tendências referentes a como seu aplicativo está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="61f90-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="61f90-106">Há uma grande variedade de métricas padrão, e você também pode criar suas próprias métricas e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="61f90-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="61f90-107">Contagens de métricas e eventos são exibidas em gráficos de valores agregados como somas, médias ou contagens.</span><span class="sxs-lookup"><span data-stu-id="61f90-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="61f90-108">Aqui está um exemplo de conjunto de gráficos:</span><span class="sxs-lookup"><span data-stu-id="61f90-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="61f90-109">Você pode encontrar gráficos de métricas em qualquer lugar no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="61f90-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="61f90-110">Na maioria dos casos, eles podem ser personalizados, e você pode adicionar mais folha toohello de gráficos.</span><span class="sxs-lookup"><span data-stu-id="61f90-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="61f90-111">Na folha de visão geral de saudação, clique nas toomore detalhadas gráficos (que têm cargos como "Servidores"), ou clique em **Metrics Explorer** tooopen uma nova folha de onde você pode criar gráficos personalizados.</span><span class="sxs-lookup"><span data-stu-id="61f90-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="61f90-112">Intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="61f90-112">Time range</span></span>
<span data-ttu-id="61f90-113">Você pode alterar Olá intervalo de tempo coberto por gráficos hello ou grades em qualquer folha.</span><span class="sxs-lookup"><span data-stu-id="61f90-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Folha de visão geral de saudação aberto de seu aplicativo no portal do Azure de saudação](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="61f90-115">Se você estiver esperando dados que não apareceram ainda, clique em Atualizar.</span><span class="sxs-lookup"><span data-stu-id="61f90-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="61f90-116">Gráficos de atualizar a mesmos em intervalos, mas intervalos de saudação são mais tempo para intervalos de tempo maior.</span><span class="sxs-lookup"><span data-stu-id="61f90-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="61f90-117">Pode levar algum tempo para dados toocome por meio do pipeline de análise de saudação em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="61f90-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="61f90-118">toozoom em parte de um gráfico, arraste sobre ele:</span><span class="sxs-lookup"><span data-stu-id="61f90-118">toozoom into part of a chart, drag over it:</span></span>

![Arraste por parte de um gráfico.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="61f90-120">Clique em Olá Desfazer Zoom botão toorestore-lo.</span><span class="sxs-lookup"><span data-stu-id="61f90-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="61f90-121">Valores de granularidade e ponto</span><span class="sxs-lookup"><span data-stu-id="61f90-121">Granularity and point values</span></span>
<span data-ttu-id="61f90-122">Passe o mouse sobre Olá gráfico toodisplay Olá valores hello métricas nesse ponto.</span><span class="sxs-lookup"><span data-stu-id="61f90-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Passe o mouse sobre um gráfico Olá](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="61f90-124">valor de saudação da métrica de saudação em um ponto específico é agregado no decorrer de saudação precede o intervalo de amostragem.</span><span class="sxs-lookup"><span data-stu-id="61f90-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="61f90-125">intervalo de amostragem de saudação ou "granularidade" é mostrada na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![cabeçalho de saudação de uma folha.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="61f90-127">Você pode ajustar a granularidade de saudação na folha de intervalo de tempo de saudação:</span><span class="sxs-lookup"><span data-stu-id="61f90-127">You can adjust hello granularity in hello Time range blade:</span></span>

![cabeçalho de saudação de uma folha.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="61f90-129">granularidades de saudação disponíveis dependem do intervalo de tempo de saudação que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="61f90-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="61f90-130">granularidades explícita Olá são granularidade "automática" do toohello alternativas para o intervalo de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="61f90-131">Edição de gráficos e grades</span><span class="sxs-lookup"><span data-stu-id="61f90-131">Editing charts and grids</span></span>
<span data-ttu-id="61f90-132">tooadd uma nova folha de toohello do gráfico:</span><span class="sxs-lookup"><span data-stu-id="61f90-132">tooadd a new chart toohello blade:</span></span>

![No Metrics Explorer, escolher Adicionar Gráfico](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="61f90-134">Selecione **editar** em um tooedit novo ou existente do gráfico que mostra:</span><span class="sxs-lookup"><span data-stu-id="61f90-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Selecionar uma ou mais métricas](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="61f90-136">Você pode exibir mais de uma métrica em um gráfico, que não existem restrições sobre combinações de saudação que podem ser exibidas juntos.</span><span class="sxs-lookup"><span data-stu-id="61f90-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="61f90-137">Assim que você escolha uma métrica, alguns Olá que outras pessoas estão desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="61f90-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="61f90-138">Se você codificou [métricas personalizadas] [ track] em seu aplicativo (chamadas tooTrackMetric e TrackEvent) serão listados aqui.</span><span class="sxs-lookup"><span data-stu-id="61f90-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="61f90-139">Segmentar os dados</span><span class="sxs-lookup"><span data-stu-id="61f90-139">Segment your data</span></span>
<span data-ttu-id="61f90-140">Você pode dividir uma métrica pela propriedade - por exemplo, as exibições de página toocompare em clientes com sistemas operacionais diferentes.</span><span class="sxs-lookup"><span data-stu-id="61f90-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="61f90-141">Selecionar um gráfico ou grade, ative o agrupamento e selecionar toogroup uma propriedade por:</span><span class="sxs-lookup"><span data-stu-id="61f90-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Selecionar Agrupamento Ativo, então selecionar uma propriedade em Agrupar Por](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="61f90-143">Quando você usa o agrupamento, tipos de gráfico de barras e de área de saudação fornecem uma exibição de empilhadas.</span><span class="sxs-lookup"><span data-stu-id="61f90-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="61f90-144">Isso é adequado em que o método de agregação hello é Sum.</span><span class="sxs-lookup"><span data-stu-id="61f90-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="61f90-145">Mas, em que o tipo de agregação Olá média, escolha tipos de exibição de grade ou de linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="61f90-146">Se você codificou [métricas personalizadas] [ track] em seu aplicativo e elas incluem os valores de propriedade, você será capaz de tooselect propriedade de Olá na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="61f90-147">Gráfico de saudação é muito pequeno para dados segmentados?</span><span class="sxs-lookup"><span data-stu-id="61f90-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="61f90-148">Ajuste sua altura:</span><span class="sxs-lookup"><span data-stu-id="61f90-148">Adjust its height:</span></span>

![Ajuste o controle deslizante de saudação](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="61f90-150">Tipos de agregação</span><span class="sxs-lookup"><span data-stu-id="61f90-150">Aggregation types</span></span>
<span data-ttu-id="61f90-151">legenda Olá no lado de saudação por padrão geralmente mostra o valor de saudação agregada por período de saudação do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="61f90-152">Se você passar o mouse sobre o gráfico de hello, ele mostra o valor de saudação nesse ponto.</span><span class="sxs-lookup"><span data-stu-id="61f90-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="61f90-153">Cada ponto de dados no gráfico de saudação é uma agregação de valores de dados Olá recebida no hello anterior "granularidade" ou o intervalo de amostragem.</span><span class="sxs-lookup"><span data-stu-id="61f90-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="61f90-154">granularidade de saudação é exibida na parte superior de saudação da folha de saudação e varia de acordo com hello geral escala de tempo do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="61f90-155">Métricas podem ser agregadas de maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="61f90-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="61f90-156">**Contagem de** é uma contagem de eventos de saudação recebidos no intervalo de amostragem de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="61f90-157">Ela é usada para eventos como solicitações.</span><span class="sxs-lookup"><span data-stu-id="61f90-157">It is used for events such as requests.</span></span> <span data-ttu-id="61f90-158">Variações de altura de saudação do gráfico de saudação indica variações na taxa de saudação ocorrem eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="61f90-159">Mas observe que o valor numérico Olá muda quando você alterar o intervalo de amostragem de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="61f90-160">**Soma** adiciona valores de saudação de todos os pontos de dados Olá recebidos no período de saudação do gráfico hello, ou intervalo de amostragem de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="61f90-161">**Médio** divide Olá soma pelo número de saudação de pontos de dados recebidos por intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="61f90-162">**Únicas** são usadas para contagens de usuários e contas.</span><span class="sxs-lookup"><span data-stu-id="61f90-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="61f90-163">Durante o intervalo de amostragem de hello, ou em período de saudação do gráfico de saudação, Figura Olá mostra contagem de saudação de diferentes usuários vistos no momento.</span><span class="sxs-lookup"><span data-stu-id="61f90-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="61f90-164">**%** – versões de percentual de cada agregação são usadas somente com gráficos segmentados.</span><span class="sxs-lookup"><span data-stu-id="61f90-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="61f90-165">Olá total sempre adiciona o too100% e gráfico Olá mostra a contribuição relativa Olá dos diferentes componentes de um total.</span><span class="sxs-lookup"><span data-stu-id="61f90-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Agregação de percentual](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="61f90-167">Alterar o tipo de agregação Olá</span><span class="sxs-lookup"><span data-stu-id="61f90-167">Change hello aggregation type</span></span>

![Editar gráfico hello e, em seguida, selecione a agregação](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="61f90-169">método padrão de saudação para cada métrica é mostrado quando você cria um novo gráfico ou quando todas as métricas serão desmarcadas:</span><span class="sxs-lookup"><span data-stu-id="61f90-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Cancele a seleção de todos os padrões de saudação toosee de métricas](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="61f90-171">Eixo Y do PIN</span><span class="sxs-lookup"><span data-stu-id="61f90-171">Pin Y-axis</span></span> 
<span data-ttu-id="61f90-172">Por padrão, um gráfico mostra valores do eixo Y a partir do zero até valores máximo no intervalo de dados hello, toogive uma representação visual de quantum de valores hello.</span><span class="sxs-lookup"><span data-stu-id="61f90-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="61f90-173">Mas em alguns casos mais de quantum Olá talvez seja interessante toovisually inspecionar pequenas alterações em valores.</span><span class="sxs-lookup"><span data-stu-id="61f90-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="61f90-174">Para personalizações, como esse uso Olá intervalo edição recurso toopin Olá eixo y mínimo ou máximo valor do eixo y no local desejado.</span><span class="sxs-lookup"><span data-stu-id="61f90-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="61f90-175">Clique em "Configurações avançadas" caixa de seleção toobring backup Olá configurações de intervalo de eixo y</span><span class="sxs-lookup"><span data-stu-id="61f90-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Clique em Configurações Avançadas, selecione Intervalo personalizado e especifique os valores mín. e máx.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="61f90-177">Filtrar seus dados</span><span class="sxs-lookup"><span data-stu-id="61f90-177">Filter your data</span></span>
<span data-ttu-id="61f90-178">métricas de saudação apenas toosee para um conjunto de valores de propriedade selecionado:</span><span class="sxs-lookup"><span data-stu-id="61f90-178">toosee just hello metrics for a selected set of property values:</span></span>

![Clicar em Filtro, expandir uma propriedade e verificar alguns valores](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="61f90-180">Se você não selecionar valores para uma determinada propriedade, ele tem Olá mesmo como selecionar todos eles: não há nenhum filtro nessa propriedade.</span><span class="sxs-lookup"><span data-stu-id="61f90-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="61f90-181">Saudação de aviso contagens de eventos ao lado de cada valor de propriedade.</span><span class="sxs-lookup"><span data-stu-id="61f90-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="61f90-182">Quando você seleciona valores de uma propriedade, Olá conta junto com outros valores são ajustados de propriedade.</span><span class="sxs-lookup"><span data-stu-id="61f90-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="61f90-183">Os filtros se aplicam a gráficos de saudação tooall em uma folha.</span><span class="sxs-lookup"><span data-stu-id="61f90-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="61f90-184">Se você quiser diferentes filtros aplicados toodifferent gráficos, criar e salvar folhas diferentes métricas.</span><span class="sxs-lookup"><span data-stu-id="61f90-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="61f90-185">Se desejar, você pode fixar gráficos do painel de toohello folhas diferentes, para que você pode vê-los lado a lado.</span><span class="sxs-lookup"><span data-stu-id="61f90-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="61f90-186">Remover o tráfego de testes da Web e de bot</span><span class="sxs-lookup"><span data-stu-id="61f90-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="61f90-187">Usar o filtro de saudação **tráfego Real ou sintético** e verificar **Real**.</span><span class="sxs-lookup"><span data-stu-id="61f90-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="61f90-188">Você também pode filtrar por **Origem do tráfego sintético**.</span><span class="sxs-lookup"><span data-stu-id="61f90-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="61f90-189">lista de filtros de toohello tooadd propriedades</span><span class="sxs-lookup"><span data-stu-id="61f90-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="61f90-190">Você gostaria que toofilter telemetria em uma categoria de sua escolha?</span><span class="sxs-lookup"><span data-stu-id="61f90-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="61f90-191">Por exemplo, talvez você divida seus usuários em categorias diferentes e queira segmentar os dados segundo essas categorias.</span><span class="sxs-lookup"><span data-stu-id="61f90-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="61f90-192">[Crie sua própria propriedade](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="61f90-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="61f90-193">Defina-o um [telemetria inicializador](app-insights-api-custom-events-metrics.md#defaults) toohave aparecem em toda a telemetria - incluindo telemetria padrão Olá enviadas por diferentes módulos do SDK.</span><span class="sxs-lookup"><span data-stu-id="61f90-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="61f90-194">Editar o tipo de gráfico de saudação</span><span class="sxs-lookup"><span data-stu-id="61f90-194">Edit hello chart type</span></span>
<span data-ttu-id="61f90-195">Observe que você pode alternar entre gráficos e grades:</span><span class="sxs-lookup"><span data-stu-id="61f90-195">Notice that you can switch between grids and graphs:</span></span>

![Selecionar uma grade ou um gráfico e escolher um tipo de gráfico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="61f90-197">Salve sua folha de métricas</span><span class="sxs-lookup"><span data-stu-id="61f90-197">Save your metrics blade</span></span>
<span data-ttu-id="61f90-198">Quando você tiver criado alguns gráficos, salve-os como favoritos.</span><span class="sxs-lookup"><span data-stu-id="61f90-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="61f90-199">Você pode escolher se tooshare-lo com outros membros da equipe, se você usar uma conta organizacional.</span><span class="sxs-lookup"><span data-stu-id="61f90-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Escolher Favorito](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="61f90-201">novamente, folha de saudação toosee **folha de visão geral de toohello vá** e abrir favoritos:</span><span class="sxs-lookup"><span data-stu-id="61f90-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![Na folha de visão geral de saudação, escolha Favoritos](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="61f90-203">Se você escolher o intervalo de tempo relativo quando você salva, folha Olá será atualizada com as métricas mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="61f90-204">Se você escolher o intervalo de tempo absoluto, ele mostrará Olá mesmos dados toda vez.</span><span class="sxs-lookup"><span data-stu-id="61f90-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="61f90-205">Redefinição Olá folha</span><span class="sxs-lookup"><span data-stu-id="61f90-205">Reset hello blade</span></span>
<span data-ttu-id="61f90-206">Se você editar uma folha, mas, em seguida, você gostaria que o conjunto de backup toohello original salvada tooget, clique em Redefinir.</span><span class="sxs-lookup"><span data-stu-id="61f90-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![Nos botões de saudação na parte superior de saudação do Explorer de métrica](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="61f90-208">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="61f90-208">Live metrics stream</span></span>

<span data-ttu-id="61f90-209">Para obter uma exibição imediata da sua telemetria, abra [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="61f90-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="61f90-210">A maioria das métricas usem tooappear de alguns minutos, devido ao processo de saudação de agregação.</span><span class="sxs-lookup"><span data-stu-id="61f90-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="61f90-211">Por outro lado, as métricas em tempo real são otimizadas para baixa latência.</span><span class="sxs-lookup"><span data-stu-id="61f90-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="61f90-212">Definir alertas</span><span class="sxs-lookup"><span data-stu-id="61f90-212">Set alerts</span></span>
<span data-ttu-id="61f90-213">toobe notificado por email sobre valores incomuns de alguma das métricas, adicionar um alerta.</span><span class="sxs-lookup"><span data-stu-id="61f90-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="61f90-214">Você pode escolher os administradores de contas toohello de email Olá toosend ou toospecific endereços de email.</span><span class="sxs-lookup"><span data-stu-id="61f90-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![No Metrics Explorer, escolher Regras de Alerta, Adicionar Alerta](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="61f90-216">[Saiba mais sobre alertas][alerts].</span><span class="sxs-lookup"><span data-stu-id="61f90-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="61f90-217">Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="61f90-217">Continuous Export</span></span>
<span data-ttu-id="61f90-218">Se desejar que os dados sejam exportados de forma contínua para que você possa processá-los externamente, considere usar a [Exportação contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="61f90-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="61f90-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="61f90-219">Power BI</span></span>
<span data-ttu-id="61f90-220">Se você quiser ainda melhores exibições dos dados, você pode [exportar tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="61f90-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="61f90-221">Análise</span><span class="sxs-lookup"><span data-stu-id="61f90-221">Analytics</span></span>
<span data-ttu-id="61f90-222">[Análise de](app-insights-analytics.md) é um tooanalyze de maneira mais versátil sua telemetria usando uma linguagem de consulta avançada.</span><span class="sxs-lookup"><span data-stu-id="61f90-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="61f90-223">Usá-lo se você deseja toocombine resultados de métricas de computação ou executar uma análise detalhada do desempenho recentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61f90-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="61f90-224">Um gráfico de métrica, você pode clicar em Olá análise ícone tooget diretamente toohello equivalente consulta analítica.</span><span class="sxs-lookup"><span data-stu-id="61f90-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="61f90-225">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="61f90-225">Troubleshooting</span></span>
<span data-ttu-id="61f90-226">*Não vejo dados no gráfico.*</span><span class="sxs-lookup"><span data-stu-id="61f90-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="61f90-227">Os filtros se aplicam a gráficos de saudação tooall na folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="61f90-228">Certifique-se de que, enquanto você estiver concentrado em um gráfico, você não definiu um filtro que exclui todos os dados de saudação em outro.</span><span class="sxs-lookup"><span data-stu-id="61f90-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="61f90-229">Se você quiser tooset filtros diferentes gráficos diferentes, criá-los em diferentes folhas, salvá-los como algo separados Favoritos.</span><span class="sxs-lookup"><span data-stu-id="61f90-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="61f90-230">Se desejar, você pode fixá-los toohello painel para que você pode vê-los lado a lado.</span><span class="sxs-lookup"><span data-stu-id="61f90-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="61f90-231">Se um gráfico são agrupados por uma propriedade que não está definida na métrica hello, haverá nada no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="61f90-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="61f90-232">Tente limpar “agrupar por” ou escolha uma propriedade de agrupamento diferente.</span><span class="sxs-lookup"><span data-stu-id="61f90-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="61f90-233">Haverá dados de desempenho (CPU, taxa de E/S, etc.) disponíveis para serviços Web Java, aplicativos da área de trabalho do Windows, [aplicativos Web e serviços do IIS se você instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md) e os [Serviços de Nuvem do Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="61f90-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="61f90-234">Esses dados não estão disponíveis para sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="61f90-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="61f90-235">Vídeo</span><span class="sxs-lookup"><span data-stu-id="61f90-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="61f90-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61f90-236">Next steps</span></span>
* [<span data-ttu-id="61f90-237">Monitorando o uso com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="61f90-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="61f90-238">Usando a Pesquisa de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="61f90-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
