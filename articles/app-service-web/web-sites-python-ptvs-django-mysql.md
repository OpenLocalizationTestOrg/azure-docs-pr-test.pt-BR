---
title: aaaDjango e MySQL no Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo web Django que armazena dados em uma instância de banco de dados MySQL e implantá-lo tooAzure aplicativos de Web do serviço de aplicativo."
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
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="89410-103">Django e MySQL no Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89410-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="89410-104">Neste tutorial, você usará [ferramentas Python para Visual Studio](https://www.visualstudio.com/vs/python) toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="89410-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="89410-105">Você aprenderá como toouse um serviço do MySQL hospedados no Azure, como tooconfigure Olá web aplicativo toouse MySQL e como toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="89410-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="89410-106">informações de saudação contidas neste tutorial também estão disponíveis no hello vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="89410-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="89410-107">[PTVS 2.1: aplicativo do Django com o MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="89410-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="89410-108">Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com serviços de armazenamento de tabela do Azure, MySQL e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="89410-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="89410-109">Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="89410-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89410-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89410-110">Prerequisites</span></span>
* <span data-ttu-id="89410-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="89410-111">Visual Studio 2015</span></span>
* <span data-ttu-id="89410-112">[Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="89410-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="89410-113">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="89410-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="89410-114">[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="89410-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="89410-115">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="89410-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="89410-116">Django 1.9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="89410-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="89410-117">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89410-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="89410-118">Nenhum cartão de crédito é exigido e não há compromissos.</span><span class="sxs-lookup"><span data-stu-id="89410-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="89410-119">Criar hello projeto</span><span class="sxs-lookup"><span data-stu-id="89410-119">Create hello Project</span></span>
<span data-ttu-id="89410-120">Nesta seção, criaremos um projeto do Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="89410-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="89410-121">Você irá criar um ambiente virtual e instalará os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="89410-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="89410-122">Você irá criar um banco de dados local usando sqlite.</span><span class="sxs-lookup"><span data-stu-id="89410-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="89410-123">Em seguida, você executará o aplicativo hello localmente.</span><span class="sxs-lookup"><span data-stu-id="89410-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="89410-124">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="89410-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="89410-125">Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**.</span><span class="sxs-lookup"><span data-stu-id="89410-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="89410-126">Selecione **sondagens Django Web projeto** e clique em projeto de saudação toocreate Okey.</span><span class="sxs-lookup"><span data-stu-id="89410-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="89410-128">Você será pacotes externos tooinstall solicitada.</span><span class="sxs-lookup"><span data-stu-id="89410-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="89410-129">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="89410-129">Select **Install into a virtual environment**.</span></span>
   
    ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="89410-131">Selecione **Python 2.7** ou **Python 3.4** como interpretador base hello.</span><span class="sxs-lookup"><span data-stu-id="89410-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="89410-133">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="89410-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="89410-134">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="89410-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="89410-135">Isso abra um Console de gerenciamento Django e criará um banco de dados sqlite na pasta de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="89410-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="89410-136">Siga Olá prompts toocreate um usuário.</span><span class="sxs-lookup"><span data-stu-id="89410-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="89410-137">Confirme se o aplicativo hello funciona pressionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="89410-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="89410-138">Clique em **login** Olá na barra de navegação na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="89410-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Barra de navegação do Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="89410-140">Insira as credenciais de saudação para usuário Olá criado quando você sincroniza o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="89410-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Formulário de logon](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="89410-142">Clique em **Criar Votações de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="89410-142">Click **Create Sample Polls**.</span></span>
    
     ![Criar Votações de Exemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="89410-144">Clique em uma pesquisa e vote.</span><span class="sxs-lookup"><span data-stu-id="89410-144">Click on a poll and vote.</span></span>
    
     ![Votação em votações de exemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="89410-146">Criar um banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="89410-146">Create a MySQL Database</span></span>
<span data-ttu-id="89410-147">Banco de dados hello, você criará um banco de dados ClearDB MySQL hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="89410-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="89410-148">Como alternativa, você pode criar sua própria máquina virtual em execução no Azure, em seguida, instalar e administrar o MySQL por conta própria.</span><span class="sxs-lookup"><span data-stu-id="89410-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="89410-149">Você pode criar um banco de dados com um plano grátis seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="89410-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="89410-150">Faça logon no toohello [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89410-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="89410-151">Na Olá superior do painel de navegação de saudação, clique em **novo**, em seguida, clique em **dados + armazenamento**e, em seguida, clique em **banco de dados MySQL**.</span><span class="sxs-lookup"><span data-stu-id="89410-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="89410-152">Configurar Olá novo MySQL banco de dados, criando um novo grupo de recursos e selecione o local apropriado do Olá para ele.</span><span class="sxs-lookup"><span data-stu-id="89410-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="89410-153">Depois que o banco de dados do hello MySQL é criado, clique em **propriedades** na folha do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="89410-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="89410-154">Use Olá cópia botão tooput Olá valor **cadeia de conexão** na área de transferência hello.</span><span class="sxs-lookup"><span data-stu-id="89410-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="89410-155">Configurar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="89410-155">Configure hello Project</span></span>
<span data-ttu-id="89410-156">Nesta seção, você vai configurar o nosso aplicativo toouse Olá MySQL banco de dados web que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="89410-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="89410-157">Você também instalará o Python pacotes necessários toouse MySQL bancos de dados adicionais com Django.</span><span class="sxs-lookup"><span data-stu-id="89410-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="89410-158">Em seguida, você executará Olá web aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="89410-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="89410-159">No Visual Studio, abra **settings.py**, da saudação *ProjectName* pasta.</span><span class="sxs-lookup"><span data-stu-id="89410-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="89410-160">Temporariamente cole a cadeia de caracteres de conexão de saudação no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="89410-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="89410-161">cadeia de caracteres de conexão de saudação é neste formato:</span><span class="sxs-lookup"><span data-stu-id="89410-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="89410-162">Alterar banco de dados de padrão de saudação **mecanismo** toouse MySQL e defina Olá valores para **nome**, **usuário**, **senha** e  **HOST** de saudação **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="89410-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="89410-163">No Gerenciador de soluções, em **Python ambientes**, com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.</span><span class="sxs-lookup"><span data-stu-id="89410-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="89410-164">Instalar o pacote de saudação `mysqlclient` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="89410-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Caixa de diálogo Instalar Pacote](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="89410-166">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="89410-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="89410-167">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="89410-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="89410-168">Isso cria tabelas de saudação do banco de dados MySQL Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="89410-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="89410-169">Siga Olá prompts toocreate um usuário, que não tem um usuário de saudação toomatch no banco de dados sqlite Olá criado na primeira seção Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="89410-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="89410-170">Executar o aplicativo hello com `F5`.</span><span class="sxs-lookup"><span data-stu-id="89410-170">Run hello application with `F5`.</span></span> <span data-ttu-id="89410-171">Pesquisas que são criadas com **criar pesquisas de exemplo** e dados saudação enviados ao votar serão serializados no banco de dados do hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="89410-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="89410-172">Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="89410-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="89410-173">Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89410-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="89410-174">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="89410-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="89410-176">Clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="89410-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="89410-177">Clique em **novo** toocreate um novo aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="89410-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="89410-178">Preencha Olá campos a seguir e clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="89410-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="89410-179">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="89410-179">**Web App name**</span></span>
   * <span data-ttu-id="89410-180">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="89410-180">**App Service plan**</span></span>
   * <span data-ttu-id="89410-181">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="89410-181">**Resource group**</span></span>
   * <span data-ttu-id="89410-182">**Região**</span><span class="sxs-lookup"><span data-stu-id="89410-182">**Region**</span></span>
   * <span data-ttu-id="89410-183">Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="89410-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="89410-184">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="89410-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="89410-185">Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados.</span><span class="sxs-lookup"><span data-stu-id="89410-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="89410-186">Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **MySQL** banco de dados hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="89410-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Navegador da Web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="89410-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="89410-188">Congratulations!</span></span> <span data-ttu-id="89410-189">Você publicou com êxito sua tooAzure de aplicativo web com base em MySQL.</span><span class="sxs-lookup"><span data-stu-id="89410-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89410-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89410-190">Next steps</span></span>
<span data-ttu-id="89410-191">Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, Django e MySQL.</span><span class="sxs-lookup"><span data-stu-id="89410-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="89410-192">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="89410-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="89410-193">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="89410-193">[Web Projects]</span></span>
  * <span data-ttu-id="89410-194">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="89410-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="89410-195">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="89410-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="89410-196">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="89410-196">[Django Documentation]</span></span>
* <span data-ttu-id="89410-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="89410-197">[MySQL]</span></span>

<span data-ttu-id="89410-198">Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="89410-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portal do Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
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
