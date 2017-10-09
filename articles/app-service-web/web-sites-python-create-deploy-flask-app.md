---
title: aplicativos web aaaCreating com bulbo no Azure
description: "Um tutorial que apresenta a você toorunning um aplicativo web do Python no Azure."
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
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="fe15b-103">Criando aplicativos Web com Flask no Azure</span><span class="sxs-lookup"><span data-stu-id="fe15b-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="fe15b-104">Este tutorial descreve como tooget iniciado Python em [aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="fe15b-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="fe15b-105">Os Aplicativos Web fornecem hospedagem gratuita limitada e implantação rápida, além permitirem a você usar o Python!</span><span class="sxs-lookup"><span data-stu-id="fe15b-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="fe15b-106">Como seu aplicativo cresce, você pode alternar a hospedagem de toopaid e você também pode integrar com todos os Olá outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe15b-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="fe15b-107">Você criará um aplicativo usando a estrutura de web do bulbo hello (consulte versões alternativas deste tutorial para [Django](web-sites-python-create-deploy-django-app.md) e [garrafa](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="fe15b-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="fe15b-108">Você criar o site de saudação do hello Galeria do Azure, configurar a implantação do Git e clonar Olá repositório localmente.</span><span class="sxs-lookup"><span data-stu-id="fe15b-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="fe15b-109">Em seguida, você executar o aplicativo hello localmente, fazer alterações, confirmar e enviá-las tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe15b-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="fe15b-110">Olá tutorial mostra como toodo isso do Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="fe15b-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="fe15b-111">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe15b-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fe15b-112">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="fe15b-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fe15b-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe15b-113">Prerequisites</span></span>
* <span data-ttu-id="fe15b-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="fe15b-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="fe15b-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="fe15b-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="fe15b-116">setuptools, pip, virtualenv (somente Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="fe15b-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="fe15b-117">Git</span><span class="sxs-lookup"><span data-stu-id="fe15b-117">Git</span></span>
* <span data-ttu-id="fe15b-118">PTVS ([Python Tools para Visual Studio][Python Tools para Visual Studio]) – Observação: isso é opcional</span><span class="sxs-lookup"><span data-stu-id="fe15b-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="fe15b-119">**Observação**: atualmente não há suporte à a publicação do TFS em projetos de Python.</span><span class="sxs-lookup"><span data-stu-id="fe15b-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="fe15b-120">Windows</span><span class="sxs-lookup"><span data-stu-id="fe15b-120">Windows</span></span>
<span data-ttu-id="fe15b-121">Caso você ainda não tenha o Python 2.7 ou 3.4 instalado (32 bits), recomendamos instalar o [SDK do Azure para Python 2.7] ou [SDK do Azure para Python 3.4] usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="fe15b-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="fe15b-122">Isso instala a versão de 32 bits de saudação do Python setuptools, pip, virtualenv, etc (Python de 32 bits é o que é instalado em computadores de host do Azure Olá).</span><span class="sxs-lookup"><span data-stu-id="fe15b-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="fe15b-123">Como alternativa, você pode obter o Python por meio de [python.org].</span><span class="sxs-lookup"><span data-stu-id="fe15b-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="fe15b-124">Para Git, recomendamos [Git para Windows] ou [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="fe15b-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="fe15b-125">Se você usar o Visual Studio, você pode usar o suporte de Git Olá integrado.</span><span class="sxs-lookup"><span data-stu-id="fe15b-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="fe15b-126">Também recomendamos a instalação das [Ferramentas Python 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="fe15b-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="fe15b-127">Isso é opcional, mas se você tiver [Visual Studio], incluindo Olá liberar o Visual Studio Community 2013 ou o Visual Studio Express 2013 para Web, e isso lhe dará um grande IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="fe15b-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="fe15b-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="fe15b-128">Mac/Linux</span></span>
<span data-ttu-id="fe15b-129">Você deve ter o Python e Git já instalados, mas certifique-se de ter uma das versões 2.7 ou 3.4 do Python.</span><span class="sxs-lookup"><span data-stu-id="fe15b-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="fe15b-130">Criar aplicativo Web em Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fe15b-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="fe15b-131">primeira etapa na criação de seu aplicativo Hello é toocreate Olá web aplicativo via Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe15b-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="fe15b-132">Faça logon no hello Portal do Azure e clique em Olá **novo** botão no canto do hello inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="fe15b-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="fe15b-133">Clique em **Web + móvel**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="fe15b-134">Na caixa de pesquisa hello, digite "python".</span><span class="sxs-lookup"><span data-stu-id="fe15b-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="fe15b-135">Nos resultados da pesquisa hello, selecione **bulbo**, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="fe15b-136">Configure o novo aplicativo de bulbo hello, como criar um novo plano de serviço de aplicativo e um novo grupo de recursos para ele.</span><span class="sxs-lookup"><span data-stu-id="fe15b-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="fe15b-137">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="fe15b-138">Configurar a publicação de Git para seu aplicativo web criado recentemente, seguindo as instruções de saudação em [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fe15b-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="fe15b-139">Visão geral do aplicativo</span><span class="sxs-lookup"><span data-stu-id="fe15b-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="fe15b-140">Conteúdos do repositório Git</span><span class="sxs-lookup"><span data-stu-id="fe15b-140">Git repository contents</span></span>
<span data-ttu-id="fe15b-141">Aqui está uma visão geral dos arquivos Olá que no repositório Git inicial Olá que podemos será clonar na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="fe15b-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="fe15b-142">Principais fontes para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fe15b-142">Main sources for hello application.</span></span>  <span data-ttu-id="fe15b-143">Consiste em 3 páginas (índice, sobre, contato) com um layout mestre.</span><span class="sxs-lookup"><span data-stu-id="fe15b-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="fe15b-144">Scripts e conteúdo estático incluem bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="fe15b-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="fe15b-145">Suporte ao servidor de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="fe15b-145">Local development server support.</span></span> <span data-ttu-id="fe15b-146">Use este aplicativo de saudação do toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="fe15b-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="fe15b-147">Arquivos de projeto para uso com [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="fe15b-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="fe15b-148">Proxy de IIS para ambientes virtuais e suporte à depuração remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="fe15b-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="fe15b-149">Pacotes externos requeridos por este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe15b-149">External packages needed by this application.</span></span> <span data-ttu-id="fe15b-150">script de implantação Hello serão pip instalar pacotes de saudação listados neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="fe15b-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="fe15b-151">Arquivos de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="fe15b-151">IIS configuration files.</span></span>  <span data-ttu-id="fe15b-152">script de implantação de saudação será usar web.x.y.config apropriado hello e copie-o como Web. config.</span><span class="sxs-lookup"><span data-stu-id="fe15b-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="fe15b-153">Arquivos opcionais - personalizando a implantação</span><span class="sxs-lookup"><span data-stu-id="fe15b-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="fe15b-154">Arquivos opcionais - tempo de execução do Python</span><span class="sxs-lookup"><span data-stu-id="fe15b-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="fe15b-155">Arquivos adicionais no servidor</span><span class="sxs-lookup"><span data-stu-id="fe15b-155">Additional files on server</span></span>
<span data-ttu-id="fe15b-156">Alguns arquivos existem no servidor de saudação, mas não são adicionados o repositório do git toohello.</span><span class="sxs-lookup"><span data-stu-id="fe15b-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="fe15b-157">Eles são criados pelo script de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe15b-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="fe15b-158">Arquivo de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="fe15b-158">IIS configuration file.</span></span>  <span data-ttu-id="fe15b-159">Criado por meio de web.x.y.config em toda implantação.</span><span class="sxs-lookup"><span data-stu-id="fe15b-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="fe15b-160">Ambiente virtual do Python.</span><span class="sxs-lookup"><span data-stu-id="fe15b-160">Python virtual environment.</span></span>  <span data-ttu-id="fe15b-161">Criado durante a implantação se um ambiente virtual compatível já não existe no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fe15b-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="fe15b-162">Os pacotes listados no requirements.txt são pip instalado, mas pip vai ignorar a instalação se Olá pacotes já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="fe15b-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="fe15b-163">Olá próximos 3 seções descrevem como tooproceed com Olá web desenvolvimento de aplicativo em 3 ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="fe15b-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="fe15b-164">Windows, com Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe15b-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="fe15b-165">Windows, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="fe15b-165">Windows, with command line</span></span>
* <span data-ttu-id="fe15b-166">Mac/Linux, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="fe15b-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="fe15b-167">Desenvolvimento de aplicativo Web - Windows - Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe15b-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="fe15b-168">Repositório de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="fe15b-168">Clone hello repository</span></span>
<span data-ttu-id="fe15b-169">Primeiro, clone o repositório de saudação usando Olá URL fornecida no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe15b-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="fe15b-170">Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fe15b-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="fe15b-171">Abra o arquivo de solução da saudação (. sln) que está incluído na raiz de saudação do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe15b-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="fe15b-172">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="fe15b-172">Create virtual environment</span></span>
<span data-ttu-id="fe15b-173">Agora vamos criar um ambiente virtual para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="fe15b-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="fe15b-174">Clique com o botão direito do mouse em **Ambientes Python** e selecione **Adicionar ambiente virtual...**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="fe15b-175">Certifique-se de nome de saudação do ambiente Olá é `env`.</span><span class="sxs-lookup"><span data-stu-id="fe15b-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="fe15b-176">Selecione o interpretador base hello.</span><span class="sxs-lookup"><span data-stu-id="fe15b-176">Select hello base interpreter.</span></span>  <span data-ttu-id="fe15b-177">Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (em runtime.txt ou Olá **configurações de aplicativo** folha do seu aplicativo web no hello Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="fe15b-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="fe15b-178">Certifique-se de saudação opção toodownload e instalar pacotes é verificada.</span><span class="sxs-lookup"><span data-stu-id="fe15b-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="fe15b-179">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-179">Click **Create**.</span></span>  <span data-ttu-id="fe15b-180">Isso será criar ambiente virtual hello e instalar dependências listadas em requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="fe15b-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="fe15b-181">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="fe15b-181">Run using development server</span></span>
<span data-ttu-id="fe15b-182">Pressione F5 toostart depuração e o navegador da web serão aberto automaticamente toohello página em execução localmente.</span><span class="sxs-lookup"><span data-stu-id="fe15b-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="fe15b-183">Você pode definir pontos de interrupção em fontes de hello, use Olá inspecionar windows, etc.  Consulte Olá [ferramentas Python para documentação do Visual Studio] para obter mais informações sobre Olá vários recursos.</span><span class="sxs-lookup"><span data-stu-id="fe15b-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="fe15b-184">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="fe15b-184">Make changes</span></span>
<span data-ttu-id="fe15b-185">Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="fe15b-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="fe15b-186">Depois de testar suas alterações, confirme repositório do Git toohello:</span><span class="sxs-lookup"><span data-stu-id="fe15b-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="fe15b-187">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="fe15b-187">Install more packages</span></span>
<span data-ttu-id="fe15b-188">Seu aplicativo pode ter dependências além de Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="fe15b-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="fe15b-189">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="fe15b-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="fe15b-190">tooinstall um pacote, clique com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="fe15b-191">Por exemplo, tooinstall hello Azure SDK para Python, que oferece acesso tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite `azure`:</span><span class="sxs-lookup"><span data-stu-id="fe15b-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="fe15b-192">Clique com botão direito no ambiente virtual hello e selecione **gerar requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="fe15b-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="fe15b-193">Em seguida, Olá confirmação altera o repositório do Git toohello toorequirements.txt.</span><span class="sxs-lookup"><span data-stu-id="fe15b-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="fe15b-194">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="fe15b-194">Deploy tooAzure</span></span>
<span data-ttu-id="fe15b-195">tootrigger uma implantação, clique em **sincronização** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="fe15b-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="fe15b-196">A opção Sincronização faz um envio por push e a extração.</span><span class="sxs-lookup"><span data-stu-id="fe15b-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="fe15b-197">implantação Olá levará algum tempo, pois ele cria um ambiente virtual, pacotes de instalação, etc.</span><span class="sxs-lookup"><span data-stu-id="fe15b-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="fe15b-198">O Visual Studio não mostra o progresso de saudação de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe15b-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="fe15b-199">Se desejar que a saída de hello tooreview, consulte a seção de saudação em [solução de problemas - implantação](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="fe15b-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="fe15b-200">Procure toohello URL do Azure tooview suas alterações.</span><span class="sxs-lookup"><span data-stu-id="fe15b-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="fe15b-201">Desenvolvimento de aplicativos Web - Windows - linha de comando</span><span class="sxs-lookup"><span data-stu-id="fe15b-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="fe15b-202">Repositório de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="fe15b-202">Clone hello repository</span></span>
<span data-ttu-id="fe15b-203">Primeiro, clonar repositório hello usando Olá URL fornecida no hello Portal do Azure e adicionar Olá repositório do Azure como um controle remoto.</span><span class="sxs-lookup"><span data-stu-id="fe15b-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="fe15b-204">Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fe15b-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="fe15b-205">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="fe15b-205">Create virtual environment</span></span>
<span data-ttu-id="fe15b-206">Vamos criar um novo ambiente virtual para fins de desenvolvimento (não adicioná-lo toohello repositório).</span><span class="sxs-lookup"><span data-stu-id="fe15b-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="fe15b-207">Ambientes virtuais no Python não são relocáveis, portanto, todos os desenvolvedores trabalhando em um aplicativo hello vai criar seus próprios localmente.</span><span class="sxs-lookup"><span data-stu-id="fe15b-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="fe15b-208">Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (em runtime.txt ou Olá **configurações de aplicativo** folha do seu aplicativo web no hello Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="fe15b-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="fe15b-209">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="fe15b-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="fe15b-210">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="fe15b-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="fe15b-211">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe15b-211">Install any external packages required by your application.</span></span> <span data-ttu-id="fe15b-212">Você pode usar o arquivo de requirements.txt de saudação na raiz de saudação de pacotes de saudação do hello repositório tooinstall em seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="fe15b-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="fe15b-213">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="fe15b-213">Run using development server</span></span>
<span data-ttu-id="fe15b-214">Você pode iniciar o aplicativo hello em um servidor de desenvolvimento com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe15b-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="fe15b-215">console Olá exibirá a URL de saudação e servidor de saudação porta escuta:</span><span class="sxs-lookup"><span data-stu-id="fe15b-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="fe15b-216">Em seguida, abra a URL de toothat do navegador da web.</span><span class="sxs-lookup"><span data-stu-id="fe15b-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="fe15b-217">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="fe15b-217">Make changes</span></span>
<span data-ttu-id="fe15b-218">Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="fe15b-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="fe15b-219">Depois de testar suas alterações, confirme repositório do Git toohello:</span><span class="sxs-lookup"><span data-stu-id="fe15b-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="fe15b-220">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="fe15b-220">Install more packages</span></span>
<span data-ttu-id="fe15b-221">Seu aplicativo pode ter dependências além de Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="fe15b-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="fe15b-222">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="fe15b-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="fe15b-223">Por exemplo, tooinstall hello Azure SDK para Python, que dá a você acessar tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="fe15b-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="fe15b-224">Certifique-se de que requirements.txt de tooupdate:</span><span class="sxs-lookup"><span data-stu-id="fe15b-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="fe15b-225">Confirme as alterações de saudação:</span><span class="sxs-lookup"><span data-stu-id="fe15b-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="fe15b-226">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="fe15b-226">Deploy tooAzure</span></span>
<span data-ttu-id="fe15b-227">tootrigger uma implantação, Olá push altera tooAzure:</span><span class="sxs-lookup"><span data-stu-id="fe15b-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="fe15b-228">Você verá uma saída Olá Olá do script de implantação, incluindo a criação do ambiente virtual, a instalação de pacotes, criação de Web. config.</span><span class="sxs-lookup"><span data-stu-id="fe15b-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="fe15b-229">Procure toohello URL do Azure tooview suas alterações.</span><span class="sxs-lookup"><span data-stu-id="fe15b-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="fe15b-230">Desenvolvimento de aplicativos Web - Mac/Linux - linha de comando</span><span class="sxs-lookup"><span data-stu-id="fe15b-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="fe15b-231">Repositório de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="fe15b-231">Clone hello repository</span></span>
<span data-ttu-id="fe15b-232">Primeiro, clonar repositório hello usando Olá URL fornecida no hello Portal do Azure e adicionar Olá repositório do Azure como um controle remoto.</span><span class="sxs-lookup"><span data-stu-id="fe15b-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="fe15b-233">Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fe15b-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="fe15b-234">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="fe15b-234">Create virtual environment</span></span>
<span data-ttu-id="fe15b-235">Vamos criar um novo ambiente virtual para fins de desenvolvimento (não adicioná-lo toohello repositório).</span><span class="sxs-lookup"><span data-stu-id="fe15b-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="fe15b-236">Ambientes virtuais no Python não são relocáveis, portanto, todos os desenvolvedores trabalhando em um aplicativo hello vai criar seus próprios localmente.</span><span class="sxs-lookup"><span data-stu-id="fe15b-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="fe15b-237">Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (em runtime.txt ou Olá **configurações de aplicativo** folha do seu aplicativo web no hello Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="fe15b-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="fe15b-238">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="fe15b-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="fe15b-239">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="fe15b-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="fe15b-240">ou pyvenv env</span><span class="sxs-lookup"><span data-stu-id="fe15b-240">or pyvenv env</span></span>

<span data-ttu-id="fe15b-241">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe15b-241">Install any external packages required by your application.</span></span> <span data-ttu-id="fe15b-242">Você pode usar o arquivo de requirements.txt de saudação na raiz de saudação de pacotes de saudação do hello repositório tooinstall em seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="fe15b-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="fe15b-243">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="fe15b-243">Run using development server</span></span>
<span data-ttu-id="fe15b-244">Você pode iniciar o aplicativo hello em um servidor de desenvolvimento com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe15b-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="fe15b-245">console Olá exibirá a URL de saudação e servidor de saudação porta escuta:</span><span class="sxs-lookup"><span data-stu-id="fe15b-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="fe15b-246">Em seguida, abra a URL de toothat do navegador da web.</span><span class="sxs-lookup"><span data-stu-id="fe15b-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="fe15b-247">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="fe15b-247">Make changes</span></span>
<span data-ttu-id="fe15b-248">Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="fe15b-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="fe15b-249">Depois de testar suas alterações, confirme repositório do Git toohello:</span><span class="sxs-lookup"><span data-stu-id="fe15b-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="fe15b-250">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="fe15b-250">Install more packages</span></span>
<span data-ttu-id="fe15b-251">Seu aplicativo pode ter dependências além de Python e Flask.</span><span class="sxs-lookup"><span data-stu-id="fe15b-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="fe15b-252">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="fe15b-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="fe15b-253">Por exemplo, tooinstall hello Azure SDK para Python, que dá a você acessar tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="fe15b-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="fe15b-254">Certifique-se de que requirements.txt de tooupdate:</span><span class="sxs-lookup"><span data-stu-id="fe15b-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="fe15b-255">Confirme as alterações de saudação:</span><span class="sxs-lookup"><span data-stu-id="fe15b-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="fe15b-256">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="fe15b-256">Deploy tooAzure</span></span>
<span data-ttu-id="fe15b-257">tootrigger uma implantação, Olá push altera tooAzure:</span><span class="sxs-lookup"><span data-stu-id="fe15b-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="fe15b-258">Você verá uma saída Olá Olá do script de implantação, incluindo a criação do ambiente virtual, a instalação de pacotes, criação de Web. config.</span><span class="sxs-lookup"><span data-stu-id="fe15b-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="fe15b-259">Procure toohello URL do Azure tooview suas alterações.</span><span class="sxs-lookup"><span data-stu-id="fe15b-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="fe15b-260">Solução de problemas - Instalação de pacotes</span><span class="sxs-lookup"><span data-stu-id="fe15b-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="fe15b-261">Solução de problemas - Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="fe15b-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="fe15b-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe15b-262">Next Steps</span></span>
<span data-ttu-id="fe15b-263">Siga essas toolearn links mais sobre bulbo e as ferramentas Python para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="fe15b-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="fe15b-264">[Documentação do Flask]</span><span class="sxs-lookup"><span data-stu-id="fe15b-264">[Flask Documentation]</span></span>
* <span data-ttu-id="fe15b-265">[ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="fe15b-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="fe15b-266">Para obter informações sobre como usar o Armazenamento de Tabela do Azure e o MongoDB:</span><span class="sxs-lookup"><span data-stu-id="fe15b-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="fe15b-267">[Flask e MongoDB no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="fe15b-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="fe15b-268">[Flask e Armazenamento de Tabela do Azure no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="fe15b-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="fe15b-269">Para obter mais informações, consulte também Olá [Central de desenvolvedores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="fe15b-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="fe15b-270">O que mudou</span><span class="sxs-lookup"><span data-stu-id="fe15b-270">What's changed</span></span>
* <span data-ttu-id="fe15b-271">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="fe15b-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask e MongoDB no Azure com Ferramentas Python para Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask e Armazenamento de Tabela do Azure no Azure com Ferramentas Python para Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[SDK do Azure para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[SDK do Azure para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do Flask]: http://flask.pocoo.org/ 

