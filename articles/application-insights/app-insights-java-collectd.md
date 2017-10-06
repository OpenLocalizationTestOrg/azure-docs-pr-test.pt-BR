---
title: aaaMonitor o desempenho do aplicativo web Java no Linux - Azure | Microsoft Docs
description: Estendido aplicativo monitoramento de desempenho do seu site de Java com hello CollectD plug-in do Application Insights.
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
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="77a55-103">collectd: métricas de desempenho do Linux no Application Insights</span><span class="sxs-lookup"><span data-stu-id="77a55-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="77a55-104">métricas de desempenho do sistema tooexplore Linux em [Application Insights](app-insights-overview.md), instalar [collectd](http://collectd.org/), junto com o plug-in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="77a55-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="77a55-105">Essa solução de software livre reúne várias estatísticas de sistema e de rede.</span><span class="sxs-lookup"><span data-stu-id="77a55-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="77a55-106">Normalmente, você usará o collectd se já tiver [instrumentado seu serviço Web Java com o Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="77a55-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="77a55-107">Isso lhe dá mais toohelp de dados você tooenhance desempenho do seu aplicativo ou diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="77a55-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Exemplo de gráficos](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="77a55-109">Obter a chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="77a55-109">Get your instrumentation key</span></span>
<span data-ttu-id="77a55-110">Em Olá [portal do Microsoft Azure](https://portal.azure.com), abra Olá [Application Insights](app-insights-overview.md) recursos onde você deseja Olá tooappear de dados.</span><span class="sxs-lookup"><span data-stu-id="77a55-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="77a55-111">(Ou [crie um novo recurso](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="77a55-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="77a55-112">Faça uma cópia da chave de instrumentação hello, que identifica o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="77a55-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Procurar tudo, abra o recurso e, em seguida, em Olá Essentials lista suspensa, selecione e copie Olá chave de instrumentação](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="77a55-114">Instalar collectd e hello plug-in</span><span class="sxs-lookup"><span data-stu-id="77a55-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="77a55-115">Em seus computadores com o servidor Linux:</span><span class="sxs-lookup"><span data-stu-id="77a55-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="77a55-116">Instale [collectd](http://collectd.org/) versão 5.4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="77a55-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="77a55-117">Baixar Olá [plug-in do Application Insights collectd gravador](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="77a55-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="77a55-118">Observe o número de versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="77a55-118">Note hello version number.</span></span>
3. <span data-ttu-id="77a55-119">Copie o plug-in Olá JAR em `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="77a55-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="77a55-120">Edite `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="77a55-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="77a55-121">Certifique-se de que [Olá Java plug-in](https://collectd.org/wiki/index.php/Plugin:Java) está habilitado.</span><span class="sxs-lookup"><span data-stu-id="77a55-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="77a55-122">Atualize hello JVMArg para Olá java.class.path tooinclude Olá JAR a seguir.</span><span class="sxs-lookup"><span data-stu-id="77a55-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="77a55-123">Atualize Olá versão número toomatch Olá que você baixou:</span><span class="sxs-lookup"><span data-stu-id="77a55-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="77a55-124">Adicione este trecho de código, usando Olá chave de instrumentação do recurso:</span><span class="sxs-lookup"><span data-stu-id="77a55-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="77a55-125">Veja o exemplo de parte de um arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="77a55-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="77a55-126">Configure outros [plug-ins collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), que possam coletar vários dados de diferentes fontes.</span><span class="sxs-lookup"><span data-stu-id="77a55-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="77a55-127">Reiniciar collectd de acordo com o tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="77a55-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="77a55-128">Exibir dados de saudação no Application Insights</span><span class="sxs-lookup"><span data-stu-id="77a55-128">View hello data in Application Insights</span></span>
<span data-ttu-id="77a55-129">Em seu recurso Application Insights, abra [Metrics Explorer e adicione gráficos][metrics], selecionar métricas Olá deseja toosee de categoria personalizada de saudação.</span><span class="sxs-lookup"><span data-stu-id="77a55-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="77a55-130">Por padrão, as métricas de saudação são agregadas em todas as máquinas de host do qual métricas Olá foram coletadas.</span><span class="sxs-lookup"><span data-stu-id="77a55-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="77a55-131">métricas de saudação tooview por host, na folha de detalhes do gráfico hello, ativar o agrupamento e escolha toogroup pelo Host CollectD.</span><span class="sxs-lookup"><span data-stu-id="77a55-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="77a55-132">carregamento de tooexclude de estatísticas específicos</span><span class="sxs-lookup"><span data-stu-id="77a55-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="77a55-133">Por padrão, o plug-in do Application Insights Olá envia todos os dados de saudação coletados por todos os collectd de saudação habilitada 'leitura' Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="77a55-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="77a55-134">tooexclude dados de fontes de dados ou plug-ins específicos:</span><span class="sxs-lookup"><span data-stu-id="77a55-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="77a55-135">Edite o arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="77a55-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="77a55-136">Em `<Plugin ApplicationInsightsWriter>`, adicione linhas diretivas como esta:</span><span class="sxs-lookup"><span data-stu-id="77a55-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="77a55-137">Diretiva</span><span class="sxs-lookup"><span data-stu-id="77a55-137">Directive</span></span> | <span data-ttu-id="77a55-138">Efeito</span><span class="sxs-lookup"><span data-stu-id="77a55-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="77a55-139">Excluir todos os dados coletados pelo Olá `disk` plug-in</span><span class="sxs-lookup"><span data-stu-id="77a55-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="77a55-140">Excluir fontes de saudação denominados `read` e `write` de saudação `disk` plug-in.</span><span class="sxs-lookup"><span data-stu-id="77a55-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="77a55-141">Diretivas separadas por uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="77a55-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="77a55-142">Problemas?</span><span class="sxs-lookup"><span data-stu-id="77a55-142">Problems?</span></span>
<span data-ttu-id="77a55-143">*Não vejo dados no portal de saudação*</span><span class="sxs-lookup"><span data-stu-id="77a55-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="77a55-144">Abra [pesquisa] [ diagnostic] toosee se eventos brutos Olá chegaram.</span><span class="sxs-lookup"><span data-stu-id="77a55-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="77a55-145">Às vezes, eles têm mais tooappear no metrics explorer.</span><span class="sxs-lookup"><span data-stu-id="77a55-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="77a55-146">Talvez seja necessário muito[definir exceções de firewall para dados de saída](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="77a55-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="77a55-147">Habilite o rastreamento no plug-in Application Insights de saudação.</span><span class="sxs-lookup"><span data-stu-id="77a55-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="77a55-148">Adicione esta linha em `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="77a55-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="77a55-149">Abrir um terminal e iniciar collectd em modo detalhado, toosee quaisquer problemas que ele estiver se comunicando:</span><span class="sxs-lookup"><span data-stu-id="77a55-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="77a55-150">Problema conhecido</span><span class="sxs-lookup"><span data-stu-id="77a55-150">Known issue</span></span>

<span data-ttu-id="77a55-151">plug-in Olá de gravação de informações do aplicativo é incompatível com determinados plug-ins de leitura.</span><span class="sxs-lookup"><span data-stu-id="77a55-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="77a55-152">Alguns plug-ins, às vezes, enviam "NaN", onde o plug-in do Application Insights Olá espera um número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="77a55-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="77a55-153">Sintoma: o log de collectd Olá mostra erros que incluem "AI:... SyntaxError: token N" inexperado.</span><span class="sxs-lookup"><span data-stu-id="77a55-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="77a55-154">Solução alternativa: Exclua dados coletados pelo plug-ins de gravação de problema hello.</span><span class="sxs-lookup"><span data-stu-id="77a55-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


