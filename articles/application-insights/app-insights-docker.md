---
title: Monitorar aplicativos do Docker no Azure Application Insights | Microsoft Docs
description: "Contadores de desempenho, eventos e exceções do Docker podem ser exibidos no Application Insights, juntamente com a telemetria dos aplicativos contidos."
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="0b57b-103">Monitorar aplicativos do Docker no Application Insights</span><span class="sxs-lookup"><span data-stu-id="0b57b-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="0b57b-104">Os eventos de ciclo de vida e os contadores de desempenho dos contêineres [Docker](https://www.docker.com/) podem ser representados em gráfico no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b57b-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="0b57b-105">Instale a imagem [Application Insights](app-insights-overview.md) em um contêiner em seu host e ele exibirá os contadores de desempenho para o host, bem como para outras imagens.</span><span class="sxs-lookup"><span data-stu-id="0b57b-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="0b57b-106">Com o Docker, você distribui os aplicativos em contêineres leves com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="0b57b-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="0b57b-107">Eles serão executados em qualquer máquina host que executa um Mecanismo de Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="0b57b-108">Ao executar a [imagem do Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) no host do Docker, você obtém estes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0b57b-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="0b57b-109">A telemetria do ciclo de vida sobre todos os contêineres em execução no host - início, parada e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0b57b-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="0b57b-110">Contadores de desempenho para todos os contêineres.</span><span class="sxs-lookup"><span data-stu-id="0b57b-110">Performance counters for all the containers.</span></span> <span data-ttu-id="0b57b-111">CPU, memória, uso da rede e muito mais.</span><span class="sxs-lookup"><span data-stu-id="0b57b-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="0b57b-112">Se você [instalou o SDK do Application Insights para Java](app-insights-java-live.md) nos aplicativos em execução nos contêineres, toda a telemetria desses aplicativos terá propriedades adicionais que identificam o contêiner e o computador host.</span><span class="sxs-lookup"><span data-stu-id="0b57b-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="0b57b-113">Portanto, por exemplo, se você tiver instâncias de um aplicativo em execução em mais de um host, poderá filtrar a telemetria do aplicativo pelo host com facilidade.</span><span class="sxs-lookup"><span data-stu-id="0b57b-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![exemplo](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="0b57b-115">Configurar seu recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="0b57b-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="0b57b-116">Entre no [portal do Microsoft Azure](https://azure.com) e abra o recurso do Application Insights de seu aplicativo ou [crie um novo](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0b57b-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="0b57b-117">*Qual recurso devo usar?*</span><span class="sxs-lookup"><span data-stu-id="0b57b-117">*Which resource should I use?*</span></span> <span data-ttu-id="0b57b-118">Se os aplicativos que estão em execução no host foram desenvolvidos por outra pessoa, você precisa [criar um novo recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0b57b-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="0b57b-119">Esse é o local em que você pode exibir e analisar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="0b57b-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="0b57b-120">(Selecione 'Geral' para o tipo de aplicativo.)</span><span class="sxs-lookup"><span data-stu-id="0b57b-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="0b57b-121">Mas se você for o desenvolvedor dos aplicativos, esperamos que você tenha [adicionado o SDK do Application Insights](app-insights-java-live.md) a cada um deles.</span><span class="sxs-lookup"><span data-stu-id="0b57b-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="0b57b-122">Se eles forem realmente todos os componentes de um único aplicativo de negócios, você poderá configurar todos eles para enviar a telemetria para um recurso e usará esse mesmo recurso para exibir os dados de desempenho e do ciclo de vida do Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="0b57b-123">Um terceiro cenário é que você desenvolveu a maioria dos aplicativos, mas está usando recursos separados para exibir a telemetria deles.</span><span class="sxs-lookup"><span data-stu-id="0b57b-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="0b57b-124">Nesse caso, provavelmente, você também desejará criar um recurso separado para os dados do Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="0b57b-125">Adicione o bloco Docker: escolha **Adicionar Bloco**, arraste o bloco Docker a partir da galeria, em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="0b57b-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![exemplo](./media/app-insights-docker/03.png)
3. <span data-ttu-id="0b57b-127">Clique no menu suspenso **Informações gerais** e copie a Chave de Instrumentação.</span><span class="sxs-lookup"><span data-stu-id="0b57b-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="0b57b-128">Você usará isso para informar ao SDK o local em que sua telemetria será enviada.</span><span class="sxs-lookup"><span data-stu-id="0b57b-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![exemplo](./media/app-insights-docker/02-props.png)

<span data-ttu-id="0b57b-130">Mantenha essa janela do navegador à mão, pois você voltará a ele em breve para examinar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="0b57b-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="0b57b-131">Executar o monitor do Application Insights em seu host</span><span class="sxs-lookup"><span data-stu-id="0b57b-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="0b57b-132">Agora que você tem algum lugar para exibir a telemetria, configure o aplicativo contido que a coletará e enviará.</span><span class="sxs-lookup"><span data-stu-id="0b57b-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="0b57b-133">Conecte-se ao seu host do Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="0b57b-134">Edite a chave de instrumentação nesse comando e, em seguida, execute-a:</span><span class="sxs-lookup"><span data-stu-id="0b57b-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="0b57b-135">Apenas uma imagem do Application Insights é necessária por host do Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="0b57b-136">Se o seu aplicativo for implantado em vários hosts do Docker, repita o comando em todos os hosts.</span><span class="sxs-lookup"><span data-stu-id="0b57b-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="0b57b-137">Atualizar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="0b57b-137">Update your app</span></span>
<span data-ttu-id="0b57b-138">Se seu aplicativo for instrumentado com o [SDK do Application Insights para Java](app-insights-java-get-started.md), adicione a seguinte linha ao arquivo ApplicationInsights.xml em seu projeto, sob o elemento `<TelemetryInitializers>`:</span><span class="sxs-lookup"><span data-stu-id="0b57b-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="0b57b-139">Isso adiciona informações do Docker, como o contêiner e a ID de host, a cada item de telemetria enviado do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b57b-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="0b57b-140">Exibir sua telemetria</span><span class="sxs-lookup"><span data-stu-id="0b57b-140">View your telemetry</span></span>
<span data-ttu-id="0b57b-141">Volte ao recurso do Application Insights no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b57b-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="0b57b-142">Clique por meio do bloco do Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-142">Click through the Docker tile.</span></span>

<span data-ttu-id="0b57b-143">Em breve, você verá os dados recebidos do aplicativo do Docker, especialmente se tiver outros contêineres em execução em seu mecanismo do Docker.</span><span class="sxs-lookup"><span data-stu-id="0b57b-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="0b57b-144">Estas são algumas das exibições que você pode obter.</span><span class="sxs-lookup"><span data-stu-id="0b57b-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="0b57b-145">Contadores de desempenho por host, atividade por imagem</span><span class="sxs-lookup"><span data-stu-id="0b57b-145">Perf counters by host, activity by image</span></span>
![exemplo](./media/app-insights-docker/10.png)

![exemplo](./media/app-insights-docker/11.png)

<span data-ttu-id="0b57b-148">Clique em qualquer nome de imagem ou host para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0b57b-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="0b57b-149">Para personalizar o modo de exibição, clique em qualquer gráfico, no título da grade ou use Adicionar Gráfico.</span><span class="sxs-lookup"><span data-stu-id="0b57b-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="0b57b-150">[Saiba mais sobre o Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="0b57b-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="0b57b-151">Eventos de contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="0b57b-151">Docker container events</span></span>
![exemplo](./media/app-insights-docker/13.png)

<span data-ttu-id="0b57b-153">Para investigar os eventos individuais, clique em [Pesquisar](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="0b57b-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="0b57b-154">Pesquise e filtre para localizar os eventos desejados.</span><span class="sxs-lookup"><span data-stu-id="0b57b-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="0b57b-155">Clique em qualquer evento para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0b57b-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="0b57b-156">Exceções por nome do contêiner</span><span class="sxs-lookup"><span data-stu-id="0b57b-156">Exceptions by container name</span></span>
![exemplo](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="0b57b-158">Contexto do Docker adicionado à telemetria do aplicativo</span><span class="sxs-lookup"><span data-stu-id="0b57b-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="0b57b-159">Telemetria da solicitação enviada do aplicativo instrumentado com o SDK do AI, aprimorada com o contexto do Docker:</span><span class="sxs-lookup"><span data-stu-id="0b57b-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![exemplo](./media/app-insights-docker/16.png)

<span data-ttu-id="0b57b-161">Tempo do processador e contadores de desempenho de memória disponíveis, aprimorados e agrupados por nome de contêiner do Docker:</span><span class="sxs-lookup"><span data-stu-id="0b57b-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![exemplo](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="0b57b-163">Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="0b57b-163">Q & A</span></span>
<span data-ttu-id="0b57b-164">*O que o Application Insights me proporciona que eu não consigo obter com o Docker?*</span><span class="sxs-lookup"><span data-stu-id="0b57b-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="0b57b-165">Análise detalhada dos contadores de desempenho por contêiner e imagem.</span><span class="sxs-lookup"><span data-stu-id="0b57b-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="0b57b-166">Integração dos dados de contêiner e do aplicativo em um painel.</span><span class="sxs-lookup"><span data-stu-id="0b57b-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="0b57b-167">[Exporte a telemetria](app-insights-export-telemetry.md) para uma análise adicional em um banco de dados, no Power BI ou em outro painel.</span><span class="sxs-lookup"><span data-stu-id="0b57b-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="0b57b-168">*Como posso obter a telemetria do próprio aplicativo?*</span><span class="sxs-lookup"><span data-stu-id="0b57b-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="0b57b-169">Instale o SDK do Application Insights no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b57b-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="0b57b-170">Saiba mais para: [aplicativos Web Java](app-insights-java-get-started.md), [aplicativos Web Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="0b57b-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="0b57b-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0b57b-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="0b57b-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b57b-172">Next steps</span></span>

* [<span data-ttu-id="0b57b-173">Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="0b57b-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="0b57b-174">Application Insights para Node.js</span><span class="sxs-lookup"><span data-stu-id="0b57b-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="0b57b-175">Application Insights para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0b57b-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
