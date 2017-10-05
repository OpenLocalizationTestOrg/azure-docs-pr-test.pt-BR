---
title: Criar recursos para os dados em um cluster Hadoop usando as consultas do Hive | Microsoft Docs
description: Exemplos de consultas de Hive que geram recursos em dados armazenados em um cluster Hadoop do Azure HDInsight.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e027a6ffcb63868be13432870e484c5cbf2eef4b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="94353-103">Criar recursos para os dados em um cluster Hadoop usando as consultas do Hive</span><span class="sxs-lookup"><span data-stu-id="94353-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="94353-104">Este documento mostra como criar recursos para os dados armazenados em um cluster Hadoop do Azure HDInsight usando consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="94353-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="94353-105">Essas consultas de Hive usam UDFs (funções definidas pelo usuário) de Hive incorporadas, Os scripts para eles são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="94353-105">These Hive queries use embedded Hive User Defined Functions (UDFs), the scripts for which are provided.</span></span>

<span data-ttu-id="94353-106">As operações necessárias para criar recursos podem ter uso intensivo de memória.</span><span class="sxs-lookup"><span data-stu-id="94353-106">The operations needed to create features can be memory intensive.</span></span> <span data-ttu-id="94353-107">O desempenho das consultas do Hive se torna mais crítico nesses casos e pode ser melhorado com o ajuste de determinados parâmetros.</span><span class="sxs-lookup"><span data-stu-id="94353-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="94353-108">O ajuste desses parâmetros é abordado na seção final.</span><span class="sxs-lookup"><span data-stu-id="94353-108">The tuning of these parameters is discussed in the final section.</span></span>

