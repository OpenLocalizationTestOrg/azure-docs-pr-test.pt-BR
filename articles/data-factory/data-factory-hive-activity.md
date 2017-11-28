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
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="fdc96-103">Transformar dados usando a Atividade de Hive no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fdc96-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="fdc96-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="fdc96-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="fdc96-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="fdc96-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="fdc96-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="fdc96-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="fdc96-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="fdc96-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="fdc96-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="fdc96-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="fdc96-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fdc96-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="fdc96-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fdc96-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="fdc96-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="fdc96-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="fdc96-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fdc96-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="fdc96-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="fdc96-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="fdc96-114">Hello atividade Hive do HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa consultas de Hive no [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight baseados no Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="fdc96-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="fdc96-115">Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="fdc96-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="fdc96-116">Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="fdc96-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="fdc96-117">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="fdc96-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="fdc96-118">Detalhes da sintaxe</span><span class="sxs-lookup"><span data-stu-id="fdc96-118">Syntax details</span></span>
| <span data-ttu-id="fdc96-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fdc96-119">Property</span></span> | <span data-ttu-id="fdc96-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="fdc96-120">Description</span></span> | <span data-ttu-id="fdc96-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fdc96-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fdc96-122">name</span><span class="sxs-lookup"><span data-stu-id="fdc96-122">name</span></span> |<span data-ttu-id="fdc96-123">Nome da atividade de saudação</span><span class="sxs-lookup"><span data-stu-id="fdc96-123">Name of hello activity</span></span> |<span data-ttu-id="fdc96-124">Sim</span><span class="sxs-lookup"><span data-stu-id="fdc96-124">Yes</span></span> |
| <span data-ttu-id="fdc96-125">description</span><span class="sxs-lookup"><span data-stu-id="fdc96-125">description</span></span> |<span data-ttu-id="fdc96-126">Texto que descreve quais atividade Olá é usada para</span><span class="sxs-lookup"><span data-stu-id="fdc96-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="fdc96-127">Não</span><span class="sxs-lookup"><span data-stu-id="fdc96-127">No</span></span> |
| <span data-ttu-id="fdc96-128">type</span><span class="sxs-lookup"><span data-stu-id="fdc96-128">type</span></span> |<span data-ttu-id="fdc96-129">HDInsightHive</span><span class="sxs-lookup"><span data-stu-id="fdc96-129">HDinsightHive</span></span> |<span data-ttu-id="fdc96-130">Sim</span><span class="sxs-lookup"><span data-stu-id="fdc96-130">Yes</span></span> |
| <span data-ttu-id="fdc96-131">inputs</span><span class="sxs-lookup"><span data-stu-id="fdc96-131">inputs</span></span> |<span data-ttu-id="fdc96-132">Entradas consumidas pela atividade de Hive Olá</span><span class="sxs-lookup"><span data-stu-id="fdc96-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="fdc96-133">Não</span><span class="sxs-lookup"><span data-stu-id="fdc96-133">No</span></span> |
| <span data-ttu-id="fdc96-134">outputs</span><span class="sxs-lookup"><span data-stu-id="fdc96-134">outputs</span></span> |<span data-ttu-id="fdc96-135">Saídas produzidas pela atividade de Hive Olá</span><span class="sxs-lookup"><span data-stu-id="fdc96-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="fdc96-136">Sim</span><span class="sxs-lookup"><span data-stu-id="fdc96-136">Yes</span></span> |
| <span data-ttu-id="fdc96-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fdc96-137">linkedServiceName</span></span> |<span data-ttu-id="fdc96-138">Cluster do HDInsight toohello registrado como um serviço vinculado na fábrica de dados de referência</span><span class="sxs-lookup"><span data-stu-id="fdc96-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="fdc96-139">Sim</span><span class="sxs-lookup"><span data-stu-id="fdc96-139">Yes</span></span> |
| <span data-ttu-id="fdc96-140">script</span><span class="sxs-lookup"><span data-stu-id="fdc96-140">script</span></span> |<span data-ttu-id="fdc96-141">Especifique o script de Hive Olá embutido</span><span class="sxs-lookup"><span data-stu-id="fdc96-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="fdc96-142">Não</span><span class="sxs-lookup"><span data-stu-id="fdc96-142">No</span></span> |
| <span data-ttu-id="fdc96-143">caminho do script</span><span class="sxs-lookup"><span data-stu-id="fdc96-143">script path</span></span> |<span data-ttu-id="fdc96-144">Saudação de repositório Hive script em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="fdc96-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="fdc96-145">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="fdc96-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="fdc96-146">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="fdc96-146">Both cannot be used together.</span></span> <span data-ttu-id="fdc96-147">nome do arquivo Hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fdc96-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="fdc96-148">Não</span><span class="sxs-lookup"><span data-stu-id="fdc96-148">No</span></span> |
| <span data-ttu-id="fdc96-149">define</span><span class="sxs-lookup"><span data-stu-id="fdc96-149">defines</span></span> |<span data-ttu-id="fdc96-150">Especifique parâmetros como pares chave/valor para fazer referência a no script do Hive hello usando 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="fdc96-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="fdc96-151">Não</span><span class="sxs-lookup"><span data-stu-id="fdc96-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="fdc96-152">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fdc96-152">Example</span></span>
<span data-ttu-id="fdc96-153">Vamos considerar um exemplo do jogo logs de análise de onde você deseja que o tempo de saudação tooidentify gasto por usuários jogos iniciado por sua empresa.</span><span class="sxs-lookup"><span data-stu-id="fdc96-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="fdc96-154">Olá, log seguinte é um log de exemplo de jogo, vírgula (`,`) separados e contém Olá campos – ProfileID, SessionStart, duração, SrcIPAddress e GameType a seguir.</span><span class="sxs-lookup"><span data-stu-id="fdc96-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="fdc96-155">Olá **script de Hive** tooprocess esses dados:</span><span class="sxs-lookup"><span data-stu-id="fdc96-155">hello **Hive script** tooprocess this data:</span></span>

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

