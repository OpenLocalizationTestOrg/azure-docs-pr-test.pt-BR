---
title: Django e MySQL no Azure com Ferramentas Python 2.2 para Visual Studio
description: "Aprenda a usar o Python Tools para Visual Studio para criar um aplicativo Django que armazena dados em uma instância do banco de dados MySQL e o implanta em Aplicativos Web do Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="c73a9-103">Django e MySQL no Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c73a9-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="c73a9-104">Neste tutorial, usaremos o [Python Tools para Visual Studio](https://www.visualstudio.com/vs/python) para criar um aplicativo Web de votação simples, usando um dos modelos de exemplo de PTVS.</span><span class="sxs-lookup"><span data-stu-id="c73a9-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="c73a9-105">Você aprenderá a usar um serviço MySQL hospedado no Azure, configurar o aplicativo Web para usar o MySQL e publicar o aplicativo Web para os [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c73a9-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="c73a9-106">As informações contidas neste tutorial também estão disponíveis no vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c73a9-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="c73a9-107">[PTVS 2.1: aplicativo do Django com o MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="c73a9-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="c73a9-108">Confira o [Python Developer Center] para obter mais artigos que abrangem o desenvolvimento de Aplicativos Web do Serviço de Aplicativo do Azure com PTVS usando estruturas da Web Bottle, Flask e Django, com serviços Armazenamento de Tabelas do Azure, MySQL e Banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="c73a9-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="c73a9-109">Embora este artigo se concentre no Serviço de Aplicativo, as etapas são semelhantes ao desenvolvimento de [Serviços de Nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="c73a9-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c73a9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c73a9-110">Prerequisites</span></span>
* <span data-ttu-id="c73a9-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c73a9-111">Visual Studio 2015</span></span>
* <span data-ttu-id="c73a9-112">[Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="c73a9-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="c73a9-113">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c73a9-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="c73a9-114">[Ferramentas do Python 2.2 para Amostras VSIX do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c73a9-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="c73a9-115">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="c73a9-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="c73a9-116">Django 1.9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="c73a9-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="c73a9-117">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c73a9-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c73a9-118">Nenhum cartão de crédito é exigido e não há compromissos.</span><span class="sxs-lookup"><span data-stu-id="c73a9-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="c73a9-119">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="c73a9-119">Create the Project</span></span>
<span data-ttu-id="c73a9-120">Nesta seção, criaremos um projeto do Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="c73a9-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="c73a9-121">Você irá criar um ambiente virtual e instalará os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="c73a9-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="c73a9-122">Você irá criar um banco de dados local usando sqlite.</span><span class="sxs-lookup"><span data-stu-id="c73a9-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="c73a9-123">Em seguida, irá executar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="c73a9-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="c73a9-124">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="c73a9-125">Os modelos de projeto das [Ferramentas do Python 2.2 para Amostras VSIX do Visual Studio] estão disponíveis em **Python**, **Amostras**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="c73a9-126">Selecione **Projeto Web Django de Votações** e clique em OK para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="c73a9-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="c73a9-128">Você será solicitado a instalar pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="c73a9-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="c73a9-129">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-129">Select **Install into a virtual environment**.</span></span>
   
    ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="c73a9-131">Selecione **Python 2.7** ou **Python 3.4** como o interpretador base.</span><span class="sxs-lookup"><span data-stu-id="c73a9-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="c73a9-133">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto, selecione **Python** e **Migrar Django**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="c73a9-134">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="c73a9-135">Isso abrirá um Console de Gerenciamento do Django e criará um banco de dados sqlite na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="c73a9-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="c73a9-136">Siga os prompts para criar um usuário.</span><span class="sxs-lookup"><span data-stu-id="c73a9-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="c73a9-137">Confirme se o aplicativo funciona pressionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="c73a9-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="c73a9-138">Clique em **Fazer logon** na barra de navegação na parte superior.</span><span class="sxs-lookup"><span data-stu-id="c73a9-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Barra de navegação do Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="c73a9-140">Insira as credenciais para o usuário que você criou quando sincronizou o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c73a9-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![Formulário de logon](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="c73a9-142">Clique em **Criar Votações de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-142">Click **Create Sample Polls**.</span></span>
    
     ![Criar Votações de Exemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="c73a9-144">Clique em uma pesquisa e vote.</span><span class="sxs-lookup"><span data-stu-id="c73a9-144">Click on a poll and vote.</span></span>
    
     ![Votação em votações de exemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="c73a9-146">Criar um banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="c73a9-146">Create a MySQL Database</span></span>
<span data-ttu-id="c73a9-147">Para banco de dados, você irá criar um banco de dados ClearDB MySQL hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a9-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="c73a9-148">Como alternativa, você pode criar sua própria máquina virtual em execução no Azure, em seguida, instalar e administrar o MySQL por conta própria.</span><span class="sxs-lookup"><span data-stu-id="c73a9-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="c73a9-149">Você pode criar um banco de dados com um plano grátis seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="c73a9-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="c73a9-150">Faça logon no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="c73a9-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="c73a9-151">Na parte superior do painel de navegação, clique em **NOVO** e clique em **Dados + Armazenamento**, e depois clique em **Banco de dados MySQL**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="c73a9-152">Configure o novo banco de dados MySQL, criando um novo grupo de recursos e selecione o local apropriado para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="c73a9-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="c73a9-153">Depois de criar o banco de dados MySQL, clique em **Propriedades** na folha do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c73a9-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="c73a9-154">É possível usar o botão de cópia para colocar o valor de **CADEIA DE CONEXÃO** na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="c73a9-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="c73a9-155">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="c73a9-155">Configure the Project</span></span>
<span data-ttu-id="c73a9-156">Nesta seção, você irá configurar nosso aplicativo Web para usar o banco de dados MySQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="c73a9-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="c73a9-157">Também irá instalar pacotes adicionais Python necessários para usar bancos de dados MySQL com Django.</span><span class="sxs-lookup"><span data-stu-id="c73a9-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="c73a9-158">Em seguida, você irá executar o aplicativo Web localmente.</span><span class="sxs-lookup"><span data-stu-id="c73a9-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="c73a9-159">No Visual Studio, abra **settings.py**, na pasta *ProjectName* .</span><span class="sxs-lookup"><span data-stu-id="c73a9-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="c73a9-160">Cole temporariamente a cadeia de conexão obtida no editor.</span><span class="sxs-lookup"><span data-stu-id="c73a9-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="c73a9-161">A cadeia de conexão está neste formato:</span><span class="sxs-lookup"><span data-stu-id="c73a9-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="c73a9-162">Altere o **MECANISMO** do banco de dados padrão para usar MySQL e defina os valores para **NOME**, **USUÁRIO**, **SENHA** e **HOST** de **CADEIA DE CONEXÃO**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="c73a9-163">No Gerenciador de Soluções, em **Ambientes Python**, clique com o botão direito do mouse no ambiente virtual e selecione **Instalar Pacote Python**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="c73a9-164">Instale o pacote `mysqlclient` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![Caixa de diálogo Instalar Pacote](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="c73a9-166">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto, selecione **Python** e **Migrar Django**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="c73a9-167">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="c73a9-168">Isso criará as tabelas de banco de dados MySQL que você criou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="c73a9-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="c73a9-169">Siga os prompts para criar um usuário, que não tem de corresponder ao usuário no banco de dados sqlite criado na primeira seção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c73a9-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="c73a9-170">Execute o aplicativo com `F5`.</span><span class="sxs-lookup"><span data-stu-id="c73a9-170">Run the application with `F5`.</span></span> <span data-ttu-id="c73a9-171">As votações criadas com **Criar Votações de Exemplo** e os dados enviados por voto serão serializados no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="c73a9-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="c73a9-172">Publicar aplicativo Web para Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="c73a9-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="c73a9-173">O SDK .NET do Azure fornece uma forma fácil de implantar seu aplicativo Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a9-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="c73a9-174">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="c73a9-176">Clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="c73a9-177">Clique em **Novo** para criar um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c73a9-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="c73a9-178">Preencha os campos a seguir e clique em **Criar**:</span><span class="sxs-lookup"><span data-stu-id="c73a9-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="c73a9-179">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="c73a9-179">**Web App name**</span></span>
   * <span data-ttu-id="c73a9-180">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="c73a9-180">**App Service plan**</span></span>
   * <span data-ttu-id="c73a9-181">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="c73a9-181">**Resource group**</span></span>
   * <span data-ttu-id="c73a9-182">**Região**</span><span class="sxs-lookup"><span data-stu-id="c73a9-182">**Region**</span></span>
   * <span data-ttu-id="c73a9-183">Deixe **Servidor de banco de dados** definido como **Nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="c73a9-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="c73a9-184">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="c73a9-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="c73a9-185">Seu navegador da Web será aberto automaticamente para o aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="c73a9-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="c73a9-186">Você deve ver o aplicativo Web funcionando conforme o esperado, usando o banco de dados **MySQL** hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a9-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Navegador da Web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="c73a9-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="c73a9-188">Congratulations!</span></span> <span data-ttu-id="c73a9-189">Você publicou com êxito seu aplicativo Web com base em MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="c73a9-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c73a9-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c73a9-190">Next steps</span></span>
<span data-ttu-id="c73a9-191">Siga estas etapas para aprender mais sobre o Python Tools para Visual Studio, Django e MySQL.</span><span class="sxs-lookup"><span data-stu-id="c73a9-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="c73a9-192">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c73a9-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="c73a9-193">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="c73a9-193">[Web Projects]</span></span>
  * <span data-ttu-id="c73a9-194">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="c73a9-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="c73a9-195">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="c73a9-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="c73a9-196">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="c73a9-196">[Django Documentation]</span></span>
* <span data-ttu-id="c73a9-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="c73a9-197">[MySQL]</span></span>

<span data-ttu-id="c73a9-198">Para saber mais, consulte o [Centro de Desenvolvedores do Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c73a9-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python Developer Center]: /develop/python/
[Serviços de Nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portal do Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do Python 2.2 para Amostras VSIX do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentação do Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
