---
title: "scripts de aaaExtend U-SQL com Python na análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como toorun Python código nos Scripts U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="39212-103">Tutorial: introdução à extensão do U-SQL com o Python</span><span class="sxs-lookup"><span data-stu-id="39212-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="39212-104">Extensões de Python para U-SQL permitem que os desenvolvedores tooperform paralela em grande escala a execução de código Python.</span><span class="sxs-lookup"><span data-stu-id="39212-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="39212-105">saudação de exemplo a seguir ilustra as etapas básicas hello:</span><span class="sxs-lookup"><span data-stu-id="39212-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="39212-106">Saudação de uso `REFERENCE ASSEMBLY` extensões de Python de tooenable de instrução para Olá Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="39212-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="39212-107">Usando Olá `REDUCE` dados em uma chave de entrada de saudação do toopartition de operação</span><span class="sxs-lookup"><span data-stu-id="39212-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="39212-108">extensões do Python para U-SQL Hello incluem um redutor interno (`Extension.Python.Reducer`) que executa o código Python em Redutor de toohello cada vértice atribuído</span><span class="sxs-lookup"><span data-stu-id="39212-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="39212-109">Olá script U-SQL contém código Python Olá inserido que tem uma função chamada `usqlml_main` que aceita um pandas DataFrame como entrada e retorna um pandas DataFrame como saída.</span><span class="sxs-lookup"><span data-stu-id="39212-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="39212-110">Como o Python se integra com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="39212-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="39212-111">Tipos de dados</span><span class="sxs-lookup"><span data-stu-id="39212-111">Datatypes</span></span>

* <span data-ttu-id="39212-112">As cadeias de caracteres e colunas numéricas do U-SQL são convertidas como estão entre Pandas e U-SQL</span><span class="sxs-lookup"><span data-stu-id="39212-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="39212-113">U-SQL nulos são convertido tooand de Pandas `NA` valores</span><span class="sxs-lookup"><span data-stu-id="39212-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="39212-114">Esquemas</span><span class="sxs-lookup"><span data-stu-id="39212-114">Schemas</span></span>

* <span data-ttu-id="39212-115">Os vetores de índice no Pandas não têm suporte no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="39212-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="39212-116">Todos os quadros de dados de entrada na função de Python Olá sempre tem um índice numérico de 64 bits de 0 até Olá número de linhas menos 1.</span><span class="sxs-lookup"><span data-stu-id="39212-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="39212-117">Conjuntos de dados U-SQL não podem ter nomes de coluna duplicados</span><span class="sxs-lookup"><span data-stu-id="39212-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="39212-118">Nomes de coluna de conjuntos de dados U-SQL que não são cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="39212-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="39212-119">Versões do Python</span><span class="sxs-lookup"><span data-stu-id="39212-119">Python Versions</span></span>
<span data-ttu-id="39212-120">Há suporte somente para o Python 3.5.1 (compilado para Windows).</span><span class="sxs-lookup"><span data-stu-id="39212-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="39212-121">Módulos de Python Standard</span><span class="sxs-lookup"><span data-stu-id="39212-121">Standard Python modules</span></span>
<span data-ttu-id="39212-122">Todos os módulos Python saudação padrão são incluídos.</span><span class="sxs-lookup"><span data-stu-id="39212-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="39212-123">Módulos de Python adicionais</span><span class="sxs-lookup"><span data-stu-id="39212-123">Additional Python modules</span></span>
<span data-ttu-id="39212-124">Além de hello bibliotecas Python padrão, várias bibliotecas python usadas estão incluídas:</span><span class="sxs-lookup"><span data-stu-id="39212-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="39212-125">Mensagens de Exceção</span><span class="sxs-lookup"><span data-stu-id="39212-125">Exception Messages</span></span>
<span data-ttu-id="39212-126">Atualmente, uma exceção no código Python aparece como falha genérica de vértice.</span><span class="sxs-lookup"><span data-stu-id="39212-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="39212-127">Olá futuras, mensagens de erro do trabalho U-SQL Olá exibirá mensagem de exceção saudação do Python.</span><span class="sxs-lookup"><span data-stu-id="39212-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="39212-128">Limitações de tamanho de Entrada e Saída</span><span class="sxs-lookup"><span data-stu-id="39212-128">Input and Output size limitations</span></span>
<span data-ttu-id="39212-129">Cada vértice tem uma quantidade limitada de memória atribuída tooit.</span><span class="sxs-lookup"><span data-stu-id="39212-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="39212-130">Atualmente, esse limite é de 6 GB para um AU.</span><span class="sxs-lookup"><span data-stu-id="39212-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="39212-131">Porque hello quadros de dados de entrada e saídos devem existir na memória no código do Python hello, o tamanho total Olá Olá entrada e saída não pode exceder 6 GB.</span><span class="sxs-lookup"><span data-stu-id="39212-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="39212-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="39212-132">See also</span></span>
* [<span data-ttu-id="39212-133">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="39212-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="39212-134">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39212-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="39212-135">Usar funções da janela do U-SQL para trabalhos de análise do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="39212-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

