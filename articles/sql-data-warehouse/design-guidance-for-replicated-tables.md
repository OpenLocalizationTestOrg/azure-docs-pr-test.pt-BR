---
title: diretrizes de aaaDesign para Azure SQL Data Warehouse de tabelas - replicadas | Microsoft Docs
description: "Recomendações para criar tabelas replicadas em seu esquema do SQL Data Warehouse do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Diretrizes de design para usar tabelas replicadas no SQL Data Warehouse do Azure
Este artigo fornece recomendações para criar tabelas replicadas no esquema do SQL Data Warehouse. Use o desempenho da consulta essas recomendações tooimprove, reduzindo a complexidade de consulta e de movimentação de dados.

> [!NOTE]
> recurso de tabela replicada Hello está atualmente em visualização pública. Alguns comportamentos são toochange de assunto.
> 

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você esteja familiarizado com os conceitos de movimentação e distribuição de dados no SQL Data Warehouse.  Para obter mais informações, consulte [Dados distribuídos](sql-data-warehouse-distributed-data.md). 

Como parte do design de tabela, entenda tanto quanto possível sobre seus dados e como os dados de saudação são consultados.  Por exemplo, considere estas perguntas:

- O tamanho é Olá?   
- A frequência de tabela Olá atualização?   
- Há tabelas de dimensões e fatos no data warehouse?   

## <a name="what-is-a-replicated-table"></a>O que é uma tabela replicada?
Uma tabela replicada tem uma cópia completa da tabela de saudação acessível em cada nó de computação. Duplicar uma tabela remove os dados de tootransfer de necessidade Olá entre nós de computação antes de uma junção ou agregação. Como tabela de saudação tem várias cópias, tabelas replicadas funcionam melhor quando o tamanho da tabela Olá é menor que 2 GB compactado.

Olá diagrama a seguir mostra uma tabela replicada que é acessível em cada nó de computação. No SQL Data Warehouse, tabela replicada Olá é tooa totalmente copiados o banco de dados de distribuição em cada nó de computação. 

![Tabela replicada](media/guidance-for-using-replicated-tables/replicated-table.png "Tabela replicada")  

As tabelas replicadas funcionam bem nas tabelas de dimensões pequenas em um esquema em estrela. Tabelas de dimensões são geralmente de um tamanho que torna mais viável toostore e mantêm várias cópias. As dimensões armazenam dados descritivos que são alterados lentamente, como nome e endereço do cliente e detalhes do produto. saudação de alteração lenta natureza dos dados Olá leva toofewer recriações de tabela replicada hello. 

Considere usar uma tabela replicada quando:

- tamanho da tabela Olá em disco é menor que 2 GB, independentemente do número de saudação de linhas. tamanho de saudação toofind de uma tabela, você pode usar o hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) comando: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- Olá tabela é usada em junções que normalmente exigiriam a movimentação de dados. Por exemplo, uma junção em tabelas de hash distribuída requer a movimentação de dados quando as colunas de junção Olá não são Olá a mesma coluna de distribuição. Se uma das tabelas de hash distribuída Olá for pequena, considere uma tabela replicada. Uma união em uma tabela round robin requer a movimentação de dados. É recomendável usar tabelas replicadas em vez de tabelas round robin na maioria dos casos. 


Considere a possibilidade de converter um existente distribuídas tooa tabela replicada tabela quando:

- Operações de movimentação de dados de uso que transmitem a nós de computação Olá dados tooall Olá os planos de consulta. Olá BroadcastMoveOperation é caro e reduz o desempenho da consulta. operações de movimentação de dados tooview em planos de consulta, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Tabelas replicadas não podem resultar em melhor desempenho de consulta hello quando:

