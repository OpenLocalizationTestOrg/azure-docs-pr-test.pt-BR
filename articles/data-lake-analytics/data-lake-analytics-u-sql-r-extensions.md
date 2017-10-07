---
title: "aaaExtend U-SQL de scripts do R na análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como toorun R código nos Scripts U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="1ecb5-103">Tutorial: introdução à extensão do U-SQL com o R</span><span class="sxs-lookup"><span data-stu-id="1ecb5-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="1ecb5-104">saudação de exemplo a seguir ilustra as etapas básicas para implantar o código R hello:</span><span class="sxs-lookup"><span data-stu-id="1ecb5-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="1ecb5-105">Saudação de uso `REFERENCE ASSEMBLY` extensões de tooenable R de instrução para Olá Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="1ecb5-106">Use o` REDUCE` dados em uma chave de entrada de saudação do toopartition de operação.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="1ecb5-107">extensões de saudação R para U-SQL incluem um redutor interno (`Extension.R.Reducer`) que executa o código R em Redutor de toohello cada vértice atribuído.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="1ecb5-108">Uso de dedicado denominado quadros de dados chamados `inputFromUSQL` e `outputToUSQL `respectivamente toopass dados entre U-SQL e R. entrada e saída corrigidos os nomes de identificador DataFrame (ou seja, os usuários não podem alterar esses nomes predefinidos de entrada e DataFrame de saída identificadores).</span><span class="sxs-lookup"><span data-stu-id="1ecb5-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="1ecb5-109">Inserindo código R em Olá script U-SQL</span><span class="sxs-lookup"><span data-stu-id="1ecb5-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="1ecb5-110">Você pode o código embutido Olá R o script U-SQL usando o parâmetro de comando de saudação do hello `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="1ecb5-111">Por exemplo, você pode declarar Olá script R como uma variável de cadeia de caracteres e passá-lo como um parâmetro toohello Redutor.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="1ecb5-112">Manter o código de saudação R em um arquivo separado e fazer referência a ela script hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="1ecb5-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="1ecb5-113">saudação de exemplo a seguir ilustra um uso mais complexo.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="1ecb5-114">Nesse caso, o código Olá R é implantado como um recurso que é hello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="1ecb5-115">Salve esse código R como um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="1ecb5-116">Use um toodeploy de script U-SQL script R com hello instrução IMPLANTAR recursos.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="1ecb5-117">Como o R se integra com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="1ecb5-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="1ecb5-118">Tipos de dados</span><span class="sxs-lookup"><span data-stu-id="1ecb5-118">Datatypes</span></span>
* <span data-ttu-id="1ecb5-119">As colunas numéricas e de cadeia de caracteres do U-SQL são convertidas no estado em que se encontram entre R DataFrame e U-SQL [tipos com suporte: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="1ecb5-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="1ecb5-120">Olá `Factor` não há suporte para o tipo de dados em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="1ecb5-121">`byte[]` deve ser serializado como uma `string` codificada em base64.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="1ecb5-122">Cadeias de caracteres de U-SQL podem ser convertido toofactors no código de R, quando U-SQL create R dataframe de entrada ou pelo parâmetro de Redutor Olá configuração `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="1ecb5-123">Esquemas</span><span class="sxs-lookup"><span data-stu-id="1ecb5-123">Schemas</span></span>
* <span data-ttu-id="1ecb5-124">Conjuntos de dados U-SQL não podem ter nomes de coluna duplicados.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="1ecb5-125">Nomes de coluna de conjuntos de dados U-SQL devem ser cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="1ecb5-126">Nomes de coluna devem ser Olá mesmo nos scripts U-SQL e R.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="1ecb5-127">Coluna somente leitura não pode ser parte da saudação dataframe de saída.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="1ecb5-128">Como colunas somente leitura são automaticamente inseridas novamente na tabela de U-SQL de saudação se ele faz parte do esquema de saída do UDO.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="1ecb5-129">Limitações funcionais</span><span class="sxs-lookup"><span data-stu-id="1ecb5-129">Functional limitations</span></span>
* <span data-ttu-id="1ecb5-130">Olá mecanismo R não pode ser instanciado duas vezes no mesmo processo de hello.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="1ecb5-131">No momento, o U-SQL não dá suporte a UDOs combinadores para previsão usando modelos particionados gerados com UDOs redutores.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="1ecb5-132">Os usuários podem declarar modelos Olá particionada como recurso e usá-los em seu Script de R (consulte o código de exemplo `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="1ecb5-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="1ecb5-133">Versões do R</span><span class="sxs-lookup"><span data-stu-id="1ecb5-133">R Versions</span></span>
<span data-ttu-id="1ecb5-134">Somente o R 3.2.2 tem suporte.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="1ecb5-135">Módulos de R padrão</span><span class="sxs-lookup"><span data-stu-id="1ecb5-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="1ecb5-136">Limitações de tamanho de Entrada e Saída</span><span class="sxs-lookup"><span data-stu-id="1ecb5-136">Input and Output size limitations</span></span>
<span data-ttu-id="1ecb5-137">Cada vértice tem uma quantidade limitada de memória atribuída tooit.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="1ecb5-138">Porque hello quadros de dados de entrada e saídos devem existir na memória no código Olá R, o tamanho total Olá Olá entrada e saída não pode exceder 500 MB.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="1ecb5-139">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="1ecb5-139">Sample Code</span></span>
<span data-ttu-id="1ecb5-140">Mais código de exemplo está disponível em sua conta do repositório Data Lake depois de instalar extensões de U-SQL Advanced Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="1ecb5-141">caminho de saudação para mais de exemplo de código é: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="1ecb5-142">Implantar módulos R personalizados com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="1ecb5-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="1ecb5-143">Primeiro, crie um módulo personalizado de R e zip-lo e carregue Olá compactado armazenamento de publicitário tooyour do arquivo de módulo personalizado R.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="1ecb5-144">Exemplo hello, podemos carregará magittr_1.5.zip toohello raiz da conta ADLS de padrão de saudação do hello conta ADLA que estamos usando.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="1ecb5-145">Quando você carregar o repositório de tooADL módulo hello, declare-o como usar o recurso IMPLANTAR toomake disponível no seu script U-SQL e chamar `install.packages` tooinstall-lo.</span><span class="sxs-lookup"><span data-stu-id="1ecb5-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="1ecb5-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ecb5-146">Next Steps</span></span>
* [<span data-ttu-id="1ecb5-147">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1ecb5-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="1ecb5-148">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ecb5-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="1ecb5-149">Usar funções da janela do U-SQL para trabalhos de análise do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1ecb5-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