<span data-ttu-id="fdc96-156">tooexecute essa seção do script em um pipeline da fábrica de dados, você precisa fazer toodo Olá seguinte</span><span class="sxs-lookup"><span data-stu-id="fdc96-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="fdc96-157">Criar um serviço vinculado tooregister [cluster de computação de sua própria HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurar [cluster de computação sob demanda HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="fdc96-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="fdc96-158">Vamos chamar esse serviço vinculado de "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="fdc96-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="fdc96-159">Criar um [serviço vinculado](data-factory-azure-blob-connector.md) tooconfigure Olá conexão tooAzure o armazenamento de Blob dados saudação de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="fdc96-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="fdc96-160">Vamos chamar esse serviço vinculado de "StorageLinkedService".</span><span class="sxs-lookup"><span data-stu-id="fdc96-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="fdc96-161">Criar [conjuntos de dados](data-factory-create-datasets.md) apontar entrada toohello e hello dados de saída.</span><span class="sxs-lookup"><span data-stu-id="fdc96-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="fdc96-162">Vamos chamar o conjunto de dados de entrada hello "HiveSampleIn" e hello "HiveSampleOut" do conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="fdc96-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="fdc96-163">Copie consulta de Hive hello como um arquivo tooAzure armazenamento de Blob configurado na etapa &#2;.</span><span class="sxs-lookup"><span data-stu-id="fdc96-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="fdc96-164">Se o armazenamento Olá para hospedar dados saudação for diferente da saudação uma hospedagem esse arquivo de consulta, crie um serviço vinculado do armazenamento do Azure separado e consulte tooit na atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="fdc96-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="fdc96-165">Use * * scriptPath * * o arquivo de consulta do toospecify Olá caminho toohive e **scriptLinkedService** toospecify Olá armazenamento do Azure que contém o arquivo de script hello.</span><span class="sxs-lookup"><span data-stu-id="fdc96-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fdc96-166">Você também pode fornecer o script hello Hive embutido na definição de atividade hello usando Olá **script** propriedade.</span><span class="sxs-lookup"><span data-stu-id="fdc96-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="fdc96-167">Não recomendamos essa abordagem, todos os caracteres especiais no script hello no documento JSON Olá precisa toobe escape e pode causa problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="fdc96-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="fdc96-168">Olá melhor prática é toofollow etapa &#4;.</span><span class="sxs-lookup"><span data-stu-id="fdc96-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="fdc96-169">Crie um pipeline com hello atividade HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="fdc96-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="fdc96-170">atividade de saudação processos/transformações dados saudação.</span><span class="sxs-lookup"><span data-stu-id="fdc96-170">hello activity processes/transforms hello data.</span></span>

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
6. <span data-ttu-id="fdc96-171">Implante o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fdc96-171">Deploy hello pipeline.</span></span> <span data-ttu-id="fdc96-172">Consulte o artigo [Criando pipelines](data-factory-create-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fdc96-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="fdc96-173">Monitorar pipeline hello usando o monitoramento de fábrica de dados hello e exibições de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="fdc96-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="fdc96-174">Consulte o artigo [Monitoramento e gerenciando pipelines do Data Factory](data-factory-monitor-manage-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fdc96-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="fdc96-175">Especificando os parâmetros para um script do Hive</span><span class="sxs-lookup"><span data-stu-id="fdc96-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="fdc96-176">Neste exemplo, os logs de jogo são incluídos diariamente no Armazenamento de Blobs do Azure e armazenados em uma pasta particionada com data e hora.</span><span class="sxs-lookup"><span data-stu-id="fdc96-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="fdc96-177">Você deseja script do Hive Olá tooparameterize e passa o local de pasta de entrada hello dinamicamente em tempo de execução e também produzir saída Olá particionada com data e hora.</span><span class="sxs-lookup"><span data-stu-id="fdc96-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="fdc96-178">toouse com parâmetros de script do Hive, faça Olá a seguir</span><span class="sxs-lookup"><span data-stu-id="fdc96-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="fdc96-179">Definir parâmetros de saudação na **define**.</span><span class="sxs-lookup"><span data-stu-id="fdc96-179">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="fdc96-180">Olá Script de Hive, consulte usando o parâmetro toohello **${hiveconf: ParameterName}**.</span><span class="sxs-lookup"><span data-stu-id="fdc96-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="fdc96-181">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fdc96-181">See Also</span></span>
* [<span data-ttu-id="fdc96-182">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="fdc96-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="fdc96-183">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="fdc96-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="fdc96-184">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="fdc96-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="fdc96-185">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="fdc96-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="fdc96-186">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="fdc96-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

