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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Tutorial: introdução à extensão do U-SQL com o R

saudação de exemplo a seguir ilustra as etapas básicas para implantar o código R hello:
* Saudação de uso `REFERENCE ASSEMBLY` extensões de tooenable R de instrução para Olá Script U-SQL.
* Use o` REDUCE` dados em uma chave de entrada de saudação do toopartition de operação.
* extensões de saudação R para U-SQL incluem um redutor interno (`Extension.R.Reducer`) que executa o código R em Redutor de toohello cada vértice atribuído. 
* Uso de dedicado denominado quadros de dados chamados `inputFromUSQL` e `outputToUSQL `respectivamente toopass dados entre U-SQL e R. entrada e saída corrigidos os nomes de identificador DataFrame (ou seja, os usuários não podem alterar esses nomes predefinidos de entrada e DataFrame de saída identificadores).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>Inserindo código R em Olá script U-SQL

Você pode o código embutido Olá R o script U-SQL usando o parâmetro de comando de saudação do hello `Extension.R.Reducer`. Por exemplo, você pode declarar Olá script R como uma variável de cadeia de caracteres e passá-lo como um parâmetro toohello Redutor.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Manter o código de saudação R em um arquivo separado e fazer referência a ela script hello U-SQL

saudação de exemplo a seguir ilustra um uso mais complexo. Nesse caso, o código Olá R é implantado como um recurso que é hello script U-SQL.

Salve esse código R como um arquivo separado.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Use um toodeploy de script U-SQL script R com hello instrução IMPLANTAR recursos.

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

## <a name="how-r-integrates-with-u-sql"></a>Como o R se integra com o U-SQL

### <a name="datatypes"></a>Tipos de dados
* As colunas numéricas e de cadeia de caracteres do U-SQL são convertidas no estado em que se encontram entre R DataFrame e U-SQL [tipos com suporte: `double`, `string`, `bool`, `integer`, `byte`].
* Olá `Factor` não há suporte para o tipo de dados em U-SQL.
* `byte[]` deve ser serializado como uma `string` codificada em base64.
* Cadeias de caracteres de U-SQL podem ser convertido toofactors no código de R, quando U-SQL create R dataframe de entrada ou pelo parâmetro de Redutor Olá configuração `stringsAsFactors: true`.

### <a name="schemas"></a>Esquemas
* Conjuntos de dados U-SQL não podem ter nomes de coluna duplicados.
* Nomes de coluna de conjuntos de dados U-SQL devem ser cadeias de caracteres.
* Nomes de coluna devem ser Olá mesmo nos scripts U-SQL e R.
* Coluna somente leitura não pode ser parte da saudação dataframe de saída. Como colunas somente leitura são automaticamente inseridas novamente na tabela de U-SQL de saudação se ele faz parte do esquema de saída do UDO.

### <a name="functional-limitations"></a>Limitações funcionais
* Olá mecanismo R não pode ser instanciado duas vezes no mesmo processo de hello. 
* No momento, o U-SQL não dá suporte a UDOs combinadores para previsão usando modelos particionados gerados com UDOs redutores. Os usuários podem declarar modelos Olá particionada como recurso e usá-los em seu Script de R (consulte o código de exemplo `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>Versões do R
Somente o R 3.2.2 tem suporte.

### <a name="standard-r-modules"></a>Módulos de R padrão

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

### <a name="input-and-output-size-limitations"></a>Limitações de tamanho de Entrada e Saída
Cada vértice tem uma quantidade limitada de memória atribuída tooit. Porque hello quadros de dados de entrada e saídos devem existir na memória no código Olá R, o tamanho total Olá Olá entrada e saída não pode exceder 500 MB.

### <a name="sample-code"></a>Exemplo de código
Mais código de exemplo está disponível em sua conta do repositório Data Lake depois de instalar extensões de U-SQL Advanced Analytics hello. caminho de saudação para mais de exemplo de código é: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Implantar módulos R personalizados com o U-SQL

Primeiro, crie um módulo personalizado de R e zip-lo e carregue Olá compactado armazenamento de publicitário tooyour do arquivo de módulo personalizado R. Exemplo hello, podemos carregará magittr_1.5.zip toohello raiz da conta ADLS de padrão de saudação do hello conta ADLA que estamos usando. Quando você carregar o repositório de tooADL módulo hello, declare-o como usar o recurso IMPLANTAR toomake disponível no seu script U-SQL e chamar `install.packages` tooinstall-lo.

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

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Usar funções da janela do U-SQL para trabalhos de análise do Azure Data Lake](data-lake-analytics-use-window-functions.md)
