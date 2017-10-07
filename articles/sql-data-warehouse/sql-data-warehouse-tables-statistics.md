---
title: "aaaManaging estatísticas em tabelas no Data Warehouse SQL | Microsoft Docs"
description: "Introdução às estatísticas em tabelas no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Gerenciamento de estatísticas em tabelas no SQL Data Warehouse
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

Hello mais SQL Data Warehouse sabe sobre seus dados, hello mais rápido ele poderá executar consultas em relação aos dados.  Olá maneira que indicam o SQL Data Warehouse sobre seus dados, é coletar estatísticas sobre os dados.  Têm estatísticas em seus dados é uma das coisas mais importantes Olá você pode fazer toooptimize suas consultas.  Estatísticas ajudam SQL Data Warehouse criar Olá o plano ideal de suas consultas.  Isso ocorre porque a consulta do SQL Data Warehouse Olá otimizador tem um custo com base em otimizador.  Ou seja, ele compara o custo de saudação de vários planos de consulta e então escolhe Olá plano com hello menor custo, que também deve ser o plano de saudação que executará hello mais rápido.

As estatísticas podem ser criadas em uma única coluna, várias colunas ou em um índice de uma tabela.  As estatísticas são armazenadas em um histograma que captura o intervalo de saudação e a seletividade dos valores.  Isso é de particular interesse quando as necessidades de otimizador Olá tooevaluate junções, GROUP BY, HAVING e cláusulas WHERE em uma consulta.  Por exemplo, se o otimizador Olá estima que date de hello você está filtrando em sua consulta retornará 1 linha, ele pode escolher um diferentes planejar que se ele estimativas que data você selecionou irá retornar 1 milhão de linhas.  Durante a criação de estatísticas é extremamente importante, é igualmente importante que estatísticas *com precisão* refletem Olá o estado atual da tabela de saudação.  Com estatísticas atualizadas, você garante que um bom plano é selecionado pelo otimizador hello.  planos de saudação criados pelo otimizador Olá só são tão boas quanto as estatísticas de saudação em seus dados.

processo de saudação de criação e atualização de estatísticas é atualmente um processo manual, mas é toodo muito simple.  Isso é diferente do SQL Server, que cria e atualiza automaticamente as estatísticas em colunas e índices únicos.  Usando informações de saudação abaixo, você pode automatizar muito gerenciamento Olá de estatísticas de saudação em seus dados. 

## <a name="getting-started-with-statistics"></a>Introdução às estatísticas
 Criando estatísticas por amostra em cada coluna é uma maneira fácil tooget iniciado com estatísticas.  Como é igualmente importante tookeep estatísticas atualizadas, uma abordagem conservadora pode ser tooupdate estatísticas diariamente ou após cada carga. Sempre há compensações entre desempenho e Olá custo toocreate e atualizar as estatísticas.  Se você achar que está levando muito toomaintain todas as estatísticas, convém tootry toobe mais seletivo sobre as colunas que têm estatísticas ou as colunas que precisa frequentes de atualização.  Por exemplo, convém colunas de data tooupdate diariamente, conforme novos valores podem ser adicionados em vez de após cada carga. Novamente, você obterá Olá maior benefício fazendo com que as estatísticas em colunas envolvidas em junções, GROUP BY, HAVING e cláusulas WHERE.  Se você tiver uma tabela com uma grande quantidade de cláusula SELECT de colunas que são usadas somente em hello, estatísticas nessas colunas não podem ajudar e gastos um pouco mais tooidentify de esforço somente colunas Olá onde as estatísticas serão útil, pode reduzir Olá tempo toomaintain estatísticas .

