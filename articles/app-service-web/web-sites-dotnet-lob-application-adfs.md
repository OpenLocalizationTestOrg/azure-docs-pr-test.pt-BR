---
title: "Criar um aplicativo de linha de negócios do Azure com autenticação do AD FS | Microsoft Docs"
description: "Saiba como criar um aplicativo de linha de negócios no Serviço de Aplicativo do Azure que realiza a autenticação com o STS local. Este tutorial destina-se ao AD FS como STS local."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="34dce-104">Criar um aplicativo de linha de negócios do Azure com autenticação do AD FS</span><span class="sxs-lookup"><span data-stu-id="34dce-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="34dce-105">Este artigo mostra como criar um aplicativo de linha de negócios ASP.NET MVC no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) usando os [Serviços de Federação do Active Directory](http://technet.microsoft.com/library/hh831502.aspx) locais como o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="34dce-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="34dce-106">Este cenário poderá funcionar quando você desejar criar aplicativos de linha de negócios no Serviço de Aplicativo do Azure, mas sua organização exigir que os dados de diretório sejam armazenados no local.</span><span class="sxs-lookup"><span data-stu-id="34dce-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="34dce-107">Para uma visão geral das diferentes opções de autenticação e autorização corporativas para o Serviço de Aplicativo do Azure, consulte [Autenticar com o Active Directory local em seu aplicativo do Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="34dce-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="34dce-108">O que você compilará</span><span class="sxs-lookup"><span data-stu-id="34dce-108">What you will build</span></span>
<span data-ttu-id="34dce-109">Você criará um aplicativo básico do ASP.NET nos Aplicativos Web do Serviço de Aplicativo do Azure com os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="34dce-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="34dce-110">Autentica usuários no AD FS</span><span class="sxs-lookup"><span data-stu-id="34dce-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="34dce-111">Usa `[Authorize]` para autorizar usuários para diferentes ações CRUD</span><span class="sxs-lookup"><span data-stu-id="34dce-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="34dce-112">Configuração estática para depuração no Visual Studio e publicação em Aplicativos Web do Serviço de Aplicativo do Azure (configurar uma vez, depurar e publicar a qualquer momento)</span><span class="sxs-lookup"><span data-stu-id="34dce-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="34dce-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="34dce-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="34dce-114">É necessário o seguinte para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="34dce-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="34dce-115">Uma implantação do AD FS local (para uma explicação de ponta a ponta do laboratório de teste neste tutorial, consulte: [Laboratório de teste: STS autônomo com o AD FS na VM do Azure (apenas para teste)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="34dce-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="34dce-116">Permissões para criar o objeto de confiança de terceira parte confiável no gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="34dce-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="34dce-117">Visual Studio 2013 Atualização 4 ou posterior</span><span class="sxs-lookup"><span data-stu-id="34dce-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="34dce-118">[SDK do Azure 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou posterior</span><span class="sxs-lookup"><span data-stu-id="34dce-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="34dce-119">Usar o aplicativo de exemplo para modelo de linha de negócios</span><span class="sxs-lookup"><span data-stu-id="34dce-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="34dce-120">O aplicativo de exemplo neste tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), foi criado pela equipe do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="34dce-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="34dce-121">Como o AD FS dá suporte ao Web Services Federation, é possível usá-lo como um modelo para criar aplicativos de linha de negócios com facilidade.</span><span class="sxs-lookup"><span data-stu-id="34dce-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="34dce-122">Ele tem as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="34dce-122">It has the following features:</span></span>

