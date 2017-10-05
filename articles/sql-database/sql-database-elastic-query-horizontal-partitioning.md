---
title: "Relatórios entre bancos de dados em nuvem expandidos | Microsoft Docs"
description: "como configurar consultas elásticas em partições horizontais"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 62b5bcd26aa1ed219fb38970916e0e8847ceb577
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="fb22f-103">Relatórios entre bancos de dados em nuvem expandidos (visualização)</span><span class="sxs-lookup"><span data-stu-id="fb22f-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Consultar em fragmentos][1]

<span data-ttu-id="fb22f-105">Bancos de dados fragmentados distribuem linhas em uma camada de dados expandida.</span><span class="sxs-lookup"><span data-stu-id="fb22f-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="fb22f-106">O esquema é idêntico em todos os bancos de dados participantes, também conhecido como particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fb22f-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="fb22f-107">Usando uma consulta elástica, você pode criar relatórios que abrangem todos os bancos de dados em um banco de dados fragmentado.</span><span class="sxs-lookup"><span data-stu-id="fb22f-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="fb22f-108">Para um início rápido, confira [Relatórios entre bancos de dados em nuvem expandidos](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="fb22f-109">Para bancos de dados não fragmentados, consulte [Query across cloud databases with different schemas (Consulta entre bancos de dados na nuvem com esquemas diferentes)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fb22f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fb22f-110">Prerequisites</span></span>
* <span data-ttu-id="fb22f-111">Crie um mapa de fragmentos usando a biblioteca de cliente do banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="fb22f-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="fb22f-112">Confira [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="fb22f-113">Ou use o aplicativo de exemplo em [Introdução às ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="fb22f-114">Como alternativa, confira [Migrar bancos de dados existentes para bancos de dados expandidos](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="fb22f-115">O usuário deve ter a permissão para ALTERAR QUALQUER FONTE DE DADOS EXTERNA.</span><span class="sxs-lookup"><span data-stu-id="fb22f-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="fb22f-116">Essa permissão está incluída na permissão ALTERAR BANCO DE DADOS.</span><span class="sxs-lookup"><span data-stu-id="fb22f-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="fb22f-117">As permissões para ALTERAR QUALQUER FONTE DE DADOS EXTERNA são necessárias para referenciar a fonte de dados subjacente.</span><span class="sxs-lookup"><span data-stu-id="fb22f-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="fb22f-118">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fb22f-118">Overview</span></span>
<span data-ttu-id="fb22f-119">Essas instruções criam a representação de metadados de sua camada de dados fragmentados no banco de dados de consulta elástico.</span><span class="sxs-lookup"><span data-stu-id="fb22f-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="fb22f-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="fb22f-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="fb22f-121">CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS</span><span class="sxs-lookup"><span data-stu-id="fb22f-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="fb22f-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="fb22f-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="fb22f-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="fb22f-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="fb22f-124">1.1 Criar chave mestra do escopo do banco de dados e credenciais</span><span class="sxs-lookup"><span data-stu-id="fb22f-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="fb22f-125">A credencial é usada pela consulta elástica para se conectar aos bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="fb22f-126">Certifique-se de que o *"\<nome de usuário\>"* não inclui nenhum sufixo *"@servername"*.</span><span class="sxs-lookup"><span data-stu-id="fb22f-126">Make sure that the *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="fb22f-127">1.2 Criar fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="fb22f-127">1.2 Create external data sources</span></span>
<span data-ttu-id="fb22f-128">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="fb22f-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="fb22f-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fb22f-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="fb22f-130">Recupere a lista de fontes de dados externas atuais:</span><span class="sxs-lookup"><span data-stu-id="fb22f-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="fb22f-131">A fonte de dados externa faz referência ao seu mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-131">The external data source references your shard map.</span></span> <span data-ttu-id="fb22f-132">Uma consulta elástica então usa a fonte de dados externa e o mapa de fragmentos subjacente para enumerar os bancos de dados que participam da camada de dados.</span><span class="sxs-lookup"><span data-stu-id="fb22f-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="fb22f-133">As mesmas credenciais são usadas para ler o mapa de fragmentos e acessar os dados nos fragmentos durante o processamento de uma consulta elástica.</span><span class="sxs-lookup"><span data-stu-id="fb22f-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="fb22f-134">1.3 Criar tabelas externas</span><span class="sxs-lookup"><span data-stu-id="fb22f-134">1.3 Create external tables</span></span>
<span data-ttu-id="fb22f-135">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="fb22f-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="fb22f-136">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="fb22f-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="fb22f-137">Recupere a lista de tabelas externas do banco de dados atual:</span><span class="sxs-lookup"><span data-stu-id="fb22f-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="fb22f-138">Para descartar tabelas externas:</span><span class="sxs-lookup"><span data-stu-id="fb22f-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="fb22f-139">Comentários</span><span class="sxs-lookup"><span data-stu-id="fb22f-139">Remarks</span></span>
<span data-ttu-id="fb22f-140">A cláusula DATA\_SOURCE define a fonte de dados externa (um mapa de fragmentos) usada para a tabela externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="fb22f-141">As cláusulas SCHEMA\_NAME e OBJECT\_NAME mapeiam a definição da tabela externa para uma tabela em um esquema diferente.</span><span class="sxs-lookup"><span data-stu-id="fb22f-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="fb22f-142">Se for omitido, o esquema do objeto remoto será considerado “dbo” e seu nome será considerado como sendo idêntico ao nome da tabela externa que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="fb22f-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="fb22f-143">Isso é útil se o nome da tabela remota já existe no banco de dados em que você deseja criar a tabela externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="fb22f-144">Por exemplo, defina uma tabela externa para obter uma exibição agregada de exibições de catálogo ou de DMVs em sua camada de dados expandida.</span><span class="sxs-lookup"><span data-stu-id="fb22f-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="fb22f-145">Como as exibições de catálogo e as DMVs já existem localmente, você não pode usar seus nomes para a definição da tabela externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="fb22f-146">Em vez disso, use um nome diferente e use a exibição do catálogo ou o nome de DMV nas cláusulas SCHEMA\_NAME e/ou OBJECT\_NAME.</span><span class="sxs-lookup"><span data-stu-id="fb22f-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="fb22f-147">(Veja o exemplo abaixo.)</span><span class="sxs-lookup"><span data-stu-id="fb22f-147">(See the example below.)</span></span> 

<span data-ttu-id="fb22f-148">A cláusula DISTRIBUTION especifica a distribuição de dados usada para esta tabela.</span><span class="sxs-lookup"><span data-stu-id="fb22f-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="fb22f-149">O processador de consultas utiliza as informações fornecidas na cláusula DISTRIBUTION para criar planos de consulta mais eficientes.</span><span class="sxs-lookup"><span data-stu-id="fb22f-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="fb22f-150">**SHARDED** significa que os dados são particionados horizontalmente entre os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb22f-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="fb22f-151">A chave de particionamento para a distribuição de dados é o parâmetro **<sharding_column_name>**.</span><span class="sxs-lookup"><span data-stu-id="fb22f-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="fb22f-152">**REPLICATED** significa que cópias idênticas da tabela estão presentes em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb22f-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="fb22f-153">É sua responsabilidade assegurar que as réplicas sejam idênticas entre os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb22f-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="fb22f-154">**ROUND\_ROBIN** significa que a tabela é horizontalmente particionada usando um método de distribuição dependente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb22f-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="fb22f-155">**Referência de camada de dados**: a DDL da tabela externa faz referência a uma fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="fb22f-156">A fonte de dados externa especifica um mapa de fragmentos que fornece à tabela externa as informações necessárias para localizar todos os bancos de dados em sua camada de dados.</span><span class="sxs-lookup"><span data-stu-id="fb22f-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="fb22f-157">Considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="fb22f-157">Security considerations</span></span>
<span data-ttu-id="fb22f-158">Usuários com acesso à tabela externa têm acesso automaticamente a tabelas remotas subjacentes com a credencial fornecida na definição de fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="fb22f-159">Evite a elevação de privilégios indesejada usando credencial da fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="fb22f-160">Use GRANT ou REVOKE para uma tabela externa como se fosse uma tabela normal.</span><span class="sxs-lookup"><span data-stu-id="fb22f-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="fb22f-161">Depois de definir a fonte de dados externa e as tabelas externas, agora você poderá usar o T-SQL completo nas tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="fb22f-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="fb22f-162">Exemplo: consultando bancos de dados particionados horizontais</span><span class="sxs-lookup"><span data-stu-id="fb22f-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="fb22f-163">A consulta a seguir executa uma junção de três vias entre depósitos, pedidos e linhas da pedido e usa várias agregações e um filtro seletivo.</span><span class="sxs-lookup"><span data-stu-id="fb22f-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="fb22f-164">Ele pressupõe que o (1) particionamento horizontal (fragmentação) e (2) esses depósitos, pedidos e linhas de pedido são fragmentados pela coluna de ID de depósito, e que a consulta elástica pode colocar as junções nos fragmentos e processar a parte cara da consulta nos fragmentos de modo paralelo.</span><span class="sxs-lookup"><span data-stu-id="fb22f-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="fb22f-165">Procedimento armazenado para a execução remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="fb22f-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="fb22f-166">A consulta elástica também apresenta um procedimento armazenado que fornece acesso direto aos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="fb22f-167">O procedimento armazenado é chamado [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) e pode ser usado para executar procedimentos armazenados remotos ou código T-SQL em bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="fb22f-168">Ele usa os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fb22f-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="fb22f-169">Nome da fonte de dados (nvarchar): o nome da fonte de dados externa do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="fb22f-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="fb22f-170">Consulta (nvarchar): a consulta T-SQL a ser executada em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="fb22f-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="fb22f-171">Declaração de parâmetro (nvarchar) - opcional: cadeia de caracteres com definições de tipo de dados para os parâmetros usados no parâmetro Query (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="fb22f-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="fb22f-172">Lista de valores de parâmetro - opcional: lista separada por vírgulas de valores de parâmetro (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="fb22f-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="fb22f-173">O sp\_execute\_remote usa a fonte de dados externa fornecida nos parâmetros de invocação para executar a instrução T-SQL especificada nos bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="fb22f-174">Ele usa a credencial da fonte de dados externa para a conexão com o banco de dados do gerenciador de mapa do fragmento e bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="fb22f-175">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="fb22f-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="fb22f-176">Conectividade de ferramentas</span><span class="sxs-lookup"><span data-stu-id="fb22f-176">Connectivity for tools</span></span>
<span data-ttu-id="fb22f-177">Use cadeias de conexão regulares do SQL Server para conectar seu aplicativo e suas ferramentas de BI e de integração de dados ao banco de dados com as definições da tabela externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="fb22f-178">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="fb22f-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="fb22f-179">Em seguida, faça referência ao banco de dados de consulta elástica como qualquer outro banco de dados do SQL Server conectado à ferramenta, e use tabelas externas de sua ferramenta ou aplicativo como se elas fossem tabelas locais.</span><span class="sxs-lookup"><span data-stu-id="fb22f-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="fb22f-180">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="fb22f-180">Best practices</span></span>
* <span data-ttu-id="fb22f-181">Verifique se o banco de dados do ponto de extremidade da consulta elástica recebeu acesso ao banco de dados do mapa de fragmentos e a todos os fragmentos por meio dos firewalls do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="fb22f-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="fb22f-182">Valide ou imponha a distribuição de dados definida pela tabela externa.</span><span class="sxs-lookup"><span data-stu-id="fb22f-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="fb22f-183">Se a distribuição de dados real for diferente da distribuição especificada na definição de tabela, as consultas podem gerar resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="fb22f-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="fb22f-184">A consulta elástica atualmente não executa a eliminação de fragmentos quando predicados da chave de fragmentação permitem que ela exclua com segurança determinados fragmentos do processamento.</span><span class="sxs-lookup"><span data-stu-id="fb22f-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="fb22f-185">A consulta elástica funciona melhor para consultas em que a maior parte da computação pode ser realizada nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="fb22f-186">Normalmente o melhor desempenho de consulta é obtido com predicados de filtro seletivo que podem ser avaliados nos fragmentos ou junções sobre as chaves de particionamento que podem ser executadas de forma alinhada por partição em todos os fragmentos.</span><span class="sxs-lookup"><span data-stu-id="fb22f-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="fb22f-187">Outros padrões de consulta podem precisar carregar grandes quantidades de dados dos fragmentos para o nó de cabeçalho e podem ter um desempenho insatisfatório</span><span class="sxs-lookup"><span data-stu-id="fb22f-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb22f-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb22f-188">Next steps</span></span>

* <span data-ttu-id="fb22f-189">Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="fb22f-190">Para obter um tutorial sobre particionamento vertical, veja [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="fb22f-191">Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="fb22f-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="fb22f-192">Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb22f-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="fb22f-193">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fb22f-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
