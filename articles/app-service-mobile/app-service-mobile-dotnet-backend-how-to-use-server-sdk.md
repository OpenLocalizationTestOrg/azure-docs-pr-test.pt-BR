---
title: "toowork aaaHow com o servidor de back-end .NET Olá SDK para aplicativos móveis | Microsoft Docs"
description: "Saiba como toowork com hello o SDK do servidor de back-end do .NET para aplicativos de celular do serviço de aplicativo do Azure."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, aplicativo móvel, serviço móvel, escala, escalonável, implantação de aplicativo, implantação de aplicativo do azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="a0a21-104">Trabalhar com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a21-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="a0a21-105">Este tópico mostra como toouse Olá servidor de back-end .NET SDK no principais cenários de aplicativos de celular do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="a0a21-106">Olá SDK de aplicativos móveis do Azure ajuda você a trabalhar com clientes móveis do seu aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a0a21-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="a0a21-107">Olá [server .NET SDK para aplicativos móveis do Azure] [ 2] é o código-fonte aberto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0a21-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="a0a21-108">repositório de saudação contém todo o código fonte incluindo o conjunto de testes de unidade do hello todo servidor SDK e alguns projetos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a0a21-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="a0a21-109">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="a0a21-109">Reference documentation</span></span>
<span data-ttu-id="a0a21-110">documentação de referência Olá para o servidor de saudação SDK está localizada aqui: [referência do .NET de aplicativos do Azure Mobile][1].</span><span class="sxs-lookup"><span data-stu-id="a0a21-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="a0a21-111"><a name="create-app"></a>Como criar um back-end do aplicativo móvel do .NET</span><span class="sxs-lookup"><span data-stu-id="a0a21-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="a0a21-112">Se você estiver iniciando um novo projeto, você pode criar um aplicativo de serviço de aplicativo usando o hello [portal do Azure] ou o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0a21-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="a0a21-113">Você pode executar Olá aplicativo de serviço de aplicativo localmente ou publicar Olá projeto tooyour baseado em nuvem do serviço de aplicativo aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="a0a21-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="a0a21-114">Se você estiver adicionando um projeto existente do tooan recursos móveis, consulte Olá [baixar e inicializar Olá SDK](#install-sdk) seção.</span><span class="sxs-lookup"><span data-stu-id="a0a21-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="a0a21-115">Criar um back-end .NET usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a21-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="a0a21-116">toocreate um back-end móvel do serviço de aplicativo, o execute Olá [tutorial de início rápido] [ 3] ou siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a0a21-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="a0a21-117">Em Olá *começar* folha, em **criar uma tabela API**, escolha **c#** como seu **idioma de back-end**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="a0a21-118">Clique em **baixar**, extraia o computador local do projeto compactado arquivos tooyour e abra a solução Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0a21-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="a0a21-119">Criar um back-end do .NET usando o Visual Studio 2013 e o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a0a21-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="a0a21-120">Instalar Olá [SDK do Azure para .NET] [ 4] (versão 2.9.0 ou posterior) toocreate um projeto de aplicativos do Azure Mobile no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0a21-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="a0a21-121">Depois de instalar o SDK do hello, crie um aplicativo ASP.NET usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0a21-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="a0a21-122">Olá abrir **novo projeto** caixa de diálogo (de *arquivo* > **novo** > **projeto...** ).</span><span class="sxs-lookup"><span data-stu-id="a0a21-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="a0a21-123">Expanda **Modelos** > **Visual C#** e selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="a0a21-124">Selecione **Aplicativo Web do ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="a0a21-125">Preencha o nome do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-125">Fill in hello project name.</span></span> <span data-ttu-id="a0a21-126">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-126">Then click **OK**.</span></span>
5. <span data-ttu-id="a0a21-127">Em *Modelos do ASP.NET 4.5.2*, selecione **Aplicativo Móvel do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="a0a21-128">Verificar **Host na nuvem Olá** toocreate um back-end móvel em Olá toowhich pode publicar esse projeto em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a0a21-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="a0a21-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-129">Click **OK**.</span></span>

