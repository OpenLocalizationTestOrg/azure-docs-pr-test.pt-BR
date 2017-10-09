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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="8a62b-103">Criar e conectar-se tooa o banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="8a62b-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="8a62b-104">Este tutorial mostra como toocreate um MySQL banco de dados em Olá [portal do Azure](https://portal.azure.com) (provedor é [ClearDB](http://www.cleardb.com/)) e como tooit tooconnect de um PHP web aplicativo em execução no [do serviço de aplicativo do Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="8a62b-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8a62b-105">Você também pode criar um banco de dados MySQL como parte de um [modelo de aplicativo do Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8a62b-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="8a62b-106">Criar um banco de dados MySQL no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8a62b-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="8a62b-107">toocreate um banco de dados MySQL no hello portal do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a62b-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="8a62b-108">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a62b-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8a62b-109">No menu à esquerda do hello, clique em **novo** > **dados + armazenamento** > **banco de dados MySQL**.</span><span class="sxs-lookup"><span data-stu-id="8a62b-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Criar um banco de dados MySQL no Azure - iniciar](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="8a62b-111">No novo banco de dados MySQL de saudação [folha](azure-portal-overview.md), configure seu novo banco de dados MySQL da seguinte maneira (*folha*: uma página de portal abre horizontalmente):</span><span class="sxs-lookup"><span data-stu-id="8a62b-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="8a62b-112">**Nome do Banco de Dados**: digite um nome que possa ser identificado de forma exclusiva</span><span class="sxs-lookup"><span data-stu-id="8a62b-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="8a62b-113">**Assinatura**: escolha Olá assinatura toouse</span><span class="sxs-lookup"><span data-stu-id="8a62b-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="8a62b-114">**Tipo de banco de dados**: selecione **compartilhado** para as camadas de baixo custo ou livres, ou **dedicado** tooget dedicado de recursos.</span><span class="sxs-lookup"><span data-stu-id="8a62b-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="8a62b-115">**Grupo de recursos**: Adicionar Olá MySQL banco de dados tooan existente [grupo de recursos](azure-resource-manager/resource-group-overview.md) ou colocá-lo em um novo.</span><span class="sxs-lookup"><span data-stu-id="8a62b-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="8a62b-116">Recursos Olá mesmo grupo pode ser facilmente gerenciado juntos.</span><span class="sxs-lookup"><span data-stu-id="8a62b-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="8a62b-117">**Local**: selecione tooyou de fechar um local.</span><span class="sxs-lookup"><span data-stu-id="8a62b-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="8a62b-118">Ao adicionar tooan ao grupo de recursos existente, você está local do grupo de recursos toohello bloqueado.</span><span class="sxs-lookup"><span data-stu-id="8a62b-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="8a62b-119">**Tipo de Preço**: clique em **Tipo de Preço** e escolha uma opção de preço (o tipo **Mercury** é gratuito) e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="8a62b-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="8a62b-120">**Termos legais**: clique em **termos legais**, examine os detalhes da aquisição hello e clique em **de compra**.</span><span class="sxs-lookup"><span data-stu-id="8a62b-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="8a62b-121">**PIN toodashboard**: selecione se deseja tooaccess-la diretamente no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a62b-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="8a62b-122">Isso é especialmente útil se você ainda não estiver familiarizado com a navegação do portal.</span><span class="sxs-lookup"><span data-stu-id="8a62b-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="8a62b-123">Olá captura de tela a seguir é apenas um exemplo de como você pode configurar seu banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8a62b-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Criar um banco de dados MySQL no Azure - configurar](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="8a62b-125">Quando tiver concluído a configuração, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8a62b-125">When you're done configuring, click **Create**.</span></span>

    ![Criar um banco de dados MySQL no Azure - criar](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="8a62b-127">Você verá uma notificação pop-up informando que a implantação foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="8a62b-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Criar um banco de dados MySQL no Azure - em andamento](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="8a62b-129">Você receberá outro pop-up depois que a implantação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8a62b-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="8a62b-130">portal de saudação também abrir a folha de banco de dados MySQL automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8a62b-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="8a62b-131">Conecte-se tooyour banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="8a62b-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="8a62b-132">informações de conexão toosee Olá para seu novo banco de dados de MySQL, basta clicar em **propriedades** na folha do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="8a62b-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Criar um banco de dados MySQL no Azure - folha Banco de Dados MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="8a62b-134">Agora você pode usar essas informações de conexão em qualquer aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8a62b-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="8a62b-135">Um exemplo que mostra como as informações de conexão do toouse Olá de um aplicativo simple do PHP estão disponíveis [aqui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="8a62b-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="8a62b-136">Conectar um aplicativo da web Laravel (de saudação PHP get tutorial de Introdução)</span><span class="sxs-lookup"><span data-stu-id="8a62b-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="8a62b-137">Suponha que você tutorial Olá apenas terminar [criar, configurar e implantar um tooAzure de aplicativo web PHP](app-service-web/app-service-web-php-get-started.md) e ter um [Laravel](https://www.laravel.com/) aplicativo web em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="8a62b-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="8a62b-138">Você pode adicionar facilmente o banco de dados recursos tooyour Laravel aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8a62b-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="8a62b-139">Basta seguir Olá estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8a62b-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="8a62b-140">Olá etapas a seguir pressupõem que você concluiu o tutorial Olá [criar, configurar e implantar um tooAzure de aplicativo web PHP](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a62b-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="8a62b-141">Configure o aplicativo de Laravel de saudação em seu local de desenvolvimento ambiente toopoint toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8a62b-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="8a62b-142">toodo isso, abra `.env` de seu aplicativo de Laravel diretório raiz e configurar opções de banco de dados MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="8a62b-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="8a62b-143">Em Olá **propriedades** folha, nome de saudação do banco de dados MySQL pode ou não pode ser Olá um mostrados na Olá **nome do banco de dados** campo.</span><span class="sxs-lookup"><span data-stu-id="8a62b-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="8a62b-144">Ele é melhor toocheck Olá banco de dados parâmetro hello **cadeia de conexão** campo.</span><span class="sxs-lookup"><span data-stu-id="8a62b-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Criar um banco de dados MySQL no Azure - em andamento](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="8a62b-146">Olá, tooverify de maneira mais rápida que agora você tem acesso ao MySQL é toouse [scaffolding de autenticação padrão do Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="8a62b-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="8a62b-147">No terminal de linha de comando hello, execute Olá comandos a seguir do diretório de raiz do seu aplicativo Laravel:</span><span class="sxs-lookup"><span data-stu-id="8a62b-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="8a62b-148">Olá primeiro comando cria tabelas Olá no Azure com base em migrações predefinidas no hello `database/migrations` diretório e o segundo comando de saudação scaffolds Olá exibições básicas e rotas para o registro de usuário e a autenticação.</span><span class="sxs-lookup"><span data-stu-id="8a62b-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="8a62b-149">Execute o servidor de desenvolvimento Olá agora:</span><span class="sxs-lookup"><span data-stu-id="8a62b-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="8a62b-150">No navegador de hello, navegar toohttp://localhost:8000 e registrar um novo usuário, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="8a62b-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Conectar o banco de dados tooMySQL no Azure - registrar usuário](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="8a62b-152">Siga o registro de prompt Olá completa de interface do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a62b-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="8a62b-153">Após a conclusão do registro, você será conectado.</span><span class="sxs-lookup"><span data-stu-id="8a62b-153">Once registration completes, you will be logged in.</span></span>

    ![Conectar o banco de dados tooMySQL no Azure - registrar usuário](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="8a62b-155">Agora você está desenvolvendo seu aplicativo no banco de dados do hello MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="8a62b-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="8a62b-156">Agora, você precisa apenas tooreplicate seu `.env` aplicativo de web do Azure tooyour configurações.</span><span class="sxs-lookup"><span data-stu-id="8a62b-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="8a62b-157">Execute hello Azure comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a62b-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="8a62b-158">Em seguida, confirmar e enviar por push tooAzure Olá as alterações locais feitas anteriormente durante a execução `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="8a62b-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="8a62b-159">Procure o aplicativo web do Azure de toohello.</span><span class="sxs-lookup"><span data-stu-id="8a62b-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="8a62b-160">Faça logon usando as credenciais do usuário Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8a62b-160">Log in using hello user credentials you created earlier.</span></span>

    ![Conectar tooMySQL banco de dados no Azure - procurar tooAzure web app](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="8a62b-162">Depois de entrar, você deverá ver a tela de pós-logon amigável do hello.</span><span class="sxs-lookup"><span data-stu-id="8a62b-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Conectar tooMySQL banco de dados no Azure - conectado](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="8a62b-164">Parabéns, seu aplicativo Web PHP no Azure está acessando os dados de seu banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8a62b-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a62b-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a62b-165">Next steps</span></span>
<span data-ttu-id="8a62b-166">Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="8a62b-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
