---
title: "Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando o Git"
description: "Um tutorial que demonstra como criar um aplicativo Web PHP que armazena dados no MySQL e como usar implantação Git no Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="ffc7c-103">Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando o Git</span><span class="sxs-lookup"><span data-stu-id="ffc7c-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="ffc7c-104">Este tutorial mostra como criar um aplicativo Web PHP-MySQL e como implantá-lo no [Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) usando o Git.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="ffc7c-105">Você usará o [PHP][install-php], a Ferramenta de Linha de Comando do MySQL (parte do [MySQL][install-mysql]), e [Git][install-git] instalados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="ffc7c-106">As instruções deste tutorial podem ser seguidas em qualquer sistema operacional, incluindo Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="ffc7c-107">Após a conclusão deste guia, você terá um aplicativo Web PHP/MySQL em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="ffc7c-108">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-108">You will learn:</span></span>

* <span data-ttu-id="ffc7c-109">Como criar um aplicativo Web e um banco de dados MySQL usando o [Portal do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="ffc7c-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="ffc7c-110">Já que o PHP está habilitado nos [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) por padrão, não é necessário nada de especial para executar seu código PHP.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="ffc7c-111">Como publicar e publicar novamente o aplicativo no Azure usando o Git.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="ffc7c-112">Como habilitar a extensão do Compositor para automatizar tarefas do Compositor em cada `git push`.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="ffc7c-113">Seguindo este tutorial, você compilará um aplicativo Web de registro simples em PHP.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="ffc7c-114">O aplicativo será hospedado em aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="ffc7c-115">Abaixo, uma captura de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-115">A screenshot of the completed application is below:</span></span>

![Site PHP do Azure][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="ffc7c-117">Configurar o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="ffc7c-117">Set up the development environment</span></span>
<span data-ttu-id="ffc7c-118">O tutorial presume que você usa o [PHP][install-php], a Ferramenta de Linha de Comando do MySQL (parte do [MySQL][install-mysql]), e [Git][install-git] instalados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="ffc7c-119">Criar um aplicativo Web e configurar a publicação Git</span><span class="sxs-lookup"><span data-stu-id="ffc7c-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="ffc7c-120">Siga estas etapas para criar um aplicativo Web e um Banco de Dados MySQL:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="ffc7c-121">Faça logon no [portal do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="ffc7c-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="ffc7c-122">Clique no ícone **Novo** .</span><span class="sxs-lookup"><span data-stu-id="ffc7c-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="ffc7c-123">Clique em **Ver tudo** ao lado de **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="ffc7c-124">Clique em **Web + Móvel** e, em seguida, em **Aplicativo Web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="ffc7c-125">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="ffc7c-126">Insira um nome válido para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-126">Enter a valid name for your resource group.</span></span>
   
    ![Definir nome do grupo de recursos][resource-group]
6. <span data-ttu-id="ffc7c-128">Insira valores para seu novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-128">Enter values for your new web app.</span></span>
   
    ![Criar um aplicativo Web][new-web-app]
7. <span data-ttu-id="ffc7c-130">Insira valores para seu novo banco de dados, incluindo concordar com os termos legais.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Criar novo banco de dados MySQL][new-mysql-db]
8. <span data-ttu-id="ffc7c-132">Quando o aplicativo web tiver sido criado, você verá a nova folha do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="ffc7c-133">Em **Configurações**, clique em **Implantação Contínua**. Em seguida, clique em *Definir configurações necessárias*.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configurar a publicação do Git][setup-publishing]
10. <span data-ttu-id="ffc7c-135">Selecione **Repositório Git local** como a fonte.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Configurar o repositório Git][setup-repository]
11. <span data-ttu-id="ffc7c-137">Para habilitar a publicação do Git, você deve fornecer um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="ffc7c-138">Anote o nome do usuário e a senha que você criou.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="ffc7c-139">(Se você tiver configurado um repositório de Git antes, esta etapa será ignorada.)</span><span class="sxs-lookup"><span data-stu-id="ffc7c-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Criar credenciais de publicação][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="ffc7c-141">Obter informações da conexão MySQL remota</span><span class="sxs-lookup"><span data-stu-id="ffc7c-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="ffc7c-142">Para conectar-se ao Banco de Dados MySQL que está em execução nos Aplicativos Web, você precisará das informações da conexão.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="ffc7c-143">Para obter informações sobre a conexão MySQL, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="ffc7c-144">No seu grupo de recursos, verifique o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-144">From your resource group, click the database:</span></span>
   
    ![Selecionar um banco de dados][select-database]
