---
title: "aplicativo de web móvel aaaDeploy um ASP.NET MVC 5 no serviço de aplicativo do Azure"
description: "Um tutorial que ensina como toodeploy uma tooAzure de aplicativo web do serviço de aplicativo móvel usando o recursos no ASP.NET MVC 5 aplicativo da web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="f55c4-103">Implantar um aplicativo Web móvel ASP.NET MVC 5 no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f55c4-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="f55c4-104">Este tutorial irá ensiná-Olá Noções básicas de como toobuild um ASP.NET MVC 5 web aplicativo amigáveis para dispositivos móveis e implantá-lo tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="f55c4-105">Para este tutorial, você precisa [Visual Studio Express 2013 para Web] [ Visual Studio Express 2013] ou a edição professional saudação do Visual Studio se ele já está instalado.</span><span class="sxs-lookup"><span data-stu-id="f55c4-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="f55c4-106">Você pode usar [Visual Studio 2015] mas capturas de tela de saudação serão diferentes e você deve usar modelos do hello ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="f55c4-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="f55c4-107">O que você vai construir</span><span class="sxs-lookup"><span data-stu-id="f55c4-107">What You'll Build</span></span>
<span data-ttu-id="f55c4-108">Para este tutorial, você adicionará recursos móveis toohello listagem de conferência aplicativo simples que é fornecido no hello [projeto inicial][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="f55c4-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="f55c4-109">Olá seguinte captura de tela mostra Olá ASP.NET sessões no aplicativo hello concluída, como visto no emulador de navegador Olá nas ferramentas de desenvolvedor F12 do Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="f55c4-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="f55c4-110">Você pode usar ferramentas de desenvolvedor Olá F12 do Internet Explorer 11 e hello [ferramenta Fiddler] [ Fiddler] toohelp depurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="f55c4-111">Qualificações que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f55c4-111">Skills You'll Learn</span></span>
<span data-ttu-id="f55c4-112">Eis o que você vai aprender:</span><span class="sxs-lookup"><span data-stu-id="f55c4-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="f55c4-113">Como toopublish toouse Visual Studio 2013 seu aplicativo web diretamente tooa de aplicativo web no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f55c4-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="f55c4-114">Como modelos Olá ASP.NET MVC 5 usam o framework de inicialização de CSS Olá para melhorar a exibição em dispositivos móveis</span><span class="sxs-lookup"><span data-stu-id="f55c4-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="f55c4-115">Como toocreate específicas para dispositivos móveis exibições tootarget específico navegadores de dispositivos móveis, como iPhone hello e Android</span><span class="sxs-lookup"><span data-stu-id="f55c4-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="f55c4-116">Como toocreate responsivo exibições (exibições que respondem toodifferent navegadores em todos os dispositivos)</span><span class="sxs-lookup"><span data-stu-id="f55c4-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="f55c4-117">Configurar o ambiente de desenvolvimento Olá</span><span class="sxs-lookup"><span data-stu-id="f55c4-117">Set up hello development environment</span></span>
<span data-ttu-id="f55c4-118">Configurar seu ambiente de desenvolvimento, instalando hello Azure SDK para .NET 2.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f55c4-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="f55c4-119">Olá tooinstall SDK do Azure para .NET, clique o link de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="f55c4-120">Se você não tiver o Visual Studio 2013 instalado, ele será instalado por um link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="f55c4-121">Este tutorial requer o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f55c4-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="f55c4-122">[SDK do Azure para o Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="f55c4-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="f55c4-123">Na janela do Web Platform Installer hello, clique em **instalar** e prosseguir com a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="f55c4-124">Também será necessário um emulador do navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="f55c4-125">Qualquer um dos seguintes Olá funcionará:</span><span class="sxs-lookup"><span data-stu-id="f55c4-125">Any of hello following will work:</span></span>

* <span data-ttu-id="f55c4-126">Emulador do navegador nas [ferramentas de desenvolvedor do Internet Explorer 11 F12][EmulatorIE11] (usado em todas as capturas de tela do navegador móvel).</span><span class="sxs-lookup"><span data-stu-id="f55c4-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="f55c4-127">Ele possui predefinições de cadeia de caracteres de agente de usuário para Windows Phone 8, Windows Phone 7 e Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="f55c4-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="f55c4-128">Emulador de navegador nas [DevTools do Google Chrome][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="f55c4-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="f55c4-129">Contém predefinições para vários dispositivos Android, e também para Apple iPhone, Apple iPad e Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="f55c4-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="f55c4-130">Ele também emula eventos de toque.</span><span class="sxs-lookup"><span data-stu-id="f55c4-130">It also emulates touch events.</span></span>
* <span data-ttu-id="f55c4-131">[Emulador do Opera para dispositivos móveis][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="f55c4-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="f55c4-132">Projetos do Visual Studio com C\# código-fonte é tooaccompany disponível neste tópico:</span><span class="sxs-lookup"><span data-stu-id="f55c4-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="f55c4-133">[Download do projeto inicial][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="f55c4-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="f55c4-134">[Download do projeto concluído][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="f55c4-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="f55c4-135"><a name="bkmk_DeployStarterProject"></a>Implantar o aplicativo de web do Azure do hello starter projeto tooan</span><span class="sxs-lookup"><span data-stu-id="f55c4-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="f55c4-136">Baixe o aplicativo de listagem de conferência hello [projeto inicial][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="f55c4-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="f55c4-137">Em seguida, no Windows Explorer, clique no arquivo ZIP de saudação baixado e escolha *propriedades*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="f55c4-138">Em Olá **propriedades** caixa de diálogo caixa, escolha Olá **desbloquear** botão.</span><span class="sxs-lookup"><span data-stu-id="f55c4-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="f55c4-139">(Desbloqueio impede que um aviso de segurança que ocorre quando você tenta toouse um *. zip* arquivo que você baixou da web hello.)</span><span class="sxs-lookup"><span data-stu-id="f55c4-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="f55c4-140">Arquivo ZIP de saudação e selecione **extrair tudo** para descompactar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="f55c4-141">No Visual Studio, abra Olá *C#\Mvc5Mobile.sln* arquivo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="f55c4-142">No Gerenciador de soluções, clique com botão direito hello e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="f55c4-143">Em Publicar Web, clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="f55c4-144">Se você ainda não tiver feito logon no Azure, clique em **Adicionar uma conta**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="f55c4-145">Siga Olá prompts toolog em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f55c4-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="f55c4-146">Olá caixa de diálogo serviço de aplicativo agora deve mostrar como conectado.</span><span class="sxs-lookup"><span data-stu-id="f55c4-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="f55c4-147">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="f55c4-148">Em Olá **nome do aplicativo Web** , especifique um prefixo de nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="f55c4-149">O nome totalmente qualificado do aplicativo Web será *&lt;prefixo>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="f55c4-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="f55c4-150">Além disso, especifique um novo nome de grupo de recursos em **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="f55c4-151">Em seguida, clique em **novo** toocreate um novo plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="f55c4-152">Configurar o novo plano de serviço de aplicativo hello e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="f55c4-153">Novamente na caixa de diálogo de criação de serviço de aplicativo hello, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="f55c4-154">Depois hello recursos do Azure são criados, de diálogo Publicar Web hello será preenchido com as configurações de saudação para seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="f55c4-155">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="f55c4-156">Depois que o Visual Studio termina publicação Olá starter projeto toohello web do Azure aplicativo, o navegador de área de trabalho Olá abre toodisplay Olá web dinâmico aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="f55c4-157">Iniciar o emulador do navegador de dispositivo móvel, copie Olá URL para o aplicativo de conferência hello (*<prefix>*. azurewebsites.net) no emulador do Windows hello e, em seguida, clique no botão superior direito e selecione **procurar por marca**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="f55c4-158">Se você estiver usando o Internet Explorer 11 como navegador padrão de saudação, basta tootype `F12`, em seguida, `Ctrl+8`e alterar o perfil de navegador Olá muito**do Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="f55c4-159">A imagem abaixo mostra Olá *AllTags* exibição no modo retrato (escolha **procurar por marca**).</span><span class="sxs-lookup"><span data-stu-id="f55c4-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="f55c4-160">Enquanto você pode depurar seu aplicativo MVC 5 de dentro do Visual Studio, você pode publicar seu tooAzure de aplicativo da web novamente tooverify Olá ao vivo aplicativo web diretamente do seu navegador móvel ou um emulador de navegador.</span><span class="sxs-lookup"><span data-stu-id="f55c4-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="f55c4-161">exibição de saudação é muito legível em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="f55c4-162">Você também já pode ver alguns dos efeitos visuais de saudação aplicados pela estrutura de inicialização CSS hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="f55c4-163">Clique em Olá **ASP.NET** link.</span><span class="sxs-lookup"><span data-stu-id="f55c4-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="f55c4-164">Olá modo de exibição ASP.NET é ajustado zoom toohello tela, que Bootstrap faz para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f55c4-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="f55c4-165">No entanto, você pode melhorar essa exibição toobetter naipe Olá navegador de dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="f55c4-166">Por exemplo, Olá **data** coluna é difícil de ler.</span><span class="sxs-lookup"><span data-stu-id="f55c4-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="f55c4-167">Posteriormente no tutorial hello, você alterará Olá *AllTags* exibir toomake-amigáveis para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f55c4-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="f55c4-168"><a name="bkmk_bootstrap"></a> Framework de CSS Bootstrap</span><span class="sxs-lookup"><span data-stu-id="f55c4-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="f55c4-169">A novidade no hello MVC 5 modelo é suporte interno a inicialização.</span><span class="sxs-lookup"><span data-stu-id="f55c4-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="f55c4-170">Você já viu como ele melhora imediatamente Olá modos de exibição em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="f55c4-171">Por exemplo, barra de navegação de saudação na parte superior da saudação é recolhível automaticamente quando a largura do navegador de saudação for menor.</span><span class="sxs-lookup"><span data-stu-id="f55c4-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="f55c4-172">No navegador de área de trabalho hello, tente redimensionar a janela do navegador hello e ver como a barra de navegação Olá altera sua aparência.</span><span class="sxs-lookup"><span data-stu-id="f55c4-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="f55c4-173">Este é o design de web responsivo Olá que é criado na inicialização.</span><span class="sxs-lookup"><span data-stu-id="f55c4-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="f55c4-174">toosee como aplicativo da Web de saudação seria sem inicialização, abra *aplicativo\_iniciar\\BundleConfig.cs* e comente as linhas de saudação que contenham *bootstrap.js* e *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="f55c4-175">Olá código a seguir mostra Olá duas últimas instruções de saudação `RegisterBundles` método após alteração hello:</span><span class="sxs-lookup"><span data-stu-id="f55c4-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="f55c4-176">Pressione `Ctrl+F5` aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="f55c4-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="f55c4-177">Observe a que barra de navegação recolhível que Olá agora é apenas uma lista não ordenada comum.</span><span class="sxs-lookup"><span data-stu-id="f55c4-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="f55c4-178">Clique em **Procurar por marcação** novamente e clique em **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="f55c4-179">No modo de exibição de emulador móvel hello, você pode ver agora que já não é ajustado para zoom toohello tela e você deve rolar lateralmente na ordem toosee, Olá direita da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="f55c4-180">Desfaça as alterações e atualizar Olá navegador móvel tooverify que a exibição de dispositivos móveis Olá foi restaurada.</span><span class="sxs-lookup"><span data-stu-id="f55c4-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="f55c4-181">Inicialização não é específico tooASP.NET MVC 5, e você pode tirar proveito desses recursos em um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f55c4-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="f55c4-182">Ele é, porém, um recurso interno do modelo de projeto MVC 5 do ASP.NET, de forma que o seu aplicativo Web MVC 5 pode, por padrão, aproveitar o Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f55c4-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="f55c4-183">Para obter mais informações sobre inicialização, vá toothe [Bootstrap] [ BootstrapSite] site.</span><span class="sxs-lookup"><span data-stu-id="f55c4-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="f55c4-184">Na próxima seção, Olá você verá como modos de exibição específicos tooprovide navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="f55c4-185"><a name="bkmk_overrideviews"></a>Substituição de modos de exibição de hello, Layouts e exibições parciais</span><span class="sxs-lookup"><span data-stu-id="f55c4-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="f55c4-186">Você pode substituir qualquer modo de exibição (inclusive layouts e modos de exibição parciais) para navegadores de dispositivos móveis em geral, para um navegador móvel individual ou para qualquer navegador específico.</span><span class="sxs-lookup"><span data-stu-id="f55c4-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="f55c4-187">Exibir do tooprovide uma específicas para dispositivos móveis, você pode copiar um arquivo de exibição e adicionar *. Mobile* toohello nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="f55c4-188">Por exemplo, toocreate móveis *índice* exibição, você pode copiar *exibições\\início\\cshtml* para *modos de exibição\\início\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="f55c4-189">Nesta seção, você criará um arquivo de layout específico para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f55c4-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="f55c4-190">toostart, cópia *exibições\\compartilhado\\\_cshtml* para *exibições\\compartilhado\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="f55c4-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="f55c4-191">Abra  *\_Layout.Mobile.cshtml* e altere o título de saudação do **MVC5 aplicativo** muito**MVC5 aplicativo (móvel)**.</span><span class="sxs-lookup"><span data-stu-id="f55c4-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="f55c4-192">Em cada `Html.ActionLink` chamada para a barra de navegação hello, remova "Procurar por" em cada link *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="f55c4-193">Olá, código a seguir mostra Olá concluída `<ul class="nav navbar-nav">` marca de arquivo de layout para dispositivos móveis hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="f55c4-194">Saudação de cópia *exibições\\início\\AllTags.cshtml* o arquivo para *exibições\\início\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="f55c4-195">Abra o novo arquivo de saudação e altere o `<h2>` elemento de "Tags" muito "marcas (M)":</span><span class="sxs-lookup"><span data-stu-id="f55c4-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="f55c4-196">Procure toohello marcas página usando um navegador da área de trabalho e usar o emulador do navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="f55c4-197">emulador de navegador móvel Olá mostra Olá duas alterações feitas (Olá título de  *\_Layout.Mobile.cshtml* e título de saudação do *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f55c4-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="f55c4-198">Por outro lado, exibição de área de trabalho Olá não foi alterada (com títulos de  *\_cshtml* e *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f55c4-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="f55c4-199"><a name="bkmk_browserviews"></a> Criar modos de exibição para um navegador específico</span><span class="sxs-lookup"><span data-stu-id="f55c4-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="f55c4-200">Além disso toomobile-área de trabalho específicas e exibições, você pode criar modos de exibição para um navegador individual.</span><span class="sxs-lookup"><span data-stu-id="f55c4-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="f55c4-201">Por exemplo, você pode criar exibições que são específicas para iPhone hello ou navegador do Android hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="f55c4-202">Nesta seção, você criará um layout para o navegador do iPhone hello e uma versão de iPhone do hello *AllTags* exibição.</span><span class="sxs-lookup"><span data-stu-id="f55c4-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="f55c4-203">Olá abrir *global. asax* de arquivos e adicionar Olá inferior toohello código a seguir o `Application_Start` método.</span><span class="sxs-lookup"><span data-stu-id="f55c4-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="f55c4-204">Este código define um novo modo de exibição denominado “iPhone”, que será comparado a todas as solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="f55c4-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="f55c4-205">Se a solicitação de entrada hello corresponder a condição definida (ou seja, se o agente do usuário Olá contém a cadeia de caracteres do hello "iPhone"), o ASP.NET MVC procurará exibições cujo nome contém o sufixo "iPhone".</span><span class="sxs-lookup"><span data-stu-id="f55c4-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="f55c4-206">Quando adicionar específicos de navegador móvel modos de exibição, como para iPhone e Android, ser se tooset Olá primeiro argumento muito`0` (inserir na parte superior de saudação da lista de saudação) toomake-se de que o modo de navegador específico Olá tem precedência sobre o modelo móveis Olá (*. Cshtml).</span><span class="sxs-lookup"><span data-stu-id="f55c4-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="f55c4-207">Se o modelo móveis hello está na parte superior de saudação da lista de saudação em vez disso, ele será selecionado em seu modo de exibição desejado (Olá primeiro wins de correspondência e modelo móveis Olá corresponde a todos os navegadores móveis).</span><span class="sxs-lookup"><span data-stu-id="f55c4-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="f55c4-208">No código de saudação, clique com botão direito `DefaultDisplayMode`, escolha **resolver**e, em seguida, escolha `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="f55c4-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="f55c4-209">Isso adiciona uma referência toothe `System.Web.WebPages` namespace, que é o local onde o `DisplayModeProvider` e `DefaultDisplayMode` tipos são definidos.</span><span class="sxs-lookup"><span data-stu-id="f55c4-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="f55c4-210">Como alternativa, você pode adicionar apenas manualmente Olá toothe linha a seguir `using` seção do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="f55c4-211">Salve alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-211">Save hello changes.</span></span> <span data-ttu-id="f55c4-212">Copie o arquivo *Views\\Shared\\\_Layout.Mobile.cshtml* para *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="f55c4-213">Abra o novo arquivo de saudação e, em seguida, altere o título de saudação do `MVC5 Application (Mobile)` para `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="f55c4-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="f55c4-214">Saudação de cópia *exibições\\início\\AllTags.Mobile.cshtml* o arquivo para *exibições\\início\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="f55c4-215">No novo arquivo de saudação, alterar Olá `<h2>` elemento de "marcas (M)" muito "marcas (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="f55c4-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="f55c4-216">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-216">Run hello application.</span></span> <span data-ttu-id="f55c4-217">Executar um emulador navegador móvel, verifique se o agente do usuário está definido muito "iPhone" e procurar toohello *AllTags* exibição.</span><span class="sxs-lookup"><span data-stu-id="f55c4-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="f55c4-218">Se você estiver usando o emulador Olá nas ferramentas de desenvolvedor F12 do Internet Explorer 11, configure a seguir toohello emulação:</span><span class="sxs-lookup"><span data-stu-id="f55c4-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="f55c4-219">Perfil do navegador = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="f55c4-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="f55c4-220">Cadeia de caracteres de agente do usuário = **Personalizado**</span><span class="sxs-lookup"><span data-stu-id="f55c4-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="f55c4-221">Cadeia de caracteres personalizada = **Apple-iPhone5C1/1001,525**</span><span class="sxs-lookup"><span data-stu-id="f55c4-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="f55c4-222">Olá, seguinte captura de tela mostra Olá *AllTags* exibição renderizada no emulador do Windows em ferramentas de desenvolvedor F12 do Internet Explorer 11 com a cadeia de caracteres de agente de usuário personalizada hello (Esta é uma cadeia de caracteres de agente de usuário do iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="f55c4-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="f55c4-223">No navegador de dispositivo móvel hello, selecione Olá **alto-falantes** link.</span><span class="sxs-lookup"><span data-stu-id="f55c4-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="f55c4-224">Porque não há uma exibição móvel (*AllSpeakers.Mobile.cshtml*), exibir alto-falantes do saudação padrão (*AllSpeakers.cshtml*) é processado usando o modo de exibição de layout para dispositivos móveis hello ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f55c4-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="f55c4-225">Conforme mostrado abaixo, título Olá **MVC5 aplicativo (móvel)** é definido em  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="f55c4-226">Globalmente você pode desabilitar o modo de exibição padrão (não móveis) da renderização dentro de um layout para dispositivos móveis, definindo `RequireConsistentDisplayMode` para `true` em Olá *exibições\\\_ViewStart.cshtml* arquivo, como este:</span><span class="sxs-lookup"><span data-stu-id="f55c4-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="f55c4-227">Quando `RequireConsistentDisplayMode` está definido muito`true`, layout móveis hello (*\_Layout.Mobile.cshtml*) é usado apenas para exibições móveis (ou seja, quando o arquivo de exibição é do formulário Olá  ***ViewName** . Cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f55c4-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="f55c4-228">Talvez você queira tooset `RequireConsistentDisplayMode` muito`true` se o layout para dispositivos móveis não funcionar bem com seus modos de exibição não móveis.</span><span class="sxs-lookup"><span data-stu-id="f55c4-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="f55c4-229">Olá captura de tela abaixo mostra como Olá *alto-falantes* page renderiza quando `RequireConsistentDisplayMode` está definido muito`true` (sem Olá cadeia de caracteres "(móvel)" em Olá navegação barra na parte superior da saudação).</span><span class="sxs-lookup"><span data-stu-id="f55c4-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="f55c4-230">Você pode desabilitar o modo de exibição consistente em um modo específico, definindo `RequireConsistentDisplayMode` muito`false` no arquivo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="f55c4-231">A seguinte marcação em Olá *exibições\\início\\AllSpeakers.cshtml* conjuntos de arquivos `RequireConsistentDisplayMode` muito`false`:</span><span class="sxs-lookup"><span data-stu-id="f55c4-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="f55c4-232">Esta seção que vimos como toocreate móveis layouts e modos de exibição e como toocreate layouts e modos de exibição para dispositivos específicos, como Olá iPhone.</span><span class="sxs-lookup"><span data-stu-id="f55c4-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="f55c4-233">No entanto, Olá principal vantagem do framework de inicialização CSS Olá é o layout dinâmico, o que significa que uma única folha de estilos pode ser aplicada de área de trabalho, telefone e tablet navegadores toocreate uma aparência consistente.</span><span class="sxs-lookup"><span data-stu-id="f55c4-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="f55c4-234">Na próxima seção, Olá você verá como tooleverage inicializar amigáveis para dispositivos móveis toocreate modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="f55c4-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="f55c4-235"><a name="bkmk_Improvespeakerslist"></a>Melhorar Olá alto-falantes lista</span><span class="sxs-lookup"><span data-stu-id="f55c4-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="f55c4-236">Como você acabou de ver, Olá *alto-falantes* modo de exibição pode ser lido, mas Olá links são pequenos e tootap difícil em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="f55c4-237">Nesta seção, você fará Olá *AllSpeakers* exibição amigáveis para dispositivos móveis, que exibe links grande, fácil de toque e contém um tooquickly da caixa de pesquisa localizar alto-falantes.</span><span class="sxs-lookup"><span data-stu-id="f55c4-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="f55c4-238">Você pode usar o hello Bootstrap [grupo de lista vinculada] [ linked list group] estilo para melhorar a saudação *alto-falantes* exibição.</span><span class="sxs-lookup"><span data-stu-id="f55c4-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="f55c4-239">Em *exibições\\início\\AllSpeakers.cshtml*, substitua o conteúdo de saudação do arquivo de Razor de saudação com código de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="f55c4-240">Olá `class="list-group"` atributo Olá `<div>` marca aplica o estilo de lista de inicialização e hello `class="input-group-item"` atributo aplica-se o link de tooeach de estilo de item de lista de inicialização.</span><span class="sxs-lookup"><span data-stu-id="f55c4-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="f55c4-241">Atualize o navegador móvel hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="f55c4-242">Olá atualizado exibição esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f55c4-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="f55c4-243">Olá Bootstrap [grupo de lista vinculada] [ linked list group] estilo torna Olá caixa inteira para cada link clicável, que é uma experiência de usuário muito melhor.</span><span class="sxs-lookup"><span data-stu-id="f55c4-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="f55c4-244">Alternar exibição da área de trabalho toothe e observar Olá aparência consistente.</span><span class="sxs-lookup"><span data-stu-id="f55c4-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="f55c4-245">Embora o modo de exibição de navegador móvel Olá melhorou, é difícil navegar longa lista Olá de alto-falantes.</span><span class="sxs-lookup"><span data-stu-id="f55c4-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="f55c4-246">O Bootstrap não oferece uma funcionalidade de filtro de pesquisa pronta para uso, mas você pode adicionar uma utilizando poucas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="f55c4-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="f55c4-247">Você primeiro adiciona uma exibição de toohello da caixa de pesquisa e a ligar com hello código JavaScript para a função de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="f55c4-248">Em *exibições\\início\\AllSpeakers.cshtml*, adicionar um \<formulário\> marca logo após Olá \<h2\> marca, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="f55c4-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="f55c4-249">Observe que Olá `<form>` e `<input>` marcas ambos têm Olá Bootstrap estilos aplicados toothem.</span><span class="sxs-lookup"><span data-stu-id="f55c4-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="f55c4-250">Olá `<span>` elemento adiciona uma inicialização [glyphicon] [ glyphicon] toothe caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f55c4-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="f55c4-251">Em Olá *Scripts* pasta, adicione um arquivo JavaScript chamado *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="f55c4-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="f55c4-252">Abra o arquivo hello e cole Olá código a seguir para ele:</span><span class="sxs-lookup"><span data-stu-id="f55c4-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="f55c4-253">Você também precisa tooinclude filter.js em seus pacotes registrados.</span><span class="sxs-lookup"><span data-stu-id="f55c4-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="f55c4-254">Abra *aplicativo\_iniciar\\BundleConfig.cs* e alterar pacotes de saudação primeiro.</span><span class="sxs-lookup"><span data-stu-id="f55c4-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="f55c4-255">Alterar o primeiro `bundles.Add` instrução (para Olá **jquery** pacote) tooinclude *Scripts\\filter.js*, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f55c4-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="f55c4-256">Olá **jquery** pacote já é renderizado por padrão Olá  *\_Layout* exibição.</span><span class="sxs-lookup"><span data-stu-id="f55c4-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="f55c4-257">Posteriormente, você pode utilizar Olá JavaScript mesmo código tooapply os modos de exibição de lista do filtro funcionalidade tooother.</span><span class="sxs-lookup"><span data-stu-id="f55c4-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="f55c4-258">Atualize o navegador móvel hello e vá toohello *AllSpeakers* exibição.</span><span class="sxs-lookup"><span data-stu-id="f55c4-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="f55c4-259">Na caixa de pesquisa, digite “sc”.</span><span class="sxs-lookup"><span data-stu-id="f55c4-259">In the search box, type "sc".</span></span> <span data-ttu-id="f55c4-260">lista de alto-falantes Olá agora deve ser filtrada acordo com a cadeia de caracteres de pesquisa tooyour.</span><span class="sxs-lookup"><span data-stu-id="f55c4-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="f55c4-261"><a name="bkmk_improvetags"></a>Melhorar Olá lista de marcas</span><span class="sxs-lookup"><span data-stu-id="f55c4-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="f55c4-262">Como Olá *alto-falantes* exibir, hello *marcas* modo de exibição pode ser lido, mas Olá links são pequeno e de difícil tootap em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="f55c4-263">Você pode corrigir Olá *marcas* exibição Olá mesmo maneira corrigir Olá *alto-falantes* exibir, se você usar as alterações de código Olá descritas anteriormente, mas com os seguintes Olá `Html.ActionLink` sintaxe de método em  *Modos de exibição\\início\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f55c4-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="f55c4-264">Olá atualizados parece navegador de área de trabalho da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f55c4-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="f55c4-265">E Olá atualizado navegador móvel parece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f55c4-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="f55c4-266">Se você notar que formatação da lista original Olá ainda está em Olá navegador móvel e o estilo de inicialização adequado com tooyour esteja se perguntando, este é um artefato da sua anteriores ação toocreate móvel exibições específicas.</span><span class="sxs-lookup"><span data-stu-id="f55c4-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="f55c4-267">No entanto, agora que você estiver usando Olá Bootstrap CSS framework toocreate um design responsivo web, vá head e remover essas exibições específicas para dispositivos móveis e modos de exibição de layout específicas para dispositivos móveis hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="f55c4-268">Depois de você ter feito isso, navegador de dispositivo móvel atualizado Olá mostrará estilo Bootstrap hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="f55c4-269"><a name="bkmk_improvedates"></a>Melhorar Olá lista de datas</span><span class="sxs-lookup"><span data-stu-id="f55c4-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="f55c4-270">Você pode melhorar Olá *datas* exibir como aprimorado Olá *alto-falantes* e *marcas* exibições se você usar alterações de código de saudação descritas anteriormente, mas com hello após `Html.ActionLink` sintaxe de método em *exibições\\início\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f55c4-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="f55c4-271">A exibição atualizada do navegador móvel será como esta:</span><span class="sxs-lookup"><span data-stu-id="f55c4-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="f55c4-272">Você pode melhorar ainda mais o hello *datas* exibição, organizando os valores de data e hora Olá por data.</span><span class="sxs-lookup"><span data-stu-id="f55c4-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="f55c4-273">Isso pode ser feito com hello Bootstrap [painéis] [ panels] de estilo.</span><span class="sxs-lookup"><span data-stu-id="f55c4-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="f55c4-274">Substitua o conteúdo de saudação do hello *exibições\\início\\AllDates.cshtml* arquivo com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55c4-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="f55c4-275">Esse código cria um separado `<div class="panel panel-primary">` marca para cada data distinta na lista de Olá e usa Olá [grupo de lista vinculada] [ linked list group] para os respectivos links como antes.</span><span class="sxs-lookup"><span data-stu-id="f55c4-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="f55c4-276">Aqui está o navegador móvel Olá aparência quando esse código é executado:</span><span class="sxs-lookup"><span data-stu-id="f55c4-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="f55c4-277">Opção toohello área de trabalho no navegador.</span><span class="sxs-lookup"><span data-stu-id="f55c4-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="f55c4-278">Novamente, observe a aparência consistente hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="f55c4-279"><a name="bkmk_improvesessionstable"></a>Melhorar Olá SessionsTable exibição</span><span class="sxs-lookup"><span data-stu-id="f55c4-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="f55c4-280">Nesta seção, você fará Olá *SessionsTable* exibir mais amigáveis para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f55c4-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="f55c4-281">Essa alteração é alterações anteriores de hello mais ampla.</span><span class="sxs-lookup"><span data-stu-id="f55c4-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="f55c4-282">No navegador de dispositivo móvel hello, toque em Olá **marca** botão e, em seguida, digite `asp` na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f55c4-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="f55c4-283">Toque em Olá **ASP.NET** link.</span><span class="sxs-lookup"><span data-stu-id="f55c4-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="f55c4-284">Como você pode ver, a exibição de saudação é formatada como uma tabela, que é atualmente projetado toobe exibido no navegador de área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55c4-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="f55c4-285">No entanto, é um pouco difícil tooread em um navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f55c4-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="f55c4-286">toofix isso, abra *exibições\\início\\SessionsTable.cshtml* e, em seguida, substitua conteúdo de saudação do arquivo hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55c4-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="f55c4-287">código de saudação faz 3:</span><span class="sxs-lookup"><span data-stu-id="f55c4-287">hello code does 3 things:</span></span>

* <span data-ttu-id="f55c4-288">usa Olá Bootstrap [grupo personalizado de lista vinculada] [ custom linked list group] tooformat Olá informações de sessão verticalmente, para que todas essas informações pode ser lidas em um navegador móvel (usando classes como lista de grupo-item-texto)</span><span class="sxs-lookup"><span data-stu-id="f55c4-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="f55c4-289">aplica-se a saudação [sistema grade] [ grid system] toothe layout, portanto essa sessão Olá itens fluxo horizontalmente no navegador de área de trabalho hello e verticalmente no navegador de dispositivo móvel hello (usando a classe do hello col-md-4)</span><span class="sxs-lookup"><span data-stu-id="f55c4-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="f55c4-290">Olá usa [utilitários responsivos] [ responsive utilities] para ocultar marcas de sessão hello quando exibido no navegador de dispositivo móvel hello (usando a classe de xs oculto de saudação)</span><span class="sxs-lookup"><span data-stu-id="f55c4-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="f55c4-291">Você também pode tocar uma título toogo toohello respectivos a sessão de link.</span><span class="sxs-lookup"><span data-stu-id="f55c4-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="f55c4-292">imagem de saudação abaixo reflete as alterações de código hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="f55c4-293">sistema de inicialização grade Olá aplicadas automaticamente Organiza as sessões verticalmente no navegador móvel hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="f55c4-294">Além disso, observe que as marcas de saudação não são mostradas.</span><span class="sxs-lookup"><span data-stu-id="f55c4-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="f55c4-295">Opção toohello área de trabalho no navegador.</span><span class="sxs-lookup"><span data-stu-id="f55c4-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="f55c4-296">No navegador de área de trabalho Olá, observe que as marcas de saudação agora são exibidas.</span><span class="sxs-lookup"><span data-stu-id="f55c4-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="f55c4-297">Além disso, você pode ver que sistema de inicialização grade Olá que você aplicou organiza os itens de sessão de saudação em duas colunas.</span><span class="sxs-lookup"><span data-stu-id="f55c4-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="f55c4-298">Se você aumentar o navegador, você verá que organização Olá muda toothree colunas.</span><span class="sxs-lookup"><span data-stu-id="f55c4-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="f55c4-299"><a name="bkmk_improvesessionbycode"></a>Melhorar Olá SessionByCode exibição</span><span class="sxs-lookup"><span data-stu-id="f55c4-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="f55c4-300">Por fim, você corrigirá Olá *SessionByCode* exibir toomake-amigáveis para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f55c4-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="f55c4-301">No navegador de dispositivo móvel hello, toque em Olá **marca** botão e, em seguida, digite `asp` na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f55c4-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="f55c4-302">Toque em Olá **ASP.NET** link.</span><span class="sxs-lookup"><span data-stu-id="f55c4-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="f55c4-303">As sessões de marca ASP.NET hello serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="f55c4-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="f55c4-304">Escolha Olá **criando um aplicativo de página única com ASP.NET e AngularJS** link.</span><span class="sxs-lookup"><span data-stu-id="f55c4-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="f55c4-305">modo de exibição da área de trabalho saudação padrão é bom, mas você pode melhorar a aparência de saudação facilmente usando alguns componentes de GUI de inicialização.</span><span class="sxs-lookup"><span data-stu-id="f55c4-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="f55c4-306">Abra *exibições\\início\\SessionByCode.cshtml* e substitua o conteúdo de saudação com hello marcação a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55c4-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="f55c4-307">nova marcação de saudação usa Bootstrap painéis definindo o estilo de modo de exibição móvel tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="f55c4-308">Atualize o navegador móvel hello.</span><span class="sxs-lookup"><span data-stu-id="f55c4-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="f55c4-309">Olá imagem a seguir reflete as alterações de código de saudação que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="f55c4-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="f55c4-310">Conclusão e revisão</span><span class="sxs-lookup"><span data-stu-id="f55c4-310">Wrap Up and Review</span></span>
<span data-ttu-id="f55c4-311">Este tutorial mostrou como aplicativos de Web toouse ASP.NET MVC 5 toodevelop amigáveis para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f55c4-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="f55c4-312">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="f55c4-312">These include:</span></span>

* <span data-ttu-id="f55c4-313">Implantar um aplicativo de ASP.NET MVC 5 tooan aplicativo do serviço de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="f55c4-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="f55c4-314">Use layout de web responsivo toocreate de inicialização em seu aplicativo MVC 5</span><span class="sxs-lookup"><span data-stu-id="f55c4-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="f55c4-315">Substituir layouts, modos de exibição e exibições parciais globalmente ou para um modo de exibição individual</span><span class="sxs-lookup"><span data-stu-id="f55c4-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="f55c4-316">Controlar a imposição de layout e de substituição parcial usando a propriedade `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="f55c4-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="f55c4-317">Criar exibições que navegadores específicos, como o navegador do iPhone Olá de destino</span><span class="sxs-lookup"><span data-stu-id="f55c4-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="f55c4-318">Aplicar estilos do Bootstrap no código Razor</span><span class="sxs-lookup"><span data-stu-id="f55c4-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="f55c4-319">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f55c4-319">See Also</span></span>
* [<span data-ttu-id="f55c4-320">9 princípios básicos do design da Web responsivo</span><span class="sxs-lookup"><span data-stu-id="f55c4-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="f55c4-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="f55c4-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="f55c4-322">[Blog oficial do Bootstrap][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="f55c4-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="f55c4-323">[Tutorial do Bootstrap no Twitter, feito pela Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="f55c4-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="f55c4-324">[Olá parque de inicialização][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="f55c4-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="f55c4-325">[Práticas recomendadas pelo W3C para Aplicativos Web Móveis][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="f55c4-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="f55c4-326">[Recomendação Candidata do W3C para consultas de mídia][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="f55c4-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f55c4-327">O que mudou</span><span class="sxs-lookup"><span data-stu-id="f55c4-327">What's changed</span></span>
* <span data-ttu-id="f55c4-328">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f55c4-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

