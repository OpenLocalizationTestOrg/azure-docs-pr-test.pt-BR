---
title: aaaGet iniciado com o Azure Application Insights com Java em Eclipse | Documentos da Microsoft
description: Use hello desempenho tooadd plug-in do Eclipse e uso de monitoramento tooyour Java com o Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="42f07-103">Introdução ao Application Insights com Java no Eclipse</span><span class="sxs-lookup"><span data-stu-id="42f07-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="42f07-104">Olá SDK do Application Insights envia telemetria do seu aplicativo da web de Java para que você pode analisar o uso e desempenho.</span><span class="sxs-lookup"><span data-stu-id="42f07-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="42f07-105">Olá Eclipse plug-in para o Application Insights instala automaticamente Olá SDK em seu projeto para que você obtenha de telemetria de caixa hello, além de uma API que você pode usar a telemetria personalizada de toowrite.</span><span class="sxs-lookup"><span data-stu-id="42f07-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="42f07-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42f07-106">Prerequisites</span></span>
<span data-ttu-id="42f07-107">Olá plug-in trabalha atualmente para projetos Maven e dinâmico da Web no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="42f07-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="42f07-108">([Tipos de tooother adicionar Application Insights do projeto Java][java].)</span><span class="sxs-lookup"><span data-stu-id="42f07-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="42f07-109">Você precisará de:</span><span class="sxs-lookup"><span data-stu-id="42f07-109">You'll need:</span></span>

