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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Monitorar dependências, exceções e tempos de execução em aplicativos Web em Java


Se você tiver [instrumentado seu aplicativo da web de Java com o Application Insights][java], você pode usar o hello agente Java tooget profundo, sem qualquer alteração de código:

* **Dependências:** dados sobre as chamadas que seu aplicativo fizer tooother componentes, incluindo:
  * **Chamadas REST** feitas por meio de HttpClient, OkHttp e RestTemplate (Spring).
  * **Redis** chamadas feitas pelo cliente de Jedis hello. Se a chamada de saudação demora mais do que por 10, agente de saudação também busca argumentos de chamada de saudação.
  * **[Chamadas JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** – MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby DB. Há suporte para chamadas “executeBatch”. Para MySQL e PostgreSQL, se a chamada de saudação demora mais do que, por 10 Olá agente se reporta o plano de consulta hello.
* **Exceções capturadas:** dados sobre exceções que são manipuladas pelo código.
* **Tempo de execução do método:** dados sobre Olá tempo métodos específicos de tooexecute usa.

Agente de Java Olá toouse, você instalá-lo em seu servidor. Seus aplicativos web devem ser instrumentados com hello [Java SDK do Application Insights][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Instalar o agente do hello Application Insights para Java
1. Na máquina de saudação executando o servidor de Java, [baixar agente Olá](https://aka.ms/aijavasdk).
2. Editar script de inicialização de servidor de aplicativo hello e, em seguida, adicione Olá JVM a seguir:
   
    `javaagent:`*arquivo JAR do caminho completo toohello agent*
   
    Por exemplo, no Tomcat em um computador Linux:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Reinicie o servidor de aplicativos.

## <a name="configure-hello-agent"></a>Configurar o agente de saudação
Crie um arquivo chamado `AI-Agent.xml` e colocá-lo em Olá mesma pasta que o arquivo JAR do hello agente.

Definir o conteúdo de saudação do arquivo xml de saudação. Editar saudação tooinclude de exemplo a seguir ou omita recursos Olá desejado.

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

Você tem a exceção de relatórios tooenable e o intervalo de método para métodos individuais.

Por padrão, `reportExecutionTime` é true e `reportCaughtExceptions` é false.

## <a name="view-hello-data"></a>Dados de saudação do modo de exibição
Em Olá recurso do Application Insights, agregados tempos de execução dependência e o método remotos aparece [em Olá desempenho bloco][metrics].

toosearch para instâncias individuais de dependência, a exceção e o método de relatórios, abra [pesquisa][diagnostic].

[Diagnosticando problemas de dependência – Saiba mais](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Perguntas? Problemas?
* Não há dados? [Definir exceções de firewall](app-insights-ip-addresses.md)
* [Solucionar problemas de Java](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
