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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Criar um aplicativo web do SQL do PHP e implantar tooAzure do serviço de aplicativo usando o Git
Este tutorial mostra como toocreate um PHP web app [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que se conecta tooAzure banco de dados SQL e como toodeploy usando Git. Este tutorial presume que você tenha [PHP][install-php], [SQL Server Express][install-SQLExpress], Olá [Drivers da Microsoft para SQL Server para PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), e [Git] [ install-git] instalado em seu computador. Após a conclusão deste guia, você terá um aplicativo Web PHP/SQL em execução no Azure.

> [!NOTE]
> Você pode instalar e configurar o PHP, SQL Server Express e Olá Drivers da Microsoft para SQL Server para PHP usando Olá [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Você aprenderá:

* Como toocreate um Azure web app e um banco de dados SQL usando Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Como PHP está habilitado no serviço de aplicativo Web de aplicativos, por padrão, nada de especial é necessário toorun seu código PHP.
* Como toopublish e publicar novamente o tooAzure de aplicativo usando o Git.

Seguindo este tutorial, você irá criar um aplicativo da web de registro simples no PHP. aplicativo Hello será hospedado em um site do Azure. É uma captura de tela do aplicativo hello concluída abaixo:

![Site PHP do Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Criar um aplicativo Web do Azure e configurar a publicação Git
Siga essas etapas toocreate um aplicativo web do Azure e um banco de dados SQL:

1. Faça logon no toohello [Portal do Azure](https://portal.azure.com/).
2. Abra hello Azure Marketplace clicando Olá **novo** ícone no início de saudação à esquerda do painel de saudação, clique em **Selecionar tudo** tooMarketplace Avançar e selecionando **Web + móvel**.
3. No hello Marketplace, selecione **Web + móvel**.
4. Clique em Olá **Web app + SQL** ícone.
5. Depois de ler a descrição de saudação do aplicativo Web de saudação + SQL aplicativo, selecione **criar**.
6. Clique em cada parte (**grupo de recursos**, **aplicativo Web**, **banco de dados**, e **assinatura**) e insira ou selecione valores para Olá necessária campos:
   
   * Insira um nome de URL de sua escolha    
   * Configurar credenciais de servidor de banco de dados
   * Selecione Olá região mais próxima tooyou
     
     ![configurar o aplicativo](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Quando terminar de definir o aplicativo web de saudação, clique em **criar**.
   
    Quando o aplicativo da web de saudação tiver sido criado, Olá **notificações** botão pisca uma verde **êxito** e Olá recurso grupo folha abrir tooshow ambos os Olá web app e hello banco de dados SQL no grupo de saudação.
8. Clique em ícone do aplicativo da web de saudação na folha de saudação recurso grupo folha tooopen saudação do aplicativo web.
   
    ![grupo de recursos do aplicativo Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. Em **Configurações**, clique em **Implantação contínua** > **Definir configurações necessárias**. Selecione **Repositório Git local** e clique em **OK**.
   
    ![onde está o código-fonte](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Se não tiver configurado um repositório Git antes, você deverá fornecer um nome de usuário e senha. toodo, clique **configurações** > **credenciais de implantação** na folha do aplicativo da web de saudação.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. Em **configurações** clique em **propriedades** toosee Olá Git remoto URL precisar toouse toodeploy seu aplicativo PHP mais tarde.

## <a name="get-sql-database-connection-information"></a>Obter informações da conexão do Banco de Dados SQL
instância de banco de dados SQL do toohello tooconnect é vinculada tooyour web app, o será necessário Olá informações de conexão, o que você especificou quando criou o banco de dados de saudação. Olá tooget informações de conexão de banco de dados SQL, siga estas etapas:

1. Na folha do grupo de recursos hello, clique em ícone Olá SQL do banco de dados.
2. Na folha de saudação SQL do banco de dados, clique em **configurações** > **propriedades**, em seguida, clique em **Mostrar cadeias de conexão de banco de dados**. 
   
    ![Exibir propriedades do banco de dados](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. De saudação **PHP** seção da caixa de diálogo resultante hello, anote os valores hello para `Server`, `SQL Database`, e `User Name`. Você usará esses valores posteriormente quando publicar seu tooAzure de aplicativo web do PHP do serviço de aplicativo.

## <a name="build-and-test-your-application-locally"></a>Criar e testar o aplicativo localmente
Olá aplicativo de registro é um aplicativo simples do PHP que permite que você tooregister para um evento, fornecendo seu nome e endereço de email. As informações sobre inscritos anteriores são exibidas em uma tabela. As informações de registro são armazenadas em uma instância do Banco de Dados SQL. aplicativo Hello consiste em dois arquivos (código de copiar/colar disponível abaixo):

* **index.php**: exibe um formulário de registro e uma tabela contendo informações sobre o inscrito.
* **CreateTable.PHP**: cria a tabela de banco de dados SQL Olá para o aplicativo hello. Este arquivo será usado apenas uma vez.

aplicativo de hello toorun localmente, siga as etapas de saudação abaixo. Observe que essas etapas pressupõem ter PHP e SQL Server Express configurado no seu computador local e que você tenha ativado Olá [extensão PDO para SQL Server][pdo-sqlsrv].

1. Crie um Banco de Dados SQL chamado `registration`. Você pode fazer isso de saudação `sqlcmd` prompt de comando com esses comandos:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. No diretório raiz de seu aplicativo, crie dois arquivos: um chamado `createtable.php` e outro chamado `index.php`.
3. Olá abrir `createtable.php` arquivo em um editor de texto ou o IDE e adicione Olá código abaixo. Esse código será usado toocreate Olá `registration_tbl` tabela Olá `registration` banco de dados.
   
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
   
    Observe que você precisará valores hello tooupdate <code>$user</code> e <code>$pwd</code> com seu nome de usuário do SQL Server local e a senha.
4. Em um terminal no diretório raiz de saudação de saudação de tipo de aplicativo hello comando a seguir:
   
        php -S localhost:8000
5. Abra um navegador da web e navegue muito**http://localhost:8000/createtable.php**. Isso criará Olá `registration_tbl` tabela no banco de dados de saudação.
6. Olá abrir **index.php** de arquivos em um editor de texto ou o IDE e adicionar Olá HTML e CSS código básico para a página de saudação (Olá código PHP será adicionado em etapas posteriores).
   
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
7. Nas marcas PHP de hello, adicione o código PHP para a conexão de banco de dados toohello.
   
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
   
    Novamente, você precisará valores hello tooupdate <code>$user</code> e <code>$pwd</code> com seu nome de usuário do MySQL local e a senha.
8. Após o código de conexão de banco de dados hello, adicione código para inserir informações de registro no banco de dados de saudação.
   
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
9. Por fim, seguindo o código Olá acima, adicione código para recuperar dados do banco de dados de saudação.
   
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

Agora você pode procurar muito**http://localhost:8000/index.php** tootest aplicativo de hello.

## <a name="publish-your-application"></a>Publicar seu aplicativo
Depois de testar seu aplicativo localmente, você pode publicar aplicativos Web do serviço tooApp usando o Git. No entanto, você primeiro precisa de informações de conexão de banco de dados tooupdate Olá no aplicativo hello. Usando informações de conexão de banco de dados Olá obtidos anteriormente (no hello **informações de conexão de banco de dados de SQL obter** seção), atualização Olá informações a seguir **ambos** Olá `createdatabase.php` e `index.php` valores adequados de arquivos com hello:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> Em Olá <code>$host</code>, valor de saudação do servidor deve ser precedida com <code>tcp:</code>.
> 
> 

Agora, você está pronto tooset a publicação no Git e publica o aplicativo hello.

> [!NOTE]
> Esses são Olá mesmas etapas observadas no fim de saudação do hello **criar um aplicativo web do Azure e configurar a publicação de Git** seção acima.
> 
> 

1. Abrir GitBash (ou um terminal, se for Git no seu `PATH`), alterar diretórios toohello diretório de raiz do seu aplicativo (Olá **registro** directory), e execução Olá comandos a seguir:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Você será solicitado para senha Olá criado anteriormente.
2. Procurar muito**http://[web aplicativo name].azurewebsites.net/createtable.php** toocreate tabela de banco de dados SQL Olá para o aplicativo hello.
3. Procurar muito**http://[web aplicativo name].azurewebsites.net/index.php** toobegin usando o aplicativo hello.

Depois de publicar seu aplicativo, você pode começar a fazer alterações tooit e usar o Git toopublish-los. 

## <a name="publish-changes-tooyour-application"></a>Publicar alterações tooyour aplicativo
toopublish altera tooapplication, siga estas etapas:

1. Faça alterações tooyour aplicativo localmente.
2. Abra GitBash (ou um terminal it Git está no seu `PATH`), altere o diretório de raiz de toohello de diretórios do seu aplicativo e executar Olá comandos a seguir:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Você será solicitado para senha Olá criado anteriormente.
3. Procurar muito**http://[web aplicativo name].azurewebsites.net/index.php** toosee suas alterações.

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

