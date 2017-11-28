---
title: aplicativos de Docker aaaMonitor no Azure Application Insights | Microsoft Docs
description: "Exceções, eventos e contadores de desempenho de docker podem ser exibidas no Application Insights, juntamente com telemetria de saudação de saudação em contêineres de aplicativos."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="ea32b-103">Monitorar aplicativos do Docker no Application Insights</span><span class="sxs-lookup"><span data-stu-id="ea32b-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="ea32b-104">Os eventos de ciclo de vida e os contadores de desempenho dos contêineres [Docker](https://www.docker.com/) podem ser representados em gráfico no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea32b-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="ea32b-105">Instalar Olá [Application Insights](app-insights-overview.md) imagem em um contêiner em seu host e ele exibirá contadores de desempenho para o host de saudação, bem como para Olá outras imagens.</span><span class="sxs-lookup"><span data-stu-id="ea32b-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="ea32b-106">Com o Docker, você distribui os aplicativos em contêineres leves com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="ea32b-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="ea32b-107">Eles serão executados em qualquer máquina host que executa um Mecanismo de Docker.</span><span class="sxs-lookup"><span data-stu-id="ea32b-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="ea32b-108">Quando você executa Olá [imagem Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) no host do Docker, você obtém esses benefícios:</span><span class="sxs-lookup"><span data-stu-id="ea32b-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="ea32b-109">Ciclo de vida telemetria sobre todos os contêineres de saudação em execução no host de saudação - Iniciar, parar e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="ea32b-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="ea32b-110">Contadores de desempenho para todos os contêineres de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea32b-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="ea32b-111">CPU, memória, uso da rede e muito mais.</span><span class="sxs-lookup"><span data-stu-id="ea32b-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="ea32b-112">Se você [instalado o SDK do Application Insights para Java](app-insights-java-live.md) em aplicativos de saudação em execução em contêineres hello, toda a telemetria Olá desses aplicativos terão propriedades adicionais que identifica o contêiner hello e o computador host.</span><span class="sxs-lookup"><span data-stu-id="ea32b-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="ea32b-113">Portanto, por exemplo, se você tiver instâncias de um aplicativo em execução em mais de um host, poderá filtrar a telemetria do aplicativo pelo host com facilidade.</span><span class="sxs-lookup"><span data-stu-id="ea32b-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![exemplo](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="ea32b-115">Configurar seu recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="ea32b-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="ea32b-116">Entrar no [portal do Microsoft Azure](https://azure.com) e abrir o recurso do Application Insights Olá para seu aplicativo; ou [criar um novo](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ea32b-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="ea32b-117">*Qual recurso devo usar?*</span><span class="sxs-lookup"><span data-stu-id="ea32b-117">*Which resource should I use?*</span></span> <span data-ttu-id="ea32b-118">Se Olá aplicativos em execução no host do foram desenvolvidos por outra pessoa, você precisará de muito[criar um novo recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ea32b-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="ea32b-119">Isso é onde você pode exibir e analisar a telemetria de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea32b-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="ea32b-120">(Selecione 'Geral' para o tipo de aplicativo hello.)</span><span class="sxs-lookup"><span data-stu-id="ea32b-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="ea32b-121">Mas se você for desenvolvedor Olá Olá aplicativos, em seguida, esperamos que você [adicionado SDK do Application Insights](app-insights-java-live.md) tooeach deles.</span><span class="sxs-lookup"><span data-stu-id="ea32b-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="ea32b-122">Se eles são todos os componentes realmente de um aplicativo de negócios único, em seguida, você pode configurar recursos de tooone telemetria toosend para todos eles, e você usará esses mesmo recurso toodisplay Olá Docker do ciclo de vida e dados de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ea32b-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="ea32b-123">Um terceiro cenário é que você desenvolveu a maioria dos aplicativos hello, mas você estiver usando recursos separados toodisplay sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="ea32b-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="ea32b-124">Nesse caso, você provavelmente também deseja toocreate um recurso separado para Olá dados Docker.</span><span class="sxs-lookup"><span data-stu-id="ea32b-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="ea32b-125">Adicionar bloco de Docker Olá: escolha **Adicionar bloco**, arraste o bloco de Docker de saudação da Galeria hello e, em seguida, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="ea32b-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![exemplo](./media/app-insights-docker/03.png)
3. <span data-ttu-id="ea32b-127">Clique em Olá **Essentials** suspenso e copie Olá chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="ea32b-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="ea32b-128">Use este Olá tootell SDK onde toosend sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="ea32b-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![exemplo](./media/app-insights-docker/02-props.png)

<span data-ttu-id="ea32b-130">Mantenha essa janela do navegador útil, pois você voltaremos tooit assim toolook em sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="ea32b-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="ea32b-131">Executar o monitor do Application Insights Olá em seu host</span><span class="sxs-lookup"><span data-stu-id="ea32b-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="ea32b-132">Agora que temos em algum lugar da telemetria do toodisplay Olá, você pode configurar o aplicativo em contêineres de saudação que coletará e enviá-lo.</span><span class="sxs-lookup"><span data-stu-id="ea32b-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="ea32b-133">Conecte-se o host do Docker tooyour.</span><span class="sxs-lookup"><span data-stu-id="ea32b-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="ea32b-134">Edite a chave de instrumentação nesse comando e, em seguida, execute-a:</span><span class="sxs-lookup"><span data-stu-id="ea32b-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="ea32b-135">Apenas uma imagem do Application Insights é necessária por host do Docker.</span><span class="sxs-lookup"><span data-stu-id="ea32b-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="ea32b-136">Se seu aplicativo for implantado em vários hosts de Docker, em seguida, repita o comando de saudação em cada host.</span><span class="sxs-lookup"><span data-stu-id="ea32b-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="ea32b-137">Atualizar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ea32b-137">Update your app</span></span>
<span data-ttu-id="ea32b-138">Se seu aplicativo está instrumentado com hello [SDK do Application Insights para Java](app-insights-java-get-started.md), adicionar Olá a seguinte linha no arquivo de ApplicationInsights.xml Olá no seu projeto, em Olá `<TelemetryInitializers>` elemento:</span><span class="sxs-lookup"><span data-stu-id="ea32b-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="ea32b-139">Isso adiciona informações de Docker como contêiner host id tooevery telemetria item e enviado de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea32b-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="ea32b-140">Exibir sua telemetria</span><span class="sxs-lookup"><span data-stu-id="ea32b-140">View your telemetry</span></span>
<span data-ttu-id="ea32b-141">Volte tooyour recurso Application Insights Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea32b-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="ea32b-142">Clique em bloco de Docker hello.</span><span class="sxs-lookup"><span data-stu-id="ea32b-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="ea32b-143">Em breve você verá dados chegando do aplicativo de Docker hello, especialmente se você tiver outros contêineres em execução no seu mecanismo do Docker.</span><span class="sxs-lookup"><span data-stu-id="ea32b-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="ea32b-144">Aqui estão algumas das exibições de saudação, que você pode obter.</span><span class="sxs-lookup"><span data-stu-id="ea32b-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="ea32b-145">Contadores de desempenho por host, atividade por imagem</span><span class="sxs-lookup"><span data-stu-id="ea32b-145">Perf counters by host, activity by image</span></span>
![exemplo](./media/app-insights-docker/10.png)

![exemplo](./media/app-insights-docker/11.png)

<span data-ttu-id="ea32b-148">Clique em qualquer nome de imagem ou host para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ea32b-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="ea32b-149">modo de exibição toocustomize hello, clique em qualquer gráfico, a grade de saudação do título ou use Adicionar gráfico.</span><span class="sxs-lookup"><span data-stu-id="ea32b-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="ea32b-150">[Saiba mais sobre o Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="ea32b-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="ea32b-151">Eventos de contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="ea32b-151">Docker container events</span></span>
![exemplo](./media/app-insights-docker/13.png)

<span data-ttu-id="ea32b-153">eventos individuais de tooinvestigate, clique em [pesquisa](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="ea32b-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="ea32b-154">Pesquisar e filtrar toofind Olá eventos que você deseja.</span><span class="sxs-lookup"><span data-stu-id="ea32b-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="ea32b-155">Clique em qualquer evento tooget mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ea32b-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="ea32b-156">Exceções por nome do contêiner</span><span class="sxs-lookup"><span data-stu-id="ea32b-156">Exceptions by container name</span></span>
![exemplo](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="ea32b-158">O contexto de docker adicionado tooapp Telemetria</span><span class="sxs-lookup"><span data-stu-id="ea32b-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="ea32b-159">Telemetria de solicitação enviada do aplicativo hello instrumentado com o SDK do AI, aprimorada com o contexto do Docker:</span><span class="sxs-lookup"><span data-stu-id="ea32b-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![exemplo](./media/app-insights-docker/16.png)

<span data-ttu-id="ea32b-161">Tempo do processador e contadores de desempenho de memória disponíveis, aprimorados e agrupados por nome de contêiner do Docker:</span><span class="sxs-lookup"><span data-stu-id="ea32b-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![exemplo](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="ea32b-163">Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="ea32b-163">Q & A</span></span>
<span data-ttu-id="ea32b-164">*O que o Application Insights me proporciona que eu não consigo obter com o Docker?*</span><span class="sxs-lookup"><span data-stu-id="ea32b-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="ea32b-165">Análise detalhada dos contadores de desempenho por contêiner e imagem.</span><span class="sxs-lookup"><span data-stu-id="ea32b-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="ea32b-166">Integração dos dados de contêiner e do aplicativo em um painel.</span><span class="sxs-lookup"><span data-stu-id="ea32b-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="ea32b-167">[Exportar telemetria](app-insights-export-telemetry.md) para o banco de dados de tooa análise adicional, o Power BI ou outro painel.</span><span class="sxs-lookup"><span data-stu-id="ea32b-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="ea32b-168">*Como obter telemetria de aplicativo hello em si?*</span><span class="sxs-lookup"><span data-stu-id="ea32b-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="ea32b-169">Instale Olá SDK do Application Insights no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ea32b-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="ea32b-170">Saiba mais para: [aplicativos Web Java](app-insights-java-get-started.md), [aplicativos Web Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ea32b-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="ea32b-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="ea32b-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="ea32b-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea32b-172">Next steps</span></span>

* [<span data-ttu-id="ea32b-173">Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="ea32b-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="ea32b-174">Application Insights para Node.js</span><span class="sxs-lookup"><span data-stu-id="ea32b-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="ea32b-175">Application Insights para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ea32b-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
