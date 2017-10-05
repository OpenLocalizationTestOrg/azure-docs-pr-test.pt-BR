---
title: "Gerenciamento de estatísticas em tabelas no SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 1d5ded69e394643ddfc3de0c6d30dbd30c8e848f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="c24f5-103">Gerenciamento de estatísticas em tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c24f5-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c24f5-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="c24f5-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c24f5-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="c24f5-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="c24f5-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="c24f5-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="c24f5-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="c24f5-107">[Index][Index]</span></span>
> * <span data-ttu-id="c24f5-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="c24f5-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="c24f5-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="c24f5-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="c24f5-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="c24f5-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="c24f5-111">Quanto mais o SQL Data Warehouse sabe sobre seus dados, mais rápido ele pode executar consultas neles.</span><span class="sxs-lookup"><span data-stu-id="c24f5-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span></span>  <span data-ttu-id="c24f5-112">A maneira com a qual você informa o SQL Data Warehouse sobre seus dados é coletando estatísticas sobre seus dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="c24f5-113">Ter estatísticas sobre seus dados é uma das coisas mais importantes que você pode fazer para otimizar as consultas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span></span>  <span data-ttu-id="c24f5-114">As estatísticas ajudam o SQL Data Warehouse a criar o plano ideal para suas consultas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span></span>  <span data-ttu-id="c24f5-115">Isso porque o otimizador de consulta do SQL Data Warehouse é um otimizador baseado em custo.</span><span class="sxs-lookup"><span data-stu-id="c24f5-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="c24f5-116">Ou seja, ele compara o custo de vários planos de consulta e depois escolhe o plano com o menor custo, que também deverá ser o plano com execução mais rápida.</span><span class="sxs-lookup"><span data-stu-id="c24f5-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span></span>

<span data-ttu-id="c24f5-117">As estatísticas podem ser criadas em uma única coluna, várias colunas ou em um índice de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="c24f5-118">As estatísticas são armazenadas em um histograma que captura o intervalo e a seletividade dos valores.</span><span class="sxs-lookup"><span data-stu-id="c24f5-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span></span>  <span data-ttu-id="c24f5-119">Isso é particularmente interessante quando o otimizador precisa avaliar cláusulas JOIN, GROUP BY, HAVING e WHERE em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="c24f5-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="c24f5-120">Por exemplo, se o otimizador estimar que a data usada para filtrar sua consulta retornará 1 linha, ele poderá escolher um plano muito diferente do que se estimar que a data selecionada retornará 1 milhão de linhas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="c24f5-121">Embora a criação de estatísticas seja extremamente importante, é igualmente importante que as estatísticas reflitam com *precisão* o estado atual da tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span></span>  <span data-ttu-id="c24f5-122">Ter estatísticas atualizadas garante a seleção de um bom plano pelo otimizador.</span><span class="sxs-lookup"><span data-stu-id="c24f5-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span></span>  <span data-ttu-id="c24f5-123">Os planos criados pelo otimizador são tão bons quanto as estatísticas sobre seus dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-123">The plans created by the optimizer are only as good as the statistics on your data.</span></span>

