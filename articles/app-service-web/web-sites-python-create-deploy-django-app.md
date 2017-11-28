---
title: aplicativos web aaaCreating com Django no Azure
description: "Um tutorial que apresenta a você toorunning um aplicativo da web Python em aplicativos de Web do serviço de aplicativo do Azure."
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
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="a6d25-103">Criando aplicativos Web com Django no Azure</span><span class="sxs-lookup"><span data-stu-id="a6d25-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="a6d25-104">Este tutorial descreve como tooget iniciada executando Python em [aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a6d25-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="a6d25-105">Os Aplicativos Web fornecem hospedagem gratuita limitada e implantação rápida, além permitirem a você usar o Python!</span><span class="sxs-lookup"><span data-stu-id="a6d25-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="a6d25-106">Como seu aplicativo cresce, você pode alternar a hospedagem de toopaid e você também pode integrar com todos os Olá outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d25-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="a6d25-107">Você criará um aplicativo usando a estrutura de web Django hello (consulte versões alternativas deste tutorial para [bulbo](web-sites-python-create-deploy-flask-app.md) e [garrafa](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="a6d25-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="a6d25-108">Você criar o aplicativo da web de saudação do hello Azure Marketplace, configurar a implantação do Git e clonar Olá repositório localmente.</span><span class="sxs-lookup"><span data-stu-id="a6d25-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="a6d25-109">Em seguida, você executar o aplicativo hello localmente, fazer alterações, confirmar e enviá-las tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a6d25-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="a6d25-110">Olá tutorial mostra como toodo isso do Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="a6d25-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a6d25-111">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6d25-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a6d25-112">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a6d25-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a6d25-113">Prerequisites</span></span>
* <span data-ttu-id="a6d25-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="a6d25-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="a6d25-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="a6d25-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="a6d25-116">setuptools, pip, virtualenv (somente Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="a6d25-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="a6d25-117">Git</span><span class="sxs-lookup"><span data-stu-id="a6d25-117">Git</span></span>
* <span data-ttu-id="a6d25-118">PTVS ([Python Tools para Visual Studio][Python Tools para Visual Studio]) – Observação: isso é opcional</span><span class="sxs-lookup"><span data-stu-id="a6d25-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="a6d25-119">**Observação**: atualmente não há suporte à a publicação do TFS em projetos de Python.</span><span class="sxs-lookup"><span data-stu-id="a6d25-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="a6d25-120">Windows</span><span class="sxs-lookup"><span data-stu-id="a6d25-120">Windows</span></span>
<span data-ttu-id="a6d25-121">Caso você ainda não tenha o Python 2.7 ou 3.4 instalado (32 bits), recomendamos instalar o [SDK do Azure para Python 2.7] ou [SDK do Azure para Python 3.4] usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="a6d25-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="a6d25-122">Isso instala a versão de 32 bits de saudação do Python setuptools, pip, virtualenv, etc (Python de 32 bits é o que é instalado em computadores de host do Azure Olá).</span><span class="sxs-lookup"><span data-stu-id="a6d25-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="a6d25-123">Como alternativa, você pode obter o Python por meio de [python.org].</span><span class="sxs-lookup"><span data-stu-id="a6d25-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="a6d25-124">Para Git, recomendamos [Git para Windows] ou [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="a6d25-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="a6d25-125">Se você usar o Visual Studio, você pode usar o suporte de Git Olá integrado.</span><span class="sxs-lookup"><span data-stu-id="a6d25-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="a6d25-126">Também recomendamos a instalação das [Ferramentas Python 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a6d25-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="a6d25-127">Isso é opcional, mas se você tiver [Visual Studio], incluindo Olá liberar o Visual Studio Community 2013 ou o Visual Studio Express 2013 para Web, e isso lhe dará um grande IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="a6d25-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="a6d25-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="a6d25-128">Mac/Linux</span></span>
<span data-ttu-id="a6d25-129">Você deve ter o Python e Git já instalados, mas certifique-se de ter uma das versões 2.7 ou 3.4 do Python.</span><span class="sxs-lookup"><span data-stu-id="a6d25-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="a6d25-130">Criação de aplicativos Web no Portal</span><span class="sxs-lookup"><span data-stu-id="a6d25-130">Web App Creation on Portal</span></span>
<span data-ttu-id="a6d25-131">primeira etapa na criação de seu aplicativo Hello é toocreate Olá web aplicativo via Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6d25-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="a6d25-132">Faça logon no hello Portal do Azure e clique em Olá **novo** botão no canto do hello inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="a6d25-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="a6d25-133">Na caixa de pesquisa hello, digite "python".</span><span class="sxs-lookup"><span data-stu-id="a6d25-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="a6d25-134">Nos resultados da pesquisa hello, selecione **Django** (publicado por PTVS), em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a6d25-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="a6d25-135">Configure o novo aplicativo de Django hello, como criar um novo plano de serviço de aplicativo e um novo grupo de recursos para ele.</span><span class="sxs-lookup"><span data-stu-id="a6d25-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="a6d25-136">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a6d25-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="a6d25-137">Configurar a publicação de Git para seu aplicativo web criado recentemente, seguindo as instruções de saudação em [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a6d25-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="a6d25-138">Visão geral do aplicativo</span><span class="sxs-lookup"><span data-stu-id="a6d25-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="a6d25-139">Conteúdos do repositório Git</span><span class="sxs-lookup"><span data-stu-id="a6d25-139">Git repository contents</span></span>
<span data-ttu-id="a6d25-140">Aqui está uma visão geral dos arquivos Olá que no repositório Git inicial Olá que podemos será clonar na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="a6d25-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

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

<span data-ttu-id="a6d25-141">Principais fontes para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-141">Main sources for hello application.</span></span> <span data-ttu-id="a6d25-142">Consiste em 3 páginas (índice, sobre, contato) com um layout mestre.</span><span class="sxs-lookup"><span data-stu-id="a6d25-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="a6d25-143">Scripts e conteúdo estático incluem bootstrap, jquery, modernizr e respond.</span><span class="sxs-lookup"><span data-stu-id="a6d25-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="a6d25-144">Gerenciamento local e suporte ao servidor de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="a6d25-144">Local management and development server support.</span></span> <span data-ttu-id="a6d25-145">Use este aplicativo de saudação toorun localmente, sincronizar o banco de dados de saudação, etc.</span><span class="sxs-lookup"><span data-stu-id="a6d25-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="a6d25-146">Banco de dados padrão.</span><span class="sxs-lookup"><span data-stu-id="a6d25-146">Default database.</span></span> <span data-ttu-id="a6d25-147">Inclui tabelas necessárias Olá Olá toorun de aplicativo, mas não contém todos os usuários (sincronizar o banco de dados de saudação toocreate um usuário).</span><span class="sxs-lookup"><span data-stu-id="a6d25-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="a6d25-148">Arquivos de projeto para uso com [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a6d25-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="a6d25-149">Proxy de IIS para ambientes virtuais e suporte à depuração remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="a6d25-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="a6d25-150">Pacotes externos requeridos por este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6d25-150">External packages needed by this application.</span></span> <span data-ttu-id="a6d25-151">script de implantação Hello serão pip instalar pacotes de saudação listados neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6d25-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="a6d25-152">Arquivos de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="a6d25-152">IIS configuration files.</span></span> <span data-ttu-id="a6d25-153">script de implantação de saudação será usar web.x.y.config apropriado hello e copie-o como Web. config.</span><span class="sxs-lookup"><span data-stu-id="a6d25-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="a6d25-154">Arquivos opcionais - personalizando a implantação</span><span class="sxs-lookup"><span data-stu-id="a6d25-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="a6d25-155">Arquivos opcionais - tempo de execução do Python</span><span class="sxs-lookup"><span data-stu-id="a6d25-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="a6d25-156">Arquivos adicionais no servidor</span><span class="sxs-lookup"><span data-stu-id="a6d25-156">Additional files on server</span></span>
<span data-ttu-id="a6d25-157">Alguns arquivos existem no servidor de saudação, mas não são adicionados o repositório do git toohello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="a6d25-158">Eles são criados pelo script de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6d25-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="a6d25-159">Arquivo de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="a6d25-159">IIS configuration file.</span></span> <span data-ttu-id="a6d25-160">Criado por meio de web.x.y.config em toda implantação.</span><span class="sxs-lookup"><span data-stu-id="a6d25-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="a6d25-161">Ambiente virtual do Python.</span><span class="sxs-lookup"><span data-stu-id="a6d25-161">Python virtual environment.</span></span> <span data-ttu-id="a6d25-162">Criado durante a implantação se um ambiente virtual compatível já não existe no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6d25-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="a6d25-163">Os pacotes listados no requirements.txt são pip instalado, mas pip vai ignorar a instalação se Olá pacotes já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="a6d25-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="a6d25-164">Olá próximos 3 seções descrevem como tooproceed com Olá web desenvolvimento de aplicativo em 3 ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="a6d25-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="a6d25-165">Windows, com Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6d25-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="a6d25-166">Windows, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="a6d25-166">Windows, with command line</span></span>
* <span data-ttu-id="a6d25-167">Mac/Linux, com linha de comando</span><span class="sxs-lookup"><span data-stu-id="a6d25-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="a6d25-168">Desenvolvimento de aplicativo Web - Windows - Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6d25-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="a6d25-169">Repositório de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="a6d25-169">Clone hello repository</span></span>
<span data-ttu-id="a6d25-170">Primeiro, clone o repositório de saudação usando Olá URL fornecida no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d25-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="a6d25-171">Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a6d25-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="a6d25-172">Abra o arquivo de solução da saudação (. sln) que está incluído na raiz de saudação do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6d25-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="a6d25-173">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="a6d25-173">Create virtual environment</span></span>
<span data-ttu-id="a6d25-174">Agora vamos criar um ambiente virtual para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="a6d25-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="a6d25-175">Clique com o botão direito do mouse em **Ambientes Python** e selecione **Adicionar ambiente virtual...**.</span><span class="sxs-lookup"><span data-stu-id="a6d25-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="a6d25-176">Certifique-se de nome de saudação do ambiente Olá é `env`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="a6d25-177">Selecione o interpretador base hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-177">Select hello base interpreter.</span></span> <span data-ttu-id="a6d25-178">Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (em runtime.txt ou Olá **configurações de aplicativo** folha do seu aplicativo web no hello Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="a6d25-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="a6d25-179">Certifique-se de saudação opção toodownload e instalar pacotes é verificada.</span><span class="sxs-lookup"><span data-stu-id="a6d25-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="a6d25-180">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a6d25-180">Click **Create**.</span></span> <span data-ttu-id="a6d25-181">Isso será criar ambiente virtual hello e instalar dependências listadas em requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="a6d25-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="a6d25-182">Criar um superusuário</span><span class="sxs-lookup"><span data-stu-id="a6d25-182">Create a superuser</span></span>
<span data-ttu-id="a6d25-183">banco de dados de saudação incluído com o aplicativo hello não tem qualquer superusuário definido.</span><span class="sxs-lookup"><span data-stu-id="a6d25-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="a6d25-184">Ordem toouse Olá entrar funcionalidade no aplicativo hello, ou interface de administração de Django hello (se você decidir tooenable ele), você precisará toocreate um superusuário.</span><span class="sxs-lookup"><span data-stu-id="a6d25-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="a6d25-185">Execute este da saudação de linha de comando da sua pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="a6d25-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="a6d25-186">Siga o nome de usuário do hello prompts tooset hello, senha, etc.</span><span class="sxs-lookup"><span data-stu-id="a6d25-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="a6d25-187">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="a6d25-187">Run using development server</span></span>
<span data-ttu-id="a6d25-188">Pressione F5 toostart depuração e o navegador da web serão aberto automaticamente toohello página em execução localmente.</span><span class="sxs-lookup"><span data-stu-id="a6d25-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="a6d25-189">Você pode definir pontos de interrupção em fontes de hello, use Olá inspecionar windows, etc. Consulte Olá [ferramentas Python para documentação do Visual Studio] para obter mais informações sobre Olá vários recursos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="a6d25-190">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="a6d25-190">Make changes</span></span>
<span data-ttu-id="a6d25-191">Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="a6d25-192">Depois de testar suas alterações, confirme repositório do Git toohello:</span><span class="sxs-lookup"><span data-stu-id="a6d25-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="a6d25-193">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="a6d25-193">Install more packages</span></span>
<span data-ttu-id="a6d25-194">Seu aplicativo pode ter dependências além de Python e Django.</span><span class="sxs-lookup"><span data-stu-id="a6d25-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="a6d25-195">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="a6d25-195">You can install additional packages using pip.</span></span> <span data-ttu-id="a6d25-196">tooinstall um pacote, clique com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.</span><span class="sxs-lookup"><span data-stu-id="a6d25-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="a6d25-197">Por exemplo, tooinstall hello Azure SDK para Python, que oferece acesso tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite `azure`:</span><span class="sxs-lookup"><span data-stu-id="a6d25-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="a6d25-198">Clique com botão direito no ambiente virtual hello e selecione **gerar requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="a6d25-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="a6d25-199">Em seguida, Olá confirmação altera o repositório do Git toohello toorequirements.txt.</span><span class="sxs-lookup"><span data-stu-id="a6d25-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="a6d25-200">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="a6d25-200">Deploy tooAzure</span></span>
<span data-ttu-id="a6d25-201">tootrigger uma implantação, clique em **sincronização** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="a6d25-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="a6d25-202">A opção Sincronização faz um envio por push e a extração.</span><span class="sxs-lookup"><span data-stu-id="a6d25-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="a6d25-203">implantação Olá levará algum tempo, pois ele cria um ambiente virtual, pacotes de instalação, etc.</span><span class="sxs-lookup"><span data-stu-id="a6d25-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="a6d25-204">O Visual Studio não mostra o progresso de saudação de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6d25-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="a6d25-205">Se desejar que a saída de hello tooreview, consulte a seção de saudação em [solução de problemas - implantação](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="a6d25-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="a6d25-206">Procure toohello URL do Azure tooview suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a6d25-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="a6d25-207">Desenvolvimento de aplicativos Web - Windows - linha de comando</span><span class="sxs-lookup"><span data-stu-id="a6d25-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="a6d25-208">Repositório de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="a6d25-208">Clone hello repository</span></span>
<span data-ttu-id="a6d25-209">Primeiro, clonar repositório hello usando Olá URL fornecida no hello Portal do Azure e adicionar Olá repositório do Azure como um controle remoto.</span><span class="sxs-lookup"><span data-stu-id="a6d25-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="a6d25-210">Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a6d25-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="a6d25-211">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="a6d25-211">Create virtual environment</span></span>
<span data-ttu-id="a6d25-212">Vamos criar um novo ambiente virtual para fins de desenvolvimento (não adicioná-lo toohello repositório).</span><span class="sxs-lookup"><span data-stu-id="a6d25-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="a6d25-213">Ambientes virtuais no Python não são relocáveis, portanto, todos os desenvolvedores trabalhando em um aplicativo hello vai criar seus próprios localmente.</span><span class="sxs-lookup"><span data-stu-id="a6d25-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="a6d25-214">Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (runtime.txt ou hello folha de configurações de aplicativo do seu aplicativo web no hello Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="a6d25-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="a6d25-215">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="a6d25-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="a6d25-216">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="a6d25-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="a6d25-217">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6d25-217">Install any external packages required by your application.</span></span> <span data-ttu-id="a6d25-218">Você pode usar o arquivo de requirements.txt de saudação na raiz de saudação de pacotes de saudação do hello repositório tooinstall em seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="a6d25-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="a6d25-219">Criar um superusuário</span><span class="sxs-lookup"><span data-stu-id="a6d25-219">Create a superuser</span></span>
<span data-ttu-id="a6d25-220">banco de dados de saudação incluído com o aplicativo hello não tem qualquer superusuário definido.</span><span class="sxs-lookup"><span data-stu-id="a6d25-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="a6d25-221">Ordem toouse Olá entrar funcionalidade no aplicativo hello, ou interface de administração de Django hello (se você decidir tooenable ele), você precisará toocreate um superusuário.</span><span class="sxs-lookup"><span data-stu-id="a6d25-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="a6d25-222">Execute este da saudação de linha de comando da sua pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="a6d25-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="a6d25-223">Siga o nome de usuário do hello prompts tooset hello, senha, etc.</span><span class="sxs-lookup"><span data-stu-id="a6d25-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="a6d25-224">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="a6d25-224">Run using development server</span></span>
<span data-ttu-id="a6d25-225">Você pode iniciar o aplicativo hello em um servidor de desenvolvimento com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6d25-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="a6d25-226">console Olá exibirá a URL de saudação e servidor de saudação porta escuta:</span><span class="sxs-lookup"><span data-stu-id="a6d25-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="a6d25-227">Em seguida, abra a URL de toothat do navegador da web.</span><span class="sxs-lookup"><span data-stu-id="a6d25-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="a6d25-228">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="a6d25-228">Make changes</span></span>
<span data-ttu-id="a6d25-229">Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="a6d25-230">Depois de testar suas alterações, confirme repositório do Git toohello:</span><span class="sxs-lookup"><span data-stu-id="a6d25-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="a6d25-231">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="a6d25-231">Install more packages</span></span>
<span data-ttu-id="a6d25-232">Seu aplicativo pode ter dependências além de Python e Django.</span><span class="sxs-lookup"><span data-stu-id="a6d25-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="a6d25-233">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="a6d25-233">You can install additional packages using pip.</span></span> <span data-ttu-id="a6d25-234">Por exemplo, tooinstall hello Azure SDK para Python, que dá a você acessar tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="a6d25-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="a6d25-235">Certifique-se de que requirements.txt de tooupdate:</span><span class="sxs-lookup"><span data-stu-id="a6d25-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="a6d25-236">Confirme as alterações de saudação:</span><span class="sxs-lookup"><span data-stu-id="a6d25-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="a6d25-237">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="a6d25-237">Deploy tooAzure</span></span>
<span data-ttu-id="a6d25-238">tootrigger uma implantação, Olá push altera tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a6d25-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="a6d25-239">Você verá uma saída Olá Olá do script de implantação, incluindo a criação do ambiente virtual, a instalação de pacotes, criação de Web. config.</span><span class="sxs-lookup"><span data-stu-id="a6d25-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="a6d25-240">Procure toohello URL do Azure tooview suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a6d25-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="a6d25-241">Desenvolvimento de aplicativos Web - Mac/Linux - linha de comando</span><span class="sxs-lookup"><span data-stu-id="a6d25-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="a6d25-242">Repositório de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="a6d25-242">Clone hello repository</span></span>
<span data-ttu-id="a6d25-243">Primeiro, clonar repositório hello usando Olá URL fornecida no hello Portal do Azure e adicionar Olá repositório do Azure como um controle remoto.</span><span class="sxs-lookup"><span data-stu-id="a6d25-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="a6d25-244">Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a6d25-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="a6d25-245">Criar um ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="a6d25-245">Create virtual environment</span></span>
<span data-ttu-id="a6d25-246">Vamos criar um novo ambiente virtual para fins de desenvolvimento (não adicioná-lo toohello repositório).</span><span class="sxs-lookup"><span data-stu-id="a6d25-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="a6d25-247">Ambientes virtuais no Python não são relocáveis, portanto, todos os desenvolvedores trabalhando em um aplicativo hello vai criar seus próprios localmente.</span><span class="sxs-lookup"><span data-stu-id="a6d25-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="a6d25-248">Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (runtime.txt ou hello folha de configurações de aplicativo do seu aplicativo web no hello Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="a6d25-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="a6d25-249">Para o Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="a6d25-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="a6d25-250">Para o Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="a6d25-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="a6d25-251">ou o</span><span class="sxs-lookup"><span data-stu-id="a6d25-251">or</span></span>

    pyvenv env

<span data-ttu-id="a6d25-252">Instale quaisquer pacotes externos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6d25-252">Install any external packages required by your application.</span></span> <span data-ttu-id="a6d25-253">Você pode usar o arquivo de requirements.txt de saudação na raiz de saudação de pacotes de saudação do hello repositório tooinstall em seu ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="a6d25-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="a6d25-254">Criar um superusuário</span><span class="sxs-lookup"><span data-stu-id="a6d25-254">Create a superuser</span></span>
<span data-ttu-id="a6d25-255">banco de dados de saudação incluído com o aplicativo hello não tem qualquer superusuário definido.</span><span class="sxs-lookup"><span data-stu-id="a6d25-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="a6d25-256">Ordem toouse Olá entrar funcionalidade no aplicativo hello, ou interface de administração de Django hello (se você decidir tooenable ele), você precisará toocreate um superusuário.</span><span class="sxs-lookup"><span data-stu-id="a6d25-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="a6d25-257">Execute este da saudação de linha de comando da sua pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="a6d25-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="a6d25-258">Siga o nome de usuário do hello prompts tooset hello, senha, etc.</span><span class="sxs-lookup"><span data-stu-id="a6d25-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="a6d25-259">Executar usando o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="a6d25-259">Run using development server</span></span>
<span data-ttu-id="a6d25-260">Você pode iniciar o aplicativo hello em um servidor de desenvolvimento com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6d25-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="a6d25-261">console Olá exibirá a URL de saudação e servidor de saudação porta escuta:</span><span class="sxs-lookup"><span data-stu-id="a6d25-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="a6d25-262">Em seguida, abra a URL de toothat do navegador da web.</span><span class="sxs-lookup"><span data-stu-id="a6d25-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="a6d25-263">Fazer alterações</span><span class="sxs-lookup"><span data-stu-id="a6d25-263">Make changes</span></span>
<span data-ttu-id="a6d25-264">Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="a6d25-265">Depois de testar suas alterações, confirme repositório do Git toohello:</span><span class="sxs-lookup"><span data-stu-id="a6d25-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="a6d25-266">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="a6d25-266">Install more packages</span></span>
<span data-ttu-id="a6d25-267">Seu aplicativo pode ter dependências além de Python e Django.</span><span class="sxs-lookup"><span data-stu-id="a6d25-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="a6d25-268">Você pode instalar pacotes adicionais usando pip.</span><span class="sxs-lookup"><span data-stu-id="a6d25-268">You can install additional packages using pip.</span></span> <span data-ttu-id="a6d25-269">Por exemplo, tooinstall hello Azure SDK para Python, que dá a você acessar tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite:</span><span class="sxs-lookup"><span data-stu-id="a6d25-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="a6d25-270">Certifique-se de que requirements.txt de tooupdate:</span><span class="sxs-lookup"><span data-stu-id="a6d25-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="a6d25-271">Confirme as alterações de saudação:</span><span class="sxs-lookup"><span data-stu-id="a6d25-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="a6d25-272">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="a6d25-272">Deploy tooAzure</span></span>
<span data-ttu-id="a6d25-273">tootrigger uma implantação, Olá push altera tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a6d25-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="a6d25-274">Você verá uma saída Olá Olá do script de implantação, incluindo a criação do ambiente virtual, a instalação de pacotes, criação de Web. config.</span><span class="sxs-lookup"><span data-stu-id="a6d25-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="a6d25-275">Procure toohello URL do Azure tooview suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a6d25-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="a6d25-276">Solução de problemas - Instalação de pacotes</span><span class="sxs-lookup"><span data-stu-id="a6d25-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="a6d25-277">Solução de problemas - Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="a6d25-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="a6d25-278">Solução de problemas - Arquivos estáticos</span><span class="sxs-lookup"><span data-stu-id="a6d25-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="a6d25-279">Django tem o conceito de saudação de coleta de arquivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="a6d25-280">Isso leva a todos os arquivos estáticos de saudação de seu local original e copiá-los tooa única pasta.</span><span class="sxs-lookup"><span data-stu-id="a6d25-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="a6d25-281">Para este aplicativo, eles serão copiados muito`/static`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="a6d25-282">Isso é feito porque arquivos estáticos podem vir de 'aplicativos' do Django diferentes.</span><span class="sxs-lookup"><span data-stu-id="a6d25-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="a6d25-283">Por exemplo, arquivos estáticos de saudação de interfaces de admin do hello Django estão localizados em uma subpasta de biblioteca Django no ambiente virtual hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="a6d25-284">Arquivos estáticos definidos por esse aplicativo estão localizados em `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="a6d25-285">Já que usa mais 'aplicativos' do Django, você terá arquivos estáticos localizados em múltiplos locais.</span><span class="sxs-lookup"><span data-stu-id="a6d25-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="a6d25-286">Ao executar o aplicativo hello no modo de depuração, o aplicativo hello serve arquivos estáticos de saudação de seu local original.</span><span class="sxs-lookup"><span data-stu-id="a6d25-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="a6d25-287">Ao executar o aplicativo hello no modo de versão, o aplicativo hello faz **não** servir arquivos estáticos hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="a6d25-288">É responsabilidade de Olá Olá arquivos da web server tooserve hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="a6d25-289">Para este aplicativo, o IIS servirá arquivos estáticos de saudação do `/static`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="a6d25-290">coleção de saudação de arquivos estáticos é feita automaticamente como parte do script de implantação de hello, limpando previamente coletado de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6d25-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="a6d25-291">Isso significa a coleção Olá ocorre em todas as implantações, diminuir a implantação de um pouco, mas garante que arquivos obsoletos não estarão disponíveis, evitando um possível problema de segurança.</span><span class="sxs-lookup"><span data-stu-id="a6d25-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="a6d25-292">Se você quiser tooskip coleção de arquivos estáticos para seu aplicativo Django:</span><span class="sxs-lookup"><span data-stu-id="a6d25-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="a6d25-293">Em seguida, você precisará coleção de saudação toodo manualmente em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="a6d25-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="a6d25-294">Em seguida, remova Olá `\static` pasta `.gitignore` e adicione-o repositório do Git toohello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="a6d25-295">Solução de problemas - Configurações</span><span class="sxs-lookup"><span data-stu-id="a6d25-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="a6d25-296">Várias configurações para o aplicativo hello podem ser alteradas em `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="a6d25-297">Para conveniência do desenvolvedor, o modo de depuração está habilitado.</span><span class="sxs-lookup"><span data-stu-id="a6d25-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="a6d25-298">Um bom efeito colateral que é que você será capaz de toosee imagens e outros conteúdos estáticos quando em execução localmente, sem a necessidade de arquivos estáticos toocollect.</span><span class="sxs-lookup"><span data-stu-id="a6d25-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="a6d25-299">modo de depuração toodisable:</span><span class="sxs-lookup"><span data-stu-id="a6d25-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="a6d25-300">Quando a depuração estiver desabilitada, Olá valor `ALLOWED_HOSTS` necessidades toobe atualizado nome de host do Azure Olá tooinclude.</span><span class="sxs-lookup"><span data-stu-id="a6d25-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="a6d25-301">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a6d25-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="a6d25-302">ou tooenable qualquer:</span><span class="sxs-lookup"><span data-stu-id="a6d25-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="a6d25-303">Na prática, convém toodo algo toodeal mais complexa com alternando de depuração e lançamento modo e ao obter nome de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6d25-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="a6d25-304">Você pode definir variáveis de ambiente por meio do portal do Azure de saudação **configurar** página Olá **configurações do aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="a6d25-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="a6d25-305">Isso pode ser útil para definir valores que você não deseja tooappear em fontes de saudação (cadeias de caracteres de conexão, senhas etc.), ou que você deseja tooset diferente entre o Azure e sua máquina local.</span><span class="sxs-lookup"><span data-stu-id="a6d25-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="a6d25-306">Em `settings.py`, você pode consultar usando as variáveis de ambiente Olá `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="a6d25-307">Usando um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a6d25-307">Using a Database</span></span>
<span data-ttu-id="a6d25-308">Olá banco de dados que está incluído no aplicativo hello for sqlite.</span><span class="sxs-lookup"><span data-stu-id="a6d25-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="a6d25-309">Este é um toouse de banco de dados padrão útil e conveniente para o desenvolvimento, pois ela requer quase nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="a6d25-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="a6d25-310">banco de dados de saudação é armazenado no arquivo de db.sqlite3 Olá na pasta de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="a6d25-311">O Azure fornece serviços de banco de dados que são toouse fácil de um aplicativo Django.</span><span class="sxs-lookup"><span data-stu-id="a6d25-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="a6d25-312">Tutoriais para usar [banco de dados SQL] e [MySQL] de um aplicativo Django mostrar etapas Olá serviço de banco de dados necessário toocreate hello, alterar as configurações de banco de dados de saudação no `DjangoWebProject/settings.py`e hello bibliotecas necessárias tooinstall.</span><span class="sxs-lookup"><span data-stu-id="a6d25-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="a6d25-313">É claro que, se você preferir toomanage seus próprios servidores de banco de dados, você pode fazer isso usando o Windows ou Linux máquinas virtuais em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d25-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="a6d25-314">Interface de administração do Django</span><span class="sxs-lookup"><span data-stu-id="a6d25-314">Django Admin Interface</span></span>
<span data-ttu-id="a6d25-315">Quando você começar a criar seus modelos, você desejará toopopulate banco de dados de saudação com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="a6d25-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="a6d25-316">Uma maneira fácil toodo adicionar e editar conteúdo interativamente é a interface de administração de Django toouse hello.</span><span class="sxs-lookup"><span data-stu-id="a6d25-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="a6d25-317">código Olá para interface de administração de saudação é comentado em fontes de aplicativo hello, mas é claramente marcada para que você pode facilmente habilitá-lo (procure 'admin').</span><span class="sxs-lookup"><span data-stu-id="a6d25-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="a6d25-318">Depois que ele é habilitado, sincronizar banco de dados hello, execute o aplicativo hello e navegue muito`/admin`.</span><span class="sxs-lookup"><span data-stu-id="a6d25-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6d25-319">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6d25-319">Next Steps</span></span>
<span data-ttu-id="a6d25-320">Siga essas toolearn links mais sobre Django e as ferramentas Python para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a6d25-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="a6d25-321">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="a6d25-321">[Django Documentation]</span></span>
* <span data-ttu-id="a6d25-322">[ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a6d25-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="a6d25-323">Para obter informações sobre como usar o MySQL e banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="a6d25-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="a6d25-324">[Django e MySQL no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a6d25-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="a6d25-325">[Django e Banco de Dados SQL no Azure com Ferramentas Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a6d25-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="a6d25-326">Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="a6d25-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a6d25-327">O que mudou</span><span class="sxs-lookup"><span data-stu-id="a6d25-327">What's changed</span></span>
* <span data-ttu-id="a6d25-328">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a6d25-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django e MySQL no Azure com Ferramentas Python para Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django e Banco de Dados SQL no Azure com Ferramentas Python para Visual Studio]: web-sites-python-ptvs-django-sql.md
[banco de dados SQL]: web-sites-python-ptvs-django-sql.md
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
[ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do Django]: https://www.djangoproject.com/
