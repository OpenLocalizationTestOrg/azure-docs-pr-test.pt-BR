---
title: aaaCreate e conecte-se tooa o banco de dados MySQL no Azure
description: "Saiba como toouse Olá toocreate portal do Azure um banco de dados MySQL e, em seguida, conecte-se tooit de um aplicativo da web PHP no Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Criar e conectar-se tooa o banco de dados MySQL no Azure
Este tutorial mostra como toocreate um MySQL banco de dados em Olá [portal do Azure](https://portal.azure.com) (provedor é [ClearDB](http://www.cleardb.com/)) e como tooit tooconnect de um PHP web aplicativo em execução no [do serviço de aplicativo do Azure](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Você também pode criar um banco de dados MySQL como parte de um [modelo de aplicativo do Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Criar um banco de dados MySQL no Portal do Azure
toocreate um banco de dados MySQL no hello portal do Azure, Olá a seguir:

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **novo** > **dados + armazenamento** > **banco de dados MySQL**.

    ![Criar um banco de dados MySQL no Azure - iniciar](./media/store-php-create-mysql-database/create-db-1-start.png)
3. No novo banco de dados MySQL de saudação [folha](azure-portal-overview.md), configure seu novo banco de dados MySQL da seguinte maneira (*folha*: uma página de portal abre horizontalmente):

   * **Nome do Banco de Dados**: digite um nome que possa ser identificado de forma exclusiva
   * **Assinatura**: escolha Olá assinatura toouse
   * **Tipo de banco de dados**: selecione **compartilhado** para as camadas de baixo custo ou livres, ou **dedicado** tooget dedicado de recursos.
   * **Grupo de recursos**: Adicionar Olá MySQL banco de dados tooan existente [grupo de recursos](azure-resource-manager/resource-group-overview.md) ou colocá-lo em um novo. Recursos Olá mesmo grupo pode ser facilmente gerenciado juntos.
   * **Local**: selecione tooyou de fechar um local. Ao adicionar tooan ao grupo de recursos existente, você está local do grupo de recursos toohello bloqueado.
   * **Tipo de Preço**: clique em **Tipo de Preço** e escolha uma opção de preço (o tipo **Mercury** é gratuito) e clique em **Selecionar**.
   * **Termos legais**: clique em **termos legais**, examine os detalhes da aquisição hello e clique em **de compra**.
   * **PIN toodashboard**: selecione se deseja tooaccess-la diretamente no painel de saudação. Isso é especialmente útil se você ainda não estiver familiarizado com a navegação do portal.

     Olá captura de tela a seguir é apenas um exemplo de como você pode configurar seu banco de dados MySQL.  
     ![Criar um banco de dados MySQL no Azure - configurar](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Quando tiver concluído a configuração, clique em **Criar**.

    ![Criar um banco de dados MySQL no Azure - criar](./media/store-php-create-mysql-database/create-db-3-create.png)

    Você verá uma notificação pop-up informando que a implantação foi iniciada.

    ![Criar um banco de dados MySQL no Azure - em andamento](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Você receberá outro pop-up depois que a implantação for bem-sucedida. portal de saudação também abrir a folha de banco de dados MySQL automaticamente.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Conecte-se tooyour banco de dados MySQL
informações de conexão toosee Olá para seu novo banco de dados de MySQL, basta clicar em **propriedades** na folha do seu aplicativo web.

![Criar um banco de dados MySQL no Azure - folha Banco de Dados MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Agora você pode usar essas informações de conexão em qualquer aplicativo Web. Um exemplo que mostra como as informações de conexão do toouse Olá de um aplicativo simple do PHP estão disponíveis [aqui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Conectar um aplicativo da web Laravel (de saudação PHP get tutorial de Introdução)
Suponha que você tutorial Olá apenas terminar [criar, configurar e implantar um tooAzure de aplicativo web PHP](app-service-web/app-service-web-php-get-started.md) e ter um [Laravel](https://www.laravel.com/) aplicativo web em execução no Azure. Você pode adicionar facilmente o banco de dados recursos tooyour Laravel aplicativo. Basta seguir Olá estas etapas:

> [!NOTE]
> Olá etapas a seguir pressupõem que você concluiu o tutorial Olá [criar, configurar e implantar um tooAzure de aplicativo web PHP](app-service-web/app-service-web-php-get-started.md).
>
>

1. Configure o aplicativo de Laravel de saudação em seu local de desenvolvimento ambiente toopoint toohello banco de dados MySQL. toodo isso, abra `.env` de seu aplicativo de Laravel diretório raiz e configurar opções de banco de dados MySQL hello.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > Em Olá **propriedades** folha, nome de saudação do banco de dados MySQL pode ou não pode ser Olá um mostrados na Olá **nome do banco de dados** campo. Ele é melhor toocheck Olá banco de dados parâmetro hello **cadeia de conexão** campo.    
   >
   > ![Criar um banco de dados MySQL no Azure - em andamento](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Olá, tooverify de maneira mais rápida que agora você tem acesso ao MySQL é toouse [scaffolding de autenticação padrão do Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   No terminal de linha de comando hello, execute Olá comandos a seguir do diretório de raiz do seu aplicativo Laravel:

         php artisan migrate
         php artisan make:auth

    Olá primeiro comando cria tabelas Olá no Azure com base em migrações predefinidas no hello `database/migrations` diretório e o segundo comando de saudação scaffolds Olá exibições básicas e rotas para o registro de usuário e a autenticação.
3. Execute o servidor de desenvolvimento Olá agora:

        php artisan serve
4. No navegador de hello, navegar toohttp://localhost:8000 e registrar um novo usuário, conforme mostrado:

    ![Conectar o banco de dados tooMySQL no Azure - registrar usuário](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Siga o registro de prompt Olá completa de interface do usuário de saudação. Após a conclusão do registro, você será conectado.

    ![Conectar o banco de dados tooMySQL no Azure - registrar usuário](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Agora você está desenvolvendo seu aplicativo no banco de dados do hello MySQL no Azure.
5. Agora, você precisa apenas tooreplicate seu `.env` aplicativo de web do Azure tooyour configurações. Execute hello Azure comandos a seguir:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Em seguida, confirmar e enviar por push tooAzure Olá as alterações locais feitas anteriormente durante a execução `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Procure o aplicativo web do Azure de toohello.

        azure site browse
8. Faça logon usando as credenciais do usuário Olá criado anteriormente.

    ![Conectar tooMySQL banco de dados no Azure - procurar tooAzure web app](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Depois de entrar, você deverá ver a tela de pós-logon amigável do hello.

    ![Conectar tooMySQL banco de dados no Azure - conectado](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Parabéns, seu aplicativo Web PHP no Azure está acessando os dados de seu banco de dados MySQL.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).
