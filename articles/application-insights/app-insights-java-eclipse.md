---
title: "Introdução ao Azure Application Insights com Java no Eclipse | Microsoft Docs"
description: Use o plug-in Eclipse para adicionar o monitoramento de desempenho e uso a seu site Java com o Application Insights
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="1018b-103">Introdução ao Application Insights com Java no Eclipse</span><span class="sxs-lookup"><span data-stu-id="1018b-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="1018b-104">O SDK do Application Insights envia telemetria por meio do seu aplicativo Web Java para que você possa analisar o uso e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="1018b-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="1018b-105">O plug-in Eclipse para o Application Insights instala automaticamente o SDK em seu projeto para que você obtenha telemetria já pronta, além de uma API que você pode usar para escrever telemetria personalizada.</span><span class="sxs-lookup"><span data-stu-id="1018b-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="1018b-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1018b-106">Prerequisites</span></span>
<span data-ttu-id="1018b-107">Atualmente, o plug-in funciona para projetos Maven e projetos dinâmicos da Web no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1018b-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="1018b-108">([Adicione o Application Insights a outros tipos de projeto Java][java].)</span><span class="sxs-lookup"><span data-stu-id="1018b-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="1018b-109">Você precisará de:</span><span class="sxs-lookup"><span data-stu-id="1018b-109">You'll need:</span></span>

