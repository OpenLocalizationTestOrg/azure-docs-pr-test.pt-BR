---
title: "análise de aplicativo da web aaaJava com o Azure Application Insights | Microsoft Docs"
description: 'Monitoramento de desempenho de aplicativos usando o Application Insights para aplicativos Web Java. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="bd4e2-103">Introdução ao Application Insights em um projeto Web Java</span><span class="sxs-lookup"><span data-stu-id="bd4e2-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="bd4e2-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) é um serviço de análise extensível para desenvolvedores da web que ajuda você a entender o uso do seu aplicativo ao vivo e desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="bd4e2-105">Usá-la também[detectar e diagnosticar problemas de desempenho e exceções](app-insights-detect-triage-diagnose.md), e [escrever código] [ api] tootrack que os usuários fazem com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![dados de exemplo](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="bd4e2-107">O Application Insights oferece suporte a aplicativos Java em execução no Windows, no Unix ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="bd4e2-108">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-108">You need:</span></span>

* <span data-ttu-id="bd4e2-109">Oracle JRE 1.6 ou posterior, ou então JRE Zulu 1.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="bd4e2-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="bd4e2-110">Uma assinatura muito[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="bd4e2-111">*Se você tiver um aplicativo web que já está ativo, você pode seguir procedimento alternativo Olá muito[adicionar Olá SDK em tempo de execução no servidor de web hello](app-insights-java-live.md). Essa alternativa evita a recompilação código hello, mas você não obterá a atividade de usuário Olá opção toowrite código tootrack.*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="bd4e2-112">1. Obter uma chave de instrumentação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="bd4e2-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="bd4e2-113">Entrar toohello [portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bd4e2-114">Crie um recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-114">Create an Application Insights resource.</span></span> <span data-ttu-id="bd4e2-115">Defina o aplicativo de web tooJava do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-115">Set hello application type tooJava web application.</span></span>

    ![Preencha um nome, escolha o aplicativo Java da Web e clique em Criar](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="bd4e2-117">Localize a chave de instrumentação de saudação do novo recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="bd4e2-118">Você precisará toopaste essa chave em seu projeto de código em breve.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="bd4e2-120">2. Adicionar hello SDK do Application Insights para projeto de tooyour de Java</span><span class="sxs-lookup"><span data-stu-id="bd4e2-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="bd4e2-121">*Escolha o modo apropriado de saudação do seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="bd4e2-122">Se você estiver usando o Eclipse toocreate um projeto Web dinâmico ou Maven...</span><span class="sxs-lookup"><span data-stu-id="bd4e2-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="bd4e2-123">Saudação de uso [SDK do Application Insights para Java plug-in][eclipse].</span><span class="sxs-lookup"><span data-stu-id="bd4e2-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="bd4e2-124">Se você estiver usando o Maven...</span><span class="sxs-lookup"><span data-stu-id="bd4e2-124">If you're using Maven...</span></span>
<span data-ttu-id="bd4e2-125">Se o projeto já está definido toouse Maven para compilação, mescle Olá arquivo de pom.xml de tooyour de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="bd4e2-126">Em seguida, atualizar Olá projeto dependências tooget Olá binários baixados.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="bd4e2-127">*Erros de build ou validação de soma de verificação?*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="bd4e2-128">Tente usar uma versão específica, como: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="bd4e2-129">Você encontrará versão mais recente Olá Olá [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) ou no nosso [artefatos Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="bd4e2-130">*Necessário tooupdate tooa SDK novo?*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="bd4e2-131">Atualize as dependências do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="bd4e2-132">Se você estiver usando o Gradle...</span><span class="sxs-lookup"><span data-stu-id="bd4e2-132">If you're using Gradle...</span></span>
<span data-ttu-id="bd4e2-133">Se o projeto já está definido toouse Gradle para compilação, mescle Olá arquivo de gradle de tooyour de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="bd4e2-134">Atualização Olá projeto dependências tooget Olá binários baixados.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="bd4e2-135">*Erros de validação de soma de verificação ou compilação? Tente usar uma versão específica, como: ** `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="bd4e2-136">*Você encontrará versão mais recente Olá Olá [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="bd4e2-137">*tooupdate tooa novo SDK*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="bd4e2-138">Atualize as dependências do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="bd4e2-139">Caso contrário...</span><span class="sxs-lookup"><span data-stu-id="bd4e2-139">Otherwise ...</span></span>
<span data-ttu-id="bd4e2-140">Adicione manualmente Olá SDK:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="bd4e2-141">Baixar Olá [SDK do Application Insights para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="bd4e2-142">Extrair os binários de saudação do arquivo zip de saudação e adicioná-los tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="bd4e2-143">Perguntas...</span><span class="sxs-lookup"><span data-stu-id="bd4e2-143">Questions...</span></span>
* <span data-ttu-id="bd4e2-144">*Qual é a relação de saudação entre hello `-core` e `-web` componentes ZIP Olá?*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="bd4e2-145">`applicationinsights-core`Fornece Olá API vazio.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="bd4e2-146">Você sempre precisa desse componente.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-146">You always need this component.</span></span>
  * <span data-ttu-id="bd4e2-147">`applicationinsights-web` fornece métricas que rastreiam as contagens de solicitação de HTTP e tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="bd4e2-148">Você poderá omitir esse componente se não quiser que a telemetria seja coletada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="bd4e2-149">Por exemplo, se você quiser toowrite seus próprios.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="bd4e2-150">*Olá tooupdate SDK quando publicamos as alterações*</span><span class="sxs-lookup"><span data-stu-id="bd4e2-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="bd4e2-151">Baixar hello mais recente [SDK do Application Insights para Java](https://aka.ms/qqkaq6) e substituir Olá antigas.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="bd4e2-152">As alterações são descritas no hello [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="bd4e2-153">3. Adicione um arquivo xml do Application Insights</span><span class="sxs-lookup"><span data-stu-id="bd4e2-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="bd4e2-154">Adicionar pasta de recursos do ApplicationInsights.xml toohello em seu projeto, ou verifique se que ele é adicionado o caminho de classe de implantação do projeto tooyour.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="bd4e2-155">Copie Olá XML a seguir para ele.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="bd4e2-156">Substitua a chave de instrumentação Olá que você obteve Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="bd4e2-157">chave de instrumentação de saudação enviada juntamente com todos os itens de telemetria e informa ao Application Insights toodisplay-lo em seu recurso.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="bd4e2-158">Olá componente de solicitação HTTP é opcional.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="bd4e2-159">Ele envia automaticamente telemetria sobre solicitações e o portal de toohello de tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="bd4e2-160">Correlação de eventos é um componente de solicitação HTTP de toohello de adição.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="bd4e2-161">Ele atribui uma solicitação de tooeach identificador recebida pelo servidor de saudação e adiciona esse identificador como um item de tooevery de propriedade de telemetria como propriedade Olá 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="bd4e2-162">Ele permite toocorrelate telemetria de saudação associada com cada solicitação, definindo um filtro no [pesquisa diagnóstica][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="bd4e2-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="bd4e2-163">Olá Application Insights chave pode ser passada dinamicamente de saudação portal do Azure como uma propriedade do sistema (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="bd4e2-164">Se não houver uma propriedade definida, ele verificará a variável de ambiente (APPLICATION_INSIGHTS_IKEY) nas Configurações do Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="bd4e2-165">Se ambas as propriedades de saudação são indefinidas, padrão Olá InstrumentationKey é usado no ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="bd4e2-166">Esta sequência ajuda toomanage InstrumentationKeys diferentes para diferentes ambientes dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="bd4e2-167">Chave de instrumentação modos alternativos tooset Olá</span><span class="sxs-lookup"><span data-stu-id="bd4e2-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="bd4e2-168">SDK do Application Insights procura chave Olá nesta ordem:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="bd4e2-169">Propriedade do sistema: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="bd4e2-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="bd4e2-170">Variável de ambiente: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="bd4e2-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="bd4e2-171">Arquivo de configuração: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="bd4e2-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="bd4e2-172">Você também pode [defini-lo no código](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="bd4e2-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="bd4e2-173">4. Adicionar um filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="bd4e2-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="bd4e2-174">a última etapa de configuração Olá permite toolog de componente de solicitação HTTP Olá cada solicitação da web.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="bd4e2-175">(Não necessárias se você quiser apenas API bare hello.)</span><span class="sxs-lookup"><span data-stu-id="bd4e2-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="bd4e2-176">Localize e abra o arquivo Web. XML de saudação em seu projeto e saudação de mesclagem após o código sob o nó de aplicativo web hello, onde os filtros de aplicativo estão configurados.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="bd4e2-177">resultados mais precisos tooget hello, filtro Olá devem ser mapeados antes de todos os outros filtros.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="bd4e2-178">Se você estiver usando Spring Web MVC 3.1 ou posterior</span><span class="sxs-lookup"><span data-stu-id="bd4e2-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="bd4e2-179">Editar esses elementos em *-pacote de aplicativo Insights servlet tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="bd4e2-180">Se você estiver usando o Struts 2</span><span class="sxs-lookup"><span data-stu-id="bd4e2-180">If you're using Struts 2</span></span>
<span data-ttu-id="bd4e2-181">Adicione esse arquivo de configuração do item toohello Struts (geralmente nomeado struts.xml ou default.xml struts):</span><span class="sxs-lookup"><span data-stu-id="bd4e2-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="bd4e2-182">(Se você tiver interceptores definidos em uma pilha padrão, interceptador Olá pode simplesmente ser adicionada pilha toothat).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="bd4e2-183">5. Execute seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-183">5. Run your application</span></span>
<span data-ttu-id="bd4e2-184">Ou executá-lo no modo de depuração no computador de desenvolvimento ou publicar tooyour server.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="bd4e2-185">6. Exibir sua telemetria no Application Insights</span><span class="sxs-lookup"><span data-stu-id="bd4e2-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="bd4e2-186">Retornar recurso Application Insights tooyour [portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="bd4e2-187">Dados de solicitações HTTP é exibida na folha de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="bd4e2-188">(Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)</span><span class="sxs-lookup"><span data-stu-id="bd4e2-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dados de exemplo](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="bd4e2-190">[Saiba mais sobre métricas.][metrics]</span><span class="sxs-lookup"><span data-stu-id="bd4e2-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="bd4e2-191">Clique em qualquer toosee de gráfico mais detalhada agregado métricas.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="bd4e2-192">Application Insights assume o formato Olá de solicitações HTTP para aplicativos MVC é: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="bd4e2-193">Por exemplo, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` e `GET Home/Product/sdf96vws` são agrupados em `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="bd4e2-194">Esse agrupamento habilita agregações significativas de solicitações, como o número de solicitações e o tempo médio de execução para solicitações.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="bd4e2-195">Dados de instância</span><span class="sxs-lookup"><span data-stu-id="bd4e2-195">Instance data</span></span>
<span data-ttu-id="bd4e2-196">Clique em instâncias individuais do tipo toosee uma solicitação específica.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="bd4e2-197">Dois tipos de dados são exibidos no Application Insights: dados agregados, armazenados e exibidos como médias, contagens e somas, e dados de instância ‒ relatórios individuais de solicitações HTTP, exceções, exibições de página ou eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="bd4e2-198">Ao exibir as propriedades de saudação de uma solicitação, você pode ver eventos de telemetria Olá associados a ele, como solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="bd4e2-199">Análise: linguagem de consulta poderosa</span><span class="sxs-lookup"><span data-stu-id="bd4e2-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="bd4e2-200">Como você acumular mais dados, você pode executar consultas em ambos os tooaggregate dados e toofind instâncias individuais.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="bd4e2-201">[Análise](app-insights-analytics.md) é uma ferramenta poderosa para entender o desempenho e o uso e para fins de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Exemplo de Análise](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="bd4e2-203">7. Instalar o aplicativo no servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="bd4e2-203">7. Install your app on hello server</span></span>
<span data-ttu-id="bd4e2-204">Publicar o seu servidor de toohello de aplicativo agora, permitem que pessoas usá-lo e assista a telemetria Olá aparecerão no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="bd4e2-205">Verifique se o firewall permite que seu aplicativo toosend telemetria toothese portas:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="bd4e2-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="bd4e2-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="bd4e2-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="bd4e2-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="bd4e2-208">Se o tráfego de saída precisar passar por um firewall, defina as propriedades do sistema `http.proxyHost` e `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="bd4e2-209">Nos servidores Windows, instale:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="bd4e2-210">Microsoft Visual C++ redistribuível</span><span class="sxs-lookup"><span data-stu-id="bd4e2-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="bd4e2-211">(Esse componente habilita contadores de desempenho.)</span><span class="sxs-lookup"><span data-stu-id="bd4e2-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="bd4e2-212">Falhas de solicitação e exceções</span><span class="sxs-lookup"><span data-stu-id="bd4e2-212">Exceptions and request failures</span></span>
<span data-ttu-id="bd4e2-213">Exceções sem tratamento são coletadas automaticamente:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-213">Unhandled exceptions are automatically collected:</span></span>

![Abra Configurações, Falhas](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="bd4e2-215">dados toocollect outras exceções, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="bd4e2-216">[Inserir chama tootrackException() no seu código][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="bd4e2-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="bd4e2-217">[Instalar Olá agente Java em seu servidor](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="bd4e2-218">Você especificar métodos Olá toowatch desejado.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="bd4e2-219">Monitorar chamadas de método e dependências externas</span><span class="sxs-lookup"><span data-stu-id="bd4e2-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="bd4e2-220">[Instalar Olá agente Java](app-insights-java-agent.md) toolog especificado métodos internos e as chamadas feitas por meio do JDBC, com dados de tempo.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="bd4e2-221">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="bd4e2-221">Performance counters</span></span>
<span data-ttu-id="bd4e2-222">Abra **configurações**, **servidores**, toosee uma variedade de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="bd4e2-223">Personalizar a coleta do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="bd4e2-223">Customize performance counter collection</span></span>
<span data-ttu-id="bd4e2-224">coleção de toodisable de conjunto de contadores de desempenho padrão Olá adicionar Olá código sob o nó de raiz de saudação do arquivo de ApplicationInsights.xml Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="bd4e2-225">Coletar contadores de desempenho adicionais</span><span class="sxs-lookup"><span data-stu-id="bd4e2-225">Collect additional performance counters</span></span>
<span data-ttu-id="bd4e2-226">Você pode especificar toobe de contadores de desempenho coletados.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="bd4e2-227">Contadores do JMX (expostas pelo Olá Máquina Virtual Java)</span><span class="sxs-lookup"><span data-stu-id="bd4e2-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="bd4e2-228">`displayName`– nome hello exibido no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="bd4e2-229">`objectName`– nome do objeto Olá JMX.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="bd4e2-230">`attribute`– atributo Olá Olá toofetch de nome de objeto JMX</span><span class="sxs-lookup"><span data-stu-id="bd4e2-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="bd4e2-231">`type`(opcional) - Olá tipo de atributo do objeto JMX:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="bd4e2-232">Padrão: um tipo simples como “int” ou “long”.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="bd4e2-233">`composite`: dados do contador de desempenho hello estão no formato de saudação do 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="bd4e2-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="bd4e2-234">`tabular`: dados do contador de desempenho hello estão no formato de saudação de uma linha da tabela</span><span class="sxs-lookup"><span data-stu-id="bd4e2-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="bd4e2-235">Contadores de desempenho do Windows</span><span class="sxs-lookup"><span data-stu-id="bd4e2-235">Windows performance counters</span></span>
<span data-ttu-id="bd4e2-236">Cada [contador de desempenho do Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) é um membro de uma categoria (em Olá mesma forma que um campo é um membro de uma classe).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="bd4e2-237">Categorias podem ser globais, ou podem ter instâncias numeradas ou nomeadas.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="bd4e2-238">displayName – nome hello exibido no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="bd4e2-239">categoryName – Olá categoria contador de desempenho (objeto de desempenho) ao qual esse contador de desempenho está associado.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="bd4e2-240">counterName – nome Olá Olá do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="bd4e2-241">instanceName – Olá nome de instância de categoria do contador de desempenho de saudação ou uma cadeia de caracteres vazia (""), se a categoria de saudação contém uma única instância.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="bd4e2-242">Se Olá categoryName é o processo e contador de desempenho de saudação você gostaria que toocollect é do processo atual de JVM Olá em que seu aplicativo é executado, especifique `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="bd4e2-243">Seus contadores de desempenho são visíveis como métricas personalizadas em [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="bd4e2-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="bd4e2-244">Contadores de desempenho do Unix</span><span class="sxs-lookup"><span data-stu-id="bd4e2-244">Unix performance counters</span></span>
* <span data-ttu-id="bd4e2-245">[Instalar collectd com plug-in Application Insights de saudação](app-insights-java-collectd.md) tooget uma ampla variedade de dados de sistema e de rede.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="bd4e2-246">Obter dados de usuário e de sessão</span><span class="sxs-lookup"><span data-stu-id="bd4e2-246">Get user and session data</span></span>
<span data-ttu-id="bd4e2-247">OK, você está enviando a telemetria do seu servidor Web.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="bd4e2-248">Agora tooget Olá visão de 360 graus completo do seu aplicativo, você pode adicionar mais monitoramento:</span><span class="sxs-lookup"><span data-stu-id="bd4e2-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="bd4e2-249">[Adicionar páginas da web a telemetria tooyour] [ usage] toomonitor página exibições e métricas de usuário.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="bd4e2-250">[Configurar testes da web] [ availability] toomake-se de que seu aplicativo permanece em tempo real e responsivo.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="bd4e2-251">Capturar rastreamentos de log</span><span class="sxs-lookup"><span data-stu-id="bd4e2-251">Capture log traces</span></span>
<span data-ttu-id="bd4e2-252">Você pode usar o Application Insights tooslice e nos dados de logs de Log4J, Logback ou outras estruturas de registro em log.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="bd4e2-253">Você pode correlacionar os logs de saudação com solicitações HTTP e outra telemetria.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="bd4e2-254">[Saiba como][javalogs].</span><span class="sxs-lookup"><span data-stu-id="bd4e2-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="bd4e2-255">Enviar sua própria telemetria</span><span class="sxs-lookup"><span data-stu-id="bd4e2-255">Send your own telemetry</span></span>
<span data-ttu-id="bd4e2-256">Agora que você instalou Olá SDK, você pode usar Olá API toosend sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="bd4e2-257">[Rastrear eventos personalizados e métricas] [ api] toolearn que os usuários estão fazendo com o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="bd4e2-258">[Pesquisar eventos e logs de] [ diagnostic] toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="bd4e2-259">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="bd4e2-259">Availability web tests</span></span>
<span data-ttu-id="bd4e2-260">Application Insights pode testar seu site em toocheck em intervalos regulares que ele está ativo e também responder.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="bd4e2-261">[tooset backup][availability], clique em testes da Web.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-261">[tooset up][availability], click Web tests.</span></span>

![Clique em Testes na Web e em Adicionar Teste na Web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="bd4e2-263">Se seu site ficar inativo, você obterá gráficos de tempos de resposta e também notificações por email.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemplo de teste da Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="bd4e2-265">[Saiba mais sobre testes de disponibilidade via web.][availability]</span><span class="sxs-lookup"><span data-stu-id="bd4e2-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="bd4e2-266">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="bd4e2-266">Questions?</span></span> <span data-ttu-id="bd4e2-267">Problemas?</span><span class="sxs-lookup"><span data-stu-id="bd4e2-267">Problems?</span></span>
[<span data-ttu-id="bd4e2-268">Solucionar problemas de Java</span><span class="sxs-lookup"><span data-stu-id="bd4e2-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="bd4e2-269">Vídeo</span><span class="sxs-lookup"><span data-stu-id="bd4e2-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="bd4e2-270">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd4e2-270">Next steps</span></span>
* [<span data-ttu-id="bd4e2-271">Monitorar chamadas de dependência</span><span class="sxs-lookup"><span data-stu-id="bd4e2-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="bd4e2-272">Monitorar os contadores de desempenho do Unix</span><span class="sxs-lookup"><span data-stu-id="bd4e2-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="bd4e2-273">Adicionar [monitoramento páginas da web de tooyour](app-insights-javascript.md) tempo de carregamento de página toomonitor, chamadas AJAX, exceções de navegador.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="bd4e2-274">Gravar [telemetria personalizada](app-insights-api-custom-events-metrics.md) tootrack uso no navegador de saudação ou no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="bd4e2-275">Criar [painéis](app-insights-dashboards.md) toobring gráficos-chave Olá juntos para seu sistema de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="bd4e2-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="bd4e2-276">Usar [Análise](app-insights-analytics.md) para consultas avançadas por telemetria a o aplicativo</span><span class="sxs-lookup"><span data-stu-id="bd4e2-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="bd4e2-277">Para saber mais, visite [Azure para desenvolvedores Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="bd4e2-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
