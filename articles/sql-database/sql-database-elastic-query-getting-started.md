---
title: "Relatórios em bancos de dados expandidos na nuvem (particionamento horizontal) | Microsoft Docs"
description: como usar consultas de banco de dados entre bancos de dados
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="04e81-103">Relatórios entre bancos de dados expandidos na nuvem (preview)</span><span class="sxs-lookup"><span data-stu-id="04e81-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="04e81-104">Você pode criar relatórios de vários bancos de dados do SQL Azure de um ponto de conexão única usando uma [consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="04e81-105">Os bancos de dados devem ser particionados horizontalmente (também conhecido como "fragmentados").</span><span class="sxs-lookup"><span data-stu-id="04e81-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="04e81-106">Se você tiver um banco de dados existente, consulte [Migrando bancos de dados existentes para bancos de dados expandidos](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="04e81-107">Para compreender os objetos SQL necessários para a consulta, veja [Consultar bancos de dados particionados horizontalmente](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04e81-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="04e81-108">Prerequisites</span></span>
<span data-ttu-id="04e81-109">Baixe e execute a [exemplo da Introdução às ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="04e81-110">Criar um gerenciador de mapa de fragmentos usando o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="04e81-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="04e81-111">Aqui você vai criar um gerenciador de mapa de fragmentos juntamente com vários fragmentos, seguido pela inserção de dados nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="04e81-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="04e81-112">Se você já tem fragmentos configurados com dados fragmentados, poderá ignorar as etapas a seguir e mover para a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="04e81-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="04e81-113">Compile e execute o aplicativo de exemplo da **Introdução às ferramentas de Banco de Dados Elástico** .</span><span class="sxs-lookup"><span data-stu-id="04e81-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="04e81-114">Siga as etapas até a 7 na seção [Baixe e execute o aplicativo de exemplo](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="04e81-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="04e81-115">No final da etapa 7, você verá o seguinte prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="04e81-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![prompt de comando][1]
2. <span data-ttu-id="04e81-117">Na janela Comando, digite "1" e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="04e81-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="04e81-118">Isso cria o gerenciador de mapa de fragmentos e adiciona dois fragmentos ao servidor.</span><span class="sxs-lookup"><span data-stu-id="04e81-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="04e81-119">Em seguida, digite "3" e pressione **Enter**. Repita a ação quatro vezes.</span><span class="sxs-lookup"><span data-stu-id="04e81-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="04e81-120">Isso insere linhas de dados de exemplo no seus fragmentos.</span><span class="sxs-lookup"><span data-stu-id="04e81-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="04e81-121">O [Portal do Azure](https://portal.azure.com) deve mostrar três novos bancos de dados em seu servidor:</span><span class="sxs-lookup"><span data-stu-id="04e81-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Confirmação do Visual Studio][2]

   <span data-ttu-id="04e81-123">Neste ponto, consultas entre bancos de dados têm suporte por meio de bibliotecas de cliente do Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="04e81-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="04e81-124">Por exemplo, use a opção 4 na janela Comando.</span><span class="sxs-lookup"><span data-stu-id="04e81-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="04e81-125">Os resultados de uma consulta de vários fragmento são sempre um **UNION ALL** dos resultados de todos os fragmentos.</span><span class="sxs-lookup"><span data-stu-id="04e81-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="04e81-126">Na próxima seção, criaremos um ponto de extremidade de banco de dados de exemplo que dá suporte a consultas mais avançadas de dados entre fragmentos.</span><span class="sxs-lookup"><span data-stu-id="04e81-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="04e81-127">Criar um banco de dados de consulta elástico</span><span class="sxs-lookup"><span data-stu-id="04e81-127">Create an elastic query database</span></span>
1. <span data-ttu-id="04e81-128">Abra o [Portal do Azure](https://portal.azure.com) e faça logon.</span><span class="sxs-lookup"><span data-stu-id="04e81-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="04e81-129">Crie um novo Banco de Dados SQL do Azure no mesmo servidor que a instalação do fragmento.</span><span class="sxs-lookup"><span data-stu-id="04e81-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="04e81-130">Nomeie o banco de dados como "ElasticDBQuery".</span><span class="sxs-lookup"><span data-stu-id="04e81-130">Name the database "ElasticDBQuery."</span></span>

    ![Portal do Azure e camada de preços][3]

    > [!NOTE]
    > <span data-ttu-id="04e81-132">você pode usar um banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="04e81-132">you can use an existing database.</span></span> <span data-ttu-id="04e81-133">Se fizer isso, ele não deve ser um dos fragmentos aonde você deseja executar suas consultas.</span><span class="sxs-lookup"><span data-stu-id="04e81-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="04e81-134">Esse banco de dados será usado para criar os objetos de metadados para uma consulta de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="04e81-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="04e81-135">Criar objetos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="04e81-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="04e81-136">Chave mestra do escopo do banco de dados e credenciais</span><span class="sxs-lookup"><span data-stu-id="04e81-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="04e81-137">Eles são usados para conectar ao gerenciador de mapa de fragmentos e aos fragmentos:</span><span class="sxs-lookup"><span data-stu-id="04e81-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="04e81-138">Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04e81-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="04e81-139">Conecte-se ao banco de dados ElasticDBQuery e execute os seguintes comandos T-SQL:</span><span class="sxs-lookup"><span data-stu-id="04e81-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="04e81-140">"username" e "password" devem ser o mesmo que as informações de logon usadas na etapa 6 do [Baixar e executar o aplicativo de exemplo](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) na [Introdução às ferramentas de banco de dados elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="04e81-141">Fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="04e81-141">External data sources</span></span>
<span data-ttu-id="04e81-142">Para criar uma fonte de dados externa, execute o seguinte comando no banco de dados ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="04e81-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="04e81-143">"CustomerIDShardMap" é o nome do mapa de fragmentos, se você tiver criado um mapa de fragmentos e o gerenciador de mapa de fragmentos usando as ferramentas de banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="04e81-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="04e81-144">No entanto, se você usou a configuração personalizada para este exemplo, ele deve ter o nome do mapa de fragmento escolhido no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04e81-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="04e81-145">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="04e81-145">External tables</span></span>
<span data-ttu-id="04e81-146">Crie uma tabela externa que corresponda à tabela de Clientes nos fragmentos executando o comando a seguir no banco de dados ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="04e81-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="04e81-147">Executar uma consulta T-SQL no banco de dados elástico de exemplo</span><span class="sxs-lookup"><span data-stu-id="04e81-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="04e81-148">Depois que tiver definido sua fonte de dados e tabelas externas, agora você poderá usar o T-SQL completo nas tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="04e81-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="04e81-149">Execute esta consulta no banco de dados ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="04e81-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="04e81-150">Você observará que a consulta agrega os resultados de todos os fragmentos e fornece a seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="04e81-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Detalhes de saída][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="04e81-152">Importar resultados de consulta de banco de dados elástico para o Excel</span><span class="sxs-lookup"><span data-stu-id="04e81-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="04e81-153">Você pode importar os resultados de uma consulta para um arquivo do Excel.</span><span class="sxs-lookup"><span data-stu-id="04e81-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="04e81-154">Inicie o Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="04e81-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="04e81-155">Navegue até a faixa de opções **Dados** .</span><span class="sxs-lookup"><span data-stu-id="04e81-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="04e81-156">Clique em **De Outras Fontes** e em **Do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="04e81-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importação de outras fontes para o Excel][5]
4. <span data-ttu-id="04e81-158">No **Assistente para conexão de dados** , digite as credenciais de logon e nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="04e81-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="04e81-159">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="04e81-159">Then click **Next**.</span></span>
5. <span data-ttu-id="04e81-160">Na caixa de diálogo **Selecione o banco de dados que contém os dados que você deseja**, selecione o banco de dados **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="04e81-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="04e81-161">Selecione a tabela **Clientes** na exibição de lista e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="04e81-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="04e81-162">Em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="04e81-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="04e81-163">No formulário **Importar Dados** em **Selecione como deseja exibir esses dados na sua pasta de trabalho**, selecione **Tabela** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="04e81-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="04e81-164">Todas as linhas da tabela **Clientes** , armazenada em fragmentos diferentes, populam a planilha do Excel.</span><span class="sxs-lookup"><span data-stu-id="04e81-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="04e81-165">Agora você pode usar funções avançadas de visualização de dados do Excel.</span><span class="sxs-lookup"><span data-stu-id="04e81-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="04e81-166">Você pode usar a cadeia de conexão com o nome do servidor, nome do banco de dados e credenciais para conectar suas ferramentas de integração de dados e BI ao banco de dados de consulta elástico.</span><span class="sxs-lookup"><span data-stu-id="04e81-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="04e81-167">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="04e81-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="04e81-168">Você pode consultar o banco de dados de consulta elástico e tabelas externas como qualquer outro banco de dados e tabela do SQL Server que se conectariam à sua ferramenta.</span><span class="sxs-lookup"><span data-stu-id="04e81-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="04e81-169">Custo</span><span class="sxs-lookup"><span data-stu-id="04e81-169">Cost</span></span>
<span data-ttu-id="04e81-170">Não há nenhum custo adicional para usar o recurso de consulta de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="04e81-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="04e81-171">Para obter informações sobre os preços, consulte [Detalhes de preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="04e81-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04e81-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04e81-172">Next steps</span></span>

* <span data-ttu-id="04e81-173">Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="04e81-174">Para obter um tutorial sobre particionamento vertical, veja [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="04e81-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="04e81-175">Para sintaxe e exemplos de consultas para dados particionados verticalmente, veja [Consulta de dados particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="04e81-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="04e81-176">Para sintaxe e exemplos de consultas para dados particionados horizontalmente, veja [Consulta de dados particionados horizontalmente](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="04e81-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="04e81-177">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="04e81-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