## <a name="multi-column-statistics"></a>Estatísticas de várias colunas
Além disso toocreating estatísticas em colunas únicas, você pode achar que suas consultas se beneficiam de estatísticas de várias colunas.  Estatísticas de várias colunas são estatísticas criadas em uma lista de colunas.  Elas incluem estatísticas de coluna única na primeira coluna de saudação na lista hello, além de algumas informações de correlação entre colunas chamado densidades.  Por exemplo, se você tiver uma tabela que une tooanother em duas colunas, você pode achar que SQL Data Warehouse poderá otimizar melhor plano de saudação que ele entenda a relação de saudação entre duas colunas.   As estatísticas de várias colunas podem melhorar o desempenho de consulta de algumas operações como junções compostas e agrupar por.

## <a name="updating-statistics"></a>Atualização de estatísticas
Atualizar as estatísticas é uma parte importante de sua rotina de gerenciamento de banco de dados.  Quando altera a distribuição de saudação de dados no banco de dados de saudação, estatísticas necessário toobe atualizado.  As estatísticas desatualizadas levará o desempenho ideal de toosub de consulta.

Uma prática recomendada é tooupdate estatísticas em colunas de data por dia à medida que novas datas são adicionadas.  Cada novas linhas de tempo são carregados no data warehouse de hello, datas de carga novo ou transação são adicionados. Esses alteram Olá distribuição de dados e faça estatísticas Olá desatualizadas. Por outro lado, as estatísticas em uma coluna de país em uma tabela de cliente nunca talvez seja necessário toobe atualizado, como a distribuição de saudação de valores geralmente não são alterados. Supondo que a distribuição de saudação é constante entre os clientes, adicionar nova variação de tabela toohello linhas não vai toochange a distribuição de dados hello. No entanto, se o data warehouse contém apenas um país e você exibir dados de um país, resultando em dados de vários países que estão sendo armazenados, definitivamente necessário tooupdate estatísticas na coluna de país hello.

Uma saudação primeiro perguntas tooask quando uma consulta de solução de problemas, "são Olá estatísticas atualizadas?"

Essa pergunta não é aquele que podem ser respondidas por idade Olá dos dados de saudação. Um objeto de estatísticas toodate backup pode ser muito antigo se não houve nenhuma toohello alteração material dados subjacentes. Quando Olá número de linhas alterado substancialmente ou há uma alteração material na distribuição de saudação de valores para uma determinada coluna *, em seguida,* é tooupdate das estatísticas.  

Para referência, o **SQL Server** (não o SQL Data Warehouse) atualiza automaticamente as estatísticas para estas situações:

* Se você tiver zero linhas na tabela hello, quando você adiciona linhas, você obterá uma atualização automática de estatísticas
* Quando você adiciona a tabela de tooa mais de 500 linhas começando com menos de 500 linhas (por exemplo, no início você tiver 499 e, em seguida, adicione 500 linhas tooa totalizando 999 linhas), você receberá uma atualização automática 
* Quando tiver mais de 500 linhas terá tooadd 500 linhas adicionais + 20% do tamanho de saudação da tabela Olá antes de você verá uma atualização automática em estatísticas de saudação

Como não há nenhum toodetermine DMV se os dados na tabela de saudação foi alterado desde Olá últimas estatísticas de tempo foram atualizadas, saber a idade de saudação de estatísticas pode fornecer com parte da imagem de saudação.  Você pode usar o hello toodetermine Olá última vez em que as estatísticas de consulta a seguir onde atualizado em cada tabela.  

> [!NOTE]
> Lembre-se de que se houver uma alteração substancial na distribuição de saudação de valores para uma determinada coluna, você deve atualizar as estatísticas independentemente Olá a última vez em que eles foram atualizados.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

As colunas de data em um data warehouse, por exemplo, normalmente precisam de atualizações frequentes de estatísticas. Cada novas linhas de tempo são carregados no data warehouse de hello, datas de carga novo ou transação são adicionados. Esses alteram Olá distribuição de dados e faça estatísticas Olá desatualizadas.  Por outro lado, as estatísticas em uma coluna de gênero em uma tabela de cliente nunca talvez seja necessário toobe atualizado. Supondo que a distribuição de saudação é constante entre os clientes, adicionar nova variação de tabela toohello linhas não vai toochange a distribuição de dados hello. No entanto, se o data warehouse contém apenas um sexo e uma nova resulta de requisito em vários gêneros, definitivamente necessário tooupdate estatísticas na coluna de sexo hello.

