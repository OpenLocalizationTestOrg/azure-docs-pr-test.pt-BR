---
title: "aaaResolve problemas de distorção de dados usando o Azure Data Lake Tools para Visual Studio | Microsoft Docs"
description: "Solucione problemas em possíveis soluções para problemas de distorção de dados usando as Ferramentas do Azure Data Lake para Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="2147a-103">Resolver problemas de distorção de dados usando as Ferramentas do Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2147a-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="2147a-104">O que é distorção de dados?</span><span class="sxs-lookup"><span data-stu-id="2147a-104">What is data skew?</span></span>

<span data-ttu-id="2147a-105">Resumidamente, distorção de dados é a super-representação de um valor.</span><span class="sxs-lookup"><span data-stu-id="2147a-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="2147a-106">Imagine que você atribuiu 50 examiners de imposto tooaudit devoluções de imposto, um examinador para cada estado dos EUA.</span><span class="sxs-lookup"><span data-stu-id="2147a-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="2147a-107">examiner do Wyoming Hello, porque há população de saudação é pequena, tem pouco toodo.</span><span class="sxs-lookup"><span data-stu-id="2147a-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="2147a-108">Na Califórnia, no entanto, examiner Olá é mantida muito ocupado devido a população grande do estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="2147a-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="2147a-109">![Exemplo de problema de distorção de dados](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="2147a-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="2147a-110">Em nosso cenário, dados saudação é desigualdade distribuídos por todos os examiners de imposto, que significa que alguns examiners devem funcionar mais do que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="2147a-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="2147a-111">Em seu trabalho, com frequência você enfrentar situações como exemplo de imposto examiner hello aqui.</span><span class="sxs-lookup"><span data-stu-id="2147a-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="2147a-112">Em termos mais técnicos, um vértice obtém dados muito mais do que seus colegas, uma situação que faz com que o vértice Olá funcionar mais do que outros e que eventualmente reduz a velocidade de todo o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2147a-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="2147a-113">O que é pior, trabalho Olá pode falhar, pois vértices podem ter, por exemplo, uma limitação de 5 horas de tempo de execução e uma limitação de 6 GB de memória.</span><span class="sxs-lookup"><span data-stu-id="2147a-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="2147a-114">Resolvendo problemas de distorções de dados</span><span class="sxs-lookup"><span data-stu-id="2147a-114">Resolving data-skew problems</span></span>

<span data-ttu-id="2147a-115">As Ferramentas do Azure Data Lake para Visual Studio podem ajudar a detectar se o trabalho tem um problema de distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="2147a-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="2147a-116">Se houver algum problema, você pode resolvê-lo experimentando soluções Olá nesta seção.</span><span class="sxs-lookup"><span data-stu-id="2147a-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="2147a-117">Solução 1: melhorar o particionamento da tabela</span><span class="sxs-lookup"><span data-stu-id="2147a-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="2147a-118">Opção 1: Olá filtro inclinada valor de chave com antecedência</span><span class="sxs-lookup"><span data-stu-id="2147a-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="2147a-119">Se ele não afeta sua lógica de negócios, você pode filtrar os valores de alta frequência Olá antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="2147a-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="2147a-120">Por exemplo, se houver muita 000-000 000 na coluna GUID, não convém tooaggregate esse valor.</span><span class="sxs-lookup"><span data-stu-id="2147a-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="2147a-121">Antes de agregação, você pode escrever "GUID onde! ="000-000 000"" valor de alta frequência Olá toofilter.</span><span class="sxs-lookup"><span data-stu-id="2147a-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="2147a-122">Opção 2: separar uma chave de partição ou distribuição diferente</span><span class="sxs-lookup"><span data-stu-id="2147a-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="2147a-123">Olá anterior como exemplo, se quiser que as cargas de trabalho de auditoria de imposto de Olá toocheck somente todos sobre Olá país, você pode melhorar a distribuição de dados Olá selecionando o número de identificação de saudação como sua chave.</span><span class="sxs-lookup"><span data-stu-id="2147a-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="2147a-124">Escolher uma partição diferente ou a chave de distribuição pode, às vezes, distribuir dados hello mais uniformemente, mas você precisa toomake-se de que essa opção não afeta sua lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="2147a-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="2147a-125">Por exemplo, toocalculate soma de imposto de saudação para cada estado, talvez você queira toodesignate _estado_ como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="2147a-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="2147a-126">Se você continuar tooexperience esse problema, tente usar a opção 3.</span><span class="sxs-lookup"><span data-stu-id="2147a-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="2147a-127">Opção 3: adicionar mais chaves de partição ou distribuição</span><span class="sxs-lookup"><span data-stu-id="2147a-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="2147a-128">Em vez de usar apenas _Estado_ como uma chave de partição, você pode usar mais de uma chave para o particionamento.</span><span class="sxs-lookup"><span data-stu-id="2147a-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="2147a-129">Por exemplo, considere adicionar _CEP_ como uma partição adicional partição de dados de chave tooreduce tamanhos e distribuir dados hello mais uniformemente.</span><span class="sxs-lookup"><span data-stu-id="2147a-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="2147a-130">Opção 4: usar a distribuição round robin</span><span class="sxs-lookup"><span data-stu-id="2147a-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="2147a-131">Se você não encontrar uma chave adequada para a partição e a distribuição, você pode tentar toouse distribuição de round-robin.</span><span class="sxs-lookup"><span data-stu-id="2147a-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="2147a-132">A distribuição round robin trata cada linha igualmente e as coloca aleatoriamente nos buckets correspondentes.</span><span class="sxs-lookup"><span data-stu-id="2147a-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="2147a-133">dados de saudação obtém distribuídos uniformemente, mas ele perde informações de localidade, uma desvantagem que também pode reduzir o desempenho do trabalho para algumas operações.</span><span class="sxs-lookup"><span data-stu-id="2147a-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="2147a-134">Além disso, se você estiver fazendo a agregação para a chave distorcidos Olá mesmo assim, o problema de distorção de dados de saudação persistirá.</span><span class="sxs-lookup"><span data-stu-id="2147a-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="2147a-135">toolearn mais sobre a distribuição de round robin, consulte Olá U-SQL tabela distribuições seção [criar tabela (U-SQL): Criando uma tabela com esquema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="2147a-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="2147a-136">Solução 2: Melhorar o plano de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="2147a-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="2147a-137">Opção 1: Usar a instrução de CREATE STATISTICS Olá</span><span class="sxs-lookup"><span data-stu-id="2147a-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="2147a-138">U-SQL fornece a instrução CREATE STATISTICS de saudação em tabelas.</span><span class="sxs-lookup"><span data-stu-id="2147a-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="2147a-139">Esta instrução oferece mais toohello Otimizador de consulta de informações sobre Olá características de dados, como distribuição de valor, que são armazenados em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2147a-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="2147a-140">Para a maioria das consultas, o otimizador de consulta de saudação já gera as estatísticas necessárias para um plano de consulta de alta qualidade hello.</span><span class="sxs-lookup"><span data-stu-id="2147a-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="2147a-141">Ocasionalmente, talvez seja necessário tooimprove desempenho de consulta criando estatísticas adicionais com CREATE STATISTICS ou modificar o design da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="2147a-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="2147a-142">Para obter mais informações, consulte Olá [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="2147a-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="2147a-143">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2147a-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="2147a-144">Informações de estatísticas não são atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2147a-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="2147a-145">Se você atualizar os dados de saudação em uma tabela sem recriar estatísticas hello, desempenho de consulta Olá pode recusar.</span><span class="sxs-lookup"><span data-stu-id="2147a-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="2147a-146">Opção 2: Usar SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="2147a-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="2147a-147">Se você quiser imposto de saudação toosum para cada estado, você deve usar GROUP BY estado, uma abordagem que não evita o problema de distorção de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2147a-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="2147a-148">No entanto, você pode fornecer uma dica de dados em seu tooidentify consulta dados distorcer chaves para que o otimizador Olá pode preparar um plano de execução para você.</span><span class="sxs-lookup"><span data-stu-id="2147a-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="2147a-149">Normalmente, você pode definir o parâmetro hello como 0,5 e 1, com o que significa não muito distorção de distorção e 1 significado pesada de 0,5.</span><span class="sxs-lookup"><span data-stu-id="2147a-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="2147a-150">Como dica Olá afeta a otimização de plano de execução para a instrução atual hello e todas as instruções de downstream, ser dica de saudação tooadd se antes Olá potencial inclinada key-wise agregação.</span><span class="sxs-lookup"><span data-stu-id="2147a-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="2147a-151">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2147a-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="2147a-152">Opção 3: usar ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="2147a-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="2147a-153">Além do tooSKEWFACTOR para inclinada-chave específica junção casos, se você souber que Olá outro conjunto de linhas unidas for pequeno, você pode informar o otimizador Olá adicionando uma dica de número de linhas na instrução de U-SQL Olá antes da junção.</span><span class="sxs-lookup"><span data-stu-id="2147a-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="2147a-154">Dessa forma, otimizador pode escolher um toohelp de estratégia de junção difusão melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="2147a-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="2147a-155">Lembre-se de que o número de linhas não resolve o problema de distorção de dados de saudação, mas possa oferecer ajuda adicional.</span><span class="sxs-lookup"><span data-stu-id="2147a-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="2147a-156">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2147a-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="2147a-157">Solução 3: Melhorar a combinação e Redutor definido pelo usuário de saudação</span><span class="sxs-lookup"><span data-stu-id="2147a-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="2147a-158">Às vezes, você pode escrever um toodeal de operador definido pelo usuário com a lógica do processo complicado e um redutor bem escrito e combinação podem reduzir um problema de distorção de dados em alguns casos.</span><span class="sxs-lookup"><span data-stu-id="2147a-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="2147a-159">Opção 1: usar um redutor recursivo, se possível</span><span class="sxs-lookup"><span data-stu-id="2147a-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="2147a-160">Por padrão, um redutor definido pelo usuário será executado no modo não recursivo, o que significa que o trabalho de redução para uma chave será distribuído em um único vértice.</span><span class="sxs-lookup"><span data-stu-id="2147a-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="2147a-161">Mas, se os dados forem precisos, Olá grandes conjuntos de dados podem ser processados em um único vértice e executados por um longo tempo.</span><span class="sxs-lookup"><span data-stu-id="2147a-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="2147a-162">tooimprove desempenho, você pode adicionar um atributo no seu toorun do código toodefine Redutor no modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="2147a-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="2147a-163">Em seguida, Olá grandes conjuntos de dados pode ser distribuída toomultiple vértices e executados em paralelo, o que acelera o seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="2147a-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="2147a-164">toochange um toorecursive Redutor de não-recursivo, você precisa toomake-se de que o algoritmo de associação.</span><span class="sxs-lookup"><span data-stu-id="2147a-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="2147a-165">Por exemplo, sum Olá é associativo e mediana Olá não é.</span><span class="sxs-lookup"><span data-stu-id="2147a-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="2147a-166">Você também precisa toomake-se de que Olá de entrada e saída para Redutor lembre-Olá mesmo esquema.</span><span class="sxs-lookup"><span data-stu-id="2147a-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="2147a-167">Atributo do redutor recursivo:</span><span class="sxs-lookup"><span data-stu-id="2147a-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="2147a-168">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2147a-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="2147a-169">Opção 2: usar o modo combinador no nível de linha, se possível</span><span class="sxs-lookup"><span data-stu-id="2147a-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="2147a-170">Dica de número de linhas de toohello semelhante para casos de associação de chave inclinada específico, o modo de combinação tenta toodistribute grande valor de chave em horários diferentes conjuntos de toomultiple vértices para que o trabalho de saudação pode ser executado simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2147a-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="2147a-171">O modo combinador não pode resolver problemas de distorção de dados, mas pode auxiliar em casos de grandes conjuntos de valores de chaves distorcidas.</span><span class="sxs-lookup"><span data-stu-id="2147a-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="2147a-172">Por padrão, o modo de combinação Olá está completo, o que significa que Olá deixado o conjunto de linhas e o conjunto correto de linhas não pode ser separado.</span><span class="sxs-lookup"><span data-stu-id="2147a-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="2147a-173">Definindo o modo hello como interna/esquerda/direita permite que a junção de nível de linha.</span><span class="sxs-lookup"><span data-stu-id="2147a-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="2147a-174">sistema de saudação separa os conjuntos de linhas correspondentes hello e distribui-los em vários vértices que são executados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="2147a-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="2147a-175">No entanto, antes de configurar o modo de combinação hello, tenha cuidado tooensure que Olá conjuntos de linhas correspondentes pode ser separado.</span><span class="sxs-lookup"><span data-stu-id="2147a-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="2147a-176">exemplo Hello a seguir mostra um conjunto de linha esquerda separados.</span><span class="sxs-lookup"><span data-stu-id="2147a-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="2147a-177">Cada linha de saída depende de uma única linha de entrada da saudação esquerda, e potencialmente depende de todas as linhas de saudação à direita com hello mesmo valor de chave.</span><span class="sxs-lookup"><span data-stu-id="2147a-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="2147a-178">Se você definir o modo de combinação hello como left, o sistema de saudação separa Olá enorme esquerda-conjunto de linhas em pequenas e atribui toomultiple vértices.</span><span class="sxs-lookup"><span data-stu-id="2147a-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Ilustração do modo combinador](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="2147a-180">Se você definir o modo de combinação incorreta Olá, combinação Olá é menos eficiente e resultados de saudação podem estar errados.</span><span class="sxs-lookup"><span data-stu-id="2147a-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="2147a-181">Atributos do modo de combinador:</span><span class="sxs-lookup"><span data-stu-id="2147a-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="2147a-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Depende de cada linha de saída em uma única linha de entrada da esquerda da saudação (e potencialmente todas as linhas a partir de saudação à direita com hello mesmo valor de chave).</span><span class="sxs-lookup"><span data-stu-id="2147a-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="2147a-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): cada linha de saída depende de uma única linha de entrada da saudação direito (e potencialmente todas as linhas da esquerda Olá com hello que mesmo valor de chave).</span><span class="sxs-lookup"><span data-stu-id="2147a-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="2147a-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Cada linha de saída depende de uma única linha de entrada da saudação à esquerda e hello direita com hello mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="2147a-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="2147a-185">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2147a-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
