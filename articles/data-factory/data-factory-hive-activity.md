---
title: aaaTransform dados usando a atividade de Hive - Azure | Microsoft Docs
description: "Saiba como você pode usar o hello atividade Hive em um consultas de Hive do Azure data factory toorun em um cluster de HDInsight próprio no-demanda/o."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Transformar dados usando a Atividade de Hive no Azure Data Factory 
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

Hello atividade Hive do HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa consultas de Hive no [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight baseados no Windows/Linux. Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.

> [!NOTE] 
> Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo. 

## <a name="syntax"></a>Sintaxe

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a>Detalhes da sintaxe
| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome da atividade de saudação |Sim |
| description |Texto que descreve quais atividade Olá é usada para |Não |
| type |HDInsightHive |Sim |
| inputs |Entradas consumidas pela atividade de Hive Olá |Não |
| outputs |Saídas produzidas pela atividade de Hive Olá |Sim |
| linkedServiceName |Cluster do HDInsight toohello registrado como um serviço vinculado na fábrica de dados de referência |Sim |
| script |Especifique o script de Hive Olá embutido |Não |
| caminho do script |Saudação de repositório Hive script em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo. Use a propriedade 'script' ou 'scriptPath'. As duas não podem ser usadas juntas. nome do arquivo Hello diferencia maiusculas de minúsculas. |Não |
| define |Especifique parâmetros como pares chave/valor para fazer referência a no script do Hive hello usando 'hiveconf' |Não |

## <a name="example"></a>Exemplo
Vamos considerar um exemplo do jogo logs de análise de onde você deseja que o tempo de saudação tooidentify gasto por usuários jogos iniciado por sua empresa. 

Olá, log seguinte é um log de exemplo de jogo, vírgula (`,`) separados e contém Olá campos – ProfileID, SessionStart, duração, SrcIPAddress e GameType a seguir.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Olá **script de Hive** tooprocess esses dados:

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

tooexecute essa seção do script em um pipeline da fábrica de dados, você precisa fazer toodo Olá seguinte

1. Criar um serviço vinculado tooregister [cluster de computação de sua própria HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurar [cluster de computação sob demanda HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Vamos chamar esse serviço vinculado de "HDInsightLinkedService".
2. Criar um [serviço vinculado](data-factory-azure-blob-connector.md) tooconfigure Olá conexão tooAzure o armazenamento de Blob dados saudação de hospedagem. Vamos chamar esse serviço vinculado de "StorageLinkedService".
3. Criar [conjuntos de dados](data-factory-create-datasets.md) apontar entrada toohello e hello dados de saída. Vamos chamar o conjunto de dados de entrada hello "HiveSampleIn" e hello "HiveSampleOut" do conjunto de dados de saída
4. Copie consulta de Hive hello como um arquivo tooAzure armazenamento de Blob configurado na etapa &#2;. Se o armazenamento Olá para hospedar dados saudação for diferente da saudação uma hospedagem esse arquivo de consulta, crie um serviço vinculado do armazenamento do Azure separado e consulte tooit na atividade de saudação. Use * * scriptPath * * o arquivo de consulta do toospecify Olá caminho toohive e **scriptLinkedService** toospecify Olá armazenamento do Azure que contém o arquivo de script hello. 
   
   > [!NOTE]
   > Você também pode fornecer o script hello Hive embutido na definição de atividade hello usando Olá **script** propriedade. Não recomendamos essa abordagem, todos os caracteres especiais no script hello no documento JSON Olá precisa toobe escape e pode causa problemas de depuração. Olá melhor prática é toofollow etapa &#4;.
   > 
   > 
5. Crie um pipeline com hello atividade HDInsightHive. atividade de saudação processos/transformações dados saudação.

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Implante o pipeline de saudação. Consulte o artigo [Criando pipelines](data-factory-create-pipelines.md) para obter detalhes. 
7. Monitorar pipeline hello usando o monitoramento de fábrica de dados hello e exibições de gerenciamento. Consulte o artigo [Monitoramento e gerenciando pipelines do Data Factory](data-factory-monitor-manage-pipelines.md) para obter detalhes. 

## <a name="specifying-parameters-for-a-hive-script"></a>Especificando os parâmetros para um script do Hive
Neste exemplo, os logs de jogo são incluídos diariamente no Armazenamento de Blobs do Azure e armazenados em uma pasta particionada com data e hora. Você deseja script do Hive Olá tooparameterize e passa o local de pasta de entrada hello dinamicamente em tempo de execução e também produzir saída Olá particionada com data e hora.

toouse com parâmetros de script do Hive, faça Olá a seguir

* Definir parâmetros de saudação na **define**.

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* Olá Script de Hive, consulte usando o parâmetro toohello **${hiveconf: ParameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>Consulte também
* [Atividade Pig](data-factory-pig-activity.md)
* [Atividade MapReduce](data-factory-map-reduce.md)
* [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

