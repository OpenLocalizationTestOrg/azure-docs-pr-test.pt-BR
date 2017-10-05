---
title: "Painéis e navegação no Azure Application Insights | Microsoft Docs"
description: "Crie exibições de suas consultas e gráficos principais do APM."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="27385-103">Navegação e painéis no portal do Application Insights</span><span class="sxs-lookup"><span data-stu-id="27385-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="27385-104">Após de ter [Configurado o Application Insights no seu projeto](app-insights-overview.md), os dados de telemetria sobre desempenho e uso do aplicativo aparecerá no recurso do Application Insights do projeto no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27385-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="27385-105">Encontrar sua telemetria</span><span class="sxs-lookup"><span data-stu-id="27385-105">Find your telemetry</span></span>
<span data-ttu-id="27385-106">Entre no [portal do Azure](https://portal.azure.com) e navegue até o recurso do Application Insights que você criou para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27385-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Clique em Procurar, selecione Application Insights e seu aplicativo.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="27385-108">A folha (página) de visão geral para seu aplicativo mostra um resumo das principais métricas de diagnóstico de seu aplicativo, e um gateway para outros recursos do portal.</span><span class="sxs-lookup"><span data-stu-id="27385-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Rotas principais para exibir sua telemetria](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="27385-110">Você pode personalizar qualquer um dos gráficos e grades e fixá-los em um painel.</span><span class="sxs-lookup"><span data-stu-id="27385-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="27385-111">Dessa forma, você pode reunir a telemetria da chave de aplicativos diferentes em um painel central.</span><span class="sxs-lookup"><span data-stu-id="27385-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="27385-112">Painéis</span><span class="sxs-lookup"><span data-stu-id="27385-112">Dashboards</span></span>
<span data-ttu-id="27385-113">A primeira coisa que você vê depois de entrar no [Portal do Microsoft Azure](https://portal.azure.com) é um painel.</span><span class="sxs-lookup"><span data-stu-id="27385-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="27385-114">Aqui, você pode reunir os gráficos que são mais importantes para você em todos os seus recursos do Azure, incluindo a telemetria do [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27385-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Um painel personalizado.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="27385-116">**Navegar até recursos específicos** como seu aplicativo no Application Insights: use a barra à esquerda.</span><span class="sxs-lookup"><span data-stu-id="27385-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="27385-117">**Voltar para o painel atual** ou alternar para outros modos recentes: use o menu suspenso na parte superior esquerda.</span><span class="sxs-lookup"><span data-stu-id="27385-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="27385-118">**Alternar painéis**: use o menu suspenso no título do painel</span><span class="sxs-lookup"><span data-stu-id="27385-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="27385-119">**Criar, editar e compartilhar painéis** na barra de ferramentas do painel.</span><span class="sxs-lookup"><span data-stu-id="27385-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="27385-120">**Editar o painel**: passe o mouse sobre um bloco e use sua barra superior para movê-lo, personalizá-lo ou removê-lo.</span><span class="sxs-lookup"><span data-stu-id="27385-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="27385-121">Adicionar a um painel</span><span class="sxs-lookup"><span data-stu-id="27385-121">Add to a dashboard</span></span>
<span data-ttu-id="27385-122">Quando estiver vendo uma folha ou conjunto de gráficos que é particularmente interessante, você poderá fixá-los no painel.</span><span class="sxs-lookup"><span data-stu-id="27385-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="27385-123">Você o verá da próxima vez que retornar.</span><span class="sxs-lookup"><span data-stu-id="27385-123">You'll see it next time you return there.</span></span>

![Para fixar um gráfico, passe o mouse sobre ele e clique em "…" no cabeçalho.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="27385-125">Fixe um gráfico no painel.</span><span class="sxs-lookup"><span data-stu-id="27385-125">Pin chart to dashboard.</span></span> <span data-ttu-id="27385-126">Uma cópia do gráfico é exibida no painel.</span><span class="sxs-lookup"><span data-stu-id="27385-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="27385-127">Fixe a folha inteira no painel - ela aparecerá no painel como um bloco em que você poderá clicar.</span><span class="sxs-lookup"><span data-stu-id="27385-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="27385-128">Clique o canto superior esquerdo para retornar ao painel atual.</span><span class="sxs-lookup"><span data-stu-id="27385-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="27385-129">Em seguida, você poderá usar o menu suspenso para retornar ao modo de exibição atual.</span><span class="sxs-lookup"><span data-stu-id="27385-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="27385-130">Observe que os gráficos são agrupados em blocos: um bloco pode conter mais de um gráfico.</span><span class="sxs-lookup"><span data-stu-id="27385-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="27385-131">O bloco inteiro é fixado no painel.</span><span class="sxs-lookup"><span data-stu-id="27385-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="27385-132">O gráfico é atualizado automaticamente com uma frequência que depende do intervalo de tempo do gráfico:</span><span class="sxs-lookup"><span data-stu-id="27385-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="27385-133">Intervalo de tempo até 1 hora: atualizar a cada 5 minutos</span><span class="sxs-lookup"><span data-stu-id="27385-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="27385-134">Intervalo de tempo de 1 a 24 horas: atualizar a cada 15 minutos</span><span class="sxs-lookup"><span data-stu-id="27385-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="27385-135">Intervalo de tempo acima de 24 horas: (intervalo de tempo)/60.</span><span class="sxs-lookup"><span data-stu-id="27385-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="27385-136">Fixar qualquer consulta no Analytics</span><span class="sxs-lookup"><span data-stu-id="27385-136">Pin any query in Analytics</span></span>
<span data-ttu-id="27385-137">Você também pode [fixar gráficos do Analytics](app-insights-analytics-using.md#pin-to-dashboard) a um painel [compartilhado](#share-dashboards-with-your-team).</span><span class="sxs-lookup"><span data-stu-id="27385-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="27385-138">Isso permite que você adicione gráficos de qualquer consulta arbitrária junto com as métricas padrão.</span><span class="sxs-lookup"><span data-stu-id="27385-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="27385-139">Os resultados são automaticamente recalculados a cada hora.</span><span class="sxs-lookup"><span data-stu-id="27385-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="27385-140">Clique no ícone Atualizar no gráfico para recalcular imediatamente.</span><span class="sxs-lookup"><span data-stu-id="27385-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="27385-141">(Atualizar do navegador não é recalculado.)</span><span class="sxs-lookup"><span data-stu-id="27385-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="27385-142">Ajustar um bloco no painel</span><span class="sxs-lookup"><span data-stu-id="27385-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="27385-143">Quando um bloco estiver no painel, você poderá ajustá-lo.</span><span class="sxs-lookup"><span data-stu-id="27385-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Passe o mouse sobre um gráfico para editá-lo.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="27385-145">Adicione um gráfico ao bloco.</span><span class="sxs-lookup"><span data-stu-id="27385-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="27385-146">Defina a métrica, a dimensão de grupo e o estilo (tabela, gráfico) de um diagrama.</span><span class="sxs-lookup"><span data-stu-id="27385-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="27385-147">Percorra o diagrama para aplicar zoom; clique no botão de desfazer para redefinir o período de tempo; defina propriedades de filtro para os gráficos no bloco.</span><span class="sxs-lookup"><span data-stu-id="27385-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="27385-148">Defina o título do bloco.</span><span class="sxs-lookup"><span data-stu-id="27385-148">Set tile title.</span></span>

<span data-ttu-id="27385-149">Blocos fixados de folhas do Metric Explorer têm mais opções de edição que aqueles fixados de uma folha de Visão Geral.</span><span class="sxs-lookup"><span data-stu-id="27385-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="27385-150">O bloco original que você fixou não é afetado por suas edições.</span><span class="sxs-lookup"><span data-stu-id="27385-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="27385-151">Alternar entre painéis</span><span class="sxs-lookup"><span data-stu-id="27385-151">Switch between dashboards</span></span>
<span data-ttu-id="27385-152">É possível salvar mais de um painel e alternar entre eles.</span><span class="sxs-lookup"><span data-stu-id="27385-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="27385-153">Quando você fixa um gráfico ou folha, ele é adicionado ao painel atual.</span><span class="sxs-lookup"><span data-stu-id="27385-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Para alternar entre os painéis, clique em Painel e selecione um painel salvo.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="27385-157">Por exemplo, você pode ter um painel para exibir em tela inteira na sala da equipe e outro para desenvolvimento geral.</span><span class="sxs-lookup"><span data-stu-id="27385-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="27385-158">No painel, uma folha é exibida como um bloco: clique nele para ir para a folha.</span><span class="sxs-lookup"><span data-stu-id="27385-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="27385-159">Um gráfico replica o gráfico em seu local original.</span><span class="sxs-lookup"><span data-stu-id="27385-159">A chart replicates the chart in its original location.</span></span>

![Clique em um bloco para abrir a folha que ele representa](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="27385-161">Compartilhar painéis</span><span class="sxs-lookup"><span data-stu-id="27385-161">Share dashboards</span></span>
<span data-ttu-id="27385-162">Quando você tiver criado um painel, poderá compartilhá-lo com outros usuários.</span><span class="sxs-lookup"><span data-stu-id="27385-162">When you've created a dashboard, you can share it with other users.</span></span>

![No cabeçalho do painel de controle, clique em Compartilhar](./media/app-insights-dashboards/41.png)

<span data-ttu-id="27385-164">Saiba mais sobre [Funções e controle de acesso](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="27385-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="27385-165">Navegação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="27385-165">App navigation</span></span>
<span data-ttu-id="27385-166">A folha de visão geral é o gateway para obter mais informações sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27385-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="27385-167">**Qualquer gráfico ou bloco** - clique em qualquer bloco ou gráfico para ver mais detalhes sobre o que ele exibe.</span><span class="sxs-lookup"><span data-stu-id="27385-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="27385-168">Botões da folha Visão geral</span><span class="sxs-lookup"><span data-stu-id="27385-168">Overview blade buttons</span></span>
![Barra de navegação superior da folha Visão geral](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="27385-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) -crie seus próprios gráficos de desempenho e de uso.</span><span class="sxs-lookup"><span data-stu-id="27385-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="27385-171">[**Pesquisa**](app-insights-diagnostic-search.md) - para investigar instâncias específicas de eventos, como solicitações, exceções ou log de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="27385-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="27385-172">[**Analytics**](app-insights-analytics.md) - consultas poderosas em sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="27385-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="27385-173">**Intervalo de tempo** -ajuste o intervalo exibido por todos os gráficos na folha.</span><span class="sxs-lookup"><span data-stu-id="27385-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="27385-174">**Excluir** -exclua o recurso Application Insights para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27385-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="27385-175">Você deve também remover os pacotes do Application Insights do código do seu aplicativo, ou editar a [chave de instrumentação](app-insights-create-new-resource.md#copy-the-instrumentation-key) em seu aplicativo para direcionar a telemetria para um recurso diferente do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="27385-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="27385-176">Guia Conceitos Básicos</span><span class="sxs-lookup"><span data-stu-id="27385-176">Essentials tab</span></span>
* <span data-ttu-id="27385-177">[Chave de instrumentação](app-insights-create-new-resource.md#copy-the-instrumentation-key) -identifica esse recurso de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27385-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="27385-178">Preço - disponibilize as funcionalidades disponíveis e defina volumes.</span><span class="sxs-lookup"><span data-stu-id="27385-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="27385-179">Barra de navegação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="27385-179">App navigation bar</span></span>
![Barra de navegação à esquerda](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="27385-181">**Visão geral** -volte para a folha de visão geral do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27385-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="27385-182">**Log de atividades** -alertas e eventos administrativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="27385-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="27385-183">[**Controle de acesso**](app-insights-resources-roles-access-control.md) -forneça acesso a membros da equipe e outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="27385-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="27385-184">[**Marcas**](../azure-resource-manager/resource-group-using-tags.md) -use marcas para agrupar seu aplicativo com outros.</span><span class="sxs-lookup"><span data-stu-id="27385-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="27385-185">INVESTIGAR</span><span class="sxs-lookup"><span data-stu-id="27385-185">INVESTIGATE</span></span>

* <span data-ttu-id="27385-186">[**Mapa de aplicativos**](app-insights-app-map.md) - mapa ativo mostrando os componentes do aplicativo, derivado das informações de dependência.</span><span class="sxs-lookup"><span data-stu-id="27385-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="27385-187">[**Detecção Inteligente**](app-insights-proactive-diagnostics.md) - Examine os alertas de desempenho recentes.</span><span class="sxs-lookup"><span data-stu-id="27385-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="27385-188">[**Live Stream**](app-insights-live-stream.md) - um conjunto fixo de métricas quase instantâneas, úteis ao implantar um novo build ou depurar.</span><span class="sxs-lookup"><span data-stu-id="27385-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="27385-189">[**Disponibilidade/testes da Web**](app-insights-monitor-web-app-availability.md) -envie solicitações regulares ao seu aplicativo Web no mundo inteiro.*</span><span class="sxs-lookup"><span data-stu-id="27385-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="27385-190">[**Falhas, Desempenho**](app-insights-web-monitor-performance.md) -exceções, taxas de falha e tempos de resposta para solicitações ao seu aplicativo e para solicitações de seu aplicativo para [dependências](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="27385-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="27385-191">[**Desempenho**](app-insights-web-monitor-performance.md) - tempo de resposta, tempos de resposta de dependência.</span><span class="sxs-lookup"><span data-stu-id="27385-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="27385-192">[Servidores](app-insights-web-monitor-performance.md) - contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="27385-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="27385-193">Disponível se você [instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="27385-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="27385-194">**Navegador** - exibição de página e desempenho do AJAX.</span><span class="sxs-lookup"><span data-stu-id="27385-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="27385-195">Disponível se você [instrumentar suas páginas da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="27385-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="27385-196">**Uso** - contagens de sessão, usuário e exibição de página.</span><span class="sxs-lookup"><span data-stu-id="27385-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="27385-197">Disponível se você [instrumentar suas páginas da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="27385-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="27385-198">CONFIGURAR</span><span class="sxs-lookup"><span data-stu-id="27385-198">CONFIGURE</span></span>

* <span data-ttu-id="27385-199">**Introdução** - tutorial embutido.</span><span class="sxs-lookup"><span data-stu-id="27385-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="27385-200">**Propriedades** - chave de instrumentação, assinatura e ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="27385-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="27385-201">[Alertas](app-insights-alerts.md) - configuração do alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="27385-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="27385-202">[Exportação contínua](app-insights-export-telemetry.md) - configure a exportação de telemetria no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="27385-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="27385-203">[Teste de desempenho](app-insights-monitor-web-app-availability.md#performance-tests) - configure uma carga sintética no seu site.</span><span class="sxs-lookup"><span data-stu-id="27385-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="27385-204">[Cota e preço](app-insights-pricing.md) e [amostragem de ingestão](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="27385-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="27385-205">**Acesso à API** - atualmente usado para criar [anotações de versão](app-insights-annotations.md) e para a API de Acesso a Dados.</span><span class="sxs-lookup"><span data-stu-id="27385-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="27385-206">[**Itens de Trabalho**](app-insights-diagnostic-search.md#create-work-item) - conecte-se a um sistema de controle do trabalho de forma que você possa criar bugs enquanto inspeciona a telemetria.</span><span class="sxs-lookup"><span data-stu-id="27385-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="27385-207">CONFIGURAÇÕES</span><span class="sxs-lookup"><span data-stu-id="27385-207">SETTINGS</span></span>

* <span data-ttu-id="27385-208">[**Bloqueios**](../azure-resource-manager/resource-group-lock-resources.md) - bloqueie recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="27385-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="27385-209">[**Script de automação**](app-insights-powershell.md) - exporte uma definição do recurso do Azure para que você possa usá-la como modelo para criar novos recursos.</span><span class="sxs-lookup"><span data-stu-id="27385-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="27385-210">Vídeo</span><span class="sxs-lookup"><span data-stu-id="27385-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="27385-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27385-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="27385-212">Metrics explorer</span><span class="sxs-lookup"><span data-stu-id="27385-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="27385-213">Métricas de filtro e de segmento</span><span class="sxs-lookup"><span data-stu-id="27385-213">Filter and segment metrics</span></span> |![Exemplo de pesquisa](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="27385-215">Pesquisa de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="27385-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="27385-216">Localize e inspecione eventos, eventos relacionados e crie bugs</span><span class="sxs-lookup"><span data-stu-id="27385-216">Find and inspect events, related events, and create bugs</span></span> |![Exemplo de pesquisa](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="27385-218">Analytics</span><span class="sxs-lookup"><span data-stu-id="27385-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="27385-219">Linguagem de consulta poderosa</span><span class="sxs-lookup"><span data-stu-id="27385-219">Powerful query language</span></span> |![Exemplo de pesquisa](./media/app-insights-dashboards/63.png) |