- tabela de saudação tem inserção frequentes, atualizar e excluir operações. Essas operações de DML (linguagem) de manipulação de dados requerem uma recriação de tabela Olá replicada. Recompilar com frequência pode causar um desempenho mais lento.
- data warehouse de saudação é dimensionado com frequência. Dimensionamento de um data warehouse altera o número de saudação de nós de computação, que gera uma recompilação.
- tabela de saudação tem um grande número de colunas, mas as operações de dados normalmente acessam somente um pequeno número de colunas. Nesse cenário, em vez de replicar toda a tabela hello, pode ser mais eficiente toohash distribuir tabela hello e, em seguida, criar um índice em colunas de saudação acessada com frequência. Quando uma consulta requer a movimentação de dados, SQL Data Warehouse apenas move dados em Olá solicitadas colunas. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Usar tabelas replicadas com predicados de consulta simples
Antes de escolher toodistribute ou replicar uma tabela, pense em tipos de saudação de consultas que você planejar toorun em relação à tabela hello. Sempre que possível,

- Use tabelas replicadas para consultas com predicados de consulta simples, como igualdade ou desigualdade.
- Use tabelas distribuídas para consultas com predicados de consulta complexos, como CURTIR ou NÃO CURTIR.

Consultas de uso intensivo de CPU ter melhor desempenho quando o trabalho de saudação é distribuído em todos os nós de computação hello. Por exemplo, as consultas que executam cálculos em cada linha de uma tabela apresentam um desempenho melhor nas tabelas distribuídas do que nas tabelas replicadas. Como uma tabela replicada é armazenada por completo em cada nó de computação, uma consulta de uso intensivo de CPU em uma tabela replicada é executado em relação à tabela inteira Olá em cada nó de computação. Olá computação extra pode diminuir o desempenho de consulta.

Por exemplo, esta consulta tem um predicado complexo.  Ele é executado mais rapidamente quando o fornecedor é uma tabela distribuída em vez de uma tabela replicada. Neste exemplo, o fornecedor pode ser distribuído em hash ou em round robin.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Converter as tabelas tooreplicated round-robin tabelas existentes
Se você já tiver tabelas round robin, recomendamos convertê-las tooreplicated tabelas se eles atender aos critérios descritos neste artigo. Tabelas replicadas melhoram o desempenho em tabelas de round-robin porque eles eliminam a necessidade de saudação de movimentação de dados.  Uma tabela round robin sempre requer a movimentação de dados para as junções. 

