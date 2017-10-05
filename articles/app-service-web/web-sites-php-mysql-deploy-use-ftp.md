---
title: "Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando FTP"
description: "Um tutorial que demonstra como criar um aplicativo Web PHP que armazena dados no MySQL e como usar a implantação FTP no Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="38d58-103">Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando FTP</span><span class="sxs-lookup"><span data-stu-id="38d58-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="38d58-104">Este tutorial mostra como criar um aplicativo Web PHP-MySQL e como implantá-lo usando FTP.</span><span class="sxs-lookup"><span data-stu-id="38d58-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="38d58-105">Este tutorial presume que você tenha [PHP][install-php], [MySQL][install-mysql], um servidor Web e um cliente de FTP instalado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="38d58-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="38d58-106">As instruções deste tutorial podem ser seguidas em qualquer sistema operacional, incluindo Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="38d58-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="38d58-107">Após a conclusão deste guia, você terá um aplicativo Web PHP/MySQL em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="38d58-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="38d58-108">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="38d58-108">You will learn:</span></span>

* <span data-ttu-id="38d58-109">Como criar um aplicativo Web e um banco de dados MySQL usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="38d58-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="38d58-110">Como o PHP está habilitado em Aplicativos Web por padrão, nada de especial é necessário para executar seu código PHP.</span><span class="sxs-lookup"><span data-stu-id="38d58-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="38d58-111">Como publicar seu aplicativo no Azure usando FTP.</span><span class="sxs-lookup"><span data-stu-id="38d58-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="38d58-112">Seguindo este tutorial, você compilará um aplicativo Web de registro simples em PHP.</span><span class="sxs-lookup"><span data-stu-id="38d58-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="38d58-113">O aplicativo será hospedado em um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="38d58-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="38d58-114">Abaixo, uma captura de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="38d58-114">A screenshot of the completed application is below:</span></span>

![Site PHP do Azure][running-app]

