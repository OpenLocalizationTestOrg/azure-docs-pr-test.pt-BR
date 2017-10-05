---
title: Criando aplicativos Web com Django no Azure
description: "Um tutorial que apresenta a execução de um aplicativo Web do Python em aplicativos Web do Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="9547f-103">Criando aplicativos Web com Django no Azure</span><span class="sxs-lookup"><span data-stu-id="9547f-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="9547f-104">Este tutorial descreve como começar a execução de Python em [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="9547f-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="9547f-105">Os Aplicativos Web fornecem hospedagem gratuita limitada e implantação rápida, além permitirem a você usar o Python!</span><span class="sxs-lookup"><span data-stu-id="9547f-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="9547f-106">Conforme o aplicativo cresce, você pode alternar para hospedagem paga e também integrar-se com todos os outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="9547f-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="9547f-107">Você criará um aplicativo usando a estrutura da Web Django (consulte versões alternativas deste tutorial para [Flask](web-sites-python-create-deploy-flask-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="9547f-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="9547f-108">Você criará o aplicativo Web no Azure Marketplace, configurará a implantação do Git e clonará o repositório localmente.</span><span class="sxs-lookup"><span data-stu-id="9547f-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="9547f-109">Em seguida, você executará o aplicativo localmente, fazer alterações, confirmá-las e enviá-las por push para o Azure.</span><span class="sxs-lookup"><span data-stu-id="9547f-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="9547f-110">O tutorial mostra como fazer isso por meio do Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="9547f-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="9547f-111">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9547f-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9547f-112">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="9547f-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9547f-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9547f-113">Prerequisites</span></span>
* <span data-ttu-id="9547f-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="9547f-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="9547f-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="9547f-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="9547f-116">setuptools, pip, virtualenv (somente Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="9547f-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="9547f-117">Git</span><span class="sxs-lookup"><span data-stu-id="9547f-117">Git</span></span>
* <span data-ttu-id="9547f-118">PTVS ([Python Tools para Visual Studio][Python Tools para Visual Studio]) – Observação: isso é opcional</span><span class="sxs-lookup"><span data-stu-id="9547f-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="9547f-119">**Observação**: atualmente não há suporte à a publicação do TFS em projetos de Python.</span><span class="sxs-lookup"><span data-stu-id="9547f-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="9547f-120">Windows</span><span class="sxs-lookup"><span data-stu-id="9547f-120">Windows</span></span>
<span data-ttu-id="9547f-121">Caso você ainda não tenha o Python 2.7 ou 3.4 instalado (32 bits), recomendamos instalar o [SDK do Azure para Python 2.7] ou [SDK do Azure para Python 3.4] usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="9547f-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="9547f-122">Isso instala a versão de 32 bits do Python, setuptools, pip, virtualenv, etc (Python de 32 bits é o que está instalado nos computadores host do Azure).</span><span class="sxs-lookup"><span data-stu-id="9547f-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="9547f-123">Como alternativa, você pode obter o Python por meio de [python.org].</span><span class="sxs-lookup"><span data-stu-id="9547f-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="9547f-124">Para Git, recomendamos [Git para Windows] ou [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="9547f-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="9547f-125">Se você usar o Visual Studio, você pode usar o suporte integrado a Git.</span><span class="sxs-lookup"><span data-stu-id="9547f-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="9547f-126">Também recomendamos a instalação das [Ferramentas Python 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="9547f-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="9547f-127">Isso é opcional, mas se você tiver o [Visual Studio], incluindo o Visual Studio Community 2013 ou o Visual Studio Express 2013 para Web gratuitos, isso lhe dará um excelente IDE (ambiente de desenvolvimento integrado) do Python.</span><span class="sxs-lookup"><span data-stu-id="9547f-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="9547f-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="9547f-128">Mac/Linux</span></span>
<span data-ttu-id="9547f-129">Você deve ter o Python e Git já instalados, mas certifique-se de ter uma das versões 2.7 ou 3.4 do Python.</span><span class="sxs-lookup"><span data-stu-id="9547f-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="9547f-130">Criação de aplicativos Web no Portal</span><span class="sxs-lookup"><span data-stu-id="9547f-130">Web App Creation on Portal</span></span>
<span data-ttu-id="9547f-131">A primeira etapa na criação de seu aplicativo é criar o aplicativo Web por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9547f-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="9547f-132">Faça logon no Portal do Azure e clique no botão **Novo** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="9547f-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="9547f-133">Na caixa de pesquisa, digite "python".</span><span class="sxs-lookup"><span data-stu-id="9547f-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="9547f-134">Nos resultados da pesquisa, selecione **Django** (publicado pelo PTVS) e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9547f-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="9547f-135">Configure o novo aplicativo Django, como a criação de um novo plano de Serviço de Aplicativo e um novo grupo de recursos para ele.</span><span class="sxs-lookup"><span data-stu-id="9547f-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="9547f-136">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9547f-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="9547f-137">Configure a publicação de Git para seu aplicativo Web recém-criado seguindo as instruções em [Implantação de GIT local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="9547f-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="9547f-138">Visão geral do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9547f-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="9547f-139">Conteúdos do repositório Git</span><span class="sxs-lookup"><span data-stu-id="9547f-139">Git repository contents</span></span>
<span data-ttu-id="9547f-140">Eis aqui uma visão geral dos arquivos que você encontrará no repositório Git inicial, o qual iremos clonar na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="9547f-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="9547f-141">Fontes principais para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9547f-141">Main sources for the application.</span></span> <span data-ttu-id="9547f-142">Consiste em 3 páginas (índice, sobre, contato) com um layout mestre.</span><span class="sxs-lookup"><span data-stu-id="9547f-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="9547f-143">Scripts e conteúdo estático incluem bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="9547f-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="9547f-144">Gerenciamento local e suporte ao servidor de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9547f-144">Local management and development server support.</span></span> <span data-ttu-id="9547f-145">Use isto para executar o aplicativo localmente, sincronizar o banco de dados, etc.</span><span class="sxs-lookup"><span data-stu-id="9547f-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="9547f-146">Banco de dados padrão.</span><span class="sxs-lookup"><span data-stu-id="9547f-146">Default database.</span></span> <span data-ttu-id="9547f-147">Inclui as tabelas necessárias para que o aplicativo seja executado, mas não contém nenhum usuário (sincronize o banco de dados para criar um usuário).</span><span class="sxs-lookup"><span data-stu-id="9547f-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="9547f-148">Arquivos de projeto para uso com [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="9547f-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="9547f-149">Proxy de IIS para ambientes virtuais e suporte à depuração remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="9547f-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="9547f-150">Pacotes externos requeridos por este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9547f-150">External packages needed by this application.</span></span> <span data-ttu-id="9547f-151">O script de implantação fará a instalação por pip dos pacotes listados nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="9547f-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="9547f-152">Arquivos de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="9547f-152">IIS configuration files.</span></span> <span data-ttu-id="9547f-153">O script de implantação usará o web.x.y.config apropriado e o copiará como web.config.</span><span class="sxs-lookup"><span data-stu-id="9547f-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="9547f-154">Arquivos opcionais - personalizando a implantação</span><span class="sxs-lookup"><span data-stu-id="9547f-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="9547f-155">Arquivos opcionais - tempo de execução do Python</span><span class="sxs-lookup"><span data-stu-id="9547f-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="9547f-156">Arquivos adicionais no servidor</span><span class="sxs-lookup"><span data-stu-id="9547f-156">Additional files on server</span></span>
<span data-ttu-id="9547f-157">Alguns arquivos existem no servidor, mas não são adicionados ao repositório git.</span><span class="sxs-lookup"><span data-stu-id="9547f-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="9547f-158">Eles são criados pelo script de implantação.</span><span class="sxs-lookup"><span data-stu-id="9547f-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="9547f-159">Arquivo de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="9547f-159">IIS configuration file.</span></span> <span data-ttu-id="9547f-160">Criado por meio de web.x.y.config em toda implantação.</span><span class="sxs-lookup"><span data-stu-id="9547f-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="9547f-161">Ambiente virtual do Python.</span><span class="sxs-lookup"><span data-stu-id="9547f-161">Python virtual environment.</span></span> <span data-ttu-id="9547f-162">Criado durante a implantação, se ainda não existir um ambiente virtual compatível no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9547f-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="9547f-163">Pacotes listados em requirements.txt são instalados por pip, mas o pip ignorará a instalação se os pacotes já estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="9547f-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="9547f-164">As próximas três seções descrevem como prosseguir com o desenvolvimento de aplicativo Web em três ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="9547f-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="9547f-165">Windows, com Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9547f-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="9547f-166">Windows, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="9547f-166">Windows, with command line</span></span>
* <span data-ttu-id="9547f-167">Mac/Linux, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="9547f-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="9547f-168">Desenvolvimento de aplicativo Web - Windows - Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9547f-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="9547f-169">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="9547f-169">Clone the repository</span></span>
<span data-ttu-id="9547f-170">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9547f-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="9547f-171">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="9547f-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="9547f-172">Abra o arquivo da solução (.sln) que está incluído na raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="9547f-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="9547f-173">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="9547f-173">Create virtual environment</span></span>
<span data-ttu-id="9547f-174">Agora vamos criar um ambiente virtual para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="9547f-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="9547f-175">Clique com o botão direito do mouse em **Ambientes Python** e selecione **Adicionar ambiente virtual...**.</span><span class="sxs-lookup"><span data-stu-id="9547f-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="9547f-176">Verifique se o nome do ambiente é `env`.</span><span class="sxs-lookup"><span data-stu-id="9547f-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="9547f-177">Selecione o interpretador de base.</span><span class="sxs-lookup"><span data-stu-id="9547f-177">Select the base interpreter.</span></span> <span data-ttu-id="9547f-178">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha **Configurações do Aplicativo** de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="9547f-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="9547f-179">Verifique se a opção para baixar e instalar pacotes está marcada.</span><span class="sxs-lookup"><span data-stu-id="9547f-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="9547f-180">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9547f-180">Click **Create**.</span></span> <span data-ttu-id="9547f-181">Isso criará o ambiente virtual e instalar dependências listadas em requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="9547f-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="9547f-182">Criar um superusuário</span><span class="sxs-lookup"><span data-stu-id="9547f-182">Create a superuser</span></span>
<span data-ttu-id="9547f-183">O banco de dados que acompanha o aplicativo não tem nenhum superusuário definido.</span><span class="sxs-lookup"><span data-stu-id="9547f-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="9547f-184">Para usar a funcionalidade de entrar no aplicativo, ou então a interface de administrador do Django (se você decidir habilitá-la), você precisará criar um superusuário.</span><span class="sxs-lookup"><span data-stu-id="9547f-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="9547f-185">Execute isso na linha de comando da sua pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="9547f-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="9547f-186">Siga os prompts para definir o nome de usuário, senha, etc.</span><span class="sxs-lookup"><span data-stu-id="9547f-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="9547f-187">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="9547f-187">Run using development server</span></span>
<span data-ttu-id="9547f-188">Pressione F5 para iniciar a depuração e o navegador da Web abrirá automaticamente na página sendo executada localmente.</span><span class="sxs-lookup"><span data-stu-id="9547f-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="9547f-189">Você pode definir pontos de interrupção nas fontes, usar as janelas de observação etc. Consulte [Ferramentas Python para Documentação] do Visual Studio para obter mais informações sobre os vários recursos.</span><span class="sxs-lookup"><span data-stu-id="9547f-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="9547f-190">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="9547f-190">Make changes</span></span>
<span data-ttu-id="9547f-191">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9547f-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="9547f-192">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="9547f-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="9547f-193">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="9547f-193">Install more packages</span></span>
<span data-ttu-id="9547f-194">Seu aplicativo pode ter dependências além de Python e Django.</span><span class="sxs-lookup"><span data-stu-id="9547f-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="9547f-195">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="9547f-195">You can install additional packages using pip.</span></span> <span data-ttu-id="9547f-196">Para instalar um pacote, clique no ambiente virtual e selecione **Instalar pacote Python**.</span><span class="sxs-lookup"><span data-stu-id="9547f-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="9547f-197">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite `azure`:</span><span class="sxs-lookup"><span data-stu-id="9547f-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="9547f-198">Clique com o botão direito do mouse em no ambiente virtual e selecione **Gerar requirements.txt** para atualizar requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="9547f-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="9547f-199">Em seguida, confirme as alterações a requirements.txt no repositório Git.</span><span class="sxs-lookup"><span data-stu-id="9547f-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="9547f-200">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="9547f-200">Deploy to Azure</span></span>
<span data-ttu-id="9547f-201">Para disparar uma implantação, clique em **Sincronização** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="9547f-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="9547f-202">A opção Sincronização faz um envio por push e a extração.</span><span class="sxs-lookup"><span data-stu-id="9547f-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="9547f-203">A primeira implantação levará algum tempo, pois isso criará um ambiente virtual, pacotes de instalação, etc.</span><span class="sxs-lookup"><span data-stu-id="9547f-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="9547f-204">O Visual Studio não mostra o progresso da implantação.</span><span class="sxs-lookup"><span data-stu-id="9547f-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="9547f-205">Se você quiser revisar a saída, consulte a seção sobre [Solução de problemas - Implantação](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="9547f-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="9547f-206">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="9547f-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="9547f-207">Desenvolvimento de aplicativos Web - Windows - linha de comando</span><span class="sxs-lookup"><span data-stu-id="9547f-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="9547f-208">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="9547f-208">Clone the repository</span></span>
<span data-ttu-id="9547f-209">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure e adicione o repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="9547f-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="9547f-210">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="9547f-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="9547f-211">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="9547f-211">Create virtual environment</span></span>
<span data-ttu-id="9547f-212">Criaremos um novo ambiente virtual para fins de desenvolvimento (não o adicione ao repositório).</span><span class="sxs-lookup"><span data-stu-id="9547f-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="9547f-213">Ambientes virtuais em Python não são relocáveis, portanto, todo desenvolvedor trabalhando no aplicativo criará seu próprio ambiente virtual localmente.</span><span class="sxs-lookup"><span data-stu-id="9547f-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="9547f-214">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha Configurações do Aplicativo de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="9547f-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="9547f-215">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="9547f-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="9547f-216">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="9547f-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="9547f-217">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9547f-217">Install any external packages required by your application.</span></span> <span data-ttu-id="9547f-218">Você pode usar o arquivo requirements.txt na raiz do repositório para instalar os pacotes no seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="9547f-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="9547f-219">Criar um superusuário</span><span class="sxs-lookup"><span data-stu-id="9547f-219">Create a superuser</span></span>
<span data-ttu-id="9547f-220">O banco de dados que acompanha o aplicativo não tem nenhum superusuário definido.</span><span class="sxs-lookup"><span data-stu-id="9547f-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="9547f-221">Para usar a funcionalidade de entrar no aplicativo, ou então a interface de administrador do Django (se você decidir habilitá-la), você precisará criar um superusuário.</span><span class="sxs-lookup"><span data-stu-id="9547f-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="9547f-222">Execute isso na linha de comando da sua pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="9547f-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="9547f-223">Siga os prompts para definir o nome de usuário, senha, etc.</span><span class="sxs-lookup"><span data-stu-id="9547f-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="9547f-224">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="9547f-224">Run using development server</span></span>
<span data-ttu-id="9547f-225">Você pode iniciar o aplicativo em um servidor de desenvolvimento com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9547f-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="9547f-226">O console exibirá a URL e a porta que o servidor escuta:</span><span class="sxs-lookup"><span data-stu-id="9547f-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="9547f-227">Em seguida, abra o navegador da Web para essa URL.</span><span class="sxs-lookup"><span data-stu-id="9547f-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="9547f-228">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="9547f-228">Make changes</span></span>
<span data-ttu-id="9547f-229">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9547f-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="9547f-230">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="9547f-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="9547f-231">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="9547f-231">Install more packages</span></span>
<span data-ttu-id="9547f-232">Seu aplicativo pode ter dependências além de Python e Django.</span><span class="sxs-lookup"><span data-stu-id="9547f-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="9547f-233">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="9547f-233">You can install additional packages using pip.</span></span> <span data-ttu-id="9547f-234">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="9547f-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="9547f-235">Certifique-se de atualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="9547f-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="9547f-236">Confirme as alterações:</span><span class="sxs-lookup"><span data-stu-id="9547f-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="9547f-237">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="9547f-237">Deploy to Azure</span></span>
<span data-ttu-id="9547f-238">Para disparar uma implantação, envie as alterações por push para o Azure:</span><span class="sxs-lookup"><span data-stu-id="9547f-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="9547f-239">Você verá a saída do script de implantação, incluindo a criação do ambiente virtual, instalação de pacotes, criação do web.config.</span><span class="sxs-lookup"><span data-stu-id="9547f-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="9547f-240">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="9547f-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="9547f-241">Desenvolvimento de aplicativos Web - Mac/Linux - linha de comando</span><span class="sxs-lookup"><span data-stu-id="9547f-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="9547f-242">Clonar o repositório</span><span class="sxs-lookup"><span data-stu-id="9547f-242">Clone the repository</span></span>
<span data-ttu-id="9547f-243">Primeiro, clone o repositório usando a URL fornecida no Portal do Azure e adicione o repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="9547f-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="9547f-244">Para saber mais, consulte a [Implantação de Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="9547f-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="9547f-245">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="9547f-245">Create virtual environment</span></span>
<span data-ttu-id="9547f-246">Criaremos um novo ambiente virtual para fins de desenvolvimento (não o adicione ao repositório).</span><span class="sxs-lookup"><span data-stu-id="9547f-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="9547f-247">Ambientes virtuais em Python não são relocáveis, portanto, todo desenvolvedor trabalhando no aplicativo criará seu próprio ambiente virtual localmente.</span><span class="sxs-lookup"><span data-stu-id="9547f-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="9547f-248">Use a mesma versão do Python selecionada para seu aplicativo Web (em runtime.txt ou na folha Configurações do Aplicativo de seu aplicativo Web no Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="9547f-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="9547f-249">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="9547f-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="9547f-250">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="9547f-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="9547f-251">ou o</span><span class="sxs-lookup"><span data-stu-id="9547f-251">or</span></span>

    pyvenv env

<span data-ttu-id="9547f-252">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9547f-252">Install any external packages required by your application.</span></span> <span data-ttu-id="9547f-253">Você pode usar o arquivo requirements.txt na raiz do repositório para instalar os pacotes no seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="9547f-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="9547f-254">Criar um superusuário</span><span class="sxs-lookup"><span data-stu-id="9547f-254">Create a superuser</span></span>
<span data-ttu-id="9547f-255">O banco de dados que acompanha o aplicativo não tem nenhum superusuário definido.</span><span class="sxs-lookup"><span data-stu-id="9547f-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="9547f-256">Para usar a funcionalidade de entrar no aplicativo, ou então a interface de administrador do Django (se você decidir habilitá-la), você precisará criar um superusuário.</span><span class="sxs-lookup"><span data-stu-id="9547f-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="9547f-257">Execute isso na linha de comando da sua pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="9547f-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="9547f-258">Siga os prompts para definir o nome de usuário, senha, etc.</span><span class="sxs-lookup"><span data-stu-id="9547f-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="9547f-259">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="9547f-259">Run using development server</span></span>
<span data-ttu-id="9547f-260">Você pode iniciar o aplicativo em um servidor de desenvolvimento com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9547f-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="9547f-261">O console exibirá a URL e a porta que o servidor escuta:</span><span class="sxs-lookup"><span data-stu-id="9547f-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="9547f-262">Em seguida, abra o navegador da Web para essa URL.</span><span class="sxs-lookup"><span data-stu-id="9547f-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="9547f-263">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="9547f-263">Make changes</span></span>
<span data-ttu-id="9547f-264">Agora você pode experimentar, fazendo alterações às fontes e/ou modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9547f-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="9547f-265">Após ter testado as alterações, confirme-as no repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="9547f-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="9547f-266">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="9547f-266">Install more packages</span></span>
<span data-ttu-id="9547f-267">Seu aplicativo pode ter dependências além de Python e Django.</span><span class="sxs-lookup"><span data-stu-id="9547f-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="9547f-268">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="9547f-268">You can install additional packages using pip.</span></span> <span data-ttu-id="9547f-269">Por exemplo, para instalar o SDK do Azure para Python, que fornece acesso ao armazenamento do Azure, ao barramento de serviço e a outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="9547f-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="9547f-270">Certifique-se de atualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="9547f-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="9547f-271">Confirme as alterações:</span><span class="sxs-lookup"><span data-stu-id="9547f-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="9547f-272">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="9547f-272">Deploy to Azure</span></span>
<span data-ttu-id="9547f-273">Para disparar uma implantação, envie as alterações por push para o Azure:</span><span class="sxs-lookup"><span data-stu-id="9547f-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="9547f-274">Você verá a saída do script de implantação, incluindo a criação do ambiente virtual, instalação de pacotes, criação do web.config.</span><span class="sxs-lookup"><span data-stu-id="9547f-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="9547f-275">Navegue até a URL do Azure para exibir suas alterações.</span><span class="sxs-lookup"><span data-stu-id="9547f-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="9547f-276">Solução de problemas - Instalação de pacotes</span><span class="sxs-lookup"><span data-stu-id="9547f-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="9547f-277">Solução de problemas - Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="9547f-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="9547f-278">Solução de problemas - Arquivos estáticos</span><span class="sxs-lookup"><span data-stu-id="9547f-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="9547f-279">O Django tem o conceito de coletar arquivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="9547f-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="9547f-280">Isso retira todos os arquivos estáticos de seu local original e copia-os para uma única pasta.</span><span class="sxs-lookup"><span data-stu-id="9547f-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="9547f-281">Para este aplicativo, eles são copiados para `/static`.</span><span class="sxs-lookup"><span data-stu-id="9547f-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="9547f-282">Isso é feito porque arquivos estáticos podem vir de 'aplicativos' do Django diferentes.</span><span class="sxs-lookup"><span data-stu-id="9547f-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="9547f-283">Por exemplo, os arquivos estáticos das interfaces de admin do Django estão localizados em uma subpasta de biblioteca do Django no ambiente virtual.</span><span class="sxs-lookup"><span data-stu-id="9547f-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="9547f-284">Arquivos estáticos definidos por esse aplicativo estão localizados em `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="9547f-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="9547f-285">Já que usa mais 'aplicativos' do Django, você terá arquivos estáticos localizados em múltiplos locais.</span><span class="sxs-lookup"><span data-stu-id="9547f-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="9547f-286">Ao executar o aplicativo no modo de depuração, o aplicativo serve os arquivos estáticos desde seu local original.</span><span class="sxs-lookup"><span data-stu-id="9547f-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="9547f-287">Ao executar o aplicativo no modo de liberação, o aplicativo **não** servirá os arquivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="9547f-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="9547f-288">Servir os arquivos é responsabilidade do servidor Web.</span><span class="sxs-lookup"><span data-stu-id="9547f-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="9547f-289">Para este aplicativo, o IIS servirá os arquivos estáticos por meio de `/static`.</span><span class="sxs-lookup"><span data-stu-id="9547f-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="9547f-290">A coleta de arquivos estáticos é feita automaticamente como parte do script de implantação, limpando arquivos coletados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9547f-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="9547f-291">Isso significa que a coleta ocorre em cada implantação, desacelerando um pouco o processo de implantação; todavia, garante que os arquivos obsoletos não estarão disponíveis, evitando um problema de segurança em potencial.</span><span class="sxs-lookup"><span data-stu-id="9547f-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="9547f-292">Se você quiser ignorar a coleção de arquivos estáticos para seu aplicativo Django:</span><span class="sxs-lookup"><span data-stu-id="9547f-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="9547f-293">Em seguida, você precisará fazer a coleta manualmente no computador local:</span><span class="sxs-lookup"><span data-stu-id="9547f-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="9547f-294">Em seguida, remova a pasta `\static` de `.gitignore` e adicione-a ao repositório Git.</span><span class="sxs-lookup"><span data-stu-id="9547f-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="9547f-295">Solução de problemas - Configurações</span><span class="sxs-lookup"><span data-stu-id="9547f-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="9547f-296">Várias configurações para o aplicativo podem ser alteradas em `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="9547f-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="9547f-297">Para conveniência do desenvolvedor, o modo de depuração está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9547f-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="9547f-298">Um bom efeito colateral disso é que você poderá ver as imagens e outros conteúdos estáticos quando em execução localmente, sem precisar coletar arquivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="9547f-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="9547f-299">Para desabilitar o modo de depuração:</span><span class="sxs-lookup"><span data-stu-id="9547f-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="9547f-300">Quando a depuração é desabilitada, o valor de `ALLOWED_HOSTS` precisa ser atualizado para incluir o nome de host do Azure.</span><span class="sxs-lookup"><span data-stu-id="9547f-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="9547f-301">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9547f-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="9547f-302">ou para habilitar qualquer um:</span><span class="sxs-lookup"><span data-stu-id="9547f-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="9547f-303">Na prática, talvez você queira fazer algo mais complexo para lidar com a alternância entre os modos de depuração e liberação, e obter o nome do host.</span><span class="sxs-lookup"><span data-stu-id="9547f-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="9547f-304">Você pode definir variáveis de ambiente por meio da página **CONFIGURAR** do Portal do Azure, na seção **configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="9547f-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="9547f-305">Isso pode ser útil para definir valores que você não deseja que apareçam nas fontes (cadeias de conexão, senhas etc.), ou que você deseja definir de maneira diferente entre o Azure e o computador local.</span><span class="sxs-lookup"><span data-stu-id="9547f-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="9547f-306">Em `settings.py`, você pode consultar as variáveis de ambiente usando `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="9547f-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="9547f-307">Usando um banco de dados</span><span class="sxs-lookup"><span data-stu-id="9547f-307">Using a Database</span></span>
<span data-ttu-id="9547f-308">O banco de dados incluído com o aplicativo é um banco de dados sqlite.</span><span class="sxs-lookup"><span data-stu-id="9547f-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="9547f-309">Isso é um banco de dados padrão útil e conveniente no uso para o desenvolvimento, pois ele não exige praticamente nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="9547f-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="9547f-310">O banco de dados é armazenado no arquivo db.sqlite3, na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="9547f-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="9547f-311">O Azure fornece serviços de banco de dados que são fáceis de usar em um aplicativo Django.</span><span class="sxs-lookup"><span data-stu-id="9547f-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="9547f-312">Tutoriais para uso de [Banco de dados SQL] e [MySQL] por meio de um aplicativo Django mostram as etapas necessárias para criar o serviço de banco de dados e alterar as configurações de banco de dados em `DjangoWebProject/settings.py`, além das bibliotecas necessárias para a instalação.</span><span class="sxs-lookup"><span data-stu-id="9547f-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="9547f-313">É claro que, se você preferir gerenciar seus próprios servidores de banco de dados, você pode fazer isso usando máquinas virtuais em Windows ou Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="9547f-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="9547f-314">Interface de administração do Django</span><span class="sxs-lookup"><span data-stu-id="9547f-314">Django Admin Interface</span></span>
<span data-ttu-id="9547f-315">Depois que você começar a criar seus modelos, você desejará preencher o banco de dados com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="9547f-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="9547f-316">Uma maneira fácil de adicionar e editar o conteúdo de modo interativo é usar a interface de administração do Django.</span><span class="sxs-lookup"><span data-stu-id="9547f-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="9547f-317">O código para a interface do administrador é comentado nas fontes de aplicativo, mas é claramente marcado para que você possa habilitá-lo com facilidade (procure por 'admin').</span><span class="sxs-lookup"><span data-stu-id="9547f-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="9547f-318">Depois que ele estiver habilitado, sincronize o banco de dados, execute o aplicativo e navegue até `/admin`.</span><span class="sxs-lookup"><span data-stu-id="9547f-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9547f-319">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9547f-319">Next Steps</span></span>
<span data-ttu-id="9547f-320">Siga esses links para saber mais sobre o Django e Python Tools para o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9547f-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="9547f-321">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="9547f-321">[Django Documentation]</span></span>
* <span data-ttu-id="9547f-322">[Ferramentas Python para Documentação]</span><span class="sxs-lookup"><span data-stu-id="9547f-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="9547f-323">Para obter informações sobre como usar o MySQL e banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="9547f-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="9547f-324">[Django e MySQL no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="9547f-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="9547f-325">[Django e Banco de Dados SQL no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="9547f-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="9547f-326">Para obter mais informações, consulte o [Centro de Desenvolvedores do Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="9547f-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="9547f-327">O que mudou</span><span class="sxs-lookup"><span data-stu-id="9547f-327">What's changed</span></span>
* <span data-ttu-id="9547f-328">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="9547f-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django e MySQL no Azure com Ferramentas Python para Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django e Banco de Dados SQL no Azure com Ferramentas Python para Visual Studio]: web-sites-python-ptvs-django-sql.md
[Banco de dados SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[SDK do Azure para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[SDK do Azure para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Ferramentas Python para Documentação]: http://aka.ms/ptvsdocs
[Documentação do Django]: https://www.djangoproject.com/
