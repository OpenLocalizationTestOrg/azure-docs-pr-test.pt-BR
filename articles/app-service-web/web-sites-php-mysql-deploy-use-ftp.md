---
title: "aaaCreate um MySQL PHP aplicativo no Azure do serviço de aplicativo da web e implantar usando FTP"
description: "Um tutorial que demonstra como toocreate um PHP web aplicativo que armazena dados em uso e MySQL tooAzure de implantação de FTP."
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
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Criar um aplicativo Web PHP-MySQL no Serviço de Aplicativo do Azure e implantá-lo usando FTP
Este tutorial mostra como o aplicativo da web toocreate um MySQL PHP e como toodeploy usando FTP. Este tutorial presume que você tenha [PHP][install-php], [MySQL][install-mysql], um servidor Web e um cliente de FTP instalado no seu computador. instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional, incluindo Windows, Mac e Linux. Após a conclusão deste guia, você terá um aplicativo Web PHP/MySQL em execução no Azure.

Você aprenderá:

* Como toocreate um aplicativo web e um MySQL do banco de dados usando Olá Portal do Azure. Como o PHP é habilitado em aplicativos da Web por padrão, nada de especial é necessário toorun seu código PHP.
* Como toopublish seu aplicativo tooAzure usando FTP.

Seguindo este tutorial, você compilará um aplicativo Web de registro simples em PHP. aplicativo Hello será hospedado em um aplicativo Web. É uma captura de tela do aplicativo hello concluída abaixo:

![Site PHP do Azure][running-app]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Criar um aplicativo Web e configurar a publicação por FTP
Siga essas etapas toocreate um aplicativo web e um banco de dados MySQL:

1. Logon toohello [Portal do Azure][management-portal].
2. Clique em Olá **+ novo** ícone no início de saudação à esquerda da saudação Portal do Azure.
   
    ![Criar um novo site do Azure][new-website]
3. Na pesquisa, digite Olá **Web app + MySQL** e clique em **Web app + MySQL**.
   
    ![Criação personalizada de um novo site][custom-create]
4. Clique em **Criar**. Insira um nome de serviço de aplicativo exclusivo, um nome válido para o grupo de recursos hello e um novo plano de serviço.
   
    ![Definir nome do grupo de recursos][resource-group]
5. Insira valores para o novo banco de dados, incluindo concorda toohello os termos legais.
   
    ![Criar novo banco de dados MySQL][new-mysql-db]
6. Quando o aplicativo da web de saudação tiver sido criado, você verá a nova folha de serviço de aplicativo hello.
7. Clique em **Configurações** > **Credenciais de implantação**. 
   
    ![Definir credenciais de implantação][set-deployment-credentials]
