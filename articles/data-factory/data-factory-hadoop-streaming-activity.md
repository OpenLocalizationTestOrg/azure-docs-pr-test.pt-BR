---
title: dados de aaaTransform usando Hadoop Streaming Activity - Azure | Microsoft Docs
description: "Saiba como você pode usar o hello Hadoop Streaming Activity em um tootransform dados da fábrica de dados do Azure executando programas de transmissão do Hadoop em um cluster de HDInsight próprio no-demanda/o."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Transformar dados usando a Atividade de Streaming do Hadoop no Azure Data Factory
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

Você pode usar o hello atividade HDInsightStreamingActivity invocar um trabalho de transmissão do Hadoop de um pipeline da fábrica de dados do Azure. Olá trecho JSON a seguir mostra Olá sintaxe usando Olá HDInsightStreamingActivity em um arquivo JSON de pipeline. 

Hello atividade de transmissão do HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa programas de transmissão do Hadoop no [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight baseados no Windows/Linux cluster. Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.

> [!NOTE] 
> Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo. 

## <a name="json-sample"></a>Exemplo de JSON
cluster do HDInsight Olá é preenchida automaticamente com programas de exemplo (wc.exe e cat.exe) e os dados (davinci.txt). Por padrão, o nome do contêiner de saudação que é usado pelo cluster do HDInsight Olá é nome de saudação do próprio cluster hello. Por exemplo, se o nome do cluster for myhdicluster, o nome do contêiner de blob Olá associado seria myhdicluster. 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

Observe Olá pontos a seguir:

1. Saudação de conjunto **linkedServiceName** toohello o nome da saudação vinculado serviço que aponta o cluster do HDInsight tooyour no qual Olá streaming mapreduce trabalho é executado.
2. Definir o tipo de saudação da atividade Olá muito**HDInsightStreaming**.
3. Para Olá **mapeador** propriedade, especifique o nome de saudação do executável do mapeador. Exemplo hello, cat.exe é executável do mapeador de saudação.
4. Para Olá **Redutor** propriedade, especifique o nome de saudação do executável do Redutor. Exemplo hello, wc.exe é Redutor de saudação executável.
5. Para Olá **entrada** a propriedade type, especifique o arquivo de entrada hello (incluindo a localização de saudação) para o mapeador de saudação. No exemplo hello: "wasb<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample é o contêiner de blob hello, example/data/Gutenberg é a pasta de saudação e davinci.txt é Olá blob.
6. Para Olá **saída** a propriedade type, especifique Olá arquivo de saída (incluindo a localização de saudação) para Redutor hello. saída de saudação do trabalho de transmissão do Hadoop Olá é gravada toohello local especificado para esta propriedade.
7. Em Olá **filePaths** seção, especifique os caminhos de saudação para executáveis do mapeador e Redutor hello. No exemplo hello: "adfsample/example/apps/wc.exe", adfsample é o contêiner de blob hello, example/apps é a pasta hello e wc.exe é hello executável.
8. Para Olá **fileLinkedService** propriedade, especifique Olá Olá de serviço vinculado que representa o armazenamento do Azure que contém arquivos de saudação especificados na seção de filePaths Olá o armazenamento do Azure.
9. Para Olá **argumentos** propriedade, especifique os argumentos Olá Olá fluxo de trabalho.
10. Olá **getDebugInfo** propriedade é um elemento opcional. Quando estiver definido como tooFailure, Olá logs são baixadas apenas em caso de falha. Quando estiver definido como tooAlways, logs são sempre baixados independentemente do status de execução de saudação.

> [!NOTE]
> Conforme mostrado no exemplo hello, você especificar um conjunto de dados de saída para hello Hadoop Streaming Activity para Olá **gera** propriedade. Este conjunto de dados é um dataset fictício que é necessário toodrive Olá pipeline agendamento. Não é necessário toospecify qualquer conjunto de dados de entrada para a atividade de saudação para Olá **entradas** propriedade.  
> 
> 

## <a name="example"></a>Exemplo
pipeline de Olá neste passo a passo executa o programa de streaming mapear/reduzir Olá contagem de palavras em seu cluster HDInsight do Azure. 

### <a name="linked-services"></a>Serviços vinculados
#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
Primeiro, crie uma saudação do serviço vinculado toolink armazenamento do Azure que é usado pelo hello Azure HDInsight cluster toohello data factory do Azure. Se você copiar/colar Olá código a seguir, não se esqueça de chave de nome e uma conta de conta de tooreplace com o nome de saudação e a chave do armazenamento do Azure. 

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
Em seguida, você criar um serviço vinculado toolink sua fábrica de dados do Azure de toohello de cluster do HDInsight do Azure. Se você copiar/colar Olá código a seguir, substitua o nome do cluster HDInsight com nome de saudação do seu cluster HDInsight e alterar os valores de nome e a senha do usuário. 

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
pipeline de saudação neste exemplo não tem entradas. Você especifica um conjunto de dados de saída para hello atividade de transmissão do HDInsight. Este conjunto de dados é um dataset fictício que é necessário toodrive Olá pipeline agendamento. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
pipeline de saudação neste exemplo tem apenas uma atividade que é do tipo: **HDInsightStreaming**. 

cluster do HDInsight Olá é preenchida automaticamente com programas de exemplo (wc.exe e cat.exe) e os dados (davinci.txt). Por padrão, o nome do contêiner de saudação que é usado pelo cluster do HDInsight Olá é nome de saudação do próprio cluster hello. Por exemplo, se o nome do cluster for myhdicluster, o nome do contêiner de blob Olá associado seria myhdicluster.  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>Consulte também
* [Atividade de Hive](data-factory-hive-activity.md)
* [Atividade Pig](data-factory-pig-activity.md)
* [Atividade MapReduce](data-factory-map-reduce.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

