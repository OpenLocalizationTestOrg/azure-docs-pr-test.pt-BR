---
title: aaaDjango e banco de dados do SQL Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo web Django que armazena dados em uma instância do banco de dados SQL e implantá-lo tooAzure aplicativos de Web do serviço de aplicativo."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="8bd18-103">Django e Banco de Dados SQL no Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8bd18-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="8bd18-104">Neste tutorial, vamos usar [ferramentas Python para Visual Studio] toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="8bd18-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="8bd18-105">Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="8bd18-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="8bd18-106">Aprenderemos como toouse um banco de dados SQL hospedado no Azure, como tooconfigure Olá toouse de aplicativo da web a um banco de dados do SQL e como toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="8bd18-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="8bd18-107">Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com serviços de armazenamento de tabela do Azure, MySQL e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="8bd18-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="8bd18-108">Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="8bd18-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bd18-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8bd18-109">Prerequisites</span></span>
* <span data-ttu-id="8bd18-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8bd18-110">Visual Studio 2015</span></span>
* <span data-ttu-id="8bd18-111">[Python 2.7 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="8bd18-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="8bd18-112">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8bd18-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="8bd18-113">[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8bd18-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="8bd18-114">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="8bd18-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="8bd18-115">Django 1.9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="8bd18-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="8bd18-116">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8bd18-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8bd18-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="8bd18-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="8bd18-118">Criar hello projeto</span><span class="sxs-lookup"><span data-stu-id="8bd18-118">Create hello Project</span></span>
<span data-ttu-id="8bd18-119">Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="8bd18-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="8bd18-120">Criaremos um ambiente virtual e instalaremos pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="8bd18-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="8bd18-121">Criaremos um banco de dados local usando sqlite.</span><span class="sxs-lookup"><span data-stu-id="8bd18-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="8bd18-122">Em seguida, vamos executar Olá web aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="8bd18-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="8bd18-123">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="8bd18-124">Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="8bd18-125">Selecione **sondagens Django Web projeto** e clique em projeto de saudação toocreate Okey.</span><span class="sxs-lookup"><span data-stu-id="8bd18-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="8bd18-127">Você será pacotes externos tooinstall solicitada.</span><span class="sxs-lookup"><span data-stu-id="8bd18-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="8bd18-128">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-128">Select **Install into a virtual environment**.</span></span>

     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="8bd18-130">Selecione **Python 2.7** como interpretador base hello.</span><span class="sxs-lookup"><span data-stu-id="8bd18-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="8bd18-132">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="8bd18-133">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="8bd18-134">Isso abra um Console de gerenciamento Django e criará um banco de dados sqlite na pasta de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="8bd18-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="8bd18-135">Siga Olá prompts toocreate um usuário.</span><span class="sxs-lookup"><span data-stu-id="8bd18-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="8bd18-136">Confirme se o aplicativo hello funciona pressionando <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="8bd18-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="8bd18-137">Clique em **login** Olá na barra de navegação na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="8bd18-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="8bd18-139">Insira as credenciais de saudação para usuário Olá criado quando você sincroniza o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bd18-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="8bd18-141">Clique em **Criar Votações de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-141">Click **Create Sample Polls**.</span></span>

      ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="8bd18-143">Clique em uma pesquisa e vote.</span><span class="sxs-lookup"><span data-stu-id="8bd18-143">Click on a poll and vote.</span></span>

      ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="8bd18-145">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="8bd18-145">Create a SQL Database</span></span>
<span data-ttu-id="8bd18-146">Banco de dados Olá, vamos criar um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd18-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="8bd18-147">Você pode criar um banco de dados seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="8bd18-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="8bd18-148">Faça logon no hello [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="8bd18-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="8bd18-149">Na parte inferior do Olá Olá do painel de navegação, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="8bd18-150">Clique em **Dados + Armazenamento** > **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="8bd18-151">Configurar Olá novo banco de dados SQL, criando um novo grupo de recursos e selecione Olá local apropriado para ele.</span><span class="sxs-lookup"><span data-stu-id="8bd18-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="8bd18-152">Depois de criar hello banco de dados SQL, clique em **aberto no Visual Studio** na folha do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bd18-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="8bd18-153">Clique em **Configurar seu firewall**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="8bd18-154">Em Olá **as configurações do Firewall** folha, adicionar uma regra de firewall com **IP inicial** e **IP final** definir toohello de endereço IP público de sua máquina de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="8bd18-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="8bd18-155">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-155">Click **Save**.</span></span>

   <span data-ttu-id="8bd18-156">Isso permitirá que o servidor de banco de dados de toohello de conexões do computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="8bd18-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="8bd18-157">Na folha do banco de dados de saudação, clique em **propriedades**, em seguida, clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="8bd18-158">Use Olá cópia botão tooput Olá valor **ADO.NET** na área de transferência hello.</span><span class="sxs-lookup"><span data-stu-id="8bd18-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="8bd18-159">Configurar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="8bd18-159">Configure hello Project</span></span>
<span data-ttu-id="8bd18-160">Nesta seção, configuraremos nosso web aplicativo toouse Olá banco de dados SQL que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="8bd18-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="8bd18-161">Também instalaremos adicionais Python pacotes necessários toouse bancos de dados SQL com Django.</span><span class="sxs-lookup"><span data-stu-id="8bd18-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="8bd18-162">Em seguida, vamos executar Olá web aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="8bd18-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="8bd18-163">No Visual Studio, abra **settings.py**, da saudação *ProjectName* pasta.</span><span class="sxs-lookup"><span data-stu-id="8bd18-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="8bd18-164">Temporariamente cole a cadeia de caracteres de conexão de saudação no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bd18-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="8bd18-165">cadeia de caracteres de conexão de saudação é neste formato:</span><span class="sxs-lookup"><span data-stu-id="8bd18-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="8bd18-166">Editar definição de saudação do `DATABASES` valores de saudação toouse acima.</span><span class="sxs-lookup"><span data-stu-id="8bd18-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="8bd18-167">No Gerenciador de soluções, em **Python ambientes**, com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="8bd18-168">Instalar o pacote de saudação `pyodbc` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Caixa de diálogo Instalar Pacote Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="8bd18-170">Instalar o pacote de saudação `django-pyodbc-azure` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Caixa de diálogo Instalar Pacote Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="8bd18-172">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="8bd18-173">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="8bd18-174">Isso cria tabelas de saudação do banco de dados do SQL Olá criada na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="8bd18-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="8bd18-175">Siga Olá prompts toocreate um usuário, que não tem um usuário de saudação toomatch no banco de dados sqlite Olá criado na primeira seção do hello.</span><span class="sxs-lookup"><span data-stu-id="8bd18-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="8bd18-176">Executar o aplicativo hello com `F5`.</span><span class="sxs-lookup"><span data-stu-id="8bd18-176">Run hello application with `F5`.</span></span> <span data-ttu-id="8bd18-177">Pesquisas que são criadas com **criar pesquisas de exemplo** e dados de saudação enviados ao votar serão serializados no banco de dados SQL Olá.</span><span class="sxs-lookup"><span data-stu-id="8bd18-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="8bd18-178">Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="8bd18-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="8bd18-179">Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo de web serviço de aplicativo Web de aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="8bd18-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="8bd18-180">Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="8bd18-182">Clique em **Aplicativos Web do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="8bd18-183">Clique em **novo** toocreate um novo aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="8bd18-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="8bd18-184">Preencha Olá campos a seguir e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="8bd18-185">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="8bd18-185">**Web App name**</span></span>
   * <span data-ttu-id="8bd18-186">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="8bd18-186">**App Service plan**</span></span>
   * <span data-ttu-id="8bd18-187">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="8bd18-187">**Resource group**</span></span>
   * <span data-ttu-id="8bd18-188">**Região**</span><span class="sxs-lookup"><span data-stu-id="8bd18-188">**Region**</span></span>
   * <span data-ttu-id="8bd18-189">Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="8bd18-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="8bd18-190">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="8bd18-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="8bd18-191">Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados.</span><span class="sxs-lookup"><span data-stu-id="8bd18-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="8bd18-192">Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **SQL** banco de dados hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd18-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="8bd18-193">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="8bd18-193">Congratulations!</span></span>

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="8bd18-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8bd18-195">Next steps</span></span>
<span data-ttu-id="8bd18-196">Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, Django e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="8bd18-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="8bd18-197">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8bd18-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="8bd18-198">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="8bd18-198">[Web Projects]</span></span>
  * <span data-ttu-id="8bd18-199">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="8bd18-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="8bd18-200">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="8bd18-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="8bd18-201">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="8bd18-201">[Django Documentation]</span></span>
* <span data-ttu-id="8bd18-202">[Banco de Dados SQL]</span><span class="sxs-lookup"><span data-stu-id="8bd18-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8bd18-203">O que mudou</span><span class="sxs-lookup"><span data-stu-id="8bd18-203">What's changed</span></span>
* <span data-ttu-id="8bd18-204">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8bd18-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Portal do Azure]: https://portal.azure.com
[ferramentas Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentação do Django]: https://www.djangoproject.com/
[Banco de Dados SQL]: /documentation/services/sql-database/
