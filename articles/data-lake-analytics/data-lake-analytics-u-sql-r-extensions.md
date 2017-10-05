---
title: Estender scripts U-SQL com R no Azure Data Lake Analytics | Microsoft Docs
description: "Saiba como executar o código R em Scripts U-SQL"
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
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="35244-103">Tutorial: introdução à extensão do U-SQL com o R</span><span class="sxs-lookup"><span data-stu-id="35244-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="35244-104">O exemplo a seguir ilustra as etapas básicas para implantar código R:</span><span class="sxs-lookup"><span data-stu-id="35244-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="35244-105">Use a instrução `REFERENCE ASSEMBLY` para habilitar as extensões R para o Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="35244-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="35244-106">Use a operação ` REDUCE` para particionar os dados de entrada em uma chave.</span><span class="sxs-lookup"><span data-stu-id="35244-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="35244-107">As extensões R para U-SQL incluem um redutor interno (`Extension.R.Reducer`) que executa o código R em cada vértice atribuído ao redutor.</span><span class="sxs-lookup"><span data-stu-id="35244-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="35244-108">O uso de quadros de dados nomeados dedicados chamados `inputFromUSQL` e `outputToUSQL ` respectivamente para passar dados entre U-SQL e R. Os nomes de identificador DataFrame de entrada e saída são fixos (ou seja, os usuários não podem alterar esses nomes predefinidos dos identificadores DataFrame de entrada e saída).</span><span class="sxs-lookup"><span data-stu-id="35244-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="35244-109">Inserindo código R no script U-SQL</span><span class="sxs-lookup"><span data-stu-id="35244-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="35244-110">Você pode embutir o código R no script U-SQL usando o parâmetro de comando do `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="35244-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="35244-111">Por exemplo, você pode declarar o script R como uma variável de cadeia de caracteres e passá-lo como um parâmetro para o Redutor.</span><span class="sxs-lookup"><span data-stu-id="35244-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="35244-112">Manter o código R em um arquivo separado e fazer referência a ela no script U-SQL</span><span class="sxs-lookup"><span data-stu-id="35244-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="35244-113">O exemplo a seguir ilustra um uso mais complexo.</span><span class="sxs-lookup"><span data-stu-id="35244-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="35244-114">Nesse caso, o código R é implantado como um RESOURCE que é o script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="35244-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="35244-115">Salve esse código R como um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="35244-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="35244-116">Use um script U-SQL para implantar esse script R com a instrução DEPLOY RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="35244-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="35244-117">Como o R se integra com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="35244-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="35244-118">Tipos de dados</span><span class="sxs-lookup"><span data-stu-id="35244-118">Datatypes</span></span>
* <span data-ttu-id="35244-119">As colunas numéricas e de cadeia de caracteres do U-SQL são convertidas no estado em que se encontram entre R DataFrame e U-SQL [tipos com suporte: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="35244-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="35244-120">Não há suporte para o tipo de dados `Factor` em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="35244-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="35244-121">`byte[]` deve ser serializado como uma `string` codificada em base64.</span><span class="sxs-lookup"><span data-stu-id="35244-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="35244-122">As cadeias de caracteres de U-SQL poderão ser convertidas em fatores no código R depois que U-SQL criar quadro de dados de entrada R ou configurando o parâmetro redutor `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="35244-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="35244-123">Esquemas</span><span class="sxs-lookup"><span data-stu-id="35244-123">Schemas</span></span>
* <span data-ttu-id="35244-124">Conjuntos de dados U-SQL não podem ter nomes de coluna duplicados.</span><span class="sxs-lookup"><span data-stu-id="35244-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="35244-125">Nomes de coluna de conjuntos de dados U-SQL devem ser cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="35244-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="35244-126">Nomes de coluna devem ser iguais em scripts U-SQL e R.</span><span class="sxs-lookup"><span data-stu-id="35244-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="35244-127">A coluna somente leitura não pode fazer parte do dataframe de saída.</span><span class="sxs-lookup"><span data-stu-id="35244-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="35244-128">Porque colunas somente leitura são injetadas automaticamente na tabela U-SQL caso ela faça parte do esquema de saída do UDO.</span><span class="sxs-lookup"><span data-stu-id="35244-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="35244-129">Limitações funcionais</span><span class="sxs-lookup"><span data-stu-id="35244-129">Functional limitations</span></span>
* <span data-ttu-id="35244-130">O mecanismo R não pode ser instanciado duas vezes no mesmo processo.</span><span class="sxs-lookup"><span data-stu-id="35244-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="35244-131">No momento, o U-SQL não dá suporte a UDOs combinadores para previsão usando modelos particionados gerados com UDOs redutores.</span><span class="sxs-lookup"><span data-stu-id="35244-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="35244-132">Os usuários podem declarar os modelos particionados como recurso e usá-los no Script de R (consulte o código de exemplo `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="35244-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="35244-133">Versões do R</span><span class="sxs-lookup"><span data-stu-id="35244-133">R Versions</span></span>
<span data-ttu-id="35244-134">Somente o R 3.2.2 tem suporte.</span><span class="sxs-lookup"><span data-stu-id="35244-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="35244-135">Módulos de R padrão</span><span class="sxs-lookup"><span data-stu-id="35244-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="35244-136">Limitações de tamanho de Entrada e Saída</span><span class="sxs-lookup"><span data-stu-id="35244-136">Input and Output size limitations</span></span>
<span data-ttu-id="35244-137">Cada vértice tem uma quantidade limitada de memória atribuída a ele.</span><span class="sxs-lookup"><span data-stu-id="35244-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="35244-138">Já que os DataFrames de entrada e de saída devem existir na memória no código R, o tamanho total para a entrada e saída não pode exceder os 500 MB.</span><span class="sxs-lookup"><span data-stu-id="35244-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="35244-139">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="35244-139">Sample Code</span></span>
<span data-ttu-id="35244-140">Mais código de exemplo está disponível em sua conta do Data Lake Store depois de você instalar as Extensões de Análise Avançada do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="35244-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="35244-141">O caminho para mais código de exemplo é: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="35244-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="35244-142">Implantar módulos R personalizados com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="35244-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="35244-143">Primeiro, crie um módulo R personalizado, compacte-o e, em seguida, carregue o arquivo de módulo R personalizado compactado em seu repositório do ADL.</span><span class="sxs-lookup"><span data-stu-id="35244-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="35244-144">No exemplo, carregaremos magittr_1.5.zip na raiz da conta do ADLS padrão para a conta do ADLA que estamos usando.</span><span class="sxs-lookup"><span data-stu-id="35244-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="35244-145">Depois que você carregar o módulo no repositório do ADL, declare-o e use DEPLOY RESOURCE para disponibilizá-lo em seu script U-SQL e chame `install.packages` para instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="35244-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
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

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="35244-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35244-146">Next Steps</span></span>
* [<span data-ttu-id="35244-147">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="35244-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="35244-148">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35244-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="35244-149">Usar funções da janela do U-SQL para trabalhos de análise do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="35244-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