Para obter mais explicações, veja [Estatísticas][Statistics] no MSDN.

## <a name="implementing-statistics-management"></a>Implementação do gerenciamento de estatísticas
Geralmente é uma boa ideia tooextend seus dados ao carregar tooensure de processo que as estatísticas são atualizadas no hello fim do carregamento de saudação. saudação de carga de dados é quando tabelas com mais frequência alterar seu tamanho e/ou sua distribuição de valores. Portanto, este é um lugar lógico tooimplement alguns processos de gerenciamento.

Para atualizar as estatísticas durante o processo de carregamento hello, alguns princípios são fornecidos abaixo:

* Certifique-se de que cada tabela carregada tenha pelo menos um objeto de estatísticas atualizado. Este Olá atualizações tabelas informações de tamanho (contagem de linha e página) como parte da atualização de estatísticas de saudação.
* Concentre-se em colunas que participam de cláusulas JOIN, GROUP BY, ORDER BY e DISTINCT
* Considere atualizar "crescente chave" colunas, como transações mais frequentemente esses valores não serão incluídos no histograma de estatísticas de saudação datas.
* Considere atualizar as colunas de distribuição estática com menos frequência.
* Lembre-se de que cada objeto de estatística é atualizado em série. Simplesmente implementar `UPDATE STATISTICS <TABLE_NAME>` talvez não seja ideal, especialmente para tabelas mais amplas com muitos objetos de estatísticas.

> [!NOTE]
> Para obter mais detalhes sobre [crescente chave] consulte o white paper de modelo de estimativa de cardinalidade toohello SQL Server 2014.
> 
> 

Para obter mais explicações, veja [Estimativa de cardinalidade][Cardinality Estimation] no MSDN.

## <a name="examples-create-statistics"></a>Exemplos: criar estatísticas
Estes exemplos mostram como toouse várias opções para a criação de estatísticas. Opções de saudação que você usa para cada coluna dependem de como Olá coluna será usada em consultas e características de saudação de seus dados.

### <a name="a-create-single-column-statistics-with-default-options"></a>R. Criar estatísticas de coluna única com opções padrão
toocreate estatísticas em uma coluna, basta fornecer um nome de objeto de estatísticas de saudação e saudação da coluna de saudação.

Essa sintaxe usa todas as opções padrão de saudação. Por padrão, o SQL Data Warehouse amostras 20 por cento da tabela de saudação ao criar estatísticas.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Por exemplo:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Criar estatísticas de coluna única examinando cada linha
taxa de amostragem saudação padrão de 20% é suficiente para a maioria das situações. No entanto, você pode ajustar a taxa de amostragem de saudação.

saudação de toosample completa da tabela, use a seguinte sintaxe:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Por exemplo:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Criar estatísticas de coluna única, especificando o tamanho do exemplo hello
Como alternativa, você pode especificar o tamanho do exemplo hello como uma porcentagem:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Criar estatísticas de coluna única em apenas algumas das linhas de saudação
Outra opção, você pode criar estatísticas em uma parte das linhas de saudação em sua tabela. Isso é chamado de estatística filtrada.

Por exemplo, você pode usar as estatísticas filtradas quando você planejar tooquery uma partição específica de uma grande tabela particionada. Ao criar estatísticas em Olá somente valores de partição, precisão de saudação das estatísticas de saudação melhorar e, portanto, melhorar o desempenho da consulta.

