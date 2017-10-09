---
title: "aaaWindows integração do SDK do contrato Phone Silverlight"
description: Como tooIntegrate Azure Mobile Engagement com aplicativos do Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="deeb8-103">Integração do SDK do Windows Phone Silverlight para o Engagement</span><span class="sxs-lookup"><span data-stu-id="deeb8-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="deeb8-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="deeb8-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="deeb8-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="deeb8-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="deeb8-106">iOS</span><span class="sxs-lookup"><span data-stu-id="deeb8-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="deeb8-107">Android</span><span class="sxs-lookup"><span data-stu-id="deeb8-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="deeb8-108">Este procedimento descreve hello mais simples maneira tooactivate do Azure Mobile Engagement análise e monitoramento de funções em seu aplicativo do Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="deeb8-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="deeb8-109">Olá, as etapas a seguir é que suficientes relatório de saudação tooactivate dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals.</span><span class="sxs-lookup"><span data-stu-id="deeb8-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="deeb8-110">Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) abaixo) desde que essas estatísticas são dependentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="deeb8-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="deeb8-111">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="deeb8-111">Supported versions</span></span>
<span data-ttu-id="deeb8-112">Olá Mobile Engagement SDK para Windows Silverlight somente pode ser integrado em aplicativos voltados para:</span><span class="sxs-lookup"><span data-stu-id="deeb8-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="deeb8-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="deeb8-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="deeb8-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="deeb8-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="deeb8-115">Se você tiver como alvo o Windows Phone 8.1 (não Silverlight), consulte toohello [procedimento de integração Universal do Windows](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="deeb8-116">Instalar Olá Silverlight SDK do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="deeb8-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="deeb8-117">Olá Mobile Engagement SDK para Windows Silverlight está disponível como um pacote do Nuget chamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="deeb8-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="deeb8-118">Você pode instalá-lo de saudação Nuget Package Manager do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="deeb8-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="deeb8-119">Adicionar recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="deeb8-119">Add hello capabilities</span></span>
<span data-ttu-id="deeb8-120">Olá contrato SDK precisa de alguns recursos de saudação do Windows Phone Silverlight SDK em ordem toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="deeb8-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="deeb8-121">Abra o `WMAppManifest.xml` de arquivos e certifique-se de que Olá recursos a seguir são declarados no hello `Capabilities` painel:</span><span class="sxs-lookup"><span data-stu-id="deeb8-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="deeb8-122">Inicializar Olá contrato SDK</span><span class="sxs-lookup"><span data-stu-id="deeb8-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="deeb8-123">Configuração do Engagement</span><span class="sxs-lookup"><span data-stu-id="deeb8-123">Engagement configuration</span></span>
<span data-ttu-id="deeb8-124">configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="deeb8-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="deeb8-125">Edite esse arquivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="deeb8-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="deeb8-126">A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="deeb8-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="deeb8-127">Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:</span><span class="sxs-lookup"><span data-stu-id="deeb8-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="deeb8-128">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida em Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="deeb8-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="deeb8-129">Inicialização do Engagement</span><span class="sxs-lookup"><span data-stu-id="deeb8-129">Engagement initialization</span></span>
<span data-ttu-id="deeb8-130">Quando você cria um novo projeto, um arquivo `App.xaml.cs` é gerado.</span><span class="sxs-lookup"><span data-stu-id="deeb8-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="deeb8-131">Essa classe herda de `Application` e contém vários métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="deeb8-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="deeb8-132">Ele também será usado tooinitialize Olá SDK do contrato.</span><span class="sxs-lookup"><span data-stu-id="deeb8-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="deeb8-133">Modificar Olá `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="deeb8-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="deeb8-134">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="deeb8-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="deeb8-135">Inserir `EngagementAgent.Instance.Init` em Olá `Application_Launching` método:</span><span class="sxs-lookup"><span data-stu-id="deeb8-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="deeb8-136">Inserir `EngagementAgent.Instance.OnActivated` em Olá `Application_Activated` método:</span><span class="sxs-lookup"><span data-stu-id="deeb8-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="deeb8-137">Altamente Desencorajamos você tooadd Olá contrato inicialização em outro lugar do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="deeb8-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="deeb8-138">No entanto, lembre-se que Olá `EngagementAgent.Instance.Init` método é executado em um thread dedicado e não Olá thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="deeb8-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="deeb8-139">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="deeb8-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="deeb8-140">Método recomendado: sobrecarregar suas classes `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="deeb8-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="deeb8-141">No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você pode simplesmente fazer todas as suas `PhoneApplicationPage` subclasses herdam Olá `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="deeb8-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="deeb8-142">Aqui está um exemplo de como toodo isso para uma página do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="deeb8-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="deeb8-143">Você pode fazer Olá igual para todas as páginas do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="deeb8-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="deeb8-144">Arquivo de código-fonte C#</span><span class="sxs-lookup"><span data-stu-id="deeb8-144">C# Source file</span></span>
<span data-ttu-id="deeb8-145">Modifique o arquivo `.xaml.cs` de paginação :</span><span class="sxs-lookup"><span data-stu-id="deeb8-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="deeb8-146">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="deeb8-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="deeb8-147">Substituir `PhoneApplicationPage` por `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="deeb8-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="deeb8-148">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="deeb8-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="deeb8-149">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="deeb8-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="deeb8-150">Se sua página herda de saudação `OnNavigatedTo` método, seja cuidadoso toolet Olá `base.OnNavigatedTo(e)` chamar.</span><span class="sxs-lookup"><span data-stu-id="deeb8-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="deeb8-151">Caso contrário, a atividade de saudação não será reportada.</span><span class="sxs-lookup"><span data-stu-id="deeb8-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="deeb8-152">Na verdade, Olá `EngagementPage` está chamando `StartActivity` dentro Olá `OnNavigatedTo` método.</span><span class="sxs-lookup"><span data-stu-id="deeb8-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="deeb8-153">Arquivo XAML</span><span class="sxs-lookup"><span data-stu-id="deeb8-153">XAML file</span></span>
<span data-ttu-id="deeb8-154">Modifique o arquivo `.xaml` de paginação :</span><span class="sxs-lookup"><span data-stu-id="deeb8-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="deeb8-155">Adicione declarações de namespaces tooyour:</span><span class="sxs-lookup"><span data-stu-id="deeb8-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="deeb8-156">Substituir `phone:PhoneApplicationPage` por `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="deeb8-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="deeb8-157">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="deeb8-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="deeb8-158">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="deeb8-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="deeb8-159">Substituir o comportamento padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="deeb8-159">Override hello default behavior</span></span>
<span data-ttu-id="deeb8-160">Por padrão, nome de classe de saudação da página de Olá será relatado como nome da atividade hello, com e sem extras.</span><span class="sxs-lookup"><span data-stu-id="deeb8-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="deeb8-161">Se a classe Olá usa Olá sufixo "Página", o contrato também removê-la.</span><span class="sxs-lookup"><span data-stu-id="deeb8-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="deeb8-162">Se você quiser comportamento do toooverride saudação padrão para nome hello, basta adicione este código tooyour:</span><span class="sxs-lookup"><span data-stu-id="deeb8-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="deeb8-163">Se você quiser tooreport informações extras com sua atividade, você pode adicionar esse código tooyour:</span><span class="sxs-lookup"><span data-stu-id="deeb8-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="deeb8-164">Esses métodos são chamados de dentro de saudação `OnNavigatedTo` método da página.</span><span class="sxs-lookup"><span data-stu-id="deeb8-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="deeb8-165">Método alternativo: chame `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="deeb8-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="deeb8-166">Se você não pode ou não toooverload seu `PhoneApplicationPage` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent` métodos diretamente.</span><span class="sxs-lookup"><span data-stu-id="deeb8-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="deeb8-167">Recomendamos chamar `StartActivity` dentro do método `OnNavigatedTo` da sua PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="deeb8-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="deeb8-168">Certifique-se de encerrar a sua sessão corretamente.</span><span class="sxs-lookup"><span data-stu-id="deeb8-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="deeb8-169">Olá SDK chama automaticamente Olá `EndActivity` método quando o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="deeb8-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="deeb8-170">Portanto, é **altamente** recomendado Olá toocall `StartActivity` sempre que alterar a atividade de saudação do usuário Olá e muito**nunca** chamada hello `EndActivity` método.</span><span class="sxs-lookup"><span data-stu-id="deeb8-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="deeb8-171">Esse método envia um servidor de contrato de toohello mensagens que o usuário atual Olá saiu aplicativo hello e isso afeta todos os logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="deeb8-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="deeb8-172">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="deeb8-172">Advanced reporting</span></span>
<span data-ttu-id="deeb8-173">Opcionalmente, convém tooreport eventos específicos do aplicativo, erros e trabalhos, toodo assim, use Olá outros métodos encontrados no hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="deeb8-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="deeb8-174">Olá contrato de API permite que toouse todos os recursos avançados do contrato.</span><span class="sxs-lookup"><span data-stu-id="deeb8-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="deeb8-175">Para obter mais informações, consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="deeb8-176">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="deeb8-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="deeb8-177">Desabilitar o relatório de falhas automático</span><span class="sxs-lookup"><span data-stu-id="deeb8-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="deeb8-178">Você pode desabilitar o recurso de contrato de relatório de falha automático do hello.</span><span class="sxs-lookup"><span data-stu-id="deeb8-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="deeb8-179">Então, quando uma exceção não tratada ocorrer, o Engagement não fará nada.</span><span class="sxs-lookup"><span data-stu-id="deeb8-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="deeb8-180">Se você planejar toodisable esse recurso, lembre-se de que, quando uma falha sem tratamento ocorrerá em seu aplicativo, contrato não enviará falha Olá **AND** não fechará sessão hello e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="deeb8-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="deeb8-181">Falha automático de toodisable reporting, apenas personalizar a configuração dependendo da maneira Olá você declarado:</span><span class="sxs-lookup"><span data-stu-id="deeb8-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="deeb8-182">No arquivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="deeb8-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="deeb8-183">Definir o relatório de falhas muito`false` entre `<reportCrash>` e `</reportCrash>` marcas.</span><span class="sxs-lookup"><span data-stu-id="deeb8-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="deeb8-184">No objeto `EngagementConfiguration` em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="deeb8-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="deeb8-185">Definir toofalse de falha de relatório usando o objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="deeb8-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="deeb8-186">Modo intermitente</span><span class="sxs-lookup"><span data-stu-id="deeb8-186">Burst mode</span></span>
<span data-ttu-id="deeb8-187">Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="deeb8-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="deeb8-188">Se seu aplicativo relatórios logs com muita frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (Isso é chamado hello "modo de disparo").</span><span class="sxs-lookup"><span data-stu-id="deeb8-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="deeb8-189">toodo assim, chame o método hello:</span><span class="sxs-lookup"><span data-stu-id="deeb8-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="deeb8-190">Olá argumento for um valor em **milissegundos**.</span><span class="sxs-lookup"><span data-stu-id="deeb8-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="deeb8-191">A qualquer momento, se desejar que o log em tempo real do tooreactivate hello, apenas chame método de saudação sem nenhum parâmetro, ou com valor de saudação 0.</span><span class="sxs-lookup"><span data-stu-id="deeb8-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="deeb8-192">Olá modo intermitente ligeiramente aumentar bateria Olá vida mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração será arredondado toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos).</span><span class="sxs-lookup"><span data-stu-id="deeb8-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="deeb8-193">É recomendável toouse um limite de disparo não mais que 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="deeb8-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="deeb8-194">Você tem toobe reconhece que salva os logs são itens too300 limitado.</span><span class="sxs-lookup"><span data-stu-id="deeb8-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="deeb8-195">Se o envio for muito longo, você poderá perder alguns logs.</span><span class="sxs-lookup"><span data-stu-id="deeb8-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="deeb8-196">Olá limite de disparo não pode ser configurado tooa período menor que um segundo.</span><span class="sxs-lookup"><span data-stu-id="deeb8-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="deeb8-197">Se você tentar toodo, portanto, Olá SDK mostrará um rastreamento com o erro hello e será automaticamente redefinir valor padrão de toohello, isto é, zero segundos.</span><span class="sxs-lookup"><span data-stu-id="deeb8-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="deeb8-198">Isso vai disparar Olá SDK tooreport Olá logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="deeb8-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

