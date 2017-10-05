---
title: Explorar os logs de rastreamento do Java no Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 5baba3deaf58a1a24995c60381592a9c2ffefd81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="70adf-103">Explore os logs de rastreamento de Java no Application Insights</span><span class="sxs-lookup"><span data-stu-id="70adf-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="70adf-104">Se você estiver usando Logback ou Log4J (v 1.2 ou 2.0) para rastreamento, você pode enviar seus logs de rastreamento automaticamente para o Application Insights, no qual você pode explorá-los e pesquisar o conteúdo deles.</span><span class="sxs-lookup"><span data-stu-id="70adf-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="70adf-105">Instalar o SDK do Java</span><span class="sxs-lookup"><span data-stu-id="70adf-105">Install the Java SDK</span></span>

<span data-ttu-id="70adf-106">Instale o [SDK do Application Insights para Java][java] se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="70adf-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="70adf-107">(Se não quiser rastrear as solicitações HTTP, você poderá omitir a maior parte do arquivo de configuração .xml, mas deverá incluir pelo menos o elemento `InstrumentationKey`.</span><span class="sxs-lookup"><span data-stu-id="70adf-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="70adf-108">Você também deve chamar `new TelemetryClient()` para inicializar o SDK.)</span><span class="sxs-lookup"><span data-stu-id="70adf-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="70adf-109">Adicionar bibliotecas de log ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="70adf-109">Add logging libraries to your project</span></span>
<span data-ttu-id="70adf-110">*Escolha o modo apropriado para seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="70adf-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="70adf-111">Se você estiver usando o Maven...</span><span class="sxs-lookup"><span data-stu-id="70adf-111">If you're using Maven...</span></span>
<span data-ttu-id="70adf-112">Se o seu projeto já estiver configurado para usar o Maven para compilação, realize a mesclagem de um dos seguintes trechos de código ao seu arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="70adf-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="70adf-113">Em seguida, atualize as dependências do projeto para obter os binários baixados.</span><span class="sxs-lookup"><span data-stu-id="70adf-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="70adf-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="70adf-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="70adf-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="70adf-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="70adf-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="70adf-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="70adf-117">Se você estiver usando o Gradle...</span><span class="sxs-lookup"><span data-stu-id="70adf-117">If you're using Gradle...</span></span>
<span data-ttu-id="70adf-118">Se seu projeto já está configurado para usar Gradle para compilação, adicione uma das linhas a seguir para o grupo `dependencies` em seu arquivo build.gradle:</span><span class="sxs-lookup"><span data-stu-id="70adf-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="70adf-119">Em seguida, atualize as dependências do projeto para obter os binários baixados.</span><span class="sxs-lookup"><span data-stu-id="70adf-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="70adf-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="70adf-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="70adf-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="70adf-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="70adf-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="70adf-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="70adf-123">Caso contrário...</span><span class="sxs-lookup"><span data-stu-id="70adf-123">Otherwise ...</span></span>
<span data-ttu-id="70adf-124">Baixe e extraia o appender apropriado, em seguida adicione a biblioteca apropriada ao seu projeto:</span><span class="sxs-lookup"><span data-stu-id="70adf-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="70adf-125">Agente</span><span class="sxs-lookup"><span data-stu-id="70adf-125">Logger</span></span> | <span data-ttu-id="70adf-126">Baixar</span><span class="sxs-lookup"><span data-stu-id="70adf-126">Download</span></span> | <span data-ttu-id="70adf-127">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="70adf-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70adf-128">Logback</span><span class="sxs-lookup"><span data-stu-id="70adf-128">Logback</span></span> |[<span data-ttu-id="70adf-129">SDK com appender de Logback</span><span class="sxs-lookup"><span data-stu-id="70adf-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="70adf-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="70adf-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="70adf-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="70adf-131">Log4J v2.0</span></span> |[<span data-ttu-id="70adf-132">SDK com appender de Log4J v2</span><span class="sxs-lookup"><span data-stu-id="70adf-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="70adf-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="70adf-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="70adf-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="70adf-134">Log4j v1.2</span></span> |[<span data-ttu-id="70adf-135">SDK com appender de Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="70adf-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="70adf-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="70adf-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="70adf-137">Adicionar o appender à sua estrutura de log</span><span class="sxs-lookup"><span data-stu-id="70adf-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="70adf-138">Para começar a obter rastreamentos, mescle o trecho de código relevante ao arquivo de configuração Log4J ou Logback:</span><span class="sxs-lookup"><span data-stu-id="70adf-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="70adf-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="70adf-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="70adf-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="70adf-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="70adf-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="70adf-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="70adf-142">Os appenders Application Insights podem ser referenciados por qualquer agente configurado e não necessariamente pelo agente raiz (conforme mostrado nos exemplos de código acima).</span><span class="sxs-lookup"><span data-stu-id="70adf-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="70adf-143">Explorar seus rastreamentos no portal do Application Insights</span><span class="sxs-lookup"><span data-stu-id="70adf-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="70adf-144">Agora que você configurou o projeto para enviar os rastreamentos para o Application Insights, é possível exibir e pesquisar esses rastreamentos no portal do Application Insights, na folha [Pesquisa][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="70adf-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![No portal do Application Insights, abra a Pesquisa](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="70adf-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70adf-146">Next steps</span></span>
<span data-ttu-id="70adf-147">[Usando a Pesquisa no Application Insights][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="70adf-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


