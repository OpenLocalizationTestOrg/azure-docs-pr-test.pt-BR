---
title: "Acompanhamento de dependência no Azure Application Insights | Microsoft Docs"
description: Analise o uso, disponibilidade e desempenho de seu local ou um aplicativo Web do Microsoft Azure com o Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="ad8bb-103">Configurar o Application Insights: acompanhamento de dependências</span><span class="sxs-lookup"><span data-stu-id="ad8bb-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="ad8bb-104">Um *dependência* é um componente externo que é chamado por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="ad8bb-105">Normalmente, ele é um serviço chamado usando HTTP, um banco de dados ou um sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="ad8bb-106">O [Application Insights](app-insights-overview.md) mede por quanto tempo o aplicativo aguarda dependências e com que frequência uma chamada de dependência falha.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="ad8bb-107">Você pode investigar chamadas específicas e relacioná-las a solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![gráficos de exemplo](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="ad8bb-109">O monitor de dependência pronto para uso atualmente relata chamadas para esses tipos de dependências:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="ad8bb-110">Servidor</span><span class="sxs-lookup"><span data-stu-id="ad8bb-110">Server</span></span>
  * <span data-ttu-id="ad8bb-111">Bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ad8bb-111">SQL databases</span></span>
  * <span data-ttu-id="ad8bb-112">Serviços Web ASP.NET e WCF que usam associações baseadas em HTTP</span><span class="sxs-lookup"><span data-stu-id="ad8bb-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="ad8bb-113">Chamadas HTTP locais ou remotas</span><span class="sxs-lookup"><span data-stu-id="ad8bb-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="ad8bb-114">Azure Cosmos DB, tabela, Armazenamento de Blobs e fila</span><span class="sxs-lookup"><span data-stu-id="ad8bb-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="ad8bb-115">Páginas da Web</span><span class="sxs-lookup"><span data-stu-id="ad8bb-115">Web pages</span></span>
  * <span data-ttu-id="ad8bb-116">Chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="ad8bb-116">AJAX calls</span></span>

