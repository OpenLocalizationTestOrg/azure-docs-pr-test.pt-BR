---
title: Monitoramento de desempenho de aplicativos Web de Java no Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="d2a78-103">Monitorar dependências, exceções e tempos de execução em aplicativos Web em Java</span><span class="sxs-lookup"><span data-stu-id="d2a78-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="d2a78-104">Se você [instrumentou seu aplicativo Web em Java com o Application Insights][java], será possível usar o Agente Java para obter uma visão mais aprofundada, sem nenhuma alteração de código:</span><span class="sxs-lookup"><span data-stu-id="d2a78-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="d2a78-105">**Dependências:** dados sobre chamadas de seu aplicativo a outros componentes, incluindo:</span><span class="sxs-lookup"><span data-stu-id="d2a78-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="d2a78-106">**Chamadas REST** feitas por meio de HttpClient, OkHttp e RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="d2a78-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="d2a78-107">**Redis** feitas por meio do cliente Jedis.</span><span class="sxs-lookup"><span data-stu-id="d2a78-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="d2a78-108">Se a chamada demorar mais de 10 segundos, o agente também buscará os argumentos da chamada.</span><span class="sxs-lookup"><span data-stu-id="d2a78-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="d2a78-109">**[Chamadas JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** – MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="d2a78-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="d2a78-110">Há suporte para chamadas “executeBatch”.</span><span class="sxs-lookup"><span data-stu-id="d2a78-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="d2a78-111">Para MySQL e PostgreSQL, se a chamada levar mais de 10 segundos, o agente relatará o plano de consulta.</span><span class="sxs-lookup"><span data-stu-id="d2a78-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="d2a78-112">**Exceções capturadas:** dados sobre exceções que são manipuladas pelo código.</span><span class="sxs-lookup"><span data-stu-id="d2a78-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="d2a78-113">**Tempo de execução do método:** dados sobre o tempo necessário para executar métodos específicos.</span><span class="sxs-lookup"><span data-stu-id="d2a78-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="d2a78-114">Para usar o agente Java, instale-o no servidor.</span><span class="sxs-lookup"><span data-stu-id="d2a78-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="d2a78-115">Seus aplicativos Web devem ser instrumentados com o [SDK do Java do Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="d2a78-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="d2a78-116">Instalar o agente do Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="d2a78-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="d2a78-117">No computador que está executando o servidor Java, [baixe o agente](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="d2a78-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="d2a78-118">Edite o script de inicialização do servidor de aplicativos e adicione a seguinte JVM:</span><span class="sxs-lookup"><span data-stu-id="d2a78-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="d2a78-119">`javaagent:`*caminho completo para o arquivo JAR do agente*</span><span class="sxs-lookup"><span data-stu-id="d2a78-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="d2a78-120">Por exemplo, no Tomcat em um computador Linux:</span><span class="sxs-lookup"><span data-stu-id="d2a78-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="d2a78-121">Reinicie o servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d2a78-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="d2a78-122">Configurar o agente</span><span class="sxs-lookup"><span data-stu-id="d2a78-122">Configure the agent</span></span>
<span data-ttu-id="d2a78-123">Crie um arquivo chamado `AI-Agent.xml` e coloque-o na mesma pasta que o arquivo JAR do agente.</span><span class="sxs-lookup"><span data-stu-id="d2a78-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="d2a78-124">Defina o conteúdo do arquivo xml.</span><span class="sxs-lookup"><span data-stu-id="d2a78-124">Set the content of the xml file.</span></span> <span data-ttu-id="d2a78-125">Edite o exemplo a seguir para incluir ou omitir os recursos desejados.</span><span class="sxs-lookup"><span data-stu-id="d2a78-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="d2a78-126">Você precisa habilitar a exceção de relatórios e o tempo de método para métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="d2a78-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="d2a78-127">Por padrão, `reportExecutionTime` é true e `reportCaughtExceptions` é false.</span><span class="sxs-lookup"><span data-stu-id="d2a78-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="d2a78-128">Exibir os dados</span><span class="sxs-lookup"><span data-stu-id="d2a78-128">View the data</span></span>
<span data-ttu-id="d2a78-129">No recurso do Application Insights, a dependência remota e os tempos de execução do método agregados aparecem [no bloco Desempenho][metrics].</span><span class="sxs-lookup"><span data-stu-id="d2a78-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="d2a78-130">Para procurar instâncias individuais de dependência, exceções e relatórios de método, abra [Pesquisar][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="d2a78-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="d2a78-131">[Diagnosticando problemas de dependência – Saiba mais](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="d2a78-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="d2a78-132">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="d2a78-132">Questions?</span></span> <span data-ttu-id="d2a78-133">Problemas?</span><span class="sxs-lookup"><span data-stu-id="d2a78-133">Problems?</span></span>
* <span data-ttu-id="d2a78-134">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="d2a78-134">No data?</span></span> [<span data-ttu-id="d2a78-135">Definir exceções de firewall</span><span class="sxs-lookup"><span data-stu-id="d2a78-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="d2a78-136">Solucionar problemas de Java</span><span class="sxs-lookup"><span data-stu-id="d2a78-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
