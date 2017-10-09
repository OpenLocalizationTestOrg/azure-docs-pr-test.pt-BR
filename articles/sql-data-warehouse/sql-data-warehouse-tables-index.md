---
title: tabelas de aaaIndexing no SQL Data Warehouse | Microsoft Azure
description: "Introdução à indexação de tabela no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Indexando tabelas no SQL Data Warehouse
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

O SQL Data Warehouse oferece várias opções de indexação, incluindo [índices columnstore clusterizados][clustered columnstore indexes], [índices clusterizados e índices não clusterizados][clustered indexes and nonclustered indexes].  Além disso, ele oferece uma opção sem índice, também conhecida como [heap][heap].  Este artigo aborda os benefícios de saudação de cada tipo de índice, bem como dicas toogetting hello mais desempenho fora de seus índices. Consulte [tabela sintaxe de create] [ create table syntax] para obter mais detalhes sobre como toocreate uma tabela no SQL Data Warehouse.

## <a name="clustered-columnstore-indexes"></a>Índice columnstore clusterizado
Por padrão, o SQL Data Warehouse cria um índice columnstore clusterizado quando nenhuma opção de índice é especificada em uma tabela. Tabelas columnstore clusterizados oferecem ambos hello mais alto nível de compactação de dados, bem como Olá melhor desempenho geral da consulta.  Tabelas columnstore clusterizado serão geralmente superam tabelas clusterizadas de índice ou heap e geralmente são a melhor opção Olá para tabelas grandes.  Por esses motivos, columnstore clusterizado é Olá melhor lugar toostart quando você não tiver certeza de como tooindex sua tabela.  

toocreate uma tabela columnstore clusterizado, simplesmente especificar o índice COLUMNSTORE CLUSTERIZADO na cláusula WITH de saudação ou deixe a cláusula WITH de saudação:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Há alguns cenários em que columnstore clusterizado pode não ser uma boa opção:

* Tabelas ColumnStore não dão suporte a varchar (max), nvarchar (max) e varbinary (max).  Considere o heap ou índice clusterizado.
* As tabelas ColumnStore podem ser menos eficientes para dados transitórios.  Considere a possibilidade de tabelas heap ou até mesmo temporárias.
* Tabelas pequenas com menos de cem milhões de linhas.  Considere as tabelas de heap.

## <a name="heap-tables"></a>Tabelas de heap
Quando você temporariamente é inicial dados no SQL Data Warehouse, você pode achar que usar uma tabela heap fará Olá processo geral mais rapidamente.  Isso ocorre porque tooheaps cargas são mais rápidos do que tabelas tooindex e em alguns Olá casos leitura subsequente pode ser feita do cache.  Se você estiver carregando dados toostage somente antes de executar mais transformações, carregando tooheap da tabela de saudação será muito mais rápido que carregar Olá dados tooa clusterizado tabela columnstore. Além disso, ao carregar dados tooa [tabela temporária] [ Temporary] também será carregado muito mais rápido do que carregar uma toopermanent de armazenamento de tabela.  

Para tabelas de pesquisa pequenas, de menos de cem milhões de linhas, as tabelas de heap geralmente são adequadas.  Tabelas do cluster columnstore começam compactação ideal tooachieve uma vez que há mais de 100 milhões de linhas.

toocreate uma tabela heap, basta especificar HEAP na cláusula WITH de saudação:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Índices clusterizados e não clusterizados
Índices clusterizados podem ter um desempenho melhor tabelas columnstore clusterizado quando precisa de uma única linha toobe recuperado rapidamente.  Para consultas em que um único ou poucas pesquisa de linha é necessário tooperformance com extrema velocidade, considere um índice de cluster ou um índice não clusterizado de secundário.  Olá desvantagem toousing um índice clusterizado é que apenas as consultas que usam um filtro altamente seletivo na coluna de índice clusterizado Olá se beneficiará.  filtro de tooimprove em outras colunas de que um índice não clusterizado pode ser adicionado tooother colunas.  No entanto, cada índice que é adicionada a tabela de tooa adicionará tanto espaço quanto tooloads de tempo de processamento.

toocreate uma tabela de índice clusterizado, basta especificar o índice CLUSTERIZADO na cláusula WITH de saudação:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd um índice não clusterizado em uma tabela, basta usar Olá sintaxe a seguir:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Otimizando índices columnstore clusterizados
As tabelas columnstore clusterizadas são organizadas em dados em segmentos.  Tenham de segmento de alta qualidade é o desempenho de consulta ideal tooachieving críticas em uma tabela columnstore.  Qualidade de segmento pode ser medida pelo número de saudação de linhas em um grupo de linhas compactado.  Qualidade de segmento é ideal quando há pelo menos 100 mil linhas por linha compactada agrupar e ganho de desempenho como número de saudação de linhas por linha grupo abordagem 1.048.576 linhas, que é Olá a maioria das linhas que pode conter um grupo de linhas.

