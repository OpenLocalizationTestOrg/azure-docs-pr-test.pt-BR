---
title: "Introdução à linguagem U-SQL | Microsoft Docs"
description: "Aprenda os conceitos básicos da linguagem U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="5efa5-103">Introdução ao U-SQL</span><span class="sxs-lookup"><span data-stu-id="5efa5-103">Get started with U-SQL</span></span>
<span data-ttu-id="5efa5-104">U-SQL é uma linguagem que combina o SQL declarativo com o C# imperativo para permitir que você processe dados em qualquer escala.</span><span class="sxs-lookup"><span data-stu-id="5efa5-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="5efa5-105">Por meio da capacidade de consulta distribuída escalonável do U-SQL, você pode analisar, de modo eficiente, dados entre repositórios relacionais como o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="5efa5-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="5efa5-106">Com o U-SQL, você pode processar dados não estruturados aplicando o esquema na leitura e inserindo lógica personalizada e UDFs.</span><span class="sxs-lookup"><span data-stu-id="5efa5-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="5efa5-107">Além disso, o U-SQL inclui extensibilidade que lhe dá controle refinado sobre como executar em escala.</span><span class="sxs-lookup"><span data-stu-id="5efa5-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="5efa5-108">Recursos de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="5efa5-108">Learning resources</span></span>

