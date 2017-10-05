---
title: Consulta entre bancos de dados na nuvem com esquemas diferentes | Microsoft Docs
description: "como configurar consultas entre bancos de dados em partições verticais"
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
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="d9363-103">Consultar entre bancos de dados na nuvem com esquemas diferentes (visualização)</span><span class="sxs-lookup"><span data-stu-id="d9363-103">Query across cloud databases with different schemas (preview)</span></span>
![Consultar tabelas em bancos de dados diferentes][1]

<span data-ttu-id="d9363-105">Bancos de dados particionados verticalmente usam diferentes conjuntos de tabelas diferentes bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d9363-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="d9363-106">Isso significa que o esquema é diferente em bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="d9363-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="d9363-107">Por exemplo, todas as tabelas de inventário estão em um banco de dados, enquanto todas as tabelas relacionadas à contabilidade estão em um segundo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d9363-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d9363-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9363-108">Prerequisites</span></span>
* <span data-ttu-id="d9363-109">O usuário deve ter a permissão para ALTERAR QUALQUER FONTE DE DADOS EXTERNA.</span><span class="sxs-lookup"><span data-stu-id="d9363-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="d9363-110">Essa permissão está incluída na permissão ALTERAR BANCO DE DADOS.</span><span class="sxs-lookup"><span data-stu-id="d9363-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="d9363-111">As permissões para ALTERAR QUALQUER FONTE DE DADOS EXTERNA são necessárias para referenciar a fonte de dados subjacente.</span><span class="sxs-lookup"><span data-stu-id="d9363-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="d9363-112">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d9363-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="d9363-113">Ao contrário do particionamento horizontal, essas instruções DDL não dependem da definição de uma camada de dados com um mapa de fragmentos por meio da biblioteca de cliente do banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="d9363-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="d9363-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="d9363-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="d9363-115">CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS</span><span class="sxs-lookup"><span data-stu-id="d9363-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="d9363-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="d9363-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="d9363-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="d9363-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="d9363-118">Criar chave mestra do escopo do banco de dados e credenciais</span><span class="sxs-lookup"><span data-stu-id="d9363-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="d9363-119">A credencial é usada pela consulta elástica para se conectar aos bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="d9363-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="d9363-120">Verifique se o `<username>` não inclui nenhum sufixo **"@servername"**.</span><span class="sxs-lookup"><span data-stu-id="d9363-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="d9363-121">Criar fontes de dados externas</span><span class="sxs-lookup"><span data-stu-id="d9363-121">Create external data sources</span></span>
<span data-ttu-id="d9363-122">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="d9363-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="d9363-123">O parâmetro TYPE deve ser definido como **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="d9363-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="d9363-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d9363-124">Example</span></span>
<span data-ttu-id="d9363-125">O exemplo a seguir ilustra o uso da instrução CRIAR para fontes de dados externas.</span><span class="sxs-lookup"><span data-stu-id="d9363-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="d9363-126">Para recuperar a lista de fontes de dados externas atuais:</span><span class="sxs-lookup"><span data-stu-id="d9363-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="d9363-127">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="d9363-127">External Tables</span></span>
<span data-ttu-id="d9363-128">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="d9363-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="d9363-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d9363-129">Example</span></span>
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

