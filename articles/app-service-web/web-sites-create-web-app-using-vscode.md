---
title: Criar um aplicativo Web ASP.NET Core no Visual Studio Code
description: "Este tutorial mostra como criar um aplicativo Web ASP.NET Core usando o código do Visual Studio."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="2cc4f-103">Criar um aplicativo Web ASP.NET Core no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2cc4f-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="2cc4f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2cc4f-104">Overview</span></span>
<span data-ttu-id="2cc4f-105">Este tutorial mostra como criar um aplicativo Web ASP.NET Core usando [Código do Visual Studio (Código do VS)](http://code.visualstudio.com//Docs/whyvscode) e implantá-lo no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="2cc4f-106">Embora este artigo esteja relacionado a aplicativos Web, ele também serve para aplicativos de API e aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="2cc4f-107">O ASP.NET Core é uma reestruturação significativa do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="2cc4f-108">ASP.NET Core é uma nova estrutura de código-fonte aberto entre plataformas para criar modernos aplicativos em nuvem da Web usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="2cc4f-109">Para obter mais informações, consulte [Introdução ao ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="2cc4f-110">Para obter informações sobre aplicativos Web do Serviço de Aplicativo do Azure, consulte [Visão geral de aplicativos Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="2cc4f-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2cc4f-111">Prerequisites</span></span>
* <span data-ttu-id="2cc4f-112">Instale o [Código do VS](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="2cc4f-113">Instalar o Git – você pode instalá-lo de um destes locais: [Chocolatey](https://chocolatey.org/packages/git) ou [git-scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="2cc4f-114">Se você for iniciante no Git, escolha [git-scm.com](http://git-scm.com/downloads) e selecione a opção para **Usar o Git no Prompt de Comando do Windows**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="2cc4f-115">Depois de instalar o Git, também será necessário definir o nome de usuário e email do Git, pois eles são necessários posteriormente no tutorial (ao realizar uma confirmação do Código do VS).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="2cc4f-116">Instalar o ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2cc4f-116">Install ASP.NET Core</span></span>
<span data-ttu-id="2cc4f-117">O ASP.NET Core é uma pilha enxuta do .NET para criar aplicativos da Web e de nuvem modernos e executados em OS X, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="2cc4f-118">Ele foi criado do zero para fornecer uma estrutura de desenvolvimento otimizada para aplicativos que são implantados na nuvem ou então executados localmente.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="2cc4f-119">Ele consiste em componentes modulares com sobrecarga mínima, para que você mantenha a flexibilidade durante a construção de suas soluções.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="2cc4f-120">Este tutorial é projetado para começar a criar aplicativos com as versões de desenvolvimento do ASP.NET Core mais recentes.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="2cc4f-121">As instruções a seguir são específicas do Windows.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="2cc4f-122">Para instruções de instalação no OS X, no Linux e no Windows, veja [Introdução ao ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="2cc4f-123">Para obter instruções de instalação mais detalhadas para OS X, Linux e Windows, consulte [Instalação do ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="2cc4f-124">Criar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="2cc4f-124">Create the web app</span></span>
<span data-ttu-id="2cc4f-125">Esta seção mostra como criar o scaffolding de um novo aplicativo Web do ASP.NET usando a ferramenta CLI do .NET.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="2cc4f-126">Digite o seguinte no prompt de comando para criar a pasta do projeto e o scaffolding do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI – gerador do ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="2cc4f-128">Para restaurar os pacotes do NuGet necessários, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="2cc4f-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="2cc4f-129">Executar o aplicativo Web localmente</span><span class="sxs-lookup"><span data-stu-id="2cc4f-129">Run the web app locally</span></span>
<span data-ttu-id="2cc4f-130">Agora que criou o aplicativo Web e recuperou todos os pacotes do NuGet para o aplicativo, você pode executar o aplicativo Web localmente.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="2cc4f-131">Execute o aplicativo (o comando `dotnet run` compilará o aplicativo quando ele estiver desatualizado):</span><span class="sxs-lookup"><span data-stu-id="2cc4f-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="2cc4f-132">Abra uma janela de navegador e navegue até a URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="2cc4f-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="2cc4f-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="2cc4f-134">A página padrão do aplicativo Web será exibida da maneira a seguir.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-134">The default page of the web app will appear as follows.</span></span>
   
    ![Aplicativo Web local em um navegador](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="2cc4f-136">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-136">Close your browser.</span></span> <span data-ttu-id="2cc4f-137">Na **Janela Comando**, pressione **Ctrl + C** para encerrar o aplicativo e feche a **Janela Comando**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="2cc4f-138">Criar um aplicativo Web no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2cc4f-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="2cc4f-139">As etapas a seguir o guiarão ao longo da criação de um aplicativo Web no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="2cc4f-140">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2cc4f-141">Clique em **NOVO** na parte superior esquerda do Portal.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="2cc4f-142">Clique em **Aplicativos Web > Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-142">Click **Web Apps > Web App**.</span></span>
   
    ![Novo aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="2cc4f-144">Insira um valor para **Nome**, como **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="2cc4f-145">Observe que esse nome precisa ser exclusivo, e o portal imporá isso quando você tentar inserir o nome.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="2cc4f-146">Portanto, se você selecionar um valor diferente, precisará substituir esse valor para cada ocorrência do **SampleWebAppDemo** que você vê neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="2cc4f-147">Selecione um **Plano de Serviço de Aplicativo** existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="2cc4f-148">Se você criar um novo plano, selecione a camada de preços, localização e outras opções.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="2cc4f-149">Para obter mais informações sobre planos de serviço de aplicativo, consulte o artigo [Visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Folha de novo aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="2cc4f-151">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-151">Click **Create**.</span></span>
   
    ![folha de aplicativo Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="2cc4f-153">Habilitar a publicação de Git para o novo aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="2cc4f-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="2cc4f-154">O Git é um sistema de controle de versão distribuído que você pode usar para implantar seu aplicativo Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="2cc4f-155">Você armazenará o código que você escreve para seu aplicativo Web em um repositório Git local e você implantará seu código no Azure enviando-o por push para um repositório remoto.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="2cc4f-156">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2cc4f-157">Clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-157">Click **Browse**.</span></span>
3. <span data-ttu-id="2cc4f-158">Clique em **aplicativos Web** para exibir uma lista dos aplicativos Web associados à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="2cc4f-159">Selecione o aplicativo Web criado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="2cc4f-160">Na folha de seu aplicativo Web, clique em **Configurações** > **Implantação contínua**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![host de aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="2cc4f-162">Clique em **Escolher fonte > Repositório Git local**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="2cc4f-163">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-163">Click **OK**.</span></span>
   
    ![Repositório Git Local do Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="2cc4f-165">Se você não configurou previamente as credenciais de implantação para publicação de um Aplicativo Web ou outro aplicativo de Serviço de Aplicativo, configure-as agora:</span><span class="sxs-lookup"><span data-stu-id="2cc4f-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="2cc4f-166">Clique em **Configurações** > **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="2cc4f-167">A folha **Definir credenciais de implantação** será exibida.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="2cc4f-168">Digite um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-168">Create a user name and password.</span></span>  <span data-ttu-id="2cc4f-169">Você precisará dessa senha posteriormente ao configurar o Git.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="2cc4f-170">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-170">Click **Save**.</span></span>
9. <span data-ttu-id="2cc4f-171">Na folha de seu aplicativo Web, clique em **Configurações > Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="2cc4f-172">A URL do repositório Git remoto na qual você implantará é mostrada em **GIT URL**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="2cc4f-173">Copie o valor de **URL do GIT** para uso posterior no tutorial.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![URL Git do Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="2cc4f-175">Publicar seu aplicativo Web no serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2cc4f-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="2cc4f-176">Nesta seção, você criará um repositório do Git local e enviará esse repositório por push ao Azure para implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="2cc4f-177">No código do VS, selecione a opção **Git** na barra de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Ícone do Git no Código do VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="2cc4f-179">Selecione **Inicializar repositório git** para assegurar que o espaço de trabalho está sob controle do código-fonte git.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Inicializar Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="2cc4f-181">Abra a Janela Comando e altere os diretórios para o diretório do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="2cc4f-182">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2cc4f-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="2cc4f-183">Esse comando previne um problema de texto envolvendo as terminações CRLF e LF.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="2cc4f-184">No Código do VS, adicione uma mensagem de confirmação e clique no ícone de verificação **Confirmar Tudo** .</span><span class="sxs-lookup"><span data-stu-id="2cc4f-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Confirmar Tudo do Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="2cc4f-186">Após a conclusão do processamento do Git, você verá que não há nenhum arquivo listado na janela do Git em **Alterações**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Sem alterações do Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="2cc4f-188">Retorne à Janela do Comando em que o prompt de comando aponta para o diretório em que o aplicativo Web está localizado.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="2cc4f-189">Crie uma referência remota para enviar atualizações para seu aplicativo Web usando a URL do Git (terminando em ".git") que você copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="2cc4f-190">Configure o Git para salvar suas credenciais localmente para que elas possam ser acrescentadas automaticamente aos seus comandos por push gerados no VS Code.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="2cc4f-191">Envie as alterações por push ao Azure usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="2cc4f-192">Depois desse push inicial no Azure, você poderá executar todos os comandos por push no VS Code.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="2cc4f-193">Será solicitada a senha que você criou anteriormente no Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="2cc4f-194">**Observação: a senha não será visível.**</span><span class="sxs-lookup"><span data-stu-id="2cc4f-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="2cc4f-195">A saída deste comando termina com uma mensagem de que a implantação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="2cc4f-196">Se fizer alterações ao seu aplicativo, você poderá publicá-las de novo diretamente no Código do VS usando a funcionalidade interna do Git selecionando a opção **Confirmar Tudo** seguida da opção **Enviar por Push**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="2cc4f-197">Você encontrará a opção **Envio por Push** disponível no menu suspenso ao lado de **Confirmar Tudo** e dos botões **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="2cc4f-198">Se precisa colaborar em um projeto, você deve considerar envios por push ao GitHub entre os envios por push ao Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="2cc4f-199">Executar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="2cc4f-199">Run the app in Azure</span></span>
<span data-ttu-id="2cc4f-200">Agora que você implantou seu aplicativo Web, vamos executar o aplicativo enquanto ele está hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="2cc4f-201">Isso pode ser feito de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="2cc4f-201">This can be done in two ways:</span></span>

* <span data-ttu-id="2cc4f-202">Abra um navegador e digite o nome do aplicativo Web da maneira a seguir.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="2cc4f-203">No Portal do Azure, localize a folha de seu aplicativo Web e clique em **Procurar** para exibi-lo</span><span class="sxs-lookup"><span data-stu-id="2cc4f-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="2cc4f-204">no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-204">in your default browser.</span></span>

![Aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="2cc4f-206">Resumo</span><span class="sxs-lookup"><span data-stu-id="2cc4f-206">Summary</span></span>
<span data-ttu-id="2cc4f-207">Neste tutorial, você aprendeu a criar um aplicativo Web no código do VS e implantá-lo no Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc4f-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="2cc4f-208">Para saber mais sobre o Código do VS, confira o artigo [Por que o Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="2cc4f-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="2cc4f-209">Para obter informações sobre os aplicativos Web do Serviço de Aplicativo, consulte [Visão geral de Aplicativos Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cc4f-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

