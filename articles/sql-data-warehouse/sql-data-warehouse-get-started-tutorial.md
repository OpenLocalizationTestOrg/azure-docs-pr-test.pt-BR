---
title: "SQL Data Warehouse - introdução ao tutorial | Microsoft Docs"
description: "Este tutorial ensina como provisionar e carregar dados no SQL Data Warehouse do Azure. Você também aprenderá as noções básicas sobre dimensionamento, pausa e ajuste."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 95e14824ba3b705bb909ec983652dd3305b98805
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="c3ff7-104">Introdução ao SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3ff7-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="c3ff7-105">Este tutorial mostra como provisionar e carregar dados no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c3ff7-106">Você também aprenderá as noções básicas sobre dimensionamento, pausa e ajuste.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="c3ff7-107">Quando terminar, você estará pronto para consultar e explorar seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="c3ff7-108">**Tempo estimado para conclusão:** este é um tutorial completo com código de exemplo que leva cerca de 30 minutos para concluir assim que os pré-requisitos são atendidos.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c3ff7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c3ff7-109">Prerequisites</span></span>

<span data-ttu-id="c3ff7-110">O tutorial pressupõe que você esteja familiarizado com os conceitos básicos do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="c3ff7-111">Se você precisar de uma introdução, consulte [O que é SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="c3ff7-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="c3ff7-112">Inscreva-se no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c3ff7-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="c3ff7-113">Se você ainda não tiver uma conta do Microsoft Azure, deverá inscrever-se em uma para usar este serviço.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="c3ff7-114">Se já tiver uma conta, você poderá ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="c3ff7-115">Navegue até as páginas de conta [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="c3ff7-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="c3ff7-116">Crie uma conta gratuita do Azure ou uma conta de compra.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="c3ff7-117">Siga as instruções</span><span class="sxs-lookup"><span data-stu-id="c3ff7-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="c3ff7-118">Instalar os devidos drivers e ferramentas do cliente SQL</span><span class="sxs-lookup"><span data-stu-id="c3ff7-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="c3ff7-119">A maioria das ferramentas do cliente SQL pode conectar o SQL Data Warehouse usando o JDBC, ODBC ou ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="c3ff7-120">Devido ao grande número de recursos do T-SQL que oferece suporte ao SQL Data Warehouse, alguns aplicativos cliente não são totalmente compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="c3ff7-121">Se você estiver executando um sistema operacional do Windows, recomendamos o uso do [Visual Studio] ou do [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="c3ff7-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="c3ff7-122">Criar um SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3ff7-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="c3ff7-123">Um SQL Data Warehouse é um tipo especial de banco de dados que foi projetado para o processamento extremamente paralelo.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="c3ff7-124">O banco de dados é distribuído entre vários nós e processa as consultas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="c3ff7-125">SQL Data Warehouse tem um nó de controle que coordena as atividades de todos os nós.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="c3ff7-126">Os próprios nós usam o Banco de Dados SQL para gerenciar seus dados.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="c3ff7-127">A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="c3ff7-128">Para obter mais informações, confira [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="c3ff7-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="c3ff7-129">Criar um data warehouse</span><span class="sxs-lookup"><span data-stu-id="c3ff7-129">Create a data warehouse</span></span>

1. <span data-ttu-id="c3ff7-130">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3ff7-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c3ff7-131">Clique em **Novo** > **Bancos de dados** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="c3ff7-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="c3ff7-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="c3ff7-133">Preencher os detalhes da implantação</span><span class="sxs-lookup"><span data-stu-id="c3ff7-133">Fill out deployment details</span></span>

    <span data-ttu-id="c3ff7-134">**Nome do banco de dados**: escolha qualquer item que desejar.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="c3ff7-135">Se você tiver vários data warehouses, é recomendável que os nomes incluem detalhes, como a região e o ambiente, por exemplo, *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="c3ff7-136">**Assinatura:** sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="c3ff7-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="c3ff7-137">**Grupo de Recursos**: crie um grupo de recursos ou use um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="c3ff7-138">Grupos de recursos são úteis para a administração de recursos como controle de acesso de escopo e implantação de modelo.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="c3ff7-139">Leia mais sobre grupos de recursos do Azure e as práticas recomendadas [aqui](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span><span class="sxs-lookup"><span data-stu-id="c3ff7-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="c3ff7-140">**Origem**: banco de dados em branco</span><span class="sxs-lookup"><span data-stu-id="c3ff7-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="c3ff7-141">**Servidor**: selecione o servidor que você criou em [Pré-requisitos].</span><span class="sxs-lookup"><span data-stu-id="c3ff7-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="c3ff7-142">**Agrupamento**: mantenha o agrupamento padrão SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="c3ff7-143">**Selecionar desempenho**: é recomendável iniciar com o 400DWU padrão.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="c3ff7-144">Escolha **Fixar no painel** ![Fixar no painel](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="c3ff7-144">Choose **Pin to dashboard** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="c3ff7-145">Relaxe e aguarde o data warehouse implantar!</span><span class="sxs-lookup"><span data-stu-id="c3ff7-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="c3ff7-146">É normal que esse processo leve vários minutos.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="c3ff7-147">O portal notifica você quando seu data warehouse está pronto para o uso.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="c3ff7-148">Conectar ao SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3ff7-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="c3ff7-149">Este tutorial usa o SQL Server Management Studio (SSMS) para conectar o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="c3ff7-150">Você pode conectar o SQL Data Warehouse por meio desses conectores com suporte: ADO.NET, JDBC, ODBC e PHP.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="c3ff7-151">Lembre-se, a funcionalidade pode ser limitada para as ferramentas sem suporte pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="c3ff7-152">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="c3ff7-152">Get connection information</span></span>

<span data-ttu-id="c3ff7-153">Para conectar seu data warehouse, você precisa conectar-se por meio do SQL Server lógico criado em [Pré-requisitos].</span><span class="sxs-lookup"><span data-stu-id="c3ff7-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="c3ff7-154">Selecione o data warehouse no painel ou procure-o em seus recursos.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![Painel do SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="c3ff7-156">Localize o nome completo do SQL Server lógico.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-156">Find the full name for the logical SQL server.</span></span>

    ![Selecionar o nome do servidor](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="c3ff7-158">Abra o SSMS e use o gerenciador de objetos para conectar este servidor usando as credenciais de administrador do servidor criadas em [Pré-requisitos]</span><span class="sxs-lookup"><span data-stu-id="c3ff7-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![Conectar com SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="c3ff7-160">Se tudo ocorrer corretamente, agora você deverá estar conectado ao SQL Server lógico.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="c3ff7-161">Como você conectado como o administrador do servidor, poderá conectar qualquer banco de dados hospedado pelo servidor, incluindo o banco de dados mestre.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="c3ff7-162">Há apenas uma conta do administrador do servidor e ela tem a maioria dos privilégios de qualquer usuário.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="c3ff7-163">Tenha cuidado para não permitir que muitas pessoas em sua organização saibam a senha do administrador.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="c3ff7-164">Você também pode ter uma conta do administrador do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="c3ff7-165">Não fornecemos os detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-165">We don't provide the details here.</span></span> <span data-ttu-id="c3ff7-166">Se você quiser saber mais sobre como usar a autenticação do Azure Active Directory, confira [Autenticação do Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="c3ff7-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="c3ff7-167">Em seguida, exploraremos a criação de logons e usuários adicionais.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="c3ff7-168">Criar um usuário do banco de dados</span><span class="sxs-lookup"><span data-stu-id="c3ff7-168">Create a database user</span></span>

<span data-ttu-id="c3ff7-169">Nesta etapa, você cria uma conta de usuário para acessar o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="c3ff7-170">Também mostramos como dar a esse usuário a capacidade de executar consultas com uma grande quantidade de memória e recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="c3ff7-171">Observações sobre as classes de recursos para alocar recursos para as consultas</span><span class="sxs-lookup"><span data-stu-id="c3ff7-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="c3ff7-172">Para manter seus dados seguros, não use o administrador do servidor para executar consultas em seus bancos de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="c3ff7-173">Ele tem a maioria dos privilégios de qualquer usuário e usá-lo para executar operações nos dados do usuário coloca seus dados em risco.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="c3ff7-174">Além disso, como o administrador do servidor deve realizar operações de gerenciamento, ele executa operações com apenas uma pequena alocação de memória e recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="c3ff7-175">O SQL Data Warehouse usa as funções do banco de dados predefinidas, denominadas classes de recursos, para alocar quantidades diferentes de memória, recursos de CPU e slots de simultaneidade para os usuários.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="c3ff7-176">Cada usuário pode pertencer a uma classe de recursos pequena, média, grande ou extragrande.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="c3ff7-177">Classe de recursos do usuário determina os recursos que o usuário tem para executar consultas e operações de carregamento.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="c3ff7-178">Para otimizar a compactação de dados, o usuário talvez precise usar alocações de recursos grandes ou extragrandes.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="c3ff7-179">Leia mais sobre classes de recursos [aqui](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="c3ff7-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="c3ff7-180">Criar uma conta que pode controlar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="c3ff7-180">Create an account that can control a database</span></span>

<span data-ttu-id="c3ff7-181">Como você está atualmente conectado como o administrador do servidor, tem permissões para criar logons e usuários.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="c3ff7-182">Usando o SSMS ou outro cliente de consulta, abra uma nova consulta para o **mestre**.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nova consulta no mestre](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nova consulta em Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="c3ff7-185">Na janela de consulta, execute este comando T-SQL para criar um logon denominado MedRCLogin e um usuário denominado LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="c3ff7-186">Este logon pode conectar o SQL Server lógico.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="c3ff7-187">Agora, consulte o *banco de dados do SQL Data Warehouse*, crie um usuário do banco de dados com base no logon criado para acessar e executar operações no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="c3ff7-188">Dê ao usuário do banco de dados permissões de controle para o banco de dados denominado NYT.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="c3ff7-189">Se o nome do banco de dados contiver hifens, coloque-o entre colchetes!</span><span class="sxs-lookup"><span data-stu-id="c3ff7-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="c3ff7-190">Conceda ao usuário as alocações de recursos de mídia</span><span class="sxs-lookup"><span data-stu-id="c3ff7-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="c3ff7-191">Execute este comando T-SQL para torná-lo um membro da classe de recursos medium, que é denominada mediumrc.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="c3ff7-192">Clique [aqui](sql-data-warehouse-develop-concurrency.md#resource-classes) para saber mais sobre simultaneidade e classes de recurso!</span><span class="sxs-lookup"><span data-stu-id="c3ff7-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="c3ff7-193">Conectar o servidor lógico com as novas credenciais</span><span class="sxs-lookup"><span data-stu-id="c3ff7-193">Connect to the logical server with the new credentials</span></span>

    ![Fazer logon com o novo logon](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="c3ff7-195">Carregar dados do armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="c3ff7-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="c3ff7-196">Agora, você está pronto para carregar dados em seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="c3ff7-197">Esta etapa mostra como carregar dados do táxi de Nova Iorque em um blob de armazenamento do Azure público.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="c3ff7-198">Uma maneira comum de carregar dados no SQL Data Warehouse é primeiro mover os dados para o armazenamento de blobs do Azure, em seguida, carregá-los em seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="c3ff7-199">Para facilitar entender como carregar, temos dados do táxi de Nova Iorque já hospedados em um blob de armazenamento do Azure público.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="c3ff7-200">Para uma referência futura, para saber como obter os dados para o armazenamento de blobs do Azure ou carregá-los diretamente do seu código-fonte no SQL Data Warehouse, consulte a [visão geral do carregamento](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="c3ff7-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="c3ff7-201">Definir dados externos</span><span class="sxs-lookup"><span data-stu-id="c3ff7-201">Define external data</span></span>

1. <span data-ttu-id="c3ff7-202">Crie uma chave mestra.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-202">Create a master key.</span></span> <span data-ttu-id="c3ff7-203">Você só precisa criar uma chave mestra uma vez por banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="c3ff7-204">Defina o local do blob do Azure que contém os dados do táxi.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="c3ff7-205">Definir os formatos de arquivo externos</span><span class="sxs-lookup"><span data-stu-id="c3ff7-205">Define the external file formats</span></span>

    <span data-ttu-id="c3ff7-206">O comando ```CREATE EXTERNAL FILE FORMAT``` é usado para especificar o formato dos arquivos que contêm os dados externos.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="c3ff7-207">Eles contêm texto separado por um ou mais caracteres denominados delimitadores.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="c3ff7-208">Para demonstrar, os dados do táxi são armazenados como dados descompactados e dados compactados em gzip.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="c3ff7-209">Execute estes comandos T-SQL para definir dois formatos diferentes: descompactado e compactado.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="c3ff7-210">Crie um esquema para o formato de arquivo externo.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="c3ff7-211">Crie as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-211">Create the external tables.</span></span> <span data-ttu-id="c3ff7-212">Essas tabelas fazem referência aos dados colocados no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="c3ff7-213">Execute os seguintes comandos T-SQL para criar várias tabelas externas que apontam para o blob do Azure definido anteriormente na nossa fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="c3ff7-214">Importe os dados do Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="c3ff7-215">O SQL Data Warehouse oferece suporte a uma instrução de chave chamada CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="c3ff7-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="c3ff7-216">Essa instrução cria uma nova tabela com base nos resultados de uma instrução select.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="c3ff7-217">A nova tabela tem as mesmas colunas e tipos de dados que os resultados da instrução select.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="c3ff7-218">Essa é uma forma elegante de importar dados do Armazenamento de Blobs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="c3ff7-219">Execute este script para importar seus dados.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-219">Run this script to import your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="c3ff7-220">Exiba os dados enquanto eles são carregados.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-220">View your data as it loads.</span></span>

   <span data-ttu-id="c3ff7-221">Você está carregando vários GBs de dados e compactando-os em índices columnstore de cluster de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="c3ff7-222">Execute a consulta a seguir que usa DMVs (exibições de gerenciamento dinâmico) para mostrar o status do carregamento.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="c3ff7-223">Após iniciar a consulta, pegue um café e alguns biscoitos enquanto o SQL Data Warehouse faz o trabalho pesado.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="c3ff7-224">Exiba todas as consultas do sistema.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="c3ff7-225">Veja os dados carregados sem problemas no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Ver dados carregados](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="c3ff7-227">Melhorar o desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="c3ff7-227">Improve query performance</span></span>

<span data-ttu-id="c3ff7-228">Há várias maneiras de melhorar o desempenho da consulta e atingir o desempenho de alta velocidade que o SQL Data Warehouse foi projetado para fornecer.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="c3ff7-229">Ver o efeito do dimensionamento no desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="c3ff7-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="c3ff7-230">Uma maneira de melhorar o desempenho da consulta é dimensionar os recursos alterando o nível de serviço do DWU para o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="c3ff7-231">Cada nível de serviço custa mais, mas você pode reduzir ou pausar recursos a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="c3ff7-232">Nesta etapa, você compara o desempenho em suas configurações diferentes de DWU.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="c3ff7-233">Primeiro, vamos reduzir para 100 DWUs para lhe dar uma ideia de como a computação como um nó pode ser executada por conta própria.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="c3ff7-234">Acesse o portal e selecione a instância do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="c3ff7-235">Selecione dimensionar na folha SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![Dimensionar DW no portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="c3ff7-237">Reduza a barra de desempenho para 100 DWU e clique em Salvar.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![Dimensionar e salvar](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="c3ff7-239">Aguarde a conclusão da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3ff7-240">Não é possível executar consultas ao alterar a escala.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="c3ff7-241">O dimensionamento **elimina** suas consultas em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="c3ff7-242">Você poderá reiniciá-las quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="c3ff7-243">Faça uma operação de verificação nos dados de viagem, selecionando os milhões de entradas principais para todas as colunas.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="c3ff7-244">Se está ansioso para continuar rapidamente, fique à vontade para selecionar menos linhas.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="c3ff7-245">Anote o tempo necessário para executar esta operação.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="c3ff7-246">Dimensione seu data warehouse de volta para 400 DWUs.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="c3ff7-247">Lembre-se de que cada 100 DWU adicionam outro nó de computação ao Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="c3ff7-248">Execute a consulta novamente!</span><span class="sxs-lookup"><span data-stu-id="c3ff7-248">Run the query again!</span></span> <span data-ttu-id="c3ff7-249">Você deve notar uma diferença significativa.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c3ff7-250">Como a consulta retorna muitos dados, a disponibilidade de largura de banda do computador executando o SSMS pode ser um afunilamento de desempenho.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-250">Because the query returns a lot of data, the bandwidth availability of the machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="c3ff7-251">Isso pode resultar em nenhuma melhoria de desempenho!</span><span class="sxs-lookup"><span data-stu-id="c3ff7-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="c3ff7-252">Como o SQL Data Warehouse usa processamento paralelo massivo.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="c3ff7-253">As consultas que examinam ou executam funções de análise em milhões de linhas experimentam o verdadeira poder do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-253">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="c3ff7-254">Ver o efeito da estatísticas no desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="c3ff7-254">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="c3ff7-255">Executar uma consulta que une a tabela de Datas à tabela de Viagens</span><span class="sxs-lookup"><span data-stu-id="c3ff7-255">Run a query that joins the Date table with the Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="c3ff7-256">Essa consulta demora um pouco porque o SQL Data Warehouse precisa movimentar os dados de forma aleatória antes de executar a junção.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-256">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="c3ff7-257">As junções não precisam movimentar os dados de forma aleatória se eles forem criados para juntar dados da mesma forma que foram distribuídos.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-257">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="c3ff7-258">Esse é um assunto mais profundo.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="c3ff7-259">Estatísticas fazem a diferença.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="c3ff7-260">Execute esta instrução para criar estatísticas em colunas de junção.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-260">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="c3ff7-261">O SQL DW não gerencia automaticamente as estatísticas para você.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="c3ff7-262">As estatísticas são importantes para o desempenho da consulta, e é altamente recomendável criar e atualizar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="c3ff7-263">**Você obterá mais benefícios se tiver estatísticas em colunas envolvidas em junções, colunas usadas na cláusula WHERE e colunas encontradas em GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="c3ff7-263">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="c3ff7-264">Execute novamente a consulta de Pré-requisitos e observe as diferenças de desempenho.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-264">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="c3ff7-265">Embora as diferenças no desempenho da consulta não sejam tão drásticas quanto o aumento, você deve observar uma aceleração.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-265">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3ff7-266">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3ff7-266">Next steps</span></span>

<span data-ttu-id="c3ff7-267">Agora você está pronto para consultar e explorar.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-267">You're now ready to query and explore.</span></span> <span data-ttu-id="c3ff7-268">Confira nossas melhores práticas recomendadas ou dicas.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="c3ff7-269">Se tiver terminado de explorar por hoje, pause a instância!</span><span class="sxs-lookup"><span data-stu-id="c3ff7-269">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="c3ff7-270">Em produção, você pode obter uma enorme economia pausando e dimensionando para atender às suas necessidades de negócios.</span><span class="sxs-lookup"><span data-stu-id="c3ff7-270">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![Pausar](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="c3ff7-272">Leituras úteis</span><span class="sxs-lookup"><span data-stu-id="c3ff7-272">Useful readings</span></span>

<span data-ttu-id="c3ff7-273">[Gerenciamento de simultaneidade e carga de trabalho][]</span><span class="sxs-lookup"><span data-stu-id="c3ff7-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="c3ff7-274">[Práticas recomendadas para o Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="c3ff7-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="c3ff7-275">[Consultar monitoramento][]</span><span class="sxs-lookup"><span data-stu-id="c3ff7-275">[Query Monitoring][]</span></span>

<span data-ttu-id="c3ff7-276">[Dez principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala][]</span><span class="sxs-lookup"><span data-stu-id="c3ff7-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="c3ff7-277">[Migrando dados para o Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="c3ff7-277">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[Gerenciamento de simultaneidade e carga de trabalho]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Práticas recomendadas para o Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Consultar monitoramento]: sql-data-warehouse-manage-monitor.md
[Dez principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migrando dados para o Azure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[Pré-requisitos]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
