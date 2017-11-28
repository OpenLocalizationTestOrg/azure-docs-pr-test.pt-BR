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
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="4da43-103">Gerenciamento de estatísticas em tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4da43-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4da43-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="4da43-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="4da43-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="4da43-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="4da43-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="4da43-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="4da43-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="4da43-107">[Index][Index]</span></span>
> * <span data-ttu-id="4da43-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="4da43-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="4da43-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="4da43-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="4da43-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="4da43-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="4da43-111">Hello mais SQL Data Warehouse sabe sobre seus dados, hello mais rápido ele poderá executar consultas em relação aos dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="4da43-112">Olá maneira que indicam o SQL Data Warehouse sobre seus dados, é coletar estatísticas sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="4da43-113">Têm estatísticas em seus dados é uma das coisas mais importantes Olá você pode fazer toooptimize suas consultas.</span><span class="sxs-lookup"><span data-stu-id="4da43-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="4da43-114">Estatísticas ajudam SQL Data Warehouse criar Olá o plano ideal de suas consultas.</span><span class="sxs-lookup"><span data-stu-id="4da43-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="4da43-115">Isso ocorre porque a consulta do SQL Data Warehouse Olá otimizador tem um custo com base em otimizador.</span><span class="sxs-lookup"><span data-stu-id="4da43-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="4da43-116">Ou seja, ele compara o custo de saudação de vários planos de consulta e então escolhe Olá plano com hello menor custo, que também deve ser o plano de saudação que executará hello mais rápido.</span><span class="sxs-lookup"><span data-stu-id="4da43-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="4da43-117">As estatísticas podem ser criadas em uma única coluna, várias colunas ou em um índice de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="4da43-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="4da43-118">As estatísticas são armazenadas em um histograma que captura o intervalo de saudação e a seletividade dos valores.</span><span class="sxs-lookup"><span data-stu-id="4da43-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="4da43-119">Isso é de particular interesse quando as necessidades de otimizador Olá tooevaluate junções, GROUP BY, HAVING e cláusulas WHERE em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="4da43-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="4da43-120">Por exemplo, se o otimizador Olá estima que date de hello você está filtrando em sua consulta retornará 1 linha, ele pode escolher um diferentes planejar que se ele estimativas que data você selecionou irá retornar 1 milhão de linhas.</span><span class="sxs-lookup"><span data-stu-id="4da43-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="4da43-121">Durante a criação de estatísticas é extremamente importante, é igualmente importante que estatísticas *com precisão* refletem Olá o estado atual da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="4da43-122">Com estatísticas atualizadas, você garante que um bom plano é selecionado pelo otimizador hello.</span><span class="sxs-lookup"><span data-stu-id="4da43-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="4da43-123">planos de saudação criados pelo otimizador Olá só são tão boas quanto as estatísticas de saudação em seus dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="4da43-124">processo de saudação de criação e atualização de estatísticas é atualmente um processo manual, mas é toodo muito simple.</span><span class="sxs-lookup"><span data-stu-id="4da43-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="4da43-125">Isso é diferente do SQL Server, que cria e atualiza automaticamente as estatísticas em colunas e índices únicos.</span><span class="sxs-lookup"><span data-stu-id="4da43-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="4da43-126">Usando informações de saudação abaixo, você pode automatizar muito gerenciamento Olá de estatísticas de saudação em seus dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="4da43-127">Introdução às estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-127">Getting started with statistics</span></span>
 <span data-ttu-id="4da43-128">Criando estatísticas por amostra em cada coluna é uma maneira fácil tooget iniciado com estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="4da43-129">Como é igualmente importante tookeep estatísticas atualizadas, uma abordagem conservadora pode ser tooupdate estatísticas diariamente ou após cada carga.</span><span class="sxs-lookup"><span data-stu-id="4da43-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="4da43-130">Sempre há compensações entre desempenho e Olá custo toocreate e atualizar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="4da43-131">Se você achar que está levando muito toomaintain todas as estatísticas, convém tootry toobe mais seletivo sobre as colunas que têm estatísticas ou as colunas que precisa frequentes de atualização.</span><span class="sxs-lookup"><span data-stu-id="4da43-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="4da43-132">Por exemplo, convém colunas de data tooupdate diariamente, conforme novos valores podem ser adicionados em vez de após cada carga.</span><span class="sxs-lookup"><span data-stu-id="4da43-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="4da43-133">Novamente, você obterá Olá maior benefício fazendo com que as estatísticas em colunas envolvidas em junções, GROUP BY, HAVING e cláusulas WHERE.</span><span class="sxs-lookup"><span data-stu-id="4da43-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="4da43-134">Se você tiver uma tabela com uma grande quantidade de cláusula SELECT de colunas que são usadas somente em hello, estatísticas nessas colunas não podem ajudar e gastos um pouco mais tooidentify de esforço somente colunas Olá onde as estatísticas serão útil, pode reduzir Olá tempo toomaintain estatísticas .</span><span class="sxs-lookup"><span data-stu-id="4da43-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="4da43-135">Estatísticas de várias colunas</span><span class="sxs-lookup"><span data-stu-id="4da43-135">Multi-column statistics</span></span>
