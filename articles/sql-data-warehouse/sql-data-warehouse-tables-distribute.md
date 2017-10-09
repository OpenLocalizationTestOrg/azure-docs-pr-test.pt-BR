---
title: tabelas de aaaDistributing no SQL Data Warehouse | Microsoft Docs
description: "Introdução à distribuição de tabelas no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Distribuindo tabelas no SQL Data Warehouse
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

SQL Data Warehouse é um sistema de banco de dados distribuído de processamento extremamente paralelo (MPP).  Ao dividir os dados e a funcionalidade de processamento em vários nós, o SQL Data Warehouse pode oferecer uma enorme escalabilidade, muito além de qualquer sistema individual.  Decidir como toodistribute seus dados no Data Warehouse do SQL são uma saudação mais importante fatores tooachieving o desempenho ideal.   desempenho de chave toooptimal Olá é minimizar a movimentação de dados e por sua vez movimentação de dados de chave toominimizing Olá é selecionando estratégia de distribuição direita hello.

## <a name="understanding-data-movement"></a>Noções básicas sobre a movimentação de dados
Em um sistema MPP, dados de saudação de cada tabela são divididos em vários bancos de dados subjacentes.  consultas Hello mais otimizado em um sistema MPP podem simplesmente ser passadas tooexecute em Olá individuais bancos de dados distribuídos sem a interação entre Olá outros bancos de dados.  Por exemplo, digamos que você tenha um banco de dados com dados de vendas que contém duas tabelas, vendas e clientes.  Se você tiver uma consulta que precisa toojoin sua tabela de cliente tooyour tabela de vendas e você dividir vendas e tabelas de cliente para cima pelo número de clientes, colocando cada cliente em um banco de dados, todas as consultas que unem vendas e clientes podem ser resolvidas dentro de cada banco de dados sem conhecimento de Olá outros bancos de dados.  Por outro lado, se seus dados de vendas é dividido pelo número de ordem e dados do cliente por número de cliente, em seguida, determinado banco de dados não terá dados correspondentes Olá para cada cliente e, portanto, se você quisesse toojoin seus dados de cliente de tooyour de dados de vendas, você precisaria tooget hello dados para cada cliente da saudação outros bancos de dados.  No segundo exemplo, a movimentação de dados necessário toooccur toomove Olá dados toohello vendas dados do cliente, para que Olá duas tabelas podem ser unidas.  

Movimentação de dados nem sempre é ruim, às vezes é necessário toosolve uma consulta.  Porém, quando essa etapa extra pode ser evitada, naturalmente a consulta é executada mais depressa.  A movimentação de dados geralmente surge quando tabelas são unidas ou são executadas agregações.  Geralmente, é necessário toodo ambos, portanto enquanto você poderá toooptimize para um cenário, como uma junção, você ainda precisa toohelp de movimentação de dados para resolver Olá outro cenário, como uma agregação.  truque Olá é descobrir qual é o menos trabalho.  Na maioria dos casos, a distribuição de grandes tabelas de fatos em uma coluna normalmente associada é Olá método mais eficaz para reduzir a saudação mais a movimentação de dados.  Distribuição de dados em colunas de junção é uma movimentação de dados de tooreduce método muito mais comum de distribuir dados em colunas envolvidas em uma agregação.

## <a name="select-distribution-method"></a>Selecionar método de distribuição
Em segundo plano hello, o SQL Data Warehouse divide os dados em 60 bancos de dados.  Cada banco de dados individual é chamado tooas um **distribuição**.  Quando dados são carregados em cada tabela, o SQL Data Warehouse tem tooknow como toodivide seus dados em 60 distribuições.  

método de distribuição de saudação é definido no nível de tabela hello e atualmente, há duas opções:

1. **Round robin** , que distribui dados uniformemente, mas aleatoriamente.
2. **Distribuídos por hash** , que distribui dados baseados em valores de hash de uma única coluna

Por padrão, quando você não definir um método de distribuição de dados, sua tabela será distribuída usando Olá **rodízio** método de distribuição.  No entanto, como se tornam mais sofisticadas em sua implementação, será conveniente usando tooconsider **hash distribuída** tabelas toominimize a movimentação de dados que por sua vez otimizar desempenho de consulta.