Este exemplo cria estatísticas em um intervalo de valores. valores Hello facilmente podem ser definido pelo intervalo de saudação toomatch de valores em uma partição.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Para Olá tooconsider de Otimizador de consulta usando estatísticas filtradas quando escolhe um plano de consulta distribuída hello, consulta Olá deve se ajustar dentro definição Olá Olá do objeto de estatísticas. Usando o exemplo anterior hello, Olá da consulta em que a cláusula precisa toospecify col1 valores entre 2000101 e 20001231.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Criar estatísticas de coluna única com todas as opções de saudação
Naturalmente, você pode combinar as opções de saudação juntos. exemplo Hello abaixo cria um objeto de estatísticas filtradas com um tamanho de amostra personalizado:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Para obter referência completa hello, consulte [CREATE STATISTICS] [ CREATE STATISTICS] no MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Criar estatísticas de várias colunas
toocreate estatísticas de várias colunas, simplesmente use exemplos anteriores hello, mas especificar mais colunas.

> [!NOTE]
> histograma Hello, que é usada tooestimate o número de linhas no resultado de consulta hello, só está disponível para Olá primeira coluna listada na definição de objeto de estatísticas de saudação.
> 
> 

Neste exemplo, o histograma hello está em *produto\_categoria*. As estatísticas entre colunas são calculadas em *product\_category* e *product\_sub_c\ategory*:

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Como há uma correlação entre *produto\_categoria* e *produto\_sub\_categoria*, um estado de várias coluna pode ser útil se essas colunas são acessadas em Olá simultaneamente.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Criar estatísticas em todas as colunas de saudação em uma tabela
Estatísticas de uma maneira toocreate são tooissues comandos CREATE STATISTICS depois de criar a tabela de saudação.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Usar estatísticas de toocreate um procedimento armazenado em todas as colunas em um banco de dados
SQL Data Warehouse não tem um equivalente de procedimento armazenado do sistema muito [] de [sp_create_stats] no SQL Server. Esse procedimento armazenado cria um objeto de estatísticas de coluna única em todas as colunas de banco de dados de saudação que ainda não tenha estatísticas.

Isso ajudará você a começar com o design do banco de dados. Sinta-se livre tooadapt-tooyour precisa.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

toocreate estatísticas em todas as colunas na tabela de saudação com esse procedimento, simplesmente chamar o procedimento de saudação.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Exemplos: atualizar as estatísticas
estatísticas de tooupdate, você pode:

1. Atualizar um objeto de estatísticas. Especifique o nome de saudação do hello desejar tooupdate do objeto de estatísticas.
2. Atualizar todos os objetos de estatísticas em uma tabela. Especifique o nome de saudação da tabela de saudação em vez de um objeto de estatísticas específicas.

### <a name="a-update-one-specific-statistics-object"></a>R. Atualizar um objeto de estatísticas específico
Use Olá sintaxe tooupdate um objeto de estatísticas específicas a seguir:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Por exemplo:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Atualizando objetos de estatísticas específico, você pode minimizar Olá tempo e recursos de estatísticas de toomanage necessária. Isso requer que algumas considerado, porém, tooupdate objetos de estatísticas recomendada toochoose hello.

### <a name="b-update-all-statistics-on-a-table"></a>B. Atualizar todas as estatísticas em uma tabela
Isso mostra um método simples para a atualização de todos os objetos de estatísticas de saudação em uma tabela.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Por exemplo:

```sql
UPDATE STATISTICS dbo.table1;
```

Essa instrução é fácil toouse. Apenas lembre-se isso atualizará todas as estatísticas na tabela de saudação e, portanto, pode realizar mais trabalho do que o necessário. Se o desempenho de saudação não for um problema, isso é definitivamente maneira mais fácil e mais completa Olá tooguarantee estatísticas estão atualizadas.

> [!NOTE]
> Ao atualizar todas as estatísticas em uma tabela, o SQL Data Warehouse faz uma tabela de saudação toosample verificação para cada estatísticas. Se Olá tabela for grande, tem várias colunas e estatísticas, talvez seja mais eficiente tooupdate individuais as estatísticas com base na necessidade.
> 
> 

Para uma implementação de um `UPDATE STATISTICS` procedimento consulte Olá [tabelas temporárias] [ Temporary] artigo. método de implementação de saudação é ligeiramente diferente toohello `CREATE STATISTICS` procedimento acima, mas o resultado final de saudação é Olá mesmo.

