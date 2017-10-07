---
title: aaaTransform dados usando a atividade de Pig do Azure Data Factory | Microsoft Docs
description: "Saiba como você pode usar o hello atividade de Pig em um scripts de Pig de toorun de fábrica de dados do Azure em um cluster de HDInsight próprio no-demanda/o."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Transformar dados usando a Atividade Pig no Azure Data Factory
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

Hello atividade de Pig de HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa consultas de Pig em [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight baseados no Windows/Linux. Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.

> [!NOTE] 
> Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo. 

## <a name="syntax"></a>Sintaxe

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
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
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a>Detalhes da sintaxe
| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome da atividade de saudação |Sim |
| description |Texto que descreve quais atividade Olá é usada para |Não |
| type |HDinsightPig |Sim |
| inputs |Uma ou mais entradas consumida por hello atividade de Pig |Não |
| outputs |Uma ou mais saídas produzido por hello atividade de Pig |Sim |
| linkedServiceName |Cluster do HDInsight toohello registrado como um serviço vinculado na fábrica de dados de referência |Sim |
| script |Especificar Olá Pig script embutido |Não |
| caminho do script |Armazenar o script de Pig de saudação em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo. Use a propriedade 'script' ou 'scriptPath'. As duas não podem ser usadas juntas. nome do arquivo Hello diferencia maiusculas de minúsculas. |Não |
| define |Especifique parâmetros como pares chave/valor para fazer referência a no script de Pig de saudação |Não |

## <a name="example"></a>Exemplo
Vamos considerar um exemplo do jogo logs de análise de onde você deseja que o tempo de saudação tooidentify gasto por players jogos iniciado por sua empresa.

Olá log jogo de exemplo a seguir é um arquivo de separados por vírgula (,). Ele contém Olá campos – ProfileID, SessionStart, duração, SrcIPAddress e GameType a seguir.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Olá **Pig script** tooprocess esses dados:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

tooexecute este Pig script em um pipeline da fábrica de dados, Olá etapas a seguir:

1. Criar um serviço vinculado tooregister [cluster de computação de sua própria HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurar [cluster de computação sob demanda HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Vamos chamar esse serviço vinculado de **HDInsightLinkedService**.
2. Criar um [serviço vinculado](data-factory-azure-blob-connector.md) tooconfigure Olá conexão tooAzure o armazenamento de Blob dados saudação de hospedagem. Vamos chamar esse serviço vinculado de **StorageLinkedService**.
3. Criar [conjuntos de dados](data-factory-create-datasets.md) apontar entrada toohello e hello dados de saída. Vamos chamar o conjunto de dados de entrada hello **PigSampleIn** e o conjunto de dados de saída de hello **PigSampleOut**.
4. Copie a consulta de Pig de saudação em uma armazenamento de BLOBs do Azure configurado na etapa &#2; de saudação do arquivo. Se Olá armazenamento do Azure que hospeda os dados de saudação for diferente da saudação um que hospeda o arquivo de consulta hello, crie um serviço vinculado do armazenamento do Azure separado. Consulte toohello vinculado de serviço na configuração de atividade de saudação. Use * * scriptPath * * o arquivo de script do toospecify Olá caminho toopig e **scriptLinkedService**. 
   
   > [!NOTE]
   > Você também pode fornecer Olá Pig script embutido na definição de atividade hello usando Olá **script** propriedade. No entanto, não recomendamos essa abordagem, como todos os caracteres especiais no script hello precisa toobe escape e pode causar problemas de depuração. Olá melhor prática é toofollow etapa &#4;.
   > 
   > 
5. Crie o pipeline de saudação com hello atividade HDInsightPig. Essa atividade processa dados de entrada hello executando script de Pig no cluster HDInsight.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. Implante o pipeline de saudação. Consulte o artigo [Criando pipelines](data-factory-create-pipelines.md) para obter detalhes. 
7. Monitorar pipeline hello usando o monitoramento de fábrica de dados hello e exibições de gerenciamento. Consulte o artigo [Monitoramento e gerenciando pipelines do Data Factory](data-factory-monitor-manage-pipelines.md) para obter detalhes.

## <a name="specifying-parameters-for-a-pig-script"></a>Especificando parâmetros para um script Pig
Considere Olá exemplo a seguir: logs de jogos são incluídos diariamente no armazenamento de Blob do Azure e armazenados em uma pasta particionada com base na data e hora. Você deseja script de Pig tooparameterize hello e passa o local de pasta de entrada hello dinamicamente em tempo de execução e também produzir saída Olá particionada com data e hora.

toouse de script Pig com parâmetros, faça Olá a seguir:

* Definir parâmetros de saudação na **define**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* Olá Script Pig, consulte toohello parâmetros usando '**$parameterName**' conforme mostrado no exemplo a seguir de saudação:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Consulte também
* [Atividade de Hive](data-factory-hive-activity.md)
* [Atividade MapReduce](data-factory-map-reduce.md)
* [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

