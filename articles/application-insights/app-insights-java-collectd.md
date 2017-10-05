---
title: Monitorar o desempenho do aplicativo Web Java no Linux - Azure | Microsoft Docs
description: Monitoramento estendido do desempenho de aplicativo do seu site Java com o plug-in CollectD para Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="1165c-103">collectd: métricas de desempenho do Linux no Application Insights</span><span class="sxs-lookup"><span data-stu-id="1165c-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="1165c-104">Para explorar as métricas de desempenho do sistema Linux no [Application Insights](app-insights-overview.md), instale [collectd](http://collectd.org/) com seu plug-in do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1165c-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="1165c-105">Essa solução de software livre reúne várias estatísticas de sistema e de rede.</span><span class="sxs-lookup"><span data-stu-id="1165c-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="1165c-106">Normalmente, você usará o collectd se já tiver [instrumentado seu serviço Web Java com o Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="1165c-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="1165c-107">Isso oferece a você mais dados para ajudá-lo a aprimorar o desempenho do aplicativo ou para diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="1165c-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![Exemplo de gráficos](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="1165c-109">Obter a chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="1165c-109">Get your instrumentation key</span></span>
<span data-ttu-id="1165c-110">No [Portal do Microsoft Azure](https://portal.azure.com), abra o recurso [Application Insights](app-insights-overview.md) onde você quer que os dados sejam exibidos.</span><span class="sxs-lookup"><span data-stu-id="1165c-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="1165c-111">(Ou [crie um novo recurso](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="1165c-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="1165c-112">Faça uma cópia da chave de instrumentação que identifica o recurso.</span><span class="sxs-lookup"><span data-stu-id="1165c-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![Procure tudo, abra seu recurso e, no menu suspenso Essentials, selecione e copie a Chave de Instrumentação](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="1165c-114">Instalar o plug-in e collectd</span><span class="sxs-lookup"><span data-stu-id="1165c-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="1165c-115">Em seus computadores com o servidor Linux:</span><span class="sxs-lookup"><span data-stu-id="1165c-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="1165c-116">Instale [collectd](http://collectd.org/) versão 5.4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1165c-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="1165c-117">Baixe o [plug-in do gravador collectd do Application Insights](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="1165c-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="1165c-118">Observe o número de versão.</span><span class="sxs-lookup"><span data-stu-id="1165c-118">Note the version number.</span></span>
3. <span data-ttu-id="1165c-119">Copie o plug-in JAR em `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="1165c-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="1165c-120">Edite `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="1165c-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="1165c-121">Verifique se [o plug-in do Java](https://collectd.org/wiki/index.php/Plugin:Java) está habilitado.</span><span class="sxs-lookup"><span data-stu-id="1165c-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="1165c-122">Atualize o JVMArg para java.class.path de modo a incluir o JAR a seguir.</span><span class="sxs-lookup"><span data-stu-id="1165c-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="1165c-123">Atualize o número de versão para corresponder àquela que você baixou:</span><span class="sxs-lookup"><span data-stu-id="1165c-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="1165c-124">Adicione esse trecho usando a chave de instrumentação do seu recurso:</span><span class="sxs-lookup"><span data-stu-id="1165c-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="1165c-125">Veja o exemplo de parte de um arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="1165c-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="1165c-126">Configure outros [plug-ins collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), que possam coletar vários dados de diferentes fontes.</span><span class="sxs-lookup"><span data-stu-id="1165c-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="1165c-127">Reinicie o collectd, de acordo com seu [manual](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="1165c-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="1165c-128">Exibir os dados no Application Insights</span><span class="sxs-lookup"><span data-stu-id="1165c-128">View the data in Application Insights</span></span>
<span data-ttu-id="1165c-129">No recurso Application Insights, abra o [Metrics Explorer e adicione gráficos][metrics], selecionando as métricas que deseja ver na categoria Personalizado.</span><span class="sxs-lookup"><span data-stu-id="1165c-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="1165c-130">Por padrão, as métricas são agregadas em todos os computadores host dos quais as métricas foram coletadas.</span><span class="sxs-lookup"><span data-stu-id="1165c-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="1165c-131">Para exibir as métricas por host, na folha Detalhes do gráfico, ative Agrupamento e escolha Agrupar por CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="1165c-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="1165c-132">Excluir o carregamento de estatísticas específicas</span><span class="sxs-lookup"><span data-stu-id="1165c-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="1165c-133">Por padrão, o plug-in do Application Insights envia todos os dados coletados por todos os plug-ins collect ‘read’ habilitados.</span><span class="sxs-lookup"><span data-stu-id="1165c-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="1165c-134">Para excluir dados de plug-ins ou fontes de dados específicos:</span><span class="sxs-lookup"><span data-stu-id="1165c-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="1165c-135">Edite o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="1165c-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="1165c-136">Em `<Plugin ApplicationInsightsWriter>`, adicione linhas diretivas como esta:</span><span class="sxs-lookup"><span data-stu-id="1165c-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="1165c-137">Diretiva</span><span class="sxs-lookup"><span data-stu-id="1165c-137">Directive</span></span> | <span data-ttu-id="1165c-138">Efeito</span><span class="sxs-lookup"><span data-stu-id="1165c-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="1165c-139">Excluir todos os dados coletados pelo plug-in `disk`</span><span class="sxs-lookup"><span data-stu-id="1165c-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="1165c-140">Exclua as fontes denominadas `read` e `write` do plug-in `disk`.</span><span class="sxs-lookup"><span data-stu-id="1165c-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="1165c-141">Diretivas separadas por uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="1165c-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="1165c-142">Problemas?</span><span class="sxs-lookup"><span data-stu-id="1165c-142">Problems?</span></span>
<span data-ttu-id="1165c-143">*Não vejo dados no portal*</span><span class="sxs-lookup"><span data-stu-id="1165c-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="1165c-144">Abra [Pesquisar][diagnostic] para ver se os eventos brutos aparecem.</span><span class="sxs-lookup"><span data-stu-id="1165c-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="1165c-145">Às vezes, eles levam mais tempo para aparecer no Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="1165c-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="1165c-146">Talvez você precise [definir exceções de firewall para dados de saída](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="1165c-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="1165c-147">Habilite o rastreamento no plug-in do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1165c-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="1165c-148">Adicione esta linha em `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="1165c-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="1165c-149">Abra um terminal e inicie collectd no modo detalhado para ver todos os problemas que ele está reportando:</span><span class="sxs-lookup"><span data-stu-id="1165c-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="1165c-150">Problema conhecido</span><span class="sxs-lookup"><span data-stu-id="1165c-150">Known issue</span></span>

<span data-ttu-id="1165c-151">O plug-in de Gravação do Application Insights é incompatível com determinados plugins de Leitura.</span><span class="sxs-lookup"><span data-stu-id="1165c-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="1165c-152">Alguns plugins às vezes enviam "NaN" onde o plug-in do Application Insights espera um número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="1165c-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="1165c-153">Sintoma: o log coletado mostra erros que incluem "AI: ... SyntaxError: token N" inexperado.</span><span class="sxs-lookup"><span data-stu-id="1165c-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="1165c-154">Solução alternativa: exclua dados coletados pelo problema de plugins de Gravação.</span><span class="sxs-lookup"><span data-stu-id="1165c-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