<span data-ttu-id="c24f5-124">NO momento, o processo de criação e atualização de estatísticas é um processo manual, mas é muito simples.</span><span class="sxs-lookup"><span data-stu-id="c24f5-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span></span>  <span data-ttu-id="c24f5-125">Isso é diferente do SQL Server, que cria e atualiza automaticamente as estatísticas em colunas e índices únicos.</span><span class="sxs-lookup"><span data-stu-id="c24f5-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="c24f5-126">Ao usar as informações a seguir, você pode automatizar bastante o gerenciamento das estatísticas em seus dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-126">By using the information below, you can greatly automate the management of the statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="c24f5-127">Introdução às estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-127">Getting started with statistics</span></span>
 <span data-ttu-id="c24f5-128">Criar estatísticas de exemplo em cada coluna é uma maneira fácil de começar a usar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span></span>  <span data-ttu-id="c24f5-129">Como é igualmente importante manter estatísticas atualizadas, pode ser uma abordagem conservadora atualizar as estatísticas diariamente ou após cada carregamento.</span><span class="sxs-lookup"><span data-stu-id="c24f5-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span></span> <span data-ttu-id="c24f5-130">Sempre há compensações entre o desempenho e o custo para a criação e a atualização das estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-130">There are always trade-offs between performance and the cost to create and update statistics.</span></span>  <span data-ttu-id="c24f5-131">Se você achar que está demorando muito para manter todas as estatísticas, convém tentar ser mais seletivo sobre quais colunas têm estatísticas ou quais colunas precisam de uma atualização frequente.</span><span class="sxs-lookup"><span data-stu-id="c24f5-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="c24f5-132">Por exemplo, convém atualizar diariamente as colunas de datas, pois novos valores podem ser adicionados, e não após cada carregamento.</span><span class="sxs-lookup"><span data-stu-id="c24f5-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="c24f5-133">Novamente, você terá mais benefícios se tiver estatísticas em colunas envolvidas em cláusulas JOINs, GROUP BY, HAVING e WHERE.</span><span class="sxs-lookup"><span data-stu-id="c24f5-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="c24f5-134">Se você tiver uma tabela com muitas colunas que são usadas somente na cláusula SELECT, as estatísticas nessas colunas não serão úteis, e gastar um pouco mais de esforço para identificar apenas as colunas nas quais as estatísticas serão úteis pode reduzir o tempo de manutenção das estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="c24f5-135">Estatísticas de várias colunas</span><span class="sxs-lookup"><span data-stu-id="c24f5-135">Multi-column statistics</span></span>
<span data-ttu-id="c24f5-136">Além de criar estatísticas em colunas únicas, talvez você perceba que suas consultas se beneficiariam de estatísticas em várias colunas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="c24f5-137">Estatísticas de várias colunas são estatísticas criadas em uma lista de colunas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="c24f5-138">Elas incluem estatísticas sobre uma única coluna na primeira coluna da lista, além de algumas informações de correlação entre colunas chamadas de densidades.</span><span class="sxs-lookup"><span data-stu-id="c24f5-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="c24f5-139">Por exemplo, se você tiver uma tabela que se une a outras duas colunas, você perceberá que o SQL Data Warehouse pode otimizar ainda mais o plano se ele compreender a relação entre as duas colunas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span></span>   <span data-ttu-id="c24f5-140">As estatísticas de várias colunas podem melhorar o desempenho de consulta de algumas operações como junções compostas e agrupar por.</span><span class="sxs-lookup"><span data-stu-id="c24f5-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="c24f5-141">Atualização de estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-141">Updating statistics</span></span>
<span data-ttu-id="c24f5-142">Atualizar as estatísticas é uma parte importante de sua rotina de gerenciamento de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="c24f5-143">Quando a distribuição dos dados no banco de dados é alterada, as estatísticas precisam ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-143">When the distribution of data in the database changes, statistics need to be updated.</span></span>  <span data-ttu-id="c24f5-144">Estatísticas desatualizadas resultarão em um desempenho de consulta abaixo do ideal.</span><span class="sxs-lookup"><span data-stu-id="c24f5-144">Out-of-date statistics will lead to sub-optimal query performance.</span></span>

<span data-ttu-id="c24f5-145">Uma prática recomendada é atualizar as estatísticas em colunas de data por dia à medida que novas datas são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-145">One best practice is to update statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="c24f5-146">Sempre que há um carregamento de novas linhas no data warehouse, novas datas de carga ou datas de transação são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="c24f5-147">Isso muda a distribuição de dados e desatualiza as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-147">These change the data distribution and make the statistics out-of-date.</span></span> <span data-ttu-id="c24f5-148">Por outro lado, as estatísticas em uma coluna de país em uma tabela de cliente talvez nunca tenham de ser atualizadas, já que a distribuição de valores geralmente não é alterada.</span><span class="sxs-lookup"><span data-stu-id="c24f5-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span></span> <span data-ttu-id="c24f5-149">Supondo que a distribuição seja constante entre os clientes, adicionar novas linhas à variação de tabela não alterará a distribuição dos dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="c24f5-150">No entanto, se seu data warehouse contiver apenas um país e se você exibir dados de um país, resultando em dados de vários países sendo armazenados, definitivamente será necessário atualizar as estatísticas na coluna país.</span><span class="sxs-lookup"><span data-stu-id="c24f5-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span></span>

<span data-ttu-id="c24f5-151">Uma das primeiras perguntas a serem feitas durante a solução de uma consulta é, "As estatísticas estão atualizadas?"</span><span class="sxs-lookup"><span data-stu-id="c24f5-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span></span>

