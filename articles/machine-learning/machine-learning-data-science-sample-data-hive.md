---
title: aaaSample dados nas tabelas do Azure HDInsight Hive | Microsoft Docs
description: Reduzir os dados de amostragem em Tabelas Hive do Azure HDInsight (Hadoop)
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="27052-103">Dados de exemplo nas tabelas Hive do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="27052-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="27052-104">Neste artigo, descrevemos como exemplo de toodown dados armazenados nas tabelas do Azure HDInsight Hive usando consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="27052-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="27052-105">Abordaremos três métodos de amostragem popularmente usados:</span><span class="sxs-lookup"><span data-stu-id="27052-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="27052-106">Amostragem aleatória uniforme</span><span class="sxs-lookup"><span data-stu-id="27052-106">Uniform random sampling</span></span>
* <span data-ttu-id="27052-107">Amostragem aleatória por grupos</span><span class="sxs-lookup"><span data-stu-id="27052-107">Random sampling by groups</span></span>
* <span data-ttu-id="27052-108">Amostragem estratificada</span><span class="sxs-lookup"><span data-stu-id="27052-108">Stratified sampling</span></span>

<span data-ttu-id="27052-109">a seguir Olá **menu** links tootopics que descrevem como toosample dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="27052-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="27052-110">**Por que fazer amostragem dos dados?**</span><span class="sxs-lookup"><span data-stu-id="27052-110">**Why sample your data?**</span></span>
<span data-ttu-id="27052-111">Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho.</span><span class="sxs-lookup"><span data-stu-id="27052-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="27052-112">Isso facilita a compreensão de dados, exploração e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="27052-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="27052-113">Sua função no hello processo de ciência de dados de equipe é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="27052-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="27052-114">Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="27052-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="27052-115">Como consultas de Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="27052-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="27052-116">Consultas de hive podem ser enviadas no console de linha de comando do Hadoop de Olá no nó principal de saudação do cluster de Hadoop de saudação.</span><span class="sxs-lookup"><span data-stu-id="27052-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="27052-117">toodo isso, faça logon no nó principal de saudação do cluster de Hadoop Olá, abrir Olá console de linha de comando do Hadoop e enviar consultas de Hive hello a partir daí.</span><span class="sxs-lookup"><span data-stu-id="27052-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="27052-118">Para obter instruções sobre o envio de consultas de Hive no console de linha de comando do Hadoop hello, consulte [como tooSubmit consultas Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="27052-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="27052-119"><a name="uniform"></a> Amostragem aleatória uniforme</span><span class="sxs-lookup"><span data-stu-id="27052-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="27052-120">Amostragem aleatória uniforme significa que cada linha no conjunto de dados Olá tem a mesma chance de amostra.</span><span class="sxs-lookup"><span data-stu-id="27052-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="27052-121">Isso pode ser implementado com a adição de um conjunto de dados do campo extra rand () toohello na consulta interna de "select" hello e em Olá externa consulta "select" essa condição nesse campo aleatório.</span><span class="sxs-lookup"><span data-stu-id="27052-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="27052-122">Veja um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="27052-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="27052-123">Aqui, `<sample rate, 0-1>` Especifica a proporção de saudação de registros que desejam que os usuários de saudação toosample.</span><span class="sxs-lookup"><span data-stu-id="27052-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="27052-124"><a name="group"></a> Amostragem aleatória por grupos</span><span class="sxs-lookup"><span data-stu-id="27052-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="27052-125">Quando dados categóricos de amostragem, convém tooeither incluir ou excluir todas as instâncias de saudação de algum valor específico de uma variável categórica.</span><span class="sxs-lookup"><span data-stu-id="27052-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="27052-126">Isso é o que "amostragem por grupo” significa.</span><span class="sxs-lookup"><span data-stu-id="27052-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="27052-127">Por exemplo, se você tiver uma variável categórica "Estado", que tem valores NY MA, Canadá, NJ, PA, etc, você deseja que os registros de saudação mesmo estado ser sempre juntos, eles são exemplificados ou não.</span><span class="sxs-lookup"><span data-stu-id="27052-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="27052-128">Veja um exemplo de consulta com amostragem por grupo:</span><span class="sxs-lookup"><span data-stu-id="27052-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="27052-129"><a name="stratified"></a>Amostragem estratificada</span><span class="sxs-lookup"><span data-stu-id="27052-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="27052-130">Amostragem aleatória é estratificada com respeito tooa variável categórica quando exemplos de saudação obtidos têm valores categóricos ou que estão em Olá mesma proporção da população do hello pai da qual Olá exemplos foram obtidos.</span><span class="sxs-lookup"><span data-stu-id="27052-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="27052-131">Usando Olá mesmo exemplo acima, suponha que os dados têm populações sub por estados, digamos NJ tem 100 observações, NY tem 60 observações e WA tem 300 observações.</span><span class="sxs-lookup"><span data-stu-id="27052-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="27052-132">Se você especificar a taxa de saudação do estratificada toobe amostragem 0,5 e hello amostra obtida deve ter aproximadamente 50, 30 e 150 observações de NJ, NY e WA respectivamente.</span><span class="sxs-lookup"><span data-stu-id="27052-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="27052-133">Veja um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="27052-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="27052-134">Para obter informações sobre os métodos de amostragem mais avançados disponíveis no Hive, consulte [Amostragem LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="27052-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

