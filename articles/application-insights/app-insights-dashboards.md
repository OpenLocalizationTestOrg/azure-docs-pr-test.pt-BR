---
title: "aaaDashboards e navegação no hello Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="7d187-103">Painéis no portal do Application Insights hello e navegação</span><span class="sxs-lookup"><span data-stu-id="7d187-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="7d187-104">Depois de ter [configurar o Application Insights no seu projeto](app-insights-overview.md), dados de telemetria sobre desempenho e uso de seu aplicativo aparecerá no recurso do Application Insights do seu projeto no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d187-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="7d187-105">Encontrar sua telemetria</span><span class="sxs-lookup"><span data-stu-id="7d187-105">Find your telemetry</span></span>
<span data-ttu-id="7d187-106">Entrar toohello [portal do Azure](https://portal.azure.com) e navegue de recurso do Application Insights toohello que você criou para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d187-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Clique em Procurar, selecione Application Insights e seu aplicativo.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="7d187-108">folha de visão geral de saudação (página) para seu aplicativo mostra um resumo dos principais métricas diagnóstico saudação do seu aplicativo e é um gateway toohello outros recursos do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d187-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Principais rotas tooview sua Telemetria](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="7d187-110">Você pode personalizar qualquer um dos gráficos hello e grades e fixá-los tooa painel.</span><span class="sxs-lookup"><span data-stu-id="7d187-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="7d187-111">Dessa forma, você pode reunir telemetria chave Olá de aplicativos diferentes em um painel central.</span><span class="sxs-lookup"><span data-stu-id="7d187-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="7d187-112">Painéis</span><span class="sxs-lookup"><span data-stu-id="7d187-112">Dashboards</span></span>
<span data-ttu-id="7d187-113">Olá primeiro você ver depois que você entra no toohello [portal do Microsoft Azure](https://portal.azure.com) é um painel.</span><span class="sxs-lookup"><span data-stu-id="7d187-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="7d187-114">Aqui você pode reunir gráficos Olá que são mais importante tooyou em todos os seus recursos do Azure, incluindo a telemetria de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Um painel personalizado.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="7d187-116">**Navegue recursos toospecific** como seu aplicativo no Application Insights: barra à esquerda do uso hello.</span><span class="sxs-lookup"><span data-stu-id="7d187-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="7d187-117">**Painel atual retorno toohello**, ou alternar exibições recente tooother: Use Olá lista suspensa na parte superior esquerda.</span><span class="sxs-lookup"><span data-stu-id="7d187-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="7d187-118">**Alternar painéis**: Use Olá lista suspensa no título do painel Olá</span><span class="sxs-lookup"><span data-stu-id="7d187-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="7d187-119">**Criar, editar e compartilhar painéis** na barra de ferramentas do painel hello.</span><span class="sxs-lookup"><span data-stu-id="7d187-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="7d187-120">**Editar o painel Olá**: focalize um bloco e, em seguida, use a parte superior da barra toomove, personalizar ou removê-lo.</span><span class="sxs-lookup"><span data-stu-id="7d187-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="7d187-121">Adicionar painel tooa</span><span class="sxs-lookup"><span data-stu-id="7d187-121">Add tooa dashboard</span></span>
<span data-ttu-id="7d187-122">Quando você está procurando em uma folha ou conjunto de gráficos que é especialmente interessante, você pode fixar uma cópia desse painel toohello.</span><span class="sxs-lookup"><span data-stu-id="7d187-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="7d187-123">Você o verá da próxima vez que retornar.</span><span class="sxs-lookup"><span data-stu-id="7d187-123">You'll see it next time you return there.</span></span>

![toopin um gráfico, passe o mouse sobre ele e, em seguida, clique em "..." no cabeçalho de saudação.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="7d187-125">Fixar toodashboard do gráfico.</span><span class="sxs-lookup"><span data-stu-id="7d187-125">Pin chart toodashboard.</span></span> <span data-ttu-id="7d187-126">Uma cópia do gráfico de saudação aparece no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d187-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="7d187-127">PIN Olá folha inteira toohello painel - ele é exibido no painel de saudação como um bloco que você pode clicar.</span><span class="sxs-lookup"><span data-stu-id="7d187-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="7d187-128">Clique em Painel do canto superior esquerdo tooreturn toohello atual hello.</span><span class="sxs-lookup"><span data-stu-id="7d187-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="7d187-129">Em seguida, você pode usar o hello menu suspenso tooreturn toohello modo de exibição atual.</span><span class="sxs-lookup"><span data-stu-id="7d187-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="7d187-130">Observe que os gráficos são agrupados em blocos: um bloco pode conter mais de um gráfico.</span><span class="sxs-lookup"><span data-stu-id="7d187-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="7d187-131">Fixar o dashboard do hello bloco inteiro toohello.</span><span class="sxs-lookup"><span data-stu-id="7d187-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="7d187-132">gráfico de saudação é atualizado automaticamente com uma frequência que depende do intervalo de tempo do gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="7d187-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="7d187-133">Tempo de intervalo de hora too1: atualizar a cada 5 minutos</span><span class="sxs-lookup"><span data-stu-id="7d187-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="7d187-134">Intervalo de tempo de 1 a 24 horas: atualizar a cada 15 minutos</span><span class="sxs-lookup"><span data-stu-id="7d187-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="7d187-135">Intervalo de tempo acima de 24 horas: (intervalo de tempo)/60.</span><span class="sxs-lookup"><span data-stu-id="7d187-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="7d187-136">Fixar qualquer consulta no Analytics</span><span class="sxs-lookup"><span data-stu-id="7d187-136">Pin any query in Analytics</span></span>
<span data-ttu-id="7d187-137">Você também pode [fixar análise](app-insights-analytics-using.md#pin-to-dashboard) gráficos tooa [compartilhado](#share-dashboards-with-your-team) painel.</span><span class="sxs-lookup"><span data-stu-id="7d187-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="7d187-138">Isso permite que você tooadd gráficos de qualquer consulta arbitrário juntamente com métricas padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d187-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="7d187-139">Os resultados são automaticamente recalculados a cada hora.</span><span class="sxs-lookup"><span data-stu-id="7d187-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="7d187-140">Clique o ícone de atualização de Olá Olá gráfico toorecalculate imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7d187-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="7d187-141">(Atualizar do navegador não é recalculado.)</span><span class="sxs-lookup"><span data-stu-id="7d187-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="7d187-142">Ajustar um bloco no painel de saudação</span><span class="sxs-lookup"><span data-stu-id="7d187-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="7d187-143">Após um bloco no painel hello, você pode ajustá-lo.</span><span class="sxs-lookup"><span data-stu-id="7d187-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Passe o mouse sobre um gráfico em ordem tooedit-lo.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="7d187-145">Adicione um bloco de toohello do gráfico.</span><span class="sxs-lookup"><span data-stu-id="7d187-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="7d187-146">Definir a métrica hello, agrupar por dimensão e estilo (tabela, gráfico) de um gráfico.</span><span class="sxs-lookup"><span data-stu-id="7d187-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="7d187-147">Percorra Olá diagrama toozoom Clique em Olá desfazer botão tooreset Olá timespan; definir as propriedades de filtro de gráficos Olá no bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d187-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="7d187-148">Defina o título do bloco.</span><span class="sxs-lookup"><span data-stu-id="7d187-148">Set tile title.</span></span>

<span data-ttu-id="7d187-149">Blocos fixados de folhas do Metric Explorer têm mais opções de edição que aqueles fixados de uma folha de Visão Geral.</span><span class="sxs-lookup"><span data-stu-id="7d187-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="7d187-150">Olá original lado a lado que você fixou não é afetada por suas edições.</span><span class="sxs-lookup"><span data-stu-id="7d187-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="7d187-151">Alternar entre painéis</span><span class="sxs-lookup"><span data-stu-id="7d187-151">Switch between dashboards</span></span>
<span data-ttu-id="7d187-152">É possível salvar mais de um painel e alternar entre eles.</span><span class="sxs-lookup"><span data-stu-id="7d187-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="7d187-153">Quando você fixa um gráfico ou folha, elas são adicionadas toohello do painel atual.</span><span class="sxs-lookup"><span data-stu-id="7d187-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch entre os painéis, clique em Painel de controle e selecione um painel salvo.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="7d187-157">Por exemplo, você pode ter um painel de exibição de tela inteira na sala de equipe hello e outro para desenvolvimento geral.</span><span class="sxs-lookup"><span data-stu-id="7d187-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="7d187-158">No painel hello, uma folha é exibido como um bloco: clique em toogo toohello folha.</span><span class="sxs-lookup"><span data-stu-id="7d187-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="7d187-159">Um gráfico de replica gráfico Olá em seu local original.</span><span class="sxs-lookup"><span data-stu-id="7d187-159">A chart replicates hello chart in its original location.</span></span>

![Clique em uma folha de saudação do bloco tooopen representa](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="7d187-161">Compartilhar painéis</span><span class="sxs-lookup"><span data-stu-id="7d187-161">Share dashboards</span></span>
<span data-ttu-id="7d187-162">Quando você tiver criado um painel, poderá compartilhá-lo com outros usuários.</span><span class="sxs-lookup"><span data-stu-id="7d187-162">When you've created a dashboard, you can share it with other users.</span></span>

![No cabeçalho do painel de saudação, clique em compartilhamento](./media/app-insights-dashboards/41.png)

<span data-ttu-id="7d187-164">Saiba mais sobre [Funções e controle de acesso](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="7d187-165">Navegação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d187-165">App navigation</span></span>
<span data-ttu-id="7d187-166">folha de visão geral de saudação é Olá gateway toomore informações de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d187-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="7d187-167">**Qualquer bloco ou gráfico** - clique em qualquer bloco ou gráfico toosee mais detalhes sobre o que é exibido.</span><span class="sxs-lookup"><span data-stu-id="7d187-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="7d187-168">Botões da folha Visão geral</span><span class="sxs-lookup"><span data-stu-id="7d187-168">Overview blade buttons</span></span>
![Barra de navegação superior da folha Visão geral](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="7d187-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) -crie seus próprios gráficos de desempenho e de uso.</span><span class="sxs-lookup"><span data-stu-id="7d187-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="7d187-171">[**Pesquisa**](app-insights-diagnostic-search.md) - para investigar instâncias específicas de eventos, como solicitações, exceções ou log de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="7d187-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="7d187-172">[**Analytics**](app-insights-analytics.md) - consultas poderosas em sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="7d187-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="7d187-173">**Intervalo de tempo** -ajustar o intervalo de saudação exibido por todos os gráficos de saudação na folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d187-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="7d187-174">**Excluir** -excluir recurso do Application Insights Olá para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d187-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="7d187-175">Você deve também remover pacotes do Application Insights Olá do código do aplicativo, ou editar Olá [chave de instrumentação](app-insights-create-new-resource.md#copy-the-instrumentation-key) em seu recurso de Application Insights diferente de tooa do aplicativo toodirect telemetria.</span><span class="sxs-lookup"><span data-stu-id="7d187-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="7d187-176">Guia Conceitos Básicos</span><span class="sxs-lookup"><span data-stu-id="7d187-176">Essentials tab</span></span>
* <span data-ttu-id="7d187-177">[Chave de instrumentação](app-insights-create-new-resource.md#copy-the-instrumentation-key) -identifica esse recurso de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d187-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="7d187-178">Preço - disponibilize as funcionalidades disponíveis e defina volumes.</span><span class="sxs-lookup"><span data-stu-id="7d187-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="7d187-179">Barra de navegação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d187-179">App navigation bar</span></span>
![Barra de navegação à esquerda](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="7d187-181">**Visão geral do** -toohello retorno folha de visão geral do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d187-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="7d187-182">**Log de atividades** -alertas e eventos administrativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d187-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="7d187-183">[**Controle de acesso** ](app-insights-resources-roles-access-control.md) -fornecem membros de tooteam de acesso e outros.</span><span class="sxs-lookup"><span data-stu-id="7d187-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="7d187-184">[**Marcas** ](../azure-resource-manager/resource-group-using-tags.md) -Use marcas toogroup seu aplicativo com outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="7d187-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="7d187-185">INVESTIGAR</span><span class="sxs-lookup"><span data-stu-id="7d187-185">INVESTIGATE</span></span>

* <span data-ttu-id="7d187-186">[**Mapa de aplicativo** ](app-insights-app-map.md) -mapa ativo mostrando componentes de saudação do seu aplicativo, derivado de informações de dependência de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d187-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="7d187-187">[**Detecção Inteligente**](app-insights-proactive-diagnostics.md) - Examine os alertas de desempenho recentes.</span><span class="sxs-lookup"><span data-stu-id="7d187-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="7d187-188">[**Live Stream**](app-insights-live-stream.md) - um conjunto fixo de métricas quase instantâneas, úteis ao implantar um novo build ou depurar.</span><span class="sxs-lookup"><span data-stu-id="7d187-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="7d187-189">[**Disponibilidade / testes na Web** ](app-insights-monitor-web-app-availability.md) -enviar solicitações regular tooyour aplicativo web em torno de saudação world.*</span><span class="sxs-lookup"><span data-stu-id="7d187-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="7d187-190">[**Falhas e desempenho** ](app-insights-web-monitor-performance.md) -exceções, taxas de falha e resposta vezes para solicitações tooyour aplicativo e para solicitações de seu aplicativo muito[dependências](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="7d187-191">[**Desempenho**](app-insights-web-monitor-performance.md) - tempo de resposta, tempos de resposta de dependência.</span><span class="sxs-lookup"><span data-stu-id="7d187-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="7d187-192">[Servidores](app-insights-web-monitor-performance.md) - contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="7d187-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="7d187-193">Disponível se você [instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="7d187-194">**Navegador** - exibição de página e desempenho do AJAX.</span><span class="sxs-lookup"><span data-stu-id="7d187-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="7d187-195">Disponível se você [instrumentar suas páginas da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="7d187-196">**Uso** - contagens de sessão, usuário e exibição de página.</span><span class="sxs-lookup"><span data-stu-id="7d187-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="7d187-197">Disponível se você [instrumentar suas páginas da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="7d187-198">CONFIGURAR</span><span class="sxs-lookup"><span data-stu-id="7d187-198">CONFIGURE</span></span>

* <span data-ttu-id="7d187-199">**Introdução** - tutorial embutido.</span><span class="sxs-lookup"><span data-stu-id="7d187-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="7d187-200">**Propriedades** - chave de instrumentação, assinatura e ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="7d187-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="7d187-201">[Alertas](app-insights-alerts.md) - configuração do alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="7d187-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="7d187-202">[A exportação contínua](app-insights-export-telemetry.md) -configurar a exportação do armazenamento de tooAzure de telemetria.</span><span class="sxs-lookup"><span data-stu-id="7d187-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="7d187-203">[Teste de desempenho](app-insights-monitor-web-app-availability.md#performance-tests) - configure uma carga sintética no seu site.</span><span class="sxs-lookup"><span data-stu-id="7d187-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="7d187-204">[Cota e preço](app-insights-pricing.md) e [amostragem de ingestão](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="7d187-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="7d187-205">**Acesso à API** -criar [versão anotações](app-insights-annotations.md) e Olá API de acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="7d187-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="7d187-206">[**Itens de trabalho** ](app-insights-diagnostic-search.md#create-work-item) -conectar-se o trabalho tooa sistema de controle para que você possa criar bugs durante a inspeção de telemetria.</span><span class="sxs-lookup"><span data-stu-id="7d187-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="7d187-207">CONFIGURAÇÕES</span><span class="sxs-lookup"><span data-stu-id="7d187-207">SETTINGS</span></span>

* <span data-ttu-id="7d187-208">[**Bloqueios**](../azure-resource-manager/resource-group-lock-resources.md) - bloqueie recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="7d187-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="7d187-209">[**Script de automação** ](app-insights-powershell.md) -exportar uma definição de saudação recursos do Azure para que você pode usá-lo como um recurso novo do modelo toocreate.</span><span class="sxs-lookup"><span data-stu-id="7d187-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="7d187-210">Vídeo</span><span class="sxs-lookup"><span data-stu-id="7d187-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="7d187-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d187-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="7d187-212">Metrics explorer</span><span class="sxs-lookup"><span data-stu-id="7d187-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="7d187-213">Métricas de filtro e de segmento</span><span class="sxs-lookup"><span data-stu-id="7d187-213">Filter and segment metrics</span></span> |![Exemplo de pesquisa](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="7d187-215">Pesquisa de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="7d187-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="7d187-216">Localize e inspecione eventos, eventos relacionados e crie bugs</span><span class="sxs-lookup"><span data-stu-id="7d187-216">Find and inspect events, related events, and create bugs</span></span> |![Exemplo de pesquisa](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="7d187-218">Analytics</span><span class="sxs-lookup"><span data-stu-id="7d187-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="7d187-219">Linguagem de consulta poderosa</span><span class="sxs-lookup"><span data-stu-id="7d187-219">Powerful query language</span></span> |![Exemplo de pesquisa](./media/app-insights-dashboards/63.png) |