* <span data-ttu-id="34dce-123">Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) para autenticar com uma implantação do AD FS local</span><span class="sxs-lookup"><span data-stu-id="34dce-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="34dce-124">Funcionalidade de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="34dce-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="34dce-125">Usa [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (em vez do Windows Identity Foundation), que é o futuro do ASP.NET e é muito mais simples de configurar para autenticação e autorização do que o WIF</span><span class="sxs-lookup"><span data-stu-id="34dce-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="34dce-126">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="34dce-126">Set up the sample application</span></span>
1. <span data-ttu-id="34dce-127">Clone ou baixe a solução de exemplo em [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) para seu diretório local.</span><span class="sxs-lookup"><span data-stu-id="34dce-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34dce-128">As instruções em [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) mostram como configurar o aplicativo com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="34dce-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="34dce-129">Mas, neste tutorial, você pode configurá-lo com o AD FS, portanto, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="34dce-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="34dce-130">Abra a solução e abra Controllers\AccountController.cs no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="34dce-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="34dce-131">Você verá que o código simplesmente emite um desafio de autenticação para autenticar o usuário usando o WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="34dce-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="34dce-132">Todas as autenticações são configuradas em App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="34dce-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="34dce-133">Abra App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="34dce-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="34dce-134">No método `ConfigureAuth`, observe a linha:</span><span class="sxs-lookup"><span data-stu-id="34dce-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="34dce-135">No mundo OWIN, este trecho é realmente o mínimo necessário para configurar a autenticação do WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="34dce-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="34dce-136">Ele é mais simples e mais elegante que o WIF, em que o Web.config é injetado com XML em todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="34dce-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="34dce-137">A única informação que você precisa é o identificador da terceira parte confiável (RP) e a URL do arquivo de metadados do serviço do AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="34dce-138">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="34dce-138">Here's an example:</span></span>
   
   * <span data-ttu-id="34dce-139">Identificador RP: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="34dce-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="34dce-140">Endereço de metadados: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="34dce-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="34dce-141">No App_Start\Startup.Auth.cs, altere as seguintes definições de cadeia de caracteres estática:</span><span class="sxs-lookup"><span data-stu-id="34dce-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="34dce-142">Agora, faça as alterações correspondentes no Web.config.</span><span class="sxs-lookup"><span data-stu-id="34dce-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="34dce-143">Abra o Web.config e modifique as seguintes configurações de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="34dce-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="34dce-144">Preencha os valores de chave com base em seu respectivo ambiente.</span><span class="sxs-lookup"><span data-stu-id="34dce-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="34dce-145">Compile o aplicativo para verificar se não existem erros.</span><span class="sxs-lookup"><span data-stu-id="34dce-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="34dce-146">É isso.</span><span class="sxs-lookup"><span data-stu-id="34dce-146">That's it.</span></span> <span data-ttu-id="34dce-147">Agora o aplicativo de exemplo está pronto para funcionar com o AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="34dce-148">Você ainda precisa configurar uma relação de confiança RP com esse aplicativo no AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="34dce-149">Implantar o aplicativo de exemplo para os Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="34dce-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="34dce-150">Aqui, você publica o aplicativo para um aplicativo Web nos Aplicativos Web do Serviço de Aplicativo, preservando o ambiente de depuração.</span><span class="sxs-lookup"><span data-stu-id="34dce-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="34dce-151">Observe que você pretende publicar o aplicativo antes que ele tenha uma relação de confiança RP com o AD FS, para que autenticação ainda não funcione.</span><span class="sxs-lookup"><span data-stu-id="34dce-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="34dce-152">No entanto, se fizer isso agora, você poderá ter a URL do aplicativo Web que também usará para configurar a relação de confiança RP mais tarde.</span><span class="sxs-lookup"><span data-stu-id="34dce-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="34dce-153">Clique duas vezes com o botão direito em seu projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="34dce-154">Clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="34dce-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="34dce-155">Se você não tiver se inscrito no Azure, clique em **Entrar** e use a conta da Microsoft para sua assinatura do Azure para entrar.</span><span class="sxs-lookup"><span data-stu-id="34dce-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="34dce-156">Depois de conectado, clique em **Novo** para criar um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="34dce-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="34dce-157">Preencha todos os campos obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="34dce-157">Fill in all required fields.</span></span> <span data-ttu-id="34dce-158">Você vai conectar-se a dados locais posteriormente, assim, não crie um banco de dados para este aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="34dce-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="34dce-159">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-159">Click **Create**.</span></span> <span data-ttu-id="34dce-160">Depois que o aplicativo Web for criado, a caixa de diálogo Publicar Web será aberta.</span><span class="sxs-lookup"><span data-stu-id="34dce-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="34dce-161">Em **URL de destino**, altere **http** para **https**.</span><span class="sxs-lookup"><span data-stu-id="34dce-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="34dce-162">Copie a URL inteira em um editor de texto para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="34dce-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="34dce-163">Em seguida, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="34dce-164">No Visual Studio, abra **Web.Release.config** em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="34dce-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="34dce-165">Insira o seguinte XML na marca `<configuration>` e substitua o valor de chave por sua URL do aplicativo Web de publicação.</span><span class="sxs-lookup"><span data-stu-id="34dce-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="34dce-166">Quando terminar, você terá dois identificadores RP configurados em seu projeto, um para o seu ambiente de depuração no Visual Studio e um para o aplicativo Web publicado no Azure.</span><span class="sxs-lookup"><span data-stu-id="34dce-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="34dce-167">Você configurará uma relação de confiança RP para cada um dos dois ambientes do AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="34dce-168">Durante a depuração, as configurações do aplicativo em Web.config são usadas para fazer sua configuração de **Depuração** funcionar com o AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="34dce-169">Quando ele é publicado (por padrão, a configuração **Versão** é publicada), um Web.config transformado é carregado e incorpora as alterações de configuração do aplicativo em Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="34dce-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="34dce-170">Se você deseja anexar o aplicativo Web publicado no Azure ao depurador (ou seja, você deve carregar símbolos de depuração do seu código no aplicativo Web publicado), você pode criar um clone da configuração de depuração para depuração do Azure, mas com sua própria transformação de Web.config (por exemplo, Web.AzureDebug.config) personalizada que usa as configurações do aplicativo de Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="34dce-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="34dce-171">Isso permite que você mantenha uma configuração estática em diferentes ambientes.</span><span class="sxs-lookup"><span data-stu-id="34dce-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="34dce-172">Configurar a terceira parte confiável no gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="34dce-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="34dce-173">Agora você precisa configurar uma relação de confiança de RP no Gerenciamento do AD FS antes de poder usar seu aplicativo de exemplo realmente se autenticar no AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="34dce-174">Você precisará configurar duas relações de confiança RP separadas, uma para o seu ambiente de depuração e outra para seu aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="34dce-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="34dce-175">Repita as etapas abaixo para os dois ambientes.</span><span class="sxs-lookup"><span data-stu-id="34dce-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="34dce-176">No servidor do AD FS, faça logon com credenciais que tenham direitos de gerenciamento para o AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="34dce-177">Abra o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-177">Open AD FS Management.</span></span> <span data-ttu-id="34dce-178">Clique com o botão direito do mouse em **AD FS\Relacionamentos confiáveis\Objetos de confiança de terceira parte confiável** e selecione **Adicionar objeto de confiança de terceira parte confiável**.</span><span class="sxs-lookup"><span data-stu-id="34dce-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="34dce-179">Na página **Selecionar fonte de dados**, selecione **Inserir dados sobre a terceira parte confiável manualmente**.</span><span class="sxs-lookup"><span data-stu-id="34dce-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="34dce-180">Na página **Especificar nome de exibição**, digite um nome de exibição para o aplicativo e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="34dce-181">Na página **Escolher protocolo**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="34dce-182">Na página **Configurar certificado**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34dce-183">Como você já deve usar HTTPS, os tokens criptografados são opcionais.</span><span class="sxs-lookup"><span data-stu-id="34dce-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="34dce-184">Se você realmente deseja criptografar tokens do AD FS nesta página, você também deve adicionar lógica de descriptografia de token em seu código.</span><span class="sxs-lookup"><span data-stu-id="34dce-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="34dce-185">Para obter mais informações, consulte [Configuração manual de middleware OWIN WS-Federation e aceitação de tokens criptografados](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="34dce-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="34dce-186">Antes de passar para a próxima etapa, você precisa de uma informação do seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34dce-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="34dce-187">Nas propriedades do projeto, observe a **URL do SSL** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34dce-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="34dce-188">De volta no gerenciamento do AD FS, a página **Configurar URL** de **Adicionar assistente de objeto de confiança de terceira parte confiável**, selecione **Habilitar o suporte para o protocolo Web Services Federation Passive** e digite a URL do SSL do seu projeto do Visual Studio que você anotou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="34dce-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="34dce-189">Em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="34dce-190">A URL especifica para onde enviar o cliente após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="34dce-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="34dce-191">Para o ambiente de depuração, deve ser <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="34dce-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="34dce-192">Para o aplicativo Web publicado, deve ser a URL do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="34dce-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="34dce-193">Na página **Configurar identificadores**, verifique se o seu projeto de URL de SSL já está listado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="34dce-194">Clique em **Avançar** até o final do assistente com as seleções padrão.</span><span class="sxs-lookup"><span data-stu-id="34dce-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34dce-195">No App_Start\Startup.Auth.cs do projeto do Visual Studio, esse identificador é combinado ao valor de <code>WsFederationAuthenticationOptions.Wtrealm</code> durante a autenticação federada.</span><span class="sxs-lookup"><span data-stu-id="34dce-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="34dce-196">Por padrão, a URL do aplicativo da etapa anterior é adicionada como um identificador RP.</span><span class="sxs-lookup"><span data-stu-id="34dce-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="34dce-197">Agora você concluiu a configuração do aplicativo de RP para seu projeto no AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="34dce-198">Em seguida, configure esse aplicativo para enviar as declarações necessitadas para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34dce-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="34dce-199">A caixa de diálogo **Editar regras de declaração** é aberta por padrão para você no final do assistente para que você possa começar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="34dce-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="34dce-200">Vamos configurar pelo menos as seguintes declarações (com esquemas entre parênteses):</span><span class="sxs-lookup"><span data-stu-id="34dce-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="34dce-201">Nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) – utilizado pelo ASP.NET para hidratar `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="34dce-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="34dce-202">Nome UPN (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) – usado para identificar de forma exclusiva os usuários da organização.</span><span class="sxs-lookup"><span data-stu-id="34dce-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="34dce-203">Agrupar associações como funções (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) – pode ser usado com a decoração `[Authorize(Roles="role1, role2,...")]` para autorizar controladores/ações.</span><span class="sxs-lookup"><span data-stu-id="34dce-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="34dce-204">Na realidade, talvez essa abordagem não tenha o melhor desempenho para autorização de função.</span><span class="sxs-lookup"><span data-stu-id="34dce-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="34dce-205">Se os usuários do AD pertencerem a centenas de grupos de segurança, eles se tornarão centenas de declarações de função no token SAML.</span><span class="sxs-lookup"><span data-stu-id="34dce-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="34dce-206">Uma abordagem alternativa é enviar uma declaração de função única condicionalmente dependendo da participação do usuário em um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="34dce-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="34dce-207">No entanto, vamos manter isso simples para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="34dce-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="34dce-208">ID do nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) – pode ser usado para validação antifalsificação.</span><span class="sxs-lookup"><span data-stu-id="34dce-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="34dce-209">Para obter mais informações sobre como fazê-lo funcionar com a validação antifalsificação, consulte a seção **Adicionar funcionalidade de linha de negócios** de [Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="34dce-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="34dce-210">Os tipos de declaração que você precisa configurar para seu aplicativo são determinados pelas necessidades do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34dce-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="34dce-211">Para obter a lista de declarações com suporte por aplicativos do Active Directory do Azure (ou seja, relações de confiança RP), por exemplo, consulte [Token e tipos de declaração com suporte](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="34dce-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="34dce-212">Na caixa de diálogo Editar regras de declaração, clique em **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="34dce-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="34dce-213">Configure as declarações de nome, UPN e função, conforme mostra a captura de tela e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="34dce-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="34dce-214">Em seguida, crie uma declaração de ID de nome temporário usando as etapas demonstradas em [Identificadores de nome em asserções SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="34dce-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="34dce-215">Clique em **Adicionar regra** novamente.</span><span class="sxs-lookup"><span data-stu-id="34dce-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="34dce-216">Selecione **Enviar Declarações Usando uma Regra Personalizada** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="34dce-217">Cole o seguinte idioma da regra na caixa **Regra personalizada**, nomeie a regra **Por identificador de sessão** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="34dce-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="34dce-218">A regra personalizada deve parecer com esta captura de tela:</span><span class="sxs-lookup"><span data-stu-id="34dce-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="34dce-219">Clique em **Adicionar regra** novamente.</span><span class="sxs-lookup"><span data-stu-id="34dce-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="34dce-220">Selecione **Transformar uma declaração de entrada** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="34dce-221">Configure a regra conforme mostra a captura de tela (usando o tipo de declaração que você criou na regra personalizada) e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="34dce-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="34dce-222">Para obter informações detalhadas sobre as etapas para a declaração de ID de nome temporário, consulte [Identificadores de nome em asserções SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="34dce-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="34dce-223">Clique em **Aplicar** na caixa de diálogo **Editar regras de declaração**.</span><span class="sxs-lookup"><span data-stu-id="34dce-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="34dce-224">Agora deve se parecer com a captura de tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="34dce-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="34dce-225">Novamente, certifique-se de repetir essas etapas para seu ambiente de depuração e o aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="34dce-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="34dce-226">Teste a autenticação federada em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="34dce-226">Test federated authentication for your application</span></span>
<span data-ttu-id="34dce-227">Você está pronto para testar a lógica de autenticação do aplicativo com o AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="34dce-228">No meu ambiente de laboratório do AD FS, tenho um usuário de teste que pertence a um grupo de teste no Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="34dce-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="34dce-229">Para testar a autenticação no depurador, agora basta digitar `F5`.</span><span class="sxs-lookup"><span data-stu-id="34dce-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="34dce-230">Se você quiser testar a autenticação no aplicativo Web publicado, navegue até a URL.</span><span class="sxs-lookup"><span data-stu-id="34dce-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="34dce-231">Depois que o aplicativo Web for carregado, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="34dce-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="34dce-232">Você verá uma caixa de diálogo de logon ou a página de logon servidas por AD FS, dependendo do método de autenticação escolhido pelo AD FS.</span><span class="sxs-lookup"><span data-stu-id="34dce-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="34dce-233">Aqui está o que acontece no Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="34dce-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="34dce-234">Depois de fazer logon com um usuário no domínio do AD de implantação do AD FS, você deverá ver a página inicial novamente com **Olá, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="34dce-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="34dce-235">no canto.</span><span class="sxs-lookup"><span data-stu-id="34dce-235">in the corner.</span></span> <span data-ttu-id="34dce-236">Aqui está o que acontece.</span><span class="sxs-lookup"><span data-stu-id="34dce-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="34dce-237">Até agora, você já teve êxito das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="34dce-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="34dce-238">Seu aplicativo atingiu com êxito o AD FS e um identificador RP correspondente foi encontrado no banco de dados do AD FS</span><span class="sxs-lookup"><span data-stu-id="34dce-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="34dce-239">O AD FS foi autenticou com êxito um usuário do AD e redirecionou você de que volta à página inicial do aplicativo</span><span class="sxs-lookup"><span data-stu-id="34dce-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="34dce-240">O AD FS enviou com êxito a declaração de nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) ao seu aplicativo, conforme indicado pelo fato de que o nome de usuário é exibido no canto.</span><span class="sxs-lookup"><span data-stu-id="34dce-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="34dce-241">Se a declaração de nome estiver ausente, você teria visto **Olá, !**.</span><span class="sxs-lookup"><span data-stu-id="34dce-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="34dce-242">Se você observar Views\Shared\\_LoginPartial.cshtml, descobrirá que ele usa `User.Identity.Name` para exibir o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="34dce-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="34dce-243">Conforme mencionado anteriormente, se a declaração de nome do usuário autenticado estiver disponível no token SAML, o ASP.NET recuperará essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="34dce-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="34dce-244">Para ver todas as declarações enviadas pelo AD FS, coloque um ponto de interrupção em Controllers\HomeController.cs, no método de ação de Índice.</span><span class="sxs-lookup"><span data-stu-id="34dce-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="34dce-245">Depois que o usuário for autenticado, inspecione a coleção `System.Security.Claims.Current.Claims` .</span><span class="sxs-lookup"><span data-stu-id="34dce-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="34dce-246">Autorizar usuários para controladores específicos ou ações</span><span class="sxs-lookup"><span data-stu-id="34dce-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="34dce-247">Como incluiu associações de grupo como declarações de função em sua configuração de confiança RP, agora você pode usá-las diretamente na decoração `[Authorize(Roles="...")]` para controladores e ações.</span><span class="sxs-lookup"><span data-stu-id="34dce-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="34dce-248">Em um aplicativo de linha de negócios com o padrão Criar-Ler-Atualizar-Excluir (CRUD), é possível autorizar funções específicas para acessar cada ação.</span><span class="sxs-lookup"><span data-stu-id="34dce-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="34dce-249">Por enquanto, você simplesmente testará esse recurso no controlador Início existente.</span><span class="sxs-lookup"><span data-stu-id="34dce-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="34dce-250">Abra Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="34dce-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="34dce-251">Decore os métodos de ação `About` e `Contact` e similares ao código abaixo, usando as associações de grupo de segurança que seu usuário autenticado tem.</span><span class="sxs-lookup"><span data-stu-id="34dce-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="34dce-252">Como adicionei **Usuário de Teste** ao **Grupo de Teste** em meu ambiente de laboratório do AD FS, usarei o Grupo de Teste para testar a autorização em `About`.</span><span class="sxs-lookup"><span data-stu-id="34dce-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="34dce-253">Para `Contact`, testarei o caso negativo de **Admins. do domínio**, ao qual o **Usuário de Teste** não pertence.</span><span class="sxs-lookup"><span data-stu-id="34dce-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="34dce-254">Inicie o depurador digitando `F5` , entre e, depois, clique em **Sobre**.</span><span class="sxs-lookup"><span data-stu-id="34dce-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="34dce-255">Você deverá ver agora a página `~/About/Index` com êxito, se o usuário autenticado for autorizado para essa ação.</span><span class="sxs-lookup"><span data-stu-id="34dce-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="34dce-256">Agora clique em **Contato**, que, em meu caso, não deve autorizar **Usuário de Teste** para a ação.</span><span class="sxs-lookup"><span data-stu-id="34dce-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="34dce-257">No entanto, o navegador é redirecionado para o AD FS, que, por fim, mostra esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="34dce-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="34dce-258">Se examinar esse erro no Visualizador de eventos no servidor do AD FS, você verá esta mensagem de exceção:</span><span class="sxs-lookup"><span data-stu-id="34dce-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="34dce-259">O motivo desse erro é que, por padrão, o MVC retorna um 401 Não autorizado quando uma função do usuário não está autorizada.</span><span class="sxs-lookup"><span data-stu-id="34dce-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="34dce-260">Isso dispara uma solicitação de nova tentativa de autenticação para seu provedor de identidade (AD FS).</span><span class="sxs-lookup"><span data-stu-id="34dce-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="34dce-261">Uma vez que o usuário já está autenticado, o AD FS retorna para a mesma página, o que, em seguida, emite outro 401, criando um loop de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="34dce-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="34dce-262">Você substituirá o método `HandleUnauthorizedRequest` de AuthorizeAttribute por lógica simples para mostrar algo que faça sentido, em vez de dar continuidade ao loop de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="34dce-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="34dce-263">Crie um arquivo no projeto chamado AuthorizeAttribute.cs e cole o código a seguir nele.</span><span class="sxs-lookup"><span data-stu-id="34dce-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="34dce-264">O código de substituição envia um HTTP 403 (Proibido) em vez de HTTP 401 (Não autorizado) em casos do tipo autenticado mas não autorizado.</span><span class="sxs-lookup"><span data-stu-id="34dce-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="34dce-265">Execute o depurador novamente com `F5`.</span><span class="sxs-lookup"><span data-stu-id="34dce-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="34dce-266">Clicar em **Contato** agora mostra uma mensagem de erro mais informativa (embora não atraente):</span><span class="sxs-lookup"><span data-stu-id="34dce-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="34dce-267">Publique o aplicativo nos Aplicativos Web do Serviço de Aplicativo do Azure novamente e teste o comportamento do aplicativo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="34dce-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="34dce-268">Conectar-se a dados locais</span><span class="sxs-lookup"><span data-stu-id="34dce-268">Connect to on-premises data</span></span>
<span data-ttu-id="34dce-269">Um motivo pelo qual você desejaria implementar seu aplicativo de linha de negócios com o AD FS, em vez de Active Directory do Azure, são os problemas de conformidade em manter dados organizacionais fora do local.</span><span class="sxs-lookup"><span data-stu-id="34dce-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="34dce-270">Isso também pode significar que o seu aplicativo Web no Azure deve acessar bancos de dados locais, pois você não tem permissão para usar o [Banco de Dados SQL](/services/sql-database/) como a camada de dados para seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="34dce-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="34dce-271">Os Aplicativos Web do Serviço de Aplicativo do Azure dão suporte ao acesso a bancos de dados locais com duas abordagens: [Conexões Híbridas](../biztalk-services/integration-hybrid-connection-overview.md) e [Redes Virtuais](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="34dce-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="34dce-272">Para obter mais informações, consulte [Usando integração de VNET e conexões híbridas com Aplicativos Web do Serviço de Aplicativo do Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="34dce-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="34dce-273">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="34dce-273">Further resources</span></span>
* [<span data-ttu-id="34dce-274">Autenticar com o Active Directory local em seu aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="34dce-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="34dce-275">Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34dce-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="34dce-276">Usar a opção de autenticação organizacional local (ADFS) com ASP.NET no Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="34dce-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="34dce-277">Migrar um projeto Web VS2013 do WIF para Katana</span><span class="sxs-lookup"><span data-stu-id="34dce-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="34dce-278">Visão geral dos Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="34dce-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="34dce-279">Especificação do WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="34dce-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

