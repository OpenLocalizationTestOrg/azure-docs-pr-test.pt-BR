---
title: 'Portal do Azure: Criar um banco de dados SQL | Microsoft Docs'
description: "Aprenda a criar um servidor lógico do Banco de Dados SQL, uma regra de firewall no nível de servidor e bancos de dados com o portal do Azure. Saiba também como consultar um Banco de Dados SQL do Azure usando o Portal do Azure."
keywords: tutorial do banco de dados SQL, criar um banco de dados SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: a863cf3ad08040906850f64db6505f30bcfa72eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="5a631-105">Criar um Banco de Dados SQL do Azure no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5a631-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="5a631-106">Este tutorial de início rápido percorre como criar um banco de dados SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="5a631-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="5a631-107">O Banco de Dados SQL do Azure é uma oferta de "Banco de Dados como Serviço" que permite executar e dimensionar os bancos de dados do SQL Server altamente disponíveis na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5a631-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="5a631-108">Este guia rápido mostra como começar criando um banco de dados SQL com o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a631-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="5a631-109">Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="5a631-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="5a631-110">Faça logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5a631-110">Log in to the Azure portal</span></span>

<span data-ttu-id="5a631-111">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5a631-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="5a631-112">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5a631-112">Create a SQL database</span></span>

<span data-ttu-id="5a631-113">Um banco de dados SQL do Azure é criado com um conjunto definido de [recursos de computação e armazenamento](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="5a631-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="5a631-114">O banco de dados é criado dentro de um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) e em um [servidor lógico de banco de dados SQL do Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="5a631-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="5a631-115">Execute estas etapas para criar um Banco de Dados SQL que contém os dados de exemplo do Adventure Works LT.</span><span class="sxs-lookup"><span data-stu-id="5a631-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="5a631-116">Clique no botão **Novo** no canto superior esquerdo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a631-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="5a631-117">Selecione **Bancos de Dados** na página **Novo** e **Banco de Dados SQL** na página **Bancos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="5a631-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

   ![criar database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="5a631-119">Preencha o formulário do Banco de Dados SQL com as informações abaixo, conforme mostrado na imagem anterior:</span><span class="sxs-lookup"><span data-stu-id="5a631-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="5a631-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="5a631-120">Setting</span></span>       | <span data-ttu-id="5a631-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5a631-121">Suggested value</span></span> | <span data-ttu-id="5a631-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a631-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="5a631-123">**Nome do banco de dados**</span><span class="sxs-lookup"><span data-stu-id="5a631-123">**Database name**</span></span> | <span data-ttu-id="5a631-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="5a631-124">mySampleDatabase</span></span> | <span data-ttu-id="5a631-125">Para ver os nomes do banco de dados válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="5a631-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="5a631-126">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="5a631-126">**Subscription**</span></span> | <span data-ttu-id="5a631-127">Sua assinatura</span><span class="sxs-lookup"><span data-stu-id="5a631-127">Your subscription</span></span>  | <span data-ttu-id="5a631-128">Para obter detalhes sobre suas assinaturas, consulte [Assinaturas](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5a631-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="5a631-129">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="5a631-129">**Resource group**</span></span>  | <span data-ttu-id="5a631-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5a631-130">myResourceGroup</span></span> | <span data-ttu-id="5a631-131">Para ver os nomes do grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="5a631-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="5a631-132">**Fonte da origem**</span><span class="sxs-lookup"><span data-stu-id="5a631-132">**Source source**</span></span> | <span data-ttu-id="5a631-133">Exemplo (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="5a631-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="5a631-134">Carrega o esquema AdventureWorksLT e os dados no novo banco de dados</span><span class="sxs-lookup"><span data-stu-id="5a631-134">Loads the AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="5a631-135">Você deve selecionar o banco de dados de exemplo neste formulário porque ele é usado no restante deste início rápido.</span><span class="sxs-lookup"><span data-stu-id="5a631-135">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="5a631-136">Em **Servidor**, clique em **Definir configurações obrigatórias** e preencha o formulário do SQL Server (servidor lógico) com as informações abaixo, conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a631-136">Under **Server**, click **Configure required settings** and fill out the SQL server (logical server) form with the following information, as shown on the following image:</span></span>   

   | <span data-ttu-id="5a631-137">Configuração</span><span class="sxs-lookup"><span data-stu-id="5a631-137">Setting</span></span>       | <span data-ttu-id="5a631-138">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5a631-138">Suggested value</span></span> | <span data-ttu-id="5a631-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a631-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="5a631-140">**Nome do servidor**</span><span class="sxs-lookup"><span data-stu-id="5a631-140">**Server name**</span></span> | <span data-ttu-id="5a631-141">Qualquer nome exclusivo globalmente</span><span class="sxs-lookup"><span data-stu-id="5a631-141">Any globally unique name</span></span> | <span data-ttu-id="5a631-142">Para ver os nomes do servidor válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="5a631-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="5a631-143">**Logon de administrador do servidor**</span><span class="sxs-lookup"><span data-stu-id="5a631-143">**Server admin login**</span></span> | <span data-ttu-id="5a631-144">Qualquer nome válido</span><span class="sxs-lookup"><span data-stu-id="5a631-144">Any valid name</span></span> | <span data-ttu-id="5a631-145">Para ver os nomes de logon válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="5a631-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="5a631-146">**Senha**</span><span class="sxs-lookup"><span data-stu-id="5a631-146">**Password**</span></span> | <span data-ttu-id="5a631-147">Qualquer senha válida</span><span class="sxs-lookup"><span data-stu-id="5a631-147">Any valid password</span></span> | <span data-ttu-id="5a631-148">Sua senha deve ter, pelo menos, oito caracteres e deve conter caracteres de três das seguintes categorias: caracteres com letras maiúsculas, letras minúsculas, números e caracteres não alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="5a631-148">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="5a631-149">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="5a631-149">**Subscription**</span></span> | <span data-ttu-id="5a631-150">Sua assinatura</span><span class="sxs-lookup"><span data-stu-id="5a631-150">Your subscription</span></span> | <span data-ttu-id="5a631-151">Para obter detalhes sobre suas assinaturas, consulte [Assinaturas](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5a631-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="5a631-152">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="5a631-152">**Resource group**</span></span> | <span data-ttu-id="5a631-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5a631-153">myResourceGroup</span></span> | <span data-ttu-id="5a631-154">Para ver os nomes do grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="5a631-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="5a631-155">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="5a631-155">**Location**</span></span> | <span data-ttu-id="5a631-156">Qualquer local válido</span><span class="sxs-lookup"><span data-stu-id="5a631-156">Any valid location</span></span> | <span data-ttu-id="5a631-157">Para obter mais informações sobre as regiões, consulte [Regiões do Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="5a631-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="5a631-158">O logon de administrador do servidor e a senha que você especificar aqui são necessárias para fazer logon no servidor e em seus bancos de dados mais tarde neste início rápido.</span><span class="sxs-lookup"><span data-stu-id="5a631-158">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="5a631-159">Lembre-se ou registre essas informações para o uso posterior.</span><span class="sxs-lookup"><span data-stu-id="5a631-159">Remember or record this information for later use.</span></span> 
   >  

   ![criar database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="5a631-161">Quando tiver concluído o formulário, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5a631-161">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="5a631-162">Clique em **Tipo de preço** para especificar o nível de desempenho e o tipo de serviço para o novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5a631-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="5a631-163">Use o controle deslizante para selecionar **20 DTUs** e **250** GB de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5a631-163">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="5a631-164">Para obter mais informações sobre as DTUs, consulte [O que é DTU?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="5a631-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![Criar database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="5a631-166">Depois de selecionar a quantidade de DTUs, clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5a631-166">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="5a631-167">Agora que você concluiu o formulário do Banco de Dados SQL, clique em **Criar** para provisionar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5a631-167">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="5a631-168">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5a631-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="5a631-169">Na barra de ferramentas, clique em **Notificações** para monitorar o processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="5a631-169">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![notificação](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="5a631-171">Criar uma regra de firewall no nível de servidor</span><span class="sxs-lookup"><span data-stu-id="5a631-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="5a631-172">O serviço do Banco de Dados SQL cria um firewall no nível do servidor impedindo que os aplicativos e ferramentas externos conectem o servidor ou os bancos de dados no servidor, a menos que uma regra de firewall seja criada para abrir o firewall para endereços IP específicos.</span><span class="sxs-lookup"><span data-stu-id="5a631-172">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="5a631-173">Execute estas etapas a fim de criar uma [regra de firewall no nível do servidor do Banco de Dados SQL](sql-database-firewall-configure.md) para o endereço IP do seu cliente e habilitar a conectividade externa por meio do firewall do Banco de Dados SQL somente para seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="5a631-173">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="5a631-174">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="5a631-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5a631-175">Se você estiver tentando conectar-se a partir de uma rede corporativa, o tráfego de saída pela porta 1433 poderá não ser permitido pelo firewall de sua rede.</span><span class="sxs-lookup"><span data-stu-id="5a631-175">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5a631-176">Se isto acontecer, você não poderá conectar o servidor do Banco de Dados SQL do Azure, a menos que o departamento de TI abra a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="5a631-176">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="5a631-177">Depois da implantação ser concluída, clique em **Bancos de dados SQL** no menu à esquerda, depois, clique em **mySampleDatabase** na página **Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="5a631-177">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="5a631-178">Uma página de visão geral de seu banco de dados é aberta, mostrando o nome totalmente qualificado do servidor (como **mynewserver20170313.database.windows.net**) e fornece opções para configurações adicionais.</span><span class="sxs-lookup"><span data-stu-id="5a631-178">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="5a631-179">Copie esse nome totalmente qualificado do servidor para um uso posterior.</span><span class="sxs-lookup"><span data-stu-id="5a631-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5a631-180">Você precisará desse nome totalmente qualificado do servidor para conectar o servidor e seus bancos de dados nos inícios rápidos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="5a631-180">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![nome do servidor](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="5a631-182">Clique em **Definir o firewall do servidor** na barra de ferramentas, conforme mostrado na imagem anterior.</span><span class="sxs-lookup"><span data-stu-id="5a631-182">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="5a631-183">A página **Configurações do firewall** do servidor de Banco de Dados SQL é aberta.</span><span class="sxs-lookup"><span data-stu-id="5a631-183">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="5a631-185">Clique em **Adicionar IP do cliente** na barra de ferramentas para adicionar seu endereço IP atual a uma nova regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="5a631-185">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="5a631-186">Uma regra de firewall pode abrir a porta 1433 para um único endereço IP ou um intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="5a631-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="5a631-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5a631-187">Click **Save**.</span></span> <span data-ttu-id="5a631-188">Uma regra de firewall no nível do servidor é criada para a porta de abertura 1433 de seu endereço IP atual no servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="5a631-188">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![definir regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="5a631-190">Clique em **OK**, em seguida, feche a página **Configurações do Firewall**.</span><span class="sxs-lookup"><span data-stu-id="5a631-190">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="5a631-191">Agora, você pode conectar o servidor do Banco de Dados SQL e seus bancos de dados usando o SQL Server Management Studio ou outra ferramenta de sua escolha neste endereço IP usando a conta do administrador do servidor criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5a631-191">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a631-192">Por padrão, o acesso através do firewall do Banco de Dados SQL está habilitado para todos os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a631-192">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="5a631-193">Clique em **DESATIVAR** nesta página para desabilitar todos os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a631-193">Click **OFF** on this page to disable for all Azure services.</span></span>
>

## <a name="query-the-sql-database"></a><span data-ttu-id="5a631-194">Consultar o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5a631-194">Query the SQL database</span></span>

<span data-ttu-id="5a631-195">Agora que você criou um banco de dados de exemplo no Azure, usaremos a ferramenta de consulta interna no portal do Azure para confirmar que você pode conectar o banco de dados e consultar os dados.</span><span class="sxs-lookup"><span data-stu-id="5a631-195">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="5a631-196">Na página do Banco de Dados SQL do seu banco de dados, clique em **Ferramentas** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="5a631-196">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="5a631-197">A página **Ferramentas** é aberta.</span><span class="sxs-lookup"><span data-stu-id="5a631-197">The **Tools** page opens.</span></span>

   ![menu ferramentas](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="5a631-199">Clique em **Editor de consultas (visualização)**, clique na caixa de seleção **Visualizar termos** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a631-199">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="5a631-200">A página do Editor de consulta é aberta.</span><span class="sxs-lookup"><span data-stu-id="5a631-200">The Query editor page opens.</span></span>

3. <span data-ttu-id="5a631-201">Clique em **Login** e, quando receber solicitação, selecione **Autenticação do SQL Server** e forneça o logon de administrador do servidor e a senha criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5a631-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

   ![logon](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="5a631-203">Clique em **OK** para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="5a631-203">Click **OK** to log in.</span></span>

5. <span data-ttu-id="5a631-204">Depois de autenticado, digite a consulta a seguir no painel do editor de consulta.</span><span class="sxs-lookup"><span data-stu-id="5a631-204">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="5a631-205">Clique em **Executar** e reveja os resultados da consulta no painel **Resultados**.</span><span class="sxs-lookup"><span data-stu-id="5a631-205">Click **Run** and then review the query results in the **Results** pane.</span></span>

   ![resultados do editor de consultas](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="5a631-207">Feche a página **Editor de consultas** e a página **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="5a631-207">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5a631-208">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="5a631-208">Clean up resources</span></span>

<span data-ttu-id="5a631-209">Se não precisar desses recursos para outro início rápido/tutorial (consulte [Próximas etapas](#next-steps)), você pode excluí-los executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5a631-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing the following:</span></span>


1. <span data-ttu-id="5a631-210">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e clique em **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5a631-210">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="5a631-211">Em sua página de grupo de recursos, clique em **Excluir**, digite **myResourceGroup** na caixa de texto e clique **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="5a631-211">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a631-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a631-212">Next steps</span></span>

<span data-ttu-id="5a631-213">Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas.</span><span class="sxs-lookup"><span data-stu-id="5a631-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="5a631-214">Saiba mais escolhendo sua ferramenta abaixo:</span><span class="sxs-lookup"><span data-stu-id="5a631-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="5a631-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5a631-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="5a631-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5a631-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="5a631-217">.NET</span><span class="sxs-lookup"><span data-stu-id="5a631-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="5a631-218">PHP</span><span class="sxs-lookup"><span data-stu-id="5a631-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="5a631-219">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a631-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="5a631-220">Java</span><span class="sxs-lookup"><span data-stu-id="5a631-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="5a631-221">Python</span><span class="sxs-lookup"><span data-stu-id="5a631-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="5a631-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="5a631-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
