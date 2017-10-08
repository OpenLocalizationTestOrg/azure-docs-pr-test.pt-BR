---
title: "Telemetria aaaSeparating de desenvolvimento, teste e de versão no Azure Application Insights | Microsoft Docs"
description: "Telemetria direto toodifferent recursos carimbos de desenvolvimento, teste e produção."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="008a3-103">Separação da telemetria de desenvolvimento, teste e produção</span><span class="sxs-lookup"><span data-stu-id="008a3-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="008a3-104">Quando você estiver desenvolvendo a próxima versão Olá de um aplicativo web, você não deseja toomix backup Olá [Application Insights](app-insights-overview.md) Telemetria da versão nova hello e Olá já foi liberado.</span><span class="sxs-lookup"><span data-stu-id="008a3-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="008a3-105">tooavoid confusão, enviar telemetria de saudação do desenvolvimento diferentes fases tooseparate recursos do Application Insights, com chaves de instrumentação separado (ikeys).</span><span class="sxs-lookup"><span data-stu-id="008a3-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="008a3-106">toomake-lo mais fácil toochange Olá instrumentação chave como uma versão é movida de um estágio tooanother, pode ser útil tooset Olá ikey no código, em vez de no arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="008a3-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="008a3-107">(Se o sistema for um Serviço de Nuvem do Azure, haverá [outro método de configuração de ikeys separados](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="008a3-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="008a3-108">Sobre recursos e chaves de instrumentação</span><span class="sxs-lookup"><span data-stu-id="008a3-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="008a3-109">Ao configurar o monitoramento do Application Insights para seu aplicativo Web, você cria um *recurso* do Application Insights no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="008a3-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="008a3-110">Abrir este recurso no hello portal do Azure em ordem toosee e analisar a telemetria Olá coletada do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="008a3-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="008a3-111">Olá recurso é identificado por um *chave de instrumentação* (ikey).</span><span class="sxs-lookup"><span data-stu-id="008a3-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="008a3-112">Quando você instala o hello Application Insights pacote toomonitor seu aplicativo, você configurá-lo com a chave de instrumentação hello, para que ele saiba onde toosend Olá telemetria.</span><span class="sxs-lookup"><span data-stu-id="008a3-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="008a3-113">Normalmente, você escolher recursos separados toouse ou um único recurso compartilhado em cenários diferentes:</span><span class="sxs-lookup"><span data-stu-id="008a3-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="008a3-114">Aplicativos independentes e diferentes – use um recurso separado e a ikey para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="008a3-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="008a3-115">Vários componentes ou funções de aplicativo de negócios - Use um [único recurso compartilhado](app-insights-monitor-multi-role-apps.md) para todos os aplicativos de componente de hello.</span><span class="sxs-lookup"><span data-stu-id="008a3-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="008a3-116">Telemetria pode ser filtrada ou segmentada por propriedade de cloud_RoleName hello.</span><span class="sxs-lookup"><span data-stu-id="008a3-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="008a3-117">Desenvolvimento, teste e liberação - usam um recurso separado e ikey para versões do sistema de saudação em 'carimbo' ou a fase de produção.</span><span class="sxs-lookup"><span data-stu-id="008a3-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="008a3-118">Teste A | B – use um único recurso.</span><span class="sxs-lookup"><span data-stu-id="008a3-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="008a3-119">Crie um tooadd TelemetryInitializer telemetria de toohello uma propriedade que identifica as variantes de saudação.</span><span class="sxs-lookup"><span data-stu-id="008a3-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="008a3-120"><a name="dynamic-ikey"></a> Chave de instrumentação dinâmica</span><span class="sxs-lookup"><span data-stu-id="008a3-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="008a3-121">toomake mais fácil toochange Olá ikey como código Olá move entre estágios de produção, configurá-lo no código em vez de no arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="008a3-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="008a3-122">Chave de saudação definida em um método de inicialização, como global.aspx.cs em um serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="008a3-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="008a3-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="008a3-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="008a3-124">Neste exemplo, Olá ikeys para recursos diferentes Olá são colocadas em diferentes versões do arquivo de configuração de web hello.</span><span class="sxs-lookup"><span data-stu-id="008a3-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="008a3-125">Trocando arquivo de configuração de web de saudação - que pode ser feito como parte do script de liberação Olá - alternará o recurso de destino hello.</span><span class="sxs-lookup"><span data-stu-id="008a3-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="008a3-126">Páginas da Web</span><span class="sxs-lookup"><span data-stu-id="008a3-126">Web pages</span></span>
<span data-ttu-id="008a3-127">Olá iKey também é usado em páginas da web do seu aplicativo, no hello [script que você obteve na folha de início rápido de saudação](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="008a3-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="008a3-128">Em vez de codificá-lo literalmente em script hello, gerá-lo do estado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="008a3-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="008a3-129">Por exemplo, em um aplicativo ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="008a3-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="008a3-130">*JavaScript no Razor*</span><span class="sxs-lookup"><span data-stu-id="008a3-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="008a3-131">Criar recursos adicionais do Application Insights</span><span class="sxs-lookup"><span data-stu-id="008a3-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="008a3-132">Telemetria tooseparate para componentes de aplicativo diferente ou para carimbos diferentes (desenvolvimento/teste/produção) de saudação mesmo componente, em seguida, você terá toocreate um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="008a3-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="008a3-133">Em Olá [portal.azure.com](https://portal.azure.com), adicionar um recurso do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="008a3-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Clique em Novo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="008a3-135">**Tipo de aplicativo** afeta o que você vê na folha de visão geral de saudação e as propriedades de saudação disponíveis no [explorer métrica](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="008a3-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="008a3-136">Se você não vir o tipo de aplicativo, escolha um dos tipos de web de saudação para páginas da web.</span><span class="sxs-lookup"><span data-stu-id="008a3-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="008a3-137">**grupo de recursos** é uma conveniência para o gerenciamento de propriedades, como [controle de acesso](app-insights-resources-roles-access-control.md)do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="008a3-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="008a3-138">Você pode usar grupos de recursos separados para desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="008a3-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="008a3-139">**Assinatura** é a sua conta de pagamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="008a3-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="008a3-140">**Local** é onde podemos manter seus dados.</span><span class="sxs-lookup"><span data-stu-id="008a3-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="008a3-141">Atualmente ele não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="008a3-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="008a3-142">**Adicionar toodashboard** coloca um bloco de acesso rápido para o recurso em sua Home page do Azure.</span><span class="sxs-lookup"><span data-stu-id="008a3-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="008a3-143">Criando recurso Olá leva alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="008a3-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="008a3-144">Quando estiver pronto, você verá um alerta.</span><span class="sxs-lookup"><span data-stu-id="008a3-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="008a3-145">(Você pode escrever um [script do PowerShell](app-insights-powershell-script-create-resource.md) toocreate um recurso automaticamente.)</span><span class="sxs-lookup"><span data-stu-id="008a3-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="008a3-146">Obtendo chave de instrumentação Olá</span><span class="sxs-lookup"><span data-stu-id="008a3-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="008a3-147">chave de instrumentação Olá identifica o recurso de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="008a3-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Clique em Essentials, Olá chave de instrumentação, CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="008a3-149">É necessário chaves de instrumentação de saudação de todos os toowhich de recursos de saudação seu aplicativo irá enviar dados.</span><span class="sxs-lookup"><span data-stu-id="008a3-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="008a3-150">Filtrar por número de compilação</span><span class="sxs-lookup"><span data-stu-id="008a3-150">Filter on build number</span></span>
<span data-ttu-id="008a3-151">Quando você publica uma nova versão do seu aplicativo, você desejará telemetria de saudação toobe tooseparate capaz de compilações diferentes.</span><span class="sxs-lookup"><span data-stu-id="008a3-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="008a3-152">Você pode definir a propriedade de versão do aplicativo hello para que você pode filtrar [pesquisa](app-insights-diagnostic-search.md) e [explorer métrica](app-insights-metrics-explorer.md) resultados.</span><span class="sxs-lookup"><span data-stu-id="008a3-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtragem em uma propriedade](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="008a3-154">Há vários métodos diferentes de configuração de propriedade de versão do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="008a3-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="008a3-155">Definir diretamente:</span><span class="sxs-lookup"><span data-stu-id="008a3-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="008a3-156">Quebrar a linha em uma [inicializador de telemetria](app-insights-api-custom-events-metrics.md#defaults) tooensure todas as instâncias de TelemetryClient são configuradas de forma consistente.</span><span class="sxs-lookup"><span data-stu-id="008a3-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="008a3-157">[ASP.NET] Versão do conjunto de saudação em `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="008a3-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="008a3-158">módulo de web Hello escolherá versão de saudação do nó de BuildLabel hello.</span><span class="sxs-lookup"><span data-stu-id="008a3-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="008a3-159">Incluir esse arquivo em seu projeto e lembre-se de tooset Olá copiar sempre propriedade no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="008a3-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="008a3-160">[ASP.NET] Gerar automaticamente BuildInfo.config no MSBuild.</span><span class="sxs-lookup"><span data-stu-id="008a3-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="008a3-161">toodo isso, adicione alguns tooyour de linhas `.csproj` arquivo:</span><span class="sxs-lookup"><span data-stu-id="008a3-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="008a3-162">Isso gera um arquivo chamado *yourProjectName*. Olá BuildInfo.config. o processo de publicação renomeia tooBuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="008a3-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="008a3-163">rótulo de compilação Olá contém um espaço reservado (autogen _...) quando compilado com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="008a3-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="008a3-164">Mas quando compilado com o MSBuild, ele será preenchido com o número correto da versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="008a3-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="008a3-165">como o conjunto Olá versão tooallow números de versão do MSBuild toogenerate, `1.0.*` em AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="008a3-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="008a3-166">Versão e controle de versão</span><span class="sxs-lookup"><span data-stu-id="008a3-166">Version and release tracking</span></span>
<span data-ttu-id="008a3-167">versão do aplicativo hello tootrack, certifique-se de `buildinfo.config` é gerado pelo seu processo Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="008a3-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="008a3-168">No arquivo. csproj, adicione:</span><span class="sxs-lookup"><span data-stu-id="008a3-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="008a3-169">Quando ele tem informações de compilação hello, módulo de web do Application Insights Olá adiciona automaticamente **versão do aplicativo** como tooevery uma propriedade de telemetria.</span><span class="sxs-lookup"><span data-stu-id="008a3-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="008a3-170">Que permite que você toofilter versão quando você executar [pesquisas diagnósticas](app-insights-diagnostic-search.md), ou quando você [explorar métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="008a3-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="008a3-171">No entanto, observe que o número de versão de compilação Olá é gerado apenas por Olá Microsoft Build Engine, não pelo desenvolvedor de saudação de compilação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="008a3-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="008a3-172">Anotações da versão</span><span class="sxs-lookup"><span data-stu-id="008a3-172">Release annotations</span></span>
<span data-ttu-id="008a3-173">Se você usar o Visual Studio Team Services, você pode [obter um marcador de anotação](app-insights-annotations.md) adicionado tooyour gráficos sempre que uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="008a3-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="008a3-174">Olá a imagem a seguir mostra como esse marcador é exibido.</span><span class="sxs-lookup"><span data-stu-id="008a3-174">hello following image shows how this marker appears.</span></span>

![Captura de tela de anotação de versão de exemplo em um gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="008a3-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="008a3-176">Next steps</span></span>

* [<span data-ttu-id="008a3-177">Recursos compartilhados para várias funções</span><span class="sxs-lookup"><span data-stu-id="008a3-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="008a3-178">Criar um toodistinguish de inicializador de telemetria A | Variantes de B</span><span class="sxs-lookup"><span data-stu-id="008a3-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
