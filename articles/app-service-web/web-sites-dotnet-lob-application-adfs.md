---
title: "aaaCreate um aplicativo de linha de negócios do Azure com autenticação do AD FS | Microsoft Docs"
description: "Saiba como toocreate um aplicativo de linha de negócios no serviço de aplicativo do Azure que se autentica com local STS. Este tutorial destina-se como Olá STS locais do AD FS."
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
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="95cec-104">Criar um aplicativo de linha de negócios do Azure com autenticação do AD FS</span><span class="sxs-lookup"><span data-stu-id="95cec-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="95cec-105">Este artigo mostra como aplicativo toocreate uma ASP.NET MVC linha de negócios em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) usando um local [os serviços de Federação do Active Directory](http://technet.microsoft.com/library/hh831502.aspx) como provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="95cec-106">Este cenário poderá funcionar quando você deseja que os aplicativos de linha de negócios toocreate no serviço de aplicativo do Azure, mas sua organização exigir toobe de dados do diretório armazenada no local.</span><span class="sxs-lookup"><span data-stu-id="95cec-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="95cec-107">Para obter uma visão geral das opções de autenticação e autorização de empresa diferente de saudação do serviço de aplicativo do Azure, consulte [autenticar com o Active Directory local em seu aplicativo do Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="95cec-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="95cec-108">O que você compilará</span><span class="sxs-lookup"><span data-stu-id="95cec-108">What you will build</span></span>
<span data-ttu-id="95cec-109">Você criará um aplicativo básico ASP.NET em aplicativos de Web do serviço de aplicativo do Azure com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="95cec-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="95cec-110">Autentica usuários no AD FS</span><span class="sxs-lookup"><span data-stu-id="95cec-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="95cec-111">Usa `[Authorize]` tooauthorize usuários para ações diferentes</span><span class="sxs-lookup"><span data-stu-id="95cec-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="95cec-112">Configuração estática para depuração no Visual Studio e publicar aplicativos Web do serviço de tooApp (configura uma vez, depurar e publicar a qualquer momento)</span><span class="sxs-lookup"><span data-stu-id="95cec-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="95cec-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="95cec-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="95cec-114">Você precisa Olá toocomplete a seguir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="95cec-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="95cec-115">Um local em implantação do AD FS (para uma explicação de ponta a ponta do laboratório de teste Olá usado neste tutorial, consulte [laboratório de teste: STS autônomo com o AD FS na VM do Azure (para teste)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="95cec-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="95cec-116">Relações de confiança de terceira parte confiável toocreate permissões no gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="95cec-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="95cec-117">Visual Studio 2013 Atualização 4 ou posterior</span><span class="sxs-lookup"><span data-stu-id="95cec-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="95cec-118">[SDK do Azure 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou posterior</span><span class="sxs-lookup"><span data-stu-id="95cec-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="95cec-119">Usar o aplicativo de exemplo para modelo de linha de negócios</span><span class="sxs-lookup"><span data-stu-id="95cec-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="95cec-120">Olá o aplicativo de exemplo neste tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), é criado pela equipe do Active Directory do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="95cec-121">Como o AD FS oferece suporte para WS-Federation, você pode usar isso como um aplicativo de linha de negócios do modelo toocreate com facilidade.</span><span class="sxs-lookup"><span data-stu-id="95cec-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="95cec-122">Ele tem Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="95cec-122">It has hello following features:</span></span>

* <span data-ttu-id="95cec-123">Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate com um local em implantação do AD FS</span><span class="sxs-lookup"><span data-stu-id="95cec-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="95cec-124">Funcionalidade de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="95cec-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="95cec-125">Usa [pt](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (em vez do Windows Identity Foundation), que é Olá futuras do ASP.NET e muito mais simples tooset para autenticação e autorização que o WIF</span><span class="sxs-lookup"><span data-stu-id="95cec-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="95cec-126">Configurar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="95cec-126">Set up hello sample application</span></span>
1. <span data-ttu-id="95cec-127">Clonar ou baixar a solução de exemplo hello em [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour diretório de local.</span><span class="sxs-lookup"><span data-stu-id="95cec-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95cec-128">Olá instruções em [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) mostram como tooset o aplicativo hello com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="95cec-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="95cec-129">Mas, neste tutorial, você configurá-lo com o AD FS, portanto, siga etapas Olá aqui em vez disso.</span><span class="sxs-lookup"><span data-stu-id="95cec-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="95cec-130">Abrir solução hello e abra Controllers\AccountController.cs em Olá **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="95cec-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="95cec-131">Você verá que o código de saudação simplesmente emite um usuário de saudação autenticação desafio tooauthenticate usando o WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="95cec-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="95cec-132">Todas as autenticações são configuradas em App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="95cec-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="95cec-133">Abra App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="95cec-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="95cec-134">Em Olá `ConfigureAuth` método, a linha de saudação de Observação:</span><span class="sxs-lookup"><span data-stu-id="95cec-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="95cec-135">Em Olá, mundo OWIN, este trecho de código é realmente Olá bare que mínimo necessário para autenticação de WS-Federation tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="95cec-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="95cec-136">É muito mais simples e mais elegante de WIF, em que o Web. config é injetado com XML em todos os lugares hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="95cec-137">Olá apenas informações que você precisa são Olá da terceira parte confiável (RP) identificador e hello URL do arquivo de metadados do serviço do AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="95cec-138">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="95cec-138">Here's an example:</span></span>
   
   * <span data-ttu-id="95cec-139">Identificador RP: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="95cec-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="95cec-140">Endereço de metadados: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="95cec-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="95cec-141">No App_Start\Startup.Auth.cs, altere Olá definições de cadeia de caracteres estática a seguir:</span><span class="sxs-lookup"><span data-stu-id="95cec-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="95cec-142">Agora, fazer as alterações correspondentes de saudação em Web. config. Abra Olá Web. config e modifique Olá configurações do aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="95cec-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="95cec-143">Preencha os valores de chave Olá com base em seu respectivo ambiente.</span><span class="sxs-lookup"><span data-stu-id="95cec-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="95cec-144">Olá aplicativo toomake-se de que não existem erros de compilação.</span><span class="sxs-lookup"><span data-stu-id="95cec-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="95cec-145">É isso.</span><span class="sxs-lookup"><span data-stu-id="95cec-145">That's it.</span></span> <span data-ttu-id="95cec-146">Agora o aplicativo de exemplo hello está pronto toowork com o AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="95cec-147">Você ainda precisa tooconfigure uma relação de confiança com este aplicativo no AD FS RP.</span><span class="sxs-lookup"><span data-stu-id="95cec-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="95cec-148">Implantar tooAzure de aplicativo de exemplo hello aplicativos de Web do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="95cec-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="95cec-149">Aqui, você publica Olá aplicativo tooa web app no aplicativo de serviço Web aplicativos enquanto preserva o ambiente de depuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="95cec-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="95cec-150">Observe que você vai aplicativo hello de toopublish antes que ele tem uma relação de confiança com o AD FS, RP para que autenticação ainda não funciona ainda.</span><span class="sxs-lookup"><span data-stu-id="95cec-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="95cec-151">No entanto, se você fazê-lo agora você pode ter Olá URL do aplicativo web que você pode usar mais tarde tooconfigure Olá RP relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="95cec-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="95cec-152">Clique duas vezes com o botão direito em seu projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="95cec-153">Clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="95cec-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="95cec-154">Se você ainda não tiver entrado no tooAzure, clique em **entrar** e usar a conta da Microsoft hello para toosign sua assinatura do Azure no.</span><span class="sxs-lookup"><span data-stu-id="95cec-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="95cec-155">Depois de conectado, clique em **novo** toocreate um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="95cec-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="95cec-156">Preencha todos os campos obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="95cec-156">Fill in all required fields.</span></span> <span data-ttu-id="95cec-157">Posteriormente, que serão os dados de local tooon tooconnect para não criar um banco de dados para este aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="95cec-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="95cec-158">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-158">Click **Create**.</span></span> <span data-ttu-id="95cec-159">Depois de criar aplicativo de web hello, de diálogo Publicar Web hello é aberto.</span><span class="sxs-lookup"><span data-stu-id="95cec-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="95cec-160">Em **URL de destino**, alterar **http** muito**https**.</span><span class="sxs-lookup"><span data-stu-id="95cec-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="95cec-161">Copie Olá todo URL tooa editor de texto para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="95cec-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="95cec-162">Em seguida, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="95cec-163">No Visual Studio, abra **Web.Release.config** em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="95cec-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="95cec-164">Inserir saudação XML a seguir em Olá `<configuration>` marca e substitua o valor da chave Olá com URL de publicação do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="95cec-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="95cec-165">Quando terminar, você tem dois identificadores RP configurados no seu projeto, um para o seu ambiente de depuração no Visual Studio, e um para Olá publicado o aplicativo web no Azure.</span><span class="sxs-lookup"><span data-stu-id="95cec-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="95cec-166">Você configurará uma relação de confiança RP para cada um dos dois ambientes de saudação do AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="95cec-167">Durante a depuração, configurações do aplicativo hello em Web. config são usada toomake seu **depurar** do trabalho de configuração com o AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="95cec-168">Quando ele é publicado (por padrão, Olá **versão** configuração é publicada), um Web. config transformados é carregado que incorpora as alterações de configuração de aplicativo hello em Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="95cec-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="95cec-169">Se você quiser tooattach Olá web publicados aplicativo no depurador de toohello do Azure (ou seja, você deve carregar símbolos de depuração do seu código no aplicativo de web publicados Olá), você pode criar um clone de saudação depurar a configuração de depuração do Azure, mas com seu próprio Web. config personalizado transformar ( Por exemplo, Web.AzureDebug.config) que usa configurações de aplicativo de saudação do Web.Release.config. Isso permite que você toomaintain estático entre ambientes diferentes hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="95cec-170">Configurar a terceira parte confiável no gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="95cec-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="95cec-171">Agora, é necessário tooconfigure uma relação de confiança RP no gerenciamento do AD FS antes de usar o aplicativo de exemplo e, na verdade, autenticar com o AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="95cec-172">Você precisará tooset backup duas relações de confiança RP separadas, uma para o seu ambiente de depuração e outra para seu aplicativo web publicado.</span><span class="sxs-lookup"><span data-stu-id="95cec-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="95cec-173">Certifique-se de que você repita Olá seguindo as etapas para ambos os ambientes.</span><span class="sxs-lookup"><span data-stu-id="95cec-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="95cec-174">No servidor do AD FS, faça logon com credenciais que tenham direitos de gerenciamento tooAD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="95cec-175">Abra o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-175">Open AD FS Management.</span></span> <span data-ttu-id="95cec-176">Clique com o botão direito do mouse em **AD FS\Relacionamentos confiáveis\Objetos de confiança de terceira parte confiável** e selecione **Adicionar objeto de confiança de terceira parte confiável**.</span><span class="sxs-lookup"><span data-stu-id="95cec-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="95cec-177">Em Olá **Selecionar fonte de dados** , selecione **inserir manualmente dados sobre a terceira parte confiável Olá**.</span><span class="sxs-lookup"><span data-stu-id="95cec-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="95cec-178">Em Olá **especificar nome de exibição** página, digite um nome para exibição para o aplicativo hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95cec-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="95cec-179">Em Olá **escolha protocolo** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95cec-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="95cec-180">Em Olá **configurar certificado** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95cec-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95cec-181">Como você já deve usar HTTPS, os tokens criptografados são opcionais.</span><span class="sxs-lookup"><span data-stu-id="95cec-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="95cec-182">Se você realmente deseja tooencrypt tokens do AD FS nesta página, você também deve adicionar lógica de descriptografia de token em seu código.</span><span class="sxs-lookup"><span data-stu-id="95cec-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="95cec-183">Para obter mais informações, consulte [Configuração manual de middleware OWIN WS-Federation e aceitação de tokens criptografados](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="95cec-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="95cec-184">Antes de passar para a próxima etapa do hello, é necessário um pedaço de informações do seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95cec-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="95cec-185">Nas propriedades do projeto hello, observe Olá **SSL URL** do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="95cec-186">Em gerenciamento do AD FS, em Olá **configurar URL** página de saudação **terceira parte confiável Assistente para adicionar confiança**, selecione **habilitar o suporte para o protocolo WS-Federation Passive do hello** e digite hello URL de SSL de seu projeto do Visual Studio que você anotou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="95cec-187">Em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="95cec-188">URL especifica onde o cliente de saudação toosend após a autenticação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="95cec-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="95cec-189">Para o ambiente de depuração hello, ele deve ser <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="95cec-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="95cec-190">Para o aplicativo de web publicados hello, deve ser URL do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="95cec-191">Em Olá **configurar identificadores** página, verifique se que seu projeto SSL URL já está listado e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95cec-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="95cec-192">Clique em **próximo** todos Olá final de toohello de maneira do Assistente de saudação com as seleções padrão.</span><span class="sxs-lookup"><span data-stu-id="95cec-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95cec-193">No App_Start\Startup.Auth.cs do projeto do Visual Studio, esse identificador é comparado com o valor de saudação do <code>WsFederationAuthenticationOptions.Wtrealm</code> durante a autenticação federada.</span><span class="sxs-lookup"><span data-stu-id="95cec-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="95cec-194">Por padrão, a URL do aplicativo hello da etapa anterior Olá é adicionado como um identificador RP.</span><span class="sxs-lookup"><span data-stu-id="95cec-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="95cec-195">Agora terminar de configurar Olá aplicativo RP para seu projeto no AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="95cec-196">Em seguida, configure toosend esse aplicativo hello declarações necessitadas para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95cec-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="95cec-197">Olá **editar regras de declaração** caixa de diálogo é aberta por padrão para você no final de saudação do Assistente de saudação para que você possa começar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="95cec-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="95cec-198">Vamos configurar pelo menos Olá seguintes declarações (com esquemas entre parênteses):</span><span class="sxs-lookup"><span data-stu-id="95cec-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="95cec-199">Nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - usado por ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="95cec-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="95cec-200">Usuário nome principal (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - usado toouniquely identificar os usuários na organização hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="95cec-201">Associações de grupo, como funções (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - pode ser usado com `[Authorize(Roles="role1, role2,...")]` decoração tooauthorize controladores/ações.</span><span class="sxs-lookup"><span data-stu-id="95cec-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="95cec-202">Na verdade, essa abordagem pode não ser Olá para autorização de função de melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="95cec-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="95cec-203">Se os usuários do AD pertencem toohundreds dos grupos de segurança, eles se tornam centenas de declarações de função no token SAML hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="95cec-204">Uma abordagem alternativa é toosend uma única função de declaração condicionalmente dependendo da associação do usuário Olá em um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="95cec-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="95cec-205">No entanto, vamos manter isso simples para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="95cec-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="95cec-206">ID do nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) – pode ser usado para validação antifalsificação.</span><span class="sxs-lookup"><span data-stu-id="95cec-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="95cec-207">Para obter mais informações sobre como toomake que ele funciona com a validação de antifalsificação, consulte Olá **adiciona a funcionalidade de linha de negócios** seção [criar um aplicativo de linha de negócios do Azure com a autenticação do Active Directory do Azure ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="95cec-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="95cec-208">Olá declaração tipos você precisará tooconfigure para seu aplicativo depende das necessidades do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95cec-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="95cec-209">Para obter lista de saudação de declarações suportado por aplicativos do Active Directory do Azure (ou seja, relações de confiança RP), por exemplo, consulte [tipos de declaração e Token com suporte](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="95cec-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="95cec-210">Na caixa de diálogo Olá editar regras de declaração, clique em **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="95cec-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="95cec-211">Configurar as declarações de nome UPN e função hello conforme mostrado na captura de tela de saudação e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="95cec-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="95cec-212">Em seguida, crie um nome transitório de declaração de ID usando etapas Olá demonstrado no [identificadores de nome em declarações SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="95cec-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="95cec-213">Clique em **Adicionar regra** novamente.</span><span class="sxs-lookup"><span data-stu-id="95cec-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="95cec-214">Selecione **Enviar Declarações Usando uma Regra Personalizada** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="95cec-215">Idioma de regra a seguir Olá colar em Olá **regra personalizada** caixa, uma regra de saudação do nome **por identificador de sessão** e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="95cec-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="95cec-216">A regra personalizada deve parecer com esta captura de tela:</span><span class="sxs-lookup"><span data-stu-id="95cec-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="95cec-217">Clique em **Adicionar regra** novamente.</span><span class="sxs-lookup"><span data-stu-id="95cec-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="95cec-218">Selecione **Transformar uma declaração de entrada** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="95cec-219">Configurar regra de hello, conforme mostrado na captura de tela de saudação (usando o tipo de declaração Olá criado na regra personalizada de saudação) e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="95cec-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="95cec-220">Para obter informações detalhadas sobre as etapas de saudação para declaração de ID de nome temporária hello, consulte [identificadores de nome em declarações SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="95cec-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="95cec-221">Clique em **aplicar** em Olá **editar regras de declaração** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95cec-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="95cec-222">Agora, ele deve ser como Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="95cec-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="95cec-223">Novamente, certifique-se de repetir essas etapas para seu ambiente de depuração e o aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="95cec-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="95cec-224">Teste a autenticação federada em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="95cec-224">Test federated authentication for your application</span></span>
<span data-ttu-id="95cec-225">Você está pronto tootest lógica de autenticação do aplicativo no AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="95cec-226">Em meu ambiente de laboratório do AD FS, tenho um usuário de teste que pertence o grupo de teste tooa no Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="95cec-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="95cec-227">autenticação tootest no depurador Olá, tudo o que você precisa toodo agora é o tipo `F5`.</span><span class="sxs-lookup"><span data-stu-id="95cec-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="95cec-228">Se você deseja que a autenticação de tootest no aplicativo de web publicados Olá, navegue toohello URL.</span><span class="sxs-lookup"><span data-stu-id="95cec-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="95cec-229">Depois que o aplicativo da web hello carrega, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="95cec-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="95cec-230">Agora, você deve obter ou uma caixa de diálogo ou Olá logon página de logon servida pelo AD FS, dependendo do método de autenticação de saudação escolhido pelo AD FS.</span><span class="sxs-lookup"><span data-stu-id="95cec-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="95cec-231">Aqui está o que acontece no Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="95cec-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="95cec-232">Depois de fazer logon com um usuário no domínio de AD de saudação da implantação do hello AD FS, você verá agora homepage Olá novamente com **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="95cec-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="95cec-233">no canto hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-233">in hello corner.</span></span> <span data-ttu-id="95cec-234">Aqui está o que acontece.</span><span class="sxs-lookup"><span data-stu-id="95cec-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="95cec-235">Até agora, você já teve êxito ao Olá maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="95cec-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="95cec-236">Seu aplicativo atingiu com êxito do AD FS e um identificador RP correspondente foi encontrado no hello banco de dados do AD FS</span><span class="sxs-lookup"><span data-stu-id="95cec-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="95cec-237">O AD FS foi autenticado com êxito um usuário do AD e fazer home page do aplicativo toohello de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="95cec-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="95cec-238">O AD FS como nome de saudação enviada com êxito de declaração (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour aplicativo, conforme indicado pelo fato de saudação usuário Olá nome é exibido no canto hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="95cec-239">Se a declaração de nome hello estiver ausente, você teria visto **Hello,!**.</span><span class="sxs-lookup"><span data-stu-id="95cec-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="95cec-240">Se você observar exibições \ compartilhadas\_LoginPartial.cshtml, você achar que ele usa `User.Identity.Name` toodisplay nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="95cec-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="95cec-241">Conforme mencionado anteriormente, se nome hello de declaração de saudação autenticada usuário está disponível no token SAML hello, ASP.NET hydrates essa propriedade com ele.</span><span class="sxs-lookup"><span data-stu-id="95cec-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="95cec-242">toosee que Olá por todas as declarações que são enviadas pelo AD FS, colocar um ponto de interrupção em Controllers\HomeController.cs, Olá método de ação do índice.</span><span class="sxs-lookup"><span data-stu-id="95cec-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="95cec-243">Depois Olá usuário é autenticado, inspecionar Olá `System.Security.Claims.Current.Claims` coleção.</span><span class="sxs-lookup"><span data-stu-id="95cec-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="95cec-244">Autorizar usuários para controladores específicos ou ações</span><span class="sxs-lookup"><span data-stu-id="95cec-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="95cec-245">Desde que você incluiu associações de grupo como declarações de função em sua configuração de confiança RP, agora você pode usá-los diretamente no hello `[Authorize(Roles="...")]` decoração de controladores e ações.</span><span class="sxs-lookup"><span data-stu-id="95cec-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="95cec-246">Em um aplicativo de linha de negócios com padrão de criar-leitura-atualização-exclusão (CRUD) hello, você pode autorizar funções específicas tooaccess cada ação.</span><span class="sxs-lookup"><span data-stu-id="95cec-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="95cec-247">Por enquanto, você será apenas experimentar esse recurso no controlador Home existente de saudação.</span><span class="sxs-lookup"><span data-stu-id="95cec-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="95cec-248">Abra Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="95cec-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="95cec-249">Decore Olá `About` e `Contact` ação métodos semelhantes toohello código a seguir, o uso de associações de grupo de segurança do usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="95cec-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="95cec-250">Como eu adicionei **usuário de teste** muito**grupo de teste** em meu ambiente de laboratório do AD FS, vou usar autorização do grupo de teste tootest em `About`.</span><span class="sxs-lookup"><span data-stu-id="95cec-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="95cec-251">Para `Contact`, vai testar caso negativo de saudação do **Admins. do domínio**, toowhich **testar usuário** não pertence.</span><span class="sxs-lookup"><span data-stu-id="95cec-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="95cec-252">Iniciar o depurador Olá digitando `F5` entrar e clique em **sobre**.</span><span class="sxs-lookup"><span data-stu-id="95cec-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="95cec-253">Você deve agora estar visualizando Olá `~/About/Index` página com êxito, se o usuário autenticado é autorizado para aquela ação.</span><span class="sxs-lookup"><span data-stu-id="95cec-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="95cec-254">Agora clique **entre em contato com**, que, em meu caso não deve autorizar **usuário de teste** para ação hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="95cec-255">No entanto, o navegador de saudação é redirecionado tooAD FS, que eventualmente mostra esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="95cec-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="95cec-256">Se você examinar este erro no Visualizador de eventos em saudação do servidor AD FS, você vir essa mensagem de exceção:</span><span class="sxs-lookup"><span data-stu-id="95cec-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="95cec-257">motivo Olá para esse erro é que por padrão, MVC retorna um 401 não autorizado quando uma função do usuário não está autorizada.</span><span class="sxs-lookup"><span data-stu-id="95cec-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="95cec-258">Isso dispara um provedor de identidade reautenticação solicitação tooyour (AD FS).</span><span class="sxs-lookup"><span data-stu-id="95cec-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="95cec-259">Como o usuário Olá já está autenticado, o AD FS retorna toohello mesma página, que, em seguida, emite outro 401, criando um loop de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="95cec-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="95cec-260">Ignorará do AuthorizeAttribute `HandleUnauthorizedRequest` método com lógica simples tooshow algo que faça sentido em vez de loop de redirecionamento Olá continuando.</span><span class="sxs-lookup"><span data-stu-id="95cec-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="95cec-261">Crie um arquivo no projeto Olá chamado AuthorizeAttribute.cs e colar Olá código a seguir para ele.</span><span class="sxs-lookup"><span data-stu-id="95cec-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
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
   
    <span data-ttu-id="95cec-262">Olá substituir envia código um HTTP 403 (proibido) em vez de HTTP 401 (não autorizado) nos casos autenticados, mas não autorizados.</span><span class="sxs-lookup"><span data-stu-id="95cec-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="95cec-263">Executar o depurador Olá novamente com `F5`.</span><span class="sxs-lookup"><span data-stu-id="95cec-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="95cec-264">Clicar em **Contato** agora mostra uma mensagem de erro mais informativa (embora não atraente):</span><span class="sxs-lookup"><span data-stu-id="95cec-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="95cec-265">Publicar novamente o hello aplicativo tooAzure aplicativos de Web do serviço de aplicativo e testar o comportamento de saudação do aplicativo ao vivo hello.</span><span class="sxs-lookup"><span data-stu-id="95cec-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="95cec-266">Conecte-se a dados locais tooon</span><span class="sxs-lookup"><span data-stu-id="95cec-266">Connect tooon-premises data</span></span>
<span data-ttu-id="95cec-267">Um motivo que você esperaria tooimplement seu aplicativo de linha de negócios com o AD FS, em vez de Active Directory do Azure é problemas de conformidade com a manter a organização dados fora do local.</span><span class="sxs-lookup"><span data-stu-id="95cec-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="95cec-268">Isso também pode significar que o seu aplicativo web no Azure deve acessar bancos de dados local, desde que você não tem permissão toouse [banco de dados SQL](/services/sql-database/) como camada de dados Olá para seus aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="95cec-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="95cec-269">Os Aplicativos Web do Serviço de Aplicativo do Azure dão suporte ao acesso a bancos de dados locais com duas abordagens: [Conexões Híbridas](../biztalk-services/integration-hybrid-connection-overview.md) e [Redes Virtuais](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="95cec-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="95cec-270">Para obter mais informações, consulte [Usando integração de VNET e conexões híbridas com Aplicativos Web do Serviço de Aplicativo do Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="95cec-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="95cec-271">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="95cec-271">Further resources</span></span>
* [<span data-ttu-id="95cec-272">Autenticar com o Active Directory local em seu aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="95cec-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="95cec-273">Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95cec-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="95cec-274">Use Olá opção de autenticação organizacional local (ADFS) com ASP.NET no Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="95cec-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="95cec-275">Migrar um tooKatana VS2013 projeto da Web do WIF</span><span class="sxs-lookup"><span data-stu-id="95cec-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="95cec-276">Visão geral dos Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="95cec-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="95cec-277">Especificação do WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="95cec-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

