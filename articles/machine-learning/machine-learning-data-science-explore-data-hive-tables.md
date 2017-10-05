---
title: Explorar dados em tabelas do Hive com consultas do Hive | Microsoft Docs
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
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="8c341-103">Explorar dados em tabelas do Hive com consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="8c341-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="8c341-104">Este documento fornece scripts do Hive de exemplo usados para explorar os dados em tabelas do Hive em um cluster Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c341-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="8c341-105">Os links do **menu** a seguir levam a tópicos que descrevem como usar as ferramentas para explorar dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c341-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="8c341-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8c341-106">Prerequisites</span></span>
<span data-ttu-id="8c341-107">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="8c341-107">This article assumes that you have:</span></span>

* <span data-ttu-id="8c341-108">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c341-108">Created an Azure storage account.</span></span> <span data-ttu-id="8c341-109">Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8c341-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="8c341-110">Provisionou um cluster do Hadoop personalizado com o serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c341-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="8c341-111">Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8c341-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="8c341-112">Os dados foram carregados para tabelas Hive em clusters do Hadoop do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c341-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="8c341-113">Se não tiverem sido, siga as instruções em [Criar e carregar dados para tabelas Hive](machine-learning-data-science-move-hive-tables.md) para carregar dados para tabelas Hive primeiro.</span><span class="sxs-lookup"><span data-stu-id="8c341-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="8c341-114">Habilitou o acesso remoto ao cluster.</span><span class="sxs-lookup"><span data-stu-id="8c341-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="8c341-115">Se precisar de instruções, consulte [Acessar o nó principal do Cluster do Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="8c341-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="8c341-116">Se você precisar de instruções sobre como enviar consultas do Hive, consulte [Como enviar consultas do Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="8c341-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="8c341-117">Exemplo de scripts de consulta do Hive para exploração de dados</span><span class="sxs-lookup"><span data-stu-id="8c341-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="8c341-118">Obter a contagem de observações por partição `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="8c341-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="8c341-119">Obter a contagem de observações por dia `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="8c341-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="8c341-120">Obter os níveis em uma coluna categórica </span><span class="sxs-lookup"><span data-stu-id="8c341-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="8c341-121">Obter o número de níveis na combinação de duas colunas categóricas `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="8c341-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="8c341-122">Obter a distribuição de colunas numéricas </span><span class="sxs-lookup"><span data-stu-id="8c341-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="8c341-123">Extrair registros de associação de duas tabelas</span><span class="sxs-lookup"><span data-stu-id="8c341-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="8c341-124">Scripts de consulta adicionais para cenários de dados de viagem de táxi</span><span class="sxs-lookup"><span data-stu-id="8c341-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="8c341-125">Exemplos de consultas que são específicas para cenários de [Dados de Viagens de Táxi em NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) também são fornecidos no [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="8c341-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="8c341-126">Essas consultas já tem o esquema de dados especificado e estão prontas para ser enviadas para execução.</span><span class="sxs-lookup"><span data-stu-id="8c341-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

