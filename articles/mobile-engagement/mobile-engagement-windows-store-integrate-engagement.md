---
title: "aaaWindows integração de SDK do contrato de aplicativos Universal"
description: Como tooIntegrate Azure Mobile Engagement com aplicativos universais do Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="5dd8c-103">Integração do SDK do Engagement do Windows Universal</span><span class="sxs-lookup"><span data-stu-id="5dd8c-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5dd8c-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="5dd8c-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="5dd8c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5dd8c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="5dd8c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="5dd8c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="5dd8c-107">Android</span><span class="sxs-lookup"><span data-stu-id="5dd8c-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="5dd8c-108">Este procedimento descreve hello mais simples maneira tooactivate contrato análise e monitoramento de funções em seu aplicativo Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="5dd8c-109">Olá, as etapas a seguir é que suficientes relatório de saudação tooactivate dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="5dd8c-110">Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado marcação API em seu aplicativo Windows Universal do Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) desde Essas estatísticas são depende do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="5dd8c-111">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="5dd8c-111">Supported versions</span></span>
<span data-ttu-id="5dd8c-112">Olá Mobile Engagement SDK para aplicativos universais do Windows só pode ser integrado em tempo de execução do Windows e o direcionamento de aplicativos de plataforma Universal do Windows:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="5dd8c-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="5dd8c-113">Windows 8</span></span>
* <span data-ttu-id="5dd8c-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="5dd8c-114">Windows 8.1</span></span>
* <span data-ttu-id="5dd8c-115">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="5dd8c-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="5dd8c-116">Windows 10 (famílias para dispositivos móveis e desktop)</span><span class="sxs-lookup"><span data-stu-id="5dd8c-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="5dd8c-117">Se você tiver como alvo o Windows Phone Silverlight, consulte toohello [procedimento de integração do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="5dd8c-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="5dd8c-118">Instalar Olá SDK de aplicativos Universal do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5dd8c-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="5dd8c-119">Todas as plataformas</span><span class="sxs-lookup"><span data-stu-id="5dd8c-119">All platforms</span></span>
<span data-ttu-id="5dd8c-120">Olá contrato SDK para Windows Universal aplicativo móvel está disponível como um pacote do Nuget chamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="5dd8c-121">Você pode instalá-lo de saudação Nuget Package Manager do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="5dd8c-122">Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="5dd8c-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="5dd8c-123">NuGet implanta automaticamente os recursos SDK Olá Olá `Resources` pasta raiz de saudação de seu projeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="5dd8c-124">Aplicativos da Plataforma do Windows Universal do Windows 10</span><span class="sxs-lookup"><span data-stu-id="5dd8c-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="5dd8c-125">O NuGet não implantar automaticamente recursos do SDK Olá em seu aplicativo de UWP ainda.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="5dd8c-126">Você tem toodo-la manualmente até a implantação de recursos é reintroduzido no NuGet:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="5dd8c-127">Abra o Explorador de Arquivos.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="5dd8c-128">Navegue toohello local a seguir (**x.x. x** é a versão de saudação do contrato que você está instalando): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x. x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="5dd8c-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="5dd8c-129">Saudação de arrastar e soltar **recursos** pasta na raiz da toohello explorer Olá arquivos do projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="5dd8c-130">No Visual Studio, selecione seu projeto e ativar Olá **Mostrar todos os arquivos** ícone sobre Olá **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="5dd8c-131">Alguns arquivos não são incluídos no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-131">Some files are not included in hello project.</span></span> <span data-ttu-id="5dd8c-132">tooimport-los de uma vez clique com botão direito em Olá **recursos** pasta, **excluir do projeto** , em seguida, outro direito do mouse em hello **recursos** pasta, **Include no projeto** toore-incluir toda a pasta hello.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="5dd8c-133">Todos os arquivos de saudação **recursos** pasta agora estão incluídas no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="5dd8c-134">Adicionar recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="5dd8c-134">Add hello capabilities</span></span>
<span data-ttu-id="5dd8c-135">Olá contrato SDK precisa de alguns recursos de saudação SDK do Windows em ordem toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="5dd8c-136">Abra sua `Package.appxmanifest` de arquivo e certifique-se de que Olá recursos a seguir são declarados:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="5dd8c-137">Inicializar Olá contrato SDK</span><span class="sxs-lookup"><span data-stu-id="5dd8c-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="5dd8c-138">Configuração do Engagement</span><span class="sxs-lookup"><span data-stu-id="5dd8c-138">Engagement configuration</span></span>
<span data-ttu-id="5dd8c-139">configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="5dd8c-140">Edite esse arquivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="5dd8c-141">A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="5dd8c-142">Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="5dd8c-143">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida em Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="5dd8c-144">Inicialização do Engagement</span><span class="sxs-lookup"><span data-stu-id="5dd8c-144">Engagement initialization</span></span>
<span data-ttu-id="5dd8c-145">Quando você cria um novo projeto, um arquivo `App.xaml.cs` é gerado.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="5dd8c-146">Essa classe herda de `Application` e contém vários métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="5dd8c-147">Ele também será usado tooinitialize Olá SDK do contrato.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="5dd8c-148">Modificar Olá `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="5dd8c-149">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="5dd8c-150">Defina uma inicialização de contrato do método tooshare Olá uma vez para todas as chamadas:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="5dd8c-151">Chamar `InitEngagement` em Olá `OnLaunched` método:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="5dd8c-152">Quando o aplicativo é iniciado usando um esquema personalizado, em seguida, Olá outra linha de comando do aplicativo ou hello `OnActivated` método é chamado.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="5dd8c-153">Você também precisa tooinitiate Olá SDK Engagement quando seu aplicativo é ativado.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="5dd8c-154">Assim, substituir toodo `OnActivated` método:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="5dd8c-155">Altamente Desencorajamos você tooadd Olá contrato inicialização em outro lugar do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="5dd8c-156">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="5dd8c-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="5dd8c-157">Método recomendado: sobrecarregar suas classes `Page`</span><span class="sxs-lookup"><span data-stu-id="5dd8c-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="5dd8c-158">No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você pode simplesmente fazer todas as suas `Page` subclasses herdam Olá `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="5dd8c-159">Aqui está um exemplo de como toodo isso para uma página do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="5dd8c-160">Você pode fazer Olá igual para todas as páginas do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="5dd8c-161">Arquivo de código-fonte C#</span><span class="sxs-lookup"><span data-stu-id="5dd8c-161">C# Source file</span></span>
<span data-ttu-id="5dd8c-162">Modifique o arquivo `.xaml.cs` de paginação:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="5dd8c-163">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="5dd8c-164">Substituir `Page` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="5dd8c-165">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5dd8c-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="5dd8c-166">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5dd8c-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="5dd8c-167">Se sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="5dd8c-168">Caso contrário, a atividade de saudação não será reportada (Olá `EngagementPage` chamadas `StartActivity` dentro de seu `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="5dd8c-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="5dd8c-169">Arquivo XAML</span><span class="sxs-lookup"><span data-stu-id="5dd8c-169">XAML file</span></span>
<span data-ttu-id="5dd8c-170">Modifique o arquivo `.xaml` de paginação:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="5dd8c-171">Adicione declarações de namespaces tooyour:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="5dd8c-172">Substituir `Page` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="5dd8c-173">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5dd8c-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="5dd8c-174">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="5dd8c-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="5dd8c-175">Substituir o comportamento padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="5dd8c-175">Override hello default behaviour</span></span>
<span data-ttu-id="5dd8c-176">Por padrão, nome de classe de saudação da página de Olá será relatado como nome da atividade hello, com e sem extras.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="5dd8c-177">Se a classe Olá usa Olá sufixo "Página", o contrato também removê-la.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="5dd8c-178">Se você quiser um comportamento toooverride saudação padrão para nome hello, basta adicione este código tooyour:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="5dd8c-179">Se você quiser tooreport algumas informações adicionais com a sua atividade, você pode adicionar esse código tooyour:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="5dd8c-180">Esses métodos são chamados de dentro de saudação `OnNavigatedTo` método da página.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="5dd8c-181">Método alternativo: chame `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="5dd8c-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="5dd8c-182">Se você não pode ou não toooverload seu `Page` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent` métodos diretamente.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="5dd8c-183">É recomendável toocall `StartActivity` dentro de sua `OnNavigatedTo` método da página.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="5dd8c-184">Certifique-se de encerrar a sua sessão corretamente.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="5dd8c-185">Olá SDK Universal do Windows chama automaticamente Olá `EndActivity` método quando o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="5dd8c-186">Assim, é **altamente** recomendado Olá toocall `StartActivity` método sempre que alterar a atividade de saudação do usuário Olá e muito**nunca** chamada hello `EndActivity` método, esse método envia tooEngagement servidor que o aplicativo hello de licença do usuário atual tem, esta será afeta todos os logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="5dd8c-187">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="5dd8c-187">Advanced reporting</span></span>
<span data-ttu-id="5dd8c-188">Opcionalmente, convém tooreport eventos específicos do aplicativo, erros e trabalhos, toodo assim, use Olá outros métodos encontrados no hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="5dd8c-189">Olá contrato de API permite que toouse todos os recursos avançados do contrato.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="5dd8c-190">Para obter mais informações, consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Windows Universal](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="5dd8c-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="5dd8c-191">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="5dd8c-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="5dd8c-192">Desabilitar o relatório de falhas automático</span><span class="sxs-lookup"><span data-stu-id="5dd8c-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="5dd8c-193">Você pode desabilitar o recurso de contrato de relatório de falha automático do hello.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="5dd8c-194">Então, quando uma exceção não tratada ocorrer, o Engagement não fará nada.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="5dd8c-195">Se você planejar toodisable esse recurso, lembre-se de que, quando uma falha sem tratamento ocorrerá em seu aplicativo, contrato não enviará falha Olá **AND** não fechará sessão hello e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="5dd8c-196">Falha automático de toodisable reporting, apenas personalizar a configuração dependendo da maneira Olá você declarado:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="5dd8c-197">No arquivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="5dd8c-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="5dd8c-198">Definir o relatório de falhas muito`false` entre `<reportCrash>` e `</reportCrash>` marcas.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="5dd8c-199">No objeto `EngagementConfiguration` em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="5dd8c-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="5dd8c-200">Definir toofalse de falha de relatório usando o objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="5dd8c-201">Modo intermitente</span><span class="sxs-lookup"><span data-stu-id="5dd8c-201">Burst mode</span></span>
<span data-ttu-id="5dd8c-202">Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="5dd8c-203">Se seu aplicativo relatórios logs com muita frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (Isso é chamado hello "modo de disparo").</span><span class="sxs-lookup"><span data-stu-id="5dd8c-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="5dd8c-204">toodo assim, chame o método hello:</span><span class="sxs-lookup"><span data-stu-id="5dd8c-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="5dd8c-205">Olá argumento for um valor em **milissegundos**.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="5dd8c-206">A qualquer momento, se desejar que o log em tempo real do tooreactivate hello, apenas chame método de saudação sem nenhum parâmetro, ou com valor de saudação 0.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="5dd8c-207">Olá modo intermitente ligeiramente aumentar bateria Olá vida mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração será arredondado toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos).</span><span class="sxs-lookup"><span data-stu-id="5dd8c-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="5dd8c-208">É recomendável toouse um limite de disparo não mais que 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="5dd8c-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="5dd8c-209">Você tem toobe reconhece que salva os logs são itens too300 limitado.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="5dd8c-210">Se o envio for muito longo, você poderá perder alguns logs.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="5dd8c-211">limite de intermitência de saudação não pode ser configurado tooa período anterior de 1s.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="5dd8c-212">Se você tentar toodo, portanto, Olá SDK mostrará um rastreamento com o erro hello e será automaticamente redefinir o valor padrão de toohello, ou seja, 0s.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="5dd8c-213">Isso vai disparar Olá SDK tooreport Olá logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5dd8c-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