Para obter a sintaxe completa de hello, consulte [Update Statistics] [ Update Statistics] no MSDN.

## <a name="statistics-metadata"></a>Metadados de estatísticas
Há várias exibição do sistema e funções que você pode usar toofind informações sobre estatísticas. Por exemplo, você pode ver se um objeto de estatísticas pode estar desatualizado usando toosee de função de estatísticas-date de hello quando as estatísticas foram criadas ou atualizadas de última.

### <a name="catalog-views-for-statistics"></a>Exibições de catálogo para as estatísticas
Essas exibições do sistema fornecem informações sobre estatísticas:

| Exibição de catálogo | Descrição |
|:--- |:--- |
| [sys.columns][sys.columns] |Uma linha para cada coluna. |
| [sys.objects][sys.objects] |Uma linha para cada objeto no banco de dados de saudação. |
| [sys.schemas][sys.schemas] |Uma linha para cada esquema no banco de dados de saudação. |
| [sys.stats][sys.stats] |Uma linha para cada objeto de estatísticas. |
| [sys.stats_columns][sys.stats_columns] |Uma linha para cada coluna no objeto de estatísticas de saudação. Links de volta toosys.columns. |
| [sys.tables][sys.tables] |Uma linha para cada tabela (inclui tabelas externas). |
| [sys.table_types][sys.table_types] |Uma linha para cada tipo de dados. |

### <a name="system-functions-for-statistics"></a>Funções de sistema para estatísticas
Essas funções de sistema são úteis para trabalhar com estatísticas:

| Função de sistema | Descrição |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Última atualização do objeto de estatísticas de saudação de data. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Fornece informações de resumo de nível e detalhadas sobre distribuição de saudação de valores conforme entendido pelo objeto de estatísticas de saudação. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Combinar colunas de estatísticas e funções em uma exibição
Essa exibição recupera colunas relacionadas juntas toostatistics e os resultados da função do hello [STATS_DATE()] [].

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>Exemplos de DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() mostra dados de saudação mantidos em um objeto de estatísticas. Esses dados estão divididos em três partes.

1. Cabeçalho
2. Vetor de densidade
3. Histograma

Olá cabeçalho metadados sobre estatísticas de saudação. histograma Olá exibe a distribuição de saudação de valores na primeira coluna chave Olá Olá do objeto de estatísticas. vetor de densidade Olá mede a correlação entre colunas. SQLDW calcula as estimativas de cardinalidade com qualquer um dos dados de saudação no objeto de estatísticas de saudação.

### <a name="show-header-density-and-histogram"></a>Mostrar cabeçalho, densidade e histograma
Este exemplo simples mostra as três partes de um objeto de estatísticas.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Por exemplo:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Mostrar uma ou mais partes de DBCC SHOW_STATISTICS();
Se você só está interessado em ver partes específicas, use Olá `WITH` cláusula e especificar quais partes que você deseja toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Por exemplo:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>Diferenças do DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() mais estritamente é implementado no SQL Data Warehouse em comparação com tooSQL Server.

1. Não há suporte para recursos não documentados
2. Não é possível usar Stats_stream
3. Não é possível associar os resultados para subconjuntos específicos de dados de estatísticas, por exemplo, (STAT_HEADER JOIN DENSITY_VECTOR)
4. NO_INFOMSGS não pode ser definido para a supressão de mensagem
5. Não é possível usar colchetes em nomes de estatísticas
6. Não é possível usar objetos de estatísticas de tooidentify de nomes de coluna
7. Não há suporte para o erro personalizado 2767

## <a name="next-steps"></a>Próximas etapas
Para obter mais detalhes, veja [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] no MSDN.  toolearn mais, consulte os artigos de saudação em [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Indexando uma tabela][Index], [particionar uma tabela] [ Partition] e [ Tabelas temporárias][Temporary].  Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].  

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
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
