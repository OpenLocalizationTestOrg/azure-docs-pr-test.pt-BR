---
title: Contadores de desempenho no Application Insights | Microsoft Docs
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
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="2c40f-103">Contadores de desempenho do sistema no Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c40f-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="2c40f-104">O Windows fornece uma ampla variedade de [contadores de desempenho](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) como ocupação da CPU, memória, disco e uso da rede.</span><span class="sxs-lookup"><span data-stu-id="2c40f-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="2c40f-105">Você também pode definir seus próprios.</span><span class="sxs-lookup"><span data-stu-id="2c40f-105">You can also define your own.</span></span> <span data-ttu-id="2c40f-106">O [Application Insights](app-insights-overview.md) pode mostrar esses contadores de desempenho se o seu aplicativo estiver em execução no IIS em um host local ou máquina virtual a qual você tem acesso administrativo.</span><span class="sxs-lookup"><span data-stu-id="2c40f-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="2c40f-107">Os gráficos indicam os recursos disponíveis para seu aplicativo ativo e podem ajudar a identificar uma carga sem balanceamento entre instâncias do servidor.</span><span class="sxs-lookup"><span data-stu-id="2c40f-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="2c40f-108">Os contadores de desempenho aparecem na folha Servidores, que inclui uma tabela que segmenta pela instância do servidor.</span><span class="sxs-lookup"><span data-stu-id="2c40f-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Contadores de desempenho reportados no Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="2c40f-110">(Os contadores de desempenho não estão disponíveis para aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c40f-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="2c40f-111">Mas você pode [enviar o Diagnóstico do Azure para o Application Insights](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="2c40f-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="2c40f-112">Visualizar contadores</span><span class="sxs-lookup"><span data-stu-id="2c40f-112">View counters</span></span>
<span data-ttu-id="2c40f-113">A folha Servidores mostra um conjunto padrão de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="2c40f-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="2c40f-114">Para ver outros contadores, edite os gráficos na folha Servidores, ou abra uma nova folha [Metrics Explorer](app-insights-metrics-explorer.md) e adicione novos gráficos.</span><span class="sxs-lookup"><span data-stu-id="2c40f-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="2c40f-115">Os contadores disponíveis são listados como métricas quando você edita um gráfico.</span><span class="sxs-lookup"><span data-stu-id="2c40f-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Contadores de desempenho reportados no Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="2c40f-117">Para ver todos os gráficos mais úteis em um único lugar, crie um [painel](app-insights-dashboards.md) e fixe-os a ele.</span><span class="sxs-lookup"><span data-stu-id="2c40f-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="2c40f-118">Adicionar contadores</span><span class="sxs-lookup"><span data-stu-id="2c40f-118">Add counters</span></span>
<span data-ttu-id="2c40f-119">Se o contador de desempenho desejado não for mostrado na lista de métricas, é porque o SDK do Application Insights não está coletando em seu servidor Web.</span><span class="sxs-lookup"><span data-stu-id="2c40f-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="2c40f-120">Você pode configurá-lo para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="2c40f-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="2c40f-121">Descubra quais contadores estão disponíveis em seu servidor usando este comando do PowerShell no servidor:</span><span class="sxs-lookup"><span data-stu-id="2c40f-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="2c40f-122">(Consulte [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="2c40f-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="2c40f-123">Abra o ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="2c40f-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="2c40f-124">Se você adicionou o Application Insights ao seu aplicativo durante o desenvolvimento, edite applicationinsights.config em seu projeto e implante-o novamente em seus servidores.</span><span class="sxs-lookup"><span data-stu-id="2c40f-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="2c40f-125">Se você usou o Status Monitor para instrumentar um aplicativo Web em tempo de execução, localize applicationinsights.config no diretório raiz do aplicativo no IIS.</span><span class="sxs-lookup"><span data-stu-id="2c40f-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="2c40f-126">Atualize-o em cada instância de servidor.</span><span class="sxs-lookup"><span data-stu-id="2c40f-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="2c40f-127">Edite a diretiva do coletor de desempenho:</span><span class="sxs-lookup"><span data-stu-id="2c40f-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="2c40f-128">Você pode capturar os contadores padrão e aqueles implementados por conta própria.</span><span class="sxs-lookup"><span data-stu-id="2c40f-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="2c40f-129">`\Objects\Processes` é um exemplo de um contador padrão, disponível em todos os sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="2c40f-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="2c40f-130">`\Sales(photo)\# Items Sold` é um exemplo de um contador personalizado que pode ser implementado em um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2c40f-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="2c40f-131">O formato é `\Category(instance)\Counter"`, ou apenas `\Category\Counter` para categorias que não têm instâncias.</span><span class="sxs-lookup"><span data-stu-id="2c40f-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="2c40f-132">`ReportAs` é necessário para os nomes de contador que não correspondem a `[a-zA-Z()/-_ \.]+` - isto é, eles contêm caracteres que não estão nos seguintes conjuntos: letras, colchetes, barra invertida, hífen, sublinhado, espaço, ponto.</span><span class="sxs-lookup"><span data-stu-id="2c40f-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="2c40f-133">Se você especificar uma instância, ela será coletada como uma dimensão "CounterInstanceName" da métrica reportada.</span><span class="sxs-lookup"><span data-stu-id="2c40f-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="2c40f-134">Coletando contadores de desempenho no código</span><span class="sxs-lookup"><span data-stu-id="2c40f-134">Collecting performance counters in code</span></span>
<span data-ttu-id="2c40f-135">Para coletar contadores de desempenho do sistema e enviá-los ao Application Insights, você pode adaptar o trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c40f-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="2c40f-136">Ou você pode fazer a mesma coisa com métricas personalizadas que você criou:</span><span class="sxs-lookup"><span data-stu-id="2c40f-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="2c40f-137">Contadores de desempenho no Analytics</span><span class="sxs-lookup"><span data-stu-id="2c40f-137">Performance counters in Analytics</span></span>
<span data-ttu-id="2c40f-138">Você pode pesquisar e exibir relatórios do contador de desempenho no [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="2c40f-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="2c40f-139">O esquema **performanceCounters** expõe o nome `category`, `counter` e o nome `instance` de cada contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="2c40f-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="2c40f-140">Na telemetria de cada aplicativo, você verá apenas os contadores para aquele aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c40f-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="2c40f-141">Por exemplo, para ver quais contadores estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2c40f-141">For example, to see what counters are available:</span></span> 

![Contadores de desempenho na análise do Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="2c40f-143">(Aqui 'Instance' refere-se á instância do contador de desempenho, não à instância do servidor ou função.</span><span class="sxs-lookup"><span data-stu-id="2c40f-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="2c40f-144">O nome da instância do contador de desempenho normalmente segmenta os contadores, como tempo de processador, pelo nome do processo ou aplicativo.)</span><span class="sxs-lookup"><span data-stu-id="2c40f-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="2c40f-145">Para obter um gráfico da memória disponível no período recente:</span><span class="sxs-lookup"><span data-stu-id="2c40f-145">To get a chart of available memory over the recent period:</span></span> 

![Gráfico de tempo da memória na análise do Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="2c40f-147">Como outras telemetrias, o **performanceCounters** também tem uma coluna `cloud_RoleInstance` que indica a identidade da instância do servidor host no qual seu aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="2c40f-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="2c40f-148">Por exemplo, para comparar o desempenho do seu aplicativo em diferentes computadores:</span><span class="sxs-lookup"><span data-stu-id="2c40f-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Desempenho segmentado por instância de função na análise do Application Insights](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="2c40f-150">Contadores do ASP.NET e do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c40f-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="2c40f-151">*Qual é a diferença entre a Taxa de exceções e as Métricas de exceções?*</span><span class="sxs-lookup"><span data-stu-id="2c40f-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="2c40f-152">*Taxa de exceções* é um contador de desempenho do sistema.</span><span class="sxs-lookup"><span data-stu-id="2c40f-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="2c40f-153">O CLR conta todas as exceções tratadas e sem tratamento que são lançadas, e divide o total em um intervalo de amostragem pela duração do intervalo.</span><span class="sxs-lookup"><span data-stu-id="2c40f-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="2c40f-154">O SDK do Application Insights coleta esse resultado e o envia para o portal.</span><span class="sxs-lookup"><span data-stu-id="2c40f-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="2c40f-155">*Exceções* é uma contagem dos relatórios TrackException recebida pelo portal no intervalo de amostragem do gráfico.</span><span class="sxs-lookup"><span data-stu-id="2c40f-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="2c40f-156">Ele inclui apenas as exceções tratadas em que você tenha gravado chamadas TrackException em seu código e não inclui todas as [exceções sem tratamento](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="2c40f-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="2c40f-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="2c40f-157">Alerts</span></span>
<span data-ttu-id="2c40f-158">Assim como ocorre com outras métricas, você pode [definir um alerta](app-insights-alerts.md) para avisar se um contador de desempenho fica fora de um limite especificado.</span><span class="sxs-lookup"><span data-stu-id="2c40f-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="2c40f-159">Abra a folha Alertas e clique em Adicionar Alerta.</span><span class="sxs-lookup"><span data-stu-id="2c40f-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="2c40f-160"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c40f-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="2c40f-161">Acompanhamento de dependência</span><span class="sxs-lookup"><span data-stu-id="2c40f-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="2c40f-162">Acompanhamento de exceções</span><span class="sxs-lookup"><span data-stu-id="2c40f-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

