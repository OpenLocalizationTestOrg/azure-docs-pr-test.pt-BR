---
title: "aaaAzure SQL Data Warehouse - Introdução tutorial | Microsoft Docs"
description: "Este tutorial ensina como tooprovision e carregar dados no Azure SQL Data Warehouse. Você também aprenderá noções básicas de saudação sobre dimensionamento, pausa e ajuste."
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
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="e05ac-104">Introdução ao SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e05ac-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="e05ac-105">Este tutorial mostra como tooprovision e carregar dados no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e05ac-106">Você também aprenderá noções básicas de saudação sobre dimensionamento, pausa e ajuste.</span><span class="sxs-lookup"><span data-stu-id="e05ac-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="e05ac-107">Quando você terminar, você usará tooquery pronto e explorar seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="e05ac-108">**Estimado tempo toocomplete:** este é um tutorial de ponta a ponta com o código de exemplo que usa toocomplete cerca de 30 minutos depois que você atingiu os pré-requisitos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e05ac-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e05ac-109">Prerequisites</span></span>

<span data-ttu-id="e05ac-110">tutorial de saudação pressupõe que você esteja familiarizado com os conceitos básicos do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="e05ac-111">Se você precisar de uma introdução, consulte [O que é SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="e05ac-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="e05ac-112">Inscreva-se no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e05ac-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="e05ac-113">Se você ainda não tiver uma conta do Microsoft Azure, você precisa toosign para um toouse desse serviço.</span><span class="sxs-lookup"><span data-stu-id="e05ac-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="e05ac-114">Se já tiver uma conta, você poderá ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="e05ac-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="e05ac-115">Navegar pelas páginas de conta toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="e05ac-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="e05ac-116">Crie uma conta gratuita do Azure ou uma conta de compra.</span><span class="sxs-lookup"><span data-stu-id="e05ac-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="e05ac-117">Siga as instruções de saudação</span><span class="sxs-lookup"><span data-stu-id="e05ac-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="e05ac-118">Instalar os devidos drivers e ferramentas do cliente SQL</span><span class="sxs-lookup"><span data-stu-id="e05ac-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="e05ac-119">A maioria das ferramentas de cliente SQL pode se conectar a tooSQL Data Warehouse usando JDBC, ODBC ou ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="e05ac-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="e05ac-120">Devido a toohello grande número de recursos de T-SQL que oferece suporte a SQL Data Warehouse, alguns aplicativos cliente não são totalmente compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="e05ac-121">Se você estiver executando um sistema operacional do Windows, recomendamos o uso do [Visual Studio] ou do [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="e05ac-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="e05ac-122">Criar um SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e05ac-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="e05ac-123">Um SQL Data Warehouse é um tipo especial de banco de dados que foi projetado para o processamento extremamente paralelo.</span><span class="sxs-lookup"><span data-stu-id="e05ac-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="e05ac-124">banco de dados de saudação é distribuído em vários nós e processa consultas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="e05ac-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="e05ac-125">SQL Data Warehouse tem um nó de controle que orquestra as atividades de saudação de todos os nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="e05ac-126">nós Olá se usam toomanage de banco de dados SQL seus dados.</span><span class="sxs-lookup"><span data-stu-id="e05ac-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="e05ac-127">A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="e05ac-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="e05ac-128">Para obter mais informações, confira [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="e05ac-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="e05ac-129">Criar um data warehouse</span><span class="sxs-lookup"><span data-stu-id="e05ac-129">Create a data warehouse</span></span>

1. <span data-ttu-id="e05ac-130">O logon no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e05ac-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e05ac-131">Clique em **Novo** > **Bancos de dados** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="e05ac-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="e05ac-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="e05ac-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="e05ac-133">Preencher os detalhes da implantação</span><span class="sxs-lookup"><span data-stu-id="e05ac-133">Fill out deployment details</span></span>

    <span data-ttu-id="e05ac-134">**Nome do banco de dados**: escolha qualquer item que desejar.</span><span class="sxs-lookup"><span data-stu-id="e05ac-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="e05ac-135">Se você tiver vários depósitos de dados, é recomendável que os nomes de incluem detalhes como região hello, ambiente, por exemplo *westus mydw-teste 1*.</span><span class="sxs-lookup"><span data-stu-id="e05ac-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="e05ac-136">**Assinatura:** sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="e05ac-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="e05ac-137">**Grupo de Recursos**: crie um grupo de recursos ou use um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="e05ac-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e05ac-138">Grupos de recursos são úteis para a administração de recursos como controle de acesso de escopo e implantação de modelo.</span><span class="sxs-lookup"><span data-stu-id="e05ac-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="e05ac-139">Leia mais sobre grupos de recursos do Azure e as práticas recomendadas [aqui](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span><span class="sxs-lookup"><span data-stu-id="e05ac-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="e05ac-140">**Origem**: banco de dados em branco</span><span class="sxs-lookup"><span data-stu-id="e05ac-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="e05ac-141">**Servidor**: servidor de saudação selecione que você criou na [pré-requisitos].</span><span class="sxs-lookup"><span data-stu-id="e05ac-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="e05ac-142">**Agrupamento**: deixe o agrupamento padrão de saudação SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="e05ac-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="e05ac-143">**Selecione desempenho**: É recomendável começar com 400DWU de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e05ac-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="e05ac-144">Escolha **Pin toodashboard** ![tooDashboard de Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="e05ac-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="e05ac-145">Aguarde e aguarde até que seu toodeploy de depósito de dados!</span><span class="sxs-lookup"><span data-stu-id="e05ac-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="e05ac-146">É normal para este processo tootake vários minutos.</span><span class="sxs-lookup"><span data-stu-id="e05ac-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="e05ac-147">portal de saudação notifica quando o data warehouse é toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="e05ac-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="e05ac-148">Conecte-se tooSQL do Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e05ac-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="e05ac-149">Este tutorial usa tooconnect toohello data warehouse de SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e05ac-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="e05ac-150">Você pode se conectar tooSQL Data Warehouse por esses conectores com suporte: ADO.NET, JDBC, ODBC e PHP.</span><span class="sxs-lookup"><span data-stu-id="e05ac-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="e05ac-151">Lembre-se, a funcionalidade pode ser limitada para as ferramentas sem suporte pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e05ac-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="e05ac-152">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="e05ac-152">Get connection information</span></span>

<span data-ttu-id="e05ac-153">data warehouse de tooconnect tooyour, você precisa tooconnect por meio de saudação lógico do SQL server criado na [pré-requisitos].</span><span class="sxs-lookup"><span data-stu-id="e05ac-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="e05ac-154">Selecione o data warehouse no painel de saudação ou procure-a em seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e05ac-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Painel do SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="e05ac-156">Localize o nome completo Olá Olá lógico do SQL server.</span><span class="sxs-lookup"><span data-stu-id="e05ac-156">Find hello full name for hello logical SQL server.</span></span>

    ![Selecionar o nome do servidor](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="e05ac-158">Abra o SSMS e usar o objeto explorer tooconnect toothis server usando credenciais de administrador de servidor de saudação criado no [pré-requisitos]</span><span class="sxs-lookup"><span data-stu-id="e05ac-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Conectar com SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="e05ac-160">Se tudo correr corretamente, você deve agora ser tooyour conectado lógica SQL server.</span><span class="sxs-lookup"><span data-stu-id="e05ac-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="e05ac-161">Desde que você fez logon como Olá administrador do servidor, você pode se conectar a banco de dados de tooany hospedado pelo servidor de saudação, inclusive o banco de dados mestre hello.</span><span class="sxs-lookup"><span data-stu-id="e05ac-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="e05ac-162">Há apenas um servidor conta de administrador e tem Olá a maioria dos privilégios de qualquer usuário.</span><span class="sxs-lookup"><span data-stu-id="e05ac-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="e05ac-163">Tenha cuidado não tooallow muitas pessoas em sua senha de administrador organização tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="e05ac-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="e05ac-164">Você também pode ter uma conta do administrador do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e05ac-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="e05ac-165">Não fornecemos detalhes Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="e05ac-165">We don't provide hello details here.</span></span> <span data-ttu-id="e05ac-166">Se você quiser toolearn mais sobre como usar a autenticação do Active Directory do Azure, consulte [autenticação do Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="e05ac-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="e05ac-167">Em seguida, exploraremos a criação de logons e usuários adicionais.</span><span class="sxs-lookup"><span data-stu-id="e05ac-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="e05ac-168">Criar um usuário do banco de dados</span><span class="sxs-lookup"><span data-stu-id="e05ac-168">Create a database user</span></span>

<span data-ttu-id="e05ac-169">Nesta etapa, você criará um tooaccess de conta de usuário o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="e05ac-170">Também mostramos como toogive que toorun de capacidade de saudação do usuário consultas com uma grande quantidade de memória e recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="e05ac-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="e05ac-171">Observações sobre classes de recursos para alocar recursos tooqueries</span><span class="sxs-lookup"><span data-stu-id="e05ac-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="e05ac-172">tookeep seus dados seguros, não use consultas de toorun de administração de servidor de saudação em seus bancos de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="e05ac-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="e05ac-173">Ele tem Olá a maioria dos privilégios de qualquer usuário e usá-lo tooperform operações nos dados de usuário coloca seus dados em risco.</span><span class="sxs-lookup"><span data-stu-id="e05ac-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="e05ac-174">Além disso, desde que o administrador do servidor de saudação deve tooperform operações de gerenciamento, ele é executado operações com apenas uma pequena alocação de memória e recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="e05ac-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="e05ac-175">SQL Data Warehouse usa funções de banco de dados predefinido, chamado de classes de recursos, tooallocate diferentes quantidades de memória, os recursos de CPU e toousers de slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="e05ac-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="e05ac-176">Cada usuário pode pertencer a classe de recurso de pequeno, médio, grande ou extra grande tooa.</span><span class="sxs-lookup"><span data-stu-id="e05ac-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="e05ac-177">Olá classe de recurso do usuário determina Olá recursos Olá usuário tem toorun consultas e operações de carregamento.</span><span class="sxs-lookup"><span data-stu-id="e05ac-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="e05ac-178">Para a compactação de dados ideal, Olá talvez ele tenha tooload com grande ou extra grande alocações.</span><span class="sxs-lookup"><span data-stu-id="e05ac-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="e05ac-179">Leia mais sobre classes de recursos [aqui](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="e05ac-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="e05ac-180">Criar uma conta que pode controlar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="e05ac-180">Create an account that can control a database</span></span>

<span data-ttu-id="e05ac-181">Como você está conectado no Olá administrador do servidor, você tem permissões toocreate logons e usuários.</span><span class="sxs-lookup"><span data-stu-id="e05ac-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="e05ac-182">Usando o SSMS ou outro cliente de consulta, abra uma nova consulta para o **mestre**.</span><span class="sxs-lookup"><span data-stu-id="e05ac-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nova consulta no mestre](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nova consulta em Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="e05ac-185">Na janela de consulta hello, execute este toocreate de comando T-SQL um logon denominado MedRCLogin e um usuário chamado LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="e05ac-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="e05ac-186">Este logon pode se conectar a toohello lógica SQL server.</span><span class="sxs-lookup"><span data-stu-id="e05ac-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="e05ac-187">Consultar agora Olá *banco de dados do SQL Data Warehouse*, crie um usuário de banco de dados com base em Olá logon criado tooaccess e executar operações no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="e05ac-188">Atribuir Olá banco de dados usuário controle permissões toohello banco de dados chamado NYT.</span><span class="sxs-lookup"><span data-stu-id="e05ac-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="e05ac-189">Se o nome do banco de dados contiver hifens, ser toowrap-se de que ele entre colchetes!</span><span class="sxs-lookup"><span data-stu-id="e05ac-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="e05ac-190">Dê Olá usuário médio alocações</span><span class="sxs-lookup"><span data-stu-id="e05ac-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="e05ac-191">Execute este toomake de comando T-SQL it um membro da classe de recurso médios hello, que é chamado mediumrc.</span><span class="sxs-lookup"><span data-stu-id="e05ac-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="e05ac-192">Clique em [aqui](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn mais sobre classes de simultaneidade e recursos!</span><span class="sxs-lookup"><span data-stu-id="e05ac-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="e05ac-193">Conecte-se o servidor lógico toohello com as novas credenciais Olá</span><span class="sxs-lookup"><span data-stu-id="e05ac-193">Connect toohello logical server with hello new credentials</span></span>

    ![Fazer logon com o novo logon](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="e05ac-195">Carregar dados do armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="e05ac-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="e05ac-196">Agora você está dados tooload pronto para o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="e05ac-197">Esta etapa mostra como dados de cab do tooload cidade de Nova York táxi de um armazenamento do Azure público de blob.</span><span class="sxs-lookup"><span data-stu-id="e05ac-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="e05ac-198">Uma maneira comum de dados tooload no SQL Data Warehouse são toofirst mover o armazenamento de blob Olá dados tooAzure e, em seguida, carregá-lo em seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="e05ac-199">toomake-lo mais fácil toounderstand como tooload, temos Nova York táxi cab dados já está hospedados em um blob de armazenamento do Azure públicos.</span><span class="sxs-lookup"><span data-stu-id="e05ac-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="e05ac-200">Para referência futura, toolearn como tooget tooAzure seus dados de blob de armazenamento ou tooload-lo diretamente da fonte no SQL Data Warehouse, consulte Olá [visão geral de carregamento](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="e05ac-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="e05ac-201">Definir dados externos</span><span class="sxs-lookup"><span data-stu-id="e05ac-201">Define external data</span></span>

1. <span data-ttu-id="e05ac-202">Crie uma chave mestra.</span><span class="sxs-lookup"><span data-stu-id="e05ac-202">Create a master key.</span></span> <span data-ttu-id="e05ac-203">Você só precisa toocreate uma chave mestra de uma vez por banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e05ac-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="e05ac-204">Defina o local de saudação do hello BLOBs do Azure que contém dados de cab táxi Olá.</span><span class="sxs-lookup"><span data-stu-id="e05ac-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="e05ac-205">Definir Olá formatos de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="e05ac-205">Define hello external file formats</span></span>

    <span data-ttu-id="e05ac-206">Olá ```CREATE EXTERNAL FILE FORMAT``` comando é toospecify usado o formato de arquivos que contêm dados externos hello.</span><span class="sxs-lookup"><span data-stu-id="e05ac-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="e05ac-207">Eles contêm texto separado por um ou mais caracteres denominados delimitadores.</span><span class="sxs-lookup"><span data-stu-id="e05ac-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="e05ac-208">Para fins de demonstração, os dados de cab do táxi de saudação são armazenados como dados não compactados e dados gzip compactado.</span><span class="sxs-lookup"><span data-stu-id="e05ac-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="e05ac-209">Execute esses comandos do T-SQL toodefine dois formatos diferentes: descompactado e compactado.</span><span class="sxs-lookup"><span data-stu-id="e05ac-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

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

4.  <span data-ttu-id="e05ac-210">Crie um esquema para o formato de arquivo externo.</span><span class="sxs-lookup"><span data-stu-id="e05ac-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="e05ac-211">Crie hello tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="e05ac-211">Create hello external tables.</span></span> <span data-ttu-id="e05ac-212">Essas tabelas fazem referência aos dados colocados no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e05ac-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="e05ac-213">Execute Olá toocreate de comandos T-SQL a seguir várias tabelas externas que toohello de ponto de todos os BLOBs do Azure definimos anteriormente na nossa fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="e05ac-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

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

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="e05ac-214">Importar dados de saudação do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e05ac-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="e05ac-215">O SQL Data Warehouse oferece suporte a uma instrução de chave chamada CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="e05ac-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="e05ac-216">Essa instrução cria uma nova tabela com base nos resultados de saudação de uma instrução select.</span><span class="sxs-lookup"><span data-stu-id="e05ac-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="e05ac-217">Olá nova tabela tem Olá mesmos colunas e tipos de dados, como a instrução select de resultados de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="e05ac-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="e05ac-218">Isso é um tooimport de maneira elegante de dados do armazenamento de BLOBs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="e05ac-219">Execute este script tooimport seus dados.</span><span class="sxs-lookup"><span data-stu-id="e05ac-219">Run this script tooimport your data.</span></span>

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

2. <span data-ttu-id="e05ac-220">Exiba os dados enquanto eles são carregados.</span><span class="sxs-lookup"><span data-stu-id="e05ac-220">View your data as it loads.</span></span>

   <span data-ttu-id="e05ac-221">Você está carregando vários GBs de dados e compactando-os em índices columnstore de cluster de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="e05ac-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="e05ac-222">Execute Olá consulta a seguir que usa um status de saudação do gerenciamento dinâmico DMVs (exibições) tooshow de carga hello.</span><span class="sxs-lookup"><span data-stu-id="e05ac-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="e05ac-223">Depois de iniciar a consulta hello, pegue um café e um lanche enquanto SQL Data Warehouse faz algum trabalho pesado.</span><span class="sxs-lookup"><span data-stu-id="e05ac-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
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

3. <span data-ttu-id="e05ac-224">Exiba todas as consultas do sistema.</span><span class="sxs-lookup"><span data-stu-id="e05ac-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="e05ac-225">Veja os dados carregados sem problemas no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Ver dados carregados](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="e05ac-227">Melhorar o desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="e05ac-227">Improve query performance</span></span>

<span data-ttu-id="e05ac-228">Há vários modos tooimprove consulta de desempenho e tooachieve Olá alta velocidade que o SQL Data Warehouse é projetada tooprovide.</span><span class="sxs-lookup"><span data-stu-id="e05ac-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="e05ac-229">Consulte o efeito de saudação do dimensionamento de desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="e05ac-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="e05ac-230">Desempenho de consulta de uma maneira tooimprove é tooscale recursos alterando o nível de serviço DWU Olá para o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="e05ac-231">Cada nível de serviço custa mais, mas você pode reduzir ou pausar recursos a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e05ac-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="e05ac-232">Nesta etapa, você compara o desempenho em suas configurações diferentes de DWU.</span><span class="sxs-lookup"><span data-stu-id="e05ac-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="e05ac-233">Primeiro, vamos dimensionar dimensionamento Olá para baixo too100 DWU para obter uma ideia de como um nó de computação pode executar por conta própria.</span><span class="sxs-lookup"><span data-stu-id="e05ac-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="e05ac-234">Vá toohello portal e selecione seu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="e05ac-235">Selecione escala na folha do hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Dimensionar DW no portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="e05ac-237">Reduzir o desempenho de saudação barra too100 DWU e clique em Salvar.</span><span class="sxs-lookup"><span data-stu-id="e05ac-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Dimensionar e salvar](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="e05ac-239">Aguarde o toofinish de operação de escala.</span><span class="sxs-lookup"><span data-stu-id="e05ac-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e05ac-240">Não é possível executar consultas ao alterar a escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="e05ac-241">O dimensionamento **elimina** suas consultas em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="e05ac-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="e05ac-242">Você pode reiniciá-los quando Olá operação é concluída.</span><span class="sxs-lookup"><span data-stu-id="e05ac-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="e05ac-243">Faça uma operação de verificação nos dados de viagem hello, selecionando Olá entradas principais de milhões para todas as colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="e05ac-244">Se você está adiantado toomove rapidamente, sinta-se livre tooselect menos linhas.</span><span class="sxs-lookup"><span data-stu-id="e05ac-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="e05ac-245">Anote Olá tempo toorun esta operação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="e05ac-246">Dimensionar seu data warehouse too400 DWU de volta.</span><span class="sxs-lookup"><span data-stu-id="e05ac-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="e05ac-247">Lembre-se de que cada DWU 100 é adicionar outra tooyour de nó de computação do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="e05ac-248">Execute novamente a consulta de Olá!</span><span class="sxs-lookup"><span data-stu-id="e05ac-248">Run hello query again!</span></span> <span data-ttu-id="e05ac-249">Você deve notar uma diferença significativa.</span><span class="sxs-lookup"><span data-stu-id="e05ac-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e05ac-250">Como consulta Olá retorna muitos dados, a disponibilidade de largura de banda de saudação da máquina Olá executando o SSMS pode ser um afunilamento de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e05ac-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="e05ac-251">Isso pode resultar em nenhuma melhoria de desempenho!</span><span class="sxs-lookup"><span data-stu-id="e05ac-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="e05ac-252">Como o SQL Data Warehouse usa processamento paralelo massivo.</span><span class="sxs-lookup"><span data-stu-id="e05ac-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="e05ac-253">As consultas que digitalizar ou executam funções analíticas em milhões de linhas sofrer verdadeiro poder saudação do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e05ac-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="e05ac-254">Ver o efeito de saudação de estatísticas sobre o desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="e05ac-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="e05ac-255">Executar uma consulta de junções Olá tabela de data por viagem Olá</span><span class="sxs-lookup"><span data-stu-id="e05ac-255">Run a query that joins hello Date table with hello Trip table</span></span>

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

    <span data-ttu-id="e05ac-256">Essa consulta demorada porque o SQL Data Warehouse tem dados tooshuffle antes de executar associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e05ac-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="e05ac-257">Junções não têm dados tooshuffle se forem dados toojoin projetado Olá mesma forma que ele seja distribuído.</span><span class="sxs-lookup"><span data-stu-id="e05ac-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="e05ac-258">Esse é um assunto mais profundo.</span><span class="sxs-lookup"><span data-stu-id="e05ac-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="e05ac-259">Estatísticas fazem a diferença.</span><span class="sxs-lookup"><span data-stu-id="e05ac-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="e05ac-260">Execute essa instrução de estatísticas de toocreate em colunas de junção hello.</span><span class="sxs-lookup"><span data-stu-id="e05ac-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="e05ac-261">O SQL DW não gerencia automaticamente as estatísticas para você.</span><span class="sxs-lookup"><span data-stu-id="e05ac-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="e05ac-262">As estatísticas são importantes para o desempenho da consulta, e é altamente recomendável criar e atualizar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="e05ac-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="e05ac-263">**Você obtém maior benefício Olá fazendo com que as estatísticas em colunas envolvidas em relações, colunas usadas em Olá onde cláusula e colunas encontrado no GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="e05ac-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="e05ac-264">Execute a consulta de saudação de pré-requisitos novamente e observar as diferenças de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e05ac-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="e05ac-265">Enquanto não será drásticas quanto o dimensionamento das diferenças de saudação de desempenho de consulta, você deve observar uma velocidade.</span><span class="sxs-lookup"><span data-stu-id="e05ac-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e05ac-266">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e05ac-266">Next steps</span></span>

<span data-ttu-id="e05ac-267">Você agora está pronto tooquery e explora.</span><span class="sxs-lookup"><span data-stu-id="e05ac-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="e05ac-268">Confira nossas melhores práticas recomendadas ou dicas.</span><span class="sxs-lookup"><span data-stu-id="e05ac-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="e05ac-269">Se você está explorando por dia hello, torne toopause-se de que sua instância!</span><span class="sxs-lookup"><span data-stu-id="e05ac-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="e05ac-270">Em produção, você pode experimentar grande economia, pausa e dimensionamento toomeet suas necessidades de negócios.</span><span class="sxs-lookup"><span data-stu-id="e05ac-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Pausar](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="e05ac-272">Leituras úteis</span><span class="sxs-lookup"><span data-stu-id="e05ac-272">Useful readings</span></span>

<span data-ttu-id="e05ac-273">[Gerenciamento de simultaneidade e carga de trabalho][]</span><span class="sxs-lookup"><span data-stu-id="e05ac-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="e05ac-274">[Práticas recomendadas para o Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="e05ac-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="e05ac-275">[Consultar monitoramento][]</span><span class="sxs-lookup"><span data-stu-id="e05ac-275">[Query Monitoring][]</span></span>

<span data-ttu-id="e05ac-276">[Dez principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala][]</span><span class="sxs-lookup"><span data-stu-id="e05ac-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="e05ac-277">[Migrando dados tooAzure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="e05ac-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Gerenciamento de simultaneidade e carga de trabalho]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Práticas recomendadas para o Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Consultar monitoramento]: sql-data-warehouse-manage-monitor.md
[Dez principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migrando dados tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[pré-requisitos]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
