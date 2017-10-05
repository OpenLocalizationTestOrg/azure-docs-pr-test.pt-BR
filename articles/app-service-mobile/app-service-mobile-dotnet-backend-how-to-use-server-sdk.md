---
title: "Como trabalhar com o SDK de servidor back-end do .NET para Aplicativos Móveis | Microsoft Docs"
description: "Aprenda como trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="ad75a-104">Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="ad75a-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="ad75a-105">Este tópico mostra como usar o SDK do servidor de back-end do .NET nos principais cenários dos Aplicativos Móveis do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="ad75a-106">Os Aplicativos Móveis SDK do Azure ajuda você a trabalhar com clientes móveis de seu aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ad75a-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="ad75a-107">O [SDK do .NET Server para Aplicativos Móveis do Azure][2] tem código aberto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad75a-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="ad75a-108">O repositório contém todo o código-fonte, incluindo o conjunto de testes de unidade do SDK para todo o servidor e alguns projetos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="ad75a-109">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="ad75a-109">Reference documentation</span></span>
<span data-ttu-id="ad75a-110">A documentação de referência para o SDK do servidor está localizada aqui: [Referência do .NET dos Aplicativos Móveis do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="ad75a-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="ad75a-111"><a name="create-app"></a>Como criar um back-end do aplicativo móvel do .NET</span><span class="sxs-lookup"><span data-stu-id="ad75a-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="ad75a-112">Se você estiver começando um novo projeto, será possível criar um aplicativo do Serviço de Aplicativo usando o [Portal do Azure] ou o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad75a-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="ad75a-113">Você pode executar o aplicativo do Serviço de Aplicativo localmente ou publicar o projeto em seu aplicativo móvel do Serviço de Aplicativo baseado em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ad75a-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="ad75a-114">Se você estiver adicionando recursos móveis a um projeto existente, veja a seção [Baixar e inicializar o SDK](#install-sdk) .</span><span class="sxs-lookup"><span data-stu-id="ad75a-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="ad75a-115">Criar um back-end do .NET usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ad75a-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="ad75a-116">Para criar um back-end móvel do Serviço de Aplicativo, siga o [Tutorial de início rápido][3] ou execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ad75a-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="ad75a-117">De volta à folha *Introdução*, em **Criar uma API de tabela**, escolha **C#** como a **Linguagem de back-end**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="ad75a-118">Clique em **Download**, extraia os arquivos compactados do projeto em seu computador local e abra a solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad75a-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="ad75a-119">Criar um back-end do .NET usando o Visual Studio 2013 e o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ad75a-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="ad75a-120">Instale o [SDK do Azure para .NET][4] (versão 2.9.0 ou posterior) para criar um projeto dos Aplicativos Móveis no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad75a-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="ad75a-121">Depois de instalar o SDK, crie um aplicativo ASP.NET usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ad75a-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="ad75a-122">Abra a caixa de diálogo **Novo Projeto** (de *Arquivo* > **Novo** > **Projeto...**).</span><span class="sxs-lookup"><span data-stu-id="ad75a-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="ad75a-123">Expanda **Modelos** > **Visual C#** e selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="ad75a-124">Selecione **Aplicativo Web do ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="ad75a-125">Preencha o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="ad75a-125">Fill in the project name.</span></span> <span data-ttu-id="ad75a-126">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-126">Then click **OK**.</span></span>
5. <span data-ttu-id="ad75a-127">Em *Modelos do ASP.NET 4.5.2*, selecione **Aplicativo Móvel do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="ad75a-128">Marque **Host na nuvem** para criar um novo back-end móvel na nuvem no qual você possa publicar esse projeto.</span><span class="sxs-lookup"><span data-stu-id="ad75a-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="ad75a-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-129">Click **OK**.</span></span>

## <span data-ttu-id="ad75a-130"><a name="install-sdk"></a>Como baixar e inicializar o SDK</span><span class="sxs-lookup"><span data-stu-id="ad75a-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="ad75a-131">O SDK está disponível em [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="ad75a-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="ad75a-132">Este pacote inclui a funcionalidade básica necessária para começar a usar o SDK.</span><span class="sxs-lookup"><span data-stu-id="ad75a-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="ad75a-133">Para inicializar o SDK, você precisa executar ações no objeto **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="ad75a-134">Instalar o SDK</span><span class="sxs-lookup"><span data-stu-id="ad75a-134">Install the SDK</span></span>
<span data-ttu-id="ad75a-135">Para instalar o SDK, clique com o botão direito do mouse no projeto do servidor no Visual Studio, selecione **Gerenciar Pacotes NuGet**, procure o pacote [Microsoft.Azure.Mobile.Server] e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="ad75a-136"><a name="server-project-setup"></a> Inicializar o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="ad75a-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="ad75a-137">Um projeto do servidor back-end .NET é inicializado de modo semelhante a outros projetos do ASP.NET, pela inclusão de uma classe de inicialização do OWIN.</span><span class="sxs-lookup"><span data-stu-id="ad75a-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="ad75a-138">Não se esqueça de referenciar o pacote NuGet `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="ad75a-139">Para adicionar essa classe no Visual Studio, clique com o botão direito do mouse em seu projeto do servidor e escolha **Adicionar** >
**Novo Item**, **Web** > **Geral** > **Classe de inicialização OWIN**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="ad75a-140">Uma classe é gerada com o seguinte atributo:</span><span class="sxs-lookup"><span data-stu-id="ad75a-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="ad75a-141">No método `Configuration()` da classe de inicialização OWIN, use um objeto **HttpConfiguration** para configurar o ambiente de Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="ad75a-142">O exemplo a seguir inicializa o projeto do servidor, sem nenhum recurso adicional:</span><span class="sxs-lookup"><span data-stu-id="ad75a-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="ad75a-143">Para habilitar recursos individuais, você deve chamar os métodos de extensão no objeto **MobileAppConfiguration** antes de chamar **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="ad75a-144">Por exemplo, o código a seguir adiciona as rotas padrão para todos os controladores de API que têm o atributo `[MobileAppController]` durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="ad75a-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="ad75a-145">O início rápido do servidor do portal do Azure chama **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="ad75a-146">Isso equivale à configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad75a-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="ad75a-147">Os métodos de extensão usados são:</span><span class="sxs-lookup"><span data-stu-id="ad75a-147">The extension methods used are:</span></span>

* <span data-ttu-id="ad75a-148">`AddMobileAppHomeController()` fornece a home page padrão dos Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="ad75a-149">`MapApiControllers()` fornece recursos personalizados de API para controladores de API Web decorados com o atributo `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="ad75a-150">`AddTables()` fornece um mapeamento dos pontos de extremidade `/tables` para controladores de tabela.</span><span class="sxs-lookup"><span data-stu-id="ad75a-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="ad75a-151">`AddTablesWithEntityFramework()` é uma abreviação para mapeamento de pontos de extremidade `/tables` usando os controladores baseados no Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="ad75a-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="ad75a-152">`AddPushNotifications()` fornece um método simples de registro de dispositivos para Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="ad75a-153">`MapLegacyCrossDomainController()` fornece os cabeçalhos de CORS padrão para o desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="ad75a-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="ad75a-154">Extensões SDK</span><span class="sxs-lookup"><span data-stu-id="ad75a-154">SDK extensions</span></span>
<span data-ttu-id="ad75a-155">Os seguintes pacotes com base em extensão no NuGet fornecem vários recursos móveis que podem ser usados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="ad75a-156">Habilitar extensões durante a inicialização usando o objeto **MobileAppConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="ad75a-157">[Microsoft.Azure.Mobile.Server.Quickstart] Dá suporte à configuração básica dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="ad75a-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="ad75a-158">Adicionado à configuração chamando o método de extensão **UseDefaultConfiguration** durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="ad75a-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="ad75a-159">Essa extensão inclui as seguintes extensões: Notificações, Autenticação, Entidade, Tabelas, pacotes Crossdomain e Home.</span><span class="sxs-lookup"><span data-stu-id="ad75a-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="ad75a-160">Esse pacote é usado pelo Início rápido dos Aplicativos Móveis disponíveis no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="ad75a-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa a página padrão *este aplicativo móvel está em execução* na raiz do site.</span><span class="sxs-lookup"><span data-stu-id="ad75a-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="ad75a-162">Adicione à configuração chamando o método de extensão **AddMobileAppHomeController** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="ad75a-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) inclui classes para trabalhar com dados e define o pipeline de dados.</span><span class="sxs-lookup"><span data-stu-id="ad75a-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="ad75a-164">Adicione à configuração chamando o método de extensão **AddTables** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="ad75a-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permite que o Entity Framework acesse dados no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ad75a-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="ad75a-166">Adicionar à configuração chamando o método de extensão **AddTablesWithEntityFramework** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="ad75a-167">[Microsoft.Azure.Mobile.Server.Authentication] Permite a autenticação e define o middleware OWIN usado para validar tokens.</span><span class="sxs-lookup"><span data-stu-id="ad75a-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="ad75a-168">Adicionar à configuração chamando os métodos de extensão **AddAppServiceAuthentication** e **IAppBuilder**.**UseAppServiceAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="ad75a-169">[Microsoft.Azure.Mobile.Server.Notifications] permite as notificações por push e define um ponto de extremidade de registro push.</span><span class="sxs-lookup"><span data-stu-id="ad75a-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="ad75a-170">Adicionar à configuração chamando o método de extensão **AddPushNotifications** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="ad75a-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Cria um controlador que fornece dados para os navegadores da Web herdados do seu Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="ad75a-172">Adicione à configuração chamando o método de extensão **MapLegacyCrossDomainController** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="ad75a-173">[Microsoft.Azure.Mobile.Server.Login] fornece o método AppServiceLoginHandler.CreateToken(), que é um método estático usado nos cenários de autenticação personalizada.</span><span class="sxs-lookup"><span data-stu-id="ad75a-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="ad75a-174"><a name="publish-server-project"></a>Como publicar o projeto do servidor</span><span class="sxs-lookup"><span data-stu-id="ad75a-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="ad75a-175">Essa seção mostra como publicar seu projeto de back-end do .NET a partir do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad75a-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="ad75a-176">Você também pode implantar seu projeto de back-end usando Git ou qualquer um dos outros métodos abordados na [documentação de implantação do Serviço de Aplicativo do Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ad75a-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="ad75a-177">No Visual Studio, recompile o projeto para restaurar os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad75a-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="ad75a-178">No Gerenciador de Soluções, clique com o botão direito no projeto e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="ad75a-179">Na primeira vez que você publicar, precisará definir um perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="ad75a-180">Quando já tiver um perfil definido, selecione-o e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="ad75a-181">Se solicitado a selecionar um destino de publicação, clique em **Serviço de Aplicativo do Microsoft Azure** > **Avançar** e (se necessário) entre com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="ad75a-182">O Visual Studio baixa e armazena suas configurações de publicação com segurança diretamente do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="ad75a-183">Escolha sua **Assinatura**, selecione o **Tipo de Recurso** em **Exibição**, expanda **Aplicativo Móvel**, clique no back-end do Aplicativo Móvel e então clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="ad75a-184">Verifique as informações de perfil de publicação e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="ad75a-185">Quando o back-end do aplicativo móvel for publicado com êxito, você verá uma página de aterrissagem indicando êxito.</span><span class="sxs-lookup"><span data-stu-id="ad75a-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="ad75a-186"><a name="define-table-controller"></a> Como definir um controlador de tabela</span><span class="sxs-lookup"><span data-stu-id="ad75a-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="ad75a-187">Defina um Controlador de Tabela para expor uma tabela SQL a clientes móveis.</span><span class="sxs-lookup"><span data-stu-id="ad75a-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="ad75a-188">A configuração de um Controlador de Tabela exige três etapas:</span><span class="sxs-lookup"><span data-stu-id="ad75a-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="ad75a-189">Criar uma classe DTO (Objeto de Transferência de Dados).</span><span class="sxs-lookup"><span data-stu-id="ad75a-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="ad75a-190">Configurar uma referência de tabela na classe DbContext móvel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="ad75a-191">Criar um controlador de tabela.</span><span class="sxs-lookup"><span data-stu-id="ad75a-191">Create a table controller.</span></span>

<span data-ttu-id="ad75a-192">Um DTO (objeto de transferência de dados) é um objeto C# simples que herda de `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="ad75a-193">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ad75a-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="ad75a-194">O DTO é usado para definir a tabela no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ad75a-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="ad75a-195">Para criar a entrada de banco de dados, adicione uma propriedade `DbSet<>` ao DbContext que você está usando.</span><span class="sxs-lookup"><span data-stu-id="ad75a-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="ad75a-196">No modelo de projeto padrão para Aplicativos Móveis do Azure, o DbContext é chamado de `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="ad75a-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="ad75a-197">Se você tiver o SDK do Azure instalado, poderá criar um controlador de tabela de modelo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ad75a-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="ad75a-198">Clique com o botão direito do mouse na pasta Controladores e selecione **Adicionar** > **Controlador...**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="ad75a-199">Selecione a opção **Controlador de Tabela de Aplicativos Móveis do Azure** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="ad75a-200">No diálogo **Adicionar controlador** :</span><span class="sxs-lookup"><span data-stu-id="ad75a-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="ad75a-201">Na lista suspensa **Classe modelo** , selecione o novo DTO.</span><span class="sxs-lookup"><span data-stu-id="ad75a-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="ad75a-202">Na lista suspensa **DbContext** , selecione a classe DbContext do serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="ad75a-203">O nome do controlador é criado para você.</span><span class="sxs-lookup"><span data-stu-id="ad75a-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="ad75a-204">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-204">Click **Add**.</span></span>

<span data-ttu-id="ad75a-205">O projeto de início rápido do servidor contém um exemplo de um simples **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="ad75a-206"><a name="adjust-pagesize"></a>Como ajustar o tamanho de paginação da tabela</span><span class="sxs-lookup"><span data-stu-id="ad75a-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="ad75a-207">Por padrão, os Aplicativos Móveis do Azure retornam 50 registros por solicitação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="ad75a-208">A paginação garante que o cliente não associará o thread de interface do usuário nem o servidor por muito tempo, garantindo uma boa experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="ad75a-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="ad75a-209">Para alterar o tamanho da tabela de paginação, aumente o "tamanho de consulta permitido" e o tamanho de página do lado do cliente. O “tamanho de consulta permitido" no lado do servidor é ajustado usando o atributo `EnableQuery`:</span><span class="sxs-lookup"><span data-stu-id="ad75a-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="ad75a-210">Verifique se PageSize é igual ou maior do que o tamanho solicitado pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="ad75a-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="ad75a-211">Consulte a documentação de instruções específicas do cliente para obter detalhes sobre a alteração do tamanho de página do cliente.</span><span class="sxs-lookup"><span data-stu-id="ad75a-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="ad75a-212">Como definir um controlador da API personalizada</span><span class="sxs-lookup"><span data-stu-id="ad75a-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="ad75a-213">O controlador da API personalizada fornece as funções mais básicas de back-end do Aplicativo Móvel, expondo um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ad75a-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="ad75a-214">Você pode registrar um controlador da API específico do dispositivo móvel usando o atributo [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="ad75a-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="ad75a-215">O atributo `MobileAppController` registra a rota, configura o serializador JSON dos Aplicativos Móveis e ativa a [verificação de versão de cliente](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ad75a-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="ad75a-216">No Visual Studio, clique com o botão direito do mouse na pasta Controladores, clique em **Adicionar** > **Controlador**, selecione **Controlador da API Web 2&mdash;Vazio** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="ad75a-217">Forneça um **Nome do controlador**, como `CustomController`, e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="ad75a-218">No novo arquivo classe de controlador, adicione a seguinte instrução de uso.</span><span class="sxs-lookup"><span data-stu-id="ad75a-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="ad75a-219">Aplique o atributo **[MobileAppController]** à definição de classe do controlador de API, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad75a-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="ad75a-220">No arquivo App_Start/Startup.MobileApp.cs, adicione uma chamada ao método de extensão **MapApiControllers**, como no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="ad75a-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="ad75a-221">Você também pode usar o método de extensão `UseDefaultConfiguration()` em vez de `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="ad75a-222">Qualquer controlador que não tenha o **MobileAppControllerAttribute** aplicado ainda poderá ser acessado pelos clientes, mas não será consumido corretamente por clientes que usem qualquer SDK do cliente do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="ad75a-223">Como trabalhar com autenticação</span><span class="sxs-lookup"><span data-stu-id="ad75a-223">How to: Work with authentication</span></span>
<span data-ttu-id="ad75a-224">Os Aplicativos Móveis do Azure usam autenticação/autorização do Serviço de Aplicativo para proteger seu back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="ad75a-225">Esta seção mostra como executar as seguintes tarefas relacionadas à autenticação em seu projeto de servidor de back-end do .NET:</span><span class="sxs-lookup"><span data-stu-id="ad75a-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="ad75a-226">Como: Adicionar autenticação a um projeto do servidor</span><span class="sxs-lookup"><span data-stu-id="ad75a-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="ad75a-227">Como usar a autenticação personalizada para o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ad75a-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="ad75a-228">Como recuperar informações do usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="ad75a-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="ad75a-229">Como restringir o acesso a dados para usuários autorizados</span><span class="sxs-lookup"><span data-stu-id="ad75a-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="ad75a-230"><a name="add-auth"></a>Como: Adicionar autenticação a um projeto do servidor</span><span class="sxs-lookup"><span data-stu-id="ad75a-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="ad75a-231">Você pode adicionar autenticação ao seu projeto de servidor estendendo o objeto **MobileAppConfiguration** e configurando o middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="ad75a-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="ad75a-232">Quando você instala o pacote [Microsoft.Azure.Mobile.Server.Quickstart] e chamar o método de extensão **UseDefaultConfiguration** , você pode pular a etapa 3.</span><span class="sxs-lookup"><span data-stu-id="ad75a-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="ad75a-233">No Visual Studio, instale o pacote [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="ad75a-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="ad75a-234">No arquivo de projeto Startup.cs, adicione a seguinte linha de código ao início do método **Configuração** :</span><span class="sxs-lookup"><span data-stu-id="ad75a-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="ad75a-235">Este componente de middleware OWIN valida os tokens emitidos pelo gateway do Serviço de Aplicativo associado.</span><span class="sxs-lookup"><span data-stu-id="ad75a-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="ad75a-236">Adicione o atributo `[Authorize]` a qualquer controlador ou método que exija autenticação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="ad75a-237">Para saber como autenticar clientes no back-end dos Aplicativos Móveis, veja [Adicionar autenticação ao seu aplicativo](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="ad75a-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="ad75a-238"><a name="custom-auth"></a>Como usar a autenticação personalizada para o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ad75a-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="ad75a-239">Caso não queria usar um dos provedores de Autenticação/Autorização do Serviço de Aplicativo, você pode implementar seu próprio sistema de logon.</span><span class="sxs-lookup"><span data-stu-id="ad75a-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="ad75a-240">Instale o pacote [Microsoft.Azure.Mobile.Server.Login] para ajudá-lo na geração de token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="ad75a-241">Forneça seu próprio código para validar as credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="ad75a-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="ad75a-242">Por exemplo, você pode comparar com senhas com sal e hash aplicados em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ad75a-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="ad75a-243">No exemplo abaixo, o método `isValidAssertion()` (definido em outro lugar) é responsável por essas verificações.</span><span class="sxs-lookup"><span data-stu-id="ad75a-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="ad75a-244">A autenticação personalizada é exposta criando um ApiController e expondo as ações `register` e `login`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="ad75a-245">O cliente deve usar uma interface do usuário personalizada para coletar as informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="ad75a-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="ad75a-246">As informações são enviadas para a API com uma chamada HTTP POST padrão.</span><span class="sxs-lookup"><span data-stu-id="ad75a-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="ad75a-247">Depois que o servidor valida a asserção, um token é emitido usando o método `AppServiceLoginHandler.CreateToken()` .</span><span class="sxs-lookup"><span data-stu-id="ad75a-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="ad75a-248">O ApiController **não deve** usar o atributo `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="ad75a-249">Uma ação `login` de exemplo:</span><span class="sxs-lookup"><span data-stu-id="ad75a-249">An example `login` action:</span></span>

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

<span data-ttu-id="ad75a-250">No exemplo anterior, LoginResult e LoginResultUser são objetos serializáveis que expõem as propriedades necessárias.</span><span class="sxs-lookup"><span data-stu-id="ad75a-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="ad75a-251">O cliente espera que as respostas de logon sejam retornadas como objetos JSON na forma:</span><span class="sxs-lookup"><span data-stu-id="ad75a-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="ad75a-252">O método `AppServiceLoginHandler.CreateToken()` inclui um parâmetro *audience* e um parâmetro *issuer*.</span><span class="sxs-lookup"><span data-stu-id="ad75a-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="ad75a-253">Ambos os parâmetros são definidos para a URL da raiz do seu aplicativo usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ad75a-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="ad75a-254">Da mesma forma, você deve definir *secretKey* como o valor da chave de conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="ad75a-255">Não distribua a chave de assinatura em um cliente, já que ela pode ser usada para forjar chaves e se fazer passar por usuários.</span><span class="sxs-lookup"><span data-stu-id="ad75a-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="ad75a-256">Você poderá obter a chave de assinatura enquanto estiver hospedado no Serviço de Aplicativo consultando a variável de ambiente *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="ad75a-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="ad75a-257">Se for necessário em um contexto de depuração local, siga as instruções na seção [Depuração local com autenticação](#local-debug) para recuperar a chave e armazená-la como uma configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="ad75a-258">O token emitido também pode incluir outras declarações e uma data de expiração.</span><span class="sxs-lookup"><span data-stu-id="ad75a-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="ad75a-259">No mínimo, o token emitido deve incluir uma declaração (**sub**) de assunto.</span><span class="sxs-lookup"><span data-stu-id="ad75a-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="ad75a-260">Você pode dar suporte ao método `loginAsync()` de cliente padrão sobrecarregando a rota de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="ad75a-261">Se o cliente chama `client.loginAsync('custom');` para fazer logon, a rota deve ser `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="ad75a-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="ad75a-262">Você pode definir a rota para o controlador de autenticação personalizada usando `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="ad75a-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="ad75a-263">Usar a abordagem `loginAsync()` garante que o token de autenticação está conectado a todas as chamadas subsequentes ao serviço.</span><span class="sxs-lookup"><span data-stu-id="ad75a-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="ad75a-264"><a name="user-info"></a>Como recuperar informações do usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="ad75a-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="ad75a-265">Quando um usuário é autenticado pelo serviço de aplicativo, você pode acessar a ID de usuário atribuída e outras informações no seu código de back-end do .NET.</span><span class="sxs-lookup"><span data-stu-id="ad75a-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="ad75a-266">As informações do usuário podem ser usadas para tomar decisões de autorização no back-end.</span><span class="sxs-lookup"><span data-stu-id="ad75a-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="ad75a-267">O código abaixo obtém a ID do usuário associada a uma solicitação:</span><span class="sxs-lookup"><span data-stu-id="ad75a-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="ad75a-268">A SID é derivado da ID de usuário específica do provedor e é estática para um determinado usuário e o provedor de logon.</span><span class="sxs-lookup"><span data-stu-id="ad75a-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="ad75a-269">O SID é nulo para tokens de autenticação inválidos.</span><span class="sxs-lookup"><span data-stu-id="ad75a-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="ad75a-270">O Serviço de Aplicativo também permite solicitar declarações específicas do provedor de logon.</span><span class="sxs-lookup"><span data-stu-id="ad75a-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="ad75a-271">Cada provedor de identidade pode fornecer mais informações usando o SDK do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="ad75a-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="ad75a-272">Por exemplo, você pode usar a API do Graph do Facebook para obter informações de amigos.</span><span class="sxs-lookup"><span data-stu-id="ad75a-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="ad75a-273">Você pode especificar as declarações solicitadas na folha do provedor no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad75a-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="ad75a-274">Algumas declarações exigem configuração adicional com o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="ad75a-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="ad75a-275">O código a seguir chama o método de extensão **GetAppServiceIdentityAsync** para obter as credenciais de logon, que incluem o token de acesso necessário para fazer solicitações na Graph API do Facebook:</span><span class="sxs-lookup"><span data-stu-id="ad75a-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="ad75a-276">Adicione uma instrução using `System.Security.Principal` para fornecer o método de extensão **GetAppServiceIdentityAsync** .</span><span class="sxs-lookup"><span data-stu-id="ad75a-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="ad75a-277"><a name="authorize"></a>Como restringir o acesso a dados para usuários autorizados</span><span class="sxs-lookup"><span data-stu-id="ad75a-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="ad75a-278">Na seção anterior, mostramos como recuperar a ID de usuário de um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="ad75a-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="ad75a-279">Você pode restringir o acesso a dados e outros recursos com base nesse valor.</span><span class="sxs-lookup"><span data-stu-id="ad75a-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="ad75a-280">Por exemplo, adicionar uma coluna userId às tabelas e filtrar os resultados da consulta segundo a ID de usuário é uma maneira simples de limitar os dados retornados apenas aos usuários autorizados.</span><span class="sxs-lookup"><span data-stu-id="ad75a-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="ad75a-281">O código a seguir retorna linhas de dados somente quando o SID corresponde ao valor na coluna UserId na tabela TodoItem:</span><span class="sxs-lookup"><span data-stu-id="ad75a-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="ad75a-282">O método `Query()` retorna um `IQueryable` que pode ser manipulado pelo LINQ para tratar da filtragem.</span><span class="sxs-lookup"><span data-stu-id="ad75a-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="ad75a-283">Adicionar notificações por push para um projeto do servidor</span><span class="sxs-lookup"><span data-stu-id="ad75a-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="ad75a-284">Adicione notificações por push ao seu projeto do servidor estendendo o objeto **MobileAppConfiguration** e criando um cliente dos Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="ad75a-285">No Visual Studio, clique com o botão direito do mouse no projeto do servidor e clique em **Gerenciar pacotes NuGet**, pesquise por `Microsoft.Azure.Mobile.Server.Notifications` e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="ad75a-286">Repita essa etapa para instalar o pacote `Microsoft.Azure.NotificationHubs` , que inclui a biblioteca do cliente dos Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="ad75a-287">Em App_Start/Startup.MobileApp.cs, adicione uma chamada ao método de extensão **AddPushNotifications** durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="ad75a-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="ad75a-288">Adicione o código a seguir que cria um cliente de Hubs de Notificação:</span><span class="sxs-lookup"><span data-stu-id="ad75a-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="ad75a-289">Você agora pode usar o cliente de Hubs de Notificação para enviar notificações por push para dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="ad75a-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="ad75a-290">Para obter mais informações, veja [Adicionar notificações por push ao seu aplicativo](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="ad75a-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="ad75a-291">Para saber mais sobre os Hubs de Notificação, confira [Visão geral dos Hubs de Notificação](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad75a-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="ad75a-292"><a name="tags"></a>Como habilitar envios direcionados por push usando marcações</span><span class="sxs-lookup"><span data-stu-id="ad75a-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="ad75a-293">Os Hubs de Notificação permitem que você envie notificações direcionadas para registros específicos usando marcas.</span><span class="sxs-lookup"><span data-stu-id="ad75a-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="ad75a-294">Várias marcações são criadas automaticamente:</span><span class="sxs-lookup"><span data-stu-id="ad75a-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="ad75a-295">A ID de instalação identifica um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="ad75a-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="ad75a-296">A ID de usuário baseada no SID autenticado identifica um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="ad75a-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="ad75a-297">A ID de instalação pode ser acessada na propriedade **installationId** do **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="ad75a-298">O exemplo a seguir mostra como usar uma ID de instalação para adicionar uma marca a uma instalação específica nos Hubs de Notificação:</span><span class="sxs-lookup"><span data-stu-id="ad75a-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="ad75a-299">As marcações fornecidas pelo cliente durante o registro de notificação por push são ignoradas pelo back-end ao criar a instalação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="ad75a-300">Para habilitar um cliente a adicionar marcas à instalação, você deverá criar uma API personalizada que adiciona marcas usando o padrão anterior.</span><span class="sxs-lookup"><span data-stu-id="ad75a-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="ad75a-301">Confira [Marcações de notificação por push adicionadas pelo cliente][5] no exemplo de início rápido concluído dos Aplicativos Móveis do Serviço de Aplicativo para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="ad75a-302"><a name="push-user"></a>Como enviar notificações por push para um usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="ad75a-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="ad75a-303">Quando um usuário autenticado se registra para notificações por push, uma marca de ID de usuário é adicionada automaticamente ao registro.</span><span class="sxs-lookup"><span data-stu-id="ad75a-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="ad75a-304">Usando essa marca, você pode enviar notificações por push para todos os dispositivos registrados por aquela pessoa.</span><span class="sxs-lookup"><span data-stu-id="ad75a-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="ad75a-305">O código abaixo obtém o SID do usuário que fez a solicitação e envia um modelo de notificação por push para cada registro de dispositivo daquela pessoa:</span><span class="sxs-lookup"><span data-stu-id="ad75a-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="ad75a-306">Ao se registrar para notificações por push de um cliente autenticado, verifique se a autenticação foi concluída antes de tentar o registro.</span><span class="sxs-lookup"><span data-stu-id="ad75a-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="ad75a-307">Para saber mais, confira [Enviar por push para usuários][6] no exemplo de início rápido dos Aplicativos Móveis do Serviço de Aplicativo para back-end do .NET.</span><span class="sxs-lookup"><span data-stu-id="ad75a-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="ad75a-308">Como depurar e solucionar problemas do SDK do .NET Server</span><span class="sxs-lookup"><span data-stu-id="ad75a-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="ad75a-309">O Serviço de Aplicativo do Azure fornece várias técnicas de depuração e de solução de problemas para aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ad75a-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="ad75a-310">Monitorando um Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ad75a-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="ad75a-311">Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ad75a-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="ad75a-312">Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ad75a-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="ad75a-313">Registro em log</span><span class="sxs-lookup"><span data-stu-id="ad75a-313">Logging</span></span>
<span data-ttu-id="ad75a-314">É possível gravar em logs de diagnóstico do Serviço de Aplicativo usando a gravação de rastreamento padrão do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ad75a-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="ad75a-315">Antes de gravar os logs, habilite o diagnóstico no back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="ad75a-316">Para habilitar o diagnóstico e gravar logs:</span><span class="sxs-lookup"><span data-stu-id="ad75a-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="ad75a-317">Siga as etapas em [Como habilitar o diagnóstico](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="ad75a-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="ad75a-318">Adicione a seguinte instrução de uso em seu arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="ad75a-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="ad75a-319">Crie um gravador de rastreamento para gravar de back-end do .NET para os logs de diagnóstico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ad75a-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="ad75a-320">Republique seu projeto de servidor e acesse o back-end do aplicativo móvel para executar o caminho de código com o registro em log.</span><span class="sxs-lookup"><span data-stu-id="ad75a-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="ad75a-321">Baixe e avalie os logs, conforme descrito em [Como baixar logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="ad75a-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="ad75a-322"><a name="local-debug"></a>Depuração local com autenticação</span><span class="sxs-lookup"><span data-stu-id="ad75a-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="ad75a-323">Você pode executar seu aplicativo localmente a fim de testar as alterações antes de publicá-lo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="ad75a-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="ad75a-324">Para a maioria dos back-ends dos Aplicativos Móveis do Azure, pressione *F5* enquanto estiver no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad75a-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="ad75a-325">No entanto, há algumas considerações adicionais ao usar a autenticação.</span><span class="sxs-lookup"><span data-stu-id="ad75a-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="ad75a-326">Você deve ter um aplicativo móvel baseado em nuvem com a Autenticação/Autorização do Serviço de Aplicativo configurado, e o cliente deve ter o ponto de extremidade de nuvem especificado como o host de logon alternativo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="ad75a-327">Confira a documentação da sua plataforma cliente para saber as etapas específicas necessárias.</span><span class="sxs-lookup"><span data-stu-id="ad75a-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="ad75a-328">Verifique se seu back-end móvel tem o [Microsoft.Azure.Mobile.Server.Authentication] instalado.</span><span class="sxs-lookup"><span data-stu-id="ad75a-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="ad75a-329">Em seguida, na classe de inicialização OWIN do aplicativo, adicione o seguinte, após aplicar `MobileAppConfiguration` ao seu `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="ad75a-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="ad75a-330">No exemplo anterior, você deve definir as configurações de aplicativo *authAudience* e *authIssuer* no arquivo Web.config para que cada uma seja a URL da raiz do aplicativo usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ad75a-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="ad75a-331">Da mesma forma, você deve definir *authSigningKey* como o valor da chave de autenticação de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad75a-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="ad75a-332">Para obter a chave de assinatura:</span><span class="sxs-lookup"><span data-stu-id="ad75a-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="ad75a-333">Navegue até o aplicativo no [Portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="ad75a-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="ad75a-334">Clique em **Ferramentas**, **Kudu**, **Ir**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="ad75a-335">No site de gerenciamento do Kudu, clique em **Ambiente**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="ad75a-336">Localize o valor para *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="ad75a-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="ad75a-337">Use a chave de assinatura para o parâmetro *authSigningKey* em sua configuração de aplicativo local.</span><span class="sxs-lookup"><span data-stu-id="ad75a-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="ad75a-338">O back-end móvel agora está equipado para validar tokens quando em execução localmente, cujo token o cliente obtém do ponto de extremidade baseados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="ad75a-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="ad75a-339">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ad75a-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="ad75a-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="ad75a-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="ad75a-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="ad75a-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="ad75a-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="ad75a-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="ad75a-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="ad75a-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="ad75a-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="ad75a-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="ad75a-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="ad75a-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
