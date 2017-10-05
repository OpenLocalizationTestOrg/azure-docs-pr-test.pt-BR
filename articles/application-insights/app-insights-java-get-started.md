---
title: "Análise de aplicativo Web Java com o Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="779da-103">Introdução ao Application Insights em um projeto Web Java</span><span class="sxs-lookup"><span data-stu-id="779da-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="779da-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) é um serviço de análise extensível para desenvolvedores da Web que ajuda você a entender o desempenho e o uso de seu aplicativo em tempo real.</span><span class="sxs-lookup"><span data-stu-id="779da-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="779da-105">Use-o para [detectar e diagnosticar exceções e problemas de desempenho](app-insights-detect-triage-diagnose.md), bem como para [escrever código][api] a fim de rastrear o que os usuários fazem com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="779da-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![dados de exemplo](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="779da-107">O Application Insights oferece suporte a aplicativos Java em execução no Windows, no Unix ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="779da-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="779da-108">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="779da-108">You need:</span></span>

* <span data-ttu-id="779da-109">Oracle JRE 1.6 ou posterior, ou então JRE Zulu 1.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="779da-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="779da-110">Uma assinatura do [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="779da-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="779da-111">*Se você tiver um aplicativo Web já em uso, siga o procedimento alternativo para [adicionar o SDK em tempo de execução ao servidor Web](app-insights-java-live.md). Essa alternativa evita a recompilação do código, mas você não obtém a opção de escrever código para rastrear a atividade do usuário.*</span><span class="sxs-lookup"><span data-stu-id="779da-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="779da-112">1. Obter uma chave de instrumentação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="779da-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="779da-113">Entre no [Portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="779da-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="779da-114">Crie um recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="779da-114">Create an Application Insights resource.</span></span> <span data-ttu-id="779da-115">Defina o tipo de aplicativo para aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="779da-115">Set the application type to Java web application.</span></span>

    ![Preencha um nome, escolha o aplicativo Java da Web e clique em Criar](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="779da-117">Localize a chave de instrumentação do novo recurso.</span><span class="sxs-lookup"><span data-stu-id="779da-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="779da-118">Você precisará colar essa chave no código de seu projeto em breve.</span><span class="sxs-lookup"><span data-stu-id="779da-118">You'll need to paste this key into your code project shortly.</span></span>

    ![Na visão geral do novo recurso, clique em Propriedades e copie a chave de instrumentação](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="779da-120">2. Adicionar o SDK do Application Insights para Java a seu projeto</span><span class="sxs-lookup"><span data-stu-id="779da-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="779da-121">*Escolha o modo apropriado para seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="779da-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="779da-122">Se você está usando o Eclipse para criar um projeto Web dinâmico ou do Maven...</span><span class="sxs-lookup"><span data-stu-id="779da-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="779da-123">Use o [plug-in SDK do Application Insights para Java][eclipse].</span><span class="sxs-lookup"><span data-stu-id="779da-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="779da-124">Se você estiver usando o Maven...</span><span class="sxs-lookup"><span data-stu-id="779da-124">If you're using Maven...</span></span>
<span data-ttu-id="779da-125">Se o seu projeto já estiver configurado para usar o Maven para compilação, realize a mesclagem do código a seguir ao seu arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="779da-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="779da-126">Em seguida, atualize as dependências do projeto para obter os binários baixados.</span><span class="sxs-lookup"><span data-stu-id="779da-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

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

* <span data-ttu-id="779da-127">*Erros de build ou validação de soma de verificação?*</span><span class="sxs-lookup"><span data-stu-id="779da-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="779da-128">Tente usar uma versão específica, como: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="779da-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="779da-129">Você encontrará a versão mais recente nas [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) ou nos nossos [artefatos Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="779da-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="779da-130">*Precisa atualizar para um novo SDK?*</span><span class="sxs-lookup"><span data-stu-id="779da-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="779da-131">Atualize as dependências do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="779da-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="779da-132">Se você estiver usando o Gradle...</span><span class="sxs-lookup"><span data-stu-id="779da-132">If you're using Gradle...</span></span>
<span data-ttu-id="779da-133">Se o seu projeto já estiver configurado para usar o Gradle para compilação, realize a mesclagem do trecho de código a seguir ao seu arquivo build.gradle.</span><span class="sxs-lookup"><span data-stu-id="779da-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="779da-134">Em seguida, atualize as dependências do projeto para obter os binários baixados.</span><span class="sxs-lookup"><span data-stu-id="779da-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="779da-135">*Erros de validação de soma de verificação ou compilação? Tente usar uma versão específica, como: ** `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="779da-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="779da-136">*Você encontrará a versão mais recente nas [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="779da-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="779da-137">*Para atualizar para um novo SDK*</span><span class="sxs-lookup"><span data-stu-id="779da-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="779da-138">Atualize as dependências do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="779da-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="779da-139">Caso contrário...</span><span class="sxs-lookup"><span data-stu-id="779da-139">Otherwise ...</span></span>
<span data-ttu-id="779da-140">Adicione manualmente o SDK:</span><span class="sxs-lookup"><span data-stu-id="779da-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="779da-141">Baixe o [SDK do Application Insights para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="779da-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="779da-142">Extraia os binários do arquivo de zip e adicione-os ao projeto.</span><span class="sxs-lookup"><span data-stu-id="779da-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="779da-143">Perguntas...</span><span class="sxs-lookup"><span data-stu-id="779da-143">Questions...</span></span>
* <span data-ttu-id="779da-144">*Qual é a relação entre `-core` e os componentes `-web` no zip?*</span><span class="sxs-lookup"><span data-stu-id="779da-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="779da-145">`applicationinsights-core` fornece a API básica.</span><span class="sxs-lookup"><span data-stu-id="779da-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="779da-146">Você sempre precisa desse componente.</span><span class="sxs-lookup"><span data-stu-id="779da-146">You always need this component.</span></span>
  * <span data-ttu-id="779da-147">`applicationinsights-web` fornece métricas que rastreiam as contagens de solicitação de HTTP e tempos de resposta.</span><span class="sxs-lookup"><span data-stu-id="779da-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="779da-148">Você poderá omitir esse componente se não quiser que a telemetria seja coletada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="779da-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="779da-149">Por exemplo, se quiser escrevê-la você mesmo.</span><span class="sxs-lookup"><span data-stu-id="779da-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="779da-150">*Para atualizar o SDK ao publicar alterações*</span><span class="sxs-lookup"><span data-stu-id="779da-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="779da-151">Baixe o [SDK do Application Insights para Java](https://aka.ms/qqkaq6) mais recente e substitua os antigos.</span><span class="sxs-lookup"><span data-stu-id="779da-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="779da-152">As alterações descritas nas [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="779da-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="779da-153">3. Adicione um arquivo xml do Application Insights</span><span class="sxs-lookup"><span data-stu-id="779da-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="779da-154">Adicione o ApplicationInsights.xml à pasta de recursos em seu projeto; caso contrário, verifique se ele é adicionado ao caminho de classe de implantação do projeto.</span><span class="sxs-lookup"><span data-stu-id="779da-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="779da-155">Copie o XML a seguir nele.</span><span class="sxs-lookup"><span data-stu-id="779da-155">Copy the following XML into it.</span></span>

<span data-ttu-id="779da-156">Substitua a chave de instrumentação que você obteve no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="779da-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="779da-157">A chave de instrumentação é enviada junto com todos os itens de telemetria e orienta o Application Insights a exibi-los em seu recurso.</span><span class="sxs-lookup"><span data-stu-id="779da-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="779da-158">O componente de solicitação HTTP é opcional.</span><span class="sxs-lookup"><span data-stu-id="779da-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="779da-159">Ele envia automaticamente a telemetria sobre solicitações e tempos de resposta para o portal.</span><span class="sxs-lookup"><span data-stu-id="779da-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="779da-160">A correlação de eventos é uma adição ao componente de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="779da-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="779da-161">Ele atribui um identificador a cada solicitação recebida pelo servidor e adiciona esse identificador como uma propriedade para cada item de telemetria, como a propriedade “Operation.Id”.</span><span class="sxs-lookup"><span data-stu-id="779da-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="779da-162">Ele permite que você correlacione a telemetria associada com cada solicitação, definindo um filtro na [pesquisa de diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="779da-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="779da-163">A chave do Application Insights pode ser passada dinamicamente do portal do Azure como uma propriedade do sistema (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span><span class="sxs-lookup"><span data-stu-id="779da-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="779da-164">Se não houver uma propriedade definida, ele verificará a variável de ambiente (APPLICATION_INSIGHTS_IKEY) nas Configurações do Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="779da-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="779da-165">Se ambas as propriedades estiverem indefinidas, o padrão InstrumentationKey será usado de ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="779da-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="779da-166">Essa sequência ajuda a gerenciar diferentes InstrumentationKeys para diferentes ambientes de forma dinâmica.</span><span class="sxs-lookup"><span data-stu-id="779da-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="779da-167">Maneiras alternativas para definir a chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="779da-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="779da-168">O SDK do Application Insights procura a chave nesta ordem:</span><span class="sxs-lookup"><span data-stu-id="779da-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="779da-169">Propriedade do sistema: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="779da-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="779da-170">Variável de ambiente: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="779da-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="779da-171">Arquivo de configuração: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="779da-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="779da-172">Você também pode [defini-lo no código](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="779da-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="779da-173">4. Adicionar um filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="779da-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="779da-174">A última etapa de configuração permite que o componente de solicitação HTTP registre cada solicitação da Web.</span><span class="sxs-lookup"><span data-stu-id="779da-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="779da-175">(Não obrigatório se você quiser apenas a API vazia.)</span><span class="sxs-lookup"><span data-stu-id="779da-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="779da-176">Localize e abra o arquivo web.xml em seu projeto. Em seguida, mescle o código a seguir com o nó do aplicativo Web no qual seus filtros de aplicativo estão configurados.</span><span class="sxs-lookup"><span data-stu-id="779da-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="779da-177">Para obter os resultados mais precisos, o filtro deve ser mapeado antes de todos os outros filtros.</span><span class="sxs-lookup"><span data-stu-id="779da-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="779da-178">Se você estiver usando Spring Web MVC 3.1 ou posterior</span><span class="sxs-lookup"><span data-stu-id="779da-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="779da-179">Edite estes elementos em *-servlet.xml para incluir o pacote do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="779da-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="779da-180">Se você estiver usando o Struts 2</span><span class="sxs-lookup"><span data-stu-id="779da-180">If you're using Struts 2</span></span>
<span data-ttu-id="779da-181">Adicione este item ao arquivo de configuração do Struts (geralmente chamado de struts.xml ou struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="779da-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="779da-182">(Se você tiver interceptores definidos em uma pilha padrão, o interceptador pode simplesmente ser adicionado àquela pilha.)</span><span class="sxs-lookup"><span data-stu-id="779da-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="779da-183">5. Execute seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="779da-183">5. Run your application</span></span>
<span data-ttu-id="779da-184">Execute-o no modo de depuração no computador de desenvolvimento ou publique em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="779da-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="779da-185">6. Exibir sua telemetria no Application Insights</span><span class="sxs-lookup"><span data-stu-id="779da-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="779da-186">Retorne para seu recurso do Application Insights no [Portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="779da-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="779da-187">Dados de solicitações HTTP são exibidos na folha de visão geral.</span><span class="sxs-lookup"><span data-stu-id="779da-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="779da-188">(Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)</span><span class="sxs-lookup"><span data-stu-id="779da-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dados de exemplo](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="779da-190">[Saiba mais sobre métricas.][metrics]</span><span class="sxs-lookup"><span data-stu-id="779da-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="779da-191">Clique em qualquer gráfico para ver métricas agregadas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="779da-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="779da-192">O Application Insights presume que o formato de solicitações HTTP para aplicativos MVC seja: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="779da-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="779da-193">Por exemplo, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` e `GET Home/Product/sdf96vws` são agrupados em `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="779da-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="779da-194">Esse agrupamento habilita agregações significativas de solicitações, como o número de solicitações e o tempo médio de execução para solicitações.</span><span class="sxs-lookup"><span data-stu-id="779da-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="779da-195">Dados de instância</span><span class="sxs-lookup"><span data-stu-id="779da-195">Instance data</span></span>
<span data-ttu-id="779da-196">Clique em um tipo de solicitação específica para ver instâncias individuais.</span><span class="sxs-lookup"><span data-stu-id="779da-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="779da-197">Dois tipos de dados são exibidos no Application Insights: dados agregados, armazenados e exibidos como médias, contagens e somas, e dados de instância ‒ relatórios individuais de solicitações HTTP, exceções, exibições de página ou eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="779da-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="779da-198">Ao exibir as propriedades de uma solicitação, você pode ver os eventos de telemetria associados a ela, como solicitações e exceções.</span><span class="sxs-lookup"><span data-stu-id="779da-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="779da-199">Análise: linguagem de consulta poderosa</span><span class="sxs-lookup"><span data-stu-id="779da-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="779da-200">À medida que acumular mais dados, você poderá executar consultas para agregar dados e localizar instâncias individuais.</span><span class="sxs-lookup"><span data-stu-id="779da-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="779da-201">[Análise](app-insights-analytics.md) é uma ferramenta poderosa para entender o desempenho e o uso e para fins de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="779da-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Exemplo de Análise](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="779da-203">7. Instalar aplicativo no servidor</span><span class="sxs-lookup"><span data-stu-id="779da-203">7. Install your app on the server</span></span>
<span data-ttu-id="779da-204">Agora, publique seu aplicativo no servidor, permita que as pessoas o usem e observe a telemetria mostrada no portal.</span><span class="sxs-lookup"><span data-stu-id="779da-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="779da-205">Verifique se o firewall permite que seu aplicativo envie telemetria para estas portas:</span><span class="sxs-lookup"><span data-stu-id="779da-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="779da-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="779da-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="779da-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="779da-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="779da-208">Se o tráfego de saída precisar passar por um firewall, defina as propriedades do sistema `http.proxyHost` e `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="779da-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="779da-209">Nos servidores Windows, instale:</span><span class="sxs-lookup"><span data-stu-id="779da-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="779da-210">Microsoft Visual C++ redistribuível</span><span class="sxs-lookup"><span data-stu-id="779da-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="779da-211">(Esse componente habilita contadores de desempenho.)</span><span class="sxs-lookup"><span data-stu-id="779da-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="779da-212">Falhas de solicitação e exceções</span><span class="sxs-lookup"><span data-stu-id="779da-212">Exceptions and request failures</span></span>
<span data-ttu-id="779da-213">Exceções sem tratamento são coletadas automaticamente:</span><span class="sxs-lookup"><span data-stu-id="779da-213">Unhandled exceptions are automatically collected:</span></span>

![Abra Configurações, Falhas](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="779da-215">Para coletar dados em outras exceções, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="779da-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="779da-216">[Insira chamadas a trackException() em seu código][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="779da-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="779da-217">[Instalar o Agente Java em seu servidor](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="779da-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="779da-218">Especifique os métodos que deseja inspecionar.</span><span class="sxs-lookup"><span data-stu-id="779da-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="779da-219">Monitorar chamadas de método e dependências externas</span><span class="sxs-lookup"><span data-stu-id="779da-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="779da-220">[Instale o Agente Java](app-insights-java-agent.md) para registrar métodos internos especificados e chamadas feitas por meio de JDBC, com dados de tempo.</span><span class="sxs-lookup"><span data-stu-id="779da-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="779da-221">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="779da-221">Performance counters</span></span>
<span data-ttu-id="779da-222">Abra **Configurações**, **Servidores** para ver um intervalo de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="779da-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="779da-223">Personalizar a coleta do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="779da-223">Customize performance counter collection</span></span>
<span data-ttu-id="779da-224">Para desabilitar a coleta do conjunto padrão de contadores de desempenho, adicione o seguinte trecho no nó raiz do arquivo ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="779da-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="779da-225">Coletar contadores de desempenho adicionais</span><span class="sxs-lookup"><span data-stu-id="779da-225">Collect additional performance counters</span></span>
<span data-ttu-id="779da-226">Você pode especificar contadores de desempenho adicionais a serem coletados.</span><span class="sxs-lookup"><span data-stu-id="779da-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="779da-227">Contadores JMX (expostos pela Máquina Virtual Java)</span><span class="sxs-lookup"><span data-stu-id="779da-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="779da-228">`displayName` – o nome exibido no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="779da-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="779da-229">`objectName` – o nome do objeto JMX.</span><span class="sxs-lookup"><span data-stu-id="779da-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="779da-230">`attribute` – o atributo do nome do objeto JMX a buscar</span><span class="sxs-lookup"><span data-stu-id="779da-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="779da-231">`type` (opcional) - o tipo do atributo do objeto JMX:</span><span class="sxs-lookup"><span data-stu-id="779da-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="779da-232">Padrão: um tipo simples como “int” ou “long”.</span><span class="sxs-lookup"><span data-stu-id="779da-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="779da-233">`composite`: os dados do contador de desempenho estão no formato “Attribute.Data”</span><span class="sxs-lookup"><span data-stu-id="779da-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="779da-234">`tabular`: os dados do contador de desempenho estão no formato de uma linha de tabela</span><span class="sxs-lookup"><span data-stu-id="779da-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="779da-235">Contadores de desempenho do Windows</span><span class="sxs-lookup"><span data-stu-id="779da-235">Windows performance counters</span></span>
<span data-ttu-id="779da-236">Cada [contador de desempenho do Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) é membro de uma categoria (do mesmo modo que um campo é um membro de uma classe).</span><span class="sxs-lookup"><span data-stu-id="779da-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="779da-237">Categorias podem ser globais, ou podem ter instâncias numeradas ou nomeadas.</span><span class="sxs-lookup"><span data-stu-id="779da-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="779da-238">displayName - o nome exibido no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="779da-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="779da-239">categoryName – a categoria de contador de desempenho (objeto de desempenho) a qual este contador de desempenho está associado</span><span class="sxs-lookup"><span data-stu-id="779da-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="779da-240">counterName – o nome do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="779da-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="779da-241">instanceName – o nome da instância da categoria do contador de desempenho ou uma cadeia de caracteres vazia (""), se a categoria contém uma única instância.</span><span class="sxs-lookup"><span data-stu-id="779da-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="779da-242">Se categoryName é o processo, e o contador de desempenho que você gostaria de coletar faz parte do processo atual da JVM em que seu aplicativo está sendo executado, especifique `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="779da-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="779da-243">Seus contadores de desempenho são visíveis como métricas personalizadas em [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="779da-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="779da-244">Contadores de desempenho do Unix</span><span class="sxs-lookup"><span data-stu-id="779da-244">Unix performance counters</span></span>
* <span data-ttu-id="779da-245">[Instale o collectd com o plug-in do Application Insights](app-insights-java-collectd.md) para obter uma ampla variedade de dados de sistema e rede.</span><span class="sxs-lookup"><span data-stu-id="779da-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="779da-246">Obter dados de usuário e de sessão</span><span class="sxs-lookup"><span data-stu-id="779da-246">Get user and session data</span></span>
<span data-ttu-id="779da-247">OK, você está enviando a telemetria do seu servidor Web.</span><span class="sxs-lookup"><span data-stu-id="779da-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="779da-248">Agora, para ver o panorama completo do seu aplicativo, você pode adicionar um monitoramento mais:</span><span class="sxs-lookup"><span data-stu-id="779da-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="779da-249">[Adicione telemetria às suas páginas da Web][usage] para monitorar exibições de página e métricas de usuário.</span><span class="sxs-lookup"><span data-stu-id="779da-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="779da-250">[Configure os testes da Web][availability] para certificar-se de manter seu aplicativo operante e responsivo.</span><span class="sxs-lookup"><span data-stu-id="779da-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="779da-251">Capturar rastreamentos de log</span><span class="sxs-lookup"><span data-stu-id="779da-251">Capture log traces</span></span>
<span data-ttu-id="779da-252">Você pode usar o Application Insights para fracionar e dividir logs de Log4J, Logback ou outras estruturas de registros.</span><span class="sxs-lookup"><span data-stu-id="779da-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="779da-253">Você pode correlacionar os logs de solicitações HTTP e outras telemetrias.</span><span class="sxs-lookup"><span data-stu-id="779da-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="779da-254">[Saiba como][javalogs].</span><span class="sxs-lookup"><span data-stu-id="779da-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="779da-255">Enviar sua própria telemetria</span><span class="sxs-lookup"><span data-stu-id="779da-255">Send your own telemetry</span></span>
<span data-ttu-id="779da-256">Agora que você instalou o SDK, você pode usar a API para enviar sua próprias telemetrias.</span><span class="sxs-lookup"><span data-stu-id="779da-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="779da-257">[Acompanhe eventos personalizados e métricas][api] para saber o que os usuários estão fazendo com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="779da-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="779da-258">[Pesquise eventos e logs][diagnostic] para ajudar a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="779da-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="779da-259">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="779da-259">Availability web tests</span></span>
<span data-ttu-id="779da-260">O Application Insights pode testar seu site em intervalos regulares para verificar ele está operante e respondendo bem.</span><span class="sxs-lookup"><span data-stu-id="779da-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="779da-261">[Para configurar][availability], clique em Testes na Web.</span><span class="sxs-lookup"><span data-stu-id="779da-261">[To set up][availability], click Web tests.</span></span>

![Clique em Testes na Web e em Adicionar Teste na Web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="779da-263">Se seu site ficar inativo, você obterá gráficos de tempos de resposta e também notificações por email.</span><span class="sxs-lookup"><span data-stu-id="779da-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemplo de teste da Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="779da-265">[Saiba mais sobre testes de disponibilidade via web.][availability]</span><span class="sxs-lookup"><span data-stu-id="779da-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="779da-266">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="779da-266">Questions?</span></span> <span data-ttu-id="779da-267">Problemas?</span><span class="sxs-lookup"><span data-stu-id="779da-267">Problems?</span></span>
[<span data-ttu-id="779da-268">Solucionar problemas de Java</span><span class="sxs-lookup"><span data-stu-id="779da-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="779da-269">Vídeo</span><span class="sxs-lookup"><span data-stu-id="779da-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="779da-270">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="779da-270">Next steps</span></span>
* [<span data-ttu-id="779da-271">Monitorar chamadas de dependência</span><span class="sxs-lookup"><span data-stu-id="779da-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="779da-272">Monitorar os contadores de desempenho do Unix</span><span class="sxs-lookup"><span data-stu-id="779da-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="779da-273">Adicionar [monitoramento a suas páginas da Web](app-insights-javascript.md) para monitorar tempos de carregamento de página, chamadas AJAX e exceções do navegador.</span><span class="sxs-lookup"><span data-stu-id="779da-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="779da-274">Gravar [telemetria personalizada](app-insights-api-custom-events-metrics.md) para controlar o uso no navegador ou no servidor.</span><span class="sxs-lookup"><span data-stu-id="779da-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="779da-275">Criar [painéis](app-insights-dashboards.md) para reunir os gráficos de chave para seu sistema de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="779da-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="779da-276">Usar [Análise](app-insights-analytics.md) para consultas avançadas por telemetria a o aplicativo</span><span class="sxs-lookup"><span data-stu-id="779da-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="779da-277">Para saber mais, visite [Azure para desenvolvedores Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="779da-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
