---
title: "aaaCreate um aplicativo da web ASP.NET Core no código do Visual Studio"
description: "Este tutorial ilustra como toocreate um núcleo de ASP.NET web app usando o código do Visual Studio."
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
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="59d6c-103">Criar um aplicativo Web ASP.NET Core no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="59d6c-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="59d6c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="59d6c-104">Overview</span></span>
<span data-ttu-id="59d6c-105">Este tutorial mostra como toocreate um núcleo de ASP.NET web app usando [código do Visual Studio (VS código)](http://code.visualstudio.com//Docs/whyvscode) e implantá-lo muito[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="59d6c-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="59d6c-106">Embora este artigo se refere a aplicativos tooweb, ela também se aplica tooAPI aplicativos e aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="59d6c-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="59d6c-107">O ASP.NET Core é uma reestruturação significativa do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="59d6c-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="59d6c-108">ASP.NET Core é uma nova estrutura de código-fonte aberto entre plataformas para criar modernos aplicativos em nuvem da Web usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="59d6c-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="59d6c-109">Para obter mais informações, consulte [tooASP.NET Introdução Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="59d6c-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="59d6c-110">Para obter informações sobre aplicativos Web do Serviço de Aplicativo do Azure, consulte [Visão geral de aplicativos Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59d6c-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="59d6c-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="59d6c-111">Prerequisites</span></span>
* <span data-ttu-id="59d6c-112">Instale o [Código do VS](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="59d6c-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="59d6c-113">Instalar o Git – você pode instalá-lo de um destes locais: [Chocolatey](https://chocolatey.org/packages/git) ou [git-scm.com](http://git-scm.com/downloads). Se você for novo tooGit, escolha [git scm.com](http://git-scm.com/downloads) e selecione a opção de saudação muito**Git de uso de saudação de Prompt de comando do Windows**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="59d6c-114">Depois de instalar o Git, você também precisará email e o nome de usuário de Git tooset Olá conforme necessário mais tarde no tutorial de saudação (quando executar uma confirmação do VS código).</span><span class="sxs-lookup"><span data-stu-id="59d6c-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="59d6c-115">Instalar o ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="59d6c-115">Install ASP.NET Core</span></span>
<span data-ttu-id="59d6c-116">O ASP.NET Core é uma pilha enxuta do .NET para criar aplicativos da Web e de nuvem modernos e executados em OS X, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="59d6c-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="59d6c-117">Ele foi criado de saudação Terra backup tooprovide uma estrutura de desenvolvimento otimizado para aplicativos que são qualquer nuvem toohello implantado ou executado localmente.</span><span class="sxs-lookup"><span data-stu-id="59d6c-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="59d6c-118">Ele consiste em componentes modulares com sobrecarga mínima, para que você mantenha a flexibilidade durante a construção de suas soluções.</span><span class="sxs-lookup"><span data-stu-id="59d6c-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="59d6c-119">Este tutorial é projetado tooget você começou a criar aplicativos com versões mais recentes de desenvolvimento saudação do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="59d6c-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="59d6c-120">Olá instruções a seguir é tooWindows específico.</span><span class="sxs-lookup"><span data-stu-id="59d6c-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="59d6c-121">Para instruções de instalação no OS X, no Linux e no Windows, veja [Introdução ao ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="59d6c-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="59d6c-122">Para obter instruções de instalação mais detalhadas para OS X, Linux e Windows, consulte [Instalação do ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="59d6c-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="59d6c-123">Criar aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="59d6c-123">Create hello web app</span></span>
<span data-ttu-id="59d6c-124">Esta seção mostra como tooscaffold um novo aplicativo ASP.NET web aplicativo usando a ferramenta de .NET CLI hello.</span><span class="sxs-lookup"><span data-stu-id="59d6c-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="59d6c-125">Digite o seguinte Olá Olá prompt de comando toocreate Olá projeto pasta scaffold Olá aplicativo e.</span><span class="sxs-lookup"><span data-stu-id="59d6c-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI – gerador do ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="59d6c-127">toorestore Olá pacotes do NuGet necessários, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="59d6c-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="59d6c-128">Executar o aplicativo da web de saudação localmente</span><span class="sxs-lookup"><span data-stu-id="59d6c-128">Run hello web app locally</span></span>
<span data-ttu-id="59d6c-129">Agora que você criou Olá web app e todos os pacotes do NuGet Olá para o aplicativo hello recuperados, você pode executar o aplicativo da web de saudação localmente.</span><span class="sxs-lookup"><span data-stu-id="59d6c-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="59d6c-130">Executar o aplicativo hello (Olá `dotnet run` comando criará o aplicativo hello quando ele está desatualizado):</span><span class="sxs-lookup"><span data-stu-id="59d6c-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="59d6c-131">Abra um navegador e navegue toohello URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="59d6c-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="59d6c-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="59d6c-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="59d6c-133">a página de aplicativo da web de saudação padrão Olá será exibida da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="59d6c-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Aplicativo Web local em um navegador](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="59d6c-135">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="59d6c-135">Close your browser.</span></span> <span data-ttu-id="59d6c-136">Em Olá **janela comando**, pressione **Ctrl + C** tooshut aplicativo hello e fechar Olá **janela de comando**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="59d6c-137">Criar um aplicativo web no hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="59d6c-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="59d6c-138">Olá etapas a seguir orientará você durante a criação de um aplicativo web no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="59d6c-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="59d6c-139">Faça logon no toohello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="59d6c-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="59d6c-140">Clique em **novo** em Olá superior esquerda da saudação Portal.</span><span class="sxs-lookup"><span data-stu-id="59d6c-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="59d6c-141">Clique em **Aplicativos Web > Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-141">Click **Web Apps > Web App**.</span></span>
   
    ![Novo aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="59d6c-143">Insira um valor para **Nome**, como **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="59d6c-144">Observe que esse nome precisa toobe exclusivo e portal Olá irá impor que durante a tentativa de nome de saudação tooenter.</span><span class="sxs-lookup"><span data-stu-id="59d6c-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="59d6c-145">Portanto, se você selecionar uma Insira um valor diferente, você precisará toosubstitute esse valor para cada ocorrência de **SampleWebAppDemo** que você vê neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="59d6c-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="59d6c-146">Selecione um **Plano de Serviço de Aplicativo** existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="59d6c-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="59d6c-147">Se você criar um novo plano, selecione Olá tipo de preço, local e outras opções.</span><span class="sxs-lookup"><span data-stu-id="59d6c-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="59d6c-148">Para obter mais informações sobre planos de serviço de aplicativo, consulte o artigo Olá [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59d6c-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Folha de novo aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="59d6c-150">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-150">Click **Create**.</span></span>
   
    ![folha de aplicativo Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="59d6c-152">Habilitar a publicação de Git para o novo aplicativo de web Olá</span><span class="sxs-lookup"><span data-stu-id="59d6c-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="59d6c-153">Git é um sistema de controle de versão distribuídos que você pode usar toodeploy seu aplicativo da web do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="59d6c-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="59d6c-154">Armazenar código Olá que gravar para seu aplicativo web em um repositório Git local e implantará seu código tooAzure enviando o repositório remoto tooa.</span><span class="sxs-lookup"><span data-stu-id="59d6c-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="59d6c-155">Faça logon no hello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="59d6c-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="59d6c-156">Clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-156">Click **Browse**.</span></span>
3. <span data-ttu-id="59d6c-157">Clique em **aplicativos Web** tooview uma lista de aplicativos da web de saudação associado à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="59d6c-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="59d6c-158">Selecione o aplicativo de web de saudação criado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="59d6c-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="59d6c-159">Na folha de saudação do aplicativo web, clique em **configurações** > **implantação contínua**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![host de aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="59d6c-161">Clique em **Escolher fonte > Repositório Git local**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="59d6c-162">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-162">Click **OK**.</span></span>
   
    ![Repositório Git Local do Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="59d6c-164">Se você não configurou previamente as credenciais de implantação para publicação de um Aplicativo Web ou outro aplicativo de Serviço de Aplicativo, configure-as agora:</span><span class="sxs-lookup"><span data-stu-id="59d6c-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="59d6c-165">Clique em **Configurações** > **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="59d6c-166">Olá **definir credenciais de implantação** folha será exibida.</span><span class="sxs-lookup"><span data-stu-id="59d6c-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="59d6c-167">Digite um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="59d6c-167">Create a user name and password.</span></span>  <span data-ttu-id="59d6c-168">Você precisará dessa senha posteriormente ao configurar o Git.</span><span class="sxs-lookup"><span data-stu-id="59d6c-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="59d6c-169">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-169">Click **Save**.</span></span>
9. <span data-ttu-id="59d6c-170">Na folha de seu aplicativo Web, clique em **Configurações > Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="59d6c-171">URL de saudação do repositório Git remoto Olá que você implantará toois mostrado em **URL do GIT**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="59d6c-172">Saudação de cópia **URL do GIT** valor para uso posterior no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="59d6c-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![URL Git do Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="59d6c-174">Publicar seu tooAzure de aplicativo web do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="59d6c-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="59d6c-175">Nesta seção, você criará um repositório Git local e enviar por push de toodeploy de tooAzure esse repositório seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="59d6c-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="59d6c-176">No código VS, selecione Olá **Git** opção na barra de navegação à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="59d6c-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Ícone do Git no Código do VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="59d6c-178">Selecione **inicializar o repositório do git** toomake-se de que seu espaço de trabalho está sob controle do código-fonte git.</span><span class="sxs-lookup"><span data-stu-id="59d6c-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Inicializar Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="59d6c-180">Abra Olá janela de comando e altere o diretório de toohello diretórios de seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="59d6c-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="59d6c-181">Em seguida, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="59d6c-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="59d6c-182">Esse comando previne um problema de texto envolvendo as terminações CRLF e LF.</span><span class="sxs-lookup"><span data-stu-id="59d6c-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="59d6c-183">No código VS, adicionar uma mensagem de confirmação e clique em Olá **confirmar todos** ícone de verificação.</span><span class="sxs-lookup"><span data-stu-id="59d6c-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Confirmar Tudo do Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="59d6c-185">Depois de concluir o processamento Git, você verá que não existem arquivos listados na janela de Git de saudação em **alterações**.</span><span class="sxs-lookup"><span data-stu-id="59d6c-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Sem alterações do Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="59d6c-187">Altere toohello back janela de comando onde o prompt de comando Olá aponta toohello diretório onde o aplicativo web está localizado.</span><span class="sxs-lookup"><span data-stu-id="59d6c-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="59d6c-188">Crie uma referência remota para enviar atualizações tooyour web app usando Olá URL de Git (terminando em ".git") que você copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="59d6c-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="59d6c-189">Configure Git toosave suas credenciais localmente para que eles serão acrescentadas automaticamente tooyour comandos de push gerados a partir de código do VS.</span><span class="sxs-lookup"><span data-stu-id="59d6c-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="59d6c-190">Enviar por push o tooAzure alterações inserindo Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="59d6c-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="59d6c-191">Após essa tooAzure push inicial, será toodo capaz de envio de saudação todos os comandos de código VS.</span><span class="sxs-lookup"><span data-stu-id="59d6c-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="59d6c-192">Você será solicitado para senha Olá que você criou anteriormente no Azure.</span><span class="sxs-lookup"><span data-stu-id="59d6c-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="59d6c-193">**Observação: a senha não será visível.**</span><span class="sxs-lookup"><span data-stu-id="59d6c-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="59d6c-194">saída de saudação do hello acima comando termina com uma mensagem de que a implantação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="59d6c-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="59d6c-195">Se você fizer alterações tooyour aplicativo, você poderá republicar diretamente no código VS usando a funcionalidade interna de Git Olá selecionando Olá **confirmar todos os** opção seguido Olá **Push** opção.</span><span class="sxs-lookup"><span data-stu-id="59d6c-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="59d6c-196">Você encontrará Olá **Push** opção disponível no hello menu suspenso próximo toohello **confirmar todos os** e **atualização** botões.</span><span class="sxs-lookup"><span data-stu-id="59d6c-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="59d6c-197">Se você precisar toocollaborate em um projeto, você deve considerar enviar por push tooGitHub entre tooAzure de envio por push.</span><span class="sxs-lookup"><span data-stu-id="59d6c-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="59d6c-198">Executar o aplicativo hello no Azure</span><span class="sxs-lookup"><span data-stu-id="59d6c-198">Run hello app in Azure</span></span>
<span data-ttu-id="59d6c-199">Agora que você implantou seu aplicativo web, vamos executar o aplicativo hello enquanto hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="59d6c-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="59d6c-200">Isso pode ser feito de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="59d6c-200">This can be done in two ways:</span></span>

* <span data-ttu-id="59d6c-201">Abra um navegador e insira o nome de saudação do seu aplicativo web da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="59d6c-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="59d6c-202">Olá Portal do Azure, localize a folha de aplicativo web Olá para seu aplicativo web e clique no **procurar** tooview seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="59d6c-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="59d6c-203">no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="59d6c-203">in your default browser.</span></span>

![Aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="59d6c-205">Resumo</span><span class="sxs-lookup"><span data-stu-id="59d6c-205">Summary</span></span>
<span data-ttu-id="59d6c-206">Neste tutorial, você aprendeu como toocreate um aplicativo web no código VS e implantá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="59d6c-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="59d6c-207">Para obter mais informações sobre código VS, consulte o artigo Olá [por código do Visual Studio?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="59d6c-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="59d6c-208">Para obter informações sobre os aplicativos Web do Serviço de Aplicativo, consulte [Visão geral de Aplicativos Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59d6c-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