* <span data-ttu-id="42f07-110">Oracle JRE 1.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="42f07-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="42f07-111">Uma assinatura muito[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="42f07-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="42f07-112">[Um IDE do Eclipse para desenvolvedores do Java EE](http://www.eclipse.org/downloads/), Indigo ou posterior.</span><span class="sxs-lookup"><span data-stu-id="42f07-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="42f07-113">Windows 7 ou posterior, ou Windows Server 2008 ou posterior</span><span class="sxs-lookup"><span data-stu-id="42f07-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="42f07-114">Instalar Olá SDK no Eclipse (uma vez)</span><span class="sxs-lookup"><span data-stu-id="42f07-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="42f07-115">Você só tem toodo dessa vez por computador.</span><span class="sxs-lookup"><span data-stu-id="42f07-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="42f07-116">Esta etapa instala um kit de ferramentas que possa adicionar Olá SDK tooeach projeto Web dinâmico.</span><span class="sxs-lookup"><span data-stu-id="42f07-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="42f07-117">No Eclipse, clique em Ajuda, depois em Instalar novo Software.</span><span class="sxs-lookup"><span data-stu-id="42f07-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Ajuda, Instalar Novo Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="42f07-119">Olá SDK está em http://dl.microsoft.com/eclipse no Kit de ferramentas do Azure.</span><span class="sxs-lookup"><span data-stu-id="42f07-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="42f07-120">Desmarque **Contatar todos os sites de atualização...**</span><span class="sxs-lookup"><span data-stu-id="42f07-120">Uncheck **Contact all update sites...**</span></span>

    ![Para o SDK do Application Insights, limpe a opção Contatar todos os sites de atualização](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="42f07-122">Siga Olá restantes etapas para cada projeto Java.</span><span class="sxs-lookup"><span data-stu-id="42f07-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="42f07-123">Criar um recurso do Application Insights no Azure</span><span class="sxs-lookup"><span data-stu-id="42f07-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="42f07-124">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42f07-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="42f07-125">Criar um novo recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="42f07-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="42f07-126">Defina o aplicativo de web tooJava do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="42f07-126">Set hello application type tooJava web application.</span></span>  

    ![Clique em + e escolha Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="42f07-128">Localize a chave de instrumentação de saudação do novo recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f07-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="42f07-129">Você precisará toopaste isso em seu projeto de código em breve.</span><span class="sxs-lookup"><span data-stu-id="42f07-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="42f07-131">Adicionar Application Insights tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="42f07-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="42f07-132">Adicione o Application Insights no menu de contexto de saudação do seu projeto da web de Java.</span><span class="sxs-lookup"><span data-stu-id="42f07-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="42f07-134">Cole a chave de instrumentação Olá que você obteve Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="42f07-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="42f07-136">chave de saudação enviada juntamente com todos os itens de telemetria e informa ao Application Insights toodisplay-lo em seu recurso.</span><span class="sxs-lookup"><span data-stu-id="42f07-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="42f07-137">Executar o aplicativo hello e ver as métricas</span><span class="sxs-lookup"><span data-stu-id="42f07-137">Run hello application and see metrics</span></span>
<span data-ttu-id="42f07-138">Execute seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42f07-138">Run your application.</span></span>

<span data-ttu-id="42f07-139">Retorne recurso do Application Insights tooyour no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42f07-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="42f07-140">Dados de solicitações HTTP serão exibida na folha de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f07-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="42f07-141">(Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)</span><span class="sxs-lookup"><span data-stu-id="42f07-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="42f07-142">Falhas, contagens de solicitação e resposta do servidor</span><span class="sxs-lookup"><span data-stu-id="42f07-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="42f07-143">Clique em por meio de qualquer gráfico toosee métricas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="42f07-143">Click through any chart toosee more detailed metrics.</span></span>

![Contagens de solicitação por nome](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="42f07-145">[Saiba mais sobre métricas.][metrics]</span><span class="sxs-lookup"><span data-stu-id="42f07-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="42f07-146">E, ao exibir as propriedades de saudação de uma solicitação, você pode ver eventos de telemetria Olá associados a ele, como solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="42f07-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Todos os rastreamentos para esta solicitação](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="42f07-148">Telemetria do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="42f07-148">Client-side telemetry</span></span>
<span data-ttu-id="42f07-149">Folha de início rápido de saudação, clique em obter código toomonitor minhas páginas da web:</span><span class="sxs-lookup"><span data-stu-id="42f07-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![Na folha de visão geral sobre seu aplicativo, selecione início rápido, obter código toomonitor minhas páginas da web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="42f07-152">Inserir o trecho de código de saudação no cabeçalho Olá dos seus arquivos HTML.</span><span class="sxs-lookup"><span data-stu-id="42f07-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="42f07-153">Exibir dados do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="42f07-153">View client-side data</span></span>
<span data-ttu-id="42f07-154">Abra suas páginas da Web atualizadas e use-as.</span><span class="sxs-lookup"><span data-stu-id="42f07-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="42f07-155">Aguarde um minuto ou dois e depois retornar tooApplication Insights e folha de uso de saudação aberto.</span><span class="sxs-lookup"><span data-stu-id="42f07-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="42f07-156">(Na folha de visão geral do hello, role para baixo e clique em uso.)</span><span class="sxs-lookup"><span data-stu-id="42f07-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="42f07-157">Métricas de sessão, de usuário e de exibição de página serão exibida na folha de uso de saudação:</span><span class="sxs-lookup"><span data-stu-id="42f07-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Sessões, usuários e modos de exibição de página](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="42f07-159">[Saiba mais sobre como configurar a telemetria do lado do cliente.][usage]</span><span class="sxs-lookup"><span data-stu-id="42f07-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="42f07-160">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="42f07-160">Publish your application</span></span>
<span data-ttu-id="42f07-161">Publicar o seu servidor de toohello de aplicativo agora, permitem que pessoas usá-lo e assista a telemetria Olá aparecerão no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f07-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="42f07-162">Verifique se o firewall permite que seu aplicativo toosend telemetria toothese portas:</span><span class="sxs-lookup"><span data-stu-id="42f07-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="42f07-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="42f07-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="42f07-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="42f07-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="42f07-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="42f07-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="42f07-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="42f07-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="42f07-167">Nos servidores Windows, instale:</span><span class="sxs-lookup"><span data-stu-id="42f07-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="42f07-168">Microsoft Visual C++ redistribuível</span><span class="sxs-lookup"><span data-stu-id="42f07-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="42f07-169">(Isso habilita os contadores de desempenho.)</span><span class="sxs-lookup"><span data-stu-id="42f07-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="42f07-170">Falhas de solicitação e exceções</span><span class="sxs-lookup"><span data-stu-id="42f07-170">Exceptions and request failures</span></span>
<span data-ttu-id="42f07-171">Exceções sem tratamento são coletadas automaticamente:</span><span class="sxs-lookup"><span data-stu-id="42f07-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="42f07-172">dados toocollect outras exceções, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="42f07-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="42f07-173">[Inserir chama tooTrackException no seu código](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="42f07-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="42f07-174">[Instalar Olá agente Java em seu servidor](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="42f07-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="42f07-175">Você especificar métodos Olá toowatch desejado.</span><span class="sxs-lookup"><span data-stu-id="42f07-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="42f07-176">Monitorar chamadas de método e dependências externas</span><span class="sxs-lookup"><span data-stu-id="42f07-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="42f07-177">[Instalar Olá agente Java](app-insights-java-agent.md) toolog especificado métodos internos e as chamadas feitas por meio do JDBC, com dados de tempo.</span><span class="sxs-lookup"><span data-stu-id="42f07-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="42f07-178">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="42f07-178">Performance counters</span></span>
<span data-ttu-id="42f07-179">Na sua folha de visão geral, role para baixo e clique em Olá **servidores** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="42f07-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="42f07-180">Você verá uma variedade de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="42f07-180">You'll see a range of performance counters.</span></span>

![Role para baixo do bloco de servidores tooclick Olá](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="42f07-182">Personalizar a coleta do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="42f07-182">Customize performance counter collection</span></span>
<span data-ttu-id="42f07-183">coleção de toodisable de conjunto de contadores de desempenho padrão Olá adicionar Olá código sob o nó de raiz de saudação do arquivo de ApplicationInsights.xml Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="42f07-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="42f07-184">Coletar contadores de desempenho adicionais</span><span class="sxs-lookup"><span data-stu-id="42f07-184">Collect additional performance counters</span></span>
<span data-ttu-id="42f07-185">Você pode especificar toobe de contadores de desempenho coletados.</span><span class="sxs-lookup"><span data-stu-id="42f07-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="42f07-186">Contadores do JMX (expostas pelo Olá Máquina Virtual Java)</span><span class="sxs-lookup"><span data-stu-id="42f07-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="42f07-187">`displayName`– nome hello exibido no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="42f07-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="42f07-188">`objectName`– nome do objeto Olá JMX.</span><span class="sxs-lookup"><span data-stu-id="42f07-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="42f07-189">`attribute`– atributo Olá Olá toofetch de nome de objeto JMX</span><span class="sxs-lookup"><span data-stu-id="42f07-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="42f07-190">`type`(opcional) - Olá tipo de atributo do objeto JMX:</span><span class="sxs-lookup"><span data-stu-id="42f07-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="42f07-191">Padrão: um tipo simples como “int” ou “long”.</span><span class="sxs-lookup"><span data-stu-id="42f07-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="42f07-192">`composite`: dados do contador de desempenho hello estão no formato de saudação do 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="42f07-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="42f07-193">`tabular`: dados do contador de desempenho hello estão no formato de saudação de uma linha da tabela</span><span class="sxs-lookup"><span data-stu-id="42f07-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="42f07-194">Contadores de desempenho do Windows</span><span class="sxs-lookup"><span data-stu-id="42f07-194">Windows performance counters</span></span>
<span data-ttu-id="42f07-195">Cada [contador de desempenho do Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) é um membro de uma categoria (em Olá mesma forma que um campo é um membro de uma classe).</span><span class="sxs-lookup"><span data-stu-id="42f07-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="42f07-196">Categorias podem ser globais, ou podem ter instâncias numeradas ou nomeadas.</span><span class="sxs-lookup"><span data-stu-id="42f07-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="42f07-197">displayName – nome hello exibido no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="42f07-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="42f07-198">categoryName – Olá categoria contador de desempenho (objeto de desempenho) ao qual esse contador de desempenho está associado.</span><span class="sxs-lookup"><span data-stu-id="42f07-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="42f07-199">counterName – nome Olá Olá do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="42f07-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="42f07-200">instanceName – Olá nome de instância de categoria do contador de desempenho de saudação ou uma cadeia de caracteres vazia (""), se a categoria de saudação contém uma única instância.</span><span class="sxs-lookup"><span data-stu-id="42f07-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="42f07-201">Se Olá categoryName é o processo e contador de desempenho de saudação você gostaria que toocollect é do processo atual de JVM Olá em que seu aplicativo é executado, especifique `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="42f07-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="42f07-202">Seus contadores de desempenho são visíveis como métricas personalizadas em [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="42f07-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="42f07-203">Contadores de desempenho do Unix</span><span class="sxs-lookup"><span data-stu-id="42f07-203">Unix performance counters</span></span>
* <span data-ttu-id="42f07-204">[Instalar collectd com plug-in Application Insights de saudação](app-insights-java-collectd.md) tooget uma ampla variedade de dados de sistema e de rede.</span><span class="sxs-lookup"><span data-stu-id="42f07-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="42f07-205">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="42f07-205">Availability web tests</span></span>
<span data-ttu-id="42f07-206">Application Insights pode testar seu site em toocheck em intervalos regulares que ele está ativo e também responder.</span><span class="sxs-lookup"><span data-stu-id="42f07-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="42f07-207">[tooset backup][availability], role para baixo tooclick disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="42f07-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Role para baixo, clique em Disponibilidade, em seguida, Adicionar teste na Web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="42f07-209">Se seu site ficar inativo, você obterá gráficos de tempos de resposta e também notificações por email.</span><span class="sxs-lookup"><span data-stu-id="42f07-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemplo de teste da Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="42f07-211">[Saiba mais sobre testes de disponibilidade via web.][availability]</span><span class="sxs-lookup"><span data-stu-id="42f07-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="42f07-212">Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="42f07-212">Diagnostic logs</span></span>
<span data-ttu-id="42f07-213">Se você estiver usando Log4J ou Logback (v 1.2 ou 2.0) para rastreamento, você pode ter seus logs de rastreamento enviados automaticamente tooApplication Insights onde você pode explorar e pesquisá-los.</span><span class="sxs-lookup"><span data-stu-id="42f07-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="42f07-214">[Saiba mais sobre logs de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="42f07-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="42f07-215">Telemetria personalizada</span><span class="sxs-lookup"><span data-stu-id="42f07-215">Custom telemetry</span></span>
<span data-ttu-id="42f07-216">Insira algumas linhas de código no seu toofind de aplicativo web Java out que os usuários estão fazendo com que ele ou toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="42f07-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="42f07-217">Você pode inserir o código na página da web JavaScript e em Java do lado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f07-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="42f07-218">[Saiba mais sobre a telemetria personalizada][track]</span><span class="sxs-lookup"><span data-stu-id="42f07-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f07-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42f07-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="42f07-220">Detectar e diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="42f07-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="42f07-221">[Adicionar telemetria do cliente web] [ usage] tooget telemetria de desempenho do cliente de web hello.</span><span class="sxs-lookup"><span data-stu-id="42f07-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="42f07-222">[Configurar testes da web] [ availability] toomake-se de que seu aplicativo permanece em tempo real e responsivo.</span><span class="sxs-lookup"><span data-stu-id="42f07-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="42f07-223">[Pesquisar eventos e logs de] [ diagnostic] toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="42f07-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="42f07-224">[Capturar rastreamentos do Log4J ou Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="42f07-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="42f07-225">Acompanhar uso</span><span class="sxs-lookup"><span data-stu-id="42f07-225">Track usage</span></span>
* <span data-ttu-id="42f07-226">[Adicionar telemetria do cliente web] [ usage] toomonitor página exibições e métricas de usuário básica.</span><span class="sxs-lookup"><span data-stu-id="42f07-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="42f07-227">[Rastrear eventos personalizados e métricas](app-insights-web-track-usage.md) toolearn sobre como seu aplicativo é usado, tanto no cliente hello e no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f07-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
