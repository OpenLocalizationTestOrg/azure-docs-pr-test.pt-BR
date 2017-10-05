---
title: Transformar dados usando a Atividade de Hive - Azure | Microsoft Docs
description: "Saiba como usar a atividade de Hive em uma Azure Data Factory para executar consultas de Hive em um cluster sob demanda/próprio de HDInsight."
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="9d722-103">Transformar dados usando a Atividade de Hive no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9d722-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9d722-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="9d722-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9d722-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="9d722-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9d722-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="9d722-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9d722-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="9d722-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9d722-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="9d722-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9d722-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9d722-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9d722-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9d722-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9d722-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="9d722-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9d722-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9d722-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9d722-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="9d722-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="9d722-114">A atividade de Hive do HDInsight em um [pipeline](data-factory-create-pipelines.md) do Data Factory executa consultas de Hive em [seu próprio cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou no [cluster sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) do HDInsight baseado em Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="9d722-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9d722-115">Este artigo se baseia no artigo sobre [atividades de transformação de dados](data-factory-data-transformation-activities.md) que apresenta uma visão geral da transformação de dados e as atividades de transformação permitidas.</span><span class="sxs-lookup"><span data-stu-id="9d722-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="9d722-116">Se você estiver conhecendo o Azure Data Factory agora, leia a [Introdução ao Azure Data Factory](data-factory-introduction.md) e siga o tutorial [Criar seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="9d722-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="9d722-117">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="9d722-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="9d722-118">Detalhes da sintaxe</span><span class="sxs-lookup"><span data-stu-id="9d722-118">Syntax details</span></span>
| <span data-ttu-id="9d722-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9d722-119">Property</span></span> | <span data-ttu-id="9d722-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="9d722-120">Description</span></span> | <span data-ttu-id="9d722-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9d722-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d722-122">name</span><span class="sxs-lookup"><span data-stu-id="9d722-122">name</span></span> |<span data-ttu-id="9d722-123">Nome da atividade</span><span class="sxs-lookup"><span data-stu-id="9d722-123">Name of the activity</span></span> |<span data-ttu-id="9d722-124">Sim</span><span class="sxs-lookup"><span data-stu-id="9d722-124">Yes</span></span> |
| <span data-ttu-id="9d722-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="9d722-125">description</span></span> |<span data-ttu-id="9d722-126">Texto que descreve qual a utilidade da atividade</span><span class="sxs-lookup"><span data-stu-id="9d722-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="9d722-127">Não</span><span class="sxs-lookup"><span data-stu-id="9d722-127">No</span></span> |
| <span data-ttu-id="9d722-128">type</span><span class="sxs-lookup"><span data-stu-id="9d722-128">type</span></span> |<span data-ttu-id="9d722-129">HDInsightHive</span><span class="sxs-lookup"><span data-stu-id="9d722-129">HDinsightHive</span></span> |<span data-ttu-id="9d722-130">Sim</span><span class="sxs-lookup"><span data-stu-id="9d722-130">Yes</span></span> |
| <span data-ttu-id="9d722-131">inputs</span><span class="sxs-lookup"><span data-stu-id="9d722-131">inputs</span></span> |<span data-ttu-id="9d722-132">Entradas consumidas pela atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="9d722-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="9d722-133">Não</span><span class="sxs-lookup"><span data-stu-id="9d722-133">No</span></span> |
| <span data-ttu-id="9d722-134">outputs</span><span class="sxs-lookup"><span data-stu-id="9d722-134">outputs</span></span> |<span data-ttu-id="9d722-135">Saídas produzidas pela atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="9d722-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="9d722-136">Sim</span><span class="sxs-lookup"><span data-stu-id="9d722-136">Yes</span></span> |
| <span data-ttu-id="9d722-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9d722-137">linkedServiceName</span></span> |<span data-ttu-id="9d722-138">Referência ao cluster HDInsight registrado como um serviço vinculado na Data Factory</span><span class="sxs-lookup"><span data-stu-id="9d722-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="9d722-139">Sim</span><span class="sxs-lookup"><span data-stu-id="9d722-139">Yes</span></span> |
| <span data-ttu-id="9d722-140">script</span><span class="sxs-lookup"><span data-stu-id="9d722-140">script</span></span> |<span data-ttu-id="9d722-141">Especifique o script de Hive embutido</span><span class="sxs-lookup"><span data-stu-id="9d722-141">Specify the Hive script inline</span></span> |<span data-ttu-id="9d722-142">Não</span><span class="sxs-lookup"><span data-stu-id="9d722-142">No</span></span> |
| <span data-ttu-id="9d722-143">script path</span><span class="sxs-lookup"><span data-stu-id="9d722-143">script path</span></span> |<span data-ttu-id="9d722-144">Armazene o script de Hive em um armazenamento de blob do Azure e forneça o caminho para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="9d722-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="9d722-145">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="9d722-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="9d722-146">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="9d722-146">Both cannot be used together.</span></span> <span data-ttu-id="9d722-147">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9d722-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="9d722-148">Não</span><span class="sxs-lookup"><span data-stu-id="9d722-148">No</span></span> |
| <span data-ttu-id="9d722-149">defines</span><span class="sxs-lookup"><span data-stu-id="9d722-149">defines</span></span> |<span data-ttu-id="9d722-150">Especifique parâmetros como pares chave/valor para referenciar dentro do script de Hive usando 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="9d722-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="9d722-151">Não</span><span class="sxs-lookup"><span data-stu-id="9d722-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="9d722-152">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9d722-152">Example</span></span>
<span data-ttu-id="9d722-153">Vamos considerar um exemplo de análises de logs de jogos nos quais você deseja identificar o tempo gasto pelos usuários em jogos lançados por sua empresa.</span><span class="sxs-lookup"><span data-stu-id="9d722-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="9d722-154">O log a seguir é um log de jogo de exemplo, que é separado por vírgula (`,`) e contém os seguintes campos – ProfileID, SessionStart, Duration, SrcIPAddress e GameType.</span><span class="sxs-lookup"><span data-stu-id="9d722-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="9d722-155">O **script do Hive** para processar esses dados:</span><span class="sxs-lookup"><span data-stu-id="9d722-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="9d722-156">Para executar o script do Hive em um pipeline do Data Factory, você precisa fazer o seguinte</span><span class="sxs-lookup"><span data-stu-id="9d722-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="9d722-157">Criar um serviço vinculado para registrar [seu próprio cluster de cálculo HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurar o [cluster de cálculo HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="9d722-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="9d722-158">Vamos chamar esse serviço vinculado de "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="9d722-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="9d722-159">Criar um [serviço vinculado](data-factory-azure-blob-connector.md) para configurar a conexão com o Armazenamento de Blob do Azure que está hospedando os dados.</span><span class="sxs-lookup"><span data-stu-id="9d722-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="9d722-160">Vamos chamar esse serviço vinculado de "StorageLinkedService".</span><span class="sxs-lookup"><span data-stu-id="9d722-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="9d722-161">Criar [conjuntos de dados](data-factory-create-datasets.md) apontando para os dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="9d722-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="9d722-162">Vamos chamar o conjunto de dados de entrada de "HiveSampleIn" e o conjunto de dados de saída de "HiveSampleOut"</span><span class="sxs-lookup"><span data-stu-id="9d722-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="9d722-163">Copie a consulta do Hive como um arquivo para o Armazenamento de Blobs do Azure configurado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="9d722-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="9d722-164">Se o armazenamento para hospedar os dados for diferente daquele que hospeda o arquivo de consulta, crie um serviço vinculado do Armazenamento do Azure separado e refira-o na atividade.</span><span class="sxs-lookup"><span data-stu-id="9d722-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="9d722-165">Use **scriptPath** para especificar o caminho para o arquivo de consulta do Hive e **scriptLinkedService** para especificar o armazenamento do Azure que contém o arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="9d722-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9d722-166">Você também pode fornecer o script Hive embutido na definição da atividade usando a propriedade **script** .</span><span class="sxs-lookup"><span data-stu-id="9d722-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="9d722-167">Não recomendamos essa abordagem, pois os caracteres especiais no script no documento JSON precisam de escape e podem causar problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="9d722-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="9d722-168">A prática recomendada é seguir a etapa 4.</span><span class="sxs-lookup"><span data-stu-id="9d722-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="9d722-169">Crie um pipeline com a atividade HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="9d722-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="9d722-170">A atividade processa/transforma os dados.</span><span class="sxs-lookup"><span data-stu-id="9d722-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="9d722-171">Implante o pipeline.</span><span class="sxs-lookup"><span data-stu-id="9d722-171">Deploy the pipeline.</span></span> <span data-ttu-id="9d722-172">Consulte o artigo [Criando pipelines](data-factory-create-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9d722-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="9d722-173">Monitore o pipeline usando as exibições de gerenciamento e monitoramento de data factory.</span><span class="sxs-lookup"><span data-stu-id="9d722-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="9d722-174">Consulte o artigo [Monitoramento e gerenciando pipelines do Data Factory](data-factory-monitor-manage-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9d722-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="9d722-175">Especificando os parâmetros para um script do Hive</span><span class="sxs-lookup"><span data-stu-id="9d722-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="9d722-176">Neste exemplo, os logs de jogo são incluídos diariamente no Armazenamento de Blobs do Azure e armazenados em uma pasta particionada com data e hora.</span><span class="sxs-lookup"><span data-stu-id="9d722-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="9d722-177">Você deseja parametrizar o script de Hive e passar o local da pasta de entrada dinamicamente durante a execução, além de produzir a saída particionada com data e hora.</span><span class="sxs-lookup"><span data-stu-id="9d722-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="9d722-178">Para usar o script do Hive com parâmetros, faça o seguinte</span><span class="sxs-lookup"><span data-stu-id="9d722-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="9d722-179">Defina os parâmetros em **defines**.</span><span class="sxs-lookup"><span data-stu-id="9d722-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="9d722-180">No script de Hive, consulte o parâmetro usando **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="9d722-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="9d722-181">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9d722-181">See Also</span></span>
* [<span data-ttu-id="9d722-182">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="9d722-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="9d722-183">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="9d722-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="9d722-184">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="9d722-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="9d722-185">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="9d722-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="9d722-186">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="9d722-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

