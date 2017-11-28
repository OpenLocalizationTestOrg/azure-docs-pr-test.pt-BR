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
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="34940-103">Explore os logs de rastreamento de Java no Application Insights</span><span class="sxs-lookup"><span data-stu-id="34940-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="34940-104">Se você estiver usando Log4J ou Logback (v 1.2 ou 2.0) para rastreamento, você pode ter seus logs de rastreamento enviados automaticamente tooApplication Insights onde você pode explorar e pesquisá-los.</span><span class="sxs-lookup"><span data-stu-id="34940-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="34940-105">Instalar Olá SDK de Java</span><span class="sxs-lookup"><span data-stu-id="34940-105">Install hello Java SDK</span></span>

<span data-ttu-id="34940-106">Instale o [SDK do Application Insights para Java][java] se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="34940-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="34940-107">(Se você não deseja solicitações tootrack HTTP, você pode omitir a maioria hello. XML do arquivo de configuração, mas você deve incluir pelo menos Olá `InstrumentationKey` elemento.</span><span class="sxs-lookup"><span data-stu-id="34940-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="34940-108">Você também deve chamar `new TelemetryClient()` tooinitialize Olá SDK.)</span><span class="sxs-lookup"><span data-stu-id="34940-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="34940-109">Adicionar projeto de tooyour de bibliotecas de registro em log</span><span class="sxs-lookup"><span data-stu-id="34940-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="34940-110">*Escolha o modo apropriado de saudação do seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="34940-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="34940-111">Se você estiver usando o Maven...</span><span class="sxs-lookup"><span data-stu-id="34940-111">If you're using Maven...</span></span>
<span data-ttu-id="34940-112">Se o projeto já está definido toouse Maven para compilação, mescle uma saudação trechos de código a seguir no arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="34940-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="34940-113">Em seguida, atualize as dependências do projeto hello, binários de saudação tooget baixados.</span><span class="sxs-lookup"><span data-stu-id="34940-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="34940-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="34940-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="34940-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="34940-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="34940-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="34940-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="34940-117">Se você estiver usando o Gradle...</span><span class="sxs-lookup"><span data-stu-id="34940-117">If you're using Gradle...</span></span>
<span data-ttu-id="34940-118">Se seu projeto já está definido toouse Gradle para compilação, adicione uma saudação toohello linhas a seguir `dependencies` grupo em seu arquivo gradle:</span><span class="sxs-lookup"><span data-stu-id="34940-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="34940-119">Em seguida, atualize as dependências do projeto hello, binários de saudação tooget baixados.</span><span class="sxs-lookup"><span data-stu-id="34940-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="34940-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="34940-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="34940-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="34940-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="34940-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="34940-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="34940-123">Caso contrário...</span><span class="sxs-lookup"><span data-stu-id="34940-123">Otherwise ...</span></span>
<span data-ttu-id="34940-124">Baixar e extrair appender apropriado hello, adicionar Olá biblioteca apropriada tooyour projeto:</span><span class="sxs-lookup"><span data-stu-id="34940-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="34940-125">Agente</span><span class="sxs-lookup"><span data-stu-id="34940-125">Logger</span></span> | <span data-ttu-id="34940-126">Baixar</span><span class="sxs-lookup"><span data-stu-id="34940-126">Download</span></span> | <span data-ttu-id="34940-127">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="34940-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34940-128">Logback</span><span class="sxs-lookup"><span data-stu-id="34940-128">Logback</span></span> |[<span data-ttu-id="34940-129">SDK com appender de Logback</span><span class="sxs-lookup"><span data-stu-id="34940-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="34940-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="34940-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="34940-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="34940-131">Log4J v2.0</span></span> |[<span data-ttu-id="34940-132">SDK com appender de Log4J v2</span><span class="sxs-lookup"><span data-stu-id="34940-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="34940-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="34940-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="34940-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="34940-134">Log4j v1.2</span></span> |[<span data-ttu-id="34940-135">SDK com appender de Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="34940-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="34940-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="34940-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="34940-137">Adicionar a estrutura do registro em log do appender tooyour Olá</span><span class="sxs-lookup"><span data-stu-id="34940-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="34940-138">toostart obtendo rastreamentos, mesclagem Olá relevantes trecho de código do código toohello Log4J ou Logback arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="34940-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="34940-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="34940-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="34940-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="34940-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="34940-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="34940-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="34940-142">appenders do Application Insights Olá podem ser referenciadas por qualquer agente configurado, mas não necessariamente pelo agente de raiz da saudação (conforme mostrado nos exemplos de código Olá acima).</span><span class="sxs-lookup"><span data-stu-id="34940-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="34940-143">Explorar os rastreamentos no portal do Application Insights Olá</span><span class="sxs-lookup"><span data-stu-id="34940-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="34940-144">Agora que você configurou seu projeto toosend rastreamentos tooApplication Insights, você pode exibir e pesquisar esses rastreamentos no portal do Application Insights hello, em Olá [pesquisa] [ diagnostic] folha.</span><span class="sxs-lookup"><span data-stu-id="34940-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![No portal do Application Insights hello, abra a pesquisa](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="34940-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="34940-146">Next steps</span></span>
<span data-ttu-id="34940-147">[Usando a Pesquisa no Application Insights][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="34940-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


