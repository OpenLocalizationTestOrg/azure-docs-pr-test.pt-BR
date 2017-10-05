---
title: Monitorar a integridade e o uso do aplicativo com o Application Insights
description: "Introdução ao Application Insights. Analise o uso, disponibilidade e desempenho de seu local ou aplicativos do Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="df48d-104">Monitore o desempenho em aplicativos da web</span><span class="sxs-lookup"><span data-stu-id="df48d-104">Monitor performance in web applications</span></span>


<span data-ttu-id="df48d-105">Certifique-se de que seu aplicativo está sendo bem executado, e saiba rapidamente sobre quaisquer falhas.</span><span class="sxs-lookup"><span data-stu-id="df48d-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="df48d-106">O [Application Insights][start] lhe informará sobre quaisquer problemas de desempenho e exceções e lhe ajudará a localizar e diagnosticar as causas raiz.</span><span class="sxs-lookup"><span data-stu-id="df48d-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="df48d-107">O Application Insights pode monitorar serviços e aplicativos Web Java e ASP.NET e serviços WCF.</span><span class="sxs-lookup"><span data-stu-id="df48d-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="df48d-108">Eles podem ser hospedados localmente, em máquinas virtuais ou como sites do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="df48d-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="df48d-109">No lado do cliente, o Application Insights pode realizar a telemetria de páginas da Web e de uma grande variedade de dispositivos, incluindo iOS, Android e aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="df48d-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="df48d-110">Disponibilizamos uma nova experiência para encontrar páginas de desempenho lento em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="df48d-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="df48d-111">Caso você não tenha acesso a ela, habilite-a configurando as opções de versão prévia na [folha Versão Prévia](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="df48d-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="df48d-112">Leia mais sobre essa nova experiência em [Encontrar e corrigir afunilamentos de desempenho com a investigação de Desempenho interativo](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="df48d-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="df48d-113"><a name="setup"></a>Configurar o monitoramento de desempenho</span><span class="sxs-lookup"><span data-stu-id="df48d-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="df48d-114">Se você ainda não tem o Application Insights adicionado ao seu projeto (ou seja, não tem o ApplicationInsights.config), escolha uma destas formas para começar:</span><span class="sxs-lookup"><span data-stu-id="df48d-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="df48d-115">Aplicativos Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="df48d-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="df48d-116">Adicionar monitoramento de exceção</span><span class="sxs-lookup"><span data-stu-id="df48d-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="df48d-117">Adicionar monitoramento de dependência</span><span class="sxs-lookup"><span data-stu-id="df48d-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="df48d-118">Aplicativos Web J2EE</span><span class="sxs-lookup"><span data-stu-id="df48d-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="df48d-119">Adicionar monitoramento de dependência</span><span class="sxs-lookup"><span data-stu-id="df48d-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="df48d-120"><a name="view"></a>Explorando métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="df48d-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="df48d-121">No [portal do Azure](https://portal.azure.com), navegue até o recurso do Application Insights que você configurou para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df48d-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="df48d-122">A folha de visão geral mostra os dados de desempenho básicos:</span><span class="sxs-lookup"><span data-stu-id="df48d-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="df48d-123">Clique em qualquer gráfico para ver mais detalhes e para ver os resultados por um período mais longo.</span><span class="sxs-lookup"><span data-stu-id="df48d-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="df48d-124">Por exemplo, clique no bloco Solicitações e, em seguida, selecione um intervalo de tempo:</span><span class="sxs-lookup"><span data-stu-id="df48d-124">For example, click the Requests tile and then select a time range:</span></span>

![Clique por mais dados e selecione um intervalo de tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="df48d-126">Clique em um gráfico para selecionar outras medidas que são exibidas, ou adicionar um novo gráfico e selecionar a métrica:</span><span class="sxs-lookup"><span data-stu-id="df48d-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Clique em um gráfico para escolher métricas](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="df48d-128">**Desmarque todas as métricas** para ver a seleção completa que está disponível.</span><span class="sxs-lookup"><span data-stu-id="df48d-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="df48d-129">As métricas se enquadram em grupos; quando qualquer membro de um grupo é selecionado, somente os outros membros do grupo aparecem.</span><span class="sxs-lookup"><span data-stu-id="df48d-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="df48d-130"><a name="metrics"></a>O que significa tudo isso?</span><span class="sxs-lookup"><span data-stu-id="df48d-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="df48d-131">Blocos e relatórios de desempenho</span><span class="sxs-lookup"><span data-stu-id="df48d-131">Performance tiles and reports</span></span>
<span data-ttu-id="df48d-132">Há várias métricas de desempenho que você pode obter.</span><span class="sxs-lookup"><span data-stu-id="df48d-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="df48d-133">Vamos começar com estas que aparecem por padrão na folha do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df48d-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="df48d-134">Solicitações</span><span class="sxs-lookup"><span data-stu-id="df48d-134">Requests</span></span>
<span data-ttu-id="df48d-135">O número de solicitações de HTTP receberam em um período especifico.</span><span class="sxs-lookup"><span data-stu-id="df48d-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="df48d-136">Compare isso com os resultados em outros reatórios para ver como seu aplicativo se comporta conforme a carga varia.</span><span class="sxs-lookup"><span data-stu-id="df48d-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="df48d-137">As solicitações HTTP incluem todas as solicitações GET ou POST para páginas, dados e imagens.</span><span class="sxs-lookup"><span data-stu-id="df48d-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="df48d-138">Clique no mosaico para obter contagens para URLs específicas.</span><span class="sxs-lookup"><span data-stu-id="df48d-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="df48d-139">Tempo de resposta média</span><span class="sxs-lookup"><span data-stu-id="df48d-139">Average response time</span></span>
<span data-ttu-id="df48d-140">Mede o tempo entre uma solicitação da web inserindo seu aplicativo e a resposta que está sendo devolvida.</span><span class="sxs-lookup"><span data-stu-id="df48d-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="df48d-141">Os pontos mostram uma média da movimentação.</span><span class="sxs-lookup"><span data-stu-id="df48d-141">The points show a moving average.</span></span> <span data-ttu-id="df48d-142">Se existe várias solicitações, pode haver agumas que desviam da média sem um pico óbvio ou profundo no gráfico.</span><span class="sxs-lookup"><span data-stu-id="df48d-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="df48d-143">Procure por picos incomuns.</span><span class="sxs-lookup"><span data-stu-id="df48d-143">Look for unusual peaks.</span></span> <span data-ttu-id="df48d-144">Em geral, espere o tempo de resposta para eevar com uma elevação nas solicitações.</span><span class="sxs-lookup"><span data-stu-id="df48d-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="df48d-145">Se a elevação é desproporcional, seu aplicativo pode ser atingido por um limite de recurso como CPU ou a capacidade de um serviço que usa.</span><span class="sxs-lookup"><span data-stu-id="df48d-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="df48d-146">Clique no bloco para obter tempos para URLs específicas.</span><span class="sxs-lookup"><span data-stu-id="df48d-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="df48d-147">Solicitações mais lentas</span><span class="sxs-lookup"><span data-stu-id="df48d-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="df48d-148">Mostra quais solicitações podem precisar de sintonização de desempenho.</span><span class="sxs-lookup"><span data-stu-id="df48d-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="df48d-149">Solicitações falhas</span><span class="sxs-lookup"><span data-stu-id="df48d-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="df48d-150">Uma contagem de solicitações que gerou exceções não capturadas.</span><span class="sxs-lookup"><span data-stu-id="df48d-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="df48d-151">Clique no mosaico para ver os detalhes de falhas específicas, e selecione uma solicitação individual para ver seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="df48d-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="df48d-152">Somente uma amostra representativa de falhas é retida para inspeção individual.</span><span class="sxs-lookup"><span data-stu-id="df48d-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="df48d-153">Outras métricas</span><span class="sxs-lookup"><span data-stu-id="df48d-153">Other metrics</span></span>
<span data-ttu-id="df48d-154">Para ver o que outras métricas que você pode exibir, clique em um gráfico e, em seguida, desmarque a seleção de todas as métricas para ver o conjunto disponível completo.</span><span class="sxs-lookup"><span data-stu-id="df48d-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="df48d-155">Clique em (i) para ver cada definição da métrica.</span><span class="sxs-lookup"><span data-stu-id="df48d-155">Click (i) to see each metric's definition.</span></span>

![Desmarque a seleção de todas as métricas para ver o conjunto completo](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="df48d-157">Selecionar uma métrica desabilitará as outras que não podem ser exibidas no mesmo gráfico.</span><span class="sxs-lookup"><span data-stu-id="df48d-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="df48d-158">Definir alertas</span><span class="sxs-lookup"><span data-stu-id="df48d-158">Set alerts</span></span>
<span data-ttu-id="df48d-159">Para ser notificado por email sobre valores incomuns de qualquer métrica, adicione um alerta.</span><span class="sxs-lookup"><span data-stu-id="df48d-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="df48d-160">Você pode escolher para enviar o email para os administradores de conta ou para endereços de email específicos.</span><span class="sxs-lookup"><span data-stu-id="df48d-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="df48d-161">Defina o recurso antes de outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="df48d-161">Set the resource before the other properties.</span></span> <span data-ttu-id="df48d-162">Não escolha os recursos webtest se você quer definir alertas em métricas de desempenho ou de uso.</span><span class="sxs-lookup"><span data-stu-id="df48d-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="df48d-163">Observe as unidades quando você for solicitado para inserir o valor de limite.</span><span class="sxs-lookup"><span data-stu-id="df48d-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="df48d-164">*Não vejo o botão Adicionar Alerta.*</span><span class="sxs-lookup"><span data-stu-id="df48d-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="df48d-165">- Esta é uma conta de grupo para a qual você tem acesso somente leitura?</span><span class="sxs-lookup"><span data-stu-id="df48d-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="df48d-166">Verifique com o administrador da conta.</span><span class="sxs-lookup"><span data-stu-id="df48d-166">Check with the account administrator.</span></span>

## <span data-ttu-id="df48d-167"><a name="diagnosis"></a>Diagnosticando problemas</span><span class="sxs-lookup"><span data-stu-id="df48d-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="df48d-168">Aqui estão algumas dicas para localizar e diagnosticar problemas de desempenho:</span><span class="sxs-lookup"><span data-stu-id="df48d-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="df48d-169">Configure os [testes da Web][availability] para serem alertados se seu site cair ou responder de forma incorreta ou lenta.</span><span class="sxs-lookup"><span data-stu-id="df48d-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="df48d-170">Compare a contagem de Solicitação com outras métricas para ver se falhas ou resposta lenta são relatadas ao carregar.</span><span class="sxs-lookup"><span data-stu-id="df48d-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="df48d-171">[Inserir e pesquisar instruções de rastreamento][diagnostic] em seu código para ajudar a detectar problemas.</span><span class="sxs-lookup"><span data-stu-id="df48d-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="df48d-172">Monitore seu aplicativo Web em operação com o [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="df48d-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="df48d-173">Capture o estado do aplicativo .Net com o [Depurador de Instantâneo][snapshot].</span><span class="sxs-lookup"><span data-stu-id="df48d-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="df48d-174">Encontrar e corrigir afunilamentos de desempenho com uma investigação de desempenho interativo</span><span class="sxs-lookup"><span data-stu-id="df48d-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="df48d-175">Use a nova investigação de desempenho interativo do Application Insights para localizar áreas de seu aplicativo Web que estão causando lentidão no desempenho geral.</span><span class="sxs-lookup"><span data-stu-id="df48d-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="df48d-176">Encontre rapidamente páginas específicas que estão causando lentidão e, em seguida, use a [ferramenta de Criação de Perfil](app-insights-profiler.md) para ver se há uma correlação entre essas páginas.</span><span class="sxs-lookup"><span data-stu-id="df48d-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="df48d-177">Criar uma lista de páginas de desempenho lento</span><span class="sxs-lookup"><span data-stu-id="df48d-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="df48d-178">A primeira etapa para encontrar problemas de desempenho é obter uma lista das páginas de resposta lenta.</span><span class="sxs-lookup"><span data-stu-id="df48d-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="df48d-179">A captura de tela abaixo demonstra como usar a folha Desempenho para obter uma lista de possíveis páginas para investigação adicional.</span><span class="sxs-lookup"><span data-stu-id="df48d-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="df48d-180">Você pode ver rapidamente nesta página que houve uma lentidão no tempo de resposta do aplicativo por volta das 18h e novamente por volta das 22h.</span><span class="sxs-lookup"><span data-stu-id="df48d-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="df48d-181">Você também pode ver que a operação GET de cliente/detalhes teve algumas operações de execução longa, com um tempo de resposta mediano de 507,05 milissegundos.</span><span class="sxs-lookup"><span data-stu-id="df48d-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Desempenho interativo do Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="df48d-183">Fazer uma busca detalhada em páginas específicas</span><span class="sxs-lookup"><span data-stu-id="df48d-183">Drill down on specific pages</span></span>

<span data-ttu-id="df48d-184">Depois de obter um instantâneo do desempenho do aplicativo, você pode obter mais detalhes sobre operações específicas de desempenho lento.</span><span class="sxs-lookup"><span data-stu-id="df48d-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="df48d-185">Clique em uma operação da lista para ver os detalhes, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="df48d-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="df48d-186">No gráfico, você pode ver se o desempenho se baseava em uma dependência.</span><span class="sxs-lookup"><span data-stu-id="df48d-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="df48d-187">Veja também quantos usuários observaram os vários tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="df48d-187">You can also see how many users experienced the various response times.</span></span> 

![Folha Operações do Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="df48d-189">Fazer uma busca detalhada em um período específico</span><span class="sxs-lookup"><span data-stu-id="df48d-189">Drill down on a specific time period</span></span>

<span data-ttu-id="df48d-190">Depois de identificar um ponto no tempo para investigar, faça uma busca detalhada para examinar as operações específicas que podem ter causado a lentidão do desempenho.</span><span class="sxs-lookup"><span data-stu-id="df48d-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="df48d-191">Ao clicar em um ponto no tempo específico, você obtém os detalhes da página, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="df48d-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="df48d-192">No exemplo abaixo, você pode ver as operações listadas para determinado período, junto com os códigos de resposta do servidor e a duração da operação.</span><span class="sxs-lookup"><span data-stu-id="df48d-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="df48d-193">Você também tem a URL para abrir um item de trabalho do TFS, caso precise enviar essas informações para sua equipe de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="df48d-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Fração de tempo do Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="df48d-195">Fazer uma busca detalhada em uma operação específica</span><span class="sxs-lookup"><span data-stu-id="df48d-195">Drill down on a specific operation</span></span>

<span data-ttu-id="df48d-196">Depois de identificar um ponto no tempo para investigar, faça uma busca detalhada para examinar as operações específicas que podem ter causado a lentidão do desempenho.</span><span class="sxs-lookup"><span data-stu-id="df48d-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="df48d-197">Clique em uma operação da lista para ver os detalhes da operação, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="df48d-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="df48d-198">Neste exemplo, você pode ver que a operação falhou e que o Application Insights forneceu os detalhes da exceção gerada pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df48d-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="df48d-199">Novamente, é possível criar um item de trabalho do TFS com facilidade nesta folha.</span><span class="sxs-lookup"><span data-stu-id="df48d-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Folha Operação do Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="df48d-201"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df48d-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="df48d-202">[Testes da Web][availability] – faça com que solicitações da Web sejam enviadas ao seu aplicativo em intervalos regulares de todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="df48d-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="df48d-203">[Capturar e pesquisar rastreamento de diagnóstico][diagnostic] – Inserir chamadas de rastreamento e separar através dos resultados para problemas de pinpoint.</span><span class="sxs-lookup"><span data-stu-id="df48d-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="df48d-204">[Acompanhamento de uso][usage] – Saiba como as pessoas usam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df48d-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="df48d-205">[Solução de problemas][qna] – e P e R</span><span class="sxs-lookup"><span data-stu-id="df48d-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



