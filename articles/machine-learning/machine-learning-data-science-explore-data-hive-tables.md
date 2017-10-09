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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Explorar dados em tabelas do Hive com consultas do Hive.
Este documento fornece amostras de scripts de Hive que são usadas tooexplore dados em tabelas de Hive em um cluster HDInsight Hadoop.

a seguir Olá **menu** links tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo supõe que você:

* Criou uma conta de armazenamento do Azure. Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Provisionar um cluster de Hadoop personalizado com hello serviço HDInsight. Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).
* dados de saudação foi carregado tooHive tabelas em clusters de Hadoop de HDInsight do Azure. Se não estiver, siga as instruções de saudação em [criar e carregar tabelas de tooHive dados](machine-learning-data-science-move-hive-tables.md) tooupload dados tooHive tabelas primeiro.
* Cluster de toohello de acesso remoto habilitado. Se você precisar de instruções, consulte [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Se você precisar de instruções sobre como consultas de Hive toosubmit, consulte [como tooSubmit consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Exemplo de scripts de consulta do Hive para exploração de dados
1. Obter a contagem de saudação de observações por partição`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Obter a contagem de saudação de observações por dia`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Obter os níveis de saudação em uma coluna categórica  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Obter o número de saudação de níveis na combinação de duas colunas categóricas`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Obter distribuição Olá para colunas numéricas  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Extrair registros de associação de duas tabelas
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Scripts de consulta adicionais para cenários de dados de viagem de táxi
Exemplos de consultas que são muito específicas[NYC táxi Trip dados](http://chriswhong.com/open-data/foil_nyc_taxi/) cenários também são fornecidos em [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Essas consultas já tiver um esquema de dados especificado e estão pronto toobe enviada toorun.