2. <span data-ttu-id="ffc7c-146">Em **Configurações** do banco de dados, escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Selecionar propriedades][select-properties]
3. <span data-ttu-id="ffc7c-148">Anote os valores de `Database`, `Host`, `User Id` e `Password`.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propriedades][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="ffc7c-150">Compilar e testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="ffc7c-150">Build and test your app locally</span></span>
<span data-ttu-id="ffc7c-151">Agora que criou um aplicativo Web, você pode desenvolvê-lo localmente e então implantá-lo após o teste.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="ffc7c-152">O aplicativo Registro é um aplicativo simples do PHP que permite que você se registre em um evento fornecendo seu nome e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="ffc7c-153">As informações sobre inscritos anteriores são exibidas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="ffc7c-154">As informações de registro são armazenadas em um banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="ffc7c-155">O aplicativo consiste em um arquivo (copie/cole o código disponível abaixo):</span><span class="sxs-lookup"><span data-stu-id="ffc7c-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="ffc7c-156">**index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="ffc7c-157">Para criar e executar o aplicativo localmente, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="ffc7c-158">Observe que essas etapas pressupõem que o PHP e a ferramenta de linha de comando do MySQL (parte do MySQL) estão configurados no computador local e que a [extensão PDO para MySQL][pdo-mysql] foi habilitada.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="ffc7c-159">Conecte-se ao servidor MySQL remoto usando os valores de `Data Source`, `User Id`, `Password` e `Database` que você recuperou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="ffc7c-160">O prompt de comando do MySQL será exibido:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="ffc7c-161">Cole no seguinte comando `CREATE TABLE` para criar a tabela `registration_tbl` em seu banco de dados:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="ffc7c-162">Na raiz da pasta do aplicativo local, crie o arquivo **index.php** .</span><span class="sxs-lookup"><span data-stu-id="ffc7c-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="ffc7c-163">Abra o arquivo **index.php** em um editor de texto ou IDE, adicione o código a seguir e conclua as alterações necessárias marcadas com os comentários `//TODO:`.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="ffc7c-164">Em um terminal, abra a sua pasta do aplicativo e digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="ffc7c-165">Agora você pode navegar para **http://localhost:8000/** para testar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="ffc7c-166">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ffc7c-166">Publish your app</span></span>
<span data-ttu-id="ffc7c-167">Depois de testar seu aplicativo localmente, você poderá publicá-lo para aplicativos Web usando Git.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="ffc7c-168">Você inicializara seu repositório local do Git e publicará o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ffc7c-169">Estas são as mesmas etapas mostradas no Portal do Azure no final da seção Criar um aplicativo Web e Configurar a publicação Git, apresentada acima.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="ffc7c-170">(Opcional) Se você tiver esquecido ou perdido a URL de seu repositório Git remoto, navegue até as propriedades do aplicativo Web no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="ffc7c-171">Abra GitBash (ou um terminal, se o Git estiver em seu `PATH`), altere para o diretório raiz de seu aplicativo e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="ffc7c-172">Será solicitada a senha que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Envio por push inicial ao Azure via Git][git-initial-push]
3. <span data-ttu-id="ffc7c-174">Navegue até **http://[nome do site].azurewebsites.net/index.php** para começar a usar o aplicativo (essas informações serão armazenadas no painel de sua conta):</span><span class="sxs-lookup"><span data-stu-id="ffc7c-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Site PHP do Azure][running-app]

<span data-ttu-id="ffc7c-176">Depois de ter publicado seu aplicativo, você pode começar a fazer alterações nele e usar o Git para publicá-lo.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="ffc7c-177">Publicar alterações em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ffc7c-177">Publish changes to your app</span></span>
<span data-ttu-id="ffc7c-178">Para publicar alterações em seu aplicativo, siga essas etapas:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="ffc7c-179">Faça alterações em seu aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="ffc7c-180">Abra GitBash (ou um terminal, se o Git estiver em seu `PATH`), altere os diretórios para o diretório raiz de seu aplicativo e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="ffc7c-181">Será solicitada a senha que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Enviando alterações por push ao Site do Azure via Git][git-change-push]
3. <span data-ttu-id="ffc7c-183">Navegue até **http://[nome do site].azurewebsites.net/index.php** para ver o aplicativo e todas as alterações feitas:</span><span class="sxs-lookup"><span data-stu-id="ffc7c-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Site PHP do Azure][running-app]

> [!NOTE]
> <span data-ttu-id="ffc7c-185">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ffc7c-186">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="ffc7c-187">Habilitar a automação do Compositor com a extensão do Compositor</span><span class="sxs-lookup"><span data-stu-id="ffc7c-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="ffc7c-188">Por padrão, o processo de implantação do git no Serviço de Aplicativo não faz nada com o composer.json, se você tiver um em seu projeto PHP.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="ffc7c-189">Você pode habilitar o processamento composer.json durante `git push` habilitando a Extensão do compositor.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="ffc7c-190">Na folha do aplicativo Web PHP no [portal do Azure][management-portal], clique em **Ferramentas** > **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Configurações de extensão do Composer][composer-extension-settings]
2. <span data-ttu-id="ffc7c-192">Clique em **Adicionar** e em **Criador**.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Suplemento da extensão do Composer][composer-extension-add]
3. <span data-ttu-id="ffc7c-194">Clique em **OK** para aceitar os termos legais.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="ffc7c-195">Clique em **OK** novamente para adicionar a extensão.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="ffc7c-196">Agora, a folha **Extensões instaladas** mostrará a Extensão do criador.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="ffc7c-197">![Exibição da extensão do Composer][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="ffc7c-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="ffc7c-198">Agora, execute `git add`, `git commit` e `git push` como na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="ffc7c-199">Agora, você verá que o Compositor está instalando dependências definidas no composer.json.</span><span class="sxs-lookup"><span data-stu-id="ffc7c-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Êxito da extensão do Composer][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="ffc7c-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ffc7c-201">Next steps</span></span>
<span data-ttu-id="ffc7c-202">Para obter mais informações, consulte o [Centro de Desenvolvimento PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ffc7c-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
