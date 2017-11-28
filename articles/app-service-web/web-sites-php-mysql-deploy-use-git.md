---
title: "aaaCreate um MySQL PHP aplicativo no Azure do serviço de aplicativo da web e implantar usando o Git"
description: "Um tutorial que demonstra como toocreate um PHP aplicativo que armazena dados em MySQL da web e usar tooAzure de implantação do Git."
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
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="af8e8-103">Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando o Git</span><span class="sxs-lookup"><span data-stu-id="af8e8-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="af8e8-104">Este tutorial mostra como o aplicativo da web toocreate um MySQL PHP e como toodeploy ele muito[do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) usando o Git.</span><span class="sxs-lookup"><span data-stu-id="af8e8-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="af8e8-105">Você usará [PHP][install-php], Olá a ferramenta de linha de comando do MySQL (parte do [MySQL][install-mysql]), e [Git] [ install-git] instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="af8e8-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="af8e8-106">instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional, incluindo Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="af8e8-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="af8e8-107">Após a conclusão deste guia, você terá um aplicativo Web PHP/MySQL em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="af8e8-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="af8e8-108">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="af8e8-108">You will learn:</span></span>

* <span data-ttu-id="af8e8-109">Como toocreate um aplicativo web e um MySQL do banco de dados usando Olá [Portal do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="af8e8-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="af8e8-110">Porque o PHP está habilitado no [aplicativo de serviço Web aplicativos](http://go.microsoft.com/fwlink/?LinkId=529714) por padrão, nada de especial é necessário toorun seu código PHP.</span><span class="sxs-lookup"><span data-stu-id="af8e8-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="af8e8-111">Como toopublish e publicar novamente o tooAzure de aplicativo usando o Git.</span><span class="sxs-lookup"><span data-stu-id="af8e8-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="af8e8-112">Como as tarefas de tooenable Olá criador extensão tooautomate criador em cada `git push`.</span><span class="sxs-lookup"><span data-stu-id="af8e8-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="af8e8-113">Seguindo este tutorial, você compilará um aplicativo Web de registro simples em PHP.</span><span class="sxs-lookup"><span data-stu-id="af8e8-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="af8e8-114">aplicativo Hello será hospedado em aplicativos da Web.</span><span class="sxs-lookup"><span data-stu-id="af8e8-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="af8e8-115">É uma captura de tela do aplicativo hello concluída abaixo:</span><span class="sxs-lookup"><span data-stu-id="af8e8-115">A screenshot of hello completed application is below:</span></span>

![Site PHP do Azure][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="af8e8-117">Configurar o ambiente de desenvolvimento Olá</span><span class="sxs-lookup"><span data-stu-id="af8e8-117">Set up hello development environment</span></span>
<span data-ttu-id="af8e8-118">Este tutorial presume que você tenha [PHP][install-php], Olá a ferramenta de linha de comando do MySQL (parte do [MySQL][install-mysql]), e [Git] [ install-git] instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="af8e8-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="af8e8-119">Criar um aplicativo Web e configurar a publicação Git</span><span class="sxs-lookup"><span data-stu-id="af8e8-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="af8e8-120">Siga essas etapas toocreate um aplicativo web e um banco de dados MySQL:</span><span class="sxs-lookup"><span data-stu-id="af8e8-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="af8e8-121">Logon toohello [Portal do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="af8e8-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="af8e8-122">Clique em Olá **novo** ícone.</span><span class="sxs-lookup"><span data-stu-id="af8e8-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="af8e8-123">Clique em **consulte todos os** Avançar muito**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="af8e8-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="af8e8-124">Clique em **Web + Móvel** e, em seguida, em **Aplicativo Web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="af8e8-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="af8e8-125">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="af8e8-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="af8e8-126">Insira um nome válido para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="af8e8-126">Enter a valid name for your resource group.</span></span>
   
    ![Definir nome do grupo de recursos][resource-group]
6. <span data-ttu-id="af8e8-128">Insira valores para seu novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="af8e8-128">Enter values for your new web app.</span></span>
   
    ![Criar um aplicativo Web][new-web-app]
7. <span data-ttu-id="af8e8-130">Insira valores para o novo banco de dados, incluindo concorda toohello os termos legais.</span><span class="sxs-lookup"><span data-stu-id="af8e8-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Criar novo banco de dados MySQL][new-mysql-db]
8. <span data-ttu-id="af8e8-132">Quando o aplicativo da web de saudação tiver sido criado, você verá nova folha de aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="af8e8-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="af8e8-133">Em **Configurações**, clique em **Implantação Contínua**. Em seguida, clique em *Definir configurações necessárias*.</span><span class="sxs-lookup"><span data-stu-id="af8e8-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configurar a publicação do Git][setup-publishing]
10. <span data-ttu-id="af8e8-135">Selecione **repositório Git Local** para a origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="af8e8-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Configurar o repositório Git][setup-repository]
11. <span data-ttu-id="af8e8-137">tooenable Git de publicação, você deve fornecer um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="af8e8-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="af8e8-138">Anote Olá nome e a senha que você criar.</span><span class="sxs-lookup"><span data-stu-id="af8e8-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="af8e8-139">(Se você tiver configurado um repositório de Git antes, esta etapa será ignorada.)</span><span class="sxs-lookup"><span data-stu-id="af8e8-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Criar credenciais de publicação][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="af8e8-141">Obter informações da conexão MySQL remota</span><span class="sxs-lookup"><span data-stu-id="af8e8-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="af8e8-142">banco de dados do tooconnect toohello MySQL em execução em aplicativos da Web, o será necessário Olá informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="af8e8-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="af8e8-143">tooget informações de conexão do MySQL, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="af8e8-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="af8e8-144">No seu grupo de recursos, clique em banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="af8e8-144">From your resource group, click hello database:</span></span>
   
    ![Selecionar um banco de dados][select-database]
2. <span data-ttu-id="af8e8-146">Do banco de dados de saudação **configurações**, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="af8e8-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Selecionar propriedades][select-properties]
3. <span data-ttu-id="af8e8-148">Anote os valores hello para `Database`, `Host`, `User Id`, e `Password`.</span><span class="sxs-lookup"><span data-stu-id="af8e8-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propriedades][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="af8e8-150">Compilar e testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="af8e8-150">Build and test your app locally</span></span>
<span data-ttu-id="af8e8-151">Agora que criou um aplicativo Web, você pode desenvolvê-lo localmente e então implantá-lo após o teste.</span><span class="sxs-lookup"><span data-stu-id="af8e8-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="af8e8-152">Olá aplicativo de registro é um aplicativo simples do PHP que permite que você tooregister para um evento, fornecendo seu nome e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="af8e8-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="af8e8-153">As informações sobre inscritos anteriores são exibidas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="af8e8-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="af8e8-154">As informações de registro são armazenadas em um banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="af8e8-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="af8e8-155">aplicativo Hello consiste em um arquivo (código de copiar/colar disponível abaixo):</span><span class="sxs-lookup"><span data-stu-id="af8e8-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="af8e8-156">**index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.</span><span class="sxs-lookup"><span data-stu-id="af8e8-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="af8e8-157">toobuild e aplicativo de execução Olá localmente, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="af8e8-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="af8e8-158">Observe que essas etapas pressupõem ter hello PHP e a ferramenta de linha de comando do MySQL (parte do MySQL) configurado no seu computador local e que você tenha ativado Olá [extensão PDO para MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="af8e8-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="af8e8-159">Conectar toohello servidor MySQL remoto, usando o valor de saudação para `Data Source`, `User Id`, `Password`, e `Database` que você recuperou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="af8e8-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="af8e8-160">prompt de comando do MySQL Olá será exibida:</span><span class="sxs-lookup"><span data-stu-id="af8e8-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="af8e8-161">Colar seguir Olá `CREATE TABLE` saudação do comando toocreate `registration_tbl` tabela no banco de dados:</span><span class="sxs-lookup"><span data-stu-id="af8e8-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="af8e8-162">Olá pasta raiz do seu aplicativo local cria **index.php** arquivo.</span><span class="sxs-lookup"><span data-stu-id="af8e8-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="af8e8-163">Olá abrir **index.php** de arquivos em um editor de texto ou o IDE e adicionar Olá o código a seguir, e as alterações necessárias Olá completa marcado com `//TODO:` comentários.</span><span class="sxs-lookup"><span data-stu-id="af8e8-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
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

1. <span data-ttu-id="af8e8-164">Em um terminal tooyour vá aplicativo pasta e digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="af8e8-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="af8e8-165">Agora você pode procurar muito**http://localhost:8000 /** aplicativo hello de tootest.</span><span class="sxs-lookup"><span data-stu-id="af8e8-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="af8e8-166">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="af8e8-166">Publish your app</span></span>
<span data-ttu-id="af8e8-167">Depois de testar seu aplicativo localmente, você pode publicar aplicativos tooWeb usando o Git.</span><span class="sxs-lookup"><span data-stu-id="af8e8-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="af8e8-168">Você inicializar o repositório Git local e publicar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="af8e8-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="af8e8-169">Esses são Olá mesmo etapas mostradas hello Azure Portal final Olá Olá criar um aplicativo web e o conjunto de publicação de Git seção acima.</span><span class="sxs-lookup"><span data-stu-id="af8e8-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="af8e8-170">(Opcional)  Se você tiver esquecido ou no local errado a URL de download remoto Git, navegue toohello propriedades do aplicativo web em Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="af8e8-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="af8e8-171">Abra GitBash (ou um terminal, se for Git no seu `PATH`), altere o diretório de raiz de toohello de diretórios do seu aplicativo e executar Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="af8e8-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="af8e8-172">Você será solicitado para senha Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af8e8-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![Inicial tooAzure Push por meio do Git][git-initial-push]
3. <span data-ttu-id="af8e8-174">Procurar muito**http://[site name].azurewebsites.net/index.php** toobegin usando o aplicativo hello (essas informações serão armazenadas no seu painel de conta):</span><span class="sxs-lookup"><span data-stu-id="af8e8-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Site PHP do Azure][running-app]

<span data-ttu-id="af8e8-176">Depois de publicar seu aplicativo, você pode começar a fazer alterações tooit e usar o Git toopublish-los.</span><span class="sxs-lookup"><span data-stu-id="af8e8-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="af8e8-177">Publicar alterações tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="af8e8-177">Publish changes tooyour app</span></span>
<span data-ttu-id="af8e8-178">toopublish alterações tooyour aplicativo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="af8e8-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="af8e8-179">Tornar alterações tooyour aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="af8e8-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="af8e8-180">Abra GitBash (ou um terminal it Git está no seu `PATH`), altere o diretório de raiz de toohello de diretórios do seu aplicativo e executar Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="af8e8-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="af8e8-181">Você será solicitado para senha Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af8e8-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Envio tooAzure de alterações do site por meio do Git][git-change-push]
3. <span data-ttu-id="af8e8-183">Procurar muito**http://[site name].azurewebsites.net/index.php** toosee seu aplicativo e as alterações feitas:</span><span class="sxs-lookup"><span data-stu-id="af8e8-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Site PHP do Azure][running-app]

> [!NOTE]
> <span data-ttu-id="af8e8-185">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="af8e8-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="af8e8-186">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="af8e8-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="af8e8-187">Habilitar a automação de criador com hello extensão criador</span><span class="sxs-lookup"><span data-stu-id="af8e8-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="af8e8-188">Por padrão, processo de implantação Olá git no serviço de aplicativo não faz nada com composer.json, se você tiver um em seu projeto do PHP.</span><span class="sxs-lookup"><span data-stu-id="af8e8-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="af8e8-189">Você pode habilitar composer.json processamento durante `git push` habilitando a extensão do criador de saudação.</span><span class="sxs-lookup"><span data-stu-id="af8e8-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="af8e8-190">No seu PHP web folha do aplicativo no hello [portal do Azure][management-portal], clique em **ferramentas** > **extensões**.</span><span class="sxs-lookup"><span data-stu-id="af8e8-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Configurações de extensão do Composer][composer-extension-settings]
2. <span data-ttu-id="af8e8-192">Clique em **Adicionar** e em **Criador**.</span><span class="sxs-lookup"><span data-stu-id="af8e8-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Suplemento da extensão do Composer][composer-extension-add]
3. <span data-ttu-id="af8e8-194">Clique em **Okey** tooaccept os termos legais.</span><span class="sxs-lookup"><span data-stu-id="af8e8-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="af8e8-195">Clique em **Okey** extensão de saudação tooadd novamente.</span><span class="sxs-lookup"><span data-stu-id="af8e8-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="af8e8-196">Olá **extensões instaladas** folha agora mostrará a extensão do criador de saudação.</span><span class="sxs-lookup"><span data-stu-id="af8e8-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="af8e8-197">![Exibição da extensão do Composer][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="af8e8-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="af8e8-198">Agora, execute `git add`, `git commit`, e `git push` , como na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="af8e8-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="af8e8-199">Agora, você verá que o Compositor está instalando dependências definidas no composer.json.</span><span class="sxs-lookup"><span data-stu-id="af8e8-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Êxito da extensão do Composer][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="af8e8-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af8e8-201">Next steps</span></span>
<span data-ttu-id="af8e8-202">Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="af8e8-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
