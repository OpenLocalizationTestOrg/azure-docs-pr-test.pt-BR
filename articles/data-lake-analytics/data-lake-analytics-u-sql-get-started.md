---
title: "Introdução à linguagem U-SQL | Microsoft Docs"
description: "Conheça os fundamentos de saudação da saudação linguagem U-SQL."
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
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="ae5ea-103">Introdução ao U-SQL</span><span class="sxs-lookup"><span data-stu-id="ae5ea-103">Get started with U-SQL</span></span>
<span data-ttu-id="ae5ea-104">U-SQL é uma linguagem que combina SQL declarativa com fundamental c# toolet você processar dados em qualquer escala.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="ae5ea-105">Olá escalonável e de consulta distribuída com o recurso de U-SQL, você pode analisar com eficiência dados em repositórios relacionais, como o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="ae5ea-106">Com o U-SQL, você pode processar dados não estruturados aplicando o esquema na leitura e inserindo lógica personalizada e UDFs.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="ae5ea-107">Além disso, U-SQL inclui extensibilidade que lhe dá controle refinado como tooexecute em escala.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="ae5ea-108">Recursos de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="ae5ea-108">Learning resources</span></span>

* <span data-ttu-id="ae5ea-109">Olá [U-SQL Tutorial](http://aka.ms/usqltutorial) fornece uma passo a passo guiado da maioria dos idiomas Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="ae5ea-110">Este documento é recomendado para todos os desenvolvedores que desejam toolearn U-SQL de leitura.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="ae5ea-111">Para obter informações detalhadas sobre Olá **sintaxe de linguagem SQL U**, consulte Olá [referência de linguagem SQL U](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="ae5ea-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="ae5ea-112">Olá toounderstand **filosofia de design U-SQL**, consulte a postagem do blog do Visual Studio Olá [apresentando U-SQL – A linguagem que torna fácil de processamento de dados grande](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="ae5ea-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae5ea-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae5ea-113">Prerequisites</span></span>

<span data-ttu-id="ae5ea-114">Antes de passar pelos exemplos Olá U-SQL neste documento, ler e concluir [Tutorial: scripts de desenvolver U-SQL usando o Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ae5ea-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="ae5ea-115">Esse tutorial explica os mecanismos de saudação do uso de U-SQL com o Azure Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="ae5ea-116">Seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="ae5ea-116">Your first U-SQL script</span></span>

<span data-ttu-id="ae5ea-117">Olá script U-SQL a seguir é simple e permite explorar o idioma de saudação U-SQL muitos aspectos.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="ae5ea-118">Esse script não possui nenhuma etapa de transformação.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="ae5ea-119">Ele lê a partir do arquivo de origem Olá chamado `SearchLog.tsv`, schematizes-lo e grava Olá linhas em um arquivo chamado SearchLog primeiro-u sql.csv.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="ae5ea-120">Observe Olá ponto de interrogação próximo toohello tipo de dados em Olá `Duration` campo.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="ae5ea-121">Isso significa que Olá `Duration` campo pode ser nulo.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="ae5ea-122">Principais conceitos</span><span class="sxs-lookup"><span data-stu-id="ae5ea-122">Key concepts</span></span>
* <span data-ttu-id="ae5ea-123">**Variáveis de conjunto de linhas**: cada expressão de consulta que produz um conjunto de linhas pode ser atribuída tooa variável.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="ae5ea-124">U-SQL segue o padrão de nomenclatura variável Olá T-SQL (`@searchlog`, por exemplo) no script hello.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="ae5ea-125">Olá **EXTRAIR** lê dados de um arquivo de palavra-chave e define o esquema de saudação na leitura.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="ae5ea-126">`Extractors.Tsv` é um extrator U-SQL interno para arquivos de valores separados por tabulação.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="ae5ea-127">Você pode desenvolver extratores personalizados.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="ae5ea-128">Olá **saída** grava os dados de um arquivo de tooa do conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="ae5ea-129">`Outputters.Csv()`é um toocreate de outputter U-SQL interna de um arquivo de valores separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="ae5ea-130">Você pode desenvolver outputters personalizados.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="ae5ea-131">Caminhos de arquivo</span><span class="sxs-lookup"><span data-stu-id="ae5ea-131">File paths</span></span>

<span data-ttu-id="ae5ea-132">Olá EXTRAIR e declarações de saída usam caminhos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="ae5ea-133">Os caminhos de arquivo podem ser absolutos ou relativos:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="ae5ea-134">Esse caminho de arquivo absoluto seguir refere-se tooa arquivo em um repositório do Data Lake chamado `mystore`:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="ae5ea-135">O caminho de arquivo a seguir começa com `"/"`.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="ae5ea-136">Ela se refere a arquivos tooa na conta de repositório Data Lake saudação padrão:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="ae5ea-137">Usar variáveis escalares</span><span class="sxs-lookup"><span data-stu-id="ae5ea-137">Use scalar variables</span></span>

<span data-ttu-id="ae5ea-138">Você pode usar variáveis escalares como toomake bem a manutenção do seu script mais fácil.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="ae5ea-139">script U-SQL anterior de saudação também pode ser escrito como:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-139">hello previous U-SQL script can also be written as:</span></span>

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
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="ae5ea-140">Transformar conjuntos de linhas</span><span class="sxs-lookup"><span data-stu-id="ae5ea-140">Transform rowsets</span></span>

<span data-ttu-id="ae5ea-141">Use **selecione** tootransform conjuntos de linhas:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-141">Use **SELECT** tootransform rowsets:</span></span>

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
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="ae5ea-142">Olá a cláusula WHERE usa um [c# booliana](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae5ea-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="ae5ea-143">Você pode usar o hello c# expressão idioma toodo suas próprias expressões e funções.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="ae5ea-144">Você pode até mesmo executar uma filtragem mais complexa combinando-os com associações lógicas (ANDs) e desassociações (ORs).</span><span class="sxs-lookup"><span data-stu-id="ae5ea-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="ae5ea-145">Olá script a seguir usa o método de DateTime.Parse() hello e um conjunto.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="ae5ea-146">consulta segundo Hello está operando no resultado de saudação do hello primeiro conjunto de linhas, que cria uma composição da saudação dois filtros.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="ae5ea-147">Também é possível reutilizar um nome de variável e nomes de saudação passam lexicalmente.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="ae5ea-148">Agregar conjuntos de linhas</span><span class="sxs-lookup"><span data-stu-id="ae5ea-148">Aggregate rowsets</span></span>
<span data-ttu-id="ae5ea-149">Fornece U-SQL Olá familiar ORDER BY, GROUP BY e agregações.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="ae5ea-150">Olá consulta a seguir localiza a duração total da saudação por região e exibe superior Olá cinco durações na ordem.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="ae5ea-151">Conjuntos de linhas U-SQL não preservar a ordem para consulta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="ae5ea-152">Portanto, tooorder uma saída, você precisa tooadd instrução ORDER BY toohello saída:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="ae5ea-153">Olá U-SQL ORDER BY cláusula requer usando a cláusula de busca de saudação em uma expressão de seleção.</span><span class="sxs-lookup"><span data-stu-id="ae5ea-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="ae5ea-154">a cláusula de ter U-SQL de Olá pode ser usado toorestrict Olá saída toogroups que satisfazem a condição HAVING hello:</span><span class="sxs-lookup"><span data-stu-id="ae5ea-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="ae5ea-155">Para cenários de agregação avançadas, consulte a documentação de referência Olá Olá U-SQL para [agregar, analítico e fazer referência a funções](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="ae5ea-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae5ea-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae5ea-156">Next steps</span></span>
* [<span data-ttu-id="ae5ea-157">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ae5ea-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ae5ea-158">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae5ea-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
