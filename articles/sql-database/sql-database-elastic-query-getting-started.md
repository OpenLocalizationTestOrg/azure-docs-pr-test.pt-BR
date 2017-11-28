---
title: aaaReport em bancos de dados de nuvem expandido (particionamento horizontal) | Microsoft Docs
description: como toouse cruzada consultas de banco de dados do banco de dados
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
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="4d33d-103">Relatórios entre bancos de dados expandidos na nuvem (preview)</span><span class="sxs-lookup"><span data-stu-id="4d33d-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="4d33d-104">Você pode criar relatórios de vários bancos de dados do SQL Azure de um ponto de conexão única usando uma [consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="4d33d-105">bancos de dados Olá devem ser particionados horizontalmente (também conhecido como "fragmentados").</span><span class="sxs-lookup"><span data-stu-id="4d33d-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="4d33d-106">Se você tiver um banco de dados existente, consulte [existente migrando bancos de dados de bancos de dados de saída tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="4d33d-107">objetos do SQL Olá toounderstand necessário tooquery, consulte [consultas em bancos de dados particionados horizontalmente](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d33d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4d33d-108">Prerequisites</span></span>
<span data-ttu-id="4d33d-109">Baixe e execute Olá [guia de Introdução com amostra das ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="4d33d-110">Criar um mapa do fragmento manager usando o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="4d33d-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="4d33d-111">Aqui você criará um mapa do fragmento manager juntamente com vários fragmentos, seguido de inserção de dados em fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="4d33d-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="4d33d-112">Se você se deparar tooalready possuem instalação fragmentos com dados fragmentados, você pode ignorar Olá etapas a seguir e mover toohello próxima seção.</span><span class="sxs-lookup"><span data-stu-id="4d33d-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="4d33d-113">Compilar e executar Olá **Introdução às ferramentas de banco de dados Elástico** aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="4d33d-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="4d33d-114">Execute as etapas de saudação até a etapa 7 na seção Olá [Baixe e execute o aplicativo de exemplo hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="4d33d-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="4d33d-115">No final da saudação da etapa 7, você verá saudação de prompt de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d33d-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![prompt de comando][1]
2. <span data-ttu-id="4d33d-117">Na janela de comando hello, digite "1" e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4d33d-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="4d33d-118">Isso cria o Gerenciador do mapa de fragmentos Olá e adiciona dois servidores toohello de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4d33d-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="4d33d-119">Em seguida, digite "3" e pressione **Enter**; repetir a ação de saudação quatro vezes.</span><span class="sxs-lookup"><span data-stu-id="4d33d-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="4d33d-120">Isso insere linhas de dados de exemplo no seus fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4d33d-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="4d33d-121">Olá [portal do Azure](https://portal.azure.com) devem mostrar três novos bancos de dados em seu servidor:</span><span class="sxs-lookup"><span data-stu-id="4d33d-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Confirmação do Visual Studio][2]

   <span data-ttu-id="4d33d-123">Neste ponto, as consultas de bancos de dados têm suporte por meio de bibliotecas de cliente do banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="4d33d-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="4d33d-124">Por exemplo, use a opção 4 na janela de comando hello.</span><span class="sxs-lookup"><span data-stu-id="4d33d-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="4d33d-125">resultados de saudação de uma consulta de vários fragmento são sempre um **UNION ALL** dos resultados de saudação de todos os fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4d33d-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="4d33d-126">Na próxima seção, Olá, podemos criar um ponto de extremidade de banco de dados de exemplo que oferece suporte a consultas mais sofisticadas de dados de saudação em fragmentos.</span><span class="sxs-lookup"><span data-stu-id="4d33d-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="4d33d-127">Criar um banco de dados de consulta elástico</span><span class="sxs-lookup"><span data-stu-id="4d33d-127">Create an elastic query database</span></span>
1. <span data-ttu-id="4d33d-128">Olá abrir [portal do Azure](https://portal.azure.com) e faça logon.</span><span class="sxs-lookup"><span data-stu-id="4d33d-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="4d33d-129">Criar um novo banco de dados do SQL Azure no hello mesmo servidor como sua configuração de fragmento.</span><span class="sxs-lookup"><span data-stu-id="4d33d-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="4d33d-130">Nome do banco de dados hello "ElasticDBQuery".</span><span class="sxs-lookup"><span data-stu-id="4d33d-130">Name hello database "ElasticDBQuery."</span></span>

    ![Portal do Azure e camada de preços][3]

    > [!NOTE]
    > <span data-ttu-id="4d33d-132">você pode usar um banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="4d33d-132">you can use an existing database.</span></span> <span data-ttu-id="4d33d-133">Se você pode fazer isso, ele não deve ser um dos fragmentos de saudação que deseja tooexecute suas consultas em.</span><span class="sxs-lookup"><span data-stu-id="4d33d-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="4d33d-134">Este banco de dados será usado para criar objetos de metadados para uma consulta de banco de dados Elástico de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d33d-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="4d33d-135">Criar objetos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="4d33d-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="4d33d-136">Chave mestra do escopo do banco de dados e credenciais</span><span class="sxs-lookup"><span data-stu-id="4d33d-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="4d33d-137">Estes são Gerenciador do mapa do fragmento usado tooconnect toohello e fragmentos de saudação:</span><span class="sxs-lookup"><span data-stu-id="4d33d-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="4d33d-138">Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d33d-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="4d33d-139">Conecte-se o banco de dados tooElasticDBQuery e execute Olá comandos T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d33d-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="4d33d-140">"username" e "password" deve ser Olá mesmo como informações de logon usadas na etapa 6 de [Baixe e execute o aplicativo de exemplo hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) na [Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="4d33d-141">Fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="4d33d-141">External data sources</span></span>
<span data-ttu-id="4d33d-142">toocreate uma fonte de dados externa, execute Olá comando a seguir no banco de dados de ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="4d33d-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="4d33d-143">"CustomerIDShardMap" é o nome de saudação do mapa do fragmento hello, se você criou o mapa do fragmento hello e o mapa do fragmento manager usando o exemplo de ferramentas de banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="4d33d-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="4d33d-144">No entanto, se você usou a configuração personalizada para este exemplo, ele deve ser nome do mapa de fragmentos Olá escolhido em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d33d-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="4d33d-145">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="4d33d-145">External tables</span></span>
<span data-ttu-id="4d33d-146">Crie uma tabela externa que coincide com a tabela de clientes de saudação em fragmentos Olá executando o comando a seguir no banco de dados ElasticDBQuery de saudação:</span><span class="sxs-lookup"><span data-stu-id="4d33d-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="4d33d-147">Executar uma consulta T-SQL no banco de dados elástico de exemplo</span><span class="sxs-lookup"><span data-stu-id="4d33d-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="4d33d-148">Depois que tiver definido sua fonte de dados e tabelas externas, agora você poderá usar o T-SQL completo nas tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="4d33d-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="4d33d-149">Execute esta consulta no banco de dados de ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="4d33d-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="4d33d-150">Você notará que consultam Olá agrega os resultados de todos os fragmentos de saudação e fornece Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d33d-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Detalhes de saída][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="4d33d-152">Importar tooExcel de resultados de consulta de banco de dados Elástico</span><span class="sxs-lookup"><span data-stu-id="4d33d-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="4d33d-153">Você pode importar resultados de saudação de um consulta tooan do arquivo de Excel.</span><span class="sxs-lookup"><span data-stu-id="4d33d-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="4d33d-154">Inicie o Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="4d33d-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="4d33d-155">Navegue toohello **dados** faixa de opções.</span><span class="sxs-lookup"><span data-stu-id="4d33d-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="4d33d-156">Clique em **De Outras Fontes** e em **Do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4d33d-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importação de outras fontes para o Excel][5]
4. <span data-ttu-id="4d33d-158">Em Olá **Assistente de Conexão de dados** digite credenciais de nome e logon do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d33d-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="4d33d-159">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="4d33d-159">Then click **Next**.</span></span>
5. <span data-ttu-id="4d33d-160">Na caixa de diálogo Olá **banco de dados Olá Select que contém dados Olá deseja**, selecione Olá **ElasticDBQuery** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4d33d-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="4d33d-161">Selecione Olá **clientes** tabela na exibição de lista hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4d33d-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="4d33d-162">Em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4d33d-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="4d33d-163">Em Olá **importar dados** formulário, em **selecione como deseja tooview esses dados na pasta de trabalho**, selecione **tabela** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4d33d-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="4d33d-164">Todos os Olá linhas de **clientes** tabela, armazenada em fragmentos diferentes preencher a planilha do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="4d33d-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="4d33d-165">Agora você pode usar funções avançadas de visualização de dados do Excel.</span><span class="sxs-lookup"><span data-stu-id="4d33d-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="4d33d-166">Você pode usar a cadeia de caracteres de conexão de saudação com seu nome de servidor, nome do banco de dados e credenciais tooconnect seu dados e BI integração ferramentas toohello Elástico consultar banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4d33d-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="4d33d-167">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="4d33d-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="4d33d-168">Você pode consultar o banco de dados de consulta Elástico toohello e tabelas externas, assim como qualquer outro banco de dados do SQL Server e tabelas do SQL Server que você se conectaria toowith sua ferramenta.</span><span class="sxs-lookup"><span data-stu-id="4d33d-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="4d33d-169">Custo</span><span class="sxs-lookup"><span data-stu-id="4d33d-169">Cost</span></span>
<span data-ttu-id="4d33d-170">Não há nenhum custo adicional para usar o recurso de consulta de banco de dados Elástico Olá.</span><span class="sxs-lookup"><span data-stu-id="4d33d-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="4d33d-171">Para obter informações sobre os preços, consulte [Detalhes de preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="4d33d-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d33d-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d33d-172">Next steps</span></span>

* <span data-ttu-id="4d33d-173">Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="4d33d-174">Para obter um tutorial sobre particionamento vertical, veja [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="4d33d-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="4d33d-175">Para sintaxe e exemplos de consultas para dados particionados verticalmente, veja [Consulta de dados particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="4d33d-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="4d33d-176">Para sintaxe e exemplos de consultas para dados particionados horizontalmente, veja [Consulta de dados particionados horizontalmente](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="4d33d-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="4d33d-177">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="4d33d-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
