---
title: aaaDependency controle no Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="ee10b-103">Configurar o Application Insights: acompanhamento de dependências</span><span class="sxs-lookup"><span data-stu-id="ee10b-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="ee10b-104">Um *dependência* é um componente externo que é chamado por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee10b-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="ee10b-105">Normalmente, ele é um serviço chamado usando HTTP, um banco de dados ou um sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ee10b-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="ee10b-106">O [Application Insights](app-insights-overview.md) mede por quanto tempo o aplicativo aguarda dependências e com que frequência uma chamada de dependência falha.</span><span class="sxs-lookup"><span data-stu-id="ee10b-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="ee10b-107">Você pode investigar chamadas específicas e relacioná-los toorequests e exceções.</span><span class="sxs-lookup"><span data-stu-id="ee10b-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![gráficos de exemplo](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="ee10b-109">monitor de dependência de caixa Olá atualmente relata chamadas toothese tipos de dependências:</span><span class="sxs-lookup"><span data-stu-id="ee10b-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="ee10b-110">Servidor</span><span class="sxs-lookup"><span data-stu-id="ee10b-110">Server</span></span>
  * <span data-ttu-id="ee10b-111">Bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ee10b-111">SQL databases</span></span>
  * <span data-ttu-id="ee10b-112">Serviços Web ASP.NET e WCF que usam associações baseadas em HTTP</span><span class="sxs-lookup"><span data-stu-id="ee10b-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="ee10b-113">Chamadas HTTP locais ou remotas</span><span class="sxs-lookup"><span data-stu-id="ee10b-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="ee10b-114">Azure Cosmos DB, tabela, Armazenamento de Blobs e fila</span><span class="sxs-lookup"><span data-stu-id="ee10b-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="ee10b-115">Páginas da Web</span><span class="sxs-lookup"><span data-stu-id="ee10b-115">Web pages</span></span>
  * <span data-ttu-id="ee10b-116">Chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="ee10b-116">AJAX calls</span></span>