### <a name="round-robin-tables"></a>Tabelas Round Robin
Usar Olá método Round Robin de distribuição de dados é muito como parece.  Como seus dados são carregados, cada linha é simplesmente enviada toohello próxima distribuição.  Esse método de distribuição de dados saudação será sempre distribui aleatoriamente dados saudação muito uniformemente em todas as distribuições de saudação.  Ou seja, não há nenhuma classificação feito durante a saudação round robin processo coloca seus dados.  Uma distribuição round robin é chamada às vezes de hash aleatório por esse motivo.  Com uma tabela distribuída round robin, não há nenhum dado de saudação do toounderstand de necessidade.  Por esse motivo, as tabelas Round Robin normalmente são bons destinos de carregamento.

Por padrão, se nenhum método de distribuição for escolhido, hello método de distribuição de round robin será usado.  No entanto, enquanto as tabelas de rodízio são toouse fácil, porque os dados são distribuídos aleatoriamente sistema Olá significa que o sistema Olá não pode garantir qual distribuição cada linha são no.  Como resultado, o sistema de hello, às vezes, precisa tooinvoke um toobetter de operação de movimentação de dados organize seus dados antes que ele possa resolver uma consulta.  Essa etapa extra pode causar lentidão em suas consultas.

Considere o uso de distribuição de Round Robin para a tabela na Olá os seguintes cenários:

* Ao começar, como um simples ponto de partida
* Se não houver uma chave de junção óbvia
* Se não houver coluna boa candidata para hash distribuindo tabela Olá
* Se hello tabela não deve compartilhar uma chave de junção comum com outras tabelas
* Se a junção Olá será menos significativa do que outras junções na consulta Olá
* Quando Olá é uma tabela de preparo temporária

Ambos os exemplos criarão uma tabela Round Robin:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Enquanto o round robin é o tipo de tabela padrão Olá sendo explícita no seu DDL é considerado uma prática recomendada para que intenções saudação de seu layout de tabela são tooothers clara.
>
>

### <a name="hash-distributed-tables"></a>Tabelas distribuídas por hash
Usando um **Hash distribuída** algoritmo toodistribute suas tabelas podem melhorar o desempenho em muitos cenários, reduzindo a movimentação de dados no momento da consulta.  Hash de tabelas distribuídas são aquelas que são divididas entre hello distribuído bancos de dados usando um algoritmo de hash em uma única coluna que você selecionar.  coluna de distribuição de saudação é o que determina como os dados saudação são divididos em seus bancos de dados distribuídos.  função de hash Olá usa Olá distribuição coluna tooassign linhas toodistributions.  Olá algoritmo de hash e distribuição resultante é determinística.  Ou seja, Olá mesmo valor com o mesmo tipo de dados será sempre de saudação tem toohello mesma distribuição.    

Este exemplo criará uma tabela distribuída na ID:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Selecionar coluna de distribuição
Quando você escolhe muito**hash distribuir** uma tabela, você precisará tooselect uma coluna de distribuição individuais.  Ao selecionar uma coluna de distribuição, há tooconsider de três fatores principais.  

Selecione uma única coluna que:

1. Não será atualizada
2. Distribuirá os dados uniformemente, evitando a distorção de dados
3. Minimizar a movimentação de dados

### <a name="select-distribution-column-which-will-not-be-updated"></a>Selecionar a coluna de distribuição que não será atualizada
As colunas de distribuição não são atualizáveis. Portanto, selecione uma coluna com valores estáticos.  Se uma coluna precisará toobe atualizado, geralmente não é um candidato de distribuição válido.  Se houver um caso em que você deve atualizar uma coluna de distribuição, isso pode ser feito primeiro excluindo linha hello e, em seguida, inserir uma nova linha.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Selecionar a coluna de distribuição que distribuirá os dados uniformemente
Como um sistema distribuído executa somente tão rápida quanto sua distribuição mais lenta, é importante toodivide Olá trabalho uniformemente em distribuições de saudação em ordem tooachieve balanceada execução em todo sistema Olá.  forma de Olá Olá trabalho é dividido em um sistema distribuído baseia-se em onde residem os dados de saudação para cada distribuição.  Isso torna coluna de distribuição direita Olá tooselect muito importante para distribuir dados saudação para que cada distribuição tem trabalho igual e será take Olá mesmo toocomplete de tempo sua parte do trabalho de saudação.  Quando o trabalho também é dividido em todo sistema hello, dados de saudação são balanceados em distribuições de saudação.  Quando os dados não são equilibrados igualmente, chamamos esse evento de **distorção de dados**.  