Este exemplo usa [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange Olá DimSalesTerritory tabela tooa replicadas de tabela. Este exemplo funciona independentemente de DimSalesTerritory ser distribuído por hash ou por round robin.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Exemplo de desempenho de consulta de round-robin versus replicado 

Uma tabela replicada não requer nenhuma movimentação de dados para junções porque a tabela inteira Olá já está presente em cada nó de computação. Se as tabelas de dimensões Olá round-robin distribuído, uma junção copia tabela de dimensões Olá tooeach completo do nó de computação. dados de saudação toomove, o plano de consulta de saudação contém uma operação chamada BroadcastMoveOperation. Esse tipo de operação de movimentação de dados reduz o desempenho da consulta e é eliminada usando tabelas replicadas. etapas de plano de consulta tooview, use Olá [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) exibição de catálogo do sistema. 

Por exemplo, na seguinte consulta no esquema de AdventureWorks hello, Olá ` FactInternetSales` tabela é distribuída de hash. Olá `DimDate` e `DimSalesTerritory` as tabelas são tabelas de dimensão menores. Esta consulta retorna o total de vendas Olá na América do Norte do ano fiscal de 2004:
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
Recriamos `DimDate` e `DimSalesTerritory` como tabelas round robin. Como resultado, a consulta Olá mostrou Olá plano de consulta, que tem vários difusão mover as operações a seguir: 
 
![Plano de consulta round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

Criamos novamente `DimDate` e `DimSalesTerritory` como tabelas replicadas e executar a consulta de saudação novamente. plano de consulta resultante Olá é muito menor e não tem qualquer difundir move.

![Plano de consulta replicado](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Considerações sobre o desempenho para modificar as tabelas replicadas
SQL Data Warehouse implementa uma tabela replicada, mantendo uma versão principal da tabela de saudação. Copia Olá versão mestre tooone distribuição banco de dados em cada nó de computação. Quando há uma alteração, o SQL Data Warehouse atualiza primeiro tabela mestre hello. Em seguida, ele exige uma recriação de tabelas de saudação em cada nó de computação. Uma recriação de uma tabela replicada inclui copiar do nó de computação tooeach Olá tabela e, em seguida, a recriação de índices de saudação.

As recompilações são necessárias depois que:
- Os dados são carregados ou modificados
- Olá data warehouse é dimensionado tooa configuração de DWU diferente
- A definição da tabela é atualizada

As recompilações não são necessárias após:
- Pausar a operação
- Retomar a operação

Olá de reconstrução não acontece imediatamente depois que os dados são modificados. Em vez disso, a recriação de saudação é disparada Olá a primeira vez que uma consulta seleciona da tabela de saudação.  Instrução select inicial, Olá da tabela de saudação são toorebuild de etapas Olá tabela replicada.  Como Olá de reconstrução é feita em consulta hello, Olá impacto toohello inicial instrução select pode ser significativa dependendo do tamanho da saudação da tabela de saudação.  Se várias tabelas replicadas estão envolvidas que precisam de uma recompilação, cada cópia será reconstruída em série como etapas dentro de instrução de saudação.  toomaintain consistência de dados durante a recriação de saudação do hello replicadas um bloqueio exclusivo é obtido na tabela de saudação de tabela.  bloqueio de saudação impede que todas as tabelas de toohello de acesso para duração Olá de reconstrução de saudação. 

### <a name="use-indexes-conservatively"></a>Use os índices de forma prudente
Práticas recomendadas de indexação padrão se aplica a tabelas tooreplicated. SQL Data Warehouse recria o índice cada tabela replicada como parte da recompilação de saudação. Só use índices ganho de desempenho Olá supera o custo de Olá de reconstrução de índices de saudação.  
 
### <a name="batch-data-loads"></a>Cargas de dados em lotes
Ao carregar dados em tabelas replicadas, tente toominimize recria por envio em lote cargas juntas. Execute todas as cargas de saudação em lote antes de executar instruções select.

Por exemplo, esse padrão de carga carrega dados de quatro fontes e invoca quatro recompilações. 

- Carregar da fonte de dados 1.
- A instrução SELECT aciona a recompilação 1.
- Carregar da fonte de dados 2.
- A instrução SELECT aciona a recompilação 2.
- Carregar da fonte de dados 3.
- A instrução SELECT aciona a recompilação 3.
- Carregar da fonte de dados 4.
- A instrução SELECT aciona a recompilação 4.

Por exemplo, esse padrão de carga carrega dados de quatro fontes, mas invoca apenas uma recompilação.

- Carregar da fonte de dados 1.
- Carregar da fonte de dados 2.
- Carregar da fonte de dados 3.
- Carregar da fonte de dados 4.
- A instrução SELECT aciona a recompilação.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Recompilar uma tabela replicada após um carregamento em lote
tempos de execução de consulta consistentes tooensure, é recomendável forçar uma atualização de tabelas de saudação replicada depois de uma carga de lote. Caso contrário, consulta primeiro Olá deve aguardar Olá tabelas toorefresh, que inclui a recriação de índices de saudação. Dependendo do tamanho de saudação e o número de tabelas replicadas afetados, o impacto no desempenho Olá pode ser significativo.  

Essa consulta usa Olá [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) saudação do DMV toolist replicadas tabelas que foram modificadas, mas não foi recompiladas.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce executar Olá instrução a seguir em cada tabela no hello precede a saída de uma recompilação. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Próximas etapas 
toocreate uma tabela replicada, use uma das instruções a seguir:

- [CRIAR TABELA (SQL Data Warehouse do Azure)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT (SQL Data Warehouse do Azure](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Para obter uma visão geral das tabelas distribuídas, consulte [Tabelas distribuídas](sql-data-warehouse-tables-distribute.md).



