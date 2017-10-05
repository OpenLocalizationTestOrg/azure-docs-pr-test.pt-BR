---
title: "Separar a telemetria do desenvolvimento, teste e lançamento no Azure Application Insights | Microsoft Docs"
description: "Direcione a telemetria para diferentes recursos para stamps de desenvolvimento, teste e produção."
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
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="47366-103">Separação da telemetria de desenvolvimento, teste e produção</span><span class="sxs-lookup"><span data-stu-id="47366-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="47366-104">Ao desenvolver a próxima versão de um aplicativo Web, não é bom misturar as telemetrias do da nova versão e da versão já lançada do [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47366-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="47366-105">Para evitar confusão, envie a telemetria de diferentes estágios de desenvolvimento a fim de separar os recursos do Application Insights, com chaves de instrumentação separadas (ikeys).</span><span class="sxs-lookup"><span data-stu-id="47366-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="47366-106">Para facilitar a alteração da chave de instrumentação, quando uma versão muda de um estágio para outro, pode ser útil definir a ikey no código em vez de no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="47366-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="47366-107">(Se o sistema for um Serviço de Nuvem do Azure, haverá [outro método de configuração de ikeys separados](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="47366-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="47366-108">Sobre recursos e chaves de instrumentação</span><span class="sxs-lookup"><span data-stu-id="47366-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="47366-109">Ao configurar o monitoramento do Application Insights para seu aplicativo Web, você cria um *recurso* do Application Insights no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47366-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="47366-110">Abra esse recurso no portal do Azure para ver e analisar a telemetria coletada de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47366-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="47366-111">O recurso é identificado por uma *chave de instrumentação* (ikey).</span><span class="sxs-lookup"><span data-stu-id="47366-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="47366-112">Ao instalar o pacote do Application Insights para monitorar seu aplicativo, você o configura com a chave de instrumentação, assim ele sabe para onde enviar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="47366-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="47366-113">Normalmente, você escolhe usar recursos separados ou um único recurso compartilhado em diversos cenários:</span><span class="sxs-lookup"><span data-stu-id="47366-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="47366-114">Aplicativos independentes e diferentes – use um recurso separado e a ikey para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47366-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="47366-115">Vários componentes ou funções de um aplicativo de negócios – use um [único recurso compartilhado](app-insights-monitor-multi-role-apps.md) para todos os aplicativos componentes.</span><span class="sxs-lookup"><span data-stu-id="47366-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="47366-116">A telemetria pode ser filtrada ou segmentada pela propriedade cloud_RoleName.</span><span class="sxs-lookup"><span data-stu-id="47366-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="47366-117">Desenvolvimento, Teste e Lançamento – usam um recurso e ikey separados para versões do sistema em 'stamp' ou estágio de produção.</span><span class="sxs-lookup"><span data-stu-id="47366-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="47366-118">Teste A | B – use um único recurso.</span><span class="sxs-lookup"><span data-stu-id="47366-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="47366-119">Crie um Inicializador de Telemetria para adicionar uma propriedade à telemetria que identifica as variantes.</span><span class="sxs-lookup"><span data-stu-id="47366-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="47366-120"><a name="dynamic-ikey"></a> Chave de instrumentação dinâmica</span><span class="sxs-lookup"><span data-stu-id="47366-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="47366-121">Para facilitar a alteração da ikey à medida que o código percorre os estágios de produção, a defina no código em vez de no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="47366-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="47366-122">Defina a chave em um método de inicialização como global.aspx.cs em um serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="47366-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="47366-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="47366-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="47366-124">Nesse exemplo, as ikeys para os diferentes recursos são colocadas em diferentes versões do arquivo de configuração da Web.</span><span class="sxs-lookup"><span data-stu-id="47366-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="47366-125">Trocar o arquivo de configuração da Web, que pode ser realizado como parte do script versão, alternará o recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="47366-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="47366-126">Páginas da Web</span><span class="sxs-lookup"><span data-stu-id="47366-126">Web pages</span></span>
<span data-ttu-id="47366-127">A iKey também é usada nas páginas da Web do aplicativo, no [script que você obteve da folha de início rápido](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="47366-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="47366-128">Em vez de codificá-la literalmente no script, gere-a a partir do estado do servidor.</span><span class="sxs-lookup"><span data-stu-id="47366-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="47366-129">Por exemplo, em um aplicativo ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="47366-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="47366-130">*JavaScript no Razor*</span><span class="sxs-lookup"><span data-stu-id="47366-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="47366-131">Criar recursos adicionais do Application Insights</span><span class="sxs-lookup"><span data-stu-id="47366-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="47366-132">Para separar a telemetria de diferentes componentes do aplicativo ou de diferentes stamps (desenvolvimento/teste/produção) do mesmo componente, será necessário criar um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="47366-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="47366-133">No [portal.azure.com](https://portal.azure.com), adicione um recurso do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="47366-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Clique em Novo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="47366-135">**tipo de aplicativo** afeta o que você vê na folha de visão geral e as propriedades disponíveis no [explorador de métricas](app-insights-metrics-explorer.md)do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47366-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="47366-136">Se você não vir o tipo de aplicativo, escolha um dos tipos da Web para páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="47366-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="47366-137">**grupo de recursos** é uma conveniência para o gerenciamento de propriedades, como [controle de acesso](app-insights-resources-roles-access-control.md)do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47366-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="47366-138">Você pode usar grupos de recursos separados para desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="47366-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="47366-139">**Assinatura** é a sua conta de pagamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="47366-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="47366-140">**Local** é onde podemos manter seus dados.</span><span class="sxs-lookup"><span data-stu-id="47366-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="47366-141">Atualmente ele não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="47366-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="47366-142">**Adicionar ao painel** coloca um bloco de acesso rápido para o recurso em sua Página Inicial do Azure.</span><span class="sxs-lookup"><span data-stu-id="47366-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="47366-143">A criação do recurso leva alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="47366-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="47366-144">Quando estiver pronto, você verá um alerta.</span><span class="sxs-lookup"><span data-stu-id="47366-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="47366-145">(Você pode escrever um [script do PowerShell](app-insights-powershell-script-create-resource.md) para criar um recurso automaticamente.)</span><span class="sxs-lookup"><span data-stu-id="47366-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="47366-146">Obter a chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="47366-146">Getting the instrumentation key</span></span>
<span data-ttu-id="47366-147">A chave de instrumentação identifica o recurso que você criou.</span><span class="sxs-lookup"><span data-stu-id="47366-147">The instrumentation key identifies the resource that you created.</span></span> 

![Clique em Essentials, clique na Chave de Instrumentação, CTRL+C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="47366-149">Você precisará das chaves de instrumentação de todos os recursos aos quais seu aplicativo enviará dados.</span><span class="sxs-lookup"><span data-stu-id="47366-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="47366-150">Filtrar por número de compilação</span><span class="sxs-lookup"><span data-stu-id="47366-150">Filter on build number</span></span>
<span data-ttu-id="47366-151">Quando publicar uma nova versão do seu aplicativo, você desejará ser capaz de separar a telemetria das compilações diferentes.</span><span class="sxs-lookup"><span data-stu-id="47366-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="47366-152">Você pode definir a propriedade de versão do aplicativo para que possa filtrar resultados da [pesquisa](app-insights-diagnostic-search.md) e do [Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="47366-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtragem em uma propriedade](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="47366-154">Há vários métodos diferentes de definir a propriedade de Versão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47366-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="47366-155">Definir diretamente:</span><span class="sxs-lookup"><span data-stu-id="47366-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="47366-156">Defina a quebra automática de linha em um [inicializador de telemetria](app-insights-api-custom-events-metrics.md#defaults) para garantir que todas as instâncias de TelemetryClient sejam configuradas de forma consistente.</span><span class="sxs-lookup"><span data-stu-id="47366-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="47366-157">[ASP.NET] Definir a versão em `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="47366-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="47366-158">O módulo da Web selecionará a versão do nó BuildLabel.</span><span class="sxs-lookup"><span data-stu-id="47366-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="47366-159">Inclua esse arquivo no seu projeto e não se esqueça de definir a propriedade Copy Always no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="47366-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

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
* <span data-ttu-id="47366-160">[ASP.NET] Gerar automaticamente BuildInfo.config no MSBuild.</span><span class="sxs-lookup"><span data-stu-id="47366-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="47366-161">Para fazer isso, adicione algumas linhas ao seu arquivo `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="47366-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="47366-162">Isso gera um arquivo chamado *nomedoSeuProjeto*.BuildInfo.config. O processo de Publicação renomeia o arquivo como BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="47366-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="47366-163">O rótulo da compilação contém um espaço reservado (AutoGen_...) quando você cria com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47366-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="47366-164">Mas quando compilado com o MSBuild, ele é preenchido com o número de versão correta.</span><span class="sxs-lookup"><span data-stu-id="47366-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="47366-165">Para permitir que o MSBuild gere números de versão, defina a versão como `1.0.*` em AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="47366-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="47366-166">Versão e controle de versão</span><span class="sxs-lookup"><span data-stu-id="47366-166">Version and release tracking</span></span>
<span data-ttu-id="47366-167">Para controlar a versão do aplicativo, certifique-se de `buildinfo.config` é gerado pelo processo de Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="47366-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="47366-168">No arquivo. csproj, adicione:</span><span class="sxs-lookup"><span data-stu-id="47366-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="47366-169">Quando ele tem as informações de compilação, o módulo da web Application Insights adiciona automaticamente **Versão do aplicativo** como uma propriedade para cada item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="47366-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="47366-170">Isso permite que você filtre por versão ao executar [pesquisas de diagnóstico](app-insights-diagnostic-search.md) ou ao [explorar métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="47366-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="47366-171">No entanto, observe que o número de versão de compilação é gerado apenas pelo Microsoft Build Engine, não pela compilação de desenvolvedor no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47366-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="47366-172">Anotações da versão</span><span class="sxs-lookup"><span data-stu-id="47366-172">Release annotations</span></span>
<span data-ttu-id="47366-173">Se usar o Visual Studio Team Services, você poderá [obter um marcador de anotação](app-insights-annotations.md) adicionado a seus gráficos sempre que lançar uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="47366-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="47366-174">A imagem a seguir mostra como esse marcador é exibido.</span><span class="sxs-lookup"><span data-stu-id="47366-174">The following image shows how this marker appears.</span></span>

![Captura de tela de anotação de versão de exemplo em um gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="47366-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47366-176">Next steps</span></span>

* [<span data-ttu-id="47366-177">Recursos compartilhados para várias funções</span><span class="sxs-lookup"><span data-stu-id="47366-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="47366-178">Criar um Inicializador de Telemetria para distinguir variantes A | B</span><span class="sxs-lookup"><span data-stu-id="47366-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
