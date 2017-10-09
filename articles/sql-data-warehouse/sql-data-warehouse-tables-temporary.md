---
title: tabelas de aaaTemporary no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a>Tabelas temporárias no SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Tipos de Dados][Data Types]
> * [Distribuir][Distribute]
> * [Índice][Index]
> * [Partição][Partition]
> * [Estatísticas][Statistics]
> * [Temporário][Temporary]
> 
> 

Tabelas temporárias são muito úteis durante o processamento de dados - especialmente durante a transformação onde os resultados intermediários de saudação são transitórios. No SQL Data Warehouse tabelas temporárias existem no nível de sessão hello.  Eles são apenas visíveis toohello sessão na qual eles foram criados e são automaticamente descartados quando a sessão faz logoff.  Tabelas temporárias oferecem uma vantagem de desempenho porque os resultados são gravados toolocal em vez de armazenamento remoto.  Tabelas temporárias são um pouco diferentes no Azure SQL Data Warehouse do banco de dados do SQL Azure, como eles podem ser acessados de qualquer lugar dentro da sessão de hello, incluindo dentro e fora de um procedimento armazenado.

Este artigo contém diretrizes essenciais para o uso de tabelas temporárias e realça os princípios de saudação de tabelas temporárias nível de sessão. Usando informações de saudação neste artigo pode ajudá-lo a modularizar seu código, melhorando a capacidade de reutilização e facilidade de manutenção do seu código.

## <a name="create-a-temporary-table"></a>Criar uma tabela temporária
As tabelas temporárias são criadas simplesmente prefixando o nome da tabela com `#`.  Por exemplo:

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

Tabelas temporárias também podem ser criadas com um `CTAS` usando Olá exatamente a mesma abordagem:

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
> `CTAS`é um comando muito poderoso e Olá adicionou vantagem de ser muito eficientes no uso do espaço de log de transações. 
> 
> 

## <a name="dropping-temporary-tables"></a>Descartando tabelas temporárias
Quando uma nova sessão é criada, não deve haver nenhuma tabela temporária.  No entanto, se você estiver chamando Olá mesmo procedimento armazenado, que cria um temporário com hello mesmo nome, tooensure que seu `CREATE TABLE` instruções forem bem-sucedidas uma verificação de pré-existência simples com um `DROP` pode ser usado como Olá exemplo abaixo:

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

Para codificar a consistência, é uma boa prática toouse esse padrão para tabelas e tabelas temporárias.  Também é uma boa ideia toouse `DROP TABLE` tooremove as tabelas temporárias quando terminar com-los em seu código.  No desenvolvimento de um procedimento armazenado é bastante comum toosee Olá comandos drop agrupados no final de saudação de um procedimento tooensure que esses objetos são limpos.

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>Modularizar o código
Como tabelas temporárias podem ser vistas em qualquer lugar em uma sessão de usuário, isso pode ser explorado toohelp modularizar código do aplicativo.  Por exemplo, hello abaixo do procedimento armazenado une Olá práticas acima toogenerate DDL que atualizará todas as estatísticas no banco de dados de saudação recomendada pelo nome da estatística.

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

Neste estágio a Olá única ação que ocorreu é a criação de saudação de um procedimento armazenado que será gerado simplesmente uma tabela temporária, #stats_ddl, com instruções DDL.  Esse procedimento armazenado removerá #stats_ddl se ele já existe tooensure não falha se executar mais de uma vez dentro de uma sessão.  No entanto, como não há nenhum `DROP TABLE` no final de saudação do procedimento armazenado de hello, quando hello procedimento armazenado é concluído, ele deixará tabela Olá criado para que ele possa ser lido fora do procedimento armazenado de saudação.  No SQL Data Warehouse, ao contrário de outros bancos de dados do SQL Server, é possível toouse Olá temporário tabela fora do procedimento de saudação que criou.  Tabelas temporárias do SQL Data Warehouse podem ser usadas **em qualquer lugar** Olá sessão. Isso pode gerar o código modular e gerenciável toomore como Olá exemplo abaixo:

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

## <a name="temporary-table-limitations"></a>Limitações da tabela temporária
O SQL Data Warehouse impõe algumas limitações ao implementar a tabelas temporárias.  Atualmente, somente a sessão com o escopo das tabelas temporárias é suportada.  Não há suporte para as Tabelas Temporárias Globais.  E mais, as exibições não podem ser criadas nas tabelas temporárias.

## <a name="next-steps"></a>Próximas etapas
toolearn mais, consulte os artigos de saudação em [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Indexando uma tabela][Index], [particionar uma tabela] [ Partition] e [ Manter estatísticas de tabela][Statistics].  Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
