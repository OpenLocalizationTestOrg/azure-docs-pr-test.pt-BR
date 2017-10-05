---
title: "Criar um aplicativo Web PHP-SQL e implantá-lo no Serviço de Aplicativo do Azure usando Git"
description: "Um tutorial que demonstra como criar um aplicativo Web do PHP que armazena dados no Banco de Dados SQL do Azure e usa a implantação do Git para o Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="668de-103">Criar um aplicativo Web PHP-SQL e implantá-lo no Serviço de Aplicativo do Azure usando Git</span><span class="sxs-lookup"><span data-stu-id="668de-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="668de-104">Este tutorial mostra como criar um aplicativo web do PHP no [serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que se conecta ao banco de dados SQL do Azure e como implantá-lo usando o Git.</span><span class="sxs-lookup"><span data-stu-id="668de-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="668de-105">Este tutorial presume que você tenha [PHP][install-php], [SQL Server Express][install-SQLExpress], [Drivers da Microsoft para SQL Server para PHP](http://www.microsoft.com/download/en/details.aspx?id=20098) e [Git][install-git] instalados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="668de-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="668de-106">Após a conclusão deste guia, você terá um aplicativo Web PHP/SQL em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="668de-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="668de-107">É possível instalar e configurar PHP, SQL Server Express, os Drivers da Microsoft para SQL Server para PHP usando o [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="668de-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="668de-108">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="668de-108">You will learn:</span></span>

* <span data-ttu-id="668de-109">Como criar um aplicativo Web do Azure e um banco de dados SQL usando o [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="668de-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="668de-110">Já que o PHP está habilitado nos Aplicativos Web do Serviço de Aplicativo por padrão, não é necessário nada de especial para executar seu código PHP.</span><span class="sxs-lookup"><span data-stu-id="668de-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="668de-111">Como publicar e publicar novamente o aplicativo no Azure usando o Git.</span><span class="sxs-lookup"><span data-stu-id="668de-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="668de-112">Seguindo este tutorial, você irá criar um aplicativo da web de registro simples no PHP.</span><span class="sxs-lookup"><span data-stu-id="668de-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="668de-113">O aplicativo será hospedado em um Site do Azure.</span><span class="sxs-lookup"><span data-stu-id="668de-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="668de-114">Abaixo, uma captura de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="668de-114">A screenshot of the completed application is below:</span></span>

![Site PHP do Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="668de-116">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="668de-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="668de-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="668de-118">Criar um aplicativo Web do Azure e configurar a publicação Git</span><span class="sxs-lookup"><span data-stu-id="668de-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="668de-119">Siga estas etapas para criar um aplicativo Web do Azure e um banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="668de-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="668de-120">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="668de-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="668de-121">Abra o Azure Marketplace clicando no ícone **Novo** no lado superior esquerdo do painel, clique em **Selecionar Tudo** próximo a Marketplace e selecione **Web + Móvel**.</span><span class="sxs-lookup"><span data-stu-id="668de-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="668de-122">No Marketplace, selecione **Web + Móvel**.</span><span class="sxs-lookup"><span data-stu-id="668de-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="668de-123">Clique no ícone **Aplicativo Web + SQL** .</span><span class="sxs-lookup"><span data-stu-id="668de-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="668de-124">Depois de ler a descrição do aplicativo Web + aplicativo SQL, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="668de-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="668de-125">Clique em cada parte (**Grupo de Recursos**, **Aplicativo Web**, **Banco de Dados** e **Assinatura**) e insira ou selecione valores para os campos obrigatórios:</span><span class="sxs-lookup"><span data-stu-id="668de-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="668de-126">Insira um nome de URL de sua escolha</span><span class="sxs-lookup"><span data-stu-id="668de-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="668de-127">Configurar credenciais de servidor de banco de dados</span><span class="sxs-lookup"><span data-stu-id="668de-127">Configure database server credentials</span></span>
   * <span data-ttu-id="668de-128">Selecione a região mais próxima de você</span><span class="sxs-lookup"><span data-stu-id="668de-128">Select the region closest to you</span></span>
     
     ![configurar o aplicativo](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="668de-130">Quando terminar de definir o aplicativo Web, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="668de-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="668de-131">Quando o aplicativo Web tiver sido criado, o botão **Notificações** piscará **SUCESSO** em verde e abrirá a folha do grupo de recursos para exibir o aplicativo Web e o banco de dados SQL no grupo.</span><span class="sxs-lookup"><span data-stu-id="668de-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="668de-132">Clique no ícone do aplicativo Web na folha do grupo de recursos para abrir a folha do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="668de-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![grupo de recursos do aplicativo Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="668de-134">Em **Configurações**, clique em **Implantação contínua** > **Definir configurações necessárias**.</span><span class="sxs-lookup"><span data-stu-id="668de-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="668de-135">Selecione **Repositório Git local** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="668de-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![onde está o código-fonte](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="668de-137">Se não tiver configurado um repositório Git antes, você deverá fornecer um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="668de-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="668de-138">Para fazer isso, clique em **Configurações** > **Credenciais de implantação** na folha do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="668de-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="668de-139">Em **Configurações**, clique em **Propriedades** para ver a URL remota do Git que você precisa usar para implantar seu aplicativo PHP posteriormente.</span><span class="sxs-lookup"><span data-stu-id="668de-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="668de-140">Obter informações da conexão do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="668de-140">Get SQL Database connection information</span></span>
<span data-ttu-id="668de-141">Para se conectar à instância do banco de dados SQL que está vinculada a seu aplicativo Web, você precisa das informações de conexão, que especificou ao criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="668de-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="668de-142">Para obter informações sobre a conexão do Banco de Dados SQL, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="668de-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="668de-143">Na folha do grupo de recursos, clique no ícone do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="668de-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="668de-144">Na folha do banco de dados SQL, clique em **Configurações** > **Propriedades** e clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="668de-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Exibir propriedades do banco de dados](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="668de-146">Na seção **PHP** da caixa de diálogo resultante, anote os valores de `Server`, `SQL Database` e `User Name`.</span><span class="sxs-lookup"><span data-stu-id="668de-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="668de-147">Você usará posteriormente esses valores ao publicar seu aplicativo Web do PHP para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="668de-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="668de-148">Criar e testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="668de-148">Build and test your application locally</span></span>
<span data-ttu-id="668de-149">O aplicativo Registro é um aplicativo simples do PHP que permite que você se registre em um evento fornecendo seu nome e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="668de-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="668de-150">As informações sobre inscritos anteriores são exibidas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="668de-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="668de-151">As informações de registro são armazenadas em uma instância do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="668de-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="668de-152">O aplicativo consiste em dois arquivos (copie/cole o código disponível abaixo):</span><span class="sxs-lookup"><span data-stu-id="668de-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="668de-153">**index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.</span><span class="sxs-lookup"><span data-stu-id="668de-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="668de-154">**createtable.php**: cria a tabela de Banco de Dados SQL para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="668de-155">Este arquivo será usado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="668de-155">This file will only be used once.</span></span>

<span data-ttu-id="668de-156">Para executar o aplicativo localmente, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="668de-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="668de-157">Observe que essas etapas pressupõem que você tem PHP e SQL Server Express definidos em sua máquina local, e que você habilitou a [Extensão PDO para SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="668de-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="668de-158">Crie um Banco de Dados SQL chamado `registration`.</span><span class="sxs-lookup"><span data-stu-id="668de-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="668de-159">Você pode fazer isso a partir do comando `sqlcmd` com estes comandos:</span><span class="sxs-lookup"><span data-stu-id="668de-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="668de-160">No diretório raiz de seu aplicativo, crie dois arquivos: um chamado `createtable.php` e outro chamado `index.php`.</span><span class="sxs-lookup"><span data-stu-id="668de-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="668de-161">Abra o arquivo `createtable.php` em um editor de texto ou IDE e adicione o código abaixo.</span><span class="sxs-lookup"><span data-stu-id="668de-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="668de-162">Esse código será usado para criar a tabela `registration_tbl` no banco de dados `registration`.</span><span class="sxs-lookup"><span data-stu-id="668de-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   
    <span data-ttu-id="668de-163">Observe que você precisa atualizar os valores para <code>$user</code> e <code>$pwd</code> com seu nome de usuário do SQL Server local e a senha.</span><span class="sxs-lookup"><span data-stu-id="668de-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="668de-164">Em um terminal no diretório raiz do aplicativo, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="668de-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="668de-165">Abra um navegador da Web e navegue para **http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="668de-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="668de-166">Isso criará a tabela `registration_tbl` no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="668de-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="668de-167">Abra o arquivo **index.php** em um editor de texto ou IDE e adicione o código básico de HTML e CSS para a página (o código PHP será adicionado em várias etapas).</span><span class="sxs-lookup"><span data-stu-id="668de-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="668de-168">Nas marcas de PHP, adicione o código PHP para conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="668de-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="668de-169">Novamente, você precisará atualizar os valores para <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.</span><span class="sxs-lookup"><span data-stu-id="668de-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="668de-170">Após o código de conexão do banco de dados, adicione código para inserir informações de registro no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="668de-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
9. <span data-ttu-id="668de-171">Finalmente, após o código acima, adicione código para recuperar dados do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="668de-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="668de-172">Agora você pode navegar para **http://localhost:8000/index.php** para testar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="668de-173">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="668de-173">Publish your application</span></span>
<span data-ttu-id="668de-174">Depois de testar o aplicativo localmente, você poderá publicá-lo nos Aplicativos Web do Serviço de Aplicativo do Azure usando o Git.</span><span class="sxs-lookup"><span data-stu-id="668de-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="668de-175">Entretanto, você precisará atualizar a conexão do banco de dados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="668de-176">Usando as informações de conexão de banco de dados obtidas previamente (na seção **Obter informações de conexão de banco de dados SQL**), atualize as seguintes informações nos **dois** arquivos `createdatabase.php` e `index.php` com os valores apropriados:</span><span class="sxs-lookup"><span data-stu-id="668de-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="668de-177">No <code>$host</code>, o valor de servidor deve ser precedido com <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="668de-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="668de-178">Agora, você está pronto para configurar a publicação Git e publicar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="668de-179">Essas são as mesmas etapas indicadas no final da seção **Criar um aplicativo web do Azure e configurar a publicação do Git** , acima.</span><span class="sxs-lookup"><span data-stu-id="668de-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="668de-180">Abra GitBash (ou um terminal, se o Git estiver em seu `PATH`), altere os diretórios para o diretório raiz de seu aplicativo (o diretório de **registro** ) e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="668de-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="668de-181">Será solicitada a senha que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="668de-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="668de-182">Navegue até **http://[nome do aplicativo Web].azurewebsites.net/createtable.php** para criar a tabela do banco de dados SQL para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="668de-183">Navegue até **http://[nome do aplicativo Web].azurewebsites.net/index.php** para começar a usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="668de-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="668de-184">Depois de ter publicado seu aplicativo, você pode começar a fazer alterações nele e usar o Git para publicá-lo.</span><span class="sxs-lookup"><span data-stu-id="668de-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="668de-185">Publicar alterações em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="668de-185">Publish changes to your application</span></span>
<span data-ttu-id="668de-186">Para publicar alterações no aplicativo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="668de-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="668de-187">Faça alterações em seu aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="668de-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="668de-188">Abra GitBash (ou um terminal, se o Git estiver em seu `PATH`), altere os diretórios para o diretório raiz de seu aplicativo e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="668de-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="668de-189">Será solicitada a senha que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="668de-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="668de-190">Navegue até **http://[nome do aplicativo Web].azurewebsites.net/index.php** para ver suas alterações.</span><span class="sxs-lookup"><span data-stu-id="668de-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="668de-191">O que mudou</span><span class="sxs-lookup"><span data-stu-id="668de-191">What's changed</span></span>
* <span data-ttu-id="668de-192">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="668de-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