Olá abaixo exibição pode ser criado e usado no hello de toocompute seu sistema linhas médias por linha de grupo em identificar quaisquer índices de columnstore cluster abaixo do ideal.  a última coluna Olá nesta exibição gerará como a instrução SQL que pode ser usado toorebuild seus índices.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Agora que você criou a exibição de hello, execute esta consulta tooidentify tabelas com grupos de linhas com menos de 100 mil linhas.  Obviamente, talvez você queira tooincrease limite de saudação de 100 mil se você estiver procurando mais qualidade de segmento ideal. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Depois que você executou a consulta Olá pode começar toolook dados hello e analisar os resultados. Esta tabela explica quais toolook para sua análise de grupo de linha.

| Coluna | Como toouse esses dados |
| --- | --- |
| [table_partition_count] |Se Olá tabela estiver particionada, você pode esperar toosee números maiores de grupo de linhas aberto. Em teoria, o cada partição na distribuição de saudação pode ter um grupo de linhas aberto associado a ele. Fatore isso na sua análise. Uma pequena tabela foi particionada pode ser otimizada removendo Olá particionamento totalmente como isso seria melhora a compactação. |
| [row_count_total] |Contagem total de linhas para a tabela de saudação. Por exemplo, você pode usar essa porcentagem de toocalculate valor de linhas no estado Olá compactado. |
| [row_count_per_distribution_MAX] |Se todas as linhas são distribuídas uniformemente esse valor seria o número de destino de saudação de linhas por distribuição. Compare esse valor com compressed_rowgroup_count hello. |
| [COMPRESSED_rowgroup_rows] |Número total de linhas no formato columnstore para tabela hello. |
| [COMPRESSED_rowgroup_rows_AVG] |Se o número médio de saudação de linhas é significativamente menor que hello máximo número de linhas para um grupo de linhas, considere usar CTAS ou ALTER INDEX REBUILD toorecompress Olá dados |
| [COMPRESSED_rowgroup_count] |Número de grupos de linhas no formato columnstore. Se esse número for muito alto na tabela de toohello relação é um indicador que densidade de columnstore hello está baixa. |
| [COMPRESSED_rowgroup_rows_DELETED] |Linhas são excluídas de forma lógica no formato columnstore. Se o número de saudação for alta tamanho tootable relativo, considere recriar partição hello ou recriando o índice de saudação pois isso remove fisicamente. |
| [COMPRESSED_rowgroup_rows_MIN] |Use em conjunto com hello médio e máximo colunas toounderstand Olá intervalo de valores para grupos de linhas de saudação o ColumnStore. Um número baixo acima do limite de carregamento de saudação (102.400 por distribuição alinhado por partição) sugere que otimizações estão disponíveis na carga de dados Olá |
| [COMPRESSED_rowgroup_rows_MAX] |Como acima |
| [OPEN_rowgroup_count] |Grupos de linhas abertos são normais. Seria razoável esperar um grupo de linhas ABERTO de acordo com a distribuição de tabela (60). Números excessivos sugerem carregamento de dados nas partições. Verifique Olá particionamento estratégia toomake se ele funciona |
| [OPEN_rowgroup_rows] |Cada grupo de linhas pode ter 1.048.576 linhas, no máximo. Use este toosee valor quanto grupos de linhas aberto Olá estão atualmente |
| [OPEN_rowgroup_rows_MIN] |Abra os grupos indicam que dados estão sendo trickle carregados na tabela de saudação ou que Olá carga anterior vazada nas linhas restantes para este grupo de linhas. Saudação de uso MIN, MAX, AVG colunas toosee a quantidade de dados é saturação em grupos de linhas aberto. Para tabelas pequenas pode ser 100% de todos os dados de Olá! Nesse caso, ALTER INDEX REBUILD tooforce Olá toocolumnstore de dados. |
| [OPEN_rowgroup_rows_MAX] |Como acima |
| [OPEN_rowgroup_rows_AVG] |Como acima |
| [CLOSED_rowgroup_rows] |Examinar linhas de grupo de linha de saudação fechada como uma verificação de integridade. |
| [CLOSED_rowgroup_count] |saudação de grupos de linhas fechados deve ser baixo se qualquer são vistas em todos os. Grupos de linhas fechados podem ser convertido toocompressed rowg rupo usando Olá ALTER INDEX... Comando REORGANISE. No entanto, normalmente isso não é obrigatório. Fechado grupos são automaticamente convertidos toocolumnstore linha pelo processo de "motor de tupla" hello em segundo plano. |
| [CLOSED_rowgroup_rows_MIN] |Os grupos de linhas fechados devem ter uma taxa de preenchimento alta. Se a taxa de preenchimento de saudação para um grupo de linhas fechado é baixa, análise adicional de saudação columnstore é necessária. |
| [CLOSED_rowgroup_rows_MAX] |Como acima |
| [CLOSED_rowgroup_rows_AVG] |Como acima |
| [Rebuild_Index_SQL] |Índice de columnstore toorebuild SQL para uma tabela |

