---
title: Aplicativos Web do Python com Bottle no Azure
description: "Um tutorial que apresenta a execução de um aplicativo Web do Python em aplicativos Web do Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="8100f-103">Criando aplicativos Web com Bottle no Azure</span><span class="sxs-lookup"><span data-stu-id="8100f-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="8100f-104">Este tutorial descreve como começar a execução de Python em Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="8100f-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="8100f-105">Os Aplicativos Web fornecem hospedagem gratuita limitada e implantação rápida, além permitirem a você usar o Python!</span><span class="sxs-lookup"><span data-stu-id="8100f-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="8100f-106">Conforme o aplicativo cresce, você pode alternar para hospedagem paga e também integrar-se com todos os outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="8100f-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="8100f-107">Você criará um aplicativo Web usando a estrutura da Web Bottle (veja as versões alternativas deste tutorial para [Django](web-sites-python-create-deploy-django-app.md) e [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="8100f-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="8100f-108">Você criará o aplicativo Web no Azure Marketplace, configurará a implantação do Git e clonará o repositório localmente.</span><span class="sxs-lookup"><span data-stu-id="8100f-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="8100f-109">Em seguida, você vai executar o aplicativo localmente, fazer alterações, confirmá-las e enviá-las por push para os [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="8100f-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="8100f-110">O tutorial mostra como fazer isso por meio do Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="8100f-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="8100f-111">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8100f-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8100f-112">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="8100f-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8100f-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8100f-113">Prerequisites</span></span>
* <span data-ttu-id="8100f-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="8100f-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="8100f-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="8100f-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="8100f-116">setuptools, pip, virtualenv (somente Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="8100f-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="8100f-117">Git</span><span class="sxs-lookup"><span data-stu-id="8100f-117">Git</span></span>
* <span data-ttu-id="8100f-118">[Ferramentas Python 2.2 para Visual Studio][Ferramentas Python 2.2 para Visual Studio] (PTVS) — Observação: isso é opcional</span><span class="sxs-lookup"><span data-stu-id="8100f-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="8100f-119">**Observação**: atualmente não há suporte à a publicação do TFS em projetos de Python.</span><span class="sxs-lookup"><span data-stu-id="8100f-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="8100f-120">Windows</span><span class="sxs-lookup"><span data-stu-id="8100f-120">Windows</span></span>
<span data-ttu-id="8100f-121">Caso você ainda não tenha o Python 2.7 ou 3.4 instalado (32 bits), recomendamos instalar o [SDK do Azure para Python 2.7] ou [SDK do Azure para Python 3.4] usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="8100f-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="8100f-122">Isso instala a versão de 32 bits do Python, setuptools, pip, virtualenv, etc (Python de 32 bits é o que está instalado nos computadores host do Azure).</span><span class="sxs-lookup"><span data-stu-id="8100f-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="8100f-123">Como alternativa, você pode obter o Python por meio de [python.org].</span><span class="sxs-lookup"><span data-stu-id="8100f-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="8100f-124">Para Git, recomendamos [Git para Windows] ou [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="8100f-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="8100f-125">Se você usar o Visual Studio, você pode usar o suporte integrado a Git.</span><span class="sxs-lookup"><span data-stu-id="8100f-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="8100f-126">Também recomendamos a instalação das [Ferramentas Python 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="8100f-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="8100f-127">Isso é opcional, mas se você tiver o [Visual Studio], incluindo o Visual Studio Community 2013 ou o Visual Studio Express 2013 para Web gratuitos, isso lhe dará um excelente IDE (ambiente de desenvolvimento integrado) do Python.</span><span class="sxs-lookup"><span data-stu-id="8100f-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="8100f-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="8100f-128">Mac/Linux</span></span>
<span data-ttu-id="8100f-129">Você deve ter o Python e Git já instalados, mas certifique-se de ter uma das versões 2.7 ou 3.4 do Python.</span><span class="sxs-lookup"><span data-stu-id="8100f-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="8100f-130">Criação de aplicativo Web no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8100f-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="8100f-131">A primeira etapa na criação de seu aplicativo é criar o aplicativo Web por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8100f-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="8100f-132">Faça logon no Portal do Azure e clique no botão **Novo** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="8100f-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="8100f-133">Na caixa de pesquisa, digite "python".</span><span class="sxs-lookup"><span data-stu-id="8100f-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="8100f-134">Nos resultados da pesquisa, selecione **Bottle** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8100f-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="8100f-135">Configure o novo aplicativo Bottle, como a criação de um novo plano de Serviço de Aplicativo e um novo grupo de recursos para ele.</span><span class="sxs-lookup"><span data-stu-id="8100f-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="8100f-136">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8100f-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="8100f-137">Configure a publicação de Git para seu aplicativo Web recém-criado seguindo as instruções em [Implantação de GIT local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="8100f-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="8100f-138">Visão geral do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8100f-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="8100f-139">Conteúdos do repositório Git</span><span class="sxs-lookup"><span data-stu-id="8100f-139">Git repository contents</span></span>
<span data-ttu-id="8100f-140">Eis aqui uma visão geral dos arquivos que você encontrará no repositório Git inicial, o qual iremos clonar na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="8100f-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="8100f-141">Fontes principais para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8100f-141">Main sources for the application.</span></span> <span data-ttu-id="8100f-142">Consiste em 3 páginas (índice, sobre, contato) com um layout mestre.</span><span class="sxs-lookup"><span data-stu-id="8100f-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="8100f-143">Scripts e conteúdo estático incluem bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="8100f-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="8100f-144">Suporte ao servidor de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="8100f-144">Local development server support.</span></span> <span data-ttu-id="8100f-145">Use esta opção para executar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="8100f-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="8100f-146">Arquivos de projeto para uso com [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="8100f-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="8100f-147">Proxy de IIS para ambientes virtuais e suporte à depuração remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="8100f-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="8100f-148">Pacotes externos requeridos por este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8100f-148">External packages needed by this application.</span></span> <span data-ttu-id="8100f-149">O script de implantação fará a instalação por pip dos pacotes listados nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="8100f-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="8100f-150">Arquivos de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="8100f-150">IIS configuration files.</span></span> <span data-ttu-id="8100f-151">O script de implantação usará o web.x.y.config apropriado e o copiará como web.config.</span><span class="sxs-lookup"><span data-stu-id="8100f-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="8100f-152">Arquivos opcionais - personalizando a implantação</span><span class="sxs-lookup"><span data-stu-id="8100f-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="8100f-153">Arquivos opcionais - tempo de execução do Python</span><span class="sxs-lookup"><span data-stu-id="8100f-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="8100f-154">Arquivos adicionais no servidor</span><span class="sxs-lookup"><span data-stu-id="8100f-154">Additional files on server</span></span>
<span data-ttu-id="8100f-155">Alguns arquivos existem no servidor, mas não são adicionados ao repositório git.</span><span class="sxs-lookup"><span data-stu-id="8100f-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="8100f-156">Eles são criados pelo script de implantação.</span><span class="sxs-lookup"><span data-stu-id="8100f-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="8100f-157">Arquivo de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="8100f-157">IIS configuration file.</span></span> <span data-ttu-id="8100f-158">Criado por meio de web.x.y.config em toda implantação.</span><span class="sxs-lookup"><span data-stu-id="8100f-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="8100f-159">Ambiente virtual do Python.</span><span class="sxs-lookup"><span data-stu-id="8100f-159">Python virtual environment.</span></span> <span data-ttu-id="8100f-160">Criado durante a implantação, se ainda não existir um ambiente virtual compatível no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8100f-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="8100f-161">Pacotes listados em requirements.txt são instalados por pip, mas o pip ignorará a instalação se os pacotes já estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="8100f-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="8100f-162">As próximas três seções descrevem como prosseguir com o desenvolvimento de aplicativo Web em três ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="8100f-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="8100f-163">Windows, com Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8100f-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="8100f-164">Windows, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="8100f-164">Windows, with command line</span></span>
* <span data-ttu-id="8100f-165">Mac/Linux, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="8100f-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="8100f-166">Desenvolvimento de aplicativo Web - Windows - Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8100f-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="8100f-167">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="8100f-167">Clone the repository</span></span>
<span data-ttu-id="8100f-168">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8100f-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="8100f-169">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="8100f-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="8100f-170">Abra o arquivo da solução (.sln) que está incluído na raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="8100f-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="8100f-171">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="8100f-171">Create virtual environment</span></span>
<span data-ttu-id="8100f-172">Agora vamos criar um ambiente virtual para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="8100f-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="8100f-173">Clique com o botão direito do mouse em **Ambientes Python** e selecione **Adicionar ambiente virtual...**.</span><span class="sxs-lookup"><span data-stu-id="8100f-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="8100f-174">Verifique se o nome do ambiente é `env`.</span><span class="sxs-lookup"><span data-stu-id="8100f-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="8100f-175">Selecione o interpretador de base.</span><span class="sxs-lookup"><span data-stu-id="8100f-175">Select the base interpreter.</span></span> <span data-ttu-id="8100f-176">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha **Configurações do Aplicativo** de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="8100f-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="8100f-177">Verifique se a opção para baixar e instalar pacotes está marcada.</span><span class="sxs-lookup"><span data-stu-id="8100f-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="8100f-178">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8100f-178">Click **Create**.</span></span> <span data-ttu-id="8100f-179">Isso criará o ambiente virtual e instalar dependências listadas em requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="8100f-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="8100f-180">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="8100f-180">Run using development server</span></span>
<span data-ttu-id="8100f-181">Pressione F5 para iniciar a depuração e o navegador da Web abrirá automaticamente na página sendo executada localmente.</span><span class="sxs-lookup"><span data-stu-id="8100f-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="8100f-182">Você pode definir pontos de interrupção nas fontes, usar as janelas de observação etc. Consulte [Ferramentas Python para Documentação] do Visual Studio para obter mais informações sobre os vários recursos.</span><span class="sxs-lookup"><span data-stu-id="8100f-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="8100f-183">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="8100f-183">Make changes</span></span>
<span data-ttu-id="8100f-184">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8100f-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="8100f-185">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="8100f-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="8100f-186">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="8100f-186">Install more packages</span></span>
<span data-ttu-id="8100f-187">Seu aplicativo pode ter dependências além de Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="8100f-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="8100f-188">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="8100f-188">You can install additional packages using pip.</span></span> <span data-ttu-id="8100f-189">Para instalar um pacote, clique no ambiente virtual e selecione **Instalar pacote Python**.</span><span class="sxs-lookup"><span data-stu-id="8100f-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="8100f-190">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite `azure`:</span><span class="sxs-lookup"><span data-stu-id="8100f-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="8100f-191">Clique com o botão direito do mouse em no ambiente virtual e selecione **Gerar requirements.txt** para atualizar requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="8100f-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="8100f-192">Em seguida, confirme as alterações a requirements.txt no repositório Git.</span><span class="sxs-lookup"><span data-stu-id="8100f-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="8100f-193">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="8100f-193">Deploy to Azure</span></span>
<span data-ttu-id="8100f-194">Para disparar uma implantação, clique em **Sincronização** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="8100f-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="8100f-195">A opção Sincronização faz um envio por push e a extração.</span><span class="sxs-lookup"><span data-stu-id="8100f-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="8100f-196">A primeira implantação levará algum tempo, pois isso criará um ambiente virtual, pacotes de instalação, etc.</span><span class="sxs-lookup"><span data-stu-id="8100f-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="8100f-197">O Visual Studio não mostra o progresso da implantação.</span><span class="sxs-lookup"><span data-stu-id="8100f-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="8100f-198">Se você quiser revisar a saída, consulte a seção sobre [Solução de problemas - Implantação](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="8100f-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="8100f-199">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="8100f-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="8100f-200">Desenvolvimento de aplicativos Web - Windows - linha de comando</span><span class="sxs-lookup"><span data-stu-id="8100f-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="8100f-201">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="8100f-201">Clone the repository</span></span>
<span data-ttu-id="8100f-202">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure e adicione o repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="8100f-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="8100f-203">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="8100f-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="8100f-204">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="8100f-204">Create virtual environment</span></span>
<span data-ttu-id="8100f-205">Criaremos um novo ambiente virtual para fins de desenvolvimento (não o adicione ao repositório).</span><span class="sxs-lookup"><span data-stu-id="8100f-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="8100f-206">Ambientes virtuais em Python não são relocáveis, portanto, todo desenvolvedor trabalhando no aplicativo criará seu próprio ambiente virtual localmente.</span><span class="sxs-lookup"><span data-stu-id="8100f-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="8100f-207">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha Configurações do Aplicativo de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="8100f-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="8100f-208">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="8100f-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="8100f-209">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="8100f-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="8100f-210">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8100f-210">Install any external packages required by your application.</span></span> <span data-ttu-id="8100f-211">Você pode usar o arquivo requirements.txt na raiz do repositório para instalar os pacotes no seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="8100f-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="8100f-212">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="8100f-212">Run using development server</span></span>
<span data-ttu-id="8100f-213">Você pode iniciar o aplicativo em um servidor de desenvolvimento com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8100f-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="8100f-214">O console exibirá a URL e a porta que o servidor escuta:</span><span class="sxs-lookup"><span data-stu-id="8100f-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="8100f-215">Em seguida, abra o navegador da Web para essa URL.</span><span class="sxs-lookup"><span data-stu-id="8100f-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="8100f-216">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="8100f-216">Make changes</span></span>
<span data-ttu-id="8100f-217">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8100f-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="8100f-218">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="8100f-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="8100f-219">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="8100f-219">Install more packages</span></span>
<span data-ttu-id="8100f-220">Seu aplicativo pode ter dependências além de Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="8100f-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="8100f-221">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="8100f-221">You can install additional packages using pip.</span></span> <span data-ttu-id="8100f-222">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="8100f-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="8100f-223">Certifique-se de atualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="8100f-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="8100f-224">Confirme as alterações:</span><span class="sxs-lookup"><span data-stu-id="8100f-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="8100f-225">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="8100f-225">Deploy to Azure</span></span>
<span data-ttu-id="8100f-226">Para disparar uma implantação, envie as alterações por push para o Azure:</span><span class="sxs-lookup"><span data-stu-id="8100f-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="8100f-227">Você verá a saída do script de implantação, incluindo a criação do ambiente virtual, instalação de pacotes, criação do web.config.</span><span class="sxs-lookup"><span data-stu-id="8100f-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="8100f-228">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="8100f-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="8100f-229">Desenvolvimento de aplicativos Web - Mac/Linux - linha de comando</span><span class="sxs-lookup"><span data-stu-id="8100f-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="8100f-230">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="8100f-230">Clone the repository</span></span>
<span data-ttu-id="8100f-231">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure e adicione o repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="8100f-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="8100f-232">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="8100f-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="8100f-233">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="8100f-233">Create virtual environment</span></span>
<span data-ttu-id="8100f-234">Criaremos um novo ambiente virtual para fins de desenvolvimento (não o adicione ao repositório).</span><span class="sxs-lookup"><span data-stu-id="8100f-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="8100f-235">Ambientes virtuais em Python não são relocáveis, portanto, todo desenvolvedor trabalhando no aplicativo criará seu próprio ambiente virtual localmente.</span><span class="sxs-lookup"><span data-stu-id="8100f-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="8100f-236">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha Configurações do Aplicativo de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="8100f-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="8100f-237">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="8100f-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="8100f-238">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="8100f-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="8100f-239">ou pyvenv env</span><span class="sxs-lookup"><span data-stu-id="8100f-239">or pyvenv env</span></span>

<span data-ttu-id="8100f-240">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8100f-240">Install any external packages required by your application.</span></span> <span data-ttu-id="8100f-241">Você pode usar o arquivo requirements.txt na raiz do repositório para instalar os pacotes no seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="8100f-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="8100f-242">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="8100f-242">Run using development server</span></span>
<span data-ttu-id="8100f-243">Você pode iniciar o aplicativo em um servidor de desenvolvimento com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8100f-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="8100f-244">O console exibirá a URL e a porta que o servidor escuta:</span><span class="sxs-lookup"><span data-stu-id="8100f-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="8100f-245">Em seguida, abra o navegador da Web para essa URL.</span><span class="sxs-lookup"><span data-stu-id="8100f-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="8100f-246">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="8100f-246">Make changes</span></span>
<span data-ttu-id="8100f-247">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8100f-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="8100f-248">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="8100f-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="8100f-249">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="8100f-249">Install more packages</span></span>
<span data-ttu-id="8100f-250">Seu aplicativo pode ter dependências além de Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="8100f-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="8100f-251">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="8100f-251">You can install additional packages using pip.</span></span> <span data-ttu-id="8100f-252">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="8100f-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="8100f-253">Certifique-se de atualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="8100f-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="8100f-254">Confirme as alterações:</span><span class="sxs-lookup"><span data-stu-id="8100f-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="8100f-255">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="8100f-255">Deploy to Azure</span></span>
<span data-ttu-id="8100f-256">Para disparar uma implantação, envie as alterações por push para o Azure:</span><span class="sxs-lookup"><span data-stu-id="8100f-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="8100f-257">Você verá a saída do script de implantação, incluindo a criação do ambiente virtual, instalação de pacotes, criação do web.config.</span><span class="sxs-lookup"><span data-stu-id="8100f-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="8100f-258">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="8100f-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="8100f-259">Solução de problemas - Instalação de pacotes</span><span class="sxs-lookup"><span data-stu-id="8100f-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="8100f-260">Solução de problemas - Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="8100f-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="8100f-261">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8100f-261">Next Steps</span></span>
<span data-ttu-id="8100f-262">Siga esses links para saber mais sobre Bottle e Python Tools para o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="8100f-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="8100f-263">[Documentação do Bottle]</span><span class="sxs-lookup"><span data-stu-id="8100f-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="8100f-264">[Ferramentas Python para Documentação]</span><span class="sxs-lookup"><span data-stu-id="8100f-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="8100f-265">Para obter informações sobre como usar o Armazenamento de Tabela do Azure e o MongoDB:</span><span class="sxs-lookup"><span data-stu-id="8100f-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="8100f-266">[Bottle e MongoDB no Azure com Ferramentas Python 2.1 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8100f-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="8100f-267">[Bottle e Armazenamento de Tabela do Azure com Ferramentas Python 2.1 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8100f-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8100f-268">O que mudou</span><span class="sxs-lookup"><span data-stu-id="8100f-268">What's changed</span></span>
* <span data-ttu-id="8100f-269">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8100f-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="8100f-270">[Bottle e MongoDB no Azure com Ferramentas Python 2.1 para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="8100f-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="8100f-271">[Bottle e Armazenamento de Tabela do Azure com Ferramentas Python 2.1 para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="8100f-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="8100f-272">[SDK do Azure para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="8100f-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="8100f-273">[SDK do Azure para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="8100f-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="8100f-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="8100f-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="8100f-275">[Git para Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="8100f-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="8100f-276">[GitHub para Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="8100f-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="8100f-277">[Python Tools para Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="8100f-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="8100f-278">[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="8100f-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="8100f-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="8100f-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="8100f-280">[Ferramentas Python para Documentação]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="8100f-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="8100f-281">[Documentação do Bottle]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="8100f-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

