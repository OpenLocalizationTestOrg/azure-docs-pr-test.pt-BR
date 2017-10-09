---
title: aaaQuery em nuvem bancos de dados com esquemas diferentes | Microsoft Docs
description: "como tooset as consultas de bancos de dados em partições verticais"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="f0fbc-103">Consultar entre bancos de dados na nuvem com esquemas diferentes (visualização)</span><span class="sxs-lookup"><span data-stu-id="f0fbc-103">Query across cloud databases with different schemas (preview)</span></span>
![Consultar tabelas em bancos de dados diferentes][1]

<span data-ttu-id="f0fbc-105">Bancos de dados particionados verticalmente usam diferentes conjuntos de tabelas diferentes bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="f0fbc-106">Isso significa que esse esquema Olá é diferente em bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="f0fbc-107">Por exemplo, todas as tabelas de inventário estão em um banco de dados, enquanto todas as tabelas relacionadas à contabilidade estão em um segundo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f0fbc-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f0fbc-108">Prerequisites</span></span>
* <span data-ttu-id="f0fbc-109">usuário Olá deve ter a permissão ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="f0fbc-110">Essa permissão é incluída com a permissão ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="f0fbc-111">Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="f0fbc-112">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f0fbc-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="f0fbc-113">Ao contrário de com o particionamento horizontal, essas instruções de DDL não dependem de definindo uma camada de dados com um mapa do fragmento pela biblioteca de cliente do banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="f0fbc-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="f0fbc-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="f0fbc-115">CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS</span><span class="sxs-lookup"><span data-stu-id="f0fbc-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="f0fbc-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="f0fbc-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="f0fbc-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="f0fbc-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="f0fbc-118">Criar chave mestra do escopo do banco de dados e credenciais</span><span class="sxs-lookup"><span data-stu-id="f0fbc-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="f0fbc-119">Olá credencial é usada pelo Olá consulta Elástico tooconnect tooyour bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="f0fbc-120">Certifique-se de que Olá `<username>` não incluir nenhum **"@servername"** sufixo.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="f0fbc-121">Criar fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="f0fbc-121">Create external data sources</span></span>
<span data-ttu-id="f0fbc-122">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="f0fbc-123">parâmetro de tipo Hello deve ser definido muito**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="f0fbc-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f0fbc-124">Example</span></span>
<span data-ttu-id="f0fbc-125">Olá, exemplo a seguir ilustra uso de saudação do hello instrução CREATE para fontes de dados externas.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="f0fbc-126">lista de saudação tooretrieve atual fontes de dados externas:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="f0fbc-127">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="f0fbc-127">External Tables</span></span>
<span data-ttu-id="f0fbc-128">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="f0fbc-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f0fbc-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="f0fbc-130">saudação de exemplo a seguir mostra como tooretrieve Olá lista de tabelas externas do banco de dados atual hello:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="f0fbc-131">Comentários</span><span class="sxs-lookup"><span data-stu-id="f0fbc-131">Remarks</span></span>
<span data-ttu-id="f0fbc-132">Consulta elástica estende Olá tabela externa sintaxe toodefine externo tabelas existentes que usam fontes de dados externas do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="f0fbc-133">Uma definição de tabela externa para o particionamento vertical abrange Olá aspectos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="f0fbc-134">**Esquema**: tabela externa de saudação DDL define um esquema que podem usar as consultas.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="f0fbc-135">esquema de saudação fornecida em sua definição de tabela externa deve toomatch esquema Olá tabelas Olá Olá banco de dados remoto onde os dados reais hello estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="f0fbc-136">**Referência de banco de dados remoto**: tabela externa de saudação DDL refere-se a fonte de dados externa tooan.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="f0fbc-137">fonte de dados externa Olá Especifica o nome de servidor lógico hello e nome de banco de dados do banco de dados remoto Olá onde são armazenados dados de tabela real hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="f0fbc-138">Tabelas externas do hello sintaxe toocreate usando uma fonte de dados externa, conforme descrito na seção anterior Olá, é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="f0fbc-139">cláusula DATA_SOURCE Olá define a fonte de dados externa da saudação (ou seja, Olá banco de dados remoto em caso de particionamento vertical) que é usado para a tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="f0fbc-140">cláusulas SCHEMA_NAME e OBJECT_NAME Olá fornecem Olá capacidade toomap Olá externo definição tooa tabela em um esquema diferente no banco de dados remoto hello, ou tooa tabela com um nome diferente, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="f0fbc-141">Isso é útil se você quiser toodefine uma exibição de catálogo tooa tabela externa ou DMV em seu banco de dados remoto - ou qualquer outra situação em que nome da tabela remota Olá já existe localmente.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="f0fbc-142">Olá instrução DDL a seguir descarta uma definição de tabela externa existente do catálogo local hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="f0fbc-143">Ele não afeta o banco de dados remoto hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="f0fbc-144">**Permissões para CREATE/DROP TABLE externo**: permissões ALTER ANY EXTERNAL DATA SOURCE são necessários para a tabela externa DDL que também é necessário toorefer toohello fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="f0fbc-145">Considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="f0fbc-145">Security considerations</span></span>
<span data-ttu-id="f0fbc-146">Os usuários com a tabela externa do acesso toohello automaticamente acessar tabelas remotas subjacentes de toohello na credencial Olá especificado na definição de fonte de dados externa hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="f0fbc-147">Você deve gerenciar cuidadosamente tabela externa do access toohello em ordem tooavoid maneira indesejada de elevação de privilégios por meio de credencial de saudação da fonte de dados externa hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="f0fbc-148">Regulares permissões do SQL podem ser usado tooGRANT ou tabela externa do REVOGAR acesso tooan como se fosse uma tabela normal.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="f0fbc-149">Exemplo: consultando bancos de dados particionados verticalmente</span><span class="sxs-lookup"><span data-stu-id="f0fbc-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="f0fbc-150">Olá consulta a seguir executa uma junção de três vias entre duas tabelas locais Olá para pedidos e linhas de ordem e tabela remota Olá para clientes.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="f0fbc-151">Este é um exemplo de caso de uso de dados de referência de Olá para consulta Elástico:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-151">This is an example of hello reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="f0fbc-152">Procedimento armazenado para a execução remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="f0fbc-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="f0fbc-153">Consulta elástica também apresenta um procedimento armazenado que fornece acesso direto toohello fragmentos.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="f0fbc-154">Olá procedimento armazenado é chamado [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) e pode ser usado tooexecute procedimentos armazenados ou código T-SQL em bancos de dados remotos hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="f0fbc-155">Ele usa Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="f0fbc-156">Nome da fonte de dados (nvarchar): nome de saudação da fonte de dados externa de saudação do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="f0fbc-157">Consulta (nvarchar): toobe de consulta Olá T-SQL executado em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="f0fbc-158">Declaração de parâmetro (nvarchar) - opcional: cadeia de caracteres com definições de tipo de dados para parâmetros de saudação usadas no parâmetro de consulta de saudação (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="f0fbc-159">Lista de valores de parâmetro - opcional: lista separada por vírgulas de valores de parâmetro (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="f0fbc-160">Olá sp\_executar\_remota usa Olá fornecida na seguinte instrução T-SQL em bancos de dados remotos Olá Olá invocação parâmetros tooexecute Olá de fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="f0fbc-161">Ele usa credenciais Olá Olá dados externos fonte tooconnect toohello shardmap manager banco de dados e bancos de dados remotos hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="f0fbc-162">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0fbc-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="f0fbc-163">Conectividade de ferramentas</span><span class="sxs-lookup"><span data-stu-id="f0fbc-163">Connectivity for tools</span></span>
<span data-ttu-id="f0fbc-164">Você pode usar tooconnect regular de cadeias de caracteres de conexão do SQL Server seu toodatabases de ferramentas de integração de BI e os dados no servidor de banco de dados SQL Olá com consulta elástica habilitado e tabelas externas definidas.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="f0fbc-165">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="f0fbc-166">Em seguida, consulte banco de dados de consulta Elástico toohello e suas tabelas externas, assim como quaisquer outros dados do SQL Server se conectaria toowith sua ferramenta.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="f0fbc-167">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="f0fbc-167">Best practices</span></span>
* <span data-ttu-id="f0fbc-168">Certifique-se de que esse banco de dados do ponto de extremidade de consulta Elástico Olá tem banco de dados do access toohello remoto por habilitar o acesso de serviços do Azure em sua configuração de firewall do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="f0fbc-169">Também verifique se essa credencial Olá fornecido em dados externos Olá definição de fonte pode fazer logon no banco de dados remoto hello e tem a tabela remota do Olá Olá permissões tooaccess.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="f0fbc-170">Consulta elástica funciona melhor para consultas onde a maioria de computação Olá pode ser feita em bancos de dados remotos hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="f0fbc-171">Você normalmente obtém o melhor desempenho de consulta Olá com predicados de filtro seletivo que pode ser avaliada em bancos de dados remotos hello ou junções que podem ser executadas completamente no banco de dados remoto hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="f0fbc-172">Outros padrões de consulta podem precisar de tooload grandes quantidades de dados do banco de dados remoto hello e podem executar baixo desempenho.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f0fbc-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0fbc-173">Next steps</span></span>

* <span data-ttu-id="f0fbc-174">Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="f0fbc-175">Para obter um tutorial sobre particionamento vertical, consulte [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="f0fbc-176">Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="f0fbc-177">Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="f0fbc-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="f0fbc-178">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