<span data-ttu-id="d9363-130">O exemplo a seguir mostra como recuperar a lista de tabelas externas do banco de dados atual:</span><span class="sxs-lookup"><span data-stu-id="d9363-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="d9363-131">Comentários</span><span class="sxs-lookup"><span data-stu-id="d9363-131">Remarks</span></span>
<span data-ttu-id="d9363-132">A consulta elástica estende a sintaxe de tabela externa existente para definir as tabelas externas que usam fontes de dados externas do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="d9363-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="d9363-133">Uma definição de tabela externa para o particionamento vertical abrange os seguintes aspectos:</span><span class="sxs-lookup"><span data-stu-id="d9363-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="d9363-134">**Esquema**: a DDL da tabela externa define um esquema que pode ser usado pelas consultas.</span><span class="sxs-lookup"><span data-stu-id="d9363-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="d9363-135">O esquema fornecido na definição da tabela externa precisa corresponder ao esquema das tabelas no banco de dados remoto em que os dados reais são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d9363-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="d9363-136">**Referência de banco de dados remoto**: a DDL da tabela externa faz referência a uma fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="d9363-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="d9363-137">A fonte de dados externa especifica o nome do servidor lógico e o nome do banco de dados remoto em que os dados da tabela real estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="d9363-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="d9363-138">Com uma fonte de dados externa, como descrito na seção anterior, a sintaxe para criar tabelas externas é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="d9363-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="d9363-139">A cláusula DATA_SOURCE define a fonte de dados externa (ou seja, o banco de dados remoto, no caso do particionamento vertical) que é usada para a tabela externa.</span><span class="sxs-lookup"><span data-stu-id="d9363-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="d9363-140">As cláusulas SCHEMA_NAME e OBJECT_NAME fornecem a capacidade de mapear a definição da tabela externa para uma tabela em um esquema diferente no banco de dados remoto ou para uma tabela com um nome diferente, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d9363-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="d9363-141">Isso será útil se você quiser definir uma tabela externa para uma exibição de catálogo ou DMV em seu banco de dados remoto – ou em qualquer outra situação em que o nome da tabela remota já esteja sendo usado localmente.</span><span class="sxs-lookup"><span data-stu-id="d9363-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="d9363-142">A instrução DDL a seguir remove uma definição existente da tabela externa do catálogo do local.</span><span class="sxs-lookup"><span data-stu-id="d9363-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="d9363-143">Ela não afeta o banco de dados remoto.</span><span class="sxs-lookup"><span data-stu-id="d9363-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="d9363-144">**Permissões para CREATE/DROP EXTERNAL TABLE**: as permissões ALTER ANY EXTERNAL DATA SOURCE são necessárias para a DDL da tabela externa, o que também é necessário para fazer referência à fonte de dados subjacente.</span><span class="sxs-lookup"><span data-stu-id="d9363-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="d9363-145">Considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="d9363-145">Security considerations</span></span>
<span data-ttu-id="d9363-146">Usuários com acesso à tabela externa têm acesso automaticamente a tabelas remotas subjacentes com a credencial fornecida na definição de fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="d9363-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="d9363-147">Você deve gerenciar cuidadosamente o acesso à tabela externa para evitar a elevação indesejada de privilégios por meio da credencial da fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="d9363-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="d9363-148">Permissões de SQL regulares podem ser usadas para o acesso de GRANT ou REVOKE a uma tabela externa como se ela fosse uma tabela normal.</span><span class="sxs-lookup"><span data-stu-id="d9363-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="d9363-149">Exemplo: consultando bancos de dados particionados verticalmente</span><span class="sxs-lookup"><span data-stu-id="d9363-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="d9363-150">A consulta a seguir executa uma junção de três vias entre as duas tabelas locais para pedidos e linhas da pedido e a tabela remota para clientes.</span><span class="sxs-lookup"><span data-stu-id="d9363-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="d9363-151">Este é um exemplo do caso de uso de dados de referência para a consulta elástica:</span><span class="sxs-lookup"><span data-stu-id="d9363-151">This is an example of the reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="d9363-152">Procedimento armazenado para a execução remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="d9363-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="d9363-153">A consulta elástica também apresenta um procedimento armazenado que fornece acesso direto aos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="d9363-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="d9363-154">O procedimento armazenado é chamado [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) e pode ser usado para executar procedimentos armazenados remotos ou código T-SQL em bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="d9363-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="d9363-155">Ele usa os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d9363-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="d9363-156">Nome da fonte de dados (nvarchar): o nome da fonte de dados externa do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="d9363-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="d9363-157">Consulta (nvarchar): a consulta T-SQL a ser executada em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="d9363-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="d9363-158">Declaração de parâmetro (nvarchar) - opcional: cadeia de caracteres com definições de tipo de dados para os parâmetros usados no parâmetro Query (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="d9363-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="d9363-159">Lista de valores de parâmetro - opcional: lista separada por vírgulas de valores de parâmetro (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="d9363-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="d9363-160">O sp\_execute\_remote usa a fonte de dados externa fornecida nos parâmetros de invocação para executar a instrução T-SQL especificada nos bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="d9363-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="d9363-161">Ele usa a credencial da fonte de dados externa para a conexão com o banco de dados do gerenciador de mapa do fragmento e bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="d9363-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="d9363-162">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="d9363-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="d9363-163">Conectividade de ferramentas</span><span class="sxs-lookup"><span data-stu-id="d9363-163">Connectivity for tools</span></span>
<span data-ttu-id="d9363-164">É possível usar cadeias de conexão regulares do SQL Server para conectar suas ferramentas de BI e de integração de dados a bancos de dados no servidor do Banco de Dados SQL que têm a consulta elástica habilitada e as tabelas externas definidas.</span><span class="sxs-lookup"><span data-stu-id="d9363-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="d9363-165">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="d9363-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="d9363-166">Em seguida, consulte o banco de dados de consulta elástica e suas tabelas externas como qualquer outro banco de dados do SQL Server ao qual você se conectaria com a sua ferramenta.</span><span class="sxs-lookup"><span data-stu-id="d9363-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="d9363-167">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="d9363-167">Best practices</span></span>
* <span data-ttu-id="d9363-168">Verifique se o banco de dados do ponto de extremidade da consulta elástica recebeu acesso ao banco de dados remoto habilitando acesso para os Serviços do Azure em sua configuração de firewall do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d9363-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="d9363-169">Também verifique se a credencial fornecida na definição da fonte de dados externa pode fazer logon com êxito no banco de dados remoto e se ela tem as permissões para acessar a tabela remota.</span><span class="sxs-lookup"><span data-stu-id="d9363-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="d9363-170">A consulta elástica funciona melhor para consultas em que a maior parte da computação pode ser realizada nos bancos de dados remotos.</span><span class="sxs-lookup"><span data-stu-id="d9363-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="d9363-171">Normalmente, você obtém o melhor desempenho de consulta com predicados de filtro seletivo que podem ser avaliados nos bancos de dados remotos ou com junções que podem ser executadas por completo no banco de dados remoto.</span><span class="sxs-lookup"><span data-stu-id="d9363-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="d9363-172">Outros padrões de consulta podem precisar carregar grandes quantidades de dados do banco de dados remoto e podem ter um desempenho insatisfatório.</span><span class="sxs-lookup"><span data-stu-id="d9363-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d9363-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9363-173">Next steps</span></span>

* <span data-ttu-id="d9363-174">Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9363-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="d9363-175">Para obter um tutorial sobre particionamento vertical, consulte [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="d9363-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="d9363-176">Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9363-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="d9363-177">Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d9363-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="d9363-178">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="d9363-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
