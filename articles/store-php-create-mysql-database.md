---
title: Criar e conectar-se a um banco de dados MySQL no Azure
description: Saiba como usar o Portal do Azure para criar um banco de dados MySQL e, em seguida, conectar-se a ele de um aplicativo Web PHP no Azure.
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
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="8413d-103">Criar e conectar-se a um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="8413d-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="8413d-104">Este tutorial mostrará como criar um banco de dados MySQL no [Portal do Azure](https://portal.azure.com) (o provedor é[ClearDB](http://www.cleardb.com/)) e como conectar a ele a partir de um aplicativo Web PHP em execução no [Serviço de Aplicativo do Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="8413d-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8413d-105">Você também pode criar um banco de dados MySQL como parte de um [modelo de aplicativo do Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8413d-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="8413d-106">Criar um banco de dados MySQL no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8413d-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="8413d-107">Para criar um banco de dados MySQL no Portal do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8413d-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="8413d-108">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8413d-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8413d-109">No menu à esquerda, clique em **Novo** > **Dados + Armazenamento** > **Banco de dados MySQL**.</span><span class="sxs-lookup"><span data-stu-id="8413d-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Criar um banco de dados MySQL no Azure - iniciar](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="8413d-111">Na [folha](azure-portal-overview.md)Novo Banco de Dados MySQL, configure seu novo banco de dados MySQL da seguinte maneira (*folha*: uma página do portal abre horizontalmente):</span><span class="sxs-lookup"><span data-stu-id="8413d-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="8413d-112">**Nome do Banco de Dados**: digite um nome que possa ser identificado de forma exclusiva</span><span class="sxs-lookup"><span data-stu-id="8413d-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="8413d-113">**Assinatura**: escolha a assinatura a ser usada</span><span class="sxs-lookup"><span data-stu-id="8413d-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="8413d-114">**Tipo de Banco de Dados**: escolha **Compartilhado** para os tipos de baixo custo ou gratuito, ou **Dedicado** para obter recursos dedicados.</span><span class="sxs-lookup"><span data-stu-id="8413d-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="8413d-115">**Grupo de recursos**: adicione o banco de dados MySQL a um [grupo de recursos](azure-resource-manager/resource-group-overview.md) existente ou coloque-o em um novo.</span><span class="sxs-lookup"><span data-stu-id="8413d-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="8413d-116">Os recursos no mesmo grupo podem ser gerenciados juntos com facilidade.</span><span class="sxs-lookup"><span data-stu-id="8413d-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="8413d-117">**Local**: escolha um local perto de você.</span><span class="sxs-lookup"><span data-stu-id="8413d-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="8413d-118">Ao adicionar a um grupo de recursos existente, você fica bloqueado no local do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8413d-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="8413d-119">**Tipo de Preço**: clique em **Tipo de Preço** e escolha uma opção de preço (o tipo **Mercury** é gratuito) e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="8413d-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="8413d-120">**Termos Legais**: clique em **Termos Legais**, examine os detalhes da compra e clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="8413d-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="8413d-121">**Fixar no painel**: selecione se você quiser acessá-lo diretamente do painel.</span><span class="sxs-lookup"><span data-stu-id="8413d-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="8413d-122">Isso é especialmente útil se você ainda não estiver familiarizado com a navegação do portal.</span><span class="sxs-lookup"><span data-stu-id="8413d-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="8413d-123">A captura de tela a seguir é apenas um exemplo de como você pode configurar o banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8413d-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Criar um banco de dados MySQL no Azure - configurar](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="8413d-125">Quando tiver concluído a configuração, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8413d-125">When you're done configuring, click **Create**.</span></span>

    ![Criar um banco de dados MySQL no Azure - criar](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="8413d-127">Você verá uma notificação pop-up informando que a implantação foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="8413d-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Criar um banco de dados MySQL no Azure - em andamento](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="8413d-129">Você receberá outro pop-up depois que a implantação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8413d-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="8413d-130">O portal também abrirá automaticamente a folha do banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8413d-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="8413d-131">Conectar-se ao seu banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="8413d-131">Connect to your MySQL database</span></span>
<span data-ttu-id="8413d-132">Para ver as informações de conexão do novo banco de dados MySQL, basta clicar em **Propriedades** na folha de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8413d-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Criar um banco de dados MySQL no Azure - folha Banco de Dados MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="8413d-134">Agora você pode usar essas informações de conexão em qualquer aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8413d-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="8413d-135">Um exemplo que mostra como usar as informações de conexão de um aplicativo PHP simples está disponível [aqui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="8413d-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="8413d-136">Conectar um aplicativo Web Laravel (a partir do tutorial de Introdução de PHP)</span><span class="sxs-lookup"><span data-stu-id="8413d-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="8413d-137">Vamos supor que você concluiu o tutorial [Criar, configurar e implantar um aplicativo Web PHP no Azure](app-service-web/app-service-web-php-get-started.md) e tem um aplicativo Web [Laravel](https://www.laravel.com/) em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="8413d-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="8413d-138">Você pode adicionar facilmente recursos de banco de dados ao seu aplicativo Laravel.</span><span class="sxs-lookup"><span data-stu-id="8413d-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="8413d-139">Basta executar as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="8413d-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="8413d-140">As etapas a seguir presumem que você concluiu o tutorial [Criar, configurar e implantar um aplicativo Web PHP no Azure](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8413d-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="8413d-141">Configure o aplicativo Laravel em seu ambiente de desenvolvimento local para apontar para o banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8413d-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="8413d-142">Para fazer isso, abra `.env` no diretório raiz de seu aplicativo Laravel e configure as opções de banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8413d-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="8413d-143">Na folha **Propriedades**, o nome do banco de dados MySQL pode ou não ser aquele mostrado no campo **NOME DO BANCO DE DADOS**.</span><span class="sxs-lookup"><span data-stu-id="8413d-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="8413d-144">É melhor verificar o parâmetro Banco de dados no campo **CADEIA DE CONEXÃO** campo.</span><span class="sxs-lookup"><span data-stu-id="8413d-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Criar um banco de dados MySQL no Azure - em andamento](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="8413d-146">A maneira mais rápida de verificar se você tem acesso ao MySQL é usar [scaffolding de autenticação padrão do Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="8413d-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="8413d-147">No terminal de linha de comando, execute os seguintes comandos do diretório raiz de seu aplicativo Laravel:</span><span class="sxs-lookup"><span data-stu-id="8413d-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="8413d-148">O primeiro comando cria as tabelas no Azure com base em migrações predefinidas no diretório `database/migrations`, e o segundo comando aplica scaffold em rotas e exibições básicas para autenticação e registro do usuário.</span><span class="sxs-lookup"><span data-stu-id="8413d-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="8413d-149">Execute o servidor de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="8413d-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="8413d-150">No navegador, navegue até http://localhost:8000 e registre um novo usuário, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="8413d-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Conectar-se ao banco de dados MySQL no Azure - registrar usuário](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="8413d-152">Siga os prompts da interface do usuário e complete o registro.</span><span class="sxs-lookup"><span data-stu-id="8413d-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="8413d-153">Após a conclusão do registro, você será conectado.</span><span class="sxs-lookup"><span data-stu-id="8413d-153">Once registration completes, you will be logged in.</span></span>

    ![Conectar-se ao banco de dados MySQL no Azure - registrar usuário](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="8413d-155">Agora você está desenvolvendo seu aplicativo no banco de dados MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="8413d-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="8413d-156">Basta apenas replicar suas configurações do `.env` em seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8413d-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="8413d-157">Execute os seguintes comandos da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="8413d-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="8413d-158">Em seguida, confirme e envie ao Azure as alterações locais feitas anteriormente durante a execução de `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="8413d-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="8413d-159">Navegue até o aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8413d-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="8413d-160">Faça logon usando as credenciais de usuário que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8413d-160">Log in using the user credentials you created earlier.</span></span>

    ![Conectar-se ao banco de dados MySQL no Azure - procurar o aplicativo Web do Azure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="8413d-162">Depois de fazer logon, você verá a tela amigável pós-logon.</span><span class="sxs-lookup"><span data-stu-id="8413d-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Conectar-se ao banco de dados MySQL no Azure - conectado](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="8413d-164">Parabéns, seu aplicativo Web PHP no Azure está acessando os dados de seu banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8413d-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8413d-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8413d-165">Next steps</span></span>
<span data-ttu-id="8413d-166">Para obter mais informações, consulte o [Centro de Desenvolvimento PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="8413d-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