## <a name="causes-of-poor-columnstore-index-quality"></a>Causas de má qualidade de índice columnstore
Se você tiver identificado as tabelas com qualidade ruim segmento, você desejará causas de saudação tooidentify.  A seguir estão algumas causas comuns de segmentos de má qualidade:

1. Pressão de memória quando o índice foi criado
2. Alto volume de operações DML
3. Operações de carregamento pequenas ou lentas
4. Número excessivo de partições

Esses fatores podem causar um toohave de índice columnstore significativamente menor que o hello ideal 1 milhão de linhas por grupo de linhas.  Eles também podem causar o grupo de linhas toogo toohello delta linhas em vez de um grupo de linhas compactado. 

### <a name="memory-pressure-when-index-was-built"></a>Pressão de memória quando o índice foi criado
Olá número de linhas por grupo de linhas compactado está diretamente relacionados toohello largura da linha de saudação e Olá a quantidade de memória disponíveis tooprocess Olá grupo de linhas.  Quando linhas são gravadas toocolumnstore tabelas sob pressão de memória, columnstore qualidade de segmento poderá ser afetado.  Portanto, Olá melhor prática é toogive sessão de saudação que está gravando a tabelas de índice de columnstore tooyour acessam tooas a quantidade de memória quanto possível.  Como há uma compensação entre a memória e simultaneidade, diretrizes de saudação em Olá certa alocação depende Olá dados em cada linha da tabela, quantidade de saudação do DWU você a memória já alocada tooyour sistema e quantidade de saudação de simultaneidade slots que você podem dar toohello sessão que está gravando tabela de tooyour de dados.  Como prática recomendada, é recomendável começar com xlargerc se você estiver usando DW300 ou menos, largerc, se você estiver usando DW400 tooDW600 e mediumrc se você estiver usando DW1000 e acima.

### <a name="high-volume-of-dml-operations"></a>Alto volume de operações DML
Um alto volume de operações DML que atualizar e excluir linhas pode introduzir ineficiência Olá ColumnStore. Isso é especialmente verdadeiro quando a maioria de saudação de linhas de saudação em um grupo de linhas são modificadas.

* A exclusão de uma linha de um grupo de linhas compactados apenas logicamente marca a linha hello como excluído. linha Hello permanece no grupo de linha compactada Olá até que seja reconstruída Olá partição ou tabela.
* Inserindo uma linha adiciona a tabela Olá linha tootooan rowstore interno chamada de um grupo de linhas delta. linha de saudação inserida não é convertido toocolumnstore até que o grupo de linhas delta hello está cheio e está marcado como fechado. Grupos de linhas são fechados assim que chegam a capacidade máxima de saudação do 1.048.576 linhas. 
* A atualização de uma linha no formato columnstore é processada como uma exclusão lógica e, em seguida, como uma inserção. linha Hello inserido pode ser armazenada no repositório de delta hello.

Em lotes de atualização e inserção operações que excedem o limite do hello em massa de 102.400 linhas por partição distribuição alinhada será gravada diretamente toohello columnstore Formatar. No entanto, supondo que uma distribuição uniforme, você precisaria toobe modificando o máximo de 6.144 milhões de linhas em uma única operação para este toooccur. Se o número de saudação de linhas para uma determinada partição alinhada a distribuição é inferior a 102.400, as linhas de saudação irão repositório delta de toohello e permanecerão lá até suficiente de linhas foram inserida ou modificadas tooclose Olá linha hello ou grupo de índice foi recriado.

### <a name="small-or-trickle-load-operations"></a>Operações de carregamento pequenas ou lentas
Às vezes, pequenas cargas que fluem para o SQL Data Warehouse também são chamadas de cargas lentas. Normalmente, eles representam um fluxo constante near dos dados que estão sendo incluídos pelo sistema hello. No entanto, como esse fluxo é quase contínua Olá volume de linhas não é muito grande. Mais dados saudação são significativamente abaixo do limite de saudação necessário para um formato de toocolumnstore carga direta.

Nessas situações, ele costuma ser melhor dados de saudação tooland primeiro no armazenamento de BLOBs do Azure e deixe-a acumular tooloading anterior. Essa técnica é conhecida normalmente como *micro envio em lote*.

