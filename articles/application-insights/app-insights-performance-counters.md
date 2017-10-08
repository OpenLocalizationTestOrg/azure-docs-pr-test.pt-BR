---
title: contadores de aaaPerformance no Application Insights | Microsoft Docs
description: Monitore o sistema e contadores de desempenho .NET personalizados no Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="8000c-103">Contadores de desempenho do sistema no Application Insights</span><span class="sxs-lookup"><span data-stu-id="8000c-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="8000c-104">O Windows fornece uma ampla variedade de [contadores de desempenho](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) como ocupação da CPU, memória, disco e uso da rede.</span><span class="sxs-lookup"><span data-stu-id="8000c-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="8000c-105">Você também pode definir seus próprios.</span><span class="sxs-lookup"><span data-stu-id="8000c-105">You can also define your own.</span></span> <span data-ttu-id="8000c-106">[Application Insights](app-insights-overview.md) pode mostrar esses contadores de desempenho se seu aplicativo estiver em execução no IIS em um toowhich de host ou máquina virtual local têm acesso administrativo.</span><span class="sxs-lookup"><span data-stu-id="8000c-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="8000c-107">gráficos de saudação indicam aplicativos em tempo real do hello recursos tooyour disponíveis e podem ajudar a tooidentify sem balanceamento de carga entre instâncias do servidor.</span><span class="sxs-lookup"><span data-stu-id="8000c-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="8000c-108">Contadores de desempenho aparecem na folha de servidores de saudação, que inclui uma tabela que segmentos por instância de servidor.</span><span class="sxs-lookup"><span data-stu-id="8000c-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Contadores de desempenho reportados no Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="8000c-110">(Os contadores de desempenho não estão disponíveis para aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8000c-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="8000c-111">Mas você pode [enviar o diagnóstico do Azure tooApplication Insights](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="8000c-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="8000c-112">Visualizar contadores</span><span class="sxs-lookup"><span data-stu-id="8000c-112">View counters</span></span>
<span data-ttu-id="8000c-113">folha de servidores Olá mostra um conjunto padrão de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="8000c-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="8000c-114">toosee outros contadores, em editar gráficos Olá na folha de servidores hello, ou abra uma nova [Metrics Explorer](app-insights-metrics-explorer.md) folha e adicionar novos gráficos.</span><span class="sxs-lookup"><span data-stu-id="8000c-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="8000c-115">contadores disponíveis Olá são listados como métricas de quando você edita um gráfico.</span><span class="sxs-lookup"><span data-stu-id="8000c-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Contadores de desempenho reportados no Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="8000c-117">toosee todos os gráficos mais úteis em um único local, crie um [painel](app-insights-dashboards.md) e fixá-los tooit.</span><span class="sxs-lookup"><span data-stu-id="8000c-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="8000c-118">Adicionar contadores</span><span class="sxs-lookup"><span data-stu-id="8000c-118">Add counters</span></span>
<span data-ttu-id="8000c-119">Se o contador de desempenho de saudação desejado não é mostrado na lista de saudação de métricas, é porque Olá SDK do Application Insights não coletá-lo no seu servidor web.</span><span class="sxs-lookup"><span data-stu-id="8000c-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="8000c-120">Você pode configurá-lo toodo assim.</span><span class="sxs-lookup"><span data-stu-id="8000c-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="8000c-121">Descubra quais contadores estão disponíveis no seu servidor usando esse comando do PowerShell no servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="8000c-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="8000c-122">(Consulte [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="8000c-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="8000c-123">Abra o ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="8000c-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="8000c-124">Se você adicionou o Application Insights tooyour aplicativo durante o desenvolvimento, edite o applicationinsights. config em seu projeto e, em seguida, implantá-lo novamente tooyour servidores.</span><span class="sxs-lookup"><span data-stu-id="8000c-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="8000c-125">Se você usou o Monitor de Status tooinstrument um aplicativo web em tempo de execução, encontre o applicationinsights. config no diretório raiz de saudação do aplicativo hello no IIS.</span><span class="sxs-lookup"><span data-stu-id="8000c-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="8000c-126">Atualize-o em cada instância de servidor.</span><span class="sxs-lookup"><span data-stu-id="8000c-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="8000c-127">Edite diretiva de coletor de desempenho hello:</span><span class="sxs-lookup"><span data-stu-id="8000c-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="8000c-128">Você pode capturar os contadores padrão e aqueles implementados por conta própria.</span><span class="sxs-lookup"><span data-stu-id="8000c-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="8000c-129">`\Objects\Processes` é um exemplo de um contador padrão, disponível em todos os sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="8000c-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="8000c-130">`\Sales(photo)\# Items Sold` é um exemplo de um contador personalizado que pode ser implementado em um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="8000c-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="8000c-131">formato de saudação é `\Category(instance)\Counter"`, ou por categorias que não têm instâncias, apenas `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="8000c-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="8000c-132">`ReportAs`é necessário para os nomes de contadores que não correspondem a `[a-zA-Z()/-_ \.]+` -ou seja, eles contêm caracteres que não estão em Olá conjuntos a seguir: letras, round colchetes, barra invertida, hífen, sublinhado, espaço, ponto.</span><span class="sxs-lookup"><span data-stu-id="8000c-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="8000c-133">Se você especificar uma instância, ele será coletado como uma dimensão "CounterInstanceName" de saudação relatado métrica.</span><span class="sxs-lookup"><span data-stu-id="8000c-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="8000c-134">Coletando contadores de desempenho no código</span><span class="sxs-lookup"><span data-stu-id="8000c-134">Collecting performance counters in code</span></span>
<span data-ttu-id="8000c-135">contadores de desempenho do sistema toocollect e enviá-los tooApplication Insights, você pode adaptar trechos de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="8000c-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="8000c-136">Ou você pode fazer Olá com métricas personalizadas que você criou a mesma coisa:</span><span class="sxs-lookup"><span data-stu-id="8000c-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="8000c-137">Contadores de desempenho no Analytics</span><span class="sxs-lookup"><span data-stu-id="8000c-137">Performance counters in Analytics</span></span>
<span data-ttu-id="8000c-138">Você pode pesquisar e exibir relatórios do contador de desempenho no [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="8000c-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="8000c-139">Olá **performanceCounters** esquema expõe Olá `category`, `counter` nome, e `instance` nome de contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="8000c-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="8000c-140">Telemetria Olá para cada aplicativo, você verá apenas os contadores Olá para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8000c-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="8000c-141">Por exemplo, toosee quais contadores estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="8000c-141">For example, toosee what counters are available:</span></span> 

![Contadores de desempenho na análise do Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="8000c-143">(Aqui 'Instance' se refere a instância do contador de desempenho toohello, Olá não funções ou servidores de instância de máquina.</span><span class="sxs-lookup"><span data-stu-id="8000c-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="8000c-144">nome de instância do contador de desempenho Olá segmentos normalmente contadores, como tempo de processador por nome de saudação do aplicativo ou processo hello.)</span><span class="sxs-lookup"><span data-stu-id="8000c-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="8000c-145">tooget um gráfico de memória disponível em Olá período recente:</span><span class="sxs-lookup"><span data-stu-id="8000c-145">tooget a chart of available memory over hello recent period:</span></span> 

![Gráfico de tempo da memória na análise do Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="8000c-147">Como outros telemetria **performanceCounters** também tem uma coluna `cloud_RoleInstance` que indica a identidade Olá Olá host da instância do servidor no qual o aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="8000c-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="8000c-148">Por exemplo, toocompare Olá desempenho do aplicativo em máquinas diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="8000c-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Desempenho segmentado por instância de função na análise do Application Insights](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="8000c-150">Contadores do ASP.NET e do Application Insights</span><span class="sxs-lookup"><span data-stu-id="8000c-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="8000c-151">*Qual é a diferença de saudação entre métricas de exceções e taxa de exceções Olá?*</span><span class="sxs-lookup"><span data-stu-id="8000c-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="8000c-152">*Taxa de exceções* é um contador de desempenho do sistema.</span><span class="sxs-lookup"><span data-stu-id="8000c-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="8000c-153">Olá CLR conta todos os Olá tratados e exceções sem tratamento que são geradas e divide o total de saudação em um intervalo de amostragem por comprimento de saudação do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8000c-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="8000c-154">Olá SDK do Application Insights coleta esse resultado e o envia toohello portal.</span><span class="sxs-lookup"><span data-stu-id="8000c-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="8000c-155">*Exceções* é uma contagem de saudação TrackException relatórios recebidos pelo portal Olá no intervalo de amostragem de saudação do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="8000c-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="8000c-156">Ele inclui somente Olá tratados exceções em que você tenha escrito TrackException chama em seu código e não inclui todos os [exceções sem tratamento](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="8000c-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="8000c-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="8000c-157">Alerts</span></span>
<span data-ttu-id="8000c-158">Como outras métricas, você pode [definir um alerta](app-insights-alerts.md) toowarn se um contador de desempenho ficar fora de um limite especificado.</span><span class="sxs-lookup"><span data-stu-id="8000c-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="8000c-159">Abra a folha de alertas de saudação e clique em Adicionar alertas.</span><span class="sxs-lookup"><span data-stu-id="8000c-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="8000c-160"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8000c-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="8000c-161">Acompanhamento de dependência</span><span class="sxs-lookup"><span data-stu-id="8000c-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="8000c-162">Acompanhamento de exceções</span><span class="sxs-lookup"><span data-stu-id="8000c-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

