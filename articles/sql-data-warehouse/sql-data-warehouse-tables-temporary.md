---
title: "Tabelas temporárias no SQL Data Warehouse | Microsoft Docs"
description: "Introdução às tabelas temporárias no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="72355-103">Tabelas temporárias no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="72355-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="72355-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="72355-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="72355-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="72355-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="72355-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="72355-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="72355-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="72355-107">[Index][Index]</span></span>
> * <span data-ttu-id="72355-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="72355-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="72355-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="72355-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="72355-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="72355-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="72355-111">As tabelas temporárias são muito úteis durante o processamento de dados - especialmente durante a transformação onde os resultados intermediários são temporários.</span><span class="sxs-lookup"><span data-stu-id="72355-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="72355-112">No SQL Data Warehouse, existem tabelas temporárias no nível de sessão.</span><span class="sxs-lookup"><span data-stu-id="72355-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="72355-113">Elas são visíveis apenas para a sessão na qual foram criadas e são descartadas automaticamente quando a sessão faz logoff.</span><span class="sxs-lookup"><span data-stu-id="72355-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="72355-114">As tabelas temporárias oferecem um benefício de desempenho, pois seus resultados são gravados no local, em vez do armazenamento remoto.</span><span class="sxs-lookup"><span data-stu-id="72355-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="72355-115">As tabelas temporárias são um pouco diferentes no Azure SQL Data Warehouse em relação ao Banco de Dados SQL porque elas podem ser acessadas de qualquer lugar na sessão, incluindo dentro e fora de um procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="72355-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="72355-116">Este artigo contém as diretrizes essenciais de como usar as tabelas temporárias e destaca os princípios das tabelas temporárias no nível da sessão.</span><span class="sxs-lookup"><span data-stu-id="72355-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="72355-117">Usar as informações neste artigo pode ajudá-lo a modularizar seu código, melhorando a reutilização e a facilidade de manutenção do seu código.</span><span class="sxs-lookup"><span data-stu-id="72355-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="72355-118">Criar uma tabela temporária</span><span class="sxs-lookup"><span data-stu-id="72355-118">Create a temporary table</span></span>
<span data-ttu-id="72355-119">As tabelas temporárias são criadas simplesmente prefixando o nome da tabela com `#`.</span><span class="sxs-lookup"><span data-stu-id="72355-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="72355-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="72355-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="72355-121">As tabelas temporárias também podem ser criadas usando `CTAS` com a mesma abordagem:</span><span class="sxs-lookup"><span data-stu-id="72355-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="72355-122">`CTAS` é um comando bastante potente e tem a vantagem extra de ser muito eficiente em seu uso do espaço de log das transações.</span><span class="sxs-lookup"><span data-stu-id="72355-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="72355-123">Descartando tabelas temporárias</span><span class="sxs-lookup"><span data-stu-id="72355-123">Dropping temporary tables</span></span>
<span data-ttu-id="72355-124">Quando uma nova sessão é criada, não deve haver nenhuma tabela temporária.</span><span class="sxs-lookup"><span data-stu-id="72355-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="72355-125">No entanto, se você estiver chamando o mesmo procedimento armazenado, que cria um temporário com o mesmo nome, para garantir que suas instruções `CREATE TABLE` sejam bem-sucedidas, uma simples verificação da existência com `DROP` pode ser usada como no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="72355-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="72355-126">Para a consistência da codificação, é recomendável usar esse padrão para as tabelas e as tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="72355-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="72355-127">Também é uma boa prática usar `DROP TABLE` para remover as tabelas temporárias quando você tiver terminado o trabalho com elas no código.</span><span class="sxs-lookup"><span data-stu-id="72355-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="72355-128">No desenvolvimento de procedimento armazenado, é bastante comum ver os comandos de remoção agrupados no fim de um procedimento para garantir que esses objetos sejam limpos.</span><span class="sxs-lookup"><span data-stu-id="72355-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="72355-129">Modularizar o código</span><span class="sxs-lookup"><span data-stu-id="72355-129">Modularizing code</span></span>
<span data-ttu-id="72355-130">Como as tabelas temporárias podem ser vistas em qualquer lugar em uma sessão do usuário, isso pode ser explorado para ajudá-lo a modularizar o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72355-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="72355-131">Por exemplo, o procedimento armazenado a seguir reúne as práticas recomendadas acima para gerar a DDL que atualizará todas as estatísticas no banco de dados pelo nome da estatística.</span><span class="sxs-lookup"><span data-stu-id="72355-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="72355-132">Neste estágio, a única ação que ocorreu é a criação de um procedimento armazenado que simplesmente irá gerar uma tabela temporária, #stats_ddl, com instruções DDL.</span><span class="sxs-lookup"><span data-stu-id="72355-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="72355-133">Esse procedimento armazenado descartará #stats_ddl se ela já existir para garantir que não falhará se for executada mais de uma vez em uma sessão.</span><span class="sxs-lookup"><span data-stu-id="72355-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="72355-134">No entanto, já que não há nenhum `DROP TABLE` no final do procedimento armazenado, quando o procedimento armazenado for concluído, ele deixará a tabela criada para que possa ser lida de fora do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="72355-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="72355-135">No SQL Data Warehouse, ao contrário dos outros bancos de dados do SQL Server, é possível usar a tabela temporária fora do procedimento que a criou.</span><span class="sxs-lookup"><span data-stu-id="72355-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="72355-136">As tabelas temporárias do SQL Data Warehouse podem ser usadas **em qualquer lugar** na sessão.</span><span class="sxs-lookup"><span data-stu-id="72355-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="72355-137">Isso pode levar a um código mais modular e gerenciável, como no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="72355-137">This can lead to more modular and manageable code as in the below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="72355-138">Limitações da tabela temporária</span><span class="sxs-lookup"><span data-stu-id="72355-138">Temporary table limitations</span></span>
<span data-ttu-id="72355-139">O SQL Data Warehouse impõe algumas limitações ao implementar a tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="72355-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="72355-140">Atualmente, somente a sessão com o escopo das tabelas temporárias é suportada.</span><span class="sxs-lookup"><span data-stu-id="72355-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="72355-141">Não há suporte para as Tabelas Temporárias Globais.</span><span class="sxs-lookup"><span data-stu-id="72355-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="72355-142">E mais, as exibições não podem ser criadas nas tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="72355-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72355-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72355-143">Next steps</span></span>
<span data-ttu-id="72355-144">Para saber mais, consulte os artigos [Table Overview][Overview] (Visão Geral da Tabela), [Table Data Types][Data Types] (Tipos de Dados da Tabela), [Distributing a Table][Distribute] (Distribuir uma Tabela), [Indexing a Table][Index] (Indexar uma Tabela), [Partitioning a Table][Partition] (Particionar uma Tabela) e [Maintaining Table Statistics][Statistics] (Manter Estatísticas de Tabela).</span><span class="sxs-lookup"><span data-stu-id="72355-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="72355-145">Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="72355-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