toodivide dados uniformemente e evitar a distorção de dados, considere a seguinte Olá ao selecionar a coluna de distribuição:

1. Selecione uma coluna quem contenha um número significativo de valores distintos.
2. Evite a distribuição de dados em colunas com poucos valores distintos.
3. Evite a distribuição de dados em colunas com uma alta frequência de valores nulos.
4. Evite a distribuição de dados em colunas de data.

Como cada valor de hash too1 de 60 distribuições, distribuição uniforme tooachieve você desejará tooselect uma coluna que é altamente exclusivo e contém mais de 60 valores exclusivos.  tooillustrate, considere um caso em que a coluna tem apenas 40 valores exclusivos.  Se esta coluna foi marcada como chave de distribuição Olá, dados Olá para aquela tabela acabaria em 40 distribuições no máximo, deixando 20 distribuições com nenhum dado e nenhum toodo de processamento.  Por outro lado, hello outras 40 distribuições teria mais toodo de trabalho que se hello dados foi distribuídos uniformemente distribuições mais de 60.  Esse cenário é um exemplo de distorção de dados.

No sistema MPP, cada etapa de consulta aguarda toocomplete de todas as distribuições seu compartilhamento de trabalho hello.  Se uma distribuição fazendo mais trabalho do hello outras pessoas, Olá recursos de saudação outras distribuições são essencialmente desperdiçadas espera na distribuição de saudação ocupado.  Quando o trabalho não é distribuído de maneira uniforme entre todas as distribuições, nós chamamos este evento de **distorção de processamento**.  Distorção de processamento fará com que consultas toorun mais lento do que se cargas de trabalho Olá possam ser distribuídas uniformemente em distribuições de saudação.  Distorção de dados levará tooprocessing distorção.

Evitar a distribuição na coluna anulável altamente como valores nulos Olá todos verá Olá mesmo distribuição. Distribuindo em uma coluna de data também pode causar distorção de processamento porque todos os dados para uma determinada data serão levadas em Olá mesmo distribuição. Se vários usuários estiverem executando consultas todos filtragem em Olá mesmo data, em seguida, apenas 1 de distribuições de 60 Olá fará todo o trabalho de saudação desde a data será apenas em uma distribuição. Nesse cenário, as consultas de saudação provavelmente serão executado 60 vezes mais lentos do que se os dados saudação foram igualmente distribuídos por todas as distribuições de saudação do.

Quando nenhuma coluna de boa candidata existe, considere o uso de rodízio como método de distribuição hello.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Selecione a coluna de distribuição que irá minimizar a movimentação de dados
Minimizando a movimentação de dados, selecionando Olá distribuição certa coluna é uma das estratégias mais importantes de saudação para otimizar o desempenho do Data Warehouse do SQL.  A movimentação de dados geralmente surge quando tabelas são unidas ou são executadas agregações.  Todas as colunas usadas nas cláusulas `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` são candidatas à **boa** distribuição de hash.

Olá por outro lado, as colunas em Olá `WHERE` cláusula execute **não** fazer candidatos a coluna hash bom porque eles limitam quais distribuições participarem consulta hello, fazendo com que o processamento de distorção.  Um bom exemplo de uma coluna que pode ser tentador toodistribute, mas geralmente pode causar esse processamento distorção é uma coluna de data.

Em geral, se você tiver duas tabelas de fatos grande envolvidas frequentemente em uma junção, você obterá Olá maioria do desempenho através da distribuição de ambas as tabelas em uma das colunas de junção de saudação.  Se você tiver uma tabela que nunca é unida tooanother grande tabela de fatos, então, ser toocolumns que estejam frequentemente em Olá `GROUP BY` cláusula.

Há alguns critérios principais que devem ser atendidos tooavoid a movimentação de dados durante uma junção:

