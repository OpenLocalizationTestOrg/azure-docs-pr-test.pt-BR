---
title: Django e Banco de Dados SQL no Azure com Ferramentas Python 2.2 para Visual Studio
description: "Aprenda a usar o Python Tools para Visual Studio para criar um aplicativo Django que armazena dados em uma instância do banco de dados SQL e o implanta em Aplicativos Web do Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e743e-103">Django e Banco de Dados SQL no Azure com Ferramentas Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e743e-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="e743e-104">Neste tutorial, usaremos o [Python Tools para Visual Studio] para criar um aplicativo Web de votação simples, usando um dos modelos de exemplo de PTVS.</span><span class="sxs-lookup"><span data-stu-id="e743e-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="e743e-105">Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="e743e-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="e743e-106">Aprenderemos como usar um banco de dados SQL hospedado no Azure, como configurar o aplicativo para usar um banco de dados SQL e como publicar o aplicativo Web em [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e743e-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e743e-107">Confira o [Centro de Desenvolvedores do Python] para obter mais artigos que abrangem o desenvolvimento de Aplicativos Web do Serviço de Aplicativo do Azure com PTVS usando as estruturas da Web Bottle, Flask e Django, com serviços do Armazenamento de Tabelas do Azure, MySQL e Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e743e-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="e743e-108">Embora este artigo se concentre no Serviço de Aplicativo, as etapas são semelhantes ao desenvolvimento de [Serviços de Nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="e743e-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e743e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e743e-109">Prerequisites</span></span>
* <span data-ttu-id="e743e-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e743e-110">Visual Studio 2015</span></span>
* <span data-ttu-id="e743e-111">[Python 2.7 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="e743e-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="e743e-112">[Ferramentas Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e743e-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e743e-113">[Ferramentas do Python 2.2 para Amostras VSIX do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e743e-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e743e-114">[Ferramentas do SDK do Azure para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="e743e-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e743e-115">Django 1.9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="e743e-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e743e-116">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e743e-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e743e-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="e743e-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="e743e-118">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="e743e-118">Create the Project</span></span>
<span data-ttu-id="e743e-119">Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra.</span><span class="sxs-lookup"><span data-stu-id="e743e-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e743e-120">Criaremos um ambiente virtual e instalaremos pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="e743e-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e743e-121">Criaremos um banco de dados local usando sqlite.</span><span class="sxs-lookup"><span data-stu-id="e743e-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="e743e-122">Em seguida, vamos executar o aplicativo Web localmente.</span><span class="sxs-lookup"><span data-stu-id="e743e-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="e743e-123">No Visual Studio, selecione **Arquivo**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e743e-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e743e-124">Os modelos de projeto das [Ferramentas do Python 2.2 para Amostras VSIX do Visual Studio] estão disponíveis em **Python**, **Amostras**.</span><span class="sxs-lookup"><span data-stu-id="e743e-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e743e-125">Selecione **Projeto Web Django de Votações** e clique em OK para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="e743e-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="e743e-127">Você será solicitado a instalar pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="e743e-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="e743e-128">Selecione **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="e743e-128">Select **Install into a virtual environment**.</span></span>

     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="e743e-130">Selecione **Python 2.7** como o interpretador de base.</span><span class="sxs-lookup"><span data-stu-id="e743e-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e743e-132">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto, selecione **Python** e **Migrar Django**.</span><span class="sxs-lookup"><span data-stu-id="e743e-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e743e-133">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="e743e-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="e743e-134">Isso abrirá um Console de Gerenciamento do Django e criará um banco de dados sqlite na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="e743e-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="e743e-135">Siga os prompts para criar um usuário.</span><span class="sxs-lookup"><span data-stu-id="e743e-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="e743e-136">Confirme se o aplicativo funciona pressionando <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="e743e-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="e743e-137">Clique em **Fazer logon** na barra de navegação na parte superior.</span><span class="sxs-lookup"><span data-stu-id="e743e-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="e743e-139">Insira as credenciais para o usuário que você criou quando sincronizou o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e743e-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="e743e-141">Clique em **Criar Votações de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="e743e-141">Click **Create Sample Polls**.</span></span>

      ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="e743e-143">Clique em uma pesquisa e vote.</span><span class="sxs-lookup"><span data-stu-id="e743e-143">Click on a poll and vote.</span></span>

      ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="e743e-145">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e743e-145">Create a SQL Database</span></span>
<span data-ttu-id="e743e-146">Para o banco de dados, vamos criar um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="e743e-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="e743e-147">Você pode criar um banco de dados seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="e743e-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="e743e-148">Faça logon no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="e743e-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="e743e-149">Na parte inferior do painel de navegação, clique em **NOVO**.</span><span class="sxs-lookup"><span data-stu-id="e743e-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="e743e-150">Clique em **Dados + Armazenamento** > **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="e743e-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="e743e-151">Configure o novo banco de dados SQL criando um novo grupo de recursos e selecione o local apropriado para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="e743e-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="e743e-152">Depois de criar o banco de dados SQL, clique em **Abrir no Visual Studio** na folha do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e743e-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="e743e-153">Clique em **Configurar seu firewall**.</span><span class="sxs-lookup"><span data-stu-id="e743e-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="e743e-154">Na folha **Configurações de Firewall**, adicione uma regra de firewall com **IP INICIAL** e **IP FINAL** definidos como o endereço IP público de seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e743e-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="e743e-155">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e743e-155">Click **Save**.</span></span>

   <span data-ttu-id="e743e-156">Isso permitirá conexões ao servidor de banco de dados em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e743e-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="e743e-157">Na folha do banco de dados, clique em **Propriedades** e em **Mostrar cadeias de conexão do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="e743e-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="e743e-158">É possível usar o botão de cópia para colocar o valor de **ADO.NET** na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="e743e-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="e743e-159">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="e743e-159">Configure the Project</span></span>
<span data-ttu-id="e743e-160">Nesta seção, configuraremos nosso aplicativo Web para usar o banco de dados SQL que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="e743e-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="e743e-161">Também instalaremos pacotes adicionais Python necessários para usar bancos de dados SQL com Django.</span><span class="sxs-lookup"><span data-stu-id="e743e-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="e743e-162">Em seguida, vamos executar o aplicativo Web localmente.</span><span class="sxs-lookup"><span data-stu-id="e743e-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="e743e-163">No Visual Studio, abra **settings.py**, na pasta *ProjectName* .</span><span class="sxs-lookup"><span data-stu-id="e743e-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="e743e-164">Cole temporariamente a cadeia de conexão obtida no editor.</span><span class="sxs-lookup"><span data-stu-id="e743e-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="e743e-165">A cadeia de conexão está neste formato:</span><span class="sxs-lookup"><span data-stu-id="e743e-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="e743e-166">Editar a definição de `DATABASES` para usar os valores acima.</span><span class="sxs-lookup"><span data-stu-id="e743e-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="e743e-167">No Gerenciador de Soluções, em **Ambientes Python**, clique com o botão direito do mouse no ambiente virtual e selecione **Instalar Pacote Python**.</span><span class="sxs-lookup"><span data-stu-id="e743e-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="e743e-168">Instale o pacote `pyodbc` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="e743e-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Caixa de diálogo Instalar Pacote Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="e743e-170">Instale o pacote `django-pyodbc-azure` usando **pip**.</span><span class="sxs-lookup"><span data-stu-id="e743e-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Caixa de diálogo Instalar Pacote Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="e743e-172">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto, selecione **Python** e **Migrar Django**.</span><span class="sxs-lookup"><span data-stu-id="e743e-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e743e-173">Em seguida, selecione **Criar Superusuário do Django**.</span><span class="sxs-lookup"><span data-stu-id="e743e-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="e743e-174">Isso criará as tabelas de banco de dados SQL que criamos na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="e743e-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="e743e-175">Siga os prompts para criar um usuário, que não tem de corresponder ao usuário no banco de dados sqlite criado na primeira seção.</span><span class="sxs-lookup"><span data-stu-id="e743e-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="e743e-176">Execute o aplicativo com `F5`.</span><span class="sxs-lookup"><span data-stu-id="e743e-176">Run the application with `F5`.</span></span> <span data-ttu-id="e743e-177">As votações criadas com **Criar Votações de Exemplo** e os dados enviados pela votação serão serializados no banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e743e-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="e743e-178">Publicar aplicativo Web para Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="e743e-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="e743e-179">O SDK .NET do Azure fornece uma forma fácil de implantar seu aplicativo Web Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="e743e-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="e743e-180">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e743e-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e743e-182">Clique em **Aplicativos Web do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e743e-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="e743e-183">Clique em **Novo** para criar um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e743e-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="e743e-184">Preencha os campos a seguir e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e743e-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="e743e-185">**Nome do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="e743e-185">**Web App name**</span></span>
   * <span data-ttu-id="e743e-186">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="e743e-186">**App Service plan**</span></span>
   * <span data-ttu-id="e743e-187">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="e743e-187">**Resource group**</span></span>
   * <span data-ttu-id="e743e-188">**Região**</span><span class="sxs-lookup"><span data-stu-id="e743e-188">**Region**</span></span>
   * <span data-ttu-id="e743e-189">Deixe **Servidor de banco de dados** definido como **Nenhum banco de dados**</span><span class="sxs-lookup"><span data-stu-id="e743e-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="e743e-190">Aceite todos os outros padrões e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e743e-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e743e-191">Seu navegador da Web será aberto automaticamente para o aplicativo Web publicado.</span><span class="sxs-lookup"><span data-stu-id="e743e-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="e743e-192">Você deve ver o aplicativo funcionando conforme o esperado, usando o banco de dados **SQL** hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="e743e-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="e743e-193">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e743e-193">Congratulations!</span></span>

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="e743e-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e743e-195">Next steps</span></span>
<span data-ttu-id="e743e-196">Siga estas etapas para aprender mais sobre o Python Tools para Visual Studio, Django e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e743e-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="e743e-197">[Ferramentas Python para documentação do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e743e-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e743e-198">[Projetos da Web]</span><span class="sxs-lookup"><span data-stu-id="e743e-198">[Web Projects]</span></span>
  * <span data-ttu-id="e743e-199">[Projetos do serviço de nuvem]</span><span class="sxs-lookup"><span data-stu-id="e743e-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e743e-200">[Depuração remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e743e-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e743e-201">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="e743e-201">[Django Documentation]</span></span>
* <span data-ttu-id="e743e-202">[Banco de Dados SQL]</span><span class="sxs-lookup"><span data-stu-id="e743e-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e743e-203">O que mudou</span><span class="sxs-lookup"><span data-stu-id="e743e-203">What's changed</span></span>
* <span data-ttu-id="e743e-204">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e743e-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="e743e-205">[Centro de Desenvolvedores do Python]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="e743e-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="e743e-206">[Serviços de Nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="e743e-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="e743e-207">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e743e-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="e743e-208">[Python Tools para Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="e743e-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="e743e-209">[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="e743e-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="e743e-210">[Ferramentas do Python 2.2 para Amostras VSIX do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="e743e-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="e743e-211">[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="e743e-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="e743e-212">[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="e743e-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="e743e-213">[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="e743e-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="e743e-214">[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="e743e-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="e743e-215">[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="e743e-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="e743e-216">[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="e743e-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="e743e-217">[Documentação do Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="e743e-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="e743e-218">[Banco de Dados SQL]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="e743e-218">[SQL Database]: /documentation/services/sql-database/</span></span>