### <a name="too-many-partitions"></a>Número excessivo de partições
Tooconsider de outra coisa que é o impacto de saudação do particionamento em suas tabelas columnstore clusterizado.  Antes do particionamento, o SQL Data Warehouse já divide seus dados em 60 bancos de dados.  O particionamento divide ainda mais seus dados.  Se você particionar seus dados, você desejará tooconsider que **cada** partição precisará de pelo menos 1 milhão de toohave toobenefit de linhas de um índice columnstore clusterizado.  Se você dividir a tabela em 100 partições, sua tabela terá pelo menos 6 bilhões de toohave toobenefit de linhas de um índice columnstore clusterizado (60 distribuições * 100 partições * 1 milhão de linhas). Se sua tabela de 100 partição não tiver 6 bilhões de linhas, reduzir o número de saudação de partições ou considere o uso de uma tabela de heap em vez disso.

Quando as tabelas tiverem sido carregadas com alguns dados, siga Olá abaixo tooidentify etapas e recriar tabelas com índices de columnstore cluster abaixo do ideal.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Recriação de qualidade de segmento tooimprove índices
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Etapa 1: Identificar ou criar o usuário que usa a classe de recurso correta Olá
Uma maneira rápida tooimmediately melhorar a qualidade do segmento é o índice de saudação do toorebuild.  Olá SQL retornado pelo Olá acima exibição retornará uma instrução ALTER INDEX REBUILD, que pode ser usado toorebuild seus índices.  Quando a recriação de índices, certifique-se de que você alocar suficiente memória toohello sessão reconstruirá o índice.  toodo, classe de recurso de saudação aumento de um usuário que contém um índice de saudação do permissões toorebuild esse mínimo recomendado de toohello de tabela.  classe de recurso de saudação do usuário de proprietário de banco de dados de saudação não pode ser alterado, portanto, se você não tiver criado um usuário no sistema hello, será necessário toodo primeiro.  mínimo de saudação que recomendamos é xlargerc se você estiver usando DW300 ou menos, largerc se você estiver usando DW400 tooDW600 e mediumrc se você estiver usando DW1000 e acima.

Abaixo está um exemplo de como tooallocate mais usuário tooa de memória, aumentando a classe de recurso.  Para obter mais informações sobre classes de recursos e como toocreate um novo usuário pode ser encontrado no hello [gerenciamento de simultaneidade e a carga de trabalho] [ Concurrency] artigo.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Etapa 2: recriar índices columnstore clusterizados com usuário de classe de recurso superior
Faça logon como Olá usuário da etapa 1 (por exemplo, LoadUser), que agora estão usando uma classe de recurso superior e execute instruções ALTER INDEX a saudação.  Certifique-se de que esse usuário tem tabelas de toohello permissão ALTER em que o índice de saudação estiver sendo recriado.  Estes exemplos mostram como toorebuild Olá todo o índice columnstore ou como toorebuild uma única partição. Em tabelas grandes, é mais práticos índices toorebuild uma única partição por vez.

Como alternativa, em vez de reconstruir o índice de saudação, você poderá copiar Olá tabela tooa nova tabela usando [CTAS][CTAS].  Qual é a melhor opção? Para grandes volumes de dados, [CTAS][CTAS] é geralmente mais rápido do que [ALTER INDEX][ALTER INDEX]. Para volumes menores de dados, [ALTER INDEX] [ ALTER INDEX] é mais fácil toouse e não exigem tooswap tabela hello.  Consulte **recompilação de índices com CTAS e alternância de partição** abaixo para obter mais detalhes sobre como toorebuild índices com CTAS.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

A recriação de um índice no SQL Data Warehouse é uma operação offline.  Para obter mais informações sobre como reconstruir índices, consulte Olá ALTER INDEX REBUILD seção [desfragmentação de índices Columnstore] [ Columnstore Indexes Defragmentation] e Olá sintaxe tópico [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Etapa 3: verificar se melhorou a qualidade do segmento columnstore clusterizado
Executar consulta novamente Olá identificado tabela com baixa qualidade de segmento e verificar melhorou a qualidade do segmento.  Se não melhorar a qualidade do segmento, é possível que as linhas de saudação na tabela são muito grande.  Considere usar uma classe de recurso maior ou mais DWU durante a recriação de índices.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Recriando índices com CTAS e alternância de partição
Este exemplo usa [CTAS] [ CTAS] e toorebuild uma partição de tabela de comutação de partição. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Para obter mais detalhes sobre como recriar partições usando `CTAS`, consulte Olá [partição] [ Partition] artigo.

## <a name="next-steps"></a>Próximas etapas
toolearn mais, consulte os artigos de saudação em [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Particionar uma tabela][Partition], [manter estatísticas de tabela] [ Statistics] e [ Tabelas temporárias][Temporary].  toolearn mais sobre as práticas recomendadas, consulte [práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