1. Hello tabelas envolvidas na junção Olá devem ser distribuído em hash **um** de colunas Olá participam da junção hello.
2. tipos de dados Olá Olá de colunas de junção devem corresponder entre as duas tabelas.
3. colunas de saudação devem estar associadas com um operador equals.
4. Olá tipo de associação não pode ser um `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Solucionando problemas de distorção de dados
Quando os dados da tabela são distribuídos usando o método de distribuição de hash hello há uma chance de que algumas distribuições será desviada toohave desproporcionalmente mais dados do que outras pessoas. Dados de distorção podem afetar o desempenho de consulta porque o resultado final de saudação de uma consulta distribuída deve esperar hello mais longa em execução toofinish de distribuição. Dependendo do grau de saudação de dados de saudação distorção, que talvez seja necessário tooaddress-lo.

### <a name="identifying-skew"></a>Identificando distorções
Tooidentify uma maneira simples uma tabela como inclinada é toouse `DBCC PDW_SHOWSPACEUSED`.  Isso é uma maneira rápida e simples toosee Olá o número de linhas da tabela que são armazenados em cada uma das distribuições de saudação 60 do seu banco de dados.  Lembre-se de que para desempenho hello mais balanceada, linhas de saudação em sua tabela distribuída devem ser divididas uniformemente em todas as distribuições de saudação.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

No entanto, se você consultar exibições de gerenciamento dinâmico Olá Azure SQL Data Warehouse (DMV), você pode executar uma análise mais detalhada.  toostart, criar exibição Olá [dbo.vTableSizes] [ dbo.vTableSizes] exibir usando Olá SQL de [visão geral da tabela] [ Overview] artigo.  Depois de saudação exibição é criada, execute este tooidentify consulta quais tabelas têm mais de distorção de dados de 10%.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Resolvendo distorções de dados
Não, todos os distorção é suficiente toowarrant uma correção.  Em alguns casos, desempenho de saudação de uma tabela em algumas consultas pode exceder danos de saudação de distorção de dados.  toodecide se você deve resolver esses dados distorcer em uma tabela, você deve compreender tanto quanto possível sobre os volumes de dados hello e consultas na carga de trabalho.   Toolook unidirecional no impacto de saudação de distorção é toouse etapas Olá Olá [consulta monitoramento] [ Query Monitoring] artigo toomonitor Olá impacto distorção no desempenho da consulta e especificamente Olá consultas demoradas de toohow de impacto assumir toocomplete distribuições de saudação individuais.

Distribuição de dados é uma questão de encontrar o equilíbrio correto de saudação entre minimizar a distorção de dados e minimizar a movimentação de dados. Eles podem ser opostas metas e, às vezes, você desejará tookeep dados distorção na movimentação de dados de tooreduce de ordem. Por exemplo, quando Olá distribuição coluna é frequentemente Olá compartilhado na junções e agregações, você será minimizando a movimentação de dados. Olá benefício de ter a movimentação de dados mínimos Olá pode compensar impacto de saudação de distorção dados.

forma comum de saudação tooresolve distorção de dados é toore-criar tabela Olá com uma coluna de distribuição diferente. Como não há nenhuma coluna de distribuição de saudação toochange em uma distribuição da tabela, Olá maneira toochange saudação de uma tabela de maneira-toorecreate-lo com um [] de [CTAS].  Aqui estão dois exemplos de como resolver a distorção de dados:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Exemplo 1: Criar novamente a tabela de saudação com uma nova coluna de distribuição
Este exemplo usa [CTAS] [] toore-criar uma tabela com uma coluna de distribuição hash diferente.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Exemplo 2: Crie novamente a tabela hello usando a distribuição de rodízio
Este exemplo usa [CTAS] [] toore-criar uma tabela com rodízio, em vez de uma distribuição de hash. Essa alteração produzirá a distribuição de dados de mesmo custo de saudação de movimentação de dados maior.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o design da tabela, consulte Olá [distribuir][Distribute], [índice][Index], [partição] [ Partition], [Tipos de dados][Data Types], [estatísticas] [ Statistics] e [tabelas temporárias] [ Temporary] artigos.

Para obter uma visão geral das práticas recomendadas, confira [Práticas recomendadas para o SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
