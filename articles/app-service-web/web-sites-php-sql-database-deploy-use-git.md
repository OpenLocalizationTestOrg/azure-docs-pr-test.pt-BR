---
title: "aaaCreate um SQL do PHP aplicativo da web e implantar tooAzure do serviço de aplicativo usando o Git"
description: "Um tutorial que demonstra como toocreate um PHP web aplicativo que armazena dados no banco de dados do SQL Azure e usar tooAzure de implantação do Git do serviço de aplicativo."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="e0bd9-103">Criar um aplicativo web do SQL do PHP e implantar tooAzure do serviço de aplicativo usando o Git</span><span class="sxs-lookup"><span data-stu-id="e0bd9-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="e0bd9-104">Este tutorial mostra como toocreate um PHP web app [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que se conecta tooAzure banco de dados SQL e como toodeploy usando Git.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="e0bd9-105">Este tutorial presume que você tenha [PHP][install-php], [SQL Server Express][install-SQLExpress], Olá [Drivers da Microsoft para SQL Server para PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), e [Git] [ install-git] instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="e0bd9-106">Após a conclusão deste guia, você terá um aplicativo Web PHP/SQL em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e0bd9-107">Você pode instalar e configurar o PHP, SQL Server Express e Olá Drivers da Microsoft para SQL Server para PHP usando Olá [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0bd9-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="e0bd9-108">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-108">You will learn:</span></span>

* <span data-ttu-id="e0bd9-109">Como toocreate um Azure web app e um banco de dados SQL usando Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="e0bd9-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="e0bd9-110">Como PHP está habilitado no serviço de aplicativo Web de aplicativos, por padrão, nada de especial é necessário toorun seu código PHP.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="e0bd9-111">Como toopublish e publicar novamente o tooAzure de aplicativo usando o Git.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="e0bd9-112">Seguindo este tutorial, você irá criar um aplicativo da web de registro simples no PHP.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="e0bd9-113">aplicativo Hello será hospedado em um site do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="e0bd9-114">É uma captura de tela do aplicativo hello concluída abaixo:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-114">A screenshot of hello completed application is below:</span></span>

![Site PHP do Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e0bd9-116">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e0bd9-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="e0bd9-118">Criar um aplicativo Web do Azure e configurar a publicação Git</span><span class="sxs-lookup"><span data-stu-id="e0bd9-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="e0bd9-119">Siga essas etapas toocreate um aplicativo web do Azure e um banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="e0bd9-120">Faça logon no toohello [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e0bd9-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e0bd9-121">Abra hello Azure Marketplace clicando Olá **novo** ícone no início de saudação à esquerda do painel de saudação, clique em **Selecionar tudo** tooMarketplace Avançar e selecionando **Web + móvel**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="e0bd9-122">No hello Marketplace, selecione **Web + móvel**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="e0bd9-123">Clique em Olá **Web app + SQL** ícone.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="e0bd9-124">Depois de ler a descrição de saudação do aplicativo Web de saudação + SQL aplicativo, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="e0bd9-125">Clique em cada parte (**grupo de recursos**, **aplicativo Web**, **banco de dados**, e **assinatura**) e insira ou selecione valores para Olá necessária campos:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="e0bd9-126">Insira um nome de URL de sua escolha</span><span class="sxs-lookup"><span data-stu-id="e0bd9-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="e0bd9-127">Configurar credenciais de servidor de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e0bd9-127">Configure database server credentials</span></span>
   * <span data-ttu-id="e0bd9-128">Selecione Olá região mais próxima tooyou</span><span class="sxs-lookup"><span data-stu-id="e0bd9-128">Select hello region closest tooyou</span></span>
     
     ![configurar o aplicativo](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="e0bd9-130">Quando terminar de definir o aplicativo web de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="e0bd9-131">Quando o aplicativo da web de saudação tiver sido criado, Olá **notificações** botão pisca uma verde **êxito** e Olá recurso grupo folha abrir tooshow ambos os Olá web app e hello banco de dados SQL no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="e0bd9-132">Clique em ícone do aplicativo da web de saudação na folha de saudação recurso grupo folha tooopen saudação do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![grupo de recursos do aplicativo Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="e0bd9-134">Em **Configurações**, clique em **Implantação contínua** > **Definir configurações necessárias**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="e0bd9-135">Selecione **Repositório Git local** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![onde está o código-fonte](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="e0bd9-137">Se não tiver configurado um repositório Git antes, você deverá fornecer um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="e0bd9-138">toodo, clique **configurações** > **credenciais de implantação** na folha do aplicativo da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="e0bd9-139">Em **configurações** clique em **propriedades** toosee Olá Git remoto URL precisar toouse toodeploy seu aplicativo PHP mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="e0bd9-140">Obter informações da conexão do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="e0bd9-140">Get SQL Database connection information</span></span>
<span data-ttu-id="e0bd9-141">instância de banco de dados SQL do toohello tooconnect é vinculada tooyour web app, o será necessário Olá informações de conexão, o que você especificou quando criou o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="e0bd9-142">Olá tooget informações de conexão de banco de dados SQL, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="e0bd9-143">Na folha do grupo de recursos hello, clique em ícone Olá SQL do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="e0bd9-144">Na folha de saudação SQL do banco de dados, clique em **configurações** > **propriedades**, em seguida, clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Exibir propriedades do banco de dados](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="e0bd9-146">De saudação **PHP** seção da caixa de diálogo resultante hello, anote os valores hello para `Server`, `SQL Database`, e `User Name`.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="e0bd9-147">Você usará esses valores posteriormente quando publicar seu tooAzure de aplicativo web do PHP do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="e0bd9-148">Criar e testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="e0bd9-148">Build and test your application locally</span></span>
<span data-ttu-id="e0bd9-149">Olá aplicativo de registro é um aplicativo simples do PHP que permite que você tooregister para um evento, fornecendo seu nome e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="e0bd9-150">As informações sobre inscritos anteriores são exibidas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="e0bd9-151">As informações de registro são armazenadas em uma instância do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="e0bd9-152">aplicativo Hello consiste em dois arquivos (código de copiar/colar disponível abaixo):</span><span class="sxs-lookup"><span data-stu-id="e0bd9-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="e0bd9-153">**index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="e0bd9-154">**CreateTable.PHP**: cria a tabela de banco de dados SQL Olá para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="e0bd9-155">Este arquivo será usado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-155">This file will only be used once.</span></span>

<span data-ttu-id="e0bd9-156">aplicativo de hello toorun localmente, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="e0bd9-157">Observe que essas etapas pressupõem ter PHP e SQL Server Express configurado no seu computador local e que você tenha ativado Olá [extensão PDO para SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="e0bd9-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="e0bd9-158">Crie um Banco de Dados SQL chamado `registration`.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="e0bd9-159">Você pode fazer isso de saudação `sqlcmd` prompt de comando com esses comandos:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="e0bd9-160">No diretório raiz de seu aplicativo, crie dois arquivos: um chamado `createtable.php` e outro chamado `index.php`.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="e0bd9-161">Olá abrir `createtable.php` arquivo em um editor de texto ou o IDE e adicione Olá código abaixo.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="e0bd9-162">Esse código será usado toocreate Olá `registration_tbl` tabela Olá `registration` banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="e0bd9-163">Observe que você precisará valores hello tooupdate <code>$user</code> e <code>$pwd</code> com seu nome de usuário do SQL Server local e a senha.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="e0bd9-164">Em um terminal no diretório raiz de saudação de saudação de tipo de aplicativo hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="e0bd9-165">Abra um navegador da web e navegue muito**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="e0bd9-166">Isso criará Olá `registration_tbl` tabela no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="e0bd9-167">Olá abrir **index.php** de arquivos em um editor de texto ou o IDE e adicionar Olá HTML e CSS código básico para a página de saudação (Olá código PHP será adicionado em etapas posteriores).</span><span class="sxs-lookup"><span data-stu-id="e0bd9-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="e0bd9-168">Nas marcas PHP de hello, adicione o código PHP para a conexão de banco de dados toohello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="e0bd9-169">Novamente, você precisará valores hello tooupdate <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="e0bd9-170">Após o código de conexão de banco de dados hello, adicione código para inserir informações de registro no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="e0bd9-171">Por fim, seguindo o código Olá acima, adicione código para recuperar dados do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="e0bd9-172">Agora você pode procurar muito**http://localhost:8000/index.php** tootest aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="e0bd9-173">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e0bd9-173">Publish your application</span></span>
<span data-ttu-id="e0bd9-174">Depois de testar seu aplicativo localmente, você pode publicar aplicativos Web do serviço tooApp usando o Git.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="e0bd9-175">No entanto, você primeiro precisa de informações de conexão de banco de dados tooupdate Olá no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="e0bd9-176">Usando informações de conexão de banco de dados Olá obtidos anteriormente (no hello **informações de conexão de banco de dados de SQL obter** seção), atualização Olá informações a seguir **ambos** Olá `createdatabase.php` e `index.php` valores adequados de arquivos com hello:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="e0bd9-177">Em Olá <code>$host</code>, valor de saudação do servidor deve ser precedida com <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="e0bd9-178">Agora, você está pronto tooset a publicação no Git e publica o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="e0bd9-179">Esses são Olá mesmas etapas observadas no fim de saudação do hello **criar um aplicativo web do Azure e configurar a publicação de Git** seção acima.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="e0bd9-180">Abrir GitBash (ou um terminal, se for Git no seu `PATH`), alterar diretórios toohello diretório de raiz do seu aplicativo (Olá **registro** directory), e execução Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="e0bd9-181">Você será solicitado para senha Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="e0bd9-182">Procurar muito**http://[web aplicativo name].azurewebsites.net/createtable.php** toocreate tabela de banco de dados SQL Olá para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="e0bd9-183">Procurar muito**http://[web aplicativo name].azurewebsites.net/index.php** toobegin usando o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="e0bd9-184">Depois de publicar seu aplicativo, você pode começar a fazer alterações tooit e usar o Git toopublish-los.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="e0bd9-185">Publicar alterações tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="e0bd9-185">Publish changes tooyour application</span></span>
<span data-ttu-id="e0bd9-186">toopublish altera tooapplication, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="e0bd9-187">Faça alterações tooyour aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="e0bd9-188">Abra GitBash (ou um terminal it Git está no seu `PATH`), altere o diretório de raiz de toohello de diretórios do seu aplicativo e executar Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0bd9-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="e0bd9-189">Você será solicitado para senha Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="e0bd9-190">Procurar muito**http://[web aplicativo name].azurewebsites.net/index.php** toosee suas alterações.</span><span class="sxs-lookup"><span data-stu-id="e0bd9-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e0bd9-191">O que mudou</span><span class="sxs-lookup"><span data-stu-id="e0bd9-191">What's changed</span></span>
* <span data-ttu-id="e0bd9-192">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e0bd9-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

