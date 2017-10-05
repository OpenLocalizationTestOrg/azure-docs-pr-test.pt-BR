---
title: Compilar um aplicativo ASP.NET no Azure com Banco de Dados SQL | Microsoft Docs
description: "Saiba como obter um aplicativo ASP.NET funcionando no Azure com conexão a um Banco de Dados SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="a3a5e-103">Compilar um aplicativo ASP.NET no Azure com Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="a3a5e-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="a3a5e-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a3a5e-105">Este tutorial mostra como implantar um aplicativo Web ASP.NET controlado por dados no Azure e conectá-lo ao [Banco de Dados SQL do Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="a3a5e-106">Quando terminar, você terá um aplicativo ASP.NET em execução no [Serviço de Aplicativo do Azure ](../app-service/app-service-value-prop-what-is.md) e conectado ao Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Aplicativo ASP.NET publicado no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="a3a5e-108">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3a5e-109">Criar um Banco de Dados SQL no Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="a3a5e-110">Conectar um aplicativo ASP.NET ao Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="a3a5e-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="a3a5e-111">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="a3a5e-112">Atualizar o modelo de dados e reimplantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="a3a5e-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="a3a5e-113">Transmitir logs do Azure para seu terminal</span><span class="sxs-lookup"><span data-stu-id="a3a5e-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="a3a5e-114">Gerenciar o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3a5e-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3a5e-115">Prerequisites</span></span>

<span data-ttu-id="a3a5e-116">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-116">To complete this tutorial:</span></span>

* <span data-ttu-id="a3a5e-117">Instale o [Visual Studio 2017](https://www.visualstudio.com/downloads/) com as cargas de trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="a3a5e-118">**Desenvolvimento Web e do ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="a3a5e-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="a3a5e-119">**Desenvolvimento do Azure**</span><span class="sxs-lookup"><span data-stu-id="a3a5e-119">**Azure development**</span></span>

  ![ASP.NET, desenvolvimento Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="a3a5e-121">Baixar o exemplo</span><span class="sxs-lookup"><span data-stu-id="a3a5e-121">Download the sample</span></span>

<span data-ttu-id="a3a5e-122">[Baixar o projeto de exemplo](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="a3a5e-123">Extrair (descompactar) o arquivo *dotnet-sqldb-tutorial-master.zip*.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="a3a5e-124">Esse projeto de exemplo contém um aplicativo [ASP.NET MVC](https://www.asp.net/mvc) CRUD (criar-ler-atualizar-excluir) básico usando o [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="a3a5e-125">Execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="a3a5e-125">Run the app</span></span>

<span data-ttu-id="a3a5e-126">Abra o arquivo *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="a3a5e-127">Tipo `Ctrl+F5` para executar o aplicativo sem depuração.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="a3a5e-128">O aplicativo é exibido no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="a3a5e-129">Selecione o link **Criar novo** e crie alguns itens *de tarefas*.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Caixa de diálogo Novo Projeto ASP .NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="a3a5e-131">Teste os links **Editar**, **Detalhes** e **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="a3a5e-132">O aplicativo usa um contexto de banco de dados para se conectar com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="a3a5e-133">Neste exemplo, o contexto do banco de dados usa uma cadeia de conexão chamada `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="a3a5e-134">Essa cadeia de conexão é definida no arquivo *Web. config* e é referenciada no arquivo *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="a3a5e-135">O nome da cadeia de conexão é usado no tutorial posteriormente para conectar o aplicativo Web do Azure a um Banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="a3a5e-136">Publicar no Azure com o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="a3a5e-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="a3a5e-137">No **Gerenciador de Soluções**, clique com botão direito no projeto **DotNetAppSqlD** e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publicar no Gerenciador de Soluções](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="a3a5e-139">Verifique se o **Serviço de Aplicativo do Microsoft Azure** está selecionado e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publicar na página de visão geral do projeto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="a3a5e-141">A publicação abre a caixa de diálogo **Criar Serviço de Aplicativo**, o que ajuda a criar todos os recursos do Azure necessários para executar seu aplicativo Web ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="a3a5e-142">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-142">Sign in to Azure</span></span>

<span data-ttu-id="a3a5e-143">Na caixa de diálogo **Criar Serviço de Aplicativo**, clique em **Adicionar uma conta**, depois, faça logon em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="a3a5e-144">Se você já entrou em uma conta da Microsoft, verifique se a conta tem sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="a3a5e-145">Se a conta da Microsoft conectada não tiver sua assinatura do Azure, clique nela para adicionar a conta correta.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Entrar no Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="a3a5e-147">Depois de conectado, você está pronto para criar todos os recursos necessários para seu aplicativo Web do Azure nesta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="a3a5e-148">Configurar o nome do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a3a5e-148">Configure the web app name</span></span>

<span data-ttu-id="a3a5e-149">Você pode manter o nome do aplicativo Web gerado ou alterá-lo para outro nome exclusivo (caracteres válidos são `a-z`, `0-9` e `-`).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="a3a5e-150">O nome do aplicativo Web é usado como parte da URL padrão para seu aplicativo (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome do aplicativo Web).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="a3a5e-151">O nome do aplicativo Web precisa ser exclusivo em todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![Criar caixa de diálogo do serviço de aplicativo](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="a3a5e-153">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a3a5e-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="a3a5e-154">Lado do **Grupo de Recursos**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-154">Next to **Resource Group**, click **New**.</span></span>

![Ao lado do Grupo de Recursos, clique em Novo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="a3a5e-156">Nomeie o grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="a3a5e-157">Não clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-157">Do not click **Create**.</span></span> <span data-ttu-id="a3a5e-158">Primeiro, você precisa configurar um Banco de Dados SQL na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a3a5e-159">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a3a5e-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="a3a5e-160">Lado do **Plano do Serviço de Aplicativo**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="a3a5e-161">Na caixa de diálogo **Configurar Plano do Serviço de Aplicativo**, configure o novo plano do Serviço de Aplicativo com as seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Criar plano de Serviço de Aplicativo](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="a3a5e-163">Configuração</span><span class="sxs-lookup"><span data-stu-id="a3a5e-163">Setting</span></span>  | <span data-ttu-id="a3a5e-164">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="a3a5e-164">Suggested value</span></span> | <span data-ttu-id="a3a5e-165">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="a3a5e-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="a3a5e-166">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="a3a5e-166">**App Service Plan**</span></span>| <span data-ttu-id="a3a5e-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a3a5e-167">myAppServicePlan</span></span> | [<span data-ttu-id="a3a5e-168">Planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a3a5e-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="a3a5e-169">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="a3a5e-169">**Location**</span></span>| <span data-ttu-id="a3a5e-170">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="a3a5e-170">West Europe</span></span> | [<span data-ttu-id="a3a5e-171">Regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="a3a5e-172">**Tamanho**</span><span class="sxs-lookup"><span data-stu-id="a3a5e-172">**Size**</span></span>| <span data-ttu-id="a3a5e-173">Grátis</span><span class="sxs-lookup"><span data-stu-id="a3a5e-173">Free</span></span> | [<span data-ttu-id="a3a5e-174">Tipos de preço</span><span class="sxs-lookup"><span data-stu-id="a3a5e-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="a3a5e-175">Criar uma instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="a3a5e-175">Create a SQL Server instance</span></span>

<span data-ttu-id="a3a5e-176">Antes de criar um banco de dados, é necessário um [servidor lógico do Banco de dados SQL do Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="a3a5e-177">Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="a3a5e-178">Selecione **Explorar serviços adicionais do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-178">Select **Explore additional Azure services**.</span></span>

![Configurar o nome do aplicativo Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="a3a5e-180">Na guia **Serviços** clique no ícone **+** próximo ao **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![Na guia Serviços, clique no ícone + próximo ao Banco de Dados SQL.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="a3a5e-182">Na caixa de diálogo **Configurar Banco de Dados SQL**, clique em **Novo** próximo ao **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="a3a5e-183">Um nome do servidor único é gerado.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-183">A unique server name is generated.</span></span> <span data-ttu-id="a3a5e-184">Esse nome é usado como parte da URL padrão do seu servidor lógico, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="a3a5e-185">Ele deve ser exclusivo em todas as instâncias do servidor lógico no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="a3a5e-186">Você pode alterar o nome do servidor, mas para este tutorial, mantenha o valor gerado.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="a3a5e-187">Adicione um nome de usuário administrador e a senha e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="a3a5e-188">Para requisitos de complexidade de senha, consulte [Política de Senha](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="a3a5e-189">Lembre desse nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-189">Remember this username and password.</span></span> <span data-ttu-id="a3a5e-190">Você precisa deles para gerenciar a instância de servidor lógico mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-190">You need them to manage the logical server instance later.</span></span>

![Criar instância do SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="a3a5e-192">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="a3a5e-192">Create a SQL Database</span></span>

<span data-ttu-id="a3a5e-193">Na caixa de diálogo **Configurar Banco de Dados SQL**:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="a3a5e-194">Mantenha o **Nome do banco de dados** padrão gerado.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="a3a5e-195">Em **Nome da Cadeia de Conexão**, digite *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="a3a5e-196">Esse nome deve corresponder à cadeia de conexão que está referenciada em *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="a3a5e-197">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-197">Select **OK**.</span></span>

![Configurar banco de dados SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="a3a5e-199">A caixa de diálogo **Criar Serviço de Aplicativo** mostra os recursos que você criou.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="a3a5e-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-200">Click **Create**.</span></span> 

![os recursos que você criou](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="a3a5e-202">Depois que o assistente terminar de criar os recursos do Azure, ele publica seu aplicativo ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="a3a5e-203">Seu navegador padrão é iniciado com a URL para o aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="a3a5e-204">Adicione alguns itens de tarefas.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-204">Add a few to-do items.</span></span>

![Aplicativo ASP.NET publicado no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="a3a5e-206">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a3a5e-206">Congratulations!</span></span> <span data-ttu-id="a3a5e-207">Seu aplicativo ASP.NET controlado por dados está em execução em tempo real no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="a3a5e-208">Acessar o Banco de Dados SQL localmente</span><span class="sxs-lookup"><span data-stu-id="a3a5e-208">Access the SQL Database locally</span></span>

<span data-ttu-id="a3a5e-209">O Visual Studio permite pesquisar e gerenciar seu novo Banco de Dados SQL facilmente no **Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="a3a5e-210">Criar uma conexão de banco de dados</span><span class="sxs-lookup"><span data-stu-id="a3a5e-210">Create a database connection</span></span>

<span data-ttu-id="a3a5e-211">No menu **Visualizar**, selecione **Pesquisador de objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="a3a5e-212">Na parte superior do **Pesquisador de Objetos do SQL Server**, clique no botão **Adicionar SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="a3a5e-213">Configurar a conexão de banco de dados</span><span class="sxs-lookup"><span data-stu-id="a3a5e-213">Configure the database connection</span></span>

<span data-ttu-id="a3a5e-214">Na caixa de diálogo **Conectar**, expanda o nó **Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="a3a5e-215">Todas as suas instâncias de Banco de Dados SQL no Azure são listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="a3a5e-216">Selecione o Banco de Dados SQL `DotNetAppSqlDb`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="a3a5e-217">A conexão criada antes é automaticamente preenchida na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="a3a5e-218">Digite a senha de administrador de banco de dados que você criou anteriormente e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Configurar a conexão de Banco de Dados do Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="a3a5e-220">Permitir conexão do cliente a partir de seu computador</span><span class="sxs-lookup"><span data-stu-id="a3a5e-220">Allow client connection from your computer</span></span>

<span data-ttu-id="a3a5e-221">A caixa de diálogo **Crie uma nova regra de firewall** é aberta.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="a3a5e-222">Por padrão, sua instância do Banco de dados SQL somente permite conexões dos serviços do Azure, como o aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="a3a5e-223">Para se conectar ao banco de dados, crie uma regra de firewall na instância do Banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="a3a5e-224">A regra de firewall permite o endereço IP público do seu computador local.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="a3a5e-225">A caixa de diálogo já está preenchida com o endereço IP público do seu computador.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="a3a5e-226">Certifique-se de que **Adicionar meu IP do cliente** está selecionado e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Define o firewall para as instância do Banco de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="a3a5e-228">Quando o Visual Studio terminar de criar a configuração de firewall para a instância do Banco de dados SQL, sua conexão aparecerá no **Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="a3a5e-229">Aqui, você pode executar as operações de banco de dados mais comuns, como executar consultas, criar exibições, procedimentos armazenados e, muito mais.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="a3a5e-230">Clique com o botão direito do mouse na tabela `Todoes` e selecione **Exibir Dados**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Explorar objetos do Banco de Dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="a3a5e-232">Atualizar aplicativo com Migrações do Code First</span><span class="sxs-lookup"><span data-stu-id="a3a5e-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="a3a5e-233">Você pode usar as ferramentas familiares do Visual Studio para atualizar o banco de dados e o aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="a3a5e-234">Nesta etapa, você usará Migrações do Code First no Entity Framework para fazer uma alteração no seu esquema de banco de dados e publicá-lo no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="a3a5e-235">Para obter mais informações sobre como usar as Migrações do Entity Framework Code First, consulte [Introdução ao Entity Framework 6 Code First usando MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="a3a5e-236">Atualizar seu modelo de dados</span><span class="sxs-lookup"><span data-stu-id="a3a5e-236">Update your data model</span></span>

<span data-ttu-id="a3a5e-237">Abra _Models\Todo.cs_ no editor de códigos.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="a3a5e-238">Adicione a seguinte propriedade à classe `ToDo`:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="a3a5e-239">Executar Migrações do Code First localmente</span><span class="sxs-lookup"><span data-stu-id="a3a5e-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="a3a5e-240">Execute alguns comandos para fazer as atualizações para seu banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="a3a5e-241">A partir do menu **Ferramentas** clique em **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="a3a5e-242">Na janela do Console do Gerenciador de Pacotes, habilite as Migrações do Code First:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="a3a5e-243">Adicione uma migração:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="a3a5e-244">Atualize o banco de dados local:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="a3a5e-245">Digite `Ctrl+F5` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="a3a5e-246">Teste os links editar, detalhes e criar.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="a3a5e-247">Se o aplicativo for carregado sem erros, as Migrações do Code First tiveram êxito.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="a3a5e-248">No entanto, sua página ainda tem a mesma aparência porque a lógica de aplicativo ainda não está usando essa nova propriedade.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="a3a5e-249">Usar a nova propriedade</span><span class="sxs-lookup"><span data-stu-id="a3a5e-249">Use the new property</span></span>

<span data-ttu-id="a3a5e-250">Faça algumas alterações em seu código para usar a propriedade `Done`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="a3a5e-251">Para simplificar este tutorial, somente as exibições `Index` e `Create` serão alteradas para observar a propriedade em ação.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="a3a5e-252">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="a3a5e-253">Localize o `Create()` método e adicione `Done` à lista de propriedades no atributo `Bind`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="a3a5e-254">Quando terminar, a assinatura do método `Create()` deverá ter o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="a3a5e-255">Abra _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="a3a5e-256">No código do Razor, você deve ver um elemento `<div class="form-group">` que usa `model.Description` e outro elemento `<div class="form-group">` que usa `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="a3a5e-257">Imediatamente após esses dois elementos, adicione outro elemento `<div class="form-group">` que usa `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="a3a5e-258">Abra _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="a3a5e-259">Procure o elemento vazio `<th></th>`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="a3a5e-260">Logo acima desse elemento, adicione o seguinte código do Razor:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="a3a5e-261">Localize o elemento `<td>` que contém os métodos auxiliares `Html.ActionLink()`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="a3a5e-262">Logo acima desse elemento, adicione o seguinte código do Razor:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="a3a5e-263">Isso é tudo o que você precisa para ver as alterações nas exibições `Index` e `Create`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="a3a5e-264">Digite `Ctrl+F5` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="a3a5e-265">Agora você pode adicionar um item de tarefas e marcar **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="a3a5e-266">Em seguida, ele deverá aparecer na sua página inicial como um item concluído.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="a3a5e-267">Lembre-se de que a exibição `Edit` não mostra o campo `Done`, porque você não alterou a exibição `Edit`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="a3a5e-268">Habilitar Migrações do Code First no Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="a3a5e-269">Agora que a alteração de código funciona, incluindo a migração de banco de dados, você também publica-o em seu aplicativo Web do Azure e atualiza seu Banco de Dados SQL com as Migrações do Code First.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="a3a5e-270">Exatamente como antes, clique com o botão direito do mouse no projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="a3a5e-271">Clique em **Configurações** para abrir o assistente de publicação.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-271">Click **Settings** to open the publish wizard.</span></span>

![Abrir as configurações de publicação](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="a3a5e-273">No assistente, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="a3a5e-274">Certifique-se de que a cadeia de conexão do banco de dados SQL está preenchida em **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="a3a5e-275">Talvez seja necessário selecionar o banco de dados **myToDoAppDb** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="a3a5e-276">Selecione **Executar o Migrations do Code First (executado na inicialização do aplicativo)** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Habilitar Migrações do Code First no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="a3a5e-278">Publicar suas alterações</span><span class="sxs-lookup"><span data-stu-id="a3a5e-278">Publish your changes</span></span>

<span data-ttu-id="a3a5e-279">Agora que as Migrações do Code First estão habilitadas no seu aplicativo Web do Azure, publique suas alterações de código.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="a3a5e-280">Na página de publicação, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="a3a5e-281">Tente adicionar os itens pendentes outra vez, selecione **Concluído** e os itens deverão aparecer na sua página inicial como um item concluído.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Aplicativo Web do Azure após Migração do Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="a3a5e-283">Observe que todos os itens de tarefas existentes ainda são exibidos.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="a3a5e-284">Quando você republicar seu aplicativo ASP.NET, os dados existentes no Banco de Dados SQL não serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="a3a5e-285">Além disso, as Migrações do Code First apenas alteram o esquema de dados e deixam os dados existentes intactos.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="a3a5e-286">Transmitir logs de aplicativos</span><span class="sxs-lookup"><span data-stu-id="a3a5e-286">Stream application logs</span></span>

<span data-ttu-id="a3a5e-287">É possível transmitir mensagens de rastreamento diretamente do seu aplicativo Web do Azure para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="a3a5e-288">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="a3a5e-289">Cada ação inicia com um método `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="a3a5e-290">Esse código é adicionado para mostrar como adicionar mensagens de rastreamento ao seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="a3a5e-291">Abra o Gerenciador de Servidores</span><span class="sxs-lookup"><span data-stu-id="a3a5e-291">Open Server Explorer</span></span>

<span data-ttu-id="a3a5e-292">No menu **Visualizar**, selecione **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="a3a5e-293">É possível configurar o log para o aplicativo Web do Azure no **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="a3a5e-294">Habilitar streaming de log</span><span class="sxs-lookup"><span data-stu-id="a3a5e-294">Enable log streaming</span></span>

<span data-ttu-id="a3a5e-295">No **Gerenciador de Servidores**, expanda **Azure** > **Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="a3a5e-296">Expanda o grupo de recursos**myResourceGroup** que você criou, ao criar pela primeira vez o aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="a3a5e-297">Clique com o botão direito do mouse no aplicativo Web do Azure e selecione **Exibir Logs de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Habilitar streaming de log](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="a3a5e-299">Os logs agora são transmitidos na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-299">The logs are now streamed into the **Output** window.</span></span> 

![Streaming de log na janela Saída](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="a3a5e-301">No entanto, ainda não é possível ver nenhuma das mensagens de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="a3a5e-302">Isso ocorre porque ao selecionar **Exibir Logs de Streaming**, seu aplicativo Web do Azure define o nível de rastreamento como `Error` que registra apenas eventos de erros (com o método`Trace.TraceError()`).</span><span class="sxs-lookup"><span data-stu-id="a3a5e-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="a3a5e-303">Alterar níveis de rastreamento</span><span class="sxs-lookup"><span data-stu-id="a3a5e-303">Change trace levels</span></span>

<span data-ttu-id="a3a5e-304">Para alterar os níveis de rastreamento e exibir outras mensagens de rastreamento, retorne para o **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="a3a5e-305">Clique com o botão direito do mouse no aplicativo Web do Azure novamente e selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="a3a5e-306">Na lista suspensa **Log de Aplicativo (Sistema de Arquivos)**, selecione **detalhado**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="a3a5e-307">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-307">Click **Save**.</span></span>

![Alterar nível de rastreamento para Detalhado](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="a3a5e-309">Você pode testar diferentes níveis de rastreamento para ver quais tipos de mensagens são exibidos para cada nível.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="a3a5e-310">Por exemplo, o nível **Informações** inclui todos os logs criados por `Trace.TraceInformation()`, `Trace.TraceWarning()` e `Trace.TraceError()`, mas não os logs criados por `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="a3a5e-311">Em seu navegador, tente clicar no aplicativo de lista de tarefas no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="a3a5e-312">As mensagens de rastreamento agora são transmitidas para a janela **Saída** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="a3a5e-313">Parar o streaming de log</span><span class="sxs-lookup"><span data-stu-id="a3a5e-313">Stop log streaming</span></span>

<span data-ttu-id="a3a5e-314">Para interromper o serviço de streaming de log, clique no botão **Parar Monitoramento** na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Parar o streaming de log](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="a3a5e-316">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-316">Manage your Azure web app</span></span>

<span data-ttu-id="a3a5e-317">Vá para o [portal do Azure](https://portal.azure.com) para ver o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="a3a5e-318">No menu à esquerda, clique em **Serviço de Aplicativo**, em seguida, clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="a3a5e-320">Você aterrissou na página do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="a3a5e-321">Por padrão, o portal mostra a página **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="a3a5e-322">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="a3a5e-323">Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="a3a5e-324">As guias no lado esquerdo da página mostram as páginas de configuração diferentes que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="a3a5e-326">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3a5e-326">Next steps</span></span>

<span data-ttu-id="a3a5e-327">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="a3a5e-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3a5e-328">Criar um Banco de Dados SQL no Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="a3a5e-329">Conectar um aplicativo ASP.NET ao Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="a3a5e-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="a3a5e-330">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="a3a5e-331">Atualizar o modelo de dados e reimplantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="a3a5e-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="a3a5e-332">Transmitir logs do Azure para seu terminal</span><span class="sxs-lookup"><span data-stu-id="a3a5e-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="a3a5e-333">Gerenciar o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="a3a5e-334">Vá para o próximo tutorial para aprender a mapear um nome DNS personalizado para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a3a5e-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3a5e-335">Mapear um nome DNS personalizado existente para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="a3a5e-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
