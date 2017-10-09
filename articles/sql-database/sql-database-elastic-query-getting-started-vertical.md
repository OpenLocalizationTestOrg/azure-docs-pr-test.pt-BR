---
title: aaaGet iniciado com consultas de bancos de dados (particionamento vertical) | Microsoft Docs
description: "como a consulta de banco de dados Elástico toouse com particionado verticalmente bancos de dados"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="e3515-103">Introdução às consultas entre bancos de dados (particionamento vertical) (preview)</span><span class="sxs-lookup"><span data-stu-id="e3515-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="e3515-104">Consulta de banco de dados Elástico (visualização) para o banco de dados SQL permite consultas do T-SQL toorun que abrangem vários bancos de dados usando um ponto de conexão única.</span><span class="sxs-lookup"><span data-stu-id="e3515-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="e3515-105">Este tópico aplica-se muito[particionado verticalmente bancos de dados](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="e3515-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="e3515-106">Quando concluído, você verá: Saiba como tooconfigure e usar um banco de dados do Azure SQL tooperform as consultas que abrangem vários bancos de dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="e3515-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="e3515-107">Para obter mais informações sobre o recurso de consulta de banco de dados Elástico hello, consulte [visão geral de consulta de banco de dados Elástico de banco de dados do Azure SQL](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3515-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e3515-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3515-108">Prerequisites</span></span>

<span data-ttu-id="e3515-109">Você deve ter a permissão para ALTERAR QUALQUER FONTE DE DADOS EXTERNA.</span><span class="sxs-lookup"><span data-stu-id="e3515-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="e3515-110">Essa permissão é incluída com a permissão ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="e3515-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="e3515-111">Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e3515-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="e3515-112">Criar hello bancos de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="e3515-112">Create hello sample databases</span></span>
<span data-ttu-id="e3515-113">toostart com, precisamos de dois bancos de dados de toocreate, **clientes** e **pedidos**, em Olá mesmos ou em diferentes servidores lógicos.</span><span class="sxs-lookup"><span data-stu-id="e3515-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="e3515-114">Executar Olá consultas a seguir no hello **pedidos** saudação do banco de dados toocreate **OrderInformation** tabela e a entrada de dados de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e3515-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="e3515-115">Agora, execute seguinte consulta no hello **clientes** saudação do banco de dados toocreate **CustomerInformation** tabela e a entrada de dados de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e3515-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="e3515-116">Criar objetos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3515-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="e3515-117">Chave mestra e credenciais do escopo do banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3515-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="e3515-118">Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3515-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="e3515-119">Conecte-se o banco de dados de pedidos de toohello e execute Olá comandos T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3515-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="e3515-120">Olá "username" e "password" devem ser Olá nome de usuário e senha usada toologin no banco de dados de clientes hello.</span><span class="sxs-lookup"><span data-stu-id="e3515-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="e3515-121">Atualmente não há suporte para a autenticação usando o Azure Active Directory com consultas elásticas.</span><span class="sxs-lookup"><span data-stu-id="e3515-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="e3515-122">Fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="e3515-122">External data sources</span></span>
<span data-ttu-id="e3515-123">toocreate uma fonte de dados externa, execute Olá comando a seguir no banco de dados de pedidos de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3515-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="e3515-124">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="e3515-124">External tables</span></span>
<span data-ttu-id="e3515-125">Crie uma tabela externa Olá pedidos banco de dados que corresponde a definição de saudação da tabela de CustomerInformation hello:</span><span class="sxs-lookup"><span data-stu-id="e3515-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="e3515-126">Executar uma consulta T-SQL no banco de dados elástico de exemplo</span><span class="sxs-lookup"><span data-stu-id="e3515-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="e3515-127">Depois de definir a fonte de dados externa e suas tabelas externas, agora você pode usar tooquery T-SQL as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="e3515-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="e3515-128">Execute esta consulta no banco de dados de pedidos de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3515-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="e3515-129">Custo</span><span class="sxs-lookup"><span data-stu-id="e3515-129">Cost</span></span>
<span data-ttu-id="e3515-130">No momento, o recurso de consulta de banco de dados Elástico Olá está incluído nos custo de saudação do banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3515-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="e3515-131">Para saber mais sobre preços, consulte [Preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="e3515-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3515-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3515-132">Next steps</span></span>

* <span data-ttu-id="e3515-133">Para obter uma visão geral de consulta elástica, consulte [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3515-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="e3515-134">Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="e3515-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="e3515-135">Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e3515-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="e3515-136">Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="e3515-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="e3515-137">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="e3515-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>