<span data-ttu-id="ad8bb-117">O monitoramento funciona com o uso da [instrumentação de código de byte](https://msdn.microsoft.com/library/z9z62c29.aspx) nos métodos selecionados.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="ad8bb-118">A sobrecarga de desempenho é mínima.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="ad8bb-119">Você também pode escrever suas próprias chamadas SDK para monitorar outras dependências, no código do cliente e servidor, usando o [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="ad8bb-120">Configurar o monitoramento de dependência</span><span class="sxs-lookup"><span data-stu-id="ad8bb-120">Set up dependency monitoring</span></span>
<span data-ttu-id="ad8bb-121">As informações de dependência parciais são coletadas automaticamente pelo [SDK do Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="ad8bb-122">Para obter dados completos, instale o agente apropriado para o servidor host.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="ad8bb-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="ad8bb-123">Platform</span></span> | <span data-ttu-id="ad8bb-124">Instalar</span><span class="sxs-lookup"><span data-stu-id="ad8bb-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="ad8bb-125">Servidor IIS</span><span class="sxs-lookup"><span data-stu-id="ad8bb-125">IIS Server</span></span> |<span data-ttu-id="ad8bb-126">Você pode [instalar o Status Monitor no servidor](app-insights-monitor-performance-live-website-now.md) ou [atualizar o aplicativo para .NET Framework 4.6 ou posterior](http://go.microsoft.com/fwlink/?LinkId=528259) e instalar o [SDK do Application Insights](app-insights-asp-net.md) no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="ad8bb-127">Aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="ad8bb-127">Azure Web App</span></span> |<span data-ttu-id="ad8bb-128">No painel de controle do aplicativo Web, [abra a folha do Application Insights no seu painel de controle do aplicativo Web](app-insights-azure-web-apps.md) e escolha Instalar, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="ad8bb-129">Serviço de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="ad8bb-129">Azure Cloud Service</span></span> |<span data-ttu-id="ad8bb-130">[Usar tarefa de inicialização](app-insights-cloudservices.md) ou [Instalar o .NET Framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="ad8bb-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="ad8bb-131">Onde encontrar dados de dependência</span><span class="sxs-lookup"><span data-stu-id="ad8bb-131">Where to find dependency data</span></span>
* <span data-ttu-id="ad8bb-132">O [Mapa de Aplicativo](#application-map) visualiza as dependências entre seu aplicativo e os componentes de vizinhança.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="ad8bb-133">As [folhas de desempenho, de navegador e de falha](#performance-and-blades) mostram dados de dependência de servidor.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="ad8bb-134">A [folha de navegadores](#ajax-calls) mostra chamadas AJAX de navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="ad8bb-135">[Clickthrough de solicitações com falha ou lentas](#diagnose-slow-requests) para verificar a dependência de chamadas.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="ad8bb-136">O [Analytics](#analytics) pode ser usado para consultar dados de dependência.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="ad8bb-137">Mapa de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ad8bb-137">Application Map</span></span>
<span data-ttu-id="ad8bb-138">O Mapa de aplicativo atua como uma ajuda visual para descobrir dependências entre os componentes do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="ad8bb-139">Ele é gerado automaticamente da telemetria do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="ad8bb-140">Este exemplo mostra chamadas AJAX de scripts de navegador e chamadas REST do aplicativo de servidor para os dois serviços externos.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Mapa de aplicativo](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="ad8bb-142">**Navegue das caixas** até a dependência relevante e outros gráficos.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="ad8bb-143">**Fixe o mapa** no [painel](app-insights-dashboards.md), onde ele ficará totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="ad8bb-144">[Saiba mais](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="ad8bb-145">Folhas de falha e de desempenho</span><span class="sxs-lookup"><span data-stu-id="ad8bb-145">Performance and failure blades</span></span>
<span data-ttu-id="ad8bb-146">A folha de desempenho mostra a duração das chamadas de dependência feitas pelo aplicativo de servidor.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="ad8bb-147">Há um gráfico de resumo e uma tabela segmentadas por chamada.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-147">There's a summary chart and a table segmented by call.</span></span>

![Gráficos de dependência de folha de desempenho](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="ad8bb-149">Clickthrough nos gráficos de resumo ou os itens de tabela para pesquisar ocorrências brutas dessas chamadas.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Instâncias de chamada de dependência](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="ad8bb-151">As **contagens de falhas** são mostrados na folha **Falhas**.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="ad8bb-152">Uma falha é qualquer código de retorno que não esteja no intervalo 200-399, ou que seja desconhecido.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="ad8bb-153">**Falhas de 100%?**</span><span class="sxs-lookup"><span data-stu-id="ad8bb-153">**100% failures?**</span></span> <span data-ttu-id="ad8bb-154">- Isso provavelmente indica que você está apenas obtendo dados de dependência parcial.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="ad8bb-155">Você precisa [configurar o monitoramento de dependência apropriado para sua plataforma](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="ad8bb-156">Chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="ad8bb-156">AJAX Calls</span></span>
<span data-ttu-id="ad8bb-157">A folha Navegadores mostra a taxa de falha e a duração de chamadas AJAX de [JavaScript nas páginas da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="ad8bb-158">Elas são mostradas como Dependências.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="ad8bb-159"><a name="diagnosis"></a> Diagnosticar solicitações lentas</span><span class="sxs-lookup"><span data-stu-id="ad8bb-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="ad8bb-160">Cada evento de solicitação está associado às chamadas de dependência, exceções e outros eventos que são rastreados enquanto seu aplicativo está processando a solicitação.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="ad8bb-161">Então se algumas solicitações são com baixo desempenho, você pode descobrir seja devido à lentidão nas respostas de uma dependência.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="ad8bb-162">Vamos examinar um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="ad8bb-163">Rastreamento de solicitações de dependências</span><span class="sxs-lookup"><span data-stu-id="ad8bb-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="ad8bb-164">Abra a folha Desempenho e examine a grade de solicitações:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Lista de solicitações com contagens e médias](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="ad8bb-166">A solicitação superior está demorando muito.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-166">The top one is taking very long.</span></span> <span data-ttu-id="ad8bb-167">Vamos ver se conseguimos descobrir onde o tempo é gasto.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="ad8bb-168">Clique nesta linha para ver os eventos de solicitação individuais:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-168">Click that row to see individual request events:</span></span>

![Lista de ocorrências de solicitação](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="ad8bb-170">Clique em qualquer instância de execução longa para inspecioná-la ainda mais e role para baixo até as chamadas de dependência remotas relacionadas a essa solicitação:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Localizar as chamadas para dependências remotas, identificar duração incomum](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="ad8bb-172">Parece a maior parte do tempo atendendo a solicitação foi gasto em uma chamada para um serviço local.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="ad8bb-173">Selecione a linha para obter mais informações:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-173">Select that row to get more information:</span></span>

![Clique nessa dependência remota para identificar o culpado](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="ad8bb-175">Parece que o problema está aí.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="ad8bb-176">Nós já identificamos o problema, então agora simplesmente precisamos descobrir por que essa chamada está demorando tanto.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="ad8bb-177">Linha do tempo da solicitação</span><span class="sxs-lookup"><span data-stu-id="ad8bb-177">Request timeline</span></span>
<span data-ttu-id="ad8bb-178">Em outro caso, não há nenhuma chamada de dependência que seja tão longa.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="ad8bb-179">Mas, ao alternar para o modo de exibição de linha do tempo, podemos ver onde está o atraso durante nosso processamento interno:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Localizar as chamadas para dependências remotas, identificar duração incomum](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="ad8bb-181">Parece haver uma grande lacuna após a primeira chamada de dependência e, portanto, devemos examinar nosso código para ver o motivo disso.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="ad8bb-182">Perfil de seu site ativo</span><span class="sxs-lookup"><span data-stu-id="ad8bb-182">Profile your live site</span></span>

<span data-ttu-id="ad8bb-183">Não sabe para onde o tempo vai?</span><span class="sxs-lookup"><span data-stu-id="ad8bb-183">No idea where the time goes?</span></span> <span data-ttu-id="ad8bb-184">O [Application Insights Profiler](app-insights-profiler.md) rastreia chamadas HTTP para seu site ativo e mostra quais são as funções mais demoradas em seu código.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="ad8bb-185">Solicitações falhas</span><span class="sxs-lookup"><span data-stu-id="ad8bb-185">Failed requests</span></span>
<span data-ttu-id="ad8bb-186">As solicitações com falha também podem ser associadas a chamadas com falha para as dependências.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="ad8bb-187">Novamente, podemos fazer um clickthrough para rastrear o problema.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-187">Again, we can click through to track down the problem.</span></span>

![Clique no gráfico de solicitações com falha](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="ad8bb-189">Clique para uma ocorrência de uma solicitação com falha e examine os eventos associados.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Clique em um tipo de solicitação e na instância para obter uma exibição diferente da mesma instância, clique nele para obter detalhes da exceção.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="ad8bb-191">Análise</span><span class="sxs-lookup"><span data-stu-id="ad8bb-191">Analytics</span></span>
<span data-ttu-id="ad8bb-192">Você pode rastrear dependências na [linguagem de consulta do Log Analytics](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="ad8bb-193">Veja alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-193">Here are some examples.</span></span>

* <span data-ttu-id="ad8bb-194">Localize todas as chamadas com falha de dependência:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="ad8bb-195">Localize as chamadas AJAX:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="ad8bb-196">Localize as chamadas de dependência associadas a solicitações:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="ad8bb-197">Localize as chamadas do AJAX associadas a exibições de página:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="ad8bb-198">Acompanhamento de dependência personalizado</span><span class="sxs-lookup"><span data-stu-id="ad8bb-198">Custom dependency tracking</span></span>
<span data-ttu-id="ad8bb-199">O módulo padrão de acompanhamento de dependência descobre automaticamente dependências externas, como bancos de dados e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="ad8bb-200">Mas, talvez você queira que alguns componentes adicionais sejam tratados da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="ad8bb-201">Você pode escrever código que envia informações de dependência usando a mesma [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency) usada pelos módulos padrão.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="ad8bb-202">Por exemplo, se você criar seu código com um assembly que não escreveu, poderá determinar o tempo de todas as chamadas nele, para descobrir qual sua contribuição aos tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="ad8bb-203">Para que esses dados sejam exibidos nos gráficos de dependência no Application Insights, envie-os usando `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

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

<span data-ttu-id="ad8bb-204">Se desejar desativar o módulo padrão de acompanhamento de dependência, remova a referência para DependencyTrackingTelemetryModule em [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="ad8bb-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ad8bb-205">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ad8bb-205">Troubleshooting</span></span>
<span data-ttu-id="ad8bb-206">*O sinalizador de êxito da dependência sempre mostra true ou false.*</span><span class="sxs-lookup"><span data-stu-id="ad8bb-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="ad8bb-207">*Consulta SQL não mostrada por completo.*</span><span class="sxs-lookup"><span data-stu-id="ad8bb-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="ad8bb-208">Atualize para a versão mais recente do SDK.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="ad8bb-209">Se sua versão do .NET for inferior à 4.6:</span><span class="sxs-lookup"><span data-stu-id="ad8bb-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="ad8bb-210">Host IIS: instale o [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) nos servidores de host.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="ad8bb-211">Aplicativo Web do Azure: abra a guia Application Insights no painel de controle do aplicativo Web e instale o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ad8bb-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="ad8bb-212">Vídeo</span><span class="sxs-lookup"><span data-stu-id="ad8bb-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="ad8bb-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad8bb-213">Next steps</span></span>
* [<span data-ttu-id="ad8bb-214">Exceções</span><span class="sxs-lookup"><span data-stu-id="ad8bb-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="ad8bb-215">Dados do usuário e da página</span><span class="sxs-lookup"><span data-stu-id="ad8bb-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="ad8bb-216">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ad8bb-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