## <span data-ttu-id="a0a21-130"><a name="install-sdk"></a>Como: baixar e inicializar Olá SDK</span><span class="sxs-lookup"><span data-stu-id="a0a21-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="a0a21-131">Olá SDK está disponível em [NuGet.org]. Este pacote inclui Olá funcionalidade básica necessária tooget iniciado usando Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="a0a21-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="a0a21-132">tooinitialize Olá SDK, você precisa tooperform ações Olá **HttpConfiguration** objeto.</span><span class="sxs-lookup"><span data-stu-id="a0a21-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="a0a21-133">Instalar o SDK de saudação</span><span class="sxs-lookup"><span data-stu-id="a0a21-133">Install hello SDK</span></span>
<span data-ttu-id="a0a21-134">Olá tooinstall SDK, com o botão direito no projeto do servidor de saudação no Visual Studio, selecione **gerenciar pacotes NuGet**, pesquise Olá [Microsoft.Azure.Mobile.Server] do pacote e, em seguida, clique em  **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="a0a21-135"><a name="server-project-setup"></a>Inicializar projeto de servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="a0a21-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="a0a21-136">Um projeto do servidor de back-end .NET é inicializado semelhante tooother projetos do ASP.NET, incluindo uma classe de inicialização OWIN.</span><span class="sxs-lookup"><span data-stu-id="a0a21-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="a0a21-137">Certifique-se de que você referenciou pacote do NuGet Olá `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="a0a21-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="a0a21-138">tooadd dessa classe no Visual Studio, clique com botão direito no projeto do servidor e selecione **adicionar** >
**Novo Item**, em seguida, **Web**  >  ** Geral** > **classe de inicialização OWIN**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="a0a21-139">Uma classe é gerada com hello atributos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0a21-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="a0a21-140">Em Olá `Configuration()` método de sua classe de inicialização OWIN, use um **HttpConfiguration** ambiente do objeto tooconfigure Olá os aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="a0a21-141">saudação de exemplo a seguir inicializa o projeto do servidor de saudação não tem recursos adicionados:</span><span class="sxs-lookup"><span data-stu-id="a0a21-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="a0a21-142">tooenable os recursos individuais, você deve chamar os métodos de extensão no hello **MobileAppConfiguration** objeto antes de chamar **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="a0a21-143">Por exemplo, Olá código a seguir adiciona padrão Olá roteia controladores tooall API que têm o atributo Olá `[MobileAppController]` durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="a0a21-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="a0a21-144">início rápido do servidor de saudação do hello chamadas portais do Azure **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="a0a21-145">Este toohello equivalente após a instalação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="a0a21-146">métodos de extensão Olá usados são:</span><span class="sxs-lookup"><span data-stu-id="a0a21-146">hello extension methods used are:</span></span>

* <span data-ttu-id="a0a21-147">`AddMobileAppHomeController()`fornece a home page do saudação padrão os aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="a0a21-148">`MapApiControllers()`fornece recursos personalizados de API para controladores WebAPI decorados com hello `[MobileAppController]` atributo.</span><span class="sxs-lookup"><span data-stu-id="a0a21-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="a0a21-149">`AddTables()`Fornece um mapeamento de saudação `/tables` controladores tootable pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="a0a21-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="a0a21-150">`AddTablesWithEntityFramework()`é uma abreviada para Olá mapeamento `/tables` controladoras baseadas em pontos de extremidade usando o Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="a0a21-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="a0a21-151">`AddPushNotifications()` fornece um método simples de registro de dispositivos para Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="a0a21-152">`MapLegacyCrossDomainController()` fornece os cabeçalhos de CORS padrão para o desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="a0a21-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="a0a21-153">Extensões SDK</span><span class="sxs-lookup"><span data-stu-id="a0a21-153">SDK extensions</span></span>
<span data-ttu-id="a0a21-154">Olá pacotes do NuGet com base em extensão a seguir fornece vários recursos móveis que podem ser usados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a0a21-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="a0a21-155">Habilitar extensões durante a inicialização usando Olá **MobileAppConfiguration** objeto.</span><span class="sxs-lookup"><span data-stu-id="a0a21-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="a0a21-156">[Microsoft.Azure.Mobile.Server.Quickstart] suporta Olá configuração básica de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="a0a21-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="a0a21-157">Configuração toohello adicionado por chamada hello **UseDefaultConfiguration** método de extensão durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="a0a21-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="a0a21-158">Essa extensão inclui as seguintes extensões: Notificações, Autenticação, Entidade, Tabelas, pacotes Crossdomain e Home.</span><span class="sxs-lookup"><span data-stu-id="a0a21-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="a0a21-159">Este pacote é usado pelo Olá Quickstart de aplicativos móveis disponíveis no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="a0a21-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa o padrão de saudação *este aplicativo móvel estiver em execução página* para a raiz do site hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="a0a21-161">Adicionar configuração toohello chamando o **AddMobileAppHomeController** método de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="a0a21-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) inclui classes para trabalhar com dados e define o pipeline de dados hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="a0a21-163">Adicionar configuração toohello Olá chamada **AddTables** método de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="a0a21-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permite que os dados de tooaccess saudação do Entity Framework no hello banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="a0a21-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="a0a21-165">Adicionar configuração toohello Olá chamada **AddTablesWithEntityFramework** método de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="a0a21-166">[Microsoft.Azure.Mobile.Server.Authentication] habilita a autenticação e conjuntos de backup Olá OWIN middleware usado toovalidate tokens.</span><span class="sxs-lookup"><span data-stu-id="a0a21-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="a0a21-167">Adicionar configuração toohello Olá chamada **AddAppServiceAuthentication** e **IAppBuilder**. **UseAppServiceAuthentication** métodos de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="a0a21-168">[Microsoft.Azure.Mobile.Server.Notifications] permite as notificações por push e define um ponto de extremidade de registro push.</span><span class="sxs-lookup"><span data-stu-id="a0a21-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="a0a21-169">Adicionar configuração toohello Olá chamada **AddPushNotifications** método de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="a0a21-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) cria um controlador que serve dados toolegacy navegadores da web do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="a0a21-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="a0a21-171">Adicionar configuração toohello chamando o **MapLegacyCrossDomainController** método de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="a0a21-172">[Microsoft.Azure.Mobile.Server.Login] fornece um método de AppServiceLoginHandler.CreateToken() hello, que é um método estático usado nos cenários de autenticação personalizada.</span><span class="sxs-lookup"><span data-stu-id="a0a21-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="a0a21-173"><a name="publish-server-project"></a>Como: publicar projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="a0a21-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="a0a21-174">Esta seção mostra como toopublish seu back-end .NET de projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0a21-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="a0a21-175">Você também pode implantar seu projeto de back-end usando Git ou qualquer um dos Olá outros métodos abordados Olá [documentação de implantação do serviço de aplicativo do Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a0a21-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="a0a21-176">No Visual Studio, reconstrua pacotes do NuGet Olá projeto toorestore.</span><span class="sxs-lookup"><span data-stu-id="a0a21-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="a0a21-177">No Gerenciador de soluções, projetos de saudação com o botão direito, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="a0a21-178">Olá primeira vez que você publicar, você precisa toodefine um perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="a0a21-179">Quando já tiver um perfil definido, selecione-o e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="a0a21-180">Se for solicitado tooselect um destino de publicação, clique em **serviço de aplicativo do Microsoft Azure** > **próximo**, e (se necessário) entrar com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="a0a21-181">O Visual Studio baixa e armazena suas configurações de publicação com segurança diretamente do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="a0a21-182">Escolha sua **Assinatura**, selecione o **Tipo de Recurso** em **Exibição**, expanda **Aplicativo Móvel**, clique no back-end do Aplicativo Móvel e então clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="a0a21-183">Verifique se Olá publicar informações de perfil e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="a0a21-184">Quando o back-end do aplicativo móvel for publicado com êxito, você verá uma página de aterrissagem indicando êxito.</span><span class="sxs-lookup"><span data-stu-id="a0a21-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="a0a21-185"><a name="define-table-controller"></a> Como definir um controlador de tabela</span><span class="sxs-lookup"><span data-stu-id="a0a21-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="a0a21-186">Defina um controlador de tabela tooexpose os clientes toomobile da tabela de SQL.</span><span class="sxs-lookup"><span data-stu-id="a0a21-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="a0a21-187">A configuração de um Controlador de Tabela exige três etapas:</span><span class="sxs-lookup"><span data-stu-id="a0a21-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="a0a21-188">Criar uma classe DTO (Objeto de Transferência de Dados).</span><span class="sxs-lookup"><span data-stu-id="a0a21-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="a0a21-189">Configure uma referência de tabela no hello classe DbContext Mobile.</span><span class="sxs-lookup"><span data-stu-id="a0a21-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="a0a21-190">Criar um controlador de tabela.</span><span class="sxs-lookup"><span data-stu-id="a0a21-190">Create a table controller.</span></span>

<span data-ttu-id="a0a21-191">Um DTO (objeto de transferência de dados) é um objeto C# simples que herda de `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="a0a21-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="a0a21-192">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a0a21-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="a0a21-193">Olá DTO é a tabela de saudação de toodefine usado no banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="a0a21-194">Olá toocreate entrada do banco de dados, adicione um `DbSet<>` propriedade à saudação DbContext que você está usando.</span><span class="sxs-lookup"><span data-stu-id="a0a21-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="a0a21-195">No modelo de projeto saudação padrão para aplicativos móveis do Azure, hello DbContext é chamado `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="a0a21-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="a0a21-196">Se você tiver Olá instalado SDK do Azure, agora você pode criar um controlador de tabela do modelo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a0a21-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="a0a21-197">Com o botão direito na pasta de controladores hello e selecione **adicionar** > **controlador...** .</span><span class="sxs-lookup"><span data-stu-id="a0a21-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="a0a21-198">Selecione Olá **controlador de tabela em aplicativos do Azure Mobile** opção e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="a0a21-199">Em Olá **Adicionar controlador** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="a0a21-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="a0a21-200">Em Olá **classe modelo** lista suspensa, selecione o novo DTO.</span><span class="sxs-lookup"><span data-stu-id="a0a21-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="a0a21-201">Em Olá **DbContext** suspenso, a classe do hello selecione DbContext de serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="a0a21-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="a0a21-202">nome do controlador Olá é criado para você.</span><span class="sxs-lookup"><span data-stu-id="a0a21-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="a0a21-203">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-203">Click **Add**.</span></span>

<span data-ttu-id="a0a21-204">projeto do servidor de saudação quickstart contém um exemplo de um simples **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="a0a21-205"><a name="adjust-pagesize"></a>Como: ajustar o tamanho de paginação da tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="a0a21-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="a0a21-206">Por padrão, os Aplicativos Móveis do Azure retornam 50 registros por solicitação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="a0a21-207">Paginação garante que o cliente Olá não obstruir o servidor de saudação nem de thread da interface do usuário por muito tempo, garantindo uma boa experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="a0a21-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="a0a21-208">tamanho de paginação da tabela toochange hello, do lado do servidor de saudação do aumento "consulta o tamanho permitido" e hello cliente página tamanho saudação do lado do servidor "tamanho de consulta permitido" é ajustado usando Olá `EnableQuery` atributo:</span><span class="sxs-lookup"><span data-stu-id="a0a21-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="a0a21-209">Certifique-se de saudação PageSize é hello mesmo ou maior que tamanho Olá solicitado pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="a0a21-210">Consulte a documentação de como de cliente específico de toohello para obter detalhes sobre como alterar o tamanho de página do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="a0a21-211">Como definir um controlador da API personalizada</span><span class="sxs-lookup"><span data-stu-id="a0a21-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="a0a21-212">controlador de API personalizada Olá fornece hello mais básico funcionalidade tooyour aplicativo móvel backend ao expor um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="a0a21-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="a0a21-213">Você pode registrar um controlador de API específicas para dispositivos móveis usando o atributo Olá [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="a0a21-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="a0a21-214">Olá `MobileAppController` atributo registra rota hello, configura o serializador JSON de aplicativos móveis hello e ativa a [verificação de versão de cliente](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a0a21-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="a0a21-215">No Visual Studio, pasta de controladores de saudação com o botão direito, em seguida, clique em **adicionar** > **controlador**, selecione **Web API 2 controlador&mdash;vazio** e Clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="a0a21-216">Forneça um **Nome do controlador**, como `CustomController`, e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="a0a21-217">No novo arquivo de classe de controlador hello, adicione o seguinte de saudação usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="a0a21-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="a0a21-218">Aplicar Olá **[MobileAppController]** definição de classe do controlador toohello API, como no exemplo a seguir de saudação do atributo:</span><span class="sxs-lookup"><span data-stu-id="a0a21-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="a0a21-219">No arquivo de App_Start/Startup.MobileApp.cs, adicione uma chamada toohello **MapApiControllers** método de extensão, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="a0a21-220">Você também pode usar o hello `UseDefaultConfiguration()` método de extensão, em vez de `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="a0a21-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="a0a21-221">Qualquer controlador que não tenha o **MobileAppControllerAttribute** aplicado ainda poderá ser acessado pelos clientes, mas não será consumido corretamente por clientes que usem qualquer SDK do cliente do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="a0a21-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="a0a21-222">Como trabalhar com autenticação</span><span class="sxs-lookup"><span data-stu-id="a0a21-222">How to: Work with authentication</span></span>
<span data-ttu-id="a0a21-223">Aplicativos móveis do Azure usa a autenticação do serviço de aplicativo / autorização toosecure seu móvel back-end.</span><span class="sxs-lookup"><span data-stu-id="a0a21-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="a0a21-224">Esta seção mostra como Olá tooperform tarefas relacionadas à autenticação no seu projeto do servidor de back-end .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0a21-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="a0a21-225">Como: adicionar um projeto do servidor de autenticação tooa</span><span class="sxs-lookup"><span data-stu-id="a0a21-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="a0a21-226">Como usar a autenticação personalizada para o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="a0a21-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="a0a21-227">Como recuperar informações do usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="a0a21-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="a0a21-228">Como restringir o acesso a dados para usuários autorizados</span><span class="sxs-lookup"><span data-stu-id="a0a21-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="a0a21-229"><a name="add-auth"></a>Como: adicionar um projeto do servidor de autenticação tooa</span><span class="sxs-lookup"><span data-stu-id="a0a21-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="a0a21-230">Você pode adicionar o projeto do servidor de autenticação tooyour estendendo Olá **MobileAppConfiguration** objeto e configurar o middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="a0a21-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="a0a21-231">Quando você instala o hello [Microsoft.Azure.Mobile.Server.Quickstart] Olá de pacote e chame **UseDefaultConfiguration** método de extensão, você pode ignorar toostep 3.</span><span class="sxs-lookup"><span data-stu-id="a0a21-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="a0a21-232">No Visual Studio, instalar Olá [Microsoft.Azure.Mobile.Server.Authentication] pacote.</span><span class="sxs-lookup"><span data-stu-id="a0a21-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="a0a21-233">No arquivo de projeto Startup.cs hello, adicionar Olá a seguinte linha de código no início de saudação do hello **configuração** método:</span><span class="sxs-lookup"><span data-stu-id="a0a21-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="a0a21-234">Este componente de middleware OWIN valida os tokens emitidos pelo gateway do serviço de aplicativo hello associado.</span><span class="sxs-lookup"><span data-stu-id="a0a21-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="a0a21-235">Adicionar Olá `[Authorize]` controlador do atributo tooany ou método que requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="a0a21-236">toolearn sobre como tooauthenticate clientes tooyour back-end de aplicativos móveis, consulte [adicionar autenticação tooyour aplicativo](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="a0a21-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="a0a21-237"><a name="custom-auth"></a>Como usar a autenticação personalizada para o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="a0a21-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="a0a21-238">Se você não desejar toouse um dos provedores de autenticação/autorização do serviço de aplicativo hello, você pode implementar seu próprio sistema de logon.</span><span class="sxs-lookup"><span data-stu-id="a0a21-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="a0a21-239">Instalar Olá [Microsoft.Azure.Mobile.Server.Login] tooassist com geração de token de autenticação do pacote.</span><span class="sxs-lookup"><span data-stu-id="a0a21-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="a0a21-240">Forneça seu próprio código para validar as credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="a0a21-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="a0a21-241">Por exemplo, você pode comparar com senhas com sal e hash aplicados em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0a21-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="a0a21-242">O exemplo hello abaixo, Olá `isValidAssertion()` método (definido em outro lugar) é responsável por essas verificações.</span><span class="sxs-lookup"><span data-stu-id="a0a21-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="a0a21-243">autenticação personalizada Olá é exposta pelo criando um ApiController e expondo `register` e `login` ações.</span><span class="sxs-lookup"><span data-stu-id="a0a21-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="a0a21-244">cliente de saudação deve usar uma personalizado da interface do usuário toocollect Olá informações Olá usuário.</span><span class="sxs-lookup"><span data-stu-id="a0a21-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="a0a21-245">informações de saudação são chamada de API de toohello enviado com um padrão HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a0a21-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="a0a21-246">Depois que o servidor de saudação valida asserção Olá, é emitido um token usando Olá `AppServiceLoginHandler.CreateToken()` método.</span><span class="sxs-lookup"><span data-stu-id="a0a21-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="a0a21-247">Olá ApiController **não** usar Olá `[MobileAppController]` atributo.</span><span class="sxs-lookup"><span data-stu-id="a0a21-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="a0a21-248">Uma ação `login` de exemplo:</span><span class="sxs-lookup"><span data-stu-id="a0a21-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="a0a21-249">No hello anterior de exemplo, LoginResult e LoginResultUser são serializáveis objetos que expõem propriedades necessárias.</span><span class="sxs-lookup"><span data-stu-id="a0a21-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="a0a21-250">cliente Olá espera toobe de respostas de logon retornado como objetos JSON do formulário de saudação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="a0a21-251">Olá `AppServiceLoginHandler.CreateToken()` método inclui um *público* e um *emissor* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a0a21-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="a0a21-252">Ambos os parâmetros são definidos toohello URL da raiz do aplicativo, usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a0a21-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="a0a21-253">Da mesma forma, você deve definir *secretKey* toobe valor de saudação do seu aplicativo de autenticação de chave.</span><span class="sxs-lookup"><span data-stu-id="a0a21-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="a0a21-254">Não distribua Olá chave em um cliente de assinatura, que pode ser usado toomint chaves e representar usuários.</span><span class="sxs-lookup"><span data-stu-id="a0a21-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="a0a21-255">Você pode obter Olá assinatura de chave enquanto hospedado no serviço de aplicativo referenciando Olá *site\_AUTH\_assinatura\_chave* variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="a0a21-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="a0a21-256">Se for necessário em um contexto de depuração local, siga as instruções de Olá Olá [depuração Local com a autenticação](#local-debug) seção chave de saudação tooretrieve e armazená-lo como uma configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a0a21-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="a0a21-257">token de saudação emitida também pode incluir outras declarações e uma data de expiração.</span><span class="sxs-lookup"><span data-stu-id="a0a21-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="a0a21-258">No mínimo, o token emitida de saudação deve incluir um assunto (**sub**) de declaração.</span><span class="sxs-lookup"><span data-stu-id="a0a21-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="a0a21-259">Você pode dar suporte a cliente padrão Olá `loginAsync()` método sobrecarregando rota de autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="a0a21-260">Se o cliente Olá chama `client.loginAsync('custom');` toolog no, a rota deve ser `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="a0a21-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="a0a21-261">Você pode definir a rota Olá para Olá autenticação personalizada controlador usando `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="a0a21-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="a0a21-262">Usando Olá `loginAsync()` abordagem garante que está anexado a esse token de autenticação Olá tooevery chamada subsequente toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="a0a21-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="a0a21-263"><a name="user-info"></a>Como recuperar informações do usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="a0a21-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="a0a21-264">Quando um usuário é autenticado pelo serviço de aplicativo, você pode acessar Olá atribuída a ID de usuário e outras informações no seu código de back-end do .NET.</span><span class="sxs-lookup"><span data-stu-id="a0a21-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="a0a21-265">informações de usuário de saudação podem ser usadas para tomar decisões de autorização na Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="a0a21-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="a0a21-266">Olá código a seguir obtém Olá ID de usuário associado a uma solicitação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="a0a21-267">Olá SID é derivado de ID de usuário específica do provedor hello e é estático para um determinado usuário e o provedor de logon.</span><span class="sxs-lookup"><span data-stu-id="a0a21-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="a0a21-268">Olá SID é nula para tokens de autenticação inválido.</span><span class="sxs-lookup"><span data-stu-id="a0a21-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="a0a21-269">O Serviço de Aplicativo também permite solicitar declarações específicas do provedor de logon.</span><span class="sxs-lookup"><span data-stu-id="a0a21-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="a0a21-270">Cada provedor de identidade pode fornecer mais informações usando o SDK do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="a0a21-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="a0a21-271">Por exemplo, você pode usar o hello Facebook Graph API para obter informações de amigos.</span><span class="sxs-lookup"><span data-stu-id="a0a21-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="a0a21-272">Você pode especificar as declarações que são solicitadas na folha de provedor de saudação em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a21-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="a0a21-273">Algumas declarações exigem configuração adicional com o provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="a0a21-274">saudação de chamadas de código a seguir Olá **GetAppServiceIdentityAsync** extensão método tooget Olá credenciais de logon, que incluem solicitações de token toomake necessário acesso Olá contra Olá Graph API do Facebook:</span><span class="sxs-lookup"><span data-stu-id="a0a21-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="a0a21-275">Adicione um usando a instrução para `System.Security.Principal` tooprovide Olá **GetAppServiceIdentityAsync** método de extensão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="a0a21-276"><a name="authorize"></a>Como restringir o acesso a dados para usuários autorizados</span><span class="sxs-lookup"><span data-stu-id="a0a21-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="a0a21-277">Na seção anterior do hello, mostramos como tooretrieve Olá ID de usuário de um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="a0a21-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="a0a21-278">Você pode restringir o acesso toodata e outros recursos com base nesse valor.</span><span class="sxs-lookup"><span data-stu-id="a0a21-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="a0a21-279">Por exemplo, adicionando um tootables de coluna de ID de usuário e filtrando resultados de consulta Olá por ID de usuário de saudação são um toolimit de maneira simples retornada dados somente tooauthorized os usuários.</span><span class="sxs-lookup"><span data-stu-id="a0a21-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="a0a21-280">Olá código a seguir retorna linhas de dados somente quando Olá SID corresponde ao valor da coluna de ID de usuário Olá na tabela TodoItem de saudação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="a0a21-281">Olá `Query()` método retorna um `IQueryable` que podem ser manipulados por filtragem de toohandle LINQ.</span><span class="sxs-lookup"><span data-stu-id="a0a21-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="a0a21-282">Como: adicionar um projeto do servidor de tooa de notificações de push</span><span class="sxs-lookup"><span data-stu-id="a0a21-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="a0a21-283">Adicionar projeto do servidor de tooyour de notificações de push estendendo Olá **MobileAppConfiguration** objeto e a criação de um cliente de Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="a0a21-284">No Visual Studio, clique com botão direito Olá servidor e clique em **gerenciar pacotes NuGet**, procure `Microsoft.Azure.Mobile.Server.Notifications`, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="a0a21-285">Repita essa saudação de tooinstall etapa `Microsoft.Azure.NotificationHubs` pacote, que inclui a biblioteca de cliente Olá Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="a0a21-286">Em App_Start/Startup.MobileApp.cs e adicione uma chamada toohello **AddPushNotifications()** método de extensão durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="a0a21-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="a0a21-287">Adicione Olá código que cria um cliente de Hubs de notificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0a21-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="a0a21-288">Agora você pode usar o hello Hubs de notificação toosend push notificações tooregistered os dispositivos cliente.</span><span class="sxs-lookup"><span data-stu-id="a0a21-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="a0a21-289">Para obter mais informações, consulte [adicionar push notificações tooyour aplicativo](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="a0a21-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="a0a21-290">toolearn mais sobre Hubs de notificação, consulte [visão geral de Hubs de notificação](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0a21-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="a0a21-291"><a name="tags"></a>Como habilitar envios direcionados por push usando marcações</span><span class="sxs-lookup"><span data-stu-id="a0a21-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="a0a21-292">Hubs de notificação permite enviar notificações destino toospecific registros usando marcas.</span><span class="sxs-lookup"><span data-stu-id="a0a21-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="a0a21-293">Várias marcações são criadas automaticamente:</span><span class="sxs-lookup"><span data-stu-id="a0a21-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="a0a21-294">Olá ID de instalação identifica um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="a0a21-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="a0a21-295">Olá Id de usuário com base em Olá autenticado SID identifica um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="a0a21-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="a0a21-296">Olá instalação ID pode ser acessado de saudação **installationId** propriedade Olá **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="a0a21-297">Olá exemplo a seguir mostra como usar um tooadd de ID de instalação uma marca tooa específicas de instalação em Hubs de notificação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="a0a21-298">Marcas fornecidas pelo cliente Olá durante o registro de notificação por push são ignoradas pelo back-end de saudação durante a criação de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="a0a21-299">tooenable tooadd um cliente marcas toohello instalação, você deve criar uma API personalizada que adiciona marcas usando Olá anterior padrão.</span><span class="sxs-lookup"><span data-stu-id="a0a21-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="a0a21-300">Consulte [marcas de notificação por push de cliente adicionado] [ 5] no exemplo de início rápido concluído Olá serviço de aplicativo móvel de aplicativos para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="a0a21-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="a0a21-301"><a name="push-user"></a>Como: enviar por push notificações tooan autenticou o usuário</span><span class="sxs-lookup"><span data-stu-id="a0a21-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="a0a21-302">Quando um usuário autenticado se registra para notificações de push, uma marca de identificação do usuário é adicionada automaticamente toohello registro.</span><span class="sxs-lookup"><span data-stu-id="a0a21-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="a0a21-303">Usando essa marca, você pode enviar por push dispositivos de tooall notificações registrados por aquela pessoa.</span><span class="sxs-lookup"><span data-stu-id="a0a21-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="a0a21-304">Olá código a seguir obtém Olá SID do usuário que fez a solicitação e envia um registro de dispositivo do modelo push notificação tooevery para essa pessoa:</span><span class="sxs-lookup"><span data-stu-id="a0a21-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="a0a21-305">Ao se registrar para notificações por push de um cliente autenticado, verifique se a autenticação foi concluída antes de tentar o registro.</span><span class="sxs-lookup"><span data-stu-id="a0a21-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="a0a21-306">Para obter mais informações, consulte [Push toousers] [ 6] no exemplo de início rápido concluído Olá serviço de aplicativo móvel de aplicativos de back-end .NET.</span><span class="sxs-lookup"><span data-stu-id="a0a21-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="a0a21-307">Como: depurar e solucionar problemas de saudação .NET SDK do servidor</span><span class="sxs-lookup"><span data-stu-id="a0a21-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="a0a21-308">O Serviço de Aplicativo do Azure fornece várias técnicas de depuração e de solução de problemas para aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a0a21-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="a0a21-309">Monitorando um Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a21-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="a0a21-310">Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a21-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="a0a21-311">Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0a21-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="a0a21-312">Registro em log</span><span class="sxs-lookup"><span data-stu-id="a0a21-312">Logging</span></span>
<span data-ttu-id="a0a21-313">Você pode escrever tooApp logs de diagnóstico de serviço usando a gravação de rastreamento ASP.NET padrão hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="a0a21-314">Antes de você pode gravar logs de toohello, você deve habilitar o diagnóstico em seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="a0a21-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="a0a21-315">tooenable logs toohello de diagnóstico e de gravação:</span><span class="sxs-lookup"><span data-stu-id="a0a21-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="a0a21-316">Siga as etapas de saudação em [como diagnóstico tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="a0a21-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="a0a21-317">Adicione o seguinte Olá usando a instrução no arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="a0a21-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="a0a21-318">Crie um toowrite do gravador de rastreamento de saudação .NET back-end toohello logs de diagnóstico, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a0a21-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="a0a21-319">Republicar o projeto de servidor e acessar Olá aplicativo móvel back-end tooexecute Olá caminho de código com o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="a0a21-320">Baixar e avaliar logs hello, conforme descrito em [como: baixar logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="a0a21-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="a0a21-321"><a name="local-debug"></a>Depuração local com autenticação</span><span class="sxs-lookup"><span data-stu-id="a0a21-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="a0a21-322">Você pode executar o aplicativo localmente tootest alterações antes de publicá-los toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="a0a21-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="a0a21-323">Para a maioria dos back-ends dos Aplicativos Móveis do Azure, pressione *F5* enquanto estiver no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0a21-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="a0a21-324">No entanto, há algumas considerações adicionais ao usar a autenticação.</span><span class="sxs-lookup"><span data-stu-id="a0a21-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="a0a21-325">Você deve ter um aplicativo móvel com base em nuvem com o aplicativo autenticação/autorização do serviço configurado, e o cliente deve ter um ponto de extremidade de nuvem Olá especificado como o host de logon alternativo hello.</span><span class="sxs-lookup"><span data-stu-id="a0a21-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="a0a21-326">Consulte a documentação de saudação para sua plataforma de cliente para etapas específicas de saudação necessárias.</span><span class="sxs-lookup"><span data-stu-id="a0a21-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="a0a21-327">Verifique se seu back-end móvel tem o [Microsoft.Azure.Mobile.Server.Authentication] instalado.</span><span class="sxs-lookup"><span data-stu-id="a0a21-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="a0a21-328">Em seguida, adicione seguinte hello, depois na classe de inicialização do aplicativo OWIN `MobileAppConfiguration` foi aplicada tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="a0a21-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="a0a21-329">Em Olá anterior de exemplo, você deve configurar Olá *authAudience* e *authIssuer* configurações de aplicativo no Web. config arquivo tooeach ser a URL da raiz do aplicativo, usando Olá HTTPS esquema.</span><span class="sxs-lookup"><span data-stu-id="a0a21-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="a0a21-330">Da mesma forma, você deve definir *authSigningKey* toobe valor de saudação do seu aplicativo de autenticação de chave.</span><span class="sxs-lookup"><span data-stu-id="a0a21-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="a0a21-331">chave de assinatura de saudação tooobtain:</span><span class="sxs-lookup"><span data-stu-id="a0a21-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="a0a21-332">Navegue tooyour aplicativo dentro Olá [portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="a0a21-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="a0a21-333">Clique em **Ferramentas**, **Kudu**, **Ir**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="a0a21-334">No site de gerenciamento Kudu hello, clique em **ambiente**.</span><span class="sxs-lookup"><span data-stu-id="a0a21-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="a0a21-335">Localizar o valor de saudação para *site\_AUTH\_assinatura\_chave*.</span><span class="sxs-lookup"><span data-stu-id="a0a21-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="a0a21-336">Olá usar assinatura de chave para Olá *authSigningKey* parâmetro em sua configuração de aplicativo local.  Seu back-end móvel agora está equipado toovalidate tokens quando em execução localmente, cliente Olá obtém o token de saudação do ponto de extremidade Olá baseado em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a0a21-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portal do Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