<span data-ttu-id="ee10b-117">O monitoramento funciona com o uso da [instrumentação de código de byte](https://msdn.microsoft.com/library/z9z62c29.aspx) nos métodos selecionados.</span><span class="sxs-lookup"><span data-stu-id="ee10b-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="ee10b-118">A sobrecarga de desempenho é mínima.</span><span class="sxs-lookup"><span data-stu-id="ee10b-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="ee10b-119">Você também pode escrever seu próprios SDK chamadas toomonitor outras dependências, ambos no código de cliente e servidor hello, usando Olá [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="ee10b-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="ee10b-120">Configurar o monitoramento de dependência</span><span class="sxs-lookup"><span data-stu-id="ee10b-120">Set up dependency monitoring</span></span>
<span data-ttu-id="ee10b-121">Informações de dependência parcial são coletadas automaticamente pelo Olá [SDK do Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ee10b-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="ee10b-122">tooget completa dos dados, instale o agente de apropriada de Olá para o servidor de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee10b-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="ee10b-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="ee10b-123">Platform</span></span> | <span data-ttu-id="ee10b-124">Instalar</span><span class="sxs-lookup"><span data-stu-id="ee10b-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="ee10b-125">Servidor IIS</span><span class="sxs-lookup"><span data-stu-id="ee10b-125">IIS Server</span></span> |<span data-ttu-id="ee10b-126">O [instalar o Monitor de Status em seu servidor](app-insights-monitor-performance-live-website-now.md) ou [atualizar a estrutura de too.NET aplicativo 4.6 ou posterior](http://go.microsoft.com/fwlink/?LinkId=528259) e instalar Olá [SDK do Application Insights](app-insights-asp-net.md) em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee10b-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="ee10b-127">Aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="ee10b-127">Azure Web App</span></span> |<span data-ttu-id="ee10b-128">No painel de controle de aplicativo web, [folha do Application Insights Olá aberto no painel de controle de aplicativo web](app-insights-azure-web-apps.md) e escolha a instalação se solicitado.</span><span class="sxs-lookup"><span data-stu-id="ee10b-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="ee10b-129">Serviço de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="ee10b-129">Azure Cloud Service</span></span> |<span data-ttu-id="ee10b-130">[Usar tarefa de inicialização](app-insights-cloudservices.md) ou [Instalar o .NET Framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="ee10b-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="ee10b-131">Onde os dados de dependência de toofind</span><span class="sxs-lookup"><span data-stu-id="ee10b-131">Where toofind dependency data</span></span>
* <span data-ttu-id="ee10b-132">O [Mapa de Aplicativo](#application-map) visualiza as dependências entre seu aplicativo e os componentes de vizinhança.</span><span class="sxs-lookup"><span data-stu-id="ee10b-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="ee10b-133">As [folhas de desempenho, de navegador e de falha](#performance-and-blades) mostram dados de dependência de servidor.</span><span class="sxs-lookup"><span data-stu-id="ee10b-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="ee10b-134">A [folha de navegadores](#ajax-calls) mostra chamadas AJAX de navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="ee10b-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="ee10b-135">[Clique em por meio de solicitações com falha ou lentas](#diagnose-slow-requests) toocheck sua dependência chama.</span><span class="sxs-lookup"><span data-stu-id="ee10b-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="ee10b-136">[Análise de](#analytics) pode ser usado tooquery dados de dependência.</span><span class="sxs-lookup"><span data-stu-id="ee10b-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="ee10b-137">Mapa de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee10b-137">Application Map</span></span>
<span data-ttu-id="ee10b-138">Mapa de aplicativo atua como um toodiscovering de auxílio visual dependências entre componentes de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee10b-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="ee10b-139">Ele é gerado automaticamente da telemetria de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee10b-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="ee10b-140">Este exemplo mostra chamadas AJAX de scripts de navegador hello e chamadas REST do servidor de saudação serviços externos de tootwo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee10b-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Mapa de aplicativo](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="ee10b-142">**Navegue nas caixas Olá** toorelevant dependência e outros gráficos.</span><span class="sxs-lookup"><span data-stu-id="ee10b-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="ee10b-143">**Mapa de saudação do PIN** toohello [painel](app-insights-dashboards.md), onde ele será totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="ee10b-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="ee10b-144">[Saiba mais](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="ee10b-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="ee10b-145">Folhas de falha e de desempenho</span><span class="sxs-lookup"><span data-stu-id="ee10b-145">Performance and failure blades</span></span>
<span data-ttu-id="ee10b-146">folha de desempenho Olá mostra a duração de saudação de chamadas de dependência feitas pelo aplicativo do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee10b-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="ee10b-147">Há um gráfico de resumo e uma tabela segmentadas por chamada.</span><span class="sxs-lookup"><span data-stu-id="ee10b-147">There's a summary chart and a table segmented by call.</span></span>

![Gráficos de dependência de folha de desempenho](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="ee10b-149">Clique nos gráficos de resumo de saudação ou Olá tabela itens toosearch bruto ocorrências dessas chamadas.</span><span class="sxs-lookup"><span data-stu-id="ee10b-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Instâncias de chamada de dependência](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="ee10b-151">**Contagens de falha** são mostrados em Olá **falhas** folha.</span><span class="sxs-lookup"><span data-stu-id="ee10b-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="ee10b-152">Uma falha é qualquer código de retorno não está no intervalo de saudação 200-399, ou desconhecido.</span><span class="sxs-lookup"><span data-stu-id="ee10b-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="ee10b-153">**Falhas de 100%?**</span><span class="sxs-lookup"><span data-stu-id="ee10b-153">**100% failures?**</span></span> <span data-ttu-id="ee10b-154">- Isso provavelmente indica que você está apenas obtendo dados de dependência parcial.</span><span class="sxs-lookup"><span data-stu-id="ee10b-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="ee10b-155">É necessário muito[configurar dependência monitoramento plataforma apropriada tooyour](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="ee10b-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="ee10b-156">Chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="ee10b-156">AJAX Calls</span></span>
<span data-ttu-id="ee10b-157">folha de navegadores Olá mostra a duração de saudação e taxa de falha de AJAX chama de [JavaScript nas páginas da web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ee10b-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="ee10b-158">Elas são mostradas como Dependências.</span><span class="sxs-lookup"><span data-stu-id="ee10b-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="ee10b-159"><a name="diagnosis"></a> Diagnosticar solicitações lentas</span><span class="sxs-lookup"><span data-stu-id="ee10b-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="ee10b-160">Cada evento de solicitação associado com chamadas de dependência hello, Olá exceções e outros eventos que são rastreados enquanto seu aplicativo está processando a solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee10b-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="ee10b-161">Portanto, se algumas solicitações são com baixo desempenho, você pode descobrir se ela é devido as respostas tooslow uma dependência.</span><span class="sxs-lookup"><span data-stu-id="ee10b-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="ee10b-162">Vamos examinar um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="ee10b-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="ee10b-163">Rastreamento de solicitações toodependencies</span><span class="sxs-lookup"><span data-stu-id="ee10b-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="ee10b-164">Abra a folha de desempenho de saudação e examine a grade de saudação de solicitações:</span><span class="sxs-lookup"><span data-stu-id="ee10b-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Lista de solicitações com contagens e médias](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="ee10b-166">superior Olá um está demorando muito.</span><span class="sxs-lookup"><span data-stu-id="ee10b-166">hello top one is taking very long.</span></span> <span data-ttu-id="ee10b-167">Vamos ver se podemos pode descobrir onde o tempo de saudação é gasto.</span><span class="sxs-lookup"><span data-stu-id="ee10b-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="ee10b-168">Clique em eventos de solicitação individual de toosee essa linha:</span><span class="sxs-lookup"><span data-stu-id="ee10b-168">Click that row toosee individual request events:</span></span>

![Lista de ocorrências de solicitação](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="ee10b-170">Clique em qualquer tooinspect de instância de execução longa ainda mais e role para baixo toohello dependência remoto chamadas relacionadas toothis solicitação:</span><span class="sxs-lookup"><span data-stu-id="ee10b-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Localizar chamadas tooRemote dependências, identifique a duração incomuns](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="ee10b-172">Parece que a maioria das Olá tempo atendendo a que essa solicitação foi gasta em um serviço local de tooa de chamada.</span><span class="sxs-lookup"><span data-stu-id="ee10b-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="ee10b-173">Selecione essa linha tooget obter mais informações:</span><span class="sxs-lookup"><span data-stu-id="ee10b-173">Select that row tooget more information:</span></span>

![Clique nas que responsável de saudação tooidentify dependência remoto](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="ee10b-175">Parece que este é onde está o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee10b-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="ee10b-176">Nós já é identificar o problema de saudação, portanto agora simplesmente necessário toofind out por essa chamada está demorando muito tempo.</span><span class="sxs-lookup"><span data-stu-id="ee10b-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="ee10b-177">Linha do tempo da solicitação</span><span class="sxs-lookup"><span data-stu-id="ee10b-177">Request timeline</span></span>
<span data-ttu-id="ee10b-178">Em outro caso, não há nenhuma chamada de dependência que seja tão longa.</span><span class="sxs-lookup"><span data-stu-id="ee10b-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="ee10b-179">Mas, alternando o modo de exibição de tempo de toohello, podemos ver onde o atraso de saudação ocorreu no nosso processamento interno:</span><span class="sxs-lookup"><span data-stu-id="ee10b-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Localizar chamadas tooRemote dependências, identifique a duração incomuns](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="ee10b-181">Parece toobe uma grande diferença após a primeira chamada de dependência hello, portanto deve observarmos nossa toosee código por que isto é.</span><span class="sxs-lookup"><span data-stu-id="ee10b-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="ee10b-182">Perfil de seu site ativo</span><span class="sxs-lookup"><span data-stu-id="ee10b-182">Profile your live site</span></span>

<span data-ttu-id="ee10b-183">Não sabe onde o tempo de saudação vai? Olá [criador de perfil do Application Insights](app-insights-profiler.md) rastreamentos HTTP chama o site ao vivo tooyour e mostra quais funções em seu código levaram tempo mais longo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee10b-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="ee10b-184">Solicitações falhas</span><span class="sxs-lookup"><span data-stu-id="ee10b-184">Failed requests</span></span>
<span data-ttu-id="ee10b-185">Solicitações com falha também podem ser associadas com toodependencies de chamadas com falha.</span><span class="sxs-lookup"><span data-stu-id="ee10b-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="ee10b-186">Novamente, estamos pode clicar tootrack problema hello.</span><span class="sxs-lookup"><span data-stu-id="ee10b-186">Again, we can click through tootrack down hello problem.</span></span>

![Clique em gráfico de solicitações com falha Olá](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="ee10b-188">Clique nas tooan ocorrência de uma solicitação com falha e examinar seus eventos associados.</span><span class="sxs-lookup"><span data-stu-id="ee10b-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Clique em um tipo de solicitação, clique em Olá instância tooget tooa exibição diferente dos Olá a mesma instância, clique em detalhes da exceção tooget.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="ee10b-190">Análise</span><span class="sxs-lookup"><span data-stu-id="ee10b-190">Analytics</span></span>
<span data-ttu-id="ee10b-191">Você pode rastrear dependências em Olá [linguagem de consulta de análise de Log](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="ee10b-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="ee10b-192">Veja alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="ee10b-192">Here are some examples.</span></span>

* <span data-ttu-id="ee10b-193">Localize todas as chamadas com falha de dependência:</span><span class="sxs-lookup"><span data-stu-id="ee10b-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="ee10b-194">Localize as chamadas AJAX:</span><span class="sxs-lookup"><span data-stu-id="ee10b-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="ee10b-195">Localize as chamadas de dependência associadas a solicitações:</span><span class="sxs-lookup"><span data-stu-id="ee10b-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="ee10b-196">Localize as chamadas do AJAX associadas a exibições de página:</span><span class="sxs-lookup"><span data-stu-id="ee10b-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="ee10b-197">Acompanhamento de dependência personalizado</span><span class="sxs-lookup"><span data-stu-id="ee10b-197">Custom dependency tracking</span></span>
<span data-ttu-id="ee10b-198">módulo de controle de dependência padrão Olá descobre automaticamente as dependências externas, como bancos de dados e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="ee10b-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="ee10b-199">Mas talvez você queira toobe alguns componentes adicionais tratado no hello mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="ee10b-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="ee10b-200">Você pode escrever código que envia informações de dependência usando Olá mesmo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) que é usado pelos módulos de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="ee10b-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="ee10b-201">Por exemplo, se você compilar seu código com um assembly que não gravar por conta própria, você poderia tempo tooit de chamadas Olá todos os, toofind out que contribuição faz resposta tooyour vezes.</span><span class="sxs-lookup"><span data-stu-id="ee10b-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="ee10b-202">toohave esses dados exibidos em gráficos de dependência Olá no Application Insights, enviá-lo usando `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="ee10b-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="ee10b-203">Se você quiser tooswitch fora do módulo de controle de dependência padrão hello, remover Olá referência tooDependencyTrackingTelemetryModule em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="ee10b-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ee10b-204">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ee10b-204">Troubleshooting</span></span>
<span data-ttu-id="ee10b-205">*O sinalizador de êxito da dependência sempre mostra true ou false.*</span><span class="sxs-lookup"><span data-stu-id="ee10b-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="ee10b-206">*Consulta SQL não mostrada por completo.*</span><span class="sxs-lookup"><span data-stu-id="ee10b-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="ee10b-207">Atualize a versão mais recente toohello de saudação SDK.</span><span class="sxs-lookup"><span data-stu-id="ee10b-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="ee10b-208">Se sua versão do .NET for inferior à 4.6:</span><span class="sxs-lookup"><span data-stu-id="ee10b-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="ee10b-209">Host de IIS: instalar [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) nos servidores de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee10b-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="ee10b-210">Aplicativo web do Azure: Abra Application Insights guia no painel de controle de aplicativo de web hello e instale o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ee10b-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="ee10b-211">Vídeo</span><span class="sxs-lookup"><span data-stu-id="ee10b-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="ee10b-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee10b-212">Next steps</span></span>
* [<span data-ttu-id="ee10b-213">Exceções</span><span class="sxs-lookup"><span data-stu-id="ee10b-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="ee10b-214">Dados do usuário e da página</span><span class="sxs-lookup"><span data-stu-id="ee10b-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="ee10b-215">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ee10b-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