<span data-ttu-id="c24f5-152">Essa questão não pode ser respondida pela idade dos dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-152">This question is not one that can be answered by the age of the data.</span></span> <span data-ttu-id="c24f5-153">Um objeto de estatísticas atualizado pode ser muito antigo se não haja nenhuma alteração material nos dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="c24f5-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span></span> <span data-ttu-id="c24f5-154">Quando o número de linhas tiver mudado substancialmente ou se houver uma alteração material na distribuição dos valores de uma determinada coluna, *será necessário* atualizar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span></span>  

<span data-ttu-id="c24f5-155">Para referência, o **SQL Server** (não o SQL Data Warehouse) atualiza automaticamente as estatísticas para estas situações:</span><span class="sxs-lookup"><span data-stu-id="c24f5-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="c24f5-156">Se você não tiver nenhuma linha na tabela, quando adicionar linhas, obterá uma atualização automática das estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="c24f5-157">Quando você adicionar mais de 500 linhas a uma tabela, começando com menos de 500 linhas (por exemplo, no início você tem 499 e, em seguida, adiciona 500 linhas para ter um total de 999 linhas), obterá uma atualização automática</span><span class="sxs-lookup"><span data-stu-id="c24f5-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="c24f5-158">Quando você tiver mais de 500 linhas, terá de adicionar outras 500 linhas mais 20% do tamanho da tabela antes de ver uma atualização automática nas estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span></span>

<span data-ttu-id="c24f5-159">Como não há nenhuma DMV para determinar se os dados da tabela foram alterados desde que a última vez em que as estatísticas foram atualizadas, saber a idade das estatísticas pode fornecer uma parte da cena.</span><span class="sxs-lookup"><span data-stu-id="c24f5-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span></span>  <span data-ttu-id="c24f5-160">Você pode usar a consulta a seguir para determinar a última vez que suas estatísticas foram atualizadas em cada tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-160">You can use the following query to determine the last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="c24f5-161">Lembre-se de que se houver uma mudança substancial na distribuição dos valores para uma determinada coluna, você deverá atualizar as estatísticas, independentemente da última vez em que elas foram atualizadas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-161">Remember if there is a material change in the distribution of values for a given column, you should update statistics regardless of the last time they were updated.</span></span>  
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

<span data-ttu-id="c24f5-162">As colunas de data em um data warehouse, por exemplo, normalmente precisam de atualizações frequentes de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="c24f5-163">Sempre que há um carregamento de novas linhas no data warehouse, novas datas de carga ou datas de transação são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="c24f5-164">Isso muda a distribuição de dados e desatualiza as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-164">These change the data distribution and make the statistics out-of-date.</span></span>  <span data-ttu-id="c24f5-165">Por outro lado, talvez as estatísticas em uma coluna de gênero de uma tabela de clientes nunca precisem ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span></span> <span data-ttu-id="c24f5-166">Supondo que a distribuição seja constante entre os clientes, adicionar novas linhas à variação de tabela não alterará a distribuição dos dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="c24f5-167">No entanto, se o data warehouse contiver apenas um gênero, e um novo requisito resultar em vários gêneros, será definitivamente necessário atualizar as estatísticas na coluna gênero.</span><span class="sxs-lookup"><span data-stu-id="c24f5-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span></span>

<span data-ttu-id="c24f5-168">Para obter mais explicações, veja [Estatísticas][Statistics] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c24f5-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="c24f5-169">Implementação do gerenciamento de estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-169">Implementing statistics management</span></span>
<span data-ttu-id="c24f5-170">Geralmente, convém estender os processos de carregamento de dados a fim de garantir que as estatísticas estejam atualizadas ao final do carregamento.</span><span class="sxs-lookup"><span data-stu-id="c24f5-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span></span> <span data-ttu-id="c24f5-171">É no carregamento de dados que as tabelas frequentemente mudam de tamanho e/ou distribuição de valores.</span><span class="sxs-lookup"><span data-stu-id="c24f5-171">The data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="c24f5-172">Portanto, esse é um momento lógico para implementar alguns processos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c24f5-172">Therefore, this is a logical place to implement some management processes.</span></span>

<span data-ttu-id="c24f5-173">Veja abaixo alguns princípios importantes para atualizar as estatísticas durante o processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="c24f5-173">Some guiding principles are provided below for updating your statistics during the load process:</span></span>