<span data-ttu-id="4da43-136">Além disso toocreating estatísticas em colunas únicas, você pode achar que suas consultas se beneficiam de estatísticas de várias colunas.</span><span class="sxs-lookup"><span data-stu-id="4da43-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="4da43-137">Estatísticas de várias colunas são estatísticas criadas em uma lista de colunas.</span><span class="sxs-lookup"><span data-stu-id="4da43-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="4da43-138">Elas incluem estatísticas de coluna única na primeira coluna de saudação na lista hello, além de algumas informações de correlação entre colunas chamado densidades.</span><span class="sxs-lookup"><span data-stu-id="4da43-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="4da43-139">Por exemplo, se você tiver uma tabela que une tooanother em duas colunas, você pode achar que SQL Data Warehouse poderá otimizar melhor plano de saudação que ele entenda a relação de saudação entre duas colunas.</span><span class="sxs-lookup"><span data-stu-id="4da43-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="4da43-140">As estatísticas de várias colunas podem melhorar o desempenho de consulta de algumas operações como junções compostas e agrupar por.</span><span class="sxs-lookup"><span data-stu-id="4da43-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="4da43-141">Atualização de estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-141">Updating statistics</span></span>
<span data-ttu-id="4da43-142">Atualizar as estatísticas é uma parte importante de sua rotina de gerenciamento de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="4da43-143">Quando altera a distribuição de saudação de dados no banco de dados de saudação, estatísticas necessário toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="4da43-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="4da43-144">As estatísticas desatualizadas levará o desempenho ideal de toosub de consulta.</span><span class="sxs-lookup"><span data-stu-id="4da43-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="4da43-145">Uma prática recomendada é tooupdate estatísticas em colunas de data por dia à medida que novas datas são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="4da43-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="4da43-146">Cada novas linhas de tempo são carregados no data warehouse de hello, datas de carga novo ou transação são adicionados.</span><span class="sxs-lookup"><span data-stu-id="4da43-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="4da43-147">Esses alteram Olá distribuição de dados e faça estatísticas Olá desatualizadas.</span><span class="sxs-lookup"><span data-stu-id="4da43-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="4da43-148">Por outro lado, as estatísticas em uma coluna de país em uma tabela de cliente nunca talvez seja necessário toobe atualizado, como a distribuição de saudação de valores geralmente não são alterados.</span><span class="sxs-lookup"><span data-stu-id="4da43-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="4da43-149">Supondo que a distribuição de saudação é constante entre os clientes, adicionar nova variação de tabela toohello linhas não vai toochange a distribuição de dados hello.</span><span class="sxs-lookup"><span data-stu-id="4da43-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="4da43-150">No entanto, se o data warehouse contém apenas um país e você exibir dados de um país, resultando em dados de vários países que estão sendo armazenados, definitivamente necessário tooupdate estatísticas na coluna de país hello.</span><span class="sxs-lookup"><span data-stu-id="4da43-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="4da43-151">Uma saudação primeiro perguntas tooask quando uma consulta de solução de problemas, "são Olá estatísticas atualizadas?"</span><span class="sxs-lookup"><span data-stu-id="4da43-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="4da43-152">Essa pergunta não é aquele que podem ser respondidas por idade Olá dos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="4da43-153">Um objeto de estatísticas toodate backup pode ser muito antigo se não houve nenhuma toohello alteração material dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="4da43-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="4da43-154">Quando Olá número de linhas alterado substancialmente ou há uma alteração material na distribuição de saudação de valores para uma determinada coluna *, em seguida,* é tooupdate das estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="4da43-155">Para referência, o **SQL Server** (não o SQL Data Warehouse) atualiza automaticamente as estatísticas para estas situações:</span><span class="sxs-lookup"><span data-stu-id="4da43-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="4da43-156">Se você tiver zero linhas na tabela hello, quando você adiciona linhas, você obterá uma atualização automática de estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="4da43-157">Quando você adiciona a tabela de tooa mais de 500 linhas começando com menos de 500 linhas (por exemplo, no início você tiver 499 e, em seguida, adicione 500 linhas tooa totalizando 999 linhas), você receberá uma atualização automática</span><span class="sxs-lookup"><span data-stu-id="4da43-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="4da43-158">Quando tiver mais de 500 linhas terá tooadd 500 linhas adicionais + 20% do tamanho de saudação da tabela Olá antes de você verá uma atualização automática em estatísticas de saudação</span><span class="sxs-lookup"><span data-stu-id="4da43-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="4da43-159">Como não há nenhum toodetermine DMV se os dados na tabela de saudação foi alterado desde Olá últimas estatísticas de tempo foram atualizadas, saber a idade de saudação de estatísticas pode fornecer com parte da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="4da43-160">Você pode usar o hello toodetermine Olá última vez em que as estatísticas de consulta a seguir onde atualizado em cada tabela.</span><span class="sxs-lookup"><span data-stu-id="4da43-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="4da43-161">Lembre-se de que se houver uma alteração substancial na distribuição de saudação de valores para uma determinada coluna, você deve atualizar as estatísticas independentemente Olá a última vez em que eles foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="4da43-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="4da43-162">As colunas de data em um data warehouse, por exemplo, normalmente precisam de atualizações frequentes de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="4da43-163">Cada novas linhas de tempo são carregados no data warehouse de hello, datas de carga novo ou transação são adicionados.</span><span class="sxs-lookup"><span data-stu-id="4da43-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="4da43-164">Esses alteram Olá distribuição de dados e faça estatísticas Olá desatualizadas.</span><span class="sxs-lookup"><span data-stu-id="4da43-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="4da43-165">Por outro lado, as estatísticas em uma coluna de gênero em uma tabela de cliente nunca talvez seja necessário toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="4da43-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="4da43-166">Supondo que a distribuição de saudação é constante entre os clientes, adicionar nova variação de tabela toohello linhas não vai toochange a distribuição de dados hello.</span><span class="sxs-lookup"><span data-stu-id="4da43-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="4da43-167">No entanto, se o data warehouse contém apenas um sexo e uma nova resulta de requisito em vários gêneros, definitivamente necessário tooupdate estatísticas na coluna de sexo hello.</span><span class="sxs-lookup"><span data-stu-id="4da43-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="4da43-168">Para obter mais explicações, veja [Estatísticas][Statistics] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4da43-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="4da43-169">Implementação do gerenciamento de estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-169">Implementing statistics management</span></span>
<span data-ttu-id="4da43-170">Geralmente é uma boa ideia tooextend seus dados ao carregar tooensure de processo que as estatísticas são atualizadas no hello fim do carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="4da43-171">saudação de carga de dados é quando tabelas com mais frequência alterar seu tamanho e/ou sua distribuição de valores.</span><span class="sxs-lookup"><span data-stu-id="4da43-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="4da43-172">Portanto, este é um lugar lógico tooimplement alguns processos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4da43-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="4da43-173">Para atualizar as estatísticas durante o processo de carregamento hello, alguns princípios são fornecidos abaixo:</span><span class="sxs-lookup"><span data-stu-id="4da43-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="4da43-174">Certifique-se de que cada tabela carregada tenha pelo menos um objeto de estatísticas atualizado.</span><span class="sxs-lookup"><span data-stu-id="4da43-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="4da43-175">Este Olá atualizações tabelas informações de tamanho (contagem de linha e página) como parte da atualização de estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="4da43-176">Concentre-se em colunas que participam de cláusulas JOIN, GROUP BY, ORDER BY e DISTINCT</span><span class="sxs-lookup"><span data-stu-id="4da43-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="4da43-177">Considere atualizar "crescente chave" colunas, como transações mais frequentemente esses valores não serão incluídos no histograma de estatísticas de saudação datas.</span><span class="sxs-lookup"><span data-stu-id="4da43-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="4da43-178">Considere atualizar as colunas de distribuição estática com menos frequência.</span><span class="sxs-lookup"><span data-stu-id="4da43-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="4da43-179">Lembre-se de que cada objeto de estatística é atualizado em série.</span><span class="sxs-lookup"><span data-stu-id="4da43-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="4da43-180">Simplesmente implementar `UPDATE STATISTICS <TABLE_NAME>` talvez não seja ideal, especialmente para tabelas mais amplas com muitos objetos de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="4da43-181">Para obter mais detalhes sobre [crescente chave] consulte o white paper de modelo de estimativa de cardinalidade toohello SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="4da43-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="4da43-182">Para obter mais explicações, veja [Estimativa de cardinalidade][Cardinality Estimation] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4da43-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="4da43-183">Exemplos: criar estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-183">Examples: Create statistics</span></span>
<span data-ttu-id="4da43-184">Estes exemplos mostram como toouse várias opções para a criação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="4da43-185">Opções de saudação que você usa para cada coluna dependem de como Olá coluna será usada em consultas e características de saudação de seus dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="4da43-186">R.</span><span class="sxs-lookup"><span data-stu-id="4da43-186">A.</span></span> <span data-ttu-id="4da43-187">Criar estatísticas de coluna única com opções padrão</span><span class="sxs-lookup"><span data-stu-id="4da43-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="4da43-188">toocreate estatísticas em uma coluna, basta fornecer um nome de objeto de estatísticas de saudação e saudação da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="4da43-189">Essa sintaxe usa todas as opções padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="4da43-190">Por padrão, o SQL Data Warehouse amostras 20 por cento da tabela de saudação ao criar estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="4da43-191">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4da43-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="4da43-192">B.</span><span class="sxs-lookup"><span data-stu-id="4da43-192">B.</span></span> <span data-ttu-id="4da43-193">Criar estatísticas de coluna única examinando cada linha</span><span class="sxs-lookup"><span data-stu-id="4da43-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="4da43-194">taxa de amostragem saudação padrão de 20% é suficiente para a maioria das situações.</span><span class="sxs-lookup"><span data-stu-id="4da43-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="4da43-195">No entanto, você pode ajustar a taxa de amostragem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="4da43-196">saudação de toosample completa da tabela, use a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="4da43-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="4da43-197">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4da43-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="4da43-198">C.</span><span class="sxs-lookup"><span data-stu-id="4da43-198">C.</span></span> <span data-ttu-id="4da43-199">Criar estatísticas de coluna única, especificando o tamanho do exemplo hello</span><span class="sxs-lookup"><span data-stu-id="4da43-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="4da43-200">Como alternativa, você pode especificar o tamanho do exemplo hello como uma porcentagem:</span><span class="sxs-lookup"><span data-stu-id="4da43-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="4da43-201">D.</span><span class="sxs-lookup"><span data-stu-id="4da43-201">D.</span></span> <span data-ttu-id="4da43-202">Criar estatísticas de coluna única em apenas algumas das linhas de saudação</span><span class="sxs-lookup"><span data-stu-id="4da43-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="4da43-203">Outra opção, você pode criar estatísticas em uma parte das linhas de saudação em sua tabela.</span><span class="sxs-lookup"><span data-stu-id="4da43-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="4da43-204">Isso é chamado de estatística filtrada.</span><span class="sxs-lookup"><span data-stu-id="4da43-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="4da43-205">Por exemplo, você pode usar as estatísticas filtradas quando você planejar tooquery uma partição específica de uma grande tabela particionada.</span><span class="sxs-lookup"><span data-stu-id="4da43-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="4da43-206">Ao criar estatísticas em Olá somente valores de partição, precisão de saudação das estatísticas de saudação melhorar e, portanto, melhorar o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="4da43-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="4da43-207">Este exemplo cria estatísticas em um intervalo de valores.</span><span class="sxs-lookup"><span data-stu-id="4da43-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="4da43-208">valores Hello facilmente podem ser definido pelo intervalo de saudação toomatch de valores em uma partição.</span><span class="sxs-lookup"><span data-stu-id="4da43-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="4da43-209">Para Olá tooconsider de Otimizador de consulta usando estatísticas filtradas quando escolhe um plano de consulta distribuída hello, consulta Olá deve se ajustar dentro definição Olá Olá do objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="4da43-210">Usando o exemplo anterior hello, Olá da consulta em que a cláusula precisa toospecify col1 valores entre 2000101 e 20001231.</span><span class="sxs-lookup"><span data-stu-id="4da43-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="4da43-211">E.</span><span class="sxs-lookup"><span data-stu-id="4da43-211">E.</span></span> <span data-ttu-id="4da43-212">Criar estatísticas de coluna única com todas as opções de saudação</span><span class="sxs-lookup"><span data-stu-id="4da43-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="4da43-213">Naturalmente, você pode combinar as opções de saudação juntos.</span><span class="sxs-lookup"><span data-stu-id="4da43-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="4da43-214">exemplo Hello abaixo cria um objeto de estatísticas filtradas com um tamanho de amostra personalizado:</span><span class="sxs-lookup"><span data-stu-id="4da43-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="4da43-215">Para obter referência completa hello, consulte [CREATE STATISTICS] [ CREATE STATISTICS] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4da43-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="4da43-216">F.</span><span class="sxs-lookup"><span data-stu-id="4da43-216">F.</span></span> <span data-ttu-id="4da43-217">Criar estatísticas de várias colunas</span><span class="sxs-lookup"><span data-stu-id="4da43-217">Create multi-column statistics</span></span>
<span data-ttu-id="4da43-218">toocreate estatísticas de várias colunas, simplesmente use exemplos anteriores hello, mas especificar mais colunas.</span><span class="sxs-lookup"><span data-stu-id="4da43-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="4da43-219">histograma Hello, que é usada tooestimate o número de linhas no resultado de consulta hello, só está disponível para Olá primeira coluna listada na definição de objeto de estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="4da43-220">Neste exemplo, o histograma hello está em *produto\_categoria*.</span><span class="sxs-lookup"><span data-stu-id="4da43-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="4da43-221">As estatísticas entre colunas são calculadas em *product\_category* e *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="4da43-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="4da43-222">Como há uma correlação entre *produto\_categoria* e *produto\_sub\_categoria*, um estado de várias coluna pode ser útil se essas colunas são acessadas em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="4da43-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="4da43-223">G.</span><span class="sxs-lookup"><span data-stu-id="4da43-223">G.</span></span> <span data-ttu-id="4da43-224">Criar estatísticas em todas as colunas de saudação em uma tabela</span><span class="sxs-lookup"><span data-stu-id="4da43-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="4da43-225">Estatísticas de uma maneira toocreate são tooissues comandos CREATE STATISTICS depois de criar a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="4da43-226">H.</span><span class="sxs-lookup"><span data-stu-id="4da43-226">H.</span></span> <span data-ttu-id="4da43-227">Usar estatísticas de toocreate um procedimento armazenado em todas as colunas em um banco de dados</span><span class="sxs-lookup"><span data-stu-id="4da43-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="4da43-228">SQL Data Warehouse não tem um equivalente de procedimento armazenado do sistema muito [] de [sp_create_stats] no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4da43-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="4da43-229">Esse procedimento armazenado cria um objeto de estatísticas de coluna única em todas as colunas de banco de dados de saudação que ainda não tenha estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="4da43-230">Isso ajudará você a começar com o design do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-230">This will help you get started with your database design.</span></span> <span data-ttu-id="4da43-231">Sinta-se livre tooadapt-tooyour precisa.</span><span class="sxs-lookup"><span data-stu-id="4da43-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="4da43-232">toocreate estatísticas em todas as colunas na tabela de saudação com esse procedimento, simplesmente chamar o procedimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="4da43-233">Exemplos: atualizar as estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-233">Examples: update statistics</span></span>
<span data-ttu-id="4da43-234">estatísticas de tooupdate, você pode:</span><span class="sxs-lookup"><span data-stu-id="4da43-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="4da43-235">Atualizar um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-235">Update one statistics object.</span></span> <span data-ttu-id="4da43-236">Especifique o nome de saudação do hello desejar tooupdate do objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="4da43-237">Atualizar todos os objetos de estatísticas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="4da43-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="4da43-238">Especifique o nome de saudação da tabela de saudação em vez de um objeto de estatísticas específicas.</span><span class="sxs-lookup"><span data-stu-id="4da43-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="4da43-239">R.</span><span class="sxs-lookup"><span data-stu-id="4da43-239">A.</span></span> <span data-ttu-id="4da43-240">Atualizar um objeto de estatísticas específico</span><span class="sxs-lookup"><span data-stu-id="4da43-240">Update one specific statistics object</span></span>
<span data-ttu-id="4da43-241">Use Olá sintaxe tooupdate um objeto de estatísticas específicas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da43-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="4da43-242">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4da43-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="4da43-243">Atualizando objetos de estatísticas específico, você pode minimizar Olá tempo e recursos de estatísticas de toomanage necessária.</span><span class="sxs-lookup"><span data-stu-id="4da43-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="4da43-244">Isso requer que algumas considerado, porém, tooupdate objetos de estatísticas recomendada toochoose hello.</span><span class="sxs-lookup"><span data-stu-id="4da43-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="4da43-245">B.</span><span class="sxs-lookup"><span data-stu-id="4da43-245">B.</span></span> <span data-ttu-id="4da43-246">Atualizar todas as estatísticas em uma tabela</span><span class="sxs-lookup"><span data-stu-id="4da43-246">Update all statistics on a table</span></span>
<span data-ttu-id="4da43-247">Isso mostra um método simples para a atualização de todos os objetos de estatísticas de saudação em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="4da43-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="4da43-248">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4da43-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="4da43-249">Essa instrução é fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="4da43-249">This statement is easy toouse.</span></span> <span data-ttu-id="4da43-250">Apenas lembre-se isso atualizará todas as estatísticas na tabela de saudação e, portanto, pode realizar mais trabalho do que o necessário.</span><span class="sxs-lookup"><span data-stu-id="4da43-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="4da43-251">Se o desempenho de saudação não for um problema, isso é definitivamente maneira mais fácil e mais completa Olá tooguarantee estatísticas estão atualizadas.</span><span class="sxs-lookup"><span data-stu-id="4da43-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="4da43-252">Ao atualizar todas as estatísticas em uma tabela, o SQL Data Warehouse faz uma tabela de saudação toosample verificação para cada estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="4da43-253">Se Olá tabela for grande, tem várias colunas e estatísticas, talvez seja mais eficiente tooupdate individuais as estatísticas com base na necessidade.</span><span class="sxs-lookup"><span data-stu-id="4da43-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="4da43-254">Para uma implementação de um `UPDATE STATISTICS` procedimento consulte Olá [tabelas temporárias] [ Temporary] artigo.</span><span class="sxs-lookup"><span data-stu-id="4da43-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="4da43-255">método de implementação de saudação é ligeiramente diferente toohello `CREATE STATISTICS` procedimento acima, mas o resultado final de saudação é Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="4da43-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="4da43-256">Para obter a sintaxe completa de hello, consulte [Update Statistics] [ Update Statistics] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4da43-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="4da43-257">Metadados de estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-257">Statistics metadata</span></span>
<span data-ttu-id="4da43-258">Há várias exibição do sistema e funções que você pode usar toofind informações sobre estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="4da43-259">Por exemplo, você pode ver se um objeto de estatísticas pode estar desatualizado usando toosee de função de estatísticas-date de hello quando as estatísticas foram criadas ou atualizadas de última.</span><span class="sxs-lookup"><span data-stu-id="4da43-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="4da43-260">Exibições de catálogo para as estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-260">Catalog views for statistics</span></span>
<span data-ttu-id="4da43-261">Essas exibições do sistema fornecem informações sobre estatísticas:</span><span class="sxs-lookup"><span data-stu-id="4da43-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="4da43-262">Exibição de catálogo</span><span class="sxs-lookup"><span data-stu-id="4da43-262">Catalog View</span></span> | <span data-ttu-id="4da43-263">Descrição</span><span class="sxs-lookup"><span data-stu-id="4da43-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4da43-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="4da43-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="4da43-265">Uma linha para cada coluna.</span><span class="sxs-lookup"><span data-stu-id="4da43-265">One row for each column.</span></span> |
| <span data-ttu-id="4da43-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="4da43-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="4da43-267">Uma linha para cada objeto no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="4da43-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="4da43-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="4da43-269">Uma linha para cada esquema no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="4da43-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="4da43-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="4da43-271">Uma linha para cada objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="4da43-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="4da43-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="4da43-273">Uma linha para cada coluna no objeto de estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="4da43-274">Links de volta toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="4da43-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="4da43-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="4da43-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="4da43-276">Uma linha para cada tabela (inclui tabelas externas).</span><span class="sxs-lookup"><span data-stu-id="4da43-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="4da43-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="4da43-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="4da43-278">Uma linha para cada tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="4da43-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="4da43-279">Funções de sistema para estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-279">System functions for statistics</span></span>
<span data-ttu-id="4da43-280">Essas funções de sistema são úteis para trabalhar com estatísticas:</span><span class="sxs-lookup"><span data-stu-id="4da43-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="4da43-281">Função de sistema</span><span class="sxs-lookup"><span data-stu-id="4da43-281">System Function</span></span> | <span data-ttu-id="4da43-282">Descrição</span><span class="sxs-lookup"><span data-stu-id="4da43-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4da43-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="4da43-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="4da43-284">Última atualização do objeto de estatísticas de saudação de data.</span><span class="sxs-lookup"><span data-stu-id="4da43-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="4da43-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="4da43-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="4da43-286">Fornece informações de resumo de nível e detalhadas sobre distribuição de saudação de valores conforme entendido pelo objeto de estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="4da43-287">Combinar colunas de estatísticas e funções em uma exibição</span><span class="sxs-lookup"><span data-stu-id="4da43-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="4da43-288">Essa exibição recupera colunas relacionadas juntas toostatistics e os resultados da função do hello [STATS_DATE()] [].</span><span class="sxs-lookup"><span data-stu-id="4da43-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="4da43-289">Exemplos de DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="4da43-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="4da43-290">DBCC SHOW_STATISTICS() mostra dados de saudação mantidos em um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="4da43-291">Esses dados estão divididos em três partes.</span><span class="sxs-lookup"><span data-stu-id="4da43-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="4da43-292">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="4da43-292">Header</span></span>
2. <span data-ttu-id="4da43-293">Vetor de densidade</span><span class="sxs-lookup"><span data-stu-id="4da43-293">Density Vector</span></span>
3. <span data-ttu-id="4da43-294">Histograma</span><span class="sxs-lookup"><span data-stu-id="4da43-294">Histogram</span></span>

