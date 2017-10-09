---
title: "aaaInvoke programa MapReduce da fábrica de dados do Azure"
description: "Saiba como dados tooprocess executando programas MapReduce em um Azure HDInsight do cluster de uma fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Chamar Programas MapReduce da Data Factory
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Atividade de Hive](data-factory-hive-activity.md) 
> * [Atividade Pig](data-factory-pig-activity.md)
> * [Atividade MapReduce](data-factory-map-reduce.md)
> * [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Atividade do Spark](data-factory-spark.md)
> * [Atividade de Execução em Lote do Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Atividade do Recurso de Atualização do Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md)
> * [Atividade do U-SQL do Data Lake Analytics](data-factory-usql-activity.md)
> * [Atividade Personalizada do .NET](data-factory-use-custom-activities.md)

Hello atividade MapReduce do HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa programas MapReduce em [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight baseados no Windows/Linux. Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.

> [!NOTE] 
> Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo.  

## <a name="introduction"></a>Introdução
Um pipeline em uma fábrica de dados do Azure processa dados nos serviços de armazenamento vinculados utilizando serviços de computação vinculados. Ela contém uma sequência de atividades em que cada atividade executa uma operação de processamento específica. Este artigo descreve como usar o hello atividade MapReduce do HDInsight.

Consulte [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) para obter detalhes sobre como executar scripts do Pig/Hive em um cluster HDInsight baseado no Windows/Linux a partir de um pipeline usando atividades do HDInsight Pig e Hive. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON para atividade do HDInsight MapReduce
Em Olá definição JSON para hello atividade de HDInsight: 

1. Saudação de conjunto **tipo** de saudação **atividade** muito**HDInsight**.
2. Especificar nome de saudação da classe de saudação para **className** propriedade.
3. Especificar Olá caminho toohello arquivo JAR, incluindo nome de arquivo hello para **jarFilePath** propriedade.
4. Especificar serviço Olá vinculado que refere-se toohello armazenamento de BLOBs do Azure que contém o arquivo JAR Olá **jarLinkedService** propriedade.   
5. Especifique quaisquer argumentos para o programa de MapReduce Olá no hello **argumentos** seção. Em tempo de execução, você ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da estrutura de MapReduce hello. toodifferentiate seus argumentos com argumentos de MapReduce hello, considere o uso de opção e valor como argumentos conforme mostrado no exemplo a seguir de saudação (- s, - entrada, --saída etc., são opções imediatamente seguidas por seus valores).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
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
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
Você pode usar o hello atividade MapReduce do HDInsight toorun qualquer arquivo jar de MapReduce em um cluster HDInsight. Olá seguinte definição de JSON de exemplo de um pipeline, hello atividade de HDInsight é configurado toorun um arquivo JAR Mahout.

## <a name="sample-on-github"></a>Exemplo no GitHub
Você pode baixar um exemplo para usar o hello atividade MapReduce do HDInsight de: [exemplos de fábrica de dados no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Executar programa de contagem de palavras Olá
pipeline de saudação neste exemplo executa Olá contar mapear/reduzir programa em seu cluster HDInsight do Azure.   

### <a name="linked-services"></a>Serviços vinculados
Primeiro, crie uma saudação do serviço vinculado toolink armazenamento do Azure que é usado pelo hello Azure HDInsight cluster toohello data factory do Azure. Se você copiar/colar Olá código a seguir, não se esqueça de tooreplace **nome da conta** e **chave de conta** com nome hello e a chave do armazenamento do Azure. 

#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Serviço vinculado do Azure HDInsight
Em seguida, você criar um serviço vinculado toolink sua fábrica de dados do Azure de toohello de cluster do HDInsight do Azure. Se você copiar/colar Olá código a seguir, substitua **nome do cluster HDInsight** com o nome de saudação do seu cluster HDInsight e alterar valores de nome e a senha do usuário.   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>CONJUNTOS DE DADOS
#### <a name="output-dataset"></a>Conjunto de dados de saída
pipeline de saudação neste exemplo não tem entradas. Você especifica um conjunto de dados de saída para hello atividade MapReduce do HDInsight. Este conjunto de dados é um dataset fictício que é necessário toodrive Olá pipeline agendamento.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
pipeline de saudação neste exemplo tem apenas uma atividade que é do tipo: HDInsightMapReduce. Algumas das propriedades importantes de saudação em Olá JSON são: 

| Propriedade | Observações |
|:--- |:--- |
| type |tipo de saudação deve ser definido muito**HDInsightMapReduce**. |
| className |É o nome da classe Olá: **wordcount** |
| jarFilePath |Arquivo do caminho toohello jar que contém a classe de saudação. Se você copiar/colar Olá código a seguir, não se esqueça de nome de saudação do toochange do cluster de saudação. |
| jarLinkedService |Serviço vinculado do armazenamento do Azure que contém o arquivo jar de saudação. Esse serviço vinculado refere-se toohello armazenamento associado ao cluster do HDInsight hello. |
| argumentos |programa de wordcount Olá leva dois argumentos, uma entrada e uma saída. Olá entrada é Olá davinci.txt arquivo. |
| frequência/intervalo |valores de saudação para essas propriedades correspondem Olá conjunto de dados de saída. |
| linkedServiceName |refere-se o serviço vinculado do HDInsight de toohello criado anteriormente. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Executar programas Spark
Você pode usar programas de Spark MapReduce atividade toorun no seu cluster HDInsight Spark. Consulte [Invoke Spark programs from Azure Data Factory (Invocar programas Spark da Azure Data Factory)](data-factory-spark.md) para obter detalhes.  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Consulte também
* [Atividade de Hive](data-factory-hive-activity.md)
* [Atividade Pig](data-factory-pig-activity.md)
* [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

