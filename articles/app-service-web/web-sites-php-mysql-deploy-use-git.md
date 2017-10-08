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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando o Git
Este tutorial mostra como o aplicativo da web toocreate um MySQL PHP e como toodeploy ele muito[do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) usando o Git. Você usará [PHP][install-php], Olá a ferramenta de linha de comando do MySQL (parte do [MySQL][install-mysql]), e [Git] [ install-git] instalado em seu computador. instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional, incluindo Windows, Mac e Linux. Após a conclusão deste guia, você terá um aplicativo Web PHP/MySQL em execução no Azure.

Você aprenderá:

* Como toocreate um aplicativo web e um MySQL do banco de dados usando Olá [Portal do Azure][management-portal]. Porque o PHP está habilitado no [aplicativo de serviço Web aplicativos](http://go.microsoft.com/fwlink/?LinkId=529714) por padrão, nada de especial é necessário toorun seu código PHP.
* Como toopublish e publicar novamente o tooAzure de aplicativo usando o Git.
* Como as tarefas de tooenable Olá criador extensão tooautomate criador em cada `git push`.

Seguindo este tutorial, você compilará um aplicativo Web de registro simples em PHP. aplicativo Hello será hospedado em aplicativos da Web. É uma captura de tela do aplicativo hello concluída abaixo:

![Site PHP do Azure][running-app]

## <a name="set-up-hello-development-environment"></a>Configurar o ambiente de desenvolvimento Olá
Este tutorial presume que você tenha [PHP][install-php], Olá a ferramenta de linha de comando do MySQL (parte do [MySQL][install-mysql]), e [Git] [ install-git] instalado em seu computador.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Criar um aplicativo Web e configurar a publicação Git
Siga essas etapas toocreate um aplicativo web e um banco de dados MySQL:

1. Logon toohello [Portal do Azure][management-portal].
2. Clique em Olá **novo** ícone.
3. Clique em **consulte todos os** Avançar muito**Marketplace**. 
4. Clique em **Web + Móvel** e, em seguida, em **Aplicativo Web + MySQL**. Em seguida, clique em **Criar**.
5. Insira um nome válido para o grupo de recursos.
   
    ![Definir nome do grupo de recursos][resource-group]
6. Insira valores para seu novo aplicativo Web.
   
    ![Criar um aplicativo Web][new-web-app]
7. Insira valores para o novo banco de dados, incluindo concorda toohello os termos legais.
   
    ![Criar novo banco de dados MySQL][new-mysql-db]
8. Quando o aplicativo da web de saudação tiver sido criado, você verá nova folha de aplicativo web hello.
9. Em **Configurações**, clique em **Implantação Contínua**. Em seguida, clique em *Definir configurações necessárias*.
   
    ![Configurar a publicação do Git][setup-publishing]
10. Selecione **repositório Git Local** para a origem de saudação.
    
     ![Configurar o repositório Git][setup-repository]
11. tooenable Git de publicação, você deve fornecer um nome de usuário e senha. Anote Olá nome e a senha que você criar. (Se você tiver configurado um repositório de Git antes, esta etapa será ignorada.)
    
     ![Criar credenciais de publicação][credentials]

## <a name="get-remote-mysql-connection-information"></a>Obter informações da conexão MySQL remota
banco de dados do tooconnect toohello MySQL em execução em aplicativos da Web, o será necessário Olá informações de conexão. tooget informações de conexão do MySQL, siga estas etapas:

1. No seu grupo de recursos, clique em banco de dados de saudação:
   
    ![Selecionar um banco de dados][select-database]
2. Do banco de dados de saudação **configurações**, selecione **propriedades**.
   
    ![Selecionar propriedades][select-properties]
3. Anote os valores hello para `Database`, `Host`, `User Id`, e `Password`.
   
    ![Anotar propriedades][note-properties]

## <a name="build-and-test-your-app-locally"></a>Compilar e testar o aplicativo localmente
Agora que criou um aplicativo Web, você pode desenvolvê-lo localmente e então implantá-lo após o teste.

Olá aplicativo de registro é um aplicativo simples do PHP que permite que você tooregister para um evento, fornecendo seu nome e endereço de email. As informações sobre inscritos anteriores são exibidas em uma tabela. As informações de registro são armazenadas em um banco de dados MySQL. aplicativo Hello consiste em um arquivo (código de copiar/colar disponível abaixo):

* **index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.

toobuild e aplicativo de execução Olá localmente, siga as etapas de saudação abaixo. Observe que essas etapas pressupõem ter hello PHP e a ferramenta de linha de comando do MySQL (parte do MySQL) configurado no seu computador local e que você tenha ativado Olá [extensão PDO para MySQL][pdo-mysql].

1. Conectar toohello servidor MySQL remoto, usando o valor de saudação para `Data Source`, `User Id`, `Password`, e `Database` que você recuperou anteriormente:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. prompt de comando do MySQL Olá será exibida:
   
        mysql>
3. Colar seguir Olá `CREATE TABLE` saudação do comando toocreate `registration_tbl` tabela no banco de dados:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Olá pasta raiz do seu aplicativo local cria **index.php** arquivo.
5. Olá abrir **index.php** de arquivos em um editor de texto ou o IDE e adicionar Olá o código a seguir, e as alterações necessárias Olá completa marcado com `//TODO:` comentários.

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

1. Em um terminal tooyour vá aplicativo pasta e digite Olá comando a seguir:
   
       php -S localhost:8000

Agora você pode procurar muito**http://localhost:8000 /** aplicativo hello de tootest.

## <a name="publish-your-app"></a>Publicar seu aplicativo
Depois de testar seu aplicativo localmente, você pode publicar aplicativos tooWeb usando o Git. Você inicializar o repositório Git local e publicar o aplicativo hello.

> [!NOTE]
> Esses são Olá mesmo etapas mostradas hello Azure Portal final Olá Olá criar um aplicativo web e o conjunto de publicação de Git seção acima.
> 
> 

1. (Opcional)  Se você tiver esquecido ou no local errado a URL de download remoto Git, navegue toohello propriedades do aplicativo web em Olá Portal do Azure.
2. Abra GitBash (ou um terminal, se for Git no seu `PATH`), altere o diretório de raiz de toohello de diretórios do seu aplicativo e executar Olá comandos a seguir:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Você será solicitado para senha Olá criado anteriormente.
   
    ![Inicial tooAzure Push por meio do Git][git-initial-push]
3. Procurar muito**http://[site name].azurewebsites.net/index.php** toobegin usando o aplicativo hello (essas informações serão armazenadas no seu painel de conta):
   
    ![Site PHP do Azure][running-app]

Depois de publicar seu aplicativo, você pode começar a fazer alterações tooit e usar o Git toopublish-los.

## <a name="publish-changes-tooyour-app"></a>Publicar alterações tooyour aplicativo
toopublish alterações tooyour aplicativo, siga estas etapas:

1. Tornar alterações tooyour aplicativo localmente.
2. Abra GitBash (ou um terminal it Git está no seu `PATH`), altere o diretório de raiz de toohello de diretórios do seu aplicativo e executar Olá comandos a seguir:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Você será solicitado para senha Olá criado anteriormente.
   
    ![Envio tooAzure de alterações do site por meio do Git][git-change-push]
3. Procurar muito**http://[site name].azurewebsites.net/index.php** toosee seu aplicativo e as alterações feitas:
   
    ![Site PHP do Azure][running-app]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Habilitar a automação de criador com hello extensão criador
Por padrão, processo de implantação Olá git no serviço de aplicativo não faz nada com composer.json, se você tiver um em seu projeto do PHP. Você pode habilitar composer.json processamento durante `git push` habilitando a extensão do criador de saudação.

1. No seu PHP web folha do aplicativo no hello [portal do Azure][management-portal], clique em **ferramentas** > **extensões**.
   
    ![Configurações de extensão do Composer][composer-extension-settings]
2. Clique em **Adicionar** e em **Criador**.
   
    ![Suplemento da extensão do Composer][composer-extension-add]
3. Clique em **Okey** tooaccept os termos legais. Clique em **Okey** extensão de saudação tooadd novamente.
   
    Olá **extensões instaladas** folha agora mostrará a extensão do criador de saudação.  
    ![Exibição da extensão do Composer][composer-extension-view]
4. Agora, execute `git add`, `git commit`, e `git push` , como na seção anterior hello. Agora, você verá que o Compositor está instalando dependências definidas no composer.json.
   
    ![Êxito da extensão do Composer][composer-extension-success]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).

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
