---
title: logs de aaaExplore rastreamento Java no Azure Application Insights | Microsoft Docs
description: Pesquisar rastreamentos Log4J ou Logback no Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a>Explore os logs de rastreamento de Java no Application Insights
Se você estiver usando Log4J ou Logback (v 1.2 ou 2.0) para rastreamento, você pode ter seus logs de rastreamento enviados automaticamente tooApplication Insights onde você pode explorar e pesquisá-los.

## <a name="install-hello-java-sdk"></a>Instalar Olá SDK de Java

Instale o [SDK do Application Insights para Java][java] se ainda não tiver feito isso.

(Se você não deseja solicitações tootrack HTTP, você pode omitir a maioria hello. XML do arquivo de configuração, mas você deve incluir pelo menos Olá `InstrumentationKey` elemento. Você também deve chamar `new TelemetryClient()` tooinitialize Olá SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Adicionar projeto de tooyour de bibliotecas de registro em log
*Escolha o modo apropriado de saudação do seu projeto.*

#### <a name="if-youre-using-maven"></a>Se você estiver usando o Maven...
Se o projeto já está definido toouse Maven para compilação, mescle uma saudação trechos de código a seguir no arquivo pom.xml.

Em seguida, atualize as dependências do projeto hello, binários de saudação tooget baixados.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Se você estiver usando o Gradle...
Se seu projeto já está definido toouse Gradle para compilação, adicione uma saudação toohello linhas a seguir `dependencies` grupo em seu arquivo gradle:

Em seguida, atualize as dependências do projeto hello, binários de saudação tooget baixados.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J v1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>Caso contrário...
Baixar e extrair appender apropriado hello, adicionar Olá biblioteca apropriada tooyour projeto:

| Agente | Baixar | Biblioteca |
| --- | --- | --- |
| Logback |[SDK com appender de Logback](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J v2.0 |[SDK com appender de Log4J v2](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J v1.2 |[SDK com appender de Log4J v1.2](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Adicionar a estrutura do registro em log do appender tooyour Olá
toostart obtendo rastreamentos, mesclagem Olá relevantes trecho de código do código toohello Log4J ou Logback arquivo de configuração: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

*Log4J v1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

appenders do Application Insights Olá podem ser referenciadas por qualquer agente configurado, mas não necessariamente pelo agente de raiz da saudação (conforme mostrado nos exemplos de código Olá acima).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Explorar os rastreamentos no portal do Application Insights Olá
Agora que você configurou seu projeto toosend rastreamentos tooApplication Insights, você pode exibir e pesquisar esses rastreamentos no portal do Application Insights hello, em Olá [pesquisa] [ diagnostic] folha.

![No portal do Application Insights hello, abra a pesquisa](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Próximas etapas
[Usando a Pesquisa no Application Insights][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