8. tooenable publicação FTP, você deve fornecer um nome de usuário e senha. Salvar credenciais hello e anote Olá nome e a senha que você criar.
   
    ![Criar credenciais de publicação][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Compilar e testar o aplicativo localmente
Olá aplicativo de registro é um aplicativo simples do PHP que permite que você tooregister para um evento, fornecendo seu nome e endereço de email. As informações sobre inscritos anteriores são exibidas em uma tabela. As informações de registro são armazenadas em um banco de dados MySQL. Olá aplicativo consiste em dois arquivos:

* **index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.
* **CreateTable.PHP**: cria a tabela de MySQL Olá para o aplicativo hello. Este arquivo será usado apenas uma vez.

toobuild e execução Olá aplicativo localmente, siga as etapas de saudação abaixo. Observe que essas etapas pressupõem que têm PHP, MySQL e um servidor web configurado no seu computador local e que você tenha ativado Olá [extensão PDO para MySQL][pdo-mysql].

1. Crie um banco de dados MySQL chamado `registration`. Você pode fazer isso em prompt de comando do MySQL Olá com este comando:
   
        mysql> create database registration;
2. No seu diretório raiz do servidor Web , crie uma pasta chamada `registration` e crie dois arquivos nela: um chamado `createtable.php` e outro chamado `index.php`.
3. Olá abrir `createtable.php` arquivo em um editor de texto ou o IDE e adicione Olá código abaixo. Esse código será usado toocreate Olá `registration_tbl` tabela Olá `registration` banco de dados.
   
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
   > Você precisará tooupdate Olá valores para <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.
   > 
   > 
4. Abra um navegador da web e navegue muito[http://localhost/registration/createtable.php][localhost-createtable]. Isso criará Olá `registration_tbl` tabela no banco de dados de saudação.
5. Olá abrir **index.php** de arquivos em um editor de texto ou o IDE e adicionar Olá HTML e CSS código básico para a página de saudação (Olá código PHP será adicionado em etapas posteriores).
   
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
6. Nas marcas PHP de hello, adicione o código PHP para a conexão de banco de dados toohello.
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > Novamente, você precisará valores hello tooupdate <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.
   > 
   > 
7. Após o código de conexão de banco de dados hello, adicione código para inserir informações de registro no banco de dados de saudação.
   
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
8. Por fim, seguindo o código Olá acima, adicione código para recuperar dados do banco de dados de saudação.
   
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

Agora você pode procurar muito[http://localhost/registration/index.php] [ localhost-index] tootest Olá aplicativo.

## <a name="get-mysql-and-ftp-connection-information"></a>Obter informações de conexão do MySQL e FTP
banco de dados do tooconnect toohello MySQL em execução em aplicativos da Web, o será necessário Olá informações de conexão. tooget informações de conexão do MySQL, siga estas etapas:

1. Do serviço de aplicativo hello folha de aplicativo web clique no link de grupo de recursos de saudação:
   
    ![Escolher Grupo de Recursos][select-resourcegroup]
2. No seu grupo de recursos, clique em banco de dados de saudação:
   
    ![Selecionar um banco de dados][select-database]
3. Olá banco de dados do resumo selecione **configurações** > **propriedades**.
   
    ![Selecionar propriedades][select-properties]
4. Anote os valores hello para `Database`, `Host`, `User Id`, e `Password`.
   
    ![Anotar propriedades][note-properties]
5. De seu aplicativo web, clique em Olá **baixar perfil de publicação** link na Olá canto inferior direito da página de saudação:
   
    ![Baixar perfil de publicação][download-publish-profile]
6. Olá abrir `.publishsettings` arquivo em um editor de XML. 
7. Localize Olá `<publishProfile >` elemento com `publishMethod="FTP"` que parece semelhante toothis:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Anote Olá `publishUrl`, `userName`, e `userPWD` atributos.

## <a name="publish-your-app"></a>Publicar seu aplicativo
Depois de testar seu aplicativo localmente, você pode publicar tooyour web app usando FTP. No entanto, você primeiro precisa de informações de conexão de banco de dados tooupdate Olá no aplicativo hello. Usando informações de conexão de banco de dados Olá obtidos anteriormente (no hello **informações de conexão FTP e obter MySQL** seção), atualização Olá informações a seguir **ambos** Olá `createdatabase.php` e `index.php` valores adequados de arquivos com hello:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Agora você está pronto toopublish seu aplicativo usando o FTP.

1. Abra o cliente de FTP de sua escolha.
2. Digite hello *parte do nome de host* de saudação `publishUrl` atributo que você anotou anteriormente no seu cliente de FTP.
3. Digite hello `userName` e `userPWD` atributos observados acima inalterados no seu cliente de FTP.
4. Estabeleça uma conexão.

Depois de se conectar você será capaz de tooupload e baixar arquivos conforme necessário. Certifique-se de que você está carregando arquivos toohello diretório raiz que é `/site/wwwroot`.

Depois de carregar ambos `index.php` e `createtable.php`, procurar muito**http://[site name].azurewebsites.net/createtable.php** toocreate Olá MySQL de tabela para o aplicativo hello e procure muito**http://[site nome ].azurewebsites.net/index.php** toobegin usando o aplicativo hello.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).

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

