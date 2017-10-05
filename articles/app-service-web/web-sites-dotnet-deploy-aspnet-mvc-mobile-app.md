---
title: "Implantar um aplicativo Web móvel ASP.NET MVC 5 no Serviço de Aplicativo do Azure"
description: "Um tutorial que ensina como implantar um aplicativo Web no Serviço de Aplicativo do Azure usando recursos móveis no aplicativo Web ASP.NET MVC 5."
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
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="f449e-103">Implantar um aplicativo Web móvel ASP.NET MVC 5 no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f449e-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="f449e-104">Este tutorial ensinará você o básico sobre como compilar um aplicativo Web do ASP.NET MVC 5 adaptado para dispositivos móveis e implantá-lo no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f449e-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="f449e-105">Para este tutorial, você precisa do [Visual Studio Express 2013 para Web][Visual Studio Express 2013] ou do Visual Studio Professional Edition, se já o tiver.</span><span class="sxs-lookup"><span data-stu-id="f449e-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="f449e-106">Você pode usar o [Visual Studio 2015], mas as capturas de tela serão diferentes e você deverá usar os modelos do ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="f449e-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="f449e-107">O que você vai construir</span><span class="sxs-lookup"><span data-stu-id="f449e-107">What You'll Build</span></span>
<span data-ttu-id="f449e-108">Neste tutorial, você adicionará recursos móveis ao aplicativo de listagem de conferência simples que é fornecido no [projeto inicial][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="f449e-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="f449e-109">A captura de tela a seguir mostra as sessões do ASP.NET no aplicativo concluído, como visto no emulador do navegador nas ferramentas de desenvolvedor do Internet Explorer 11 F12.</span><span class="sxs-lookup"><span data-stu-id="f449e-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="f449e-110">É possível utilizar as ferramentas de desenvolvedor do Internet Explorer 11 F12 e a [ferramenta Fiddler][Fiddler] para ajudar a depurar o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="f449e-111">Qualificações que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f449e-111">Skills You'll Learn</span></span>
<span data-ttu-id="f449e-112">Eis o que você vai aprender:</span><span class="sxs-lookup"><span data-stu-id="f449e-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="f449e-113">Como usar o Visual Studio 2013 para publicar seu aplicativo Web diretamente em um aplicativo Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f449e-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="f449e-114">Como os modelos do ASP.NET MVC 5 utilizam o framework de CSS Bootstrap para melhorar a exibição em dispositivos móveis</span><span class="sxs-lookup"><span data-stu-id="f449e-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="f449e-115">Como criar modos de exibição para dispositivos móveis voltados para navegadores de dispositivos móveis específicos, tais como iPhone e Android</span><span class="sxs-lookup"><span data-stu-id="f449e-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="f449e-116">Como criar modos de exibição dinâmicos (que respondam a navegadores diferentes em todos os dispositivos)</span><span class="sxs-lookup"><span data-stu-id="f449e-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="f449e-117">Configurar o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="f449e-117">Set up the development environment</span></span>
<span data-ttu-id="f449e-118">Configure o ambiente de desenvolvimento instalando o SDK do Azure para .NET 2.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f449e-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="f449e-119">Para instalar o SDK do Azure para .NET, clique no link abaixo.</span><span class="sxs-lookup"><span data-stu-id="f449e-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="f449e-120">Se você ainda não tiver o Visual Studio 2013 instalado, ele será instalado pelo link.</span><span class="sxs-lookup"><span data-stu-id="f449e-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="f449e-121">Este tutorial requer o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f449e-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="f449e-122">[SDK do Azure para o Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="f449e-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="f449e-123">Na janela do Web Platform Installer, clique em **Instalar** e prossiga com a instalação.</span><span class="sxs-lookup"><span data-stu-id="f449e-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="f449e-124">Também será necessário um emulador do navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="f449e-125">Qualquer uma das opções a seguir funcionará:</span><span class="sxs-lookup"><span data-stu-id="f449e-125">Any of the following will work:</span></span>

* <span data-ttu-id="f449e-126">Emulador do navegador nas [ferramentas de desenvolvedor do Internet Explorer 11 F12][EmulatorIE11] (usado em todas as capturas de tela do navegador móvel).</span><span class="sxs-lookup"><span data-stu-id="f449e-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="f449e-127">Ele possui predefinições de cadeia de caracteres de agente de usuário para Windows Phone 8, Windows Phone 7 e Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="f449e-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="f449e-128">Emulador de navegador nas [DevTools do Google Chrome][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="f449e-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="f449e-129">Contém predefinições para vários dispositivos Android, e também para Apple iPhone, Apple iPad e Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="f449e-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="f449e-130">Ele também emula eventos de toque.</span><span class="sxs-lookup"><span data-stu-id="f449e-130">It also emulates touch events.</span></span>
* <span data-ttu-id="f449e-131">[Emulador do Opera para dispositivos móveis][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="f449e-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="f449e-132">Os projetos do Visual Studio com o código-fonte em C\# estão disponíveis para acompanhar este tópico:</span><span class="sxs-lookup"><span data-stu-id="f449e-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="f449e-133">[Download do projeto inicial][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="f449e-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="f449e-134">[Download do projeto concluído][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="f449e-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="f449e-135"><a name="bkmk_DeployStarterProject"></a>Implantar o projeto inicial em um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="f449e-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="f449e-136">Baixe o [projeto inicial][StarterProject] do aplicativo de listagem de conferência.</span><span class="sxs-lookup"><span data-stu-id="f449e-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="f449e-137">Em seguida, no Windows Explorer, clique com o botão direito do mouse no arquivo ZIP baixado e escolha *Propriedades*.</span><span class="sxs-lookup"><span data-stu-id="f449e-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="f449e-138">Na caixa de diálogo **Propriedades**, escolha o botão **Desbloquear**.</span><span class="sxs-lookup"><span data-stu-id="f449e-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="f449e-139">(Desbloquear impede um aviso de segurança que ocorre quando você tenta usar um arquivo *.zip* que você baixou da Web).</span><span class="sxs-lookup"><span data-stu-id="f449e-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="f449e-140">Clique com o botão direito do mouse no arquivo ZIP e selecione **Extrair tudo** para descompactar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="f449e-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="f449e-141">No Visual Studio, abra o arquivo *C#\Mvc5Mobile.sln*.</span><span class="sxs-lookup"><span data-stu-id="f449e-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="f449e-142">No Gerenciador de Soluções, clique com o botão direito no projeto e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f449e-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="f449e-143">Em Publicar Web, clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f449e-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="f449e-144">Se você ainda não tiver feito logon no Azure, clique em **Adicionar uma conta**.</span><span class="sxs-lookup"><span data-stu-id="f449e-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="f449e-145">Siga os prompts para fazer logon na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f449e-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="f449e-146">A caixa de diálogo serviço de aplicativo agora deve mostrar que você entrou.</span><span class="sxs-lookup"><span data-stu-id="f449e-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="f449e-147">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="f449e-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="f449e-148">No campo **Nome do Aplicativo Web** , especifique um prefixo único para o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="f449e-149">O nome totalmente qualificado do aplicativo Web será *&lt;prefixo>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="f449e-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="f449e-150">Além disso, especifique um novo nome de grupo de recursos em **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="f449e-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="f449e-151">Em seguida, clique em **Novo** para criar um novo plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="f449e-152">Configurar o novo plano do Serviço de Aplicativo e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f449e-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="f449e-153">De volta na caixa de diálogo Criar Serviço de Aplicativo, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f449e-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="f449e-154">Após os recursos do Azure serem criados, a caixa de diálogo Publicar Web será preenchida com as configurações para seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="f449e-155">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f449e-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="f449e-156">Depois que o Visual Studio terminar de publicar o projeto inicial para o aplicativo Web do Azure, o navegador da área de trabalho se abre para exibir o aplicativo Web online.</span><span class="sxs-lookup"><span data-stu-id="f449e-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="f449e-157">Inicie o emulador de navegador móvel, copie a URL para o aplicativo de conferência (*<prefix>*.azurewebsites.net) do emulador e depois clique no botão da parte superior direita e selecione **Procurar por marca**.</span><span class="sxs-lookup"><span data-stu-id="f449e-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="f449e-158">Se você estiver usando o Internet Explorer 11 como navegador padrão, basta digitar `F12`, depois `Ctrl+8` e, em seguida, alterar o perfil do navegador para **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="f449e-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="f449e-159">A imagem abaixo mostra o modo de exibição *AllTags* em modo retrato (ao escolher **Procurar por marca**).</span><span class="sxs-lookup"><span data-stu-id="f449e-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="f449e-160">Enquanto depura o aplicativo MVC 5 no Visual Studio, você pode publicar seu aplicativo Web no Azure novamente para verificar o aplicativo Web online, diretamente no navegador móvel ou um emulador de navegador.</span><span class="sxs-lookup"><span data-stu-id="f449e-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="f449e-161">A exibição é muito legível em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="f449e-162">Você também já pode ver alguns dos efeitos visuais aplicados pelo framework de Bootstrap CSS.</span><span class="sxs-lookup"><span data-stu-id="f449e-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="f449e-163">Clique no link **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="f449e-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="f449e-164">O modo de exibição de marca do ASP.NET é ajustado à tela, o que é feito automaticamente pelo Bootstrap para você.</span><span class="sxs-lookup"><span data-stu-id="f449e-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="f449e-165">No entanto, é possível aprimorar esse modo de exibição para melhor se adequar ao navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="f449e-166">Por exemplo, a coluna **Data** é muito difícil de ler.</span><span class="sxs-lookup"><span data-stu-id="f449e-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="f449e-167">Mais adiante no tutorial, você vai alterar o modo de exibição *AllTags* para torná-lo acessível a dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="f449e-168"><a name="bkmk_bootstrap"></a> Framework de CSS Bootstrap</span><span class="sxs-lookup"><span data-stu-id="f449e-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="f449e-169">Uma novidade do modelo MVC 5 é o suporte interno ao Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f449e-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="f449e-170">Você já viu como ele aprimora imediatamente os diferentes modos de exibição em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="f449e-171">Por exemplo, a barra de navegação na parte superior é recolhida automaticamente quando a largura do navegador é menor.</span><span class="sxs-lookup"><span data-stu-id="f449e-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="f449e-172">No navegador da área de trabalho, tente redimensionar a janela e veja como a barra de navegação muda de aparência e estilo.</span><span class="sxs-lookup"><span data-stu-id="f449e-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="f449e-173">O responsável é o design Web dinâmico interno do Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f449e-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="f449e-174">Para ver como ficaria a aparência do aplicativo Web sem o Bootstrap, abra *App\_Start\\BundleConfig.cs* e transforme em comentário as linhas que contêm *bootstrap.js* e *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="f449e-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="f449e-175">O código a seguir mostra as duas últimas instruções do método `RegisterBundles` após a alteração:</span><span class="sxs-lookup"><span data-stu-id="f449e-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="f449e-176">Pressione `Ctrl+F5` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="f449e-177">Observe que a barra de navegação recolhível é agora apenas uma lista simples e desordenada.</span><span class="sxs-lookup"><span data-stu-id="f449e-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="f449e-178">Clique em **Procurar por marcação** novamente e clique em **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="f449e-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="f449e-179">No modo de exibição do emulador do navegador móvel, é possível ver que ele já não se ajusta à tela, e você precisa rolar para os lados para conseguir vero lado direito da tabela.</span><span class="sxs-lookup"><span data-stu-id="f449e-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="f449e-180">Desfaça as alterações e atualize o navegador móvel para verificar se a exibição acessível para dispositivo móvel foi restaurada.</span><span class="sxs-lookup"><span data-stu-id="f449e-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="f449e-181">O Bootstrap não é específico para o ASP.NET MVC 5, e você pode aproveitar esses recursos em qualquer aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f449e-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="f449e-182">Ele é, porém, um recurso interno do modelo de projeto MVC 5 do ASP.NET, de forma que o seu aplicativo Web MVC 5 pode, por padrão, aproveitar o Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f449e-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="f449e-183">Para saber mais sobre o Bootstrap, visite o site do [Bootstrap][BootstrapSite].</span><span class="sxs-lookup"><span data-stu-id="f449e-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="f449e-184">Na próxima seção, você verá como fornecer modos de exibição específicos para navegadores móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="f449e-185"><a name="bkmk_overrideviews"></a> Substituir os modos de exibição, os layouts e as exibições parciais</span><span class="sxs-lookup"><span data-stu-id="f449e-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="f449e-186">Você pode substituir qualquer modo de exibição (inclusive layouts e modos de exibição parciais) para navegadores de dispositivos móveis em geral, para um navegador móvel individual ou para qualquer navegador específico.</span><span class="sxs-lookup"><span data-stu-id="f449e-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="f449e-187">Para fornecer uma exibição específica para dispositivos móveis, você pode copiar um arquivo de modo de exibição e adicionar *.Mobile* ao nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f449e-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="f449e-188">Por exemplo, para criar uma exibição *Index* móvel, você pode copiar *Views\\Home\\Index.cshtml* para *Views\\Home\\Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f449e-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="f449e-189">Nesta seção, você criará um arquivo de layout específico para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="f449e-190">Para começar, copie *Views\\Shared\\\_Layout.cshtml* para *Views\\Shared\\\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f449e-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="f449e-191">Abra *\_Layout.Mobile.cshtml* e altere o título de **Aplicativo MVC5** para **Aplicativo MVC5(Móvel)**.</span><span class="sxs-lookup"><span data-stu-id="f449e-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="f449e-192">Em cada chamada `Html.ActionLink` à barra de navegação, remova "Procurar por" em cada link *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="f449e-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="f449e-193">O código a seguir mostra a marca `<ul class="nav navbar-nav">` completa do arquivo de layout para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="f449e-194">Copie o arquivo *Views\\Home\\AllTags.cshtml* para *Views\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f449e-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="f449e-195">Abra o novo arquivo e altere o elemento `<h2>` das "Marcas" para "marcas (M)":</span><span class="sxs-lookup"><span data-stu-id="f449e-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="f449e-196">Navegue até a página de marcas utilizando um navegador de desktop e o emulador do navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="f449e-197">O emulador do navegador móvel mostra as duas alterações que você fez (o título de *\_Layout.Mobile.cshtml* e de *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f449e-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="f449e-198">Por outro lado, a exibição do navegador da área de trabalho não foi alterada (com títulos de *\_Layout.cshtml* e *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f449e-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="f449e-199"><a name="bkmk_browserviews"></a> Criar modos de exibição para um navegador específico</span><span class="sxs-lookup"><span data-stu-id="f449e-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="f449e-200">Além dos modos de exibição específicos para navegadores móveis e de desktop, você pode criar modos de exibição para um único navegador.</span><span class="sxs-lookup"><span data-stu-id="f449e-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="f449e-201">Por exemplo, é possível criar modos de exibição específicos para o navegador do iPhone ou do Android.</span><span class="sxs-lookup"><span data-stu-id="f449e-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="f449e-202">Nesta seção, você criará um layout para o navegador do iPhone e uma versão para iPhone do modo de exibição *AllTags* .</span><span class="sxs-lookup"><span data-stu-id="f449e-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="f449e-203">Abra o arquivo *Global.asax* e adicione o código a seguir ao fim do método `Application_Start`.</span><span class="sxs-lookup"><span data-stu-id="f449e-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="f449e-204">Este código define um novo modo de exibição denominado “iPhone”, que será comparado a todas as solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="f449e-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="f449e-205">Se a solicitação de entrada corresponder à condição que você definiu (isto é, se o agente do usuário contiver a cadeia de caracteres “iPhone”), o ASP.NET MVC vai procurar por modos de exibição cujo nome contenha o sufixo “iPhone”.</span><span class="sxs-lookup"><span data-stu-id="f449e-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="f449e-206">Ao adicionar modos de exibição específicos para determinado navegador móvel, como para iPhone e Android, configure o primeiro argumento como `0` (inserido no topo da lista) para garantir que o modo específico para um navegador tenha precedência sobre o modelo para dispositivos móveis (*.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="f449e-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="f449e-207">Se o modelo para dispositivos móveis estiver no topo da lista, ele será selecionado no lugar do modo de exibição que você pretendia usar (a primeira correspondência predomina, e o modelo para dispositivos móveis corresponde a todos os navegadores móveis).</span><span class="sxs-lookup"><span data-stu-id="f449e-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="f449e-208">No código, clique com botão direito em `DefaultDisplayMode`, escolha **Resolver** e, em seguida, escolha `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="f449e-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="f449e-209">Isso inclui uma referência ao namespace `System.Web.WebPages`, que é onde os tipos de `DisplayModeProvider` e `DefaultDisplayMode` são definidos.</span><span class="sxs-lookup"><span data-stu-id="f449e-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="f449e-210">Como alternativa, basta adicionar manualmente a seguinte linha na seção `using` do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f449e-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="f449e-211">Salve as alterações.</span><span class="sxs-lookup"><span data-stu-id="f449e-211">Save the changes.</span></span> <span data-ttu-id="f449e-212">Copie o arquivo *Views\\Shared\\\_Layout.Mobile.cshtml* para *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f449e-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="f449e-213">Abra o novo arquivo e altere o título de `MVC5 Application (Mobile)` para `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="f449e-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="f449e-214">Copie o arquivo *Views\\Home\\AllTags.Mobile.cshtml* para *Views\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f449e-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="f449e-215">Abra o novo arquivo, altere o elemento `<h2>` de "Tags (M)" para "Tags (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="f449e-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="f449e-216">Execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f449e-216">Run the application.</span></span> <span data-ttu-id="f449e-217">Execute o emulador de navegador móvel com o agente do usuário definido como “iPhone” e navegue até o modo de exibição *AllTags* .</span><span class="sxs-lookup"><span data-stu-id="f449e-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="f449e-218">Se você estiver usando o emulador nas ferramentas de desenvolvedor do Internet Explorer 11 F12, configure a emulação para fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f449e-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="f449e-219">Perfil do navegador = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="f449e-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="f449e-220">Cadeia de caracteres de agente do usuário = **Personalizado**</span><span class="sxs-lookup"><span data-stu-id="f449e-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="f449e-221">Cadeia de caracteres personalizada = **Apple-iPhone5C1/1001,525**</span><span class="sxs-lookup"><span data-stu-id="f449e-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="f449e-222">A captura de tela a seguir mostra o modo de exibição *AllTags* renderizado no emulador das ferramentas de desenvolvedor do Internet Explorer 11 F12 com a cadeia de caracteres de agente do usuário personalizada (trata-se de uma cadeia de caracteres de agente do usuário do iPhone 5C).</span><span class="sxs-lookup"><span data-stu-id="f449e-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="f449e-223">No navegador móvel, selecione o link **Alto-falantes** .</span><span class="sxs-lookup"><span data-stu-id="f449e-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="f449e-224">Como não há um modo de exibição móvel (*AllSpeakers.Mobile.cshtml*), a exibição padrão de alto-falantes (*AllSpeakers.cshtml*) é renderizada utilizando o modo de exibição de layout para dispositivos móveis (*\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f449e-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="f449e-225">Como mostrado abaixo, o título **MVC5 Application (Móvel)** é definido em *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f449e-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="f449e-226">Você pode desativar globalmente a renderização do modo de exibição padrão (não móvel) dentro de um layout móvel ao configurar `RequireConsistentDisplayMode` como `true` no arquivo *Views\\\_ViewStart.cshtml*, desta forma:</span><span class="sxs-lookup"><span data-stu-id="f449e-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="f449e-227">Quando `RequireConsistentDisplayMode` estiver definido como `true`, o layout móvel (*\_Layout.Mobile.cshtml*) será usado apenas para modos de exibição móveis (ou seja, quando o arquivo de exibição tiver o formato ***ViewName**.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="f449e-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="f449e-228">Talvez você queira definir `RequireConsistentDisplayMode` como `true` se o layout voltado para dispositivos móveis não funcionar bem com seus modos de exibição não voltados para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="f449e-229">A captura de tela abaixo mostra como a página *Alto-falantes* é renderizada quando `RequireConsistentDisplayMode` é definido como `true` (sem a cadeia de caracteres "(Móvel)" na barra de navegação na parte superior).</span><span class="sxs-lookup"><span data-stu-id="f449e-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="f449e-230">Você pode desativar o modo de exibição consistente em um modo específico definindo o `RequireConsistentDisplayMode` como `false` no arquivo do modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f449e-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="f449e-231">A seguinte marcação no arquivo *Views\\Home\\AllSpeakers.cshtml* define `RequireConsistentDisplayMode` como `false`:</span><span class="sxs-lookup"><span data-stu-id="f449e-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="f449e-232">Nesta seção, você viu como criar layouts e exibições móveis e como criar layouts e exibições para dispositivos específicos, como o iPhone.</span><span class="sxs-lookup"><span data-stu-id="f449e-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="f449e-233">No entanto, a principal vantagem do framework de Bootstrap CSS é o layout responsivo, o que significa que uma única folha de estilos pode ser aplicada em área de trabalho, telefone e navegadores de tablet para criar uma aparência consistente.</span><span class="sxs-lookup"><span data-stu-id="f449e-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="f449e-234">Na próxima seção, você verá como aproveitar o Bootstrap para criar modos de exibição para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="f449e-235"><a name="bkmk_Improvespeakerslist"></a> Melhorar a lista de alto-falantes</span><span class="sxs-lookup"><span data-stu-id="f449e-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="f449e-236">Como você acabou de ver, o modo de exibição *Alto-falantes* é legível, mas os links são pequenos e difíceis de tocar em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="f449e-237">Nesta seção, você tornará o modo de exibição *AllSpeakers* acessível para dispositivos móveis, que exibe links grandes, fáceis de tocar e contém uma caixa de pesquisa para localizar alto-falantes rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f449e-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="f449e-238">É possível usar os estilos do [grupo de listas vinculadas][linked list group] do Bootstrap para aprimorar a exibição de *Speakers*.</span><span class="sxs-lookup"><span data-stu-id="f449e-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="f449e-239">Em *Views\\Home\\AllSpeakers.cshtml*, substitua o conteúdo do arquivo Razor pelo código abaixo.</span><span class="sxs-lookup"><span data-stu-id="f449e-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

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

<span data-ttu-id="f449e-240">O atributo `class="list-group"` na marca `<div>` aplica o estilo da lista do Bootstrap, e o atributo `class="input-group-item"` aplica o estilo do item da lista do Bootstrap a todos os links.</span><span class="sxs-lookup"><span data-stu-id="f449e-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="f449e-241">Atualize o navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-241">Refresh the mobile browser.</span></span> <span data-ttu-id="f449e-242">O modo de exibição atualizado tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f449e-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="f449e-243">Os estilos do [grupo de listas vinculadas][linked list group] do Bootstrap torna clicável a caixa inteira de todos os links, proporcionando uma experiência de usuário muito melhor.</span><span class="sxs-lookup"><span data-stu-id="f449e-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="f449e-244">Alterne para o modo de exibição de desktop e observe a consistência na aparência e no estilo.</span><span class="sxs-lookup"><span data-stu-id="f449e-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="f449e-245">Embora o modo de exibição do navegador móvel tenha sido aprimorado, é difícil navegar pela longa lista de alto-falantes.</span><span class="sxs-lookup"><span data-stu-id="f449e-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="f449e-246">O Bootstrap não oferece uma funcionalidade de filtro de pesquisa pronta para uso, mas você pode adicionar uma utilizando poucas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="f449e-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="f449e-247">Primeiro, adicione uma caixa de pesquisa à exibição, em seguida, vincule ao código do JavaScript para a função de filtro.</span><span class="sxs-lookup"><span data-stu-id="f449e-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="f449e-248">Em *Views\\Home\\AllSpeakers.cshtml*, adicione uma marcação \<form\> logo após a marcação \<h2\>, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="f449e-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

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

<span data-ttu-id="f449e-249">Observe que os estilos Bootstrap são aplicados às marcas `<form>` e `<input>`.</span><span class="sxs-lookup"><span data-stu-id="f449e-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="f449e-250">O elemento `<span>` adiciona um ícone [glyphicon][glyphicon] do Bootstrap à caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f449e-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="f449e-251">Na pasta *Scripts*, adicione um Arquivo JavaScript chamado *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="f449e-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="f449e-252">Abra o arquivo e cole o seguinte código nele:</span><span class="sxs-lookup"><span data-stu-id="f449e-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
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

<span data-ttu-id="f449e-253">Também será preciso incluir o filter.js em seus pacotes registrados.</span><span class="sxs-lookup"><span data-stu-id="f449e-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="f449e-254">Abra *App\_Start\\BundleConfig.cs* e altere os primeiros pacotes.</span><span class="sxs-lookup"><span data-stu-id="f449e-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="f449e-255">Altere a primeira instrução `bundles.Add` (para o pacote **jquery**) para incluir *Scripts\\filter.js*, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f449e-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="f449e-256">O pacote **jquery** já está renderizado pelo modo de exibição padrão *\_Layout*.</span><span class="sxs-lookup"><span data-stu-id="f449e-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="f449e-257">Mais tarde, você pode utilizar o mesmo código JavaScript para aplicar a funcionalidade de filtro a outros modos de exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="f449e-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="f449e-258">Atualize o navegador móvel e vá para o modo de exibição *AllSpeakers* .</span><span class="sxs-lookup"><span data-stu-id="f449e-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="f449e-259">Na caixa de pesquisa, digite “sc”.</span><span class="sxs-lookup"><span data-stu-id="f449e-259">In the search box, type "sc".</span></span> <span data-ttu-id="f449e-260">Agora, a lista de alto-falantes deve ser filtrada de acordo com a cadeia de caracteres de busca.</span><span class="sxs-lookup"><span data-stu-id="f449e-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="f449e-261"><a name="bkmk_improvetags"></a> Melhorar a lista de marcas</span><span class="sxs-lookup"><span data-stu-id="f449e-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="f449e-262">Como acontece com o modo de exibição *Alto-falantes*, o modo de exibição *Marcações* é legível, mas os links são pequenos e difíceis de tocar em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="f449e-263">É possível corrigir o modo de exibição *Marcações* da mesma forma que o modo de exibição *Alto-falantes* foi corrigido; basta usar as alterações de código descritas anteriormente com a seguinte sintaxe do método `Html.ActionLink` em *Views\\Home\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f449e-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="f449e-264">O navegador de desktop atualizado terá a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="f449e-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="f449e-265">E o navegador móvel atualizado terá a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="f449e-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="f449e-266">Se você perceber que o formato de lista original ainda permanece no navegador móvel e ficar imaginando o que aconteceu com o seu belo estilo do Bootstrap, isso é consequência de alguma alteração indesejada feita durante o processo para criar modos de exibição específicos para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="f449e-267">No entanto, agora que você está usando o Framework de CSS Bootstrap para criar um design Web dinâmico, vá em frente e exclua os modos de exibição e os layouts específicos para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="f449e-268">Assim que tiver feito isso, o navegador móvel atualizado vai exibir o estilo do Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f449e-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="f449e-269"><a name="bkmk_improvedates"></a> Melhorar a lista de datas</span><span class="sxs-lookup"><span data-stu-id="f449e-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="f449e-270">É possível melhorar o modo de exibição *Datas* da mesma forma como você melhorou o modo de exibição *Alto-falantes* e *Marcações*; basta usar as alterações de código descritas anteriormente com a seguinte sintaxe do método `Html.ActionLink` em *Views\\Home\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f449e-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="f449e-271">A exibição atualizada do navegador móvel será como esta:</span><span class="sxs-lookup"><span data-stu-id="f449e-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="f449e-272">Você pode aprimorar ainda mais o modo de exibição de *Datas* organizando os valores data-hora por data.</span><span class="sxs-lookup"><span data-stu-id="f449e-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="f449e-273">Isso pode ser feito com os estilos de [painéis][panels] do Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f449e-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="f449e-274">Substitua o conteúdo do arquivo *Views\\Home\\AllDates.cshtml* pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f449e-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="f449e-275">Esse código cria uma marcação `<div class="panel panel-primary">` separada para cada data diferente da lista e usa o [grupo de listas vinculadas][linked list group] para os respectivos links, como antes.</span><span class="sxs-lookup"><span data-stu-id="f449e-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="f449e-276">Esta é a aparência do navegador móvel quando esse código é executado:</span><span class="sxs-lookup"><span data-stu-id="f449e-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="f449e-277">Alterne para o navegador de desktop.</span><span class="sxs-lookup"><span data-stu-id="f449e-277">Switch to the desktop browser.</span></span> <span data-ttu-id="f449e-278">Novamente, repare na consistência de aparência.</span><span class="sxs-lookup"><span data-stu-id="f449e-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="f449e-279"><a name="bkmk_improvesessionstable"></a> Melhorar o modo de exibição da tabela de sessões</span><span class="sxs-lookup"><span data-stu-id="f449e-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="f449e-280">Nesta seção, você tornará o modo de exibição *SessionsTable* mais acessível a dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="f449e-281">Esta mudança é mais extensa que as anteriores.</span><span class="sxs-lookup"><span data-stu-id="f449e-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="f449e-282">No navegador móvel, toque o botão **Marcação** e insira `asp` na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f449e-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="f449e-283">Toque o link **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="f449e-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="f449e-284">Como você pode ver, a exibição está formatada como uma tabela, que foi desenhada para ser exibida em um navegador de desktop.</span><span class="sxs-lookup"><span data-stu-id="f449e-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="f449e-285">No entanto, é um pouco difícil de ler em um navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="f449e-286">Para corrigir isso, abra *Views\\Home\\SessionsTable.cshtml* e substitua o conteúdo do arquivo pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f449e-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

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

<span data-ttu-id="f449e-287">O código faz 3 coisas:</span><span class="sxs-lookup"><span data-stu-id="f449e-287">The code does 3 things:</span></span>

* <span data-ttu-id="f449e-288">Utiliza o [grupo de listas vinculadas personalizado][custom linked list group] do Bootstrap para formatar as informações da sessão verticalmente, de modo que elas possam ser lidas em um navegador móvel (usando classes como list-group-item-text)</span><span class="sxs-lookup"><span data-stu-id="f449e-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="f449e-289">Aplica o [sistema de grades][grid system] ao layout, de modo que os itens da sessão fluam horizontalmente no navegador da área de trabalho e verticalmente no navegador móvel (usando a classe col-md-4)</span><span class="sxs-lookup"><span data-stu-id="f449e-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="f449e-290">Usa os [utilitários dinâmicos][responsive utilities] para ocultar as marcações de sessão quando exibidas em um navegador móvel (usando a classe hidden-xs)</span><span class="sxs-lookup"><span data-stu-id="f449e-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="f449e-291">Você também pode tocar no link de um título para ir à respectiva sessão.</span><span class="sxs-lookup"><span data-stu-id="f449e-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="f449e-292">A imagem abaixo reflete as alterações de código.</span><span class="sxs-lookup"><span data-stu-id="f449e-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="f449e-293">O sistema de grades do Bootstrap organiza as sessões verticalmente, de maneira automática, no navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="f449e-294">Perceba, também, que as marcas não são exibidas.</span><span class="sxs-lookup"><span data-stu-id="f449e-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="f449e-295">Alterne para o navegador de desktop.</span><span class="sxs-lookup"><span data-stu-id="f449e-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="f449e-296">Perceba que, neste navegador, as marcas são exibidas.</span><span class="sxs-lookup"><span data-stu-id="f449e-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="f449e-297">Você também pode notar que o sistema de grades do Bootstrap organiza os itens da sessão em duas colunas.</span><span class="sxs-lookup"><span data-stu-id="f449e-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="f449e-298">Se ampliar o navegador, você perceberá que o arranjo muda para três colunas.</span><span class="sxs-lookup"><span data-stu-id="f449e-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="f449e-299"><a name="bkmk_improvesessionbycode"></a> Melhorar o modo de exibição SessionByCode</span><span class="sxs-lookup"><span data-stu-id="f449e-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="f449e-300">Finalmente, você consertará o modo de exibição *SessionByCode* , para torná-lo acessível a dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="f449e-301">No navegador móvel, toque o botão **Marcação** e insira `asp` na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f449e-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="f449e-302">Toque o link **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="f449e-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="f449e-303">As sessões para a marca ASP.NET são exibidas.</span><span class="sxs-lookup"><span data-stu-id="f449e-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="f449e-304">Escolha o link **Construindo um aplicativo de página única com o ASP.NET e AngularJS** .</span><span class="sxs-lookup"><span data-stu-id="f449e-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="f449e-305">A exibição padrão para navegador de desktop é boa, mas você pode aprimorar a aparência facilmente usando alguns componentes GUI do Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f449e-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="f449e-306">Abra *Views\\Home\\SessionByCode.cshtml* e substitua o conteúdo pela seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="f449e-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

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

<span data-ttu-id="f449e-307">A nova marcação usa o estilo de painéis do Bootstrap para melhorar o modo de exibição no dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="f449e-308">Atualize o navegador móvel.</span><span class="sxs-lookup"><span data-stu-id="f449e-308">Refresh the mobile browser.</span></span> <span data-ttu-id="f449e-309">A imagem a seguir reflete as alterações de código que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="f449e-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="f449e-310">Conclusão e revisão</span><span class="sxs-lookup"><span data-stu-id="f449e-310">Wrap Up and Review</span></span>
<span data-ttu-id="f449e-311">Este tutorial mostrou como usar o ASP.NET MVC 5 para desenvolver aplicativos Web com opção para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="f449e-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="f449e-312">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="f449e-312">These include:</span></span>

* <span data-ttu-id="f449e-313">Implantar um aplicativo ASP.NET MVC 5 em um aplicativo Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="f449e-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="f449e-314">Usar o Bootstrap para criar layouts Web dinâmicos em seu aplicativo MVC 5</span><span class="sxs-lookup"><span data-stu-id="f449e-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="f449e-315">Substituir layouts, modos de exibição e exibições parciais globalmente ou para um modo de exibição individual</span><span class="sxs-lookup"><span data-stu-id="f449e-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="f449e-316">Controlar a imposição de layout e de substituição parcial usando a propriedade `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="f449e-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="f449e-317">Criar modos de exibição voltados para navegadores específicos, como o do iPhone</span><span class="sxs-lookup"><span data-stu-id="f449e-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="f449e-318">Aplicar estilos do Bootstrap no código Razor</span><span class="sxs-lookup"><span data-stu-id="f449e-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="f449e-319">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f449e-319">See Also</span></span>
* [<span data-ttu-id="f449e-320">9 princípios básicos do design da Web responsivo</span><span class="sxs-lookup"><span data-stu-id="f449e-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="f449e-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="f449e-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="f449e-322">[Blog oficial do Bootstrap][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="f449e-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="f449e-323">[Tutorial do Bootstrap no Twitter, feito pela Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="f449e-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="f449e-324">[The Bootstrap Playground][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="f449e-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="f449e-325">[Práticas recomendadas pelo W3C para Aplicativos Web Móveis][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="f449e-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="f449e-326">[Recomendação Candidata do W3C para consultas de mídia][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="f449e-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f449e-327">O que mudou</span><span class="sxs-lookup"><span data-stu-id="f449e-327">What's changed</span></span>
* <span data-ttu-id="f449e-328">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f449e-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

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
[The Bootstrap Playground]: http://www.bootply.com/
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

