---
title: "Introdução às consultas entre bancos de dados (particionamento vertical) | Microsoft Docs"
description: "como usar a consulta de banco de dados elástico com bancos de dados particionados verticalmente"
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
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="0af79-103">Introdução às consultas entre bancos de dados (particionamento vertical) (preview)</span><span class="sxs-lookup"><span data-stu-id="0af79-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="0af79-104">A consulta de banco de dados elástico (visualização) para o Banco de Dados SQL do Azure permite executar consultas T-SQL que abrangem vários bancos de dados usando um único ponto de conexão.</span><span class="sxs-lookup"><span data-stu-id="0af79-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="0af79-105">Este tópico se aplica a [bancos de dados particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="0af79-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="0af79-106">Quando tiver concluído, você saberá como configurar e usar um Banco de Dados SQL do Azure para executar consultas que abrangem vários bancos de dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="0af79-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="0af79-107">Para saber mais sobre o recurso de consulta de banco de dados elástico, veja a [visão geral da consulta de banco de dados elástico do Banco de Dados SQL do Azure](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0af79-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0af79-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0af79-108">Prerequisites</span></span>

<span data-ttu-id="0af79-109">Você deve ter a permissão para ALTERAR QUALQUER FONTE DE DADOS EXTERNA.</span><span class="sxs-lookup"><span data-stu-id="0af79-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="0af79-110">Essa permissão está incluída na permissão ALTERAR BANCO DE DADOS.</span><span class="sxs-lookup"><span data-stu-id="0af79-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="0af79-111">As permissões para ALTERAR QUALQUER FONTE DE DADOS EXTERNA são necessárias para referenciar a fonte de dados subjacente.</span><span class="sxs-lookup"><span data-stu-id="0af79-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="0af79-112">Criar os bancos de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="0af79-112">Create the sample databases</span></span>
<span data-ttu-id="0af79-113">Para começar, precisamos criar dois bancos de dados, **Customers** e **Orders**, nos mesmos servidores lógicos ou em servidores diferentes.</span><span class="sxs-lookup"><span data-stu-id="0af79-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="0af79-114">Execute as consultas a seguir no banco de dados **Orders** para criar a tabela **OrderInformation** e inserir os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0af79-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="0af79-115">Agora, execute a consulta a seguir no banco de dados **Customers** para criar a tabela **CustomerInformation** e inserir os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0af79-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="0af79-116">Criar objetos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="0af79-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="0af79-117">Chave mestra e credenciais do escopo do banco de dados</span><span class="sxs-lookup"><span data-stu-id="0af79-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="0af79-118">Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0af79-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="0af79-119">Conecte-se ao banco de dados Orders e execute os seguintes comandos T-SQL:</span><span class="sxs-lookup"><span data-stu-id="0af79-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="0af79-120">O "nome de usuário" e a "senha" devem ser o nome de usuário e a senha usados para fazer logon no banco de dados Customers.</span><span class="sxs-lookup"><span data-stu-id="0af79-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="0af79-121">Atualmente não há suporte para a autenticação usando o Azure Active Directory com consultas elásticas.</span><span class="sxs-lookup"><span data-stu-id="0af79-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="0af79-122">Fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="0af79-122">External data sources</span></span>
<span data-ttu-id="0af79-123">Para criar uma fonte de dados externa, execute o seguinte comando no banco de dados Orders:</span><span class="sxs-lookup"><span data-stu-id="0af79-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="0af79-124">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="0af79-124">External tables</span></span>
<span data-ttu-id="0af79-125">Crie uma tabela externa ao banco de dados Orders, que corresponde à definição da tabela CustomerInformation:</span><span class="sxs-lookup"><span data-stu-id="0af79-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="0af79-126">Executar uma consulta T-SQL no banco de dados elástico de exemplo</span><span class="sxs-lookup"><span data-stu-id="0af79-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="0af79-127">Depois de definir sua fonte de dados e suas tabelas externas, agora você poderá usar o T-SQL para consultar suas tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="0af79-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="0af79-128">Execute esta consulta no banco de dados Orders:</span><span class="sxs-lookup"><span data-stu-id="0af79-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="0af79-129">Custo</span><span class="sxs-lookup"><span data-stu-id="0af79-129">Cost</span></span>
<span data-ttu-id="0af79-130">Atualmente, o recurso de consulta de banco de dados elástico está incluído no custo de seu Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af79-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="0af79-131">Para saber mais sobre preços, consulte [Preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="0af79-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0af79-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0af79-132">Next steps</span></span>

* <span data-ttu-id="0af79-133">Para obter uma visão geral de consulta elástica, consulte [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0af79-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="0af79-134">Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="0af79-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="0af79-135">Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0af79-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="0af79-136">Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="0af79-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="0af79-137">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="0af79-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>