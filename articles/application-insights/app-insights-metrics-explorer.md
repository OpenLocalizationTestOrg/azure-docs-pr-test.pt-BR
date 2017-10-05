---
title: "Explorando métricas no Azure Application Insights | Microsoft Docs"
description: "Como interpretar os gráficos no gerenciador de métricas e como personalizar as folhas do gerenciador de métricas."
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
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="634b1-103">Explorar métricas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="634b1-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="634b1-104">Métricas no [Application Insights][start] são contagens e valores medidos de eventos enviados em telemetria do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="634b1-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="634b1-105">Eles ajudam você a detectar problemas de desempenho e observar as tendências referentes a como seu aplicativo está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="634b1-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="634b1-106">Há uma grande variedade de métricas padrão, e você também pode criar suas próprias métricas e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="634b1-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="634b1-107">Contagens de métricas e eventos são exibidas em gráficos de valores agregados como somas, médias ou contagens.</span><span class="sxs-lookup"><span data-stu-id="634b1-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="634b1-108">Aqui está um exemplo de conjunto de gráficos:</span><span class="sxs-lookup"><span data-stu-id="634b1-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="634b1-109">No portal do Application Insights, você encontra gráficos de métricas em todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="634b1-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="634b1-110">Na maioria dos casos, eles podem ser personalizados e você pode adicionar mais gráficos à folha.</span><span class="sxs-lookup"><span data-stu-id="634b1-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="634b1-111">Na folha visão geral, clique para gráficos mais detalhados (que têm títulos como "Servidor") ou clique em **Metrics Explorer** para abrir uma nova folha em que você possa criar gráficos personalizados.</span><span class="sxs-lookup"><span data-stu-id="634b1-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="634b1-112">Intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="634b1-112">Time range</span></span>
<span data-ttu-id="634b1-113">Você pode alterar o intervalo de tempo coberto pelos gráficos ou grades em qualquer folha.</span><span class="sxs-lookup"><span data-stu-id="634b1-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Abrir a lâmina de visão geral do seu aplicativo no portal do Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="634b1-115">Se você estiver esperando dados que não apareceram ainda, clique em Atualizar.</span><span class="sxs-lookup"><span data-stu-id="634b1-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="634b1-116">Os gráficos são atualizados em intervalos, mas os intervalos são mais longos para intervalos de tempo maiores.</span><span class="sxs-lookup"><span data-stu-id="634b1-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="634b1-117">Pode levar algum tempo para que dados passem pelo pipeline de análise e sejam representados em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="634b1-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="634b1-118">Para ampliar parte de um gráfico, arraste sobre ele:</span><span class="sxs-lookup"><span data-stu-id="634b1-118">To zoom into part of a chart, drag over it:</span></span>

