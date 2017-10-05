---
title: Criando aplicativos Web com Flask no Azure
description: "Um tutorial que apresenta a execução de um aplicativo Web Python no Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="0ba04-103">Criando aplicativos Web com Flask no Azure</span><span class="sxs-lookup"><span data-stu-id="0ba04-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="0ba04-104">Este tutorial descreve como começar a execução de Python em [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="0ba04-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="0ba04-105">Os Aplicativos Web fornecem hospedagem gratuita limitada e implantação rápida, além permitirem a você usar o Python!</span><span class="sxs-lookup"><span data-stu-id="0ba04-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="0ba04-106">Conforme o aplicativo cresce, você pode alternar para hospedagem paga e também integrar-se com todos os outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ba04-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="0ba04-107">Você criará um aplicativo usando a estrutura da Web Flask (confira versões alternativas deste tutorial para [Django](web-sites-python-create-deploy-django-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="0ba04-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="0ba04-108">Você vai criar o site na Galeria do Azure, configurar a implantação do Git e clonar o repositório localmente.</span><span class="sxs-lookup"><span data-stu-id="0ba04-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="0ba04-109">Em seguida, você vai executar o aplicativo localmente, fazer alterações, confirmá-las e enviá-las por push para o Azure.</span><span class="sxs-lookup"><span data-stu-id="0ba04-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="0ba04-110">O tutorial mostra como fazer isso por meio do Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="0ba04-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="0ba04-111">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0ba04-112">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="0ba04-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0ba04-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ba04-113">Prerequisites</span></span>
* <span data-ttu-id="0ba04-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="0ba04-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="0ba04-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="0ba04-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="0ba04-116">setuptools, pip, virtualenv (somente Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="0ba04-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="0ba04-117">Git</span><span class="sxs-lookup"><span data-stu-id="0ba04-117">Git</span></span>
* <span data-ttu-id="0ba04-118">PTVS ([Python Tools para Visual Studio][Python Tools para Visual Studio]) – Observação: isso é opcional</span><span class="sxs-lookup"><span data-stu-id="0ba04-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="0ba04-119">**Observação**: atualmente não há suporte à a publicação do TFS em projetos de Python.</span><span class="sxs-lookup"><span data-stu-id="0ba04-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="0ba04-120">Windows</span><span class="sxs-lookup"><span data-stu-id="0ba04-120">Windows</span></span>
<span data-ttu-id="0ba04-121">Caso você ainda não tenha o Python 2.7 ou 3.4 instalado (32 bits), recomendamos instalar o [SDK do Azure para Python 2.7] ou [SDK do Azure para Python 3.4] usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="0ba04-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="0ba04-122">Isso instala a versão de 32 bits do Python, setuptools, pip, virtualenv, etc (Python de 32 bits é o que está instalado nos computadores host do Azure).</span><span class="sxs-lookup"><span data-stu-id="0ba04-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="0ba04-123">Como alternativa, você pode obter o Python por meio de [python.org].</span><span class="sxs-lookup"><span data-stu-id="0ba04-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="0ba04-124">Para Git, recomendamos [Git para Windows] ou [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="0ba04-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="0ba04-125">Se você usar o Visual Studio, você pode usar o suporte integrado a Git.</span><span class="sxs-lookup"><span data-stu-id="0ba04-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="0ba04-126">Também recomendamos a instalação das [Ferramentas Python 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="0ba04-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="0ba04-127">Isso é opcional, mas se você tiver o [Visual Studio], incluindo o Visual Studio Community 2013 ou o Visual Studio Express 2013 para Web gratuitos, isso lhe dará um excelente IDE (ambiente de desenvolvimento integrado) do Python.</span><span class="sxs-lookup"><span data-stu-id="0ba04-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="0ba04-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="0ba04-128">Mac/Linux</span></span>
<span data-ttu-id="0ba04-129">Você deve ter o Python e Git já instalados, mas certifique-se de ter uma das versões 2.7 ou 3.4 do Python.</span><span class="sxs-lookup"><span data-stu-id="0ba04-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="0ba04-130">Criar um aplicativo Web no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0ba04-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="0ba04-131">A primeira etapa na criação de seu aplicativo é criar o aplicativo Web por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ba04-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="0ba04-132">Faça logon no Portal do Azure e clique no botão **Novo** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="0ba04-133">Clique em **Web + móvel**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="0ba04-134">Na caixa de pesquisa, digite "python".</span><span class="sxs-lookup"><span data-stu-id="0ba04-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="0ba04-135">Nos resultados da pesquisa, selecione **Flask** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="0ba04-136">Configure o novo aplicativo Flask, como a criação de um novo plano do Serviço de Aplicativo e um novo grupo de recursos para ele.</span><span class="sxs-lookup"><span data-stu-id="0ba04-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="0ba04-137">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="0ba04-138">Configure a publicação de Git para seu aplicativo Web recém-criado seguindo as instruções em [Implantação de GIT local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="0ba04-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="0ba04-139">Visão geral do aplicativo</span><span class="sxs-lookup"><span data-stu-id="0ba04-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="0ba04-140">Conteúdos do repositório Git</span><span class="sxs-lookup"><span data-stu-id="0ba04-140">Git repository contents</span></span>
<span data-ttu-id="0ba04-141">Eis aqui uma visão geral dos arquivos que você encontrará no repositório Git inicial, o qual iremos clonar na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="0ba04-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="0ba04-142">Fontes principais para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-142">Main sources for the application.</span></span>  <span data-ttu-id="0ba04-143">Consiste em 3 páginas (índice, sobre, contato) com um layout mestre.</span><span class="sxs-lookup"><span data-stu-id="0ba04-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="0ba04-144">Scripts e conteúdo estático incluem bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="0ba04-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="0ba04-145">Suporte ao servidor de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="0ba04-145">Local development server support.</span></span> <span data-ttu-id="0ba04-146">Use esta opção para executar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="0ba04-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="0ba04-147">Arquivos de projeto para uso com [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="0ba04-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="0ba04-148">Proxy de IIS para ambientes virtuais e suporte à depuração remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="0ba04-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="0ba04-149">Pacotes externos requeridos por este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-149">External packages needed by this application.</span></span> <span data-ttu-id="0ba04-150">O script de implantação fará a instalação por pip dos pacotes listados nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="0ba04-151">Arquivos de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="0ba04-151">IIS configuration files.</span></span>  <span data-ttu-id="0ba04-152">O script de implantação usará o web.x.y.config apropriado e o copiará como web.config.</span><span class="sxs-lookup"><span data-stu-id="0ba04-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="0ba04-153">Arquivos opcionais - personalizando a implantação</span><span class="sxs-lookup"><span data-stu-id="0ba04-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="0ba04-154">Arquivos opcionais - tempo de execução do Python</span><span class="sxs-lookup"><span data-stu-id="0ba04-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="0ba04-155">Arquivos adicionais no servidor</span><span class="sxs-lookup"><span data-stu-id="0ba04-155">Additional files on server</span></span>
<span data-ttu-id="0ba04-156">Alguns arquivos existem no servidor, mas não são adicionados ao repositório git.</span><span class="sxs-lookup"><span data-stu-id="0ba04-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="0ba04-157">Eles são criados pelo script de implantação.</span><span class="sxs-lookup"><span data-stu-id="0ba04-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="0ba04-158">Arquivo de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="0ba04-158">IIS configuration file.</span></span>  <span data-ttu-id="0ba04-159">Criado por meio de web.x.y.config em toda implantação.</span><span class="sxs-lookup"><span data-stu-id="0ba04-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="0ba04-160">Ambiente virtual do Python.</span><span class="sxs-lookup"><span data-stu-id="0ba04-160">Python virtual environment.</span></span>  <span data-ttu-id="0ba04-161">Criado durante a implantação, se ainda não existir um ambiente virtual compatível no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="0ba04-162">Pacotes listados em requirements.txt são instalados por pip, mas o pip ignorará a instalação se os pacotes já estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="0ba04-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="0ba04-163">As próximas três seções descrevem como prosseguir com o desenvolvimento de aplicativo Web em três ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="0ba04-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="0ba04-164">Windows, com Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ba04-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="0ba04-165">Windows, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="0ba04-165">Windows, with command line</span></span>
* <span data-ttu-id="0ba04-166">Mac/Linux, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="0ba04-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="0ba04-167">Desenvolvimento de aplicativo Web - Windows - Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ba04-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="0ba04-168">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="0ba04-168">Clone the repository</span></span>
<span data-ttu-id="0ba04-169">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ba04-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="0ba04-170">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="0ba04-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="0ba04-171">Abra o arquivo da solução (.sln) que está incluído na raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="0ba04-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="0ba04-172">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="0ba04-172">Create virtual environment</span></span>
<span data-ttu-id="0ba04-173">Agora vamos criar um ambiente virtual para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="0ba04-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="0ba04-174">Clique com o botão direito do mouse em **Ambientes Python** e selecione **Adicionar ambiente virtual...**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="0ba04-175">Verifique se o nome do ambiente é `env`.</span><span class="sxs-lookup"><span data-stu-id="0ba04-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="0ba04-176">Selecione o interpretador de base.</span><span class="sxs-lookup"><span data-stu-id="0ba04-176">Select the base interpreter.</span></span>  <span data-ttu-id="0ba04-177">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha **Configurações do Aplicativo** de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="0ba04-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="0ba04-178">Verifique se a opção para baixar e instalar pacotes está marcada.</span><span class="sxs-lookup"><span data-stu-id="0ba04-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="0ba04-179">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-179">Click **Create**.</span></span>  <span data-ttu-id="0ba04-180">Isso criará o ambiente virtual e instalar dependências listadas em requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="0ba04-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="0ba04-181">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="0ba04-181">Run using development server</span></span>
<span data-ttu-id="0ba04-182">Pressione F5 para iniciar a depuração e o navegador da Web abrirá automaticamente na página sendo executada localmente.</span><span class="sxs-lookup"><span data-stu-id="0ba04-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="0ba04-183">Você pode definir pontos de interrupção nas fontes, usar as janelas de observação etc.  Consulte [Ferramentas Python para Documentação] do Visual Studio para obter mais informações sobre os vários recursos.</span><span class="sxs-lookup"><span data-stu-id="0ba04-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="0ba04-184">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="0ba04-184">Make changes</span></span>
<span data-ttu-id="0ba04-185">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0ba04-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="0ba04-186">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="0ba04-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="0ba04-187">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="0ba04-187">Install more packages</span></span>
<span data-ttu-id="0ba04-188">Seu aplicativo pode ter dependências além de Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="0ba04-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="0ba04-189">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="0ba04-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="0ba04-190">Para instalar um pacote, clique no ambiente virtual e selecione **Instalar pacote Python**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="0ba04-191">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite `azure`:</span><span class="sxs-lookup"><span data-stu-id="0ba04-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="0ba04-192">Clique com o botão direito do mouse em no ambiente virtual e selecione **Gerar requirements.txt** para atualizar requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="0ba04-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="0ba04-193">Em seguida, confirme as alterações a requirements.txt no repositório Git.</span><span class="sxs-lookup"><span data-stu-id="0ba04-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="0ba04-194">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="0ba04-194">Deploy to Azure</span></span>
<span data-ttu-id="0ba04-195">Para disparar uma implantação, clique em **Sincronização** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="0ba04-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="0ba04-196">A opção Sincronização faz um envio por push e a extração.</span><span class="sxs-lookup"><span data-stu-id="0ba04-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="0ba04-197">A primeira implantação levará algum tempo, pois isso criará um ambiente virtual, pacotes de instalação, etc.</span><span class="sxs-lookup"><span data-stu-id="0ba04-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="0ba04-198">O Visual Studio não mostra o progresso da implantação.</span><span class="sxs-lookup"><span data-stu-id="0ba04-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="0ba04-199">Se você quiser revisar a saída, consulte a seção sobre [Solução de problemas - Implantação](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="0ba04-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="0ba04-200">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="0ba04-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="0ba04-201">Desenvolvimento de aplicativos Web - Windows - linha de comando</span><span class="sxs-lookup"><span data-stu-id="0ba04-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="0ba04-202">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="0ba04-202">Clone the repository</span></span>
<span data-ttu-id="0ba04-203">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure e adicione o repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="0ba04-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="0ba04-204">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="0ba04-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="0ba04-205">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="0ba04-205">Create virtual environment</span></span>
<span data-ttu-id="0ba04-206">Criaremos um novo ambiente virtual para fins de desenvolvimento (não o adicione ao repositório).</span><span class="sxs-lookup"><span data-stu-id="0ba04-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="0ba04-207">Ambientes virtuais em Python não são relocáveis, portanto, todo desenvolvedor trabalhando no aplicativo criará seu próprio ambiente virtual localmente.</span><span class="sxs-lookup"><span data-stu-id="0ba04-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="0ba04-208">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha **Configurações do Aplicativo** de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="0ba04-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="0ba04-209">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="0ba04-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="0ba04-210">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="0ba04-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="0ba04-211">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-211">Install any external packages required by your application.</span></span> <span data-ttu-id="0ba04-212">Você pode usar o arquivo requirements.txt na raiz do repositório para instalar os pacotes no seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="0ba04-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="0ba04-213">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="0ba04-213">Run using development server</span></span>
<span data-ttu-id="0ba04-214">Você pode iniciar o aplicativo em um servidor de desenvolvimento com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0ba04-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="0ba04-215">O console exibirá a URL e a porta que o servidor escuta:</span><span class="sxs-lookup"><span data-stu-id="0ba04-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="0ba04-216">Em seguida, abra o navegador da Web para essa URL.</span><span class="sxs-lookup"><span data-stu-id="0ba04-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="0ba04-217">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="0ba04-217">Make changes</span></span>
<span data-ttu-id="0ba04-218">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0ba04-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="0ba04-219">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="0ba04-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="0ba04-220">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="0ba04-220">Install more packages</span></span>
<span data-ttu-id="0ba04-221">Seu aplicativo pode ter dependências além de Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="0ba04-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="0ba04-222">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="0ba04-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="0ba04-223">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="0ba04-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="0ba04-224">Certifique-se de atualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="0ba04-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="0ba04-225">Confirme as alterações:</span><span class="sxs-lookup"><span data-stu-id="0ba04-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="0ba04-226">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="0ba04-226">Deploy to Azure</span></span>
<span data-ttu-id="0ba04-227">Para disparar uma implantação, envie as alterações por push para o Azure:</span><span class="sxs-lookup"><span data-stu-id="0ba04-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="0ba04-228">Você verá a saída do script de implantação, incluindo a criação do ambiente virtual, instalação de pacotes, criação do web.config.</span><span class="sxs-lookup"><span data-stu-id="0ba04-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="0ba04-229">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="0ba04-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="0ba04-230">Desenvolvimento de aplicativos Web - Mac/Linux - linha de comando</span><span class="sxs-lookup"><span data-stu-id="0ba04-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="0ba04-231">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="0ba04-231">Clone the repository</span></span>
<span data-ttu-id="0ba04-232">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure e adicione o repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="0ba04-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="0ba04-233">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="0ba04-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="0ba04-234">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="0ba04-234">Create virtual environment</span></span>
<span data-ttu-id="0ba04-235">Criaremos um novo ambiente virtual para fins de desenvolvimento (não o adicione ao repositório).</span><span class="sxs-lookup"><span data-stu-id="0ba04-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="0ba04-236">Ambientes virtuais em Python não são relocáveis, portanto, todo desenvolvedor trabalhando no aplicativo criará seu próprio ambiente virtual localmente.</span><span class="sxs-lookup"><span data-stu-id="0ba04-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="0ba04-237">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha **Configurações do Aplicativo** de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="0ba04-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="0ba04-238">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="0ba04-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="0ba04-239">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="0ba04-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="0ba04-240">ou pyvenv env</span><span class="sxs-lookup"><span data-stu-id="0ba04-240">or pyvenv env</span></span>

<span data-ttu-id="0ba04-241">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba04-241">Install any external packages required by your application.</span></span> <span data-ttu-id="0ba04-242">Você pode usar o arquivo requirements.txt na raiz do repositório para instalar os pacotes no seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="0ba04-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="0ba04-243">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="0ba04-243">Run using development server</span></span>
<span data-ttu-id="0ba04-244">Você pode iniciar o aplicativo em um servidor de desenvolvimento com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0ba04-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="0ba04-245">O console exibirá a URL e a porta que o servidor escuta:</span><span class="sxs-lookup"><span data-stu-id="0ba04-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="0ba04-246">Em seguida, abra o navegador da Web para essa URL.</span><span class="sxs-lookup"><span data-stu-id="0ba04-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="0ba04-247">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="0ba04-247">Make changes</span></span>
<span data-ttu-id="0ba04-248">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0ba04-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="0ba04-249">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="0ba04-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="0ba04-250">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="0ba04-250">Install more packages</span></span>
<span data-ttu-id="0ba04-251">Seu aplicativo pode ter dependências além de Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="0ba04-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="0ba04-252">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="0ba04-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="0ba04-253">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="0ba04-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="0ba04-254">Certifique-se de atualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="0ba04-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="0ba04-255">Confirme as alterações:</span><span class="sxs-lookup"><span data-stu-id="0ba04-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="0ba04-256">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="0ba04-256">Deploy to Azure</span></span>
<span data-ttu-id="0ba04-257">Para disparar uma implantação, envie as alterações por push para o Azure:</span><span class="sxs-lookup"><span data-stu-id="0ba04-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="0ba04-258">Você verá a saída do script de implantação, incluindo a criação do ambiente virtual, instalação de pacotes, criação do web.config.</span><span class="sxs-lookup"><span data-stu-id="0ba04-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="0ba04-259">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="0ba04-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="0ba04-260">Solução de problemas - Instalação de pacotes</span><span class="sxs-lookup"><span data-stu-id="0ba04-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="0ba04-261">Solução de problemas - Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="0ba04-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="0ba04-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ba04-262">Next Steps</span></span>
<span data-ttu-id="0ba04-263">Siga esses links para saber mais sobre o Flask e Python Tools para o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="0ba04-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="0ba04-264">[Documentação do Flask]</span><span class="sxs-lookup"><span data-stu-id="0ba04-264">[Flask Documentation]</span></span>
* <span data-ttu-id="0ba04-265">[Ferramentas Python para Documentação]</span><span class="sxs-lookup"><span data-stu-id="0ba04-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="0ba04-266">Para obter informações sobre como usar o Armazenamento de Tabela do Azure e o MongoDB:</span><span class="sxs-lookup"><span data-stu-id="0ba04-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="0ba04-267">[Flask e MongoDB no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="0ba04-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="0ba04-268">[Flask e Armazenamento de Tabela do Azure no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="0ba04-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="0ba04-269">Para obter mais informações, consulte também o [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="0ba04-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="0ba04-270">O que mudou</span><span class="sxs-lookup"><span data-stu-id="0ba04-270">What's changed</span></span>
* <span data-ttu-id="0ba04-271">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0ba04-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="0ba04-272">[Flask e MongoDB no Azure com Ferramentas Python para Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="0ba04-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="0ba04-273">[Flask e Armazenamento de Tabela do Azure no Azure com Ferramentas Python para Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="0ba04-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="0ba04-274">[SDK do Azure para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="0ba04-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="0ba04-275">[SDK do Azure para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="0ba04-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="0ba04-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="0ba04-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="0ba04-277">[Git para Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="0ba04-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="0ba04-278">[GitHub para Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="0ba04-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="0ba04-279">[Python Tools para Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="0ba04-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="0ba04-280">[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="0ba04-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="0ba04-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="0ba04-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="0ba04-282">[Ferramentas Python para Documentação]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="0ba04-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="0ba04-283">[Documentação do Flask]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="0ba04-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

