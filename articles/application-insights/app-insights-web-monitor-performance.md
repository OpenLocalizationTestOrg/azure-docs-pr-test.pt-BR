---
title: aaaMonitor uso com o Application Insights e a integridade de seu aplicativo
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
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="04514-104">Monitore o desempenho em aplicativos da web</span><span class="sxs-lookup"><span data-stu-id="04514-104">Monitor performance in web applications</span></span>


<span data-ttu-id="04514-105">Certifique-se de que seu aplicativo está sendo bem executado, e saiba rapidamente sobre quaisquer falhas.</span><span class="sxs-lookup"><span data-stu-id="04514-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="04514-106">[Application Insights] [ start] será informam sobre quaisquer problemas de desempenho e exceções e causas raiz de ajudam você a localiza e diagnosticar hello.</span><span class="sxs-lookup"><span data-stu-id="04514-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="04514-107">O Application Insights pode monitorar serviços e aplicativos Web Java e ASP.NET e serviços WCF.</span><span class="sxs-lookup"><span data-stu-id="04514-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="04514-108">Eles podem ser hospedados localmente, em máquinas virtuais ou como sites do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="04514-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="04514-109">No lado do cliente hello, Application Insights pode levar a telemetria de páginas da web e uma ampla variedade de dispositivos, incluindo iOS, Android e aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="04514-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="04514-110">Disponibilizamos uma nova experiência para encontrar páginas de desempenho lento em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="04514-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="04514-111">Se você não tiver acesso tooit, habilitá-lo ao configurar as opções de visualização com hello [folha de visualização](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="04514-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="04514-112">Leia sobre essa nova experiência em [localizar e corrigir afunilamentos de desempenho com investigações de desempenho interativa Olá](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="04514-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="04514-113"><a name="setup"></a>Configurar o monitoramento de desempenho</span><span class="sxs-lookup"><span data-stu-id="04514-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="04514-114">Se você ainda não adicionou tooyour Application Insights (ou seja, se ele não tem applicationinsights. config) do projeto, escolha uma destas maneiras tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="04514-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="04514-115">Aplicativos Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="04514-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="04514-116">Adicionar monitoramento de exceção</span><span class="sxs-lookup"><span data-stu-id="04514-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="04514-117">Adicionar monitoramento de dependência</span><span class="sxs-lookup"><span data-stu-id="04514-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="04514-118">Aplicativos Web J2EE</span><span class="sxs-lookup"><span data-stu-id="04514-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="04514-119">Adicionar monitoramento de dependência</span><span class="sxs-lookup"><span data-stu-id="04514-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="04514-120"><a name="view"></a>Explorando métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="04514-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="04514-121">Em [Olá portal do Azure](https://portal.azure.com), procure o recurso do Application Insights toohello que você configurou para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04514-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="04514-122">folha de visão geral de saudação mostra dados de desempenho básicos:</span><span class="sxs-lookup"><span data-stu-id="04514-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="04514-123">Clique em qualquer toosee gráfico mais detalhes e os resultados de toosee por um período maior.</span><span class="sxs-lookup"><span data-stu-id="04514-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="04514-124">Por exemplo, clique em bloco de solicitações de saudação e, em seguida, selecione um intervalo de tempo:</span><span class="sxs-lookup"><span data-stu-id="04514-124">For example, click hello Requests tile and then select a time range:</span></span>

![Clicar em toomore dados e selecione um intervalo de tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="04514-126">Clique em um gráfico toochoose quais métricas ele exibe, ou adicionar um novo gráfico e selecione suas métricas:</span><span class="sxs-lookup"><span data-stu-id="04514-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Clique em métricas de toochoose um gráfico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="04514-128">**Desmarque todas as métricas de saudação** toosee Olá completo seleção disponível.</span><span class="sxs-lookup"><span data-stu-id="04514-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="04514-129">métricas de saudação se encaixam em grupos; Quando qualquer membro de um grupo é selecionado, somente hello outros membros do grupo aparecem.</span><span class="sxs-lookup"><span data-stu-id="04514-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="04514-130"><a name="metrics"></a>O que significa tudo isso?</span><span class="sxs-lookup"><span data-stu-id="04514-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="04514-131">Blocos e relatórios de desempenho</span><span class="sxs-lookup"><span data-stu-id="04514-131">Performance tiles and reports</span></span>
<span data-ttu-id="04514-132">Há várias métricas de desempenho que você pode obter.</span><span class="sxs-lookup"><span data-stu-id="04514-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="04514-133">Vamos começar com aqueles que aparecem por padrão na folha de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="04514-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="04514-134">Solicitações</span><span class="sxs-lookup"><span data-stu-id="04514-134">Requests</span></span>
<span data-ttu-id="04514-135">número de saudação de solicitações HTTP recebidas em um período especificado.</span><span class="sxs-lookup"><span data-stu-id="04514-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="04514-136">Compare isso com resultados de saudação em outros toosee relatórios como o seu aplicativo se comporta como carga de saudação varia.</span><span class="sxs-lookup"><span data-stu-id="04514-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="04514-137">As solicitações HTTP incluem todas as solicitações GET ou POST para páginas, dados e imagens.</span><span class="sxs-lookup"><span data-stu-id="04514-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="04514-138">Clique em Olá bloco tooget contagens de URLs específicas.</span><span class="sxs-lookup"><span data-stu-id="04514-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="04514-139">Tempo médio de resposta</span><span class="sxs-lookup"><span data-stu-id="04514-139">Average response time</span></span>
<span data-ttu-id="04514-140">Tempo de saudação de medidas entre uma solicitação da web inserir sua resposta de aplicativo e hello está sendo retornada.</span><span class="sxs-lookup"><span data-stu-id="04514-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="04514-141">pontos Olá mostram a movimentação de uma média.</span><span class="sxs-lookup"><span data-stu-id="04514-141">hello points show a moving average.</span></span> <span data-ttu-id="04514-142">Se houver muitas solicitações, pode haver alguns desvio da média de saudação sem um horário de pico óbvio ou ficarem no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="04514-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="04514-143">Procure por picos incomuns.</span><span class="sxs-lookup"><span data-stu-id="04514-143">Look for unusual peaks.</span></span> <span data-ttu-id="04514-144">Em geral, espera toorise de tempo de resposta com um aumento nas solicitações.</span><span class="sxs-lookup"><span data-stu-id="04514-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="04514-145">Se o aumento de saudação desproporcional, seu aplicativo pode ser atingir um limite de recursos, como a capacidade de CPU ou saudação de um serviço que ele usa.</span><span class="sxs-lookup"><span data-stu-id="04514-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="04514-146">Clique em tempos de tooget Olá lado a lado para URLs específicas.</span><span class="sxs-lookup"><span data-stu-id="04514-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="04514-147">Solicitações mais lentas</span><span class="sxs-lookup"><span data-stu-id="04514-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="04514-148">Mostra quais solicitações podem precisar de sintonização de desempenho.</span><span class="sxs-lookup"><span data-stu-id="04514-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="04514-149">Solicitações falhas</span><span class="sxs-lookup"><span data-stu-id="04514-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="04514-150">Uma contagem de solicitações que gerou exceções não capturadas.</span><span class="sxs-lookup"><span data-stu-id="04514-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="04514-151">Clique em Olá bloco toosee Olá detalhes de falhas específicas e selecione uma solicitação individual toosee seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="04514-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="04514-152">Somente uma amostra representativa de falhas é retida para inspeção individual.</span><span class="sxs-lookup"><span data-stu-id="04514-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="04514-153">Outras métricas</span><span class="sxs-lookup"><span data-stu-id="04514-153">Other metrics</span></span>
<span data-ttu-id="04514-154">toosee que outras métricas, você pode exibir, clique em um gráfico e, em seguida, desmarque Olá métricas toosee Olá completo disponível definidos.</span><span class="sxs-lookup"><span data-stu-id="04514-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="04514-155">Clique em (i) toosee definição de cada métrica.</span><span class="sxs-lookup"><span data-stu-id="04514-155">Click (i) toosee each metric's definition.</span></span>

![Desmarque todas as métricas toosee Olá todo o conjunto](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="04514-157">Outras pessoas que não pode aparecer em qualquer Olá métrica desabilita a seleção Olá mesmo gráfico.</span><span class="sxs-lookup"><span data-stu-id="04514-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="04514-158">Definir alertas</span><span class="sxs-lookup"><span data-stu-id="04514-158">Set alerts</span></span>
<span data-ttu-id="04514-159">toobe notificado por email sobre valores incomuns de alguma das métricas, adicionar um alerta.</span><span class="sxs-lookup"><span data-stu-id="04514-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="04514-160">Você pode escolher os administradores de contas toohello de email Olá toosend ou toospecific endereços de email.</span><span class="sxs-lookup"><span data-stu-id="04514-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="04514-161">Defina outras propriedades do recurso de saudação antes de saudação.</span><span class="sxs-lookup"><span data-stu-id="04514-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="04514-162">Não escolha a recursos de webtest Olá se você quiser tooset alertas em métricas de uso ou de desempenho.</span><span class="sxs-lookup"><span data-stu-id="04514-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="04514-163">Ser unidades de saudação toonote cuidado em que você for questionado tooenter valor de limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="04514-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="04514-164">*Não vejo o botão de alerta de adicionar hello.*</span><span class="sxs-lookup"><span data-stu-id="04514-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="04514-165">-Este é um toowhich de conta de grupo têm acesso somente leitura?</span><span class="sxs-lookup"><span data-stu-id="04514-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="04514-166">Verifique com o administrador da conta hello.</span><span class="sxs-lookup"><span data-stu-id="04514-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="04514-167"><a name="diagnosis"></a>Diagnosticando problemas</span><span class="sxs-lookup"><span data-stu-id="04514-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="04514-168">Aqui estão algumas dicas para localizar e diagnosticar problemas de desempenho:</span><span class="sxs-lookup"><span data-stu-id="04514-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="04514-169">Configurar [testes na web] [ availability] toobe alertado se seu site é desativado ou responde lentamente ou incorretamente.</span><span class="sxs-lookup"><span data-stu-id="04514-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="04514-170">Compare contagem de solicitações de saudação com outra métricas toosee se falhas ou resposta lenta tooload relacionado.</span><span class="sxs-lookup"><span data-stu-id="04514-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="04514-171">[Inserir e instruções de rastreamento de pesquisa] [ diagnostic] no seu código toohelp a identificar problemas.</span><span class="sxs-lookup"><span data-stu-id="04514-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="04514-172">Monitore seu aplicativo Web em operação com o [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="04514-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="04514-173">Capturar o estado de saudação do seu aplicativo .net com [instantâneo depurador][snapshot].</span><span class="sxs-lookup"><span data-stu-id="04514-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="04514-174">Encontrar e corrigir afunilamentos de desempenho com uma investigação de desempenho interativo</span><span class="sxs-lookup"><span data-stu-id="04514-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="04514-175">Você pode usar o hello novo Application Insights interativo investigação toolocate áreas de desempenho de seu aplicativo Web que estão prejudicando o desempenho geral.</span><span class="sxs-lookup"><span data-stu-id="04514-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="04514-176">Você pode rapidamente localizar páginas específicas que estão diminuindo e usam Olá [ferramenta de criação de perfil](app-insights-profiler.md) toosee se não houver uma correlação entre essas páginas.</span><span class="sxs-lookup"><span data-stu-id="04514-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="04514-177">Criar uma lista de páginas de desempenho lento</span><span class="sxs-lookup"><span data-stu-id="04514-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="04514-178">Olá primeira etapa para localizar problemas de desempenho é tooget uma lista de saudação lenta de páginas de responder.</span><span class="sxs-lookup"><span data-stu-id="04514-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="04514-179">Olá captura tela abaixo demonstra como usar o hello desempenho folha tooget uma lista de possíveis tooinvestigate páginas adicionais.</span><span class="sxs-lookup"><span data-stu-id="04514-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="04514-180">Você pode ver rapidamente nesta página que houve um retardar no tempo de resposta de saudação do aplicativo hello em cerca de 6:00 PM e novamente em aproximadamente 10 PM.</span><span class="sxs-lookup"><span data-stu-id="04514-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="04514-181">Você também pode ver que a operação de detalhes do cliente GET hello sofreu algum tempo executando operações com um tempo de resposta médio de 507.05 milissegundos.</span><span class="sxs-lookup"><span data-stu-id="04514-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Desempenho interativo do Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="04514-183">Fazer uma busca detalhada em páginas específicas</span><span class="sxs-lookup"><span data-stu-id="04514-183">Drill down on specific pages</span></span>

<span data-ttu-id="04514-184">Depois de obter um instantâneo do desempenho do aplicativo, você pode obter mais detalhes sobre operações específicas de desempenho lento.</span><span class="sxs-lookup"><span data-stu-id="04514-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="04514-185">Clique em qualquer operação em Olá lista toosee Olá detalhes conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="04514-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="04514-186">Gráfico de saudação você pode ver se o desempenho de saudação foi baseado em uma dependência.</span><span class="sxs-lookup"><span data-stu-id="04514-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="04514-187">Você também pode ver quantos Olá experientes de usuários vários tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="04514-187">You can also see how many users experienced hello various response times.</span></span> 

![Folha Operações do Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="04514-189">Fazer uma busca detalhada em um período específico</span><span class="sxs-lookup"><span data-stu-id="04514-189">Drill down on a specific time period</span></span>

<span data-ttu-id="04514-190">Depois de identificar um ponto no tempo tooinvestigate, aprofunde ainda mais toolook em operações específicas de saudação que possam ter causado retardar de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="04514-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="04514-191">Quando você clica em um ponto específico no tempo você obter detalhes de saudação da página Olá conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="04514-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="04514-192">No hello exemplo abaixo, você pode ver operações Olá listadas para um determinado período de tempo junto com os códigos de resposta do servidor de saudação e a duração da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="04514-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="04514-193">Você também tem Olá url para abrir um item de trabalho do TFS, se você precisar toosend essa equipe de desenvolvimento tooyour informações.</span><span class="sxs-lookup"><span data-stu-id="04514-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Fração de tempo do Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="04514-195">Fazer uma busca detalhada em uma operação específica</span><span class="sxs-lookup"><span data-stu-id="04514-195">Drill down on a specific operation</span></span>

<span data-ttu-id="04514-196">Depois de identificar um ponto no tempo tooinvestigate, aprofunde ainda mais toolook em operações específicas de saudação que possam ter causado retardar de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="04514-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="04514-197">Clique em uma operação de saudação listar toosee Olá detalhes da operação Olá conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="04514-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="04514-198">Neste exemplo, que você pode ver que falha na operação de saudação e do Application Insights fornece detalhes de saudação do hello aplicativo hello de exceção gerou.</span><span class="sxs-lookup"><span data-stu-id="04514-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="04514-199">Novamente, é possível criar um item de trabalho do TFS com facilidade nesta folha.</span><span class="sxs-lookup"><span data-stu-id="04514-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Folha Operação do Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="04514-201"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04514-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="04514-202">[Testes na Web] [ availability] -solicitações da web enviaram tooyour aplicativo em intervalos regulares do mundo hello.</span><span class="sxs-lookup"><span data-stu-id="04514-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="04514-203">[Capturar e pesquisar rastreamentos de diagnóstico] [ diagnostic] - inserir chamadas de rastreamento e examinar os problemas de toopinpoint Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="04514-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="04514-204">[Acompanhamento de uso][usage] – Saiba como as pessoas usam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04514-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="04514-205">[Solução de problemas][qna] – e P e R</span><span class="sxs-lookup"><span data-stu-id="04514-205">[Troubleshooting][qna] - and Q & A</span></span>



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



