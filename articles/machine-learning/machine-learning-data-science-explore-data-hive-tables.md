---
title: aaaExplore dados nas tabelas de Hive com consultas de Hive | Microsoft Docs
description: Explorar dados em tabelas do Hive usando consultas do Hive.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="fc136-103">Explorar dados em tabelas do Hive com consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="fc136-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="fc136-104">Este documento fornece amostras de scripts de Hive que são usadas tooexplore dados em tabelas de Hive em um cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="fc136-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="fc136-105">a seguir Olá **menu** links tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc136-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="fc136-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc136-106">Prerequisites</span></span>
<span data-ttu-id="fc136-107">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="fc136-107">This article assumes that you have:</span></span>

* <span data-ttu-id="fc136-108">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc136-108">Created an Azure storage account.</span></span> <span data-ttu-id="fc136-109">Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="fc136-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="fc136-110">Provisionar um cluster de Hadoop personalizado com hello serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fc136-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="fc136-111">Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="fc136-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="fc136-112">dados de saudação foi carregado tooHive tabelas em clusters de Hadoop de HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc136-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="fc136-113">Se não estiver, siga as instruções de saudação em [criar e carregar tabelas de tooHive dados](machine-learning-data-science-move-hive-tables.md) tooupload dados tooHive tabelas primeiro.</span><span class="sxs-lookup"><span data-stu-id="fc136-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="fc136-114">Cluster de toohello de acesso remoto habilitado.</span><span class="sxs-lookup"><span data-stu-id="fc136-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="fc136-115">Se você precisar de instruções, consulte [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="fc136-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="fc136-116">Se você precisar de instruções sobre como consultas de Hive toosubmit, consulte [como tooSubmit consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="fc136-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="fc136-117">Exemplo de scripts de consulta do Hive para exploração de dados</span><span class="sxs-lookup"><span data-stu-id="fc136-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="fc136-118">Obter a contagem de saudação de observações por partição`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="fc136-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="fc136-119">Obter a contagem de saudação de observações por dia`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="fc136-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="fc136-120">Obter os níveis de saudação em uma coluna categórica</span><span class="sxs-lookup"><span data-stu-id="fc136-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="fc136-121">Obter o número de saudação de níveis na combinação de duas colunas categóricas`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="fc136-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="fc136-122">Obter distribuição Olá para colunas numéricas</span><span class="sxs-lookup"><span data-stu-id="fc136-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="fc136-123">Extrair registros de associação de duas tabelas</span><span class="sxs-lookup"><span data-stu-id="fc136-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="fc136-124">Scripts de consulta adicionais para cenários de dados de viagem de táxi</span><span class="sxs-lookup"><span data-stu-id="fc136-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="fc136-125">Exemplos de consultas que são muito específicas[NYC táxi Trip dados](http://chriswhong.com/open-data/foil_nyc_taxi/) cenários também são fornecidos em [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="fc136-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="fc136-126">Essas consultas já tiver um esquema de dados especificado e estão pronto toobe enviada toorun.</span><span class="sxs-lookup"><span data-stu-id="fc136-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