> [!NOTE]
> <span data-ttu-id="38d58-116">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d58-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="38d58-117">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="38d58-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="38d58-118">Criar um aplicativo Web e configurar a publicação por FTP</span><span class="sxs-lookup"><span data-stu-id="38d58-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="38d58-119">Siga estas etapas para criar um aplicativo Web e um Banco de Dados MySQL:</span><span class="sxs-lookup"><span data-stu-id="38d58-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="38d58-120">Faça logon no [portal do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="38d58-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="38d58-121">Clique no ícone **+ Novo** no canto superior esquerdo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="38d58-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Criar um novo site do Azure][new-website]
3. <span data-ttu-id="38d58-123">Na pesquisa, digite **Aplicativo Web + MySQL** e clique em **Aplicativo Web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="38d58-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Criação personalizada de um novo site][custom-create]
4. <span data-ttu-id="38d58-125">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="38d58-125">Click **Create**.</span></span> <span data-ttu-id="38d58-126">Insira um nome de serviço de aplicativo exclusivo, um nome válido para o grupo de recursos e um novo plano de serviço.</span><span class="sxs-lookup"><span data-stu-id="38d58-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Definir nome do grupo de recursos][resource-group]
5. <span data-ttu-id="38d58-128">Insira valores para seu novo banco de dados, incluindo concordar com os termos legais.</span><span class="sxs-lookup"><span data-stu-id="38d58-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Criar novo banco de dados MySQL][new-mysql-db]
6. <span data-ttu-id="38d58-130">Quando o aplicativo Web tiver sido criado, você verá a nova folha do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d58-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="38d58-131">Clique em **Configurações** > **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="38d58-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Definir credenciais de implantação][set-deployment-credentials]
8. <span data-ttu-id="38d58-133">Para habilitar publicação de FTP, você deverá fornecer um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="38d58-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="38d58-134">Salve as credenciais e anote o nome de usuário e a senha que você criar.</span><span class="sxs-lookup"><span data-stu-id="38d58-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Criar credenciais de publicação][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="38d58-136">Compilar e testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="38d58-136">Build and test your app locally</span></span>
<span data-ttu-id="38d58-137">O aplicativo Registro é um aplicativo simples do PHP que permite que você se registre em um evento fornecendo seu nome e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="38d58-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="38d58-138">As informações sobre inscritos anteriores são exibidas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="38d58-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="38d58-139">As informações de registro são armazenadas em um banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="38d58-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="38d58-140">O aplicativo consiste de dois arquivos:</span><span class="sxs-lookup"><span data-stu-id="38d58-140">The app consists of two files:</span></span>

* <span data-ttu-id="38d58-141">**index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.</span><span class="sxs-lookup"><span data-stu-id="38d58-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="38d58-142">**createtable.php**: cria a tabela MySQL para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d58-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="38d58-143">Este arquivo será usado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="38d58-143">This file will only be used once.</span></span>

<span data-ttu-id="38d58-144">Para compilar e executar o aplicativo localmente, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="38d58-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="38d58-145">Observe que essas etapas pressupõem que você tem PHP, MySQL e um servidor Web definido na sua máquina local, e que você tenha habilitado a [extensão PDO para MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="38d58-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="38d58-146">Crie um banco de dados MySQL chamado `registration`.</span><span class="sxs-lookup"><span data-stu-id="38d58-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="38d58-147">Você pode fazer isso no prompt de comando MySQL com este comando:</span><span class="sxs-lookup"><span data-stu-id="38d58-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="38d58-148">No seu diretório raiz do servidor Web , crie uma pasta chamada `registration` e crie dois arquivos nela: um chamado `createtable.php` e outro chamado `index.php`.</span><span class="sxs-lookup"><span data-stu-id="38d58-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="38d58-149">Abra o arquivo `createtable.php` em um editor de texto ou IDE e adicione o código abaixo.</span><span class="sxs-lookup"><span data-stu-id="38d58-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="38d58-150">Esse código será usado para criar a tabela `registration_tbl` no banco de dados `registration`.</span><span class="sxs-lookup"><span data-stu-id="38d58-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="38d58-151">Você precisará atualizar os valores para <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.</span><span class="sxs-lookup"><span data-stu-id="38d58-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="38d58-152">Abra um navegador da web e navegue para [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="38d58-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="38d58-153">Isso criará a tabela `registration_tbl` no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="38d58-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="38d58-154">Abra o arquivo **index.php** em um editor de texto ou IDE e adicione o código básico de HTML e CSS para a página (o código PHP será adicionado em várias etapas).</span><span class="sxs-lookup"><span data-stu-id="38d58-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="38d58-155">Nas marcas de PHP, adicione o código PHP para conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="38d58-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="38d58-156">Novamente, você precisará atualizar os valores para <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.</span><span class="sxs-lookup"><span data-stu-id="38d58-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="38d58-157">Após o código de conexão do banco de dados, adicione código para inserir informações de registro no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="38d58-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="38d58-158">Finalmente, após o código acima, adicione código para recuperar dados do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="38d58-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="38d58-159">Agora você pode navegar para [http://localhost/registration/index.php][localhost-index] para testar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d58-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="38d58-160">Obter informações de conexão do MySQL e FTP</span><span class="sxs-lookup"><span data-stu-id="38d58-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="38d58-161">Para conectar-se ao Banco de Dados MySQL que está em execução nos Aplicativos Web, você precisará das informações da conexão.</span><span class="sxs-lookup"><span data-stu-id="38d58-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="38d58-162">Para obter informações sobre a conexão MySQL, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="38d58-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="38d58-163">Na folha do aplicativo Web do serviço de aplicativo clique no link do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="38d58-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Escolher Grupo de Recursos][select-resourcegroup]
2. <span data-ttu-id="38d58-165">No seu grupo de recursos, verifique o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="38d58-165">From your resource group, click the database:</span></span>
   
    ![Selecionar um banco de dados][select-database]
3. <span data-ttu-id="38d58-167">No resumo do banco de dados, escolha **Configurações** > **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="38d58-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Selecionar propriedades][select-properties]
4. <span data-ttu-id="38d58-169">Anote os valores de `Database`, `Host`, `User Id` e `Password`.</span><span class="sxs-lookup"><span data-stu-id="38d58-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propriedades][note-properties]
5. <span data-ttu-id="38d58-171">Em seu aplicativo Web, clique no link **Baixar perfil de publicação** na parte inferior direito da página:</span><span class="sxs-lookup"><span data-stu-id="38d58-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Baixar perfil de publicação][download-publish-profile]
6. <span data-ttu-id="38d58-173">Abra o arquivo `.publishsettings` em um editor XML.</span><span class="sxs-lookup"><span data-stu-id="38d58-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="38d58-174">Localize o elemento `<publishProfile >` com `publishMethod="FTP"` que parece semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="38d58-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="38d58-175">Anote os atributos de `publishUrl`, `userName` e `userPWD`.</span><span class="sxs-lookup"><span data-stu-id="38d58-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="38d58-176">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="38d58-176">Publish your app</span></span>
<span data-ttu-id="38d58-177">Depois de testar seu aplicativo localmente, você poderá publicá-lo para o aplicativo Web usando FTP.</span><span class="sxs-lookup"><span data-stu-id="38d58-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="38d58-178">Entretanto, você precisará atualizar a conexão do banco de dados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d58-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="38d58-179">Usando as informações de conexão do banco de dados obtidas anteriormente (na seção **Obter informações de conexão do MySQL e FTP**), atualize as seguintes informações nos **dois** arquivos, `createdatabase.php` e `index.php`, com os valores apropriados:</span><span class="sxs-lookup"><span data-stu-id="38d58-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="38d58-180">Agora você está pronto para publicar seu aplicativo usando FTP.</span><span class="sxs-lookup"><span data-stu-id="38d58-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="38d58-181">Abra o cliente de FTP de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="38d58-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="38d58-182">Insira a *parte do nome de host* do atributo `publishUrl` que foi observado acima no seu cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="38d58-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="38d58-183">Insira os atributos `userName` e `userPWD` que foram anotados acima inalterados no seu cliente de FTP.</span><span class="sxs-lookup"><span data-stu-id="38d58-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="38d58-184">Estabeleça uma conexão.</span><span class="sxs-lookup"><span data-stu-id="38d58-184">Establish a connection.</span></span>

<span data-ttu-id="38d58-185">Após você ter se conectado, será capaz de carregar e descarregar arquivos de downloads, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="38d58-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="38d58-186">Tenha certeza de que você está carregando arquivos para o diretório raiz, que é `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="38d58-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="38d58-187">Após carregar `index.php` e `createtable.php`, navegue para **http://[nome do site].azurewebsites.net/createtable.php** de modo a criar a tabela MySQL para o aplicativo e, em seguida, navegue para **http://[nome do site].azurewebsites.net/index.php** para começar usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d58-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38d58-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38d58-188">Next steps</span></span>
<span data-ttu-id="38d58-189">Para obter mais informações, consulte o [Centro de Desenvolvimento PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="38d58-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