* <span data-ttu-id="c24f5-174">Certifique-se de que cada tabela carregada tenha pelo menos um objeto de estatísticas atualizado.</span><span class="sxs-lookup"><span data-stu-id="c24f5-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="c24f5-175">Isso atualiza as informações de tamanho da tabela (contagem de linhas e contagem de páginas) como parte da atualização de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-175">This updates the tables size (row count and page count) information as part of the stats update.</span></span>
* <span data-ttu-id="c24f5-176">Concentre-se em colunas que participam de cláusulas JOIN, GROUP BY, ORDER BY e DISTINCT</span><span class="sxs-lookup"><span data-stu-id="c24f5-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="c24f5-177">Considere uma atualização mais frequentes das colunas de "chave crescente", por exemplo, datas de transação, pois esses valores não serão incluídos no histograma de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span></span>
* <span data-ttu-id="c24f5-178">Considere atualizar as colunas de distribuição estática com menos frequência.</span><span class="sxs-lookup"><span data-stu-id="c24f5-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="c24f5-179">Lembre-se de que cada objeto de estatística é atualizado em série.</span><span class="sxs-lookup"><span data-stu-id="c24f5-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="c24f5-180">Simplesmente implementar `UPDATE STATISTICS <TABLE_NAME>` talvez não seja ideal, especialmente para tabelas mais amplas com muitos objetos de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="c24f5-181">Para obter mais detalhes sobre [chave crescente], confira o white paper sobre modelo de estimativa de cardinalidade do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="c24f5-181">For more details on [ascending key] please refer to the SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="c24f5-182">Para obter mais explicações, veja [Estimativa de cardinalidade][Cardinality Estimation] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c24f5-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="c24f5-183">Exemplos: criar estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-183">Examples: Create statistics</span></span>
<span data-ttu-id="c24f5-184">Estes exemplos mostram como usar várias opções para a criação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-184">These examples show how to use various options for creating statistics.</span></span> <span data-ttu-id="c24f5-185">As opções usadas para cada coluna dependem das características dos dados e de como a coluna será usada em consultas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="c24f5-186">R.</span><span class="sxs-lookup"><span data-stu-id="c24f5-186">A.</span></span> <span data-ttu-id="c24f5-187">Criar estatísticas de coluna única com opções padrão</span><span class="sxs-lookup"><span data-stu-id="c24f5-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="c24f5-188">Para criar estatísticas em uma coluna, basta fornecer um nome para o objeto de estatísticas e o nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="c24f5-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span></span>

<span data-ttu-id="c24f5-189">Esta sintaxe usa todas as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="c24f5-189">This syntax uses all of the default options.</span></span> <span data-ttu-id="c24f5-190">Por padrão, o SQL Data Warehouse utiliza uma amostragem de 20 por cento da tabela ao criar estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="c24f5-191">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c24f5-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="c24f5-192">B.</span><span class="sxs-lookup"><span data-stu-id="c24f5-192">B.</span></span> <span data-ttu-id="c24f5-193">Criar estatísticas de coluna única examinando cada linha</span><span class="sxs-lookup"><span data-stu-id="c24f5-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="c24f5-194">A taxa de amostragem padrão de 20 por cento é suficiente para a maioria das situações.</span><span class="sxs-lookup"><span data-stu-id="c24f5-194">The default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="c24f5-195">No entanto, você pode ajustar essa taxa de amostragem.</span><span class="sxs-lookup"><span data-stu-id="c24f5-195">However, you can adjust the sampling rate.</span></span>