* <span data-ttu-id="1018b-110">Oracle JRE 1.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="1018b-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="1018b-111">Uma assinatura do [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1018b-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="1018b-112">[Um IDE do Eclipse para desenvolvedores do Java EE](http://www.eclipse.org/downloads/), Indigo ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1018b-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="1018b-113">Windows 7 ou posterior, ou Windows Server 2008 ou posterior</span><span class="sxs-lookup"><span data-stu-id="1018b-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="1018b-114">Instalar o SDK no Eclipse (uma vez)</span><span class="sxs-lookup"><span data-stu-id="1018b-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="1018b-115">Você só precisa fazer isso uma vez por computador.</span><span class="sxs-lookup"><span data-stu-id="1018b-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="1018b-116">Esta etapa instala um kit de ferramentas que pode então adicionar o SDK para cada projeto Web dinâmico.</span><span class="sxs-lookup"><span data-stu-id="1018b-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="1018b-117">No Eclipse, clique em Ajuda, depois em Instalar novo Software.</span><span class="sxs-lookup"><span data-stu-id="1018b-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Ajuda, Instalar Novo Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="1018b-119">O SDK está em http://dl.microsoft.com/eclipse, no Kit de Ferramentas do Azure.</span><span class="sxs-lookup"><span data-stu-id="1018b-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="1018b-120">Desmarque **Contatar todos os sites de atualização...**</span><span class="sxs-lookup"><span data-stu-id="1018b-120">Uncheck **Contact all update sites...**</span></span>

    ![Para o SDK do Application Insights, limpe a opção Contatar todos os sites de atualização](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="1018b-122">Siga as etapas restantes para cada projeto Java.</span><span class="sxs-lookup"><span data-stu-id="1018b-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="1018b-123">Criar um recurso do Application Insights no Azure</span><span class="sxs-lookup"><span data-stu-id="1018b-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="1018b-124">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1018b-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1018b-125">Criar um novo recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="1018b-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="1018b-126">Defina o tipo de aplicativo para aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="1018b-126">Set the application type to Java web application.</span></span>  

    ![Clique em + e escolha Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="1018b-128">Localize a chave de instrumentação do novo recurso.</span><span class="sxs-lookup"><span data-stu-id="1018b-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="1018b-129">Você precisará colar isto no código de seu projeto em breve.</span><span class="sxs-lookup"><span data-stu-id="1018b-129">You'll need to paste this into your code project shortly.</span></span>  

    ![Na visão geral do novo recurso, clique em Propriedades e copie a chave de instrumentação](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="1018b-131">Adicione o Application Insights ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="1018b-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="1018b-132">Adicione o Application Insights no menu de contexto do seu projeto Web Java.</span><span class="sxs-lookup"><span data-stu-id="1018b-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![Na visão geral do novo recurso, clique em Propriedades e copie a chave de instrumentação](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="1018b-134">Cole a chave de instrumentação que você obteve no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1018b-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![Na visão geral do novo recurso, clique em Propriedades e copie a chave de instrumentação](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="1018b-136">A chave é enviada junto com todos os itens de telemetria e orienta o Application Insights a exibi-los em seu recurso.</span><span class="sxs-lookup"><span data-stu-id="1018b-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="1018b-137">Executar o aplicativo e ver as métricas</span><span class="sxs-lookup"><span data-stu-id="1018b-137">Run the application and see metrics</span></span>
<span data-ttu-id="1018b-138">Execute seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1018b-138">Run your application.</span></span>

<span data-ttu-id="1018b-139">Retorne para seu recurso Application Insights no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1018b-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="1018b-140">Dados de solicitações HTTP aparecerão na folha de visão geral.</span><span class="sxs-lookup"><span data-stu-id="1018b-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="1018b-141">(Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)</span><span class="sxs-lookup"><span data-stu-id="1018b-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="1018b-142">Falhas, contagens de solicitação e resposta do servidor</span><span class="sxs-lookup"><span data-stu-id="1018b-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="1018b-143">Clique em qualquer gráfico para ver métricas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="1018b-143">Click through any chart to see more detailed metrics.</span></span>

![Contagens de solicitação por nome](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="1018b-145">[Saiba mais sobre métricas.][metrics]</span><span class="sxs-lookup"><span data-stu-id="1018b-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="1018b-146">Ao exibir as propriedades de uma solicitação, você pode ver os eventos de telemetria associados a ela, como solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="1018b-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Todos os rastreamentos para esta solicitação](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="1018b-148">Telemetria do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="1018b-148">Client-side telemetry</span></span>
<span data-ttu-id="1018b-149">Na folha Início Rápido, clique em Obter código para monitorar as minhas páginas da Web:</span><span class="sxs-lookup"><span data-stu-id="1018b-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![Na folha de visão geral de seu aplicativo, escolha Início Rápido, Obter o código para monitorar minhas páginas da Web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="1018b-152">Insira o trecho de código no título dos arquivos HTML.</span><span class="sxs-lookup"><span data-stu-id="1018b-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="1018b-153">Exibir dados do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="1018b-153">View client-side data</span></span>
<span data-ttu-id="1018b-154">Abra suas páginas da Web atualizadas e use-as.</span><span class="sxs-lookup"><span data-stu-id="1018b-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="1018b-155">Aguarde um ou dois minutos, retorne ao Application Insights e abra a folha de uso.</span><span class="sxs-lookup"><span data-stu-id="1018b-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="1018b-156">(Na folha Visão geral, role para baixo e clique em Uso.)</span><span class="sxs-lookup"><span data-stu-id="1018b-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="1018b-157">As métricas de sessão, usuário e exibição de página serão exibidas na folha de uso:</span><span class="sxs-lookup"><span data-stu-id="1018b-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Sessões, usuários e modos de exibição de página](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="1018b-159">[Saiba mais sobre como configurar a telemetria do lado do cliente.][usage]</span><span class="sxs-lookup"><span data-stu-id="1018b-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="1018b-160">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1018b-160">Publish your application</span></span>
<span data-ttu-id="1018b-161">Agora, publique seu aplicativo no servidor, permita que as pessoas o usem e observe a telemetria mostrada no portal.</span><span class="sxs-lookup"><span data-stu-id="1018b-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="1018b-162">Verifique se o firewall permite que seu aplicativo envie telemetria para estas portas:</span><span class="sxs-lookup"><span data-stu-id="1018b-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="1018b-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="1018b-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="1018b-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="1018b-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="1018b-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="1018b-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="1018b-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="1018b-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="1018b-167">Nos servidores Windows, instale:</span><span class="sxs-lookup"><span data-stu-id="1018b-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="1018b-168">Microsoft Visual C++ redistribuível</span><span class="sxs-lookup"><span data-stu-id="1018b-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="1018b-169">(Isso habilita os contadores de desempenho.)</span><span class="sxs-lookup"><span data-stu-id="1018b-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="1018b-170">Falhas de solicitação e exceções</span><span class="sxs-lookup"><span data-stu-id="1018b-170">Exceptions and request failures</span></span>
<span data-ttu-id="1018b-171">Exceções sem tratamento são coletadas automaticamente:</span><span class="sxs-lookup"><span data-stu-id="1018b-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="1018b-172">Para coletar dados em outras exceções, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="1018b-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="1018b-173">[Inserir chamadas a TrackException em seu código](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="1018b-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="1018b-174">[Instalar o Agente Java em seu servidor](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="1018b-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="1018b-175">Especifique os métodos que deseja inspecionar.</span><span class="sxs-lookup"><span data-stu-id="1018b-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="1018b-176">Monitorar chamadas de método e dependências externas</span><span class="sxs-lookup"><span data-stu-id="1018b-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="1018b-177">[Instale o Agente Java](app-insights-java-agent.md) para registrar métodos internos especificados e chamadas feitas por meio de JDBC, com dados de tempo.</span><span class="sxs-lookup"><span data-stu-id="1018b-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="1018b-178">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="1018b-178">Performance counters</span></span>
<span data-ttu-id="1018b-179">Na folha Visão geral, role para baixo e clique no bloco **Servidores**.</span><span class="sxs-lookup"><span data-stu-id="1018b-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="1018b-180">Você verá uma variedade de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="1018b-180">You'll see a range of performance counters.</span></span>

![Role para baixo e clique no bloco Servidores](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="1018b-182">Personalizar a coleta do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="1018b-182">Customize performance counter collection</span></span>
<span data-ttu-id="1018b-183">Para desabilitar a coleta do conjunto padrão de contadores de desempenho, adicione o seguinte trecho no nó raiz do arquivo ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="1018b-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="1018b-184">Coletar contadores de desempenho adicionais</span><span class="sxs-lookup"><span data-stu-id="1018b-184">Collect additional performance counters</span></span>
<span data-ttu-id="1018b-185">Você pode especificar contadores de desempenho adicionais a serem coletados.</span><span class="sxs-lookup"><span data-stu-id="1018b-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="1018b-186">Contadores JMX (expostos pela Máquina Virtual Java)</span><span class="sxs-lookup"><span data-stu-id="1018b-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="1018b-187">`displayName` – o nome exibido no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1018b-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="1018b-188">`objectName` – o nome do objeto JMX.</span><span class="sxs-lookup"><span data-stu-id="1018b-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="1018b-189">`attribute` – o atributo do nome do objeto JMX a buscar</span><span class="sxs-lookup"><span data-stu-id="1018b-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="1018b-190">`type` (opcional) - o tipo do atributo do objeto JMX:</span><span class="sxs-lookup"><span data-stu-id="1018b-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="1018b-191">Padrão: um tipo simples como “int” ou “long”.</span><span class="sxs-lookup"><span data-stu-id="1018b-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="1018b-192">`composite`: os dados do contador de desempenho estão no formato “Attribute.Data”</span><span class="sxs-lookup"><span data-stu-id="1018b-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="1018b-193">`tabular`: os dados do contador de desempenho estão no formato de uma linha de tabela</span><span class="sxs-lookup"><span data-stu-id="1018b-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="1018b-194">Contadores de desempenho do Windows</span><span class="sxs-lookup"><span data-stu-id="1018b-194">Windows performance counters</span></span>
<span data-ttu-id="1018b-195">Cada [contador de desempenho do Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) é membro de uma categoria (do mesmo modo que um campo é um membro de uma classe).</span><span class="sxs-lookup"><span data-stu-id="1018b-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="1018b-196">Categorias podem ser globais, ou podem ter instâncias numeradas ou nomeadas.</span><span class="sxs-lookup"><span data-stu-id="1018b-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="1018b-197">displayName - o nome exibido no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1018b-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="1018b-198">categoryName – a categoria de contador de desempenho (objeto de desempenho) a qual este contador de desempenho está associado</span><span class="sxs-lookup"><span data-stu-id="1018b-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="1018b-199">counterName – o nome do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="1018b-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="1018b-200">instanceName – o nome da instância da categoria do contador de desempenho ou uma cadeia de caracteres vazia (""), se a categoria contém uma única instância.</span><span class="sxs-lookup"><span data-stu-id="1018b-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="1018b-201">Se categoryName é o processo, e o contador de desempenho que você gostaria de coletar faz parte do processo atual da JVM em que seu aplicativo está sendo executado, especifique `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="1018b-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="1018b-202">Seus contadores de desempenho são visíveis como métricas personalizadas em [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="1018b-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="1018b-203">Contadores de desempenho do Unix</span><span class="sxs-lookup"><span data-stu-id="1018b-203">Unix performance counters</span></span>
* <span data-ttu-id="1018b-204">[Instale o collectd com o plug-in do Application Insights](app-insights-java-collectd.md) para obter uma ampla variedade de dados de sistema e rede.</span><span class="sxs-lookup"><span data-stu-id="1018b-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="1018b-205">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="1018b-205">Availability web tests</span></span>
<span data-ttu-id="1018b-206">O Application Insights pode testar seu site em intervalos regulares para verificar ele está operante e respondendo bem.</span><span class="sxs-lookup"><span data-stu-id="1018b-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="1018b-207">[Para configurar][availability], role para baixo para clicar em Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="1018b-207">[To set up][availability], scroll down to click Availability.</span></span>

![Role para baixo, clique em Disponibilidade, em seguida, Adicionar teste na Web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="1018b-209">Se seu site ficar inativo, você obterá gráficos de tempos de resposta e também notificações por email.</span><span class="sxs-lookup"><span data-stu-id="1018b-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemplo de teste da Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="1018b-211">[Saiba mais sobre testes de disponibilidade via web.][availability]</span><span class="sxs-lookup"><span data-stu-id="1018b-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="1018b-212">Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="1018b-212">Diagnostic logs</span></span>
<span data-ttu-id="1018b-213">Se você estiver usando Logback ou Log4J (v 1.2 ou 2.0) para rastreamento, você pode enviar seus logs de rastreamento automaticamente para o Application Insights, no qual você pode explorá-los e pesquisar o conteúdo deles.</span><span class="sxs-lookup"><span data-stu-id="1018b-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="1018b-214">[Saiba mais sobre logs de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="1018b-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="1018b-215">Telemetria personalizada</span><span class="sxs-lookup"><span data-stu-id="1018b-215">Custom telemetry</span></span>
<span data-ttu-id="1018b-216">Insira algumas linhas de código em seu aplicativo Web Java para descobrir o que os usuários estão fazendo com ele, ou para ajudar a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="1018b-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="1018b-217">Você pode inserir o código tanto no JavaScript da página da Web quanto no Java do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="1018b-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="1018b-218">[Saiba mais sobre a telemetria personalizada][track]</span><span class="sxs-lookup"><span data-stu-id="1018b-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1018b-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1018b-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="1018b-220">Detectar e diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="1018b-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="1018b-221">[Adicione telemetria do cliente Web][usage] para obter a telemetria de desempenho do cliente Web.</span><span class="sxs-lookup"><span data-stu-id="1018b-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="1018b-222">[Configure os testes da Web][availability] para certificar-se de manter seu aplicativo operante e responsivo.</span><span class="sxs-lookup"><span data-stu-id="1018b-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="1018b-223">[Pesquise eventos e logs][diagnostic] para ajudar a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="1018b-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="1018b-224">[Capturar rastreamentos do Log4J ou Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="1018b-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="1018b-225">Acompanhar uso</span><span class="sxs-lookup"><span data-stu-id="1018b-225">Track usage</span></span>
* <span data-ttu-id="1018b-226">[Adicione telemetria do cliente Web][usage] para monitorar modos de exibição de página e métricas de usuário básico.</span><span class="sxs-lookup"><span data-stu-id="1018b-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="1018b-227">[Acompanhe métricas e eventos personalizados](app-insights-web-track-usage.md) para saber mais sobre como o aplicativo é usado, tanto no cliente quanto no servidor.</span><span class="sxs-lookup"><span data-stu-id="1018b-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