<span data-ttu-id="4da43-295">Olá cabeçalho metadados sobre estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="4da43-296">histograma Olá exibe a distribuição de saudação de valores na primeira coluna chave Olá Olá do objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="4da43-297">vetor de densidade Olá mede a correlação entre colunas.</span><span class="sxs-lookup"><span data-stu-id="4da43-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="4da43-298">SQLDW calcula as estimativas de cardinalidade com qualquer um dos dados de saudação no objeto de estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da43-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="4da43-299">Mostrar cabeçalho, densidade e histograma</span><span class="sxs-lookup"><span data-stu-id="4da43-299">Show header, density, and histogram</span></span>
<span data-ttu-id="4da43-300">Este exemplo simples mostra as três partes de um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4da43-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="4da43-301">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4da43-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="4da43-302">Mostrar uma ou mais partes de DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="4da43-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="4da43-303">Se você só está interessado em ver partes específicas, use Olá `WITH` cláusula e especificar quais partes que você deseja toosee:</span><span class="sxs-lookup"><span data-stu-id="4da43-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="4da43-304">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4da43-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="4da43-305">Diferenças do DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="4da43-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="4da43-306">DBCC SHOW_STATISTICS() mais estritamente é implementado no SQL Data Warehouse em comparação com tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="4da43-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="4da43-307">Não há suporte para recursos não documentados</span><span class="sxs-lookup"><span data-stu-id="4da43-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="4da43-308">Não é possível usar Stats_stream</span><span class="sxs-lookup"><span data-stu-id="4da43-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="4da43-309">Não é possível associar os resultados para subconjuntos específicos de dados de estatísticas, por exemplo, (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="4da43-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="4da43-310">NO_INFOMSGS não pode ser definido para a supressão de mensagem</span><span class="sxs-lookup"><span data-stu-id="4da43-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="4da43-311">Não é possível usar colchetes em nomes de estatísticas</span><span class="sxs-lookup"><span data-stu-id="4da43-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="4da43-312">Não é possível usar objetos de estatísticas de tooidentify de nomes de coluna</span><span class="sxs-lookup"><span data-stu-id="4da43-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="4da43-313">Não há suporte para o erro personalizado 2767</span><span class="sxs-lookup"><span data-stu-id="4da43-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="4da43-314">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4da43-314">Next steps</span></span>
<span data-ttu-id="4da43-315">Para obter mais detalhes, veja [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4da43-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="4da43-316">toolearn mais, consulte os artigos de saudação em [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Indexando uma tabela][Index], [particionar uma tabela] [ Partition] e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="4da43-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="4da43-317">Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="4da43-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