<span data-ttu-id="c24f5-196">Para usar toda a tabela como amostragem, use a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="c24f5-196">To sample the full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="c24f5-197">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c24f5-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-the-sample-size"></a><span data-ttu-id="c24f5-198">C.</span><span class="sxs-lookup"><span data-stu-id="c24f5-198">C.</span></span> <span data-ttu-id="c24f5-199">Criar estatísticas de coluna única, especificando o tamanho da amostra</span><span class="sxs-lookup"><span data-stu-id="c24f5-199">Create single-column statistics by specifying the sample size</span></span>
<span data-ttu-id="c24f5-200">Como alternativa, você pode especificar o tamanho da amostra como uma porcentagem:</span><span class="sxs-lookup"><span data-stu-id="c24f5-200">Alternatively, you can specify the sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-the-rows"></a><span data-ttu-id="c24f5-201">D.</span><span class="sxs-lookup"><span data-stu-id="c24f5-201">D.</span></span> <span data-ttu-id="c24f5-202">Criar estatísticas de coluna única em apenas algumas das linhas</span><span class="sxs-lookup"><span data-stu-id="c24f5-202">Create single-column statistics on only some of the rows</span></span>
<span data-ttu-id="c24f5-203">Outra opção é criar estatísticas em uma parte das linhas na tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-203">Another option, you can create statistics on a portion of the rows in your table.</span></span> <span data-ttu-id="c24f5-204">Isso é chamado de estatística filtrada.</span><span class="sxs-lookup"><span data-stu-id="c24f5-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="c24f5-205">Por exemplo, ao planejar consultar uma partição específica de uma grande tabela particionada, você pode usar as estatísticas filtradas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span></span> <span data-ttu-id="c24f5-206">Ao criar estatísticas apenas nos valores de partição, a precisão das estatísticas melhora e, portanto, o desempenho da consulta também.</span><span class="sxs-lookup"><span data-stu-id="c24f5-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="c24f5-207">Este exemplo cria estatísticas em um intervalo de valores.</span><span class="sxs-lookup"><span data-stu-id="c24f5-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="c24f5-208">Os valores podem ser facilmente definidos de acordo com o intervalo de valores em uma partição.</span><span class="sxs-lookup"><span data-stu-id="c24f5-208">The values could easily be defined to match the range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="c24f5-209">Para que o otimizador de consulta considere usar estatísticas filtradas ao escolher o plano de consulta distribuída, a consulta deve ser adequada à definição do objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-209">For the query optimizer to consider using filtered statistics when it chooses the distributed query plan, the query must fit inside the definition of the statistics object.</span></span> <span data-ttu-id="c24f5-210">Usando o exemplo anterior, a cláusula WHERE da consulta precisa especificar valores col1 entre 2000101 e 20001231.</span><span class="sxs-lookup"><span data-stu-id="c24f5-210">Using the previous example, the query's where clause needs to specify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-the-options"></a><span data-ttu-id="c24f5-211">E.</span><span class="sxs-lookup"><span data-stu-id="c24f5-211">E.</span></span> <span data-ttu-id="c24f5-212">Criar estatísticas de coluna única com todas as opções</span><span class="sxs-lookup"><span data-stu-id="c24f5-212">Create single-column statistics with all the options</span></span>
<span data-ttu-id="c24f5-213">Obviamente, você pode combinar as opções.</span><span class="sxs-lookup"><span data-stu-id="c24f5-213">You can, of course, combine the options together.</span></span> <span data-ttu-id="c24f5-214">O exemplo abaixo cria um objeto de estatísticas filtradas com um tamanho de amostra personalizado:</span><span class="sxs-lookup"><span data-stu-id="c24f5-214">The example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="c24f5-215">Para obter a referência completa, veja [CREATE STATISTICS][CREATE STATISTICS] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c24f5-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="c24f5-216">F.</span><span class="sxs-lookup"><span data-stu-id="c24f5-216">F.</span></span> <span data-ttu-id="c24f5-217">Criar estatísticas de várias colunas</span><span class="sxs-lookup"><span data-stu-id="c24f5-217">Create multi-column statistics</span></span>
<span data-ttu-id="c24f5-218">Para criar estatísticas de várias colunas, basta usar os exemplos anteriores, mas especificar mais colunas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="c24f5-219">O histograma, que é usado para estimar o número de linhas no resultado da consulta, só está disponível para a primeira coluna listada na definição do objeto da estatística.</span><span class="sxs-lookup"><span data-stu-id="c24f5-219">The histogram, which is used to estimate number of rows in the query result, is only available for the first column listed in the statistics object definition.</span></span>
> 
> 

<span data-ttu-id="c24f5-220">Neste exemplo, o histograma está em *product\_category*.</span><span class="sxs-lookup"><span data-stu-id="c24f5-220">In this example, the histogram is on *product\_category*.</span></span> <span data-ttu-id="c24f5-221">As estatísticas entre colunas são calculadas em *product\_category* e *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="c24f5-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="c24f5-222">Como há uma correlação entre *product\_category* e *product\_sub\_category*, uma estatística de várias colunas pode ser útil se essas colunas forem acessadas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="c24f5-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span></span>

