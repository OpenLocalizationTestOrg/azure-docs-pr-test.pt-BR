---
title: "desempenho do índice columnstore aaaImprove no SQL Azure | Microsoft Docs"
description: "Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas de que um índice columnstore compacta em cada grupo de linhas."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Maximizando a qualidade do grupo de linhas para o columnstore

Qualidade do grupo de linhas é determinada pelo número de saudação de linhas em um grupo de linhas. Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas de que um índice columnstore compacta em cada grupo de linhas.  Use essas taxas de compactação métodos tooimprove e o desempenho da consulta para índices columnstore.

## <a name="why-hello-rowgroup-size-matters"></a>Por que o tamanho do rowgroup Olá é importante
Desde que um índice columnstore examina uma tabela por meio do exame segmentos de colunas de rowgroups individuais, maximizar o número de saudação de linhas em cada grupo de linhas melhora o desempenho de consulta. Quando rowgroups tiver um grande número de linhas, a compactação de dados melhora o que significa que há menos tooread de dados do disco.

Para obter mais informações sobre rowgroups, consulte [Guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Tamanho de destino para rowgroups
Para melhor desempenho de consulta, o objetivo de Olá é toomaximize número de saudação de linhas por grupo de linhas em um índice columnstore. Um rowgroup pode ter, no máximo, 1.048.576 linhas. Seu toonot okey tem o número de máximo de saudação de linhas por rowgroup. Os índices Columnstore obtêm um bom desempenho quando os rowgroups têm, pelo menos, 100.000 linhas.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Os rowgroups podem ser cortados durante a compactação

Durante uma bulk load ou columnstore recompilação de índice, às vezes, há não suficiente toocompress disponíveis de memória que todos Olá linhas designadas para cada grupo de linhas. Quando há pressão de memória, índices columnstore trim tamanhos do rowgroup Olá para que compactação ColumnStore Olá pode ter êxito. 

Quando há linhas de toocompress 10.000 pelo menos memória insuficiente em cada grupo de linhas, o SQL Data Warehouse gera um erro.

Para obter mais informações sobre o carregamento em massa, consulte [Carregamento em massa em um índice columnstore clusterizado](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Como toomonitor rowgroup qualidade

Há uma DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expõe informações úteis, como o número de linhas em rowgroups e hello motivo para a fragmentação se há foi cortar. Você pode criar hello após a exibição como uma maneira útil tooquery informações tooget DMV na remoção do grupo de linhas.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Olá trim_reason_desc informa se Olá rowgroup foi cortado (trim_reason_desc = NO_TRIM implica sem corte e grupo de linhas é de melhor qualidade). Olá motivos trim indicam prematuro corte do grupo de linhas de saudação:
- Carregamento em MASSA: Esse motivo do corte é usado quando o lote de entrada hello de linhas para carregamento Olá tinha menos de 1 milhão de linhas. mecanismo de saudação criará grupos de linhas compactado se há maior que 100.000 linhas sendo inseridas (como tooinserting contrário no repositório de delta Olá), mas conjuntos Olá tooBULKLOAD motivo trim. Nesse cenário, considere aumentar o tooaccumulate de janela de carga de lote mais linhas. Além disso, reavalie sua tooensure de esquema de particionamento não está muito granular, como grupos de linhas não podem abranger os limites de partição.
- MEMORY_LIMITATION: toocreate grupos de linhas com 1 milhão de linhas, uma determinada quantidade de memória de trabalho é exigido pelo mecanismo de saudação. Quando a memória disponível de saudação ao carregar a sessão é menor que o hello necessário trabalhar memória, grupos de linhas prematuramente obtenham cortados. Olá seções a seguir explica como tooestimate memória necessária e alocar mais memória.
- DICTIONARY_SIZE: Este motivo do corte indica que a fragmentação do grupo de linhas ocorreu devido a pelo menos uma coluna de cadeia de caracteres com cadeias de caracteres ampla e/ou de alta cardinalidade. tamanho do dicionário Olá é limitado too16 MB na memória e quando esse limite é atingido o grupo de linhas de saudação é compactado. Se você se deparar com essa situação, considere isolar coluna problemático Olá em uma tabela separada.

## <a name="how-tooestimate-memory-requirements"></a>Como os requisitos de memória tooestimate

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Olá máximo de memória necessária toocompress um rowgroup é aproximadamente

- 72 MB +
- \#linhas \* \#colunas \* 8 bytes +
- \#linhas \* \#colunas de cadeia de caracteres curta \* 32 bytes +
- \#colunas de cadeia de caracteres longa \* 16 MB para o dicionário de compactação

em que as colunas de cadeia de caracteres curta usam tipos de dados de cadeia de caracteres de <= 32 bytes e as colunas de cadeia de caracteres longa usam tipos de dados de cadeia de caracteres de > 32 bytes.

As cadeias de caracteres longas são compactadas com um método de compactação projetado para a compactação de texto. Esse método de compactação usa um *dicionário* toostore padrões de texto. tamanho máximo de saudação de um dicionário é 16 MB. Há apenas um dicionário para cada coluna de cadeia de caracteres longa no grupo de linhas de saudação.

Para obter uma discussão detalhada sobre os requisitos de memória de columnstore, assista ao vídeo [Escala do SQL Data Warehouse do Azure: configuração e diretrizes](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Requisitos de memória tooreduce maneiras

Use Olá seguindo os requisitos de memória de saudação técnicas tooreduce para compactar os rowgroups em índices columnstore.

### <a name="use-fewer-columns"></a>Usar menos colunas
Se possível, crie tabela Olá com menos colunas. Quando um rowgroup é compactado no columnstore hello, o índice de columnstore Olá compacta cada segmento de coluna separadamente. Olá, portanto, os requisitos de memória toocompress um grupo de linhas aumente como Olá aumento do número de colunas.


### <a name="use-fewer-string-columns"></a>Usar menos colunas de cadeia de caracteres
As colunas de tipos de dados de cadeia de caracteres exigem mais memória do que os tipos de dados numéricos e de data. requisitos de memória tooreduce, considere remover colunas de cadeia de caracteres de tabelas de fatos e colocá-los em tabelas de dimensão menores.

Requisitos de memória adicionais para a compactação de cadeia de caracteres:

- Tipos de dados de cadeia de caracteres too32 caracteres podem exigir 32 bytes adicionais por valor.
- Tipos de dados de cadeia de caracteres com mais de 32 caracteres são compactados usando métodos de dicionário.  Cada coluna no rowgroup Olá pode exigir o dicionário do tooan adicional 16 MB toobuild hello.

### <a name="avoid-over-partitioning"></a>Evitar o excesso de particionamento

Os índices Columnstore criam um ou mais rowgroups por partição. No SQL Data Warehouse, o número de saudação de partições rapidamente aumenta porque dados saudação são distribuídos e cada distribuição é particionada. Se a tabela Olá tem muitas partições, pode não ser suficiente rowgroups de saudação toofill linhas. falta de saudação de linhas não cria a pressão de memória durante a compactação, mas leva toorowgroups que não obtenha o melhor desempenho de consulta de columnstore hello.

Outro motivo tooavoid excesso de particionamento é uma sobrecarga de memória para carregamento de linhas em um índice columnstore em uma tabela particionada. Durante o carregamento, várias partições podem receber linhas de entrada hello, que são mantidas na memória até que cada partição tem suficiente toobe linhas compactada. Ter um número excessivo de partições cria pressão de memória adicional.

### <a name="simplify-hello-load-query"></a>Simplificar a consulta de carga Olá

banco de dados de saudação compartilha Olá concessão de memória para uma consulta entre todos os operadores de saudação na consulta de saudação. Quando uma consulta de carga tem relações e tipos complexos, Olá memória disponível para a compactação é reduzida.

Olá carga consulta toofocus somente na consulta Olá de carregamento de design. Se você precisar toorun transformações nos dados hello, executá-los separado da consulta de carga hello. Por exemplo, dados de saudação do estágio em uma tabela de heap, executar transformações de saudação e, em seguida, carregar Olá tabela de preparo no índice de columnstore hello. Você pode também carregar dados saudação primeiro e usar Olá MPP sistema tootransform Olá dados.

### <a name="adjust-maxdop"></a>Ajustar o MAXDOP

Cada distribuição compacta rowgroups Olá ColumnStore em paralelo quando há mais de um núcleo de CPU disponível por distribuição. paralelismo de saudação requer mais recursos de memória, que podem levar a pressão toomemory e remoção de linhas.

tooreduce pressão de memória, você pode usar o hello MAXDOP consulta dica tooforce Olá carga operação toorun em modo serial dentro de cada distribuição.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Maneiras tooallocate mais memória

Classe de recurso de usuário de tamanho e hello DWU juntos determinar quanta memória está disponível para uma consulta de usuário. tooincrease Olá para concessão de memória para uma consulta de carga, você pode aumentar o número de saudação do DWUs ou aumentar a classe de recurso de saudação.

- Olá tooincrease DWUs, consulte [como dimensionar o desempenho?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- classe de recurso de saudação toochange para uma consulta, consulte [alterar um exemplo de classe de recurso de usuário](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Por exemplo, em 100 DWU um usuário na classe de recurso Olá smallrc pode usar 100 MB de memória para cada distribuição. Para obter detalhes hello, consulte [simultaneidade no Data Warehouse SQL](sql-data-warehouse-develop-concurrency.md).

Suponha que você determinar que precisa de 700 MB de tamanhos do rowgroup de alta qualidade de tooget de memória. Estes exemplos mostram como você pode executar a consulta de carga Olá com memória suficiente.

- Usando 1000 DWUs e mediumrc, a concessão de memória é de 800 MB
- Usando 600 DWUs e largerc, a concessão de memória é de 800 MB.


## <a name="next-steps"></a>Próximas etapas

toofind mais maneiras tooimprove desempenho SQL Data Warehouse, consulte Olá [visão geral do desempenho](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