<span data-ttu-id="94353-109">Alguns exemplos de consultas apresentados são específicos para cenários de [Dados de Corridas de Táxi em Nova York](http://chriswhong.com/open-data/foil_nyc_taxi/) e também são fornecidos no [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="94353-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="94353-110">Essas consultas já tem o esquema de dados especificado e estão prontas para ser enviadas para execução.</span><span class="sxs-lookup"><span data-stu-id="94353-110">These queries already have data schema specified and are ready to be submitted to run.</span></span> <span data-ttu-id="94353-111">Na seção final, são discutidos os parâmetros que os usuários podem ajustar para que o desempenho das consultas do Hive possa ser melhorado.</span><span class="sxs-lookup"><span data-stu-id="94353-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="94353-112">Este **menu** leva você até os tópicos que descrevem como criar recursos para dados em vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="94353-112">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="94353-113">Essa tarefa é uma etapa no [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="94353-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94353-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94353-114">Prerequisites</span></span>
<span data-ttu-id="94353-115">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="94353-115">This article assumes that you have:</span></span>

* <span data-ttu-id="94353-116">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="94353-116">Created an Azure storage account.</span></span> <span data-ttu-id="94353-117">Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="94353-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="94353-118">Provisionou um cluster do Hadoop personalizado com o serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="94353-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="94353-119">Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="94353-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="94353-120">Os dados foram carregados para tabelas Hive em clusters do Hadoop do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="94353-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="94353-121">Se não, siga as instruções de [Criar e carregar dados nas tabelas Hive](machine-learning-data-science-move-hive-tables.md) para carregar dados nas tabelas Hive primeiro.</span><span class="sxs-lookup"><span data-stu-id="94353-121">If it has not, please follow [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="94353-122">Habilitou o acesso remoto ao cluster.</span><span class="sxs-lookup"><span data-stu-id="94353-122">Enabled remote access to the cluster.</span></span> <span data-ttu-id="94353-123">Se precisar de instruções, consulte [Acessar o nó principal do Cluster do Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="94353-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="94353-124"><a name="hive-featureengineering"></a>Geração de recursos</span><span class="sxs-lookup"><span data-stu-id="94353-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="94353-125">Nesta seção, veja vários exemplos dos modos pelos quais os recursos podem ser gerados usando consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="94353-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="94353-126">Depois de gerar recursos adicionais, você pode adicioná-los como colunas à tabela existente ou criar uma nova tabela com os recursos adicionais e a chave primária, que pode ser associada à tabela original.</span><span class="sxs-lookup"><span data-stu-id="94353-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span></span> <span data-ttu-id="94353-127">Estes são os exemplos apresentados:</span><span class="sxs-lookup"><span data-stu-id="94353-127">Here are the examples presented:</span></span>

1. [<span data-ttu-id="94353-128">Geração de recursos baseada em frequência</span><span class="sxs-lookup"><span data-stu-id="94353-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="94353-129">Riscos de variáveis categóricas na classificação binária</span><span class="sxs-lookup"><span data-stu-id="94353-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="94353-130">Extrair recursos do campo Datetime</span><span class="sxs-lookup"><span data-stu-id="94353-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="94353-131">Extrair recursos de campo de texto</span><span class="sxs-lookup"><span data-stu-id="94353-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="94353-132">Calcular a distância entre coordenadas de GPS</span><span class="sxs-lookup"><span data-stu-id="94353-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="94353-133"><a name="hive-frequencyfeature"></a>Geração de recursos baseada em frequência</span><span class="sxs-lookup"><span data-stu-id="94353-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="94353-134">Geralmente é útil calcular as frequências dos níveis de uma variável categórica ou as frequências de determinadas combinações de níveis de diversas variáveis categóricas.</span><span class="sxs-lookup"><span data-stu-id="94353-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="94353-135">Os usuários podem usar o script a seguir para calcular tais frequências:</span><span class="sxs-lookup"><span data-stu-id="94353-135">Users can use the following script to calculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="94353-136"><a name="hive-riskfeature"></a>Riscos de variáveis categóricas na classificação binária</span><span class="sxs-lookup"><span data-stu-id="94353-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="94353-137">Na classificação binária, é necessário converter variáveis categóricas não numéricas em recursos numéricos quando os modelos usados aceitam apenas recursos numéricos.</span><span class="sxs-lookup"><span data-stu-id="94353-137">In binary classification, we need to convert non-numeric categorical variables into numeric features when the models being used only take numeric features.</span></span> <span data-ttu-id="94353-138">Isso é feito substituindo cada nível não numéricos por um risco numérico.</span><span class="sxs-lookup"><span data-stu-id="94353-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="94353-139">Nesta seção, mostraremos algumas consultas de Hive genéricas para calcular os valores de risco (probabilidade de log) de uma variável categórica.</span><span class="sxs-lookup"><span data-stu-id="94353-139">In this section, we show some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="94353-140">Neste exemplo, as variáveis `smooth_param1` e `smooth_param2` são definidas para suavizar os valores de risco calculados por meio dos dados.</span><span class="sxs-lookup"><span data-stu-id="94353-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span></span> <span data-ttu-id="94353-141">Riscos tem um intervalo entre -Inf e Inf.</span><span class="sxs-lookup"><span data-stu-id="94353-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="94353-142">Riscos > 0 indica que a probabilidade de o destino ser igual a 1 é maior que 0,5.</span><span class="sxs-lookup"><span data-stu-id="94353-142">A risks > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span></span>

<span data-ttu-id="94353-143">Depois da tabela de risco ser calculada, os usuários podem atribuir valores de risco a uma tabela associando-a à tabela de risco.</span><span class="sxs-lookup"><span data-stu-id="94353-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span></span> <span data-ttu-id="94353-144">A consulta de associação de Hive foi indicada na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="94353-144">The Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="94353-145"><a name="hive-datefeatures"></a>Extrair recursos de campos Datetime</span><span class="sxs-lookup"><span data-stu-id="94353-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="94353-146">O Hive vem com um conjunto de UDFs para processar campos datetime.</span><span class="sxs-lookup"><span data-stu-id="94353-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="94353-147">No Hive, o formato de datetime padrão é “aaaa-MM-dd 00:00:00” (“1970-01-01 12:21:32”, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="94353-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="94353-148">Nesta seção, vamos mostrar exemplos de como extrair o dia do mês e o mês de um campo datetime, bem como exemplos de conversão de uma cadeia de caracteres de datetime em um formato diferente do formato padrão para uma cadeia de caracteres de datetime no formato padrão.</span><span class="sxs-lookup"><span data-stu-id="94353-148">In this section, we show examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="94353-149">Essa consulta de Hive pressupõe que o *&#60;campo datetime>* esteja no formato datetime padrão.</span><span class="sxs-lookup"><span data-stu-id="94353-149">This Hive query assumes that the *&#60;datetime field>* is in the default datetime format.</span></span>

<span data-ttu-id="94353-150">Se um campo datetime não estiver no formato padrão, é necessário primeiro converter o campo datetime em carimbo de data/hora de Unix e, em seguida, converter o carimbo de data/hora do Unix em uma cadeia de caracteres datetime no formato padrão.</span><span class="sxs-lookup"><span data-stu-id="94353-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span></span> <span data-ttu-id="94353-151">Quando o datetime estiver no formato padrão, os usuários poderão aplicar UDFs datetime incorporadas para extrair recursos.</span><span class="sxs-lookup"><span data-stu-id="94353-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of the datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="94353-152">Nesta consulta, se o *&#60;campo datetime>* tiver o padrão *03/26/2015 12:04:39*, o *'&#60;padrão do campo datetime >'* deve ser `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="94353-152">In this query, if the *&#60;datetime field>* has the pattern like *03/26/2015 12:04:39*, the *'&#60;pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="94353-153">Para testá-lo, os usuários podem executar</span><span class="sxs-lookup"><span data-stu-id="94353-153">To test it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="94353-154">O *hivesampletable* nesta consulta vem pré-instalado com todos os clusters do Hadoop do Azure HDInsight por padrão quando os clusters são provisionados.</span><span class="sxs-lookup"><span data-stu-id="94353-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span></span>

### <span data-ttu-id="94353-155"><a name="hive-textfeatures"></a>Extrair recursos de campos de Texto</span><span class="sxs-lookup"><span data-stu-id="94353-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="94353-156">Quando a tabela Hive tem um campo de texto que contém uma cadeia de caracteres de palavras delimitada por espaços, a consulta a seguir extrai o comprimento da cadeia de caracteres e o número de palavras na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="94353-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="94353-157"><a name="hive-gpsdistance"></a>Calcular a distância entre conjuntos de coordenadas de GPS</span><span class="sxs-lookup"><span data-stu-id="94353-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="94353-158">A consulta fornecida nesta seção pode ser aplicada diretamente aos Dados de Viagens de Táxi em NYC.</span><span class="sxs-lookup"><span data-stu-id="94353-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span></span> <span data-ttu-id="94353-159">A finalidade dessa consulta é mostrar como aplicar funções matemáticas incorporadas no Hive para gerar recursos.</span><span class="sxs-lookup"><span data-stu-id="94353-159">The purpose of this query is to show how to apply an embedded mathematical functions in Hive to generate features.</span></span>

<span data-ttu-id="94353-160">Os campos que são usados nesta consulta são coordenadas de GPS de locais de saída e chegada, chamadas *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude* e *dropoff\_latitude*.</span><span class="sxs-lookup"><span data-stu-id="94353-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="94353-161">As consultas que calculam a distância direta entre as coordenadas de saída e chegada são:</span><span class="sxs-lookup"><span data-stu-id="94353-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="94353-162">As equações matemáticas que calculam a distância entre duas coordenadas de GPS podem ser encontradas no site <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Scripts de Tipo Móvel</a>, as quais foram criadas por Peter Lapisu.</span><span class="sxs-lookup"><span data-stu-id="94353-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="94353-163">No Javascript dele, a função `toRad()` é apenas *lat_or_lon*pi/180*, que converte graus em radianos.</span><span class="sxs-lookup"><span data-stu-id="94353-163">In his Javascript, the function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees to radians.</span></span> <span data-ttu-id="94353-164">Aqui, *lat_or_lon* é a latitude ou a longitude.</span><span class="sxs-lookup"><span data-stu-id="94353-164">Here, *lat_or_lon* is the latitude or longitude.</span></span> <span data-ttu-id="94353-165">Como o Hive não fornece a função `atan2`, mas fornece a função `atan`, a função `atan2` é implementada pela função `atan` na consulta de Hive acima usando a definição fornecida na <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipédia</a>.</span><span class="sxs-lookup"><span data-stu-id="94353-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="94353-167">Uma lista completa de UDFs internas do Hive pode ser encontrada na seção **Funções Internas** no <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">wiki do Apache Hive</a>.</span><span class="sxs-lookup"><span data-stu-id="94353-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="94353-168"><a name="tuning"></a> Tópicos avançados: ajustar parâmetros de Hive para melhorar a velocidade de consulta</span><span class="sxs-lookup"><span data-stu-id="94353-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters to Improve Query Speed</span></span>
<span data-ttu-id="94353-169">As configurações de parâmetro padrão do cluster de Hive talvez não sejam adequadas para as consultas de Hive e os dados que as consultas estão processando.</span><span class="sxs-lookup"><span data-stu-id="94353-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span></span> <span data-ttu-id="94353-170">Nesta seção, discutiremos alguns parâmetros que os usuários podem ajustar para melhorar o desempenho das consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="94353-170">In this section, we discuss some parameters that users can tune that improve the performance of Hive queries.</span></span> <span data-ttu-id="94353-171">Os usuários precisam adicionar as consultas de ajuste de parâmetro antes das consultas de processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="94353-171">Users need to add the parameter tuning queries before the queries of processing data.</span></span>

1. <span data-ttu-id="94353-172">**Espaço de heap de Java**: para consultas que envolvem ingressar grandes conjuntos de dados ou processar longos registros, um erro comum é **ficar sem espaço de heap**.</span><span class="sxs-lookup"><span data-stu-id="94353-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common error.</span></span> <span data-ttu-id="94353-173">Isso pode ser ajustado definindo os parâmetros *mapreduce.map.java.opts* e *mapreduce.task.io.sort.mb* com os valores desejados.</span><span class="sxs-lookup"><span data-stu-id="94353-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span></span> <span data-ttu-id="94353-174">Veja um exemplo:</span><span class="sxs-lookup"><span data-stu-id="94353-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="94353-175">Esse parâmetro aloca memória de 4 GB para o espaço de heap de Java e também torna a classificação mais eficiente ao alocar mais memória para ela.</span><span class="sxs-lookup"><span data-stu-id="94353-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="94353-176">É uma boa ideia explorar essas alocações se houver erros de falha de trabalho relacionados ao espaço de heap.</span><span class="sxs-lookup"><span data-stu-id="94353-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span></span>

1. <span data-ttu-id="94353-177">**Tamanho do bloco de DFS** : esse parâmetro define a menor unidade de dados armazenada pelo sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="94353-177">**DFS block size** : This parameter sets the smallest unit of data that the file system stores.</span></span> <span data-ttu-id="94353-178">Por exemplo, se o tamanho do bloco de DFS for 128 MB, todos os dados de tamanho menor ou até 128 MB serão armazenados em um único bloco, enquanto os dados maiores que 128 MB serão alocados em blocos extras.</span><span class="sxs-lookup"><span data-stu-id="94353-178">As an example, if the DFS block size is 128MB, then any data of size less than and up to 128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="94353-179">Escolher um tamanho de bloco muito pequeno causa grandes sobrecargas no Hadoop, pois o nó de nome precisa processar muitas solicitações a mais para localizar o bloco relevante em relação ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="94353-179">Choosing a very small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span></span> <span data-ttu-id="94353-180">Uma configuração recomendada ao trabalhar com gigabytes de dados (ou mais ainda) é:</span><span class="sxs-lookup"><span data-stu-id="94353-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="94353-181">**Otimizar a operação de ingresso no Hive** : embora operações de ingresso na estrutura de mapear/reduzir geralmente ocorram na fase de redução, algumas vezes, é possível obter enormes ganhos agendando associações na fase de mapeamento (também chamada de "mapjoins").</span><span class="sxs-lookup"><span data-stu-id="94353-181">**Optimizing join operation in Hive** : While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span></span> <span data-ttu-id="94353-182">Para direcionar o Hive para fazer isso sempre que possível, podemos definir:</span><span class="sxs-lookup"><span data-stu-id="94353-182">To direct Hive to do this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="94353-183">**Especificar o número de mapeadores de Hive** : embora o Hadoop permita ao usuário definir o número de redutores, o número de mapeadores não é normalmente definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="94353-183">**Specifying the number of mappers to Hive** : While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span></span> <span data-ttu-id="94353-184">Um truque que permite certo grau de controle sobre esse número é escolher as variáveis do Hadoop, *mapred.min.split.size* e *mapred.max.split.size*, pois cada tarefa de mapeamento é determinada por:</span><span class="sxs-lookup"><span data-stu-id="94353-184">A trick that allows some degree of control on this number is to choose the Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="94353-185">Normalmente, o valor padrão de *mapred.min.split.size* é 0, o de *mapred.max.split.size* é **Long.MAX** e o de *dfs.block.size* é 64 MB.</span><span class="sxs-lookup"><span data-stu-id="94353-185">Typically, the default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="94353-186">Como vemos, dado o tamanho dos dados, ajustar esses parâmetros ao “configurá-los” permite ajustar o número de mapeadores usado.</span><span class="sxs-lookup"><span data-stu-id="94353-186">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span></span>
4. <span data-ttu-id="94353-187">Algumas outras opções mais **avançadas** para otimizar o desempenho de Hive são mencionadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="94353-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="94353-188">Eles permitem definir a memória alocada para mapear e reduzir as tarefas e podem ser úteis no ajuste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="94353-188">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="94353-189">Tenha em mente que o *mapreduce.reduce.memory.mb* não pode ser maior que o tamanho da memória física de cada nó de trabalho no cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="94353-189">Please keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