### <a name="g-create-statistics-on-all-the-columns-in-a-table"></a><span data-ttu-id="c24f5-223">G.</span><span class="sxs-lookup"><span data-stu-id="c24f5-223">G.</span></span> <span data-ttu-id="c24f5-224">Criar estatísticas em todas as colunas em uma tabela</span><span class="sxs-lookup"><span data-stu-id="c24f5-224">Create statistics on all the columns in a table</span></span>
<span data-ttu-id="c24f5-225">É uma maneira de criar estatísticas é emitir comandos CREATE STATISTICS depois de criar a tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span></span>

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

### <a name="h-use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="c24f5-226">H.</span><span class="sxs-lookup"><span data-stu-id="c24f5-226">H.</span></span> <span data-ttu-id="c24f5-227">Use um procedimento armazenado para criar estatísticas em todas as colunas em um banco de dados</span><span class="sxs-lookup"><span data-stu-id="c24f5-227">Use a stored procedure to create statistics on all columns in a database</span></span>
<span data-ttu-id="c24f5-228">O SQL Data Warehouse não tem um procedimento armazenado no sistema equivalente a [sp_create_stats][] no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c24f5-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="c24f5-229">Esse procedimento armazenado cria um objeto de estatísticas de coluna única em todas as colunas do banco de dados que ainda não tenham estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span></span>

<span data-ttu-id="c24f5-230">Isso ajudará você a começar com o design do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-230">This will help you get started with your database design.</span></span> <span data-ttu-id="c24f5-231">Fique à vontade para adaptá-lo às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="c24f5-231">Feel free to adapt it to your needs.</span></span>

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

<span data-ttu-id="c24f5-232">Para criar estatísticas em todas as colunas na tabela com esse procedimento, simplesmente chame o procedimento.</span><span class="sxs-lookup"><span data-stu-id="c24f5-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="c24f5-233">Exemplos: atualizar as estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-233">Examples: update statistics</span></span>
<span data-ttu-id="c24f5-234">Para atualizar as estatísticas, você pode:</span><span class="sxs-lookup"><span data-stu-id="c24f5-234">To update statistics, you can:</span></span>