* <span data-ttu-id="5efa5-109">O [Tutorial do U-SQL](http://aka.ms/usqltutorial) fornece um passo a passo guiado sobre a maior parte da linguagem U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5efa5-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="5efa5-110">A leitura deste documento é recomendada para todos os desenvolvedores que desejam aprender sobre U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5efa5-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="5efa5-111">Para obter informações detalhadas sobre a **sintaxe da linguagem U-SQL**, consulte a [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348) (Referência da linguagem U-SQL).</span><span class="sxs-lookup"><span data-stu-id="5efa5-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="5efa5-112">Para entender a **filosofia de design do U-SQL**, confira a postagem do blog do Visual Studio [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/) (Apresentando o U-SQL – Uma linguagem que torna fácil o processamento de Big Data).</span><span class="sxs-lookup"><span data-stu-id="5efa5-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5efa5-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5efa5-113">Prerequisites</span></span>

<span data-ttu-id="5efa5-114">Antes de percorrer os exemplos do U-SQL nesse documento, leia e conclua o [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5efa5-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="5efa5-115">Esse tutorial explica a mecânica do uso do U-SQL com as Ferramentas do Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5efa5-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="5efa5-116">Seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="5efa5-116">Your first U-SQL script</span></span>

<span data-ttu-id="5efa5-117">O script U-SQL a seguir é simples e nos permite explorar muitos aspectos da linguagem U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5efa5-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="5efa5-118">Esse script não possui nenhuma etapa de transformação.</span><span class="sxs-lookup"><span data-stu-id="5efa5-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="5efa5-119">Ele faz a leitura do arquivo de origem chamado `SearchLog.tsv`, o esquematiza e grava o conjunto de linhas de volta em um arquivo chamado SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="5efa5-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="5efa5-120">Observe o ponto de interrogação ao lado do tipo de dados no campo `Duration`.</span><span class="sxs-lookup"><span data-stu-id="5efa5-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="5efa5-121">Isso significa que o campo `Duration` pode ser nulo.</span><span class="sxs-lookup"><span data-stu-id="5efa5-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="5efa5-122">Principais conceitos</span><span class="sxs-lookup"><span data-stu-id="5efa5-122">Key concepts</span></span>
* <span data-ttu-id="5efa5-123">**Variáveis de conjunto de linhas**: cada expressão de consulta que produz um conjunto de linhas pode ser atribuído a uma variável.</span><span class="sxs-lookup"><span data-stu-id="5efa5-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="5efa5-124">O U-SQL segue o padrão de nomenclatura de variável do T-SQL (`@searchlog`, por exemplo) no script.</span><span class="sxs-lookup"><span data-stu-id="5efa5-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="5efa5-125">A palavra-chave **EXTRACT** lê dados de um arquivo e define o esquema na leitura.</span><span class="sxs-lookup"><span data-stu-id="5efa5-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="5efa5-126">`Extractors.Tsv` é um extrator U-SQL interno para arquivos de valores separados por tabulação.</span><span class="sxs-lookup"><span data-stu-id="5efa5-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="5efa5-127">Você pode desenvolver extratores personalizados.</span><span class="sxs-lookup"><span data-stu-id="5efa5-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="5efa5-128">**OUTPUT** grava dados de um conjunto de linhas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="5efa5-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="5efa5-129">`Outputters.Csv()` é um outputter U-SQL interno para criar um arquivo de valores separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="5efa5-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="5efa5-130">Você pode desenvolver outputters personalizados.</span><span class="sxs-lookup"><span data-stu-id="5efa5-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="5efa5-131">Caminhos de arquivo</span><span class="sxs-lookup"><span data-stu-id="5efa5-131">File paths</span></span>

<span data-ttu-id="5efa5-132">As instruções EXTRACT e OUTPUT usam caminhos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5efa5-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="5efa5-133">Os caminhos de arquivo podem ser absolutos ou relativos:</span><span class="sxs-lookup"><span data-stu-id="5efa5-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="5efa5-134">O caminho de arquivo absoluto a seguir se refere a um arquivo em um Data Lake Store chamado `mystore`:</span><span class="sxs-lookup"><span data-stu-id="5efa5-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="5efa5-135">O caminho de arquivo a seguir começa com `"/"`.</span><span class="sxs-lookup"><span data-stu-id="5efa5-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="5efa5-136">Ele se refere a um arquivo na conta padrão do Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="5efa5-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="5efa5-137">Usar variáveis escalares</span><span class="sxs-lookup"><span data-stu-id="5efa5-137">Use scalar variables</span></span>

<span data-ttu-id="5efa5-138">Você pode usar variáveis escalares também para facilitar a manutenção do seu script.</span><span class="sxs-lookup"><span data-stu-id="5efa5-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="5efa5-139">O script U-SQL anterior também pode ser escrito da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5efa5-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="5efa5-140">Transformar conjuntos de linhas</span><span class="sxs-lookup"><span data-stu-id="5efa5-140">Transform rowsets</span></span>

<span data-ttu-id="5efa5-141">Use **SELECT** para transformar conjuntos de linhas:</span><span class="sxs-lookup"><span data-stu-id="5efa5-141">Use **SELECT** to transform rowsets:</span></span>

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="5efa5-142">A cláusula WHERE usa uma [expressão booliana C#](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="5efa5-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="5efa5-143">Você pode usar a linguagem de expressão do C# para fazer suas próprias expressões e funções.</span><span class="sxs-lookup"><span data-stu-id="5efa5-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="5efa5-144">Você pode até mesmo executar uma filtragem mais complexa combinando-os com associações lógicas (ANDs) e desassociações (ORs).</span><span class="sxs-lookup"><span data-stu-id="5efa5-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="5efa5-145">O script a seguir usa o método DateTime.Parse() e um conjunto.</span><span class="sxs-lookup"><span data-stu-id="5efa5-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="5efa5-146">A segunda consulta está operando no resultado do primeiro conjunto de linhas, que cria uma composição dos dois filtros.</span><span class="sxs-lookup"><span data-stu-id="5efa5-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="5efa5-147">Também é possível reutilizar um nome de variável; o escopo dos nomes é definido lexicalmente.</span><span class="sxs-lookup"><span data-stu-id="5efa5-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="5efa5-148">Agregar conjuntos de linhas</span><span class="sxs-lookup"><span data-stu-id="5efa5-148">Aggregate rowsets</span></span>
<span data-ttu-id="5efa5-149">O U-SQL fornece a você as conhecidas funções ORDER BY, GROUP BY e agregações.</span><span class="sxs-lookup"><span data-stu-id="5efa5-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="5efa5-150">A consulta a seguir localiza a duração total por região e então exibe as cinco maiores durações, na ordem.</span><span class="sxs-lookup"><span data-stu-id="5efa5-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="5efa5-151">Os conjuntos de linhas do U-SQL não mantêm a ordem para a consulta seguinte.</span><span class="sxs-lookup"><span data-stu-id="5efa5-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="5efa5-152">Portanto, para solicitar uma saída, você precisa adicionar ORDER BY à instrução OUTPUT:</span><span class="sxs-lookup"><span data-stu-id="5efa5-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="5efa5-153">A cláusula ORDER BY do U-SQL requer o uso da cláusula FETCH em uma expressão SELECT.</span><span class="sxs-lookup"><span data-stu-id="5efa5-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="5efa5-154">A cláusula HAVING do U-SQL pode ser usada para restringir a saída aos grupos que satisfazem a condição de HAVING:</span><span class="sxs-lookup"><span data-stu-id="5efa5-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="5efa5-155">Para cenários de agregação avançados, consulte a documentação de referência do U-SQL sobre as [funções de agregação, análise e referência](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="5efa5-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5efa5-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5efa5-156">Next steps</span></span>
* [<span data-ttu-id="5efa5-157">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5efa5-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="5efa5-158">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5efa5-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
