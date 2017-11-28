---
title: "aaaReporting em bancos de dados de nuvem expansíveis | Microsoft Docs"
description: "como tooset Elástico consultas sobre partições horizontais"
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
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="897dd-103">Relatórios entre bancos de dados em nuvem expandidos (visualização)</span><span class="sxs-lookup"><span data-stu-id="897dd-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Consultar em fragmentos][1]

<span data-ttu-id="897dd-105">Bancos de dados fragmentados distribuem linhas em uma camada de dados expandida.</span><span class="sxs-lookup"><span data-stu-id="897dd-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="897dd-106">esquema de saudação é idêntica em todos os bancos de dados participantes, também conhecidos como o particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="897dd-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="897dd-107">Usando uma consulta elástica, você pode criar relatórios que abrangem todos os bancos de dados em um banco de dados fragmentado.</span><span class="sxs-lookup"><span data-stu-id="897dd-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="897dd-108">Para um início rápido, confira [Relatórios entre bancos de dados em nuvem expandidos](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="897dd-109">Para bancos de dados não fragmentados, consulte [Query across cloud databases with different schemas (Consulta entre bancos de dados na nuvem com esquemas diferentes)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="897dd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="897dd-110">Prerequisites</span></span>
* <span data-ttu-id="897dd-111">Crie um mapa do fragmento usando a biblioteca de cliente do banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="897dd-112">Confira [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="897dd-113">Ou use o aplicativo de exemplo hello no [Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="897dd-114">Como alternativa, consulte [existente Migrar bancos de dados de bancos de dados de saída tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="897dd-115">usuário Olá deve ter a permissão ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="897dd-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="897dd-116">Essa permissão é incluída com a permissão ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="897dd-117">Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="897dd-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="897dd-118">Visão geral</span><span class="sxs-lookup"><span data-stu-id="897dd-118">Overview</span></span>
<span data-ttu-id="897dd-119">Essas instruções criam representação de metadados de saudação de sua camada de dados fragmentado no banco de dados de consulta Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="897dd-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="897dd-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="897dd-121">CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS</span><span class="sxs-lookup"><span data-stu-id="897dd-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="897dd-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="897dd-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="897dd-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="897dd-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="897dd-124">1.1 Criar chave mestra do escopo do banco de dados e credenciais</span><span class="sxs-lookup"><span data-stu-id="897dd-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="897dd-125">Olá credencial é usada pelo Olá consulta Elástico tooconnect tooyour bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="897dd-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="897dd-126">Certifique-se de que Olá *"\<username\>"* não incluir nenhum *"@servername"* sufixo.</span><span class="sxs-lookup"><span data-stu-id="897dd-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="897dd-127">1.2 Criar fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="897dd-127">1.2 Create external data sources</span></span>
<span data-ttu-id="897dd-128">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="897dd-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="897dd-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="897dd-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="897dd-130">Recupere a lista de saudação de fontes de dados externas atual:</span><span class="sxs-lookup"><span data-stu-id="897dd-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="897dd-131">fonte de dados externa Olá faz referência a seu mapa de fragmento.</span><span class="sxs-lookup"><span data-stu-id="897dd-131">hello external data source references your shard map.</span></span> <span data-ttu-id="897dd-132">Uma consulta elástica usa fonte de dados externa hello e Olá subjacente fragmento mapa tooenumerate Olá bancos de dados que participam da camada de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="897dd-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="897dd-133">Olá, mesmo credenciais são mapa do fragmento Olá tooread usado e tooaccess Olá dados em fragmentos Olá durante o processamento de saudação de uma consulta Elástico.</span><span class="sxs-lookup"><span data-stu-id="897dd-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="897dd-134">1.3 Criar tabelas externas</span><span class="sxs-lookup"><span data-stu-id="897dd-134">1.3 Create external tables</span></span>
<span data-ttu-id="897dd-135">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="897dd-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="897dd-136">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="897dd-136">**Example**</span></span>

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

<span data-ttu-id="897dd-137">Recupere a lista de saudação de tabelas externas do banco de dados atual hello:</span><span class="sxs-lookup"><span data-stu-id="897dd-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="897dd-138">tabelas externas toodrop:</span><span class="sxs-lookup"><span data-stu-id="897dd-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="897dd-139">Comentários</span><span class="sxs-lookup"><span data-stu-id="897dd-139">Remarks</span></span>
<span data-ttu-id="897dd-140">Olá dados\_cláusula de fonte define a fonte de dados externa da saudação (um mapa do fragmento) que é usado para a tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="897dd-141">Olá esquema\_nome e o objeto\_cláusulas de nome mapeiam a tabela de tooa de definição de tabela externa de saudação em um esquema diferente.</span><span class="sxs-lookup"><span data-stu-id="897dd-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="897dd-142">Se omitido, o esquema de saudação do objeto remoto Olá é considerada toobe "dbo" e seu nome é considerado o nome da tabela externa toobe toohello idênticos que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="897dd-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="897dd-143">Isso é útil se Olá nome da tabela remota já existe no banco de dados de saudação onde deseja que a tabela externa do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="897dd-144">Por exemplo, você deseja toodefine tooget uma tabela externa uma exibição agregada de exibições do catálogo ou DMVs em seus dados de expansão de camada.</span><span class="sxs-lookup"><span data-stu-id="897dd-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="897dd-145">Como DMVs e modos de exibição de catálogo já existem localmente, você não pode usar seus nomes de definição de tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="897dd-146">Em vez disso, use um nome diferente e usar da exibição de catálogo hello ou Olá nome DMVS no esquema de saudação\_nome e/ou objeto\_cláusulas de nome.</span><span class="sxs-lookup"><span data-stu-id="897dd-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="897dd-147">(Consulte o exemplo hello abaixo).</span><span class="sxs-lookup"><span data-stu-id="897dd-147">(See hello example below.)</span></span> 

<span data-ttu-id="897dd-148">cláusula de distribuição de saudação especifica a distribuição de dados Olá usada para esta tabela.</span><span class="sxs-lookup"><span data-stu-id="897dd-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="897dd-149">processador de consultas Olá utiliza informações Olá fornecidas Olá distribuição cláusula toobuild hello mais eficientes planos de consulta.</span><span class="sxs-lookup"><span data-stu-id="897dd-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="897dd-150">**FRAGMENTADA** significa que dados são particionados horizontalmente em bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="897dd-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="897dd-151">Olá, chave de particionamento para distribuição de dados Olá Olá **< sharding_column_name >** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="897dd-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="897dd-152">**REPLICADAS** significa que cópias idênticas de tabela Olá estão presentes em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="897dd-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="897dd-153">É o tooensure responsabilidade réplicas Olá são idênticas em bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="897dd-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="897dd-154">**ROUND\_ROBIN** significa que essa tabela Olá é particionada horizontalmente usando um método de distribuição do aplicativo dependente.</span><span class="sxs-lookup"><span data-stu-id="897dd-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="897dd-155">**Referência da camada de dados**: tabela externa de saudação DDL refere-se a fonte de dados externa tooan.</span><span class="sxs-lookup"><span data-stu-id="897dd-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="897dd-156">fonte de dados externa Olá Especifica um mapa do fragmento que fornece tabela externa Olá Olá informações necessárias toolocate todos os bancos de dados de saudação em sua camada de dados.</span><span class="sxs-lookup"><span data-stu-id="897dd-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="897dd-157">Considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="897dd-157">Security considerations</span></span>
<span data-ttu-id="897dd-158">Os usuários com a tabela externa do acesso toohello automaticamente acessar tabelas remotas subjacentes de toohello na credencial Olá especificado na definição de fonte de dados externa hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="897dd-159">Evite indesejada elevação de privilégios por meio de credencial Olá Olá externo de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="897dd-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="897dd-160">Use GRANT ou REVOKE para uma tabela externa como se fosse uma tabela normal.</span><span class="sxs-lookup"><span data-stu-id="897dd-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="897dd-161">Depois de definir a fonte de dados externa e as tabelas externas, agora você poderá usar o T-SQL completo nas tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="897dd-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="897dd-162">Exemplo: consultando bancos de dados particionados horizontais</span><span class="sxs-lookup"><span data-stu-id="897dd-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="897dd-163">Olá consulta a seguir executa uma junção de três vias entre depósitos, pedidos e linhas de ordem e usa várias agregações e um filtro seletivo.</span><span class="sxs-lookup"><span data-stu-id="897dd-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="897dd-164">Ele assume o particionamento horizontal (1) (fragmentação) e (2) que depósitos, pedidos e linhas de ordem são fragmentadas pela coluna de id de warehouse hello e consulta Elástico Olá pode posicionar Olá junções em fragmentos hello e processar parte caro Olá consulta Olá Olá fragmentos em paralelo.</span><span class="sxs-lookup"><span data-stu-id="897dd-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="897dd-165">Procedimento armazenado para a execução remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="897dd-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="897dd-166">Consulta elástica também apresenta um procedimento armazenado que fornece acesso direto toohello fragmentos.</span><span class="sxs-lookup"><span data-stu-id="897dd-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="897dd-167">Olá procedimento armazenado é chamado [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) e pode ser usado tooexecute procedimentos armazenados ou código T-SQL em bancos de dados remotos hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="897dd-168">Ele usa Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="897dd-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="897dd-169">Nome da fonte de dados (nvarchar): nome de saudação da fonte de dados externa de saudação do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="897dd-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="897dd-170">Consulta (nvarchar): toobe de consulta Olá T-SQL executado em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="897dd-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="897dd-171">Declaração de parâmetro (nvarchar) - opcional: cadeia de caracteres com definições de tipo de dados para parâmetros de saudação usadas no parâmetro de consulta de saudação (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="897dd-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="897dd-172">Lista de valores de parâmetro - opcional: lista separada por vírgulas de valores de parâmetro (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="897dd-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="897dd-173">Olá sp\_executar\_remota usa Olá fornecida na seguinte instrução T-SQL em bancos de dados remotos Olá Olá invocação parâmetros tooexecute Olá de fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="897dd-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="897dd-174">Ele usa credenciais Olá Olá dados externos fonte tooconnect toohello shardmap manager banco de dados e bancos de dados remotos hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="897dd-175">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="897dd-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="897dd-176">Conectividade de ferramentas</span><span class="sxs-lookup"><span data-stu-id="897dd-176">Connectivity for tools</span></span>
<span data-ttu-id="897dd-177">Use tooconnect regular de cadeias de caracteres de conexão do SQL Server seu aplicativo, dados e BI integração ferramentas toohello banco de dados com suas definições de tabela externa.</span><span class="sxs-lookup"><span data-stu-id="897dd-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="897dd-178">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="897dd-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="897dd-179">Em seguida, fazer referência Olá Elástico consultar banco de dados como qualquer outra ferramenta de toohello conectado de banco de dados do SQL Server e use tabelas externas de seu aplicativo ou uma ferramenta como se fossem tabelas locais.</span><span class="sxs-lookup"><span data-stu-id="897dd-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="897dd-180">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="897dd-180">Best practices</span></span>
* <span data-ttu-id="897dd-181">Certifique-se de que esse banco de dados do ponto de extremidade de consulta Elástico Olá tem o banco de dados do access toohello shardmap e todos os fragmentos por meio de saudação que firewalls de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="897dd-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="897dd-182">Validar ou impor a distribuição de dados Olá definida pela tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="897dd-183">Se a distribuição de dados real é diferente de distribuição de saudação especificada na definição de tabela, as consultas podem produzir resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="897dd-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="897dd-184">Elástica consulta atualmente não executar eliminação de fragmento quando predicados de chave de fragmentação Olá permitiria que toosafely excluir determinados fragmentos do processamento.</span><span class="sxs-lookup"><span data-stu-id="897dd-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="897dd-185">Consulta elástica funciona melhor para consultas onde a maioria de computação Olá pode ser feita em fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="897dd-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="897dd-186">Você normalmente obtém melhor desempenho de consulta Olá com predicados de filtro seletivo que pode ser avaliada em fragmentos hello ou junções em Olá chaves que podem ser executadas de forma alinhado por partição em todos os fragmentos de particionamento.</span><span class="sxs-lookup"><span data-stu-id="897dd-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="897dd-187">Outros padrões de consulta podem precisar de tooload grandes quantidades de dados do nó principal do toohello Olá fragmentos e podem executar mal</span><span class="sxs-lookup"><span data-stu-id="897dd-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="897dd-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="897dd-188">Next steps</span></span>

* <span data-ttu-id="897dd-189">Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="897dd-190">Para obter um tutorial sobre particionamento vertical, veja [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="897dd-191">Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="897dd-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="897dd-192">Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="897dd-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="897dd-193">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="897dd-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
