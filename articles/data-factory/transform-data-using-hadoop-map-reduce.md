---
title: Transformar dados usando a atividade do MapReduce do Hadoop no Azure Data Factory | Microsoft Docs
description: Saiba como processar dados executando programas MapReduce do Hadoop em um cluster do Azure HDInsight em um Azure Data Factory.
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: shengc
ms.openlocfilehash: c1fbb6864629874ef116cdf81d48df4a9ed5af1f
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="transform-data-using-hadoop-mapreduce-activity-in-azure-data-factory"></a>Transformar dados usando a atividade do MapReduce do Hadoop no Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 – já disponível](v1/data-factory-map-reduce.md)
> * [Versão 2 – Versão prévia](transform-data-using-hadoop-map-reduce.md)


A atividade do MapReduce no HDInsight em um [pipeline](concepts-pipelines-activities.md) do Data Factory invoca programas MapReduce em um cluster do HDInsight [de sua propriedade](compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Este artigo se baseia no artigo sobre [atividades de transformação de dados](transform-data.md) que apresenta uma visão geral da transformação de dados e as atividades de transformação permitidas.

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que já está disponível, consulte a [Atividade do MapReduce na V1](v1/data-factory-map-reduce.md).


Se você é novo no Azure Data Factory, leia a [Introduction to Azure Data Factory](introduction.md) (Introdução ao Azure Data Factory) e siga o tutorial: [Tutorial: transformar dados](tutorial-transform-data-spark-powershell.md) antes de ler este artigo. 

Consulte [Pig](transform-data-using-hadoop-pig.md) e [Hive](transform-data-using-hadoop-hive.md) para obter detalhes sobre a execução de scripts do Pig/Hive em um cluster do HDInsight de um pipeline usando atividades do Pig e do Hive no HDInsight. 

## <a name="syntax"></a>Sintaxe

```json
{
    "name": "Map Reduce Activity",
    "description": "Description",
    "type": "HDInsightMapReduce",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "className": "org.myorg.SampleClass",
        "jarLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "jarFilePath": "MyAzureStorage/jars/sample.jar",
        "getDebugInfo": "Failure",
        "arguments": [
          "-SampleHadoopJobArgument1"
        ],
        "defines": {
          "param1": "param1Value"
        }
    }
}
```

## <a name="syntax-details"></a>Detalhes da sintaxe

| Propriedade          | DESCRIÇÃO                              | Obrigatório |
| ----------------- | ---------------------------------------- | -------- |
| Nome              | Nome da atividade                     | sim      |
| Descrição       | Texto que descreve qual a utilidade da atividade | Não        |
| Tipo              | Para a atividade do MapReduce, o tipo de atividade é HDinsightMapReduce | sim      |
| linkedServiceName | Referência ao cluster do HDInsight registrado como um serviço vinculado no Data Factory. Para saber mais sobre esse serviço vinculado, consulte o artigo [Compute linked services](compute-linked-services.md) (Serviços de computação vinculados). | sim      |
| className         | Nome da classe a ser executada         | sim      |
| jarLinkedService  | Referência a um serviço vinculado do Armazenamento do Azure usado para armazenar os arquivos Jar. Se você não especificar esse serviço vinculado, será usado o serviço vinculado do Armazenamento do Azure definido no serviço vinculado do HDInsight. | Não        |
| jarFilePath       | Forneça o caminho para os arquivos Jar armazenados no Armazenamento do Azure referenciado por jarLinkedService. O nome do arquivo diferencia maiúsculas de minúsculas. | sim      |
| jarlibs           | Matriz de cadeia de caracteres do caminho para os arquivos de biblioteca Jar referenciados pelo trabalho armazenado no Armazenamento do Azure referenciado por jarLinkedService. O nome do arquivo diferencia maiúsculas de minúsculas. | Não        |
| getDebugInfo      | Especifica quando os arquivos de log são copiados para o Armazenamento do Azure usado pelo cluster do HDInsight (ou) especificado por jarLinkedService. Valores permitidos: Nenhum, Sempre ou Falha. Valor padrão: Nenhum. | Não        |
| argumentos         | Especifica uma matriz de argumentos para um trabalho do Hadoop. Os argumentos são passados como argumentos de linha de comando para cada tarefa. | Não        |
| define           | Especifique parâmetros como pares chave-valor para referências no script do Hive. | Não        |



## <a name="example"></a>Exemplo
Você pode usar a atividade do HDInsight MapReduce para executar qualquer arquivo de jar do MapReduce em um cluster do HDInsight. Na seguinte definição de JSON de exemplo de uma pipeline, a Atividade HDInsight é configurada para executar um arquivo JAR do Mahout.

```json   
{
    "name": "MapReduce Activity for Mahout",
    "description": "Custom MapReduce to generate Mahout result",
    "type": "HDInsightMapReduce",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
        "jarLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
        "arguments": [
            "-s",
            "SIMILARITY_LOGLIKELIHOOD",
            "--input",
            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
            "--output",
            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
            "--maxSimilaritiesPerItem",
            "500",
            "--tempDir",
            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
        ]
    }
}
```
Você pode especificar argumentos para o programa MapReduce na seção **argumentos**. Em tempo de execução, você verá alguns argumentos extras (por exemplo: mapreduce.job.tags) da estrutura MapReduce. Para diferenciar seus argumentos com os argumentos MapReduce, considere usar opção e valor como argumentos, conforme mostrado no exemplo a seguir (- s, --input - output etc... são opções seguidas imediatamente por seus valores).

## <a name="next-steps"></a>Próximas etapas
Consulte os seguintes artigos que explicam como transformar dados de outras maneiras: 

* [U-SQL activity](transform-data-using-data-lake-analytics.md) (Atividade do U-SQL)
* [Hive activity](transform-data-using-hadoop-hive.md) (Atividade do Hive)
* [Pig activity](transform-data-using-hadoop-pig.md) (Atividade do Pig)
* [Hadoop Streaming activity](transform-data-using-hadoop-streaming.md) (Atividade de streaming do Hadoop)
* [Spark activity](transform-data-using-spark.md) (Atividade do Spark)
* [Atividade personalizada do .NET](transform-data-using-dotnet-custom-activity.md)
* [Machine Learning Batch Execution activity](transform-data-using-machine-learning.md) (Atividade de execução em lotes do Machine Learning)
* [Stored procedure activity](transform-data-using-stored-procedure.md) (Atividade de procedimento armazenado)