![Arraste por parte de um gráfico.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="634b1-120">Clique no botão Desfazer Zoom para restaurá-lo.</span><span class="sxs-lookup"><span data-stu-id="634b1-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="634b1-121">Valores de granularidade e ponto</span><span class="sxs-lookup"><span data-stu-id="634b1-121">Granularity and point values</span></span>
<span data-ttu-id="634b1-122">Passe o mouse sobre o gráfico para exibir os valores das métricas nesse determinado ponto.</span><span class="sxs-lookup"><span data-stu-id="634b1-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![Passar o ponteiro do mouse sobre um gráfico](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="634b1-124">O valor de métrica em um ponto específico é agregado durante o intervalo de amostragem anterior.</span><span class="sxs-lookup"><span data-stu-id="634b1-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="634b1-125">O intervalo de amostragem ou "granularidade" é mostrado na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="634b1-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![O cabeçalho de uma folha.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="634b1-127">Você pode ajustar a granularidade na folha Intervalo de tempo:</span><span class="sxs-lookup"><span data-stu-id="634b1-127">You can adjust the granularity in the Time range blade:</span></span>

![O cabeçalho de uma folha.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="634b1-129">As granularidades disponíveis dependem do intervalo de tempo selecionado.</span><span class="sxs-lookup"><span data-stu-id="634b1-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="634b1-130">As granularidades explícitas são alternativas à granularidade "automática" para o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="634b1-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="634b1-131">Edição de gráficos e grades</span><span class="sxs-lookup"><span data-stu-id="634b1-131">Editing charts and grids</span></span>
<span data-ttu-id="634b1-132">Para adicionar um novo gráfico à folha:</span><span class="sxs-lookup"><span data-stu-id="634b1-132">To add a new chart to the blade:</span></span>

![No Metrics Explorer, escolher Adicionar Gráfico](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="634b1-134">Escolha **Editar** em um gráfico novo ou existente para editar o conteúdo exibido por ele:</span><span class="sxs-lookup"><span data-stu-id="634b1-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![Selecionar uma ou mais métricas](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="634b1-136">Você pode exibir mais de uma métrica em um gráfico, porém há restrições sobre as combinações que podem ser exibidas em conjunto.</span><span class="sxs-lookup"><span data-stu-id="634b1-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="634b1-137">Assim que você escolher uma métrica, algumas das outras serão desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="634b1-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="634b1-138">Se você tiver codificado [métricas personalizadas][track] em seu aplicativo (chamadas para TrackMetric e TrackEvent), elas serão listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="634b1-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="634b1-139">Segmentar os dados</span><span class="sxs-lookup"><span data-stu-id="634b1-139">Segment your data</span></span>
<span data-ttu-id="634b1-140">Você pode dividir uma métrica por propriedade - por exemplo, para comparar exibições de página em clientes com sistemas operacionais diferentes.</span><span class="sxs-lookup"><span data-stu-id="634b1-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="634b1-141">Selecione um gráfico ou uma grade, ative o agrupamento e escolha uma propriedade pela qual agrupar:</span><span class="sxs-lookup"><span data-stu-id="634b1-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![Selecionar Agrupamento Ativo, então selecionar uma propriedade em Agrupar Por](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="634b1-143">Quando você usa o agrupamento, os tipos de gráfico de Barras e de Área fornecem uma exibição empilhada.</span><span class="sxs-lookup"><span data-stu-id="634b1-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="634b1-144">Isso é adequado quando o método de Agregação é Soma.</span><span class="sxs-lookup"><span data-stu-id="634b1-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="634b1-145">Mas onde o tipo de agregação é Média, escolha os tipos de exibição de Linha ou Grade.</span><span class="sxs-lookup"><span data-stu-id="634b1-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="634b1-146">Se você tiver codificado [métricas personalizadas][track] em seu aplicativo e elas incluírem valores de propriedade, você poderá selecionar a propriedade na lista.</span><span class="sxs-lookup"><span data-stu-id="634b1-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="634b1-147">O gráfico é muito pequeno para dados segmentados?</span><span class="sxs-lookup"><span data-stu-id="634b1-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="634b1-148">Ajuste sua altura:</span><span class="sxs-lookup"><span data-stu-id="634b1-148">Adjust its height:</span></span>

![Ajustar a barra de controle deslizante](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="634b1-150">Tipos de agregação</span><span class="sxs-lookup"><span data-stu-id="634b1-150">Aggregation types</span></span>
<span data-ttu-id="634b1-151">A legenda na lateral normalmente mostra, por padrão, o valor agregado durante o período do gráfico.</span><span class="sxs-lookup"><span data-stu-id="634b1-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="634b1-152">Se você passar o mouse sobre o gráfico, ele mostra o valor nesse ponto.</span><span class="sxs-lookup"><span data-stu-id="634b1-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="634b1-153">Cada ponto de dados no gráfico é um acumulado dos valores de dados recebidos no intervalo de amostragem anterior, ou "granularidade".</span><span class="sxs-lookup"><span data-stu-id="634b1-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="634b1-154">A granularidade é mostrada na parte superior da folha e varia de acordo com a escala de tempo total do gráfico.</span><span class="sxs-lookup"><span data-stu-id="634b1-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="634b1-155">Métricas podem ser agregadas de maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="634b1-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="634b1-156">**Contagem** é uma contagem de eventos recebidos no intervalo de amostragem.</span><span class="sxs-lookup"><span data-stu-id="634b1-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="634b1-157">Ela é usada para eventos como solicitações.</span><span class="sxs-lookup"><span data-stu-id="634b1-157">It is used for events such as requests.</span></span> <span data-ttu-id="634b1-158">Variações na altura do gráfico indicam variações na taxa em que os eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="634b1-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="634b1-159">Mas observe que o valor numérico é alterado quando você altera o intervalo de amostragem.</span><span class="sxs-lookup"><span data-stu-id="634b1-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="634b1-160">**Soma** adiciona os valores de todos os pontos de dados recebidos no intervalo de amostragem ou no período do gráfico.</span><span class="sxs-lookup"><span data-stu-id="634b1-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="634b1-161">**Média** divide a Soma pelo número de pontos de dados recebidos durante o intervalo.</span><span class="sxs-lookup"><span data-stu-id="634b1-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="634b1-162">**Únicas** são usadas para contagens de usuários e contas.</span><span class="sxs-lookup"><span data-stu-id="634b1-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="634b1-163">Durante o intervalo de amostragem, ou durante o período do gráfico, a figura mostra a contagem de diferentes usuários vistos no momento.</span><span class="sxs-lookup"><span data-stu-id="634b1-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="634b1-164">**%** – versões de percentual de cada agregação são usadas somente com gráficos segmentados.</span><span class="sxs-lookup"><span data-stu-id="634b1-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="634b1-165">O total sempre resulta em 100% e o gráfico mostra a contribuição relativa de diferentes componentes de um total.</span><span class="sxs-lookup"><span data-stu-id="634b1-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![Agregação de percentual](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="634b1-167">Alterar o tipo de agregação</span><span class="sxs-lookup"><span data-stu-id="634b1-167">Change the aggregation type</span></span>

![Editar o gráfico e selecionar agregação](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="634b1-169">O método padrão para cada métrica é mostrado quando você cria um novo gráfico ou quando todas as métricas são desmarcadas:</span><span class="sxs-lookup"><span data-stu-id="634b1-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Desmarque a seleção de todas as métricas para ver os padrões](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="634b1-171">Eixo Y do PIN</span><span class="sxs-lookup"><span data-stu-id="634b1-171">Pin Y-axis</span></span> 
<span data-ttu-id="634b1-172">Por padrão, um gráfico mostra valores do eixo Y a partir do zero até os valores máximos no intervalo de dados, para fornecer uma representação visual do quantum dos valores.</span><span class="sxs-lookup"><span data-stu-id="634b1-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="634b1-173">Mas, em alguns casos, mais do que o quantum, pode ser interessante inspecionar visualmente pequenas alterações nos valores.</span><span class="sxs-lookup"><span data-stu-id="634b1-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="634b1-174">Para personalizações como essa, use o recurso de edição de intervalo do eixo Y para fixar o valor mínimo ou máximo do eixo Y no local desejado.</span><span class="sxs-lookup"><span data-stu-id="634b1-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="634b1-175">Clique na caixa de seleção "Configurações Avançadas" para exibir as configurações do intervalo do eixo Y</span><span class="sxs-lookup"><span data-stu-id="634b1-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![Clique em Configurações Avançadas, selecione Intervalo personalizado e especifique os valores mín. e máx.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="634b1-177">Filtrar seus dados</span><span class="sxs-lookup"><span data-stu-id="634b1-177">Filter your data</span></span>
<span data-ttu-id="634b1-178">Para ver apenas as métricas para um conjunto selecionado de valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="634b1-178">To see just the metrics for a selected set of property values:</span></span>

![Clicar em Filtro, expandir uma propriedade e verificar alguns valores](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="634b1-180">Se você não selecionar nenhum valor para uma determinada propriedade, será o mesmo que selecionar todas elas: não há nenhum filtro para essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="634b1-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="634b1-181">Observe as contagens de eventos junto a cada valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="634b1-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="634b1-182">Quando você seleciona valores de uma propriedade, as contagens junto a outros valores de propriedade são ajustadas.</span><span class="sxs-lookup"><span data-stu-id="634b1-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="634b1-183">Os filtros se aplicam a todos os gráficos em uma folha.</span><span class="sxs-lookup"><span data-stu-id="634b1-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="634b1-184">Se você quiser filtros diferentes aplicados a gráficos diferentes, crie e salve folhas de métricas diferentes.</span><span class="sxs-lookup"><span data-stu-id="634b1-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="634b1-185">Se desejar, você pode fixar gráficos de diferentes folhas ao painel para vê-los lado a lado.</span><span class="sxs-lookup"><span data-stu-id="634b1-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="634b1-186">Remover o tráfego de testes da Web e de bot</span><span class="sxs-lookup"><span data-stu-id="634b1-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="634b1-187">Use o filtro **Tráfego real ou sintético** e marque **Real**.</span><span class="sxs-lookup"><span data-stu-id="634b1-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="634b1-188">Você também pode filtrar por **Origem do tráfego sintético**.</span><span class="sxs-lookup"><span data-stu-id="634b1-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="634b1-189">Para adicionar propriedades à lista de filtros</span><span class="sxs-lookup"><span data-stu-id="634b1-189">To add properties to the filter list</span></span>
<span data-ttu-id="634b1-190">Você deseja filtrar a telemetria em uma categoria de sua escolha?</span><span class="sxs-lookup"><span data-stu-id="634b1-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="634b1-191">Por exemplo, talvez você divida seus usuários em categorias diferentes e queira segmentar os dados segundo essas categorias.</span><span class="sxs-lookup"><span data-stu-id="634b1-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="634b1-192">[Crie sua própria propriedade](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="634b1-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="634b1-193">Defina-a em um [Inicializador de Telemetria](app-insights-api-custom-events-metrics.md#defaults) para que ela apareça em toda a telemetria, incluindo a telemetria padrão enviada por diferentes módulos do SDK.</span><span class="sxs-lookup"><span data-stu-id="634b1-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="634b1-194">Editar o tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="634b1-194">Edit the chart type</span></span>
<span data-ttu-id="634b1-195">Observe que você pode alternar entre gráficos e grades:</span><span class="sxs-lookup"><span data-stu-id="634b1-195">Notice that you can switch between grids and graphs:</span></span>

![Selecionar uma grade ou um gráfico e escolher um tipo de gráfico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="634b1-197">Salve sua folha de métricas</span><span class="sxs-lookup"><span data-stu-id="634b1-197">Save your metrics blade</span></span>
<span data-ttu-id="634b1-198">Quando você tiver criado alguns gráficos, salve-os como favoritos.</span><span class="sxs-lookup"><span data-stu-id="634b1-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="634b1-199">Se você utiliza uma conta organizacional, você pode escolher entre compartilhá-la ou não com outros membros da equipe.</span><span class="sxs-lookup"><span data-stu-id="634b1-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![Escolher Favorito](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="634b1-201">Para ver a folha novamente, **vá até a folha de visão geral** e abra Favoritos:</span><span class="sxs-lookup"><span data-stu-id="634b1-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![Na folha Visão Geral, selecionar Favoritos](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="634b1-203">Se você escolheu o intervalo de tempo Relativo quando salvou, a folha será atualizada com as métricas mais recentes.</span><span class="sxs-lookup"><span data-stu-id="634b1-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="634b1-204">Se você escolheu o intervalo de tempo Absoluto, ele mostrará sempre os mesmos dados.</span><span class="sxs-lookup"><span data-stu-id="634b1-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="634b1-205">Redefinir a folha</span><span class="sxs-lookup"><span data-stu-id="634b1-205">Reset the blade</span></span>
<span data-ttu-id="634b1-206">Se você editar uma folha mas em seguida decidir voltar ao conjunto original salvo, clique em Redefinir.</span><span class="sxs-lookup"><span data-stu-id="634b1-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![Nos botões na parte superior do Metrics Explorer](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="634b1-208">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="634b1-208">Live metrics stream</span></span>

<span data-ttu-id="634b1-209">Para obter uma exibição imediata da sua telemetria, abra [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="634b1-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="634b1-210">A maioria das métricas leva alguns minutos para aparecer devido ao processo de agregação.</span><span class="sxs-lookup"><span data-stu-id="634b1-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="634b1-211">Por outro lado, as métricas em tempo real são otimizadas para baixa latência.</span><span class="sxs-lookup"><span data-stu-id="634b1-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="634b1-212">Definir alertas</span><span class="sxs-lookup"><span data-stu-id="634b1-212">Set alerts</span></span>
<span data-ttu-id="634b1-213">Para ser notificado por email sobre valores incomuns de qualquer métrica, adicione um alerta.</span><span class="sxs-lookup"><span data-stu-id="634b1-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="634b1-214">Você pode escolher para enviar o email para os administradores de conta ou para endereços de email específicos.</span><span class="sxs-lookup"><span data-stu-id="634b1-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![No Metrics Explorer, escolher Regras de Alerta, Adicionar Alerta](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="634b1-216">[Saiba mais sobre alertas][alerts].</span><span class="sxs-lookup"><span data-stu-id="634b1-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="634b1-217">Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="634b1-217">Continuous Export</span></span>
<span data-ttu-id="634b1-218">Se desejar que os dados sejam exportados de forma contínua para que você possa processá-los externamente, considere usar a [Exportação contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="634b1-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="634b1-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="634b1-219">Power BI</span></span>
<span data-ttu-id="634b1-220">Se desejar obter exibições ainda mais avançadas dos seus dados, você poderá [exportar para o Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="634b1-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="634b1-221">Análise</span><span class="sxs-lookup"><span data-stu-id="634b1-221">Analytics</span></span>
<span data-ttu-id="634b1-222">[Análise](app-insights-analytics.md) é uma maneira mais versátil de analisar a telemetria usando uma linguagem de consulta eficiente.</span><span class="sxs-lookup"><span data-stu-id="634b1-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="634b1-223">Use-a se quiser combinar ou calcular resultados de métricas ou executar uma exploração detalhada do desempenho recente de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="634b1-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="634b1-224">Em um gráfico de métricas, clique no ícone do Analytics para ir diretamente à consulta do Analytics equivalente.</span><span class="sxs-lookup"><span data-stu-id="634b1-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="634b1-225">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="634b1-225">Troubleshooting</span></span>
<span data-ttu-id="634b1-226">*Não vejo dados no gráfico.*</span><span class="sxs-lookup"><span data-stu-id="634b1-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="634b1-227">Os filtros se aplicam a todos os gráficos da folha.</span><span class="sxs-lookup"><span data-stu-id="634b1-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="634b1-228">Verifique se, ao se concentrar em um gráfico, não definiu um filtro que excluía todos os dados em outro.</span><span class="sxs-lookup"><span data-stu-id="634b1-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="634b1-229">Se quiser definir filtros diferentes em gráficos diferentes, crie-os em folhas diferentes e os salve como favoritos separados.</span><span class="sxs-lookup"><span data-stu-id="634b1-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="634b1-230">Se desejar, você poderá fixá-los ao painel para que eles sejam exibidos lado a lado.</span><span class="sxs-lookup"><span data-stu-id="634b1-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="634b1-231">Se você agrupar um gráfico por uma propriedade que não esteja definida na métrica, o gráfico ficará vazio.</span><span class="sxs-lookup"><span data-stu-id="634b1-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="634b1-232">Tente limpar “agrupar por” ou escolha uma propriedade de agrupamento diferente.</span><span class="sxs-lookup"><span data-stu-id="634b1-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="634b1-233">Haverá dados de desempenho (CPU, taxa de E/S, etc.) disponíveis para serviços Web Java, aplicativos da área de trabalho do Windows, [aplicativos Web e serviços do IIS se você instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md) e os [Serviços de Nuvem do Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="634b1-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="634b1-234">Esses dados não estão disponíveis para sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="634b1-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="634b1-235">Vídeo</span><span class="sxs-lookup"><span data-stu-id="634b1-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="634b1-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="634b1-236">Next steps</span></span>
* [<span data-ttu-id="634b1-237">Monitorando o uso com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="634b1-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="634b1-238">Usando a Pesquisa de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="634b1-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
