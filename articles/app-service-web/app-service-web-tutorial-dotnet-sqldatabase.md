---
title: um aplicativo ASP.NET no Azure com o banco de dados SQL do aaaBuild | Microsoft Docs
description: "Saiba como tooget um ASP.NET aplicativo trabalhando no Azure, com conexão tooa banco de dados SQL."
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="e76ae-103">Compilar um aplicativo ASP.NET no Azure com Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="e76ae-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="e76ae-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="e76ae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e76ae-105">Este tutorial mostra como toodeploy um ASP.NET controladas por dados aplicativo no Azure da web e conectá-lo muito[banco de dados do SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e76ae-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="e76ae-106">Quando você terminar, você tem um aplicativo ASP.NET em execução no [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) e conectado tooSQL banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e76ae-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Aplicativo ASP.NET publicado no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="e76ae-108">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="e76ae-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e76ae-109">Criar um Banco de Dados SQL no Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="e76ae-110">Conecte-se um aplicativo ASP.NET tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="e76ae-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="e76ae-111">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="e76ae-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e76ae-112">Atualizar o modelo de dados hello e reimplantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="e76ae-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e76ae-113">Logs de fluxo do Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="e76ae-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="e76ae-114">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e76ae-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e76ae-115">Prerequisites</span></span>

<span data-ttu-id="e76ae-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="e76ae-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="e76ae-117">Instalar [2017 do Visual Studio](https://www.visualstudio.com/downloads/) com hello cargas de trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="e76ae-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="e76ae-118">**Desenvolvimento Web e do ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="e76ae-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="e76ae-119">**Desenvolvimento do Azure**</span><span class="sxs-lookup"><span data-stu-id="e76ae-119">**Azure development**</span></span>

  ![ASP.NET, desenvolvimento Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="e76ae-121">Baixe o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="e76ae-121">Download hello sample</span></span>

<span data-ttu-id="e76ae-122">[Baixe o projeto de exemplo hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="e76ae-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="e76ae-123">Extrair (Descompactar) Olá *dotnet-sqldb tutorial master.zip* arquivo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="e76ae-124">projeto de exemplo Hello contém básico [ASP.NET MVC](https://www.asp.net/mvc) CRUD (criar-leitura-atualização-exclusão) usando o aplicativo [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="e76ae-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="e76ae-125">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="e76ae-125">Run hello app</span></span>

<span data-ttu-id="e76ae-126">Olá abrir *dotnet-sqldb-tutorial-mestre/DotNetAppSqlDb.sln* arquivo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e76ae-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="e76ae-127">Tipo `Ctrl+F5` toorun Olá aplicativo sem depuração.</span><span class="sxs-lookup"><span data-stu-id="e76ae-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="e76ae-128">Olá aplicativo é exibido no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="e76ae-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="e76ae-129">Selecione Olá **criar novo** vincular e criar algumas *tarefas* itens.</span><span class="sxs-lookup"><span data-stu-id="e76ae-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Caixa de diálogo Novo Projeto ASP .NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="e76ae-131">Saudação de teste **editar**, **detalhes**, e **excluir** links.</span><span class="sxs-lookup"><span data-stu-id="e76ae-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="e76ae-132">aplicativo Hello usa um tooconnect de contexto do banco de dados com o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="e76ae-133">Neste exemplo, o contexto de banco de dados de saudação usa uma cadeia de caracteres de conexão chamada `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="e76ae-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="e76ae-134">cadeia de caracteres de conexão de saudação é definida no hello *Web. config* arquivo e hello referenciado no *Models/MyDatabaseContext.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="e76ae-135">nome de cadeia de caracteres de conexão de saudação é usado posteriormente Olá tooconnect tutorial Olá web do Azure aplicativo tooan banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="e76ae-136">Publicar tooAzure com o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e76ae-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="e76ae-137">Em Olá **Solution Explorer**, clique com botão direito seu **DotNetAppSqlDb** do projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publicar no Gerenciador de Soluções](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="e76ae-139">Verifique se o **Serviço de Aplicativo do Microsoft Azure** está selecionado e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publicar na página de visão geral do projeto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="e76ae-141">Publicação abre Olá **criar serviço de aplicativo** caixa de diálogo, que ajuda a criar todos os Olá recursos do Azure, você precisa toorun seu aplicativo da web ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="e76ae-142">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="e76ae-142">Sign in tooAzure</span></span>

<span data-ttu-id="e76ae-143">Em Olá **criar serviço de aplicativo** caixa de diálogo, clique em **adicionar uma conta**e entre tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="e76ae-144">Se você já entrou em uma conta da Microsoft, verifique se a conta tem sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="e76ae-145">Se conectado no hello conta da Microsoft não tem a sua assinatura do Azure, clique em tooadd Olá corretas da conta.</span><span class="sxs-lookup"><span data-stu-id="e76ae-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Entrar tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="e76ae-147">Depois de conectado, você está pronto toocreate que Olá a todos os recursos que necessários para seu aplicativo web do Azure nesta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="e76ae-148">Configurar o nome do aplicativo web Olá</span><span class="sxs-lookup"><span data-stu-id="e76ae-148">Configure hello web app name</span></span>

<span data-ttu-id="e76ae-149">Você pode manter o nome do aplicativo web hello gerado ou altere-o nome exclusivo do tooanother (caracteres válidos são `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="e76ae-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="e76ae-150">nome do aplicativo web Hello é usado como parte da URL do saudação padrão para seu aplicativo (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome do aplicativo web).</span><span class="sxs-lookup"><span data-stu-id="e76ae-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="e76ae-151">nome do aplicativo web Hello precisa toobe exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Criar caixa de diálogo do serviço de aplicativo](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="e76ae-153">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e76ae-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="e76ae-154">Avançar muito**grupo de recursos**, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-154">Next too**Resource Group**, click **New**.</span></span>

![TooResource próximo grupo, clique em novo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="e76ae-156">Grupo de recursos do nome hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="e76ae-157">Não clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-157">Do not click **Create**.</span></span> <span data-ttu-id="e76ae-158">É necessário primeiro tooset um banco de dados SQL em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="e76ae-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e76ae-159">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e76ae-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e76ae-160">Avançar muito**plano do serviço de aplicativo**, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="e76ae-161">Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, configure o novo plano de serviço de aplicativo hello com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e76ae-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Criar plano de Serviço de Aplicativo](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="e76ae-163">Configuração</span><span class="sxs-lookup"><span data-stu-id="e76ae-163">Setting</span></span>  | <span data-ttu-id="e76ae-164">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="e76ae-164">Suggested value</span></span> | <span data-ttu-id="e76ae-165">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="e76ae-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="e76ae-166">**Plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="e76ae-166">**App Service Plan**</span></span>| <span data-ttu-id="e76ae-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e76ae-167">myAppServicePlan</span></span> | [<span data-ttu-id="e76ae-168">Planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e76ae-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="e76ae-169">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="e76ae-169">**Location**</span></span>| <span data-ttu-id="e76ae-170">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="e76ae-170">West Europe</span></span> | [<span data-ttu-id="e76ae-171">Regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="e76ae-172">**Tamanho**</span><span class="sxs-lookup"><span data-stu-id="e76ae-172">**Size**</span></span>| <span data-ttu-id="e76ae-173">Grátis</span><span class="sxs-lookup"><span data-stu-id="e76ae-173">Free</span></span> | [<span data-ttu-id="e76ae-174">Tipos de preço</span><span class="sxs-lookup"><span data-stu-id="e76ae-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="e76ae-175">Criar uma instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="e76ae-175">Create a SQL Server instance</span></span>

<span data-ttu-id="e76ae-176">Antes de criar um banco de dados, é necessário um [servidor lógico do Banco de dados SQL do Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="e76ae-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="e76ae-177">Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="e76ae-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="e76ae-178">Selecione **Explorar serviços adicionais do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-178">Select **Explore additional Azure services**.</span></span>

![Configurar o nome do aplicativo Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="e76ae-180">Em Olá **serviços** , clique em Olá  **+**  ícone Avançar muito**banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Na Olá serviços guia, clique no ícone + Olá tooSQL próximo banco de dados.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="e76ae-182">Em Olá **configurar banco de dados SQL** caixa de diálogo, clique em **novo** Avançar muito**do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="e76ae-183">Um nome do servidor único é gerado.</span><span class="sxs-lookup"><span data-stu-id="e76ae-183">A unique server name is generated.</span></span> <span data-ttu-id="e76ae-184">Esse nome é usado como parte da URL de padrão de saudação do seu servidor lógico, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e76ae-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="e76ae-185">Ele deve ser exclusivo em todas as instâncias do servidor lógico no Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="e76ae-186">Você pode alterar o nome do servidor de saudação, mas para este tutorial, mantenha o valor de saudação gerada.</span><span class="sxs-lookup"><span data-stu-id="e76ae-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="e76ae-187">Adicione um nome de usuário administrador e a senha e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="e76ae-188">Para requisitos de complexidade de senha, consulte [Política de Senha](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="e76ae-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="e76ae-189">Lembre desse nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="e76ae-189">Remember this username and password.</span></span> <span data-ttu-id="e76ae-190">Você precisa servidor lógico de saudação toomanage instância mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e76ae-190">You need them toomanage hello logical server instance later.</span></span>

![Criar instância do SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="e76ae-192">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e76ae-192">Create a SQL Database</span></span>

<span data-ttu-id="e76ae-193">Em Olá **configurar banco de dados SQL** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="e76ae-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="e76ae-194">Mantenha saudação padrão gerado **nome do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="e76ae-195">Em **Nome da Cadeia de Conexão**, digite *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="e76ae-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="e76ae-196">Esse nome deve corresponder a cadeia de caracteres de conexão de saudação que é referenciada em *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="e76ae-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="e76ae-197">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-197">Select **OK**.</span></span>

![Configurar banco de dados SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="e76ae-199">Olá **criar serviço de aplicativo** caixa de diálogo mostra os recursos de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="e76ae-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="e76ae-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-200">Click **Create**.</span></span> 

![recursos de saudação que você criou](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="e76ae-202">Depois que o Assistente de saudação terminar de criar hello recursos do Azure, ela publica seu tooAzure de aplicativo do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e76ae-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="e76ae-203">Navegador padrão é iniciado com hello URL toohello implantado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="e76ae-204">Adicione alguns itens de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e76ae-204">Add a few to-do items.</span></span>

![Aplicativo ASP.NET publicado no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="e76ae-206">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e76ae-206">Congratulations!</span></span> <span data-ttu-id="e76ae-207">Seu aplicativo ASP.NET controlado por dados está em execução em tempo real no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="e76ae-208">Acessar Olá localmente no banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e76ae-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="e76ae-209">O Visual Studio permite explorar e gerenciar seu novo banco de dados SQL facilmente no hello **Pesquisador de objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="e76ae-210">Criar uma conexão de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e76ae-210">Create a database connection</span></span>

<span data-ttu-id="e76ae-211">De saudação **exibição** menu, selecione **Pesquisador de objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="e76ae-212">Na parte superior de saudação do **Pesquisador de objetos do SQL Server**, clique em Olá **adicionar SQL Server** botão.</span><span class="sxs-lookup"><span data-stu-id="e76ae-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="e76ae-213">Configurar conexão do banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="e76ae-213">Configure hello database connection</span></span>

<span data-ttu-id="e76ae-214">Em Olá **conectar** caixa de diálogo, expanda Olá **Azure** nó.</span><span class="sxs-lookup"><span data-stu-id="e76ae-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="e76ae-215">Todas as suas instâncias de Banco de Dados SQL no Azure são listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="e76ae-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="e76ae-216">Selecione Olá `DotNetAppSqlDb` banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e76ae-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="e76ae-217">conexão Olá criado anteriormente é preenchido automaticamente na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="e76ae-218">Digite a senha de administrador de banco de dados Olá criado anteriormente e clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Configurar a conexão de Banco de Dados do Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="e76ae-220">Permitir conexão do cliente a partir de seu computador</span><span class="sxs-lookup"><span data-stu-id="e76ae-220">Allow client connection from your computer</span></span>

<span data-ttu-id="e76ae-221">Olá **criar uma nova regra de firewall** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="e76ae-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="e76ae-222">Por padrão, sua instância do Banco de dados SQL somente permite conexões dos serviços do Azure, como o aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="e76ae-223">tooconnect tooyour de banco de dados, crie uma regra de firewall na instância de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="e76ae-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="e76ae-224">regra de firewall Olá permite que o endereço IP público de saudação do computador local.</span><span class="sxs-lookup"><span data-stu-id="e76ae-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="e76ae-225">caixa de diálogo Olá já é preenchida com o endereço IP público do seu computador.</span><span class="sxs-lookup"><span data-stu-id="e76ae-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="e76ae-226">Certifique-se de que **Adicionar meu IP do cliente** está selecionado e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Define o firewall para as instância do Banco de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="e76ae-228">Depois que o Visual Studio termina de criar a configuração de firewall de saudação para sua instância de banco de dados SQL, sua conexão aparece na **Pesquisador de objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="e76ae-229">Aqui, você pode executar operações de banco de dados mais comuns hello, como consultas de execução, criam exibições e procedimentos armazenados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="e76ae-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="e76ae-230">Clique duas vezes em Olá `Todoes` de tabela e selecione **exibir dados**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Explorar objetos do Banco de Dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="e76ae-232">Atualizar aplicativo com Migrações do Code First</span><span class="sxs-lookup"><span data-stu-id="e76ae-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="e76ae-233">Você pode usar as ferramentas familiares do hello no Visual Studio tooupdate seu banco de dados e o aplicativo web no Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="e76ae-234">Nesta etapa, você use migrações do Code First no Entity Framework toomake um esquema de banco de dados de tooyour de alteração e publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="e76ae-235">Para obter mais informações sobre como usar as Migrações do Entity Framework Code First, consulte [Introdução ao Entity Framework 6 Code First usando MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="e76ae-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="e76ae-236">Atualizar seu modelo de dados</span><span class="sxs-lookup"><span data-stu-id="e76ae-236">Update your data model</span></span>

<span data-ttu-id="e76ae-237">Abra _Models\Todo.cs_ no editor de códigos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="e76ae-238">Adicionar Olá toohello de propriedade a seguir `ToDo` classe:</span><span class="sxs-lookup"><span data-stu-id="e76ae-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="e76ae-239">Executar Migrações do Code First localmente</span><span class="sxs-lookup"><span data-stu-id="e76ae-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="e76ae-240">Execute alguns comandos toomake atualizações tooyour banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76ae-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="e76ae-241">De saudação **ferramentas** menu, clique em **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="e76ae-242">Em Olá janela do Console do Gerenciador de pacotes, habilite migrações do Code First:</span><span class="sxs-lookup"><span data-stu-id="e76ae-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="e76ae-243">Adicione uma migração:</span><span class="sxs-lookup"><span data-stu-id="e76ae-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="e76ae-244">Atualize o banco de dados local hello:</span><span class="sxs-lookup"><span data-stu-id="e76ae-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="e76ae-245">Tipo `Ctrl+F5` toorun Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="e76ae-246">Saudação de teste editar detalhes e criar links.</span><span class="sxs-lookup"><span data-stu-id="e76ae-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="e76ae-247">Se o aplicativo hello carregado sem erros, migrações do Code First foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e76ae-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="e76ae-248">No entanto, a aparência de página ainda Olá mesmo porque a lógica do aplicativo ainda não usando essa nova propriedade.</span><span class="sxs-lookup"><span data-stu-id="e76ae-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="e76ae-249">Usar a nova propriedade de saudação</span><span class="sxs-lookup"><span data-stu-id="e76ae-249">Use hello new property</span></span>

<span data-ttu-id="e76ae-250">Fazer algumas alterações no seu Olá toouse de código `Done` propriedade.</span><span class="sxs-lookup"><span data-stu-id="e76ae-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="e76ae-251">Para simplificar este tutorial, você terá apenas Olá toochange `Index` e `Create` exibe a propriedade de saudação toosee em ação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="e76ae-252">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="e76ae-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="e76ae-253">Localize Olá `Create()` método e adicionar `Done` toohello lista de propriedades em Olá `Bind` atributo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="e76ae-254">Quando terminar, sua `Create()` assinatura do método aparência Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e76ae-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="e76ae-255">Abra _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e76ae-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="e76ae-256">Olá código Razor, você verá um `<div class="form-group">` elemento usa `model.Description`e, em seguida, outro `<div class="form-group">` elemento usa `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="e76ae-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="e76ae-257">Imediatamente após esses dois elementos, adicione outro elemento `<div class="form-group">` que usa `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="e76ae-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="e76ae-258">Abra _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e76ae-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="e76ae-259">Pesquise Olá vazio `<th></th>` elemento.</span><span class="sxs-lookup"><span data-stu-id="e76ae-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="e76ae-260">Acima desse elemento, adicione Olá código Razor a seguir:</span><span class="sxs-lookup"><span data-stu-id="e76ae-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="e76ae-261">Localize Olá `<td>` elemento que contém a saudação `Html.ActionLink()` métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="e76ae-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="e76ae-262">Acima desse elemento, adicione Olá código Razor a seguir:</span><span class="sxs-lookup"><span data-stu-id="e76ae-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="e76ae-263">Isso é tudo o que você precisa toosee alterações Olá Olá `Index` e `Create` modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="e76ae-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="e76ae-264">Tipo `Ctrl+F5` toorun Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="e76ae-265">Agora você pode adicionar um item de tarefas e marcar **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="e76ae-266">Em seguida, ele deverá aparecer na sua página inicial como um item concluído.</span><span class="sxs-lookup"><span data-stu-id="e76ae-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="e76ae-267">Lembre-se de que Olá `Edit` exibição não mostra Olá `Done` campo, porque você não alterar Olá `Edit` exibição.</span><span class="sxs-lookup"><span data-stu-id="e76ae-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="e76ae-268">Habilitar Migrações do Code First no Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="e76ae-269">Agora que seu código alterar funciona, incluindo a migração do banco de dados, você publicá-lo tooyour aplicativo de web do Azure e atualizar o banco de dados SQL com migrações do Code First muito.</span><span class="sxs-lookup"><span data-stu-id="e76ae-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="e76ae-270">Exatamente como antes, clique com o botão direito do mouse no projeto e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="e76ae-271">Clique em **configurações** tooopen Olá Assistente de publicação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Abrir as configurações de publicação](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="e76ae-273">No Assistente de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="e76ae-274">Verifique se essa cadeia de caracteres de conexão de saudação para seu banco de dados SQL é populado em **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="e76ae-275">Talvez seja necessário Olá tooselect **myToDoAppDb** banco de dados na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="e76ae-276">Selecione **Executar o Migrations do Code First (executado na inicialização do aplicativo)** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Habilitar Migrações do Code First no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="e76ae-278">Publicar suas alterações</span><span class="sxs-lookup"><span data-stu-id="e76ae-278">Publish your changes</span></span>

<span data-ttu-id="e76ae-279">Agora que as Migrações do Code First estão habilitadas no seu aplicativo Web do Azure, publique suas alterações de código.</span><span class="sxs-lookup"><span data-stu-id="e76ae-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="e76ae-280">No hello publicar página, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="e76ae-281">Tente adicionar os itens pendentes outra vez, selecione **Concluído** e os itens deverão aparecer na sua página inicial como um item concluído.</span><span class="sxs-lookup"><span data-stu-id="e76ae-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Aplicativo Web do Azure após Migração do Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="e76ae-283">Observe que todos os itens de tarefas existentes ainda são exibidos.</span><span class="sxs-lookup"><span data-stu-id="e76ae-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="e76ae-284">Quando você republicar seu aplicativo ASP.NET, os dados existentes no Banco de Dados SQL não serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="e76ae-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="e76ae-285">Além disso, migrações do Code First altera somente o esquema de dados hello e deixa os dados existentes intactas.</span><span class="sxs-lookup"><span data-stu-id="e76ae-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="e76ae-286">Transmitir logs de aplicativos</span><span class="sxs-lookup"><span data-stu-id="e76ae-286">Stream application logs</span></span>

<span data-ttu-id="e76ae-287">Você pode transmitir mensagens de rastreamento diretamente do seu aplicativo de web do Azure tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="e76ae-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="e76ae-288">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="e76ae-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="e76ae-289">Cada ação inicia com um método `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="e76ae-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="e76ae-290">Esse código é adicionado tooshow você como as mensagens de rastreamento tooadd tooyour aplicativo de web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="e76ae-291">Abra o Gerenciador de Servidores</span><span class="sxs-lookup"><span data-stu-id="e76ae-291">Open Server Explorer</span></span>

<span data-ttu-id="e76ae-292">De saudação **exibição** menu, selecione **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="e76ae-293">É possível configurar o log para o aplicativo Web do Azure no **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="e76ae-294">Habilitar streaming de log</span><span class="sxs-lookup"><span data-stu-id="e76ae-294">Enable log streaming</span></span>

<span data-ttu-id="e76ae-295">No **Gerenciador de Servidores**, expanda **Azure** > **Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="e76ae-296">Expanda Olá **myResourceGroup** grupo de recursos que você criou ao criar aplicativo web do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="e76ae-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="e76ae-297">Clique com o botão direito do mouse no aplicativo Web do Azure e selecione **Exibir Logs de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Habilitar streaming de log](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="e76ae-299">Olá logs são agora transmitidos em Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="e76ae-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Streaming de log na janela Saída](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="e76ae-301">No entanto, você não vir quaisquer mensagens de saudação do rastreamento ainda.</span><span class="sxs-lookup"><span data-stu-id="e76ae-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="e76ae-302">Isso porque, quando você seleciona pela primeira vez **Exibir Logs de Streaming**, seu aplicativo web do Azure define o nível de rastreamento de saudação muito`Error`, que registra somente eventos de erro (com hello `Trace.TraceError()` método).</span><span class="sxs-lookup"><span data-stu-id="e76ae-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="e76ae-303">Alterar níveis de rastreamento</span><span class="sxs-lookup"><span data-stu-id="e76ae-303">Change trace levels</span></span>

<span data-ttu-id="e76ae-304">rastreamento de saudação toochange níveis toooutput outras mensagens de rastreamento, vá volta muito**Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="e76ae-305">Clique com o botão direito do mouse no aplicativo Web do Azure novamente e selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="e76ae-306">Em Olá **(sistema de arquivos) de log de aplicativo** lista suspensa, selecione **detalhado**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="e76ae-307">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e76ae-307">Click **Save**.</span></span>

![Alterar tooVerbose de nível de rastreamento](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="e76ae-309">Você pode fazer experiências com toosee de níveis diferentes de rastreamento que tipos de mensagens são exibidos para cada nível.</span><span class="sxs-lookup"><span data-stu-id="e76ae-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="e76ae-310">Por exemplo, Olá **informações** nível inclui todos os logs criados por `Trace.TraceInformation()`, `Trace.TraceWarning()`, e `Trace.TraceError()`, mas não os logs criados por `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="e76ae-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="e76ae-311">No navegador, tente clicar em torno do aplicativo de lista de tarefas pendentes de hello no Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="e76ae-312">mensagens de rastreamento de saudação agora são transmitidas toohello **saída** janela no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e76ae-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="e76ae-313">Parar o streaming de log</span><span class="sxs-lookup"><span data-stu-id="e76ae-313">Stop log streaming</span></span>

<span data-ttu-id="e76ae-314">toostop Olá serviço log de streaming, clique em Olá **parar de monitorar** botão Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="e76ae-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Parar o streaming de log](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e76ae-316">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-316">Manage your Azure web app</span></span>

<span data-ttu-id="e76ae-317">Vá toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="e76ae-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="e76ae-318">No menu à esquerda do hello, clique em **do serviço de aplicativo**, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76ae-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="e76ae-320">Você aterrissou na página do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e76ae-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="e76ae-321">Por padrão, o portal de saudação mostra Olá **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="e76ae-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="e76ae-322">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e76ae-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e76ae-323">Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="e76ae-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="e76ae-324">guias de Olá no lado esquerdo de saudação da página de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="e76ae-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e76ae-326">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e76ae-326">Next steps</span></span>

<span data-ttu-id="e76ae-327">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="e76ae-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e76ae-328">Criar um Banco de Dados SQL no Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="e76ae-329">Conecte-se um aplicativo ASP.NET tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="e76ae-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="e76ae-330">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="e76ae-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e76ae-331">Atualizar o modelo de dados hello e reimplantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="e76ae-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e76ae-332">Logs de fluxo do Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="e76ae-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="e76ae-333">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e76ae-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="e76ae-334">Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome toohello web app.</span><span class="sxs-lookup"><span data-stu-id="e76ae-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e76ae-335">Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="e76ae-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