1. <span data-ttu-id="c24f5-235">Atualizar um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-235">Update one statistics object.</span></span> <span data-ttu-id="c24f5-236">Especifique o nome do objeto de estatísticas que você deseja atualizar.</span><span class="sxs-lookup"><span data-stu-id="c24f5-236">Specify the name of the statistics object you wish to update.</span></span>
2. <span data-ttu-id="c24f5-237">Atualizar todos os objetos de estatísticas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="c24f5-238">Especifique o nome da tabela em vez de um objeto de estatísticas específico.</span><span class="sxs-lookup"><span data-stu-id="c24f5-238">Specify the name of the table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="c24f5-239">R.</span><span class="sxs-lookup"><span data-stu-id="c24f5-239">A.</span></span> <span data-ttu-id="c24f5-240">Atualizar um objeto de estatísticas específico</span><span class="sxs-lookup"><span data-stu-id="c24f5-240">Update one specific statistics object</span></span>
<span data-ttu-id="c24f5-241">Use a sintaxe a seguir para atualizar um objeto de estatísticas específico:</span><span class="sxs-lookup"><span data-stu-id="c24f5-241">Use the following syntax to update a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="c24f5-242">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c24f5-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="c24f5-243">Ao atualizar objetos de estatísticas específicos, você pode minimizar o tempo e os recursos necessários para o gerenciamento de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span></span> <span data-ttu-id="c24f5-244">No entanto, isso exige um pouco de planejamento para escolher os melhores objetos de estatísticas para atualizar.</span><span class="sxs-lookup"><span data-stu-id="c24f5-244">This requires some thought, though, to choose the best statistics objects to update.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="c24f5-245">B.</span><span class="sxs-lookup"><span data-stu-id="c24f5-245">B.</span></span> <span data-ttu-id="c24f5-246">Atualizar todas as estatísticas em uma tabela</span><span class="sxs-lookup"><span data-stu-id="c24f5-246">Update all statistics on a table</span></span>
<span data-ttu-id="c24f5-247">O código abaixo mostra um método simples para atualizar todos os objetos de estatísticas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c24f5-247">This shows a simple method for updating all the statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="c24f5-248">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c24f5-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="c24f5-249">Esta instrução é fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="c24f5-249">This statement is easy to use.</span></span> <span data-ttu-id="c24f5-250">Lembre-se de que isso atualizará todas as estatísticas na tabela e, portanto, pode executar mais trabalho do que o necessário.</span><span class="sxs-lookup"><span data-stu-id="c24f5-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="c24f5-251">Se o desempenho não for um problema, essa é definitivamente a maneira mais fácil e completa de garantir a atualização das estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="c24f5-252">Ao atualizar todas as estatísticas em uma tabela, o SQL Data Warehouse realiza uma verificação da tabela para coletar amostragens para cada estatística.</span><span class="sxs-lookup"><span data-stu-id="c24f5-252">When updating all statistics on a table, SQL Data Warehouse does a scan to sample the table for each statistics.</span></span> <span data-ttu-id="c24f5-253">Se a tabela for grande, tiver muitas colunas e estatísticas, talvez seja mais eficiente para atualizar estatísticas individuais com base na necessidade.</span><span class="sxs-lookup"><span data-stu-id="c24f5-253">If the table is large, has many columns, and many statistics, it might be more efficient to update individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="c24f5-254">Para a implementação de um procedimento `UPDATE STATISTICS`, leia o artigo [Tabelas Temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="c24f5-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="c24f5-255">O método de implementação é ligeiramente diferente para o procedimento `CREATE STATISTICS` acima, mas o resultado final é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="c24f5-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span></span>

<span data-ttu-id="c24f5-256">Para obter a sintaxe completa, veja [Atualizar estatísticas][Update Statistics] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c24f5-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="c24f5-257">Metadados de estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-257">Statistics metadata</span></span>
<span data-ttu-id="c24f5-258">Há várias funções e exibições do sistema que você pode usar para localizar informações sobre estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-258">There are several system view and functions that you can use to find information about statistics.</span></span> <span data-ttu-id="c24f5-259">Por exemplo, você pode ver se um objeto de estatísticas está desatualizado usando a função stats-date para ver quando as estatísticas foram criadas ou atualizadas pela última vez.</span><span class="sxs-lookup"><span data-stu-id="c24f5-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="c24f5-260">Exibições de catálogo para as estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-260">Catalog views for statistics</span></span>
<span data-ttu-id="c24f5-261">Essas exibições do sistema fornecem informações sobre estatísticas:</span><span class="sxs-lookup"><span data-stu-id="c24f5-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="c24f5-262">Exibição de catálogo</span><span class="sxs-lookup"><span data-stu-id="c24f5-262">Catalog View</span></span> | <span data-ttu-id="c24f5-263">Descrição</span><span class="sxs-lookup"><span data-stu-id="c24f5-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c24f5-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="c24f5-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="c24f5-265">Uma linha para cada coluna.</span><span class="sxs-lookup"><span data-stu-id="c24f5-265">One row for each column.</span></span> |
| <span data-ttu-id="c24f5-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="c24f5-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="c24f5-267">Uma linha para cada objeto no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-267">One row for each object in the database.</span></span> |
| <span data-ttu-id="c24f5-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="c24f5-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="c24f5-269">Uma linha para cada esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-269">One row for each schema in the database.</span></span> |
| <span data-ttu-id="c24f5-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="c24f5-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="c24f5-271">Uma linha para cada objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="c24f5-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="c24f5-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="c24f5-273">Uma linha para cada coluna no objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-273">One row for each column in the statistics object.</span></span> <span data-ttu-id="c24f5-274">Conecta novamente a sys.columns.</span><span class="sxs-lookup"><span data-stu-id="c24f5-274">Links back to sys.columns.</span></span> |
| <span data-ttu-id="c24f5-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="c24f5-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="c24f5-276">Uma linha para cada tabela (inclui tabelas externas).</span><span class="sxs-lookup"><span data-stu-id="c24f5-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="c24f5-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="c24f5-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="c24f5-278">Uma linha para cada tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="c24f5-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="c24f5-279">Funções de sistema para estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-279">System functions for statistics</span></span>
<span data-ttu-id="c24f5-280">Essas funções de sistema são úteis para trabalhar com estatísticas:</span><span class="sxs-lookup"><span data-stu-id="c24f5-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="c24f5-281">Função de sistema</span><span class="sxs-lookup"><span data-stu-id="c24f5-281">System Function</span></span> | <span data-ttu-id="c24f5-282">Descrição</span><span class="sxs-lookup"><span data-stu-id="c24f5-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c24f5-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="c24f5-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="c24f5-284">Data da última atualização do objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-284">Date the statistics object was last updated.</span></span> |
| <span data-ttu-id="c24f5-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="c24f5-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="c24f5-286">Fornece informações detalhadas e resumidas sobre a distribuição de valores, conforme entendido pelo objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="c24f5-287">Combinar colunas de estatísticas e funções em uma exibição</span><span class="sxs-lookup"><span data-stu-id="c24f5-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="c24f5-288">Essa exibição une as colunas relacionadas às estatísticas e os resultados da função [STATS_DATE()][].</span><span class="sxs-lookup"><span data-stu-id="c24f5-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="c24f5-289">Exemplos de DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="c24f5-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="c24f5-290">DBCC SHOW_STATISTICS() mostra os dados contidos em um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span></span> <span data-ttu-id="c24f5-291">Esses dados estão divididos em três partes.</span><span class="sxs-lookup"><span data-stu-id="c24f5-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="c24f5-292">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="c24f5-292">Header</span></span>
2. <span data-ttu-id="c24f5-293">Vetor de densidade</span><span class="sxs-lookup"><span data-stu-id="c24f5-293">Density Vector</span></span>
3. <span data-ttu-id="c24f5-294">Histograma</span><span class="sxs-lookup"><span data-stu-id="c24f5-294">Histogram</span></span>

<span data-ttu-id="c24f5-295">Os metadados de cabeçalho sobre as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-295">The header metadata about the statistics.</span></span> <span data-ttu-id="c24f5-296">O histograma exibe a distribuição de valores na primeira coluna de chave do objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-296">The histogram displays the distribution of values in the first key column of the statistics object.</span></span> <span data-ttu-id="c24f5-297">O vetor de densidade mede a correlação entre colunas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-297">The density vector measures cross-column correlation.</span></span> <span data-ttu-id="c24f5-298">O SQLDW calcula as estimativas de cardinalidade com os dados no objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="c24f5-299">Mostrar cabeçalho, densidade e histograma</span><span class="sxs-lookup"><span data-stu-id="c24f5-299">Show header, density, and histogram</span></span>
<span data-ttu-id="c24f5-300">Este exemplo simples mostra as três partes de um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="c24f5-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="c24f5-301">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c24f5-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="c24f5-302">Mostrar uma ou mais partes de DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="c24f5-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="c24f5-303">Se você só estiver interessado em ver partes específicas, use a cláusula `WITH` e especifique quais partes deseja ver:</span><span class="sxs-lookup"><span data-stu-id="c24f5-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="c24f5-304">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c24f5-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="c24f5-305">Diferenças do DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="c24f5-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="c24f5-306">DBCC SHOW_STATISTICS() é implementado mais estritamente no SQL Data Warehouse comparado ao SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c24f5-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span></span>

1. <span data-ttu-id="c24f5-307">Não há suporte para recursos não documentados</span><span class="sxs-lookup"><span data-stu-id="c24f5-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="c24f5-308">Não é possível usar Stats_stream</span><span class="sxs-lookup"><span data-stu-id="c24f5-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="c24f5-309">Não é possível associar os resultados para subconjuntos específicos de dados de estatísticas, por exemplo, (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="c24f5-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="c24f5-310">NO_INFOMSGS não pode ser definido para a supressão de mensagem</span><span class="sxs-lookup"><span data-stu-id="c24f5-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="c24f5-311">Não é possível usar colchetes em nomes de estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="c24f5-312">Não é possível usar nomes de coluna para identificar objetos de estatísticas</span><span class="sxs-lookup"><span data-stu-id="c24f5-312">Cannot use column names to identify statistics objects</span></span>
7. <span data-ttu-id="c24f5-313">Não há suporte para o erro personalizado 2767</span><span class="sxs-lookup"><span data-stu-id="c24f5-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="c24f5-314">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c24f5-314">Next steps</span></span>
<span data-ttu-id="c24f5-315">Para obter mais detalhes, veja [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c24f5-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="c24f5-316">Para saber mais, consulte os artigos sobre [Visão geral da tabela][Overview], [Tipos de dados da tabela][Data Types], [Distribuição de uma tabela][Distribute], [Indexação de uma tabela][Index], [Particionamento de uma tabela][Partition] e [Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="c24f5-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="c24f5-317">Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="c24f5-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
