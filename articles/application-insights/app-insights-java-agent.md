---
title: aaaPerformance monitoramento para aplicativos da web de Java no Azure Application Insights | Microsoft Docs
description: Desempenho e monitoramento de uso estendidos do seu site Java com o Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="040a9-103">Monitorar dependências, exceções e tempos de execução em aplicativos Web em Java</span><span class="sxs-lookup"><span data-stu-id="040a9-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="040a9-104">Se você tiver [instrumentado seu aplicativo da web de Java com o Application Insights][java], você pode usar o hello agente Java tooget profundo, sem qualquer alteração de código:</span><span class="sxs-lookup"><span data-stu-id="040a9-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="040a9-105">**Dependências:** dados sobre as chamadas que seu aplicativo fizer tooother componentes, incluindo:</span><span class="sxs-lookup"><span data-stu-id="040a9-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="040a9-106">**Chamadas REST** feitas por meio de HttpClient, OkHttp e RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="040a9-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="040a9-107">**Redis** chamadas feitas pelo cliente de Jedis hello.</span><span class="sxs-lookup"><span data-stu-id="040a9-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="040a9-108">Se a chamada de saudação demora mais do que por 10, agente de saudação também busca argumentos de chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="040a9-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="040a9-109">**[Chamadas JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** – MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="040a9-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="040a9-110">Há suporte para chamadas “executeBatch”.</span><span class="sxs-lookup"><span data-stu-id="040a9-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="040a9-111">Para MySQL e PostgreSQL, se a chamada de saudação demora mais do que, por 10 Olá agente se reporta o plano de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="040a9-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="040a9-112">**Exceções capturadas:** dados sobre exceções que são manipuladas pelo código.</span><span class="sxs-lookup"><span data-stu-id="040a9-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="040a9-113">**Tempo de execução do método:** dados sobre Olá tempo métodos específicos de tooexecute usa.</span><span class="sxs-lookup"><span data-stu-id="040a9-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="040a9-114">Agente de Java Olá toouse, você instalá-lo em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="040a9-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="040a9-115">Seus aplicativos web devem ser instrumentados com hello [Java SDK do Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="040a9-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="040a9-116">Instalar o agente do hello Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="040a9-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="040a9-117">Na máquina de saudação executando o servidor de Java, [baixar agente Olá](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="040a9-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="040a9-118">Editar script de inicialização de servidor de aplicativo hello e, em seguida, adicione Olá JVM a seguir:</span><span class="sxs-lookup"><span data-stu-id="040a9-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="040a9-119">`javaagent:`*arquivo JAR do caminho completo toohello agent*</span><span class="sxs-lookup"><span data-stu-id="040a9-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="040a9-120">Por exemplo, no Tomcat em um computador Linux:</span><span class="sxs-lookup"><span data-stu-id="040a9-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="040a9-121">Reinicie o servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="040a9-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="040a9-122">Configurar o agente de saudação</span><span class="sxs-lookup"><span data-stu-id="040a9-122">Configure hello agent</span></span>
<span data-ttu-id="040a9-123">Crie um arquivo chamado `AI-Agent.xml` e colocá-lo em Olá mesma pasta que o arquivo JAR do hello agente.</span><span class="sxs-lookup"><span data-stu-id="040a9-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="040a9-124">Definir o conteúdo de saudação do arquivo xml de saudação.</span><span class="sxs-lookup"><span data-stu-id="040a9-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="040a9-125">Editar saudação tooinclude de exemplo a seguir ou omita recursos Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="040a9-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="040a9-126">Você tem a exceção de relatórios tooenable e o intervalo de método para métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="040a9-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="040a9-127">Por padrão, `reportExecutionTime` é true e `reportCaughtExceptions` é false.</span><span class="sxs-lookup"><span data-stu-id="040a9-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="040a9-128">Dados de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="040a9-128">View hello data</span></span>
<span data-ttu-id="040a9-129">Em Olá recurso do Application Insights, agregados tempos de execução dependência e o método remotos aparece [em Olá desempenho bloco][metrics].</span><span class="sxs-lookup"><span data-stu-id="040a9-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="040a9-130">toosearch para instâncias individuais de dependência, a exceção e o método de relatórios, abra [pesquisa][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="040a9-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="040a9-131">[Diagnosticando problemas de dependência – Saiba mais](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="040a9-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="040a9-132">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="040a9-132">Questions?</span></span> <span data-ttu-id="040a9-133">Problemas?</span><span class="sxs-lookup"><span data-stu-id="040a9-133">Problems?</span></span>
* <span data-ttu-id="040a9-134">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="040a9-134">No data?</span></span> [<span data-ttu-id="040a9-135">Definir exceções de firewall</span><span class="sxs-lookup"><span data-stu-id="040a9-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="040a9-136">Solucionar problemas de Java</span><span class="sxs-lookup"><span data-stu-id="040a9-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
