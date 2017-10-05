---
title: Transformar dados usando a Atividade Pig no Azure Data Factory | Microsoft Docs
description: "Saiba como usar a Atividade Pig em uma data factory do Azure para executar scripts Pig em um cluster sob demanda/próprio do HDInsight."
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
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="47331-103">Transformar dados usando a Atividade Pig no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="47331-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="47331-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="47331-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="47331-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="47331-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="47331-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="47331-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="47331-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="47331-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="47331-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="47331-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="47331-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="47331-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="47331-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="47331-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="47331-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="47331-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="47331-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="47331-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="47331-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="47331-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="47331-114">A atividade de Pig do HDInsight em um [pipeline](data-factory-create-pipelines.md) de Data Factory executa consultas de Pig em [seu próprio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) cluster ou no cluster [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) do HDInsight baseado em Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="47331-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="47331-115">Este artigo se baseia no artigo sobre [atividades de transformação de dados](data-factory-data-transformation-activities.md) que apresenta uma visão geral da transformação de dados e as atividades de transformação permitidas.</span><span class="sxs-lookup"><span data-stu-id="47331-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="47331-116">Se você estiver conhecendo o Azure Data Factory agora, leia a [Introdução ao Azure Data Factory](data-factory-introduction.md) e siga o tutorial [Criar seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="47331-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="47331-117">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="47331-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="47331-118">Detalhes da sintaxe</span><span class="sxs-lookup"><span data-stu-id="47331-118">Syntax details</span></span>
| <span data-ttu-id="47331-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47331-119">Property</span></span> | <span data-ttu-id="47331-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="47331-120">Description</span></span> | <span data-ttu-id="47331-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="47331-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47331-122">name</span><span class="sxs-lookup"><span data-stu-id="47331-122">name</span></span> |<span data-ttu-id="47331-123">Nome da atividade</span><span class="sxs-lookup"><span data-stu-id="47331-123">Name of the activity</span></span> |<span data-ttu-id="47331-124">Sim</span><span class="sxs-lookup"><span data-stu-id="47331-124">Yes</span></span> |
| <span data-ttu-id="47331-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="47331-125">description</span></span> |<span data-ttu-id="47331-126">Texto que descreve qual a utilidade da atividade</span><span class="sxs-lookup"><span data-stu-id="47331-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="47331-127">Não</span><span class="sxs-lookup"><span data-stu-id="47331-127">No</span></span> |
| <span data-ttu-id="47331-128">type</span><span class="sxs-lookup"><span data-stu-id="47331-128">type</span></span> |<span data-ttu-id="47331-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="47331-129">HDinsightPig</span></span> |<span data-ttu-id="47331-130">Sim</span><span class="sxs-lookup"><span data-stu-id="47331-130">Yes</span></span> |
| <span data-ttu-id="47331-131">inputs</span><span class="sxs-lookup"><span data-stu-id="47331-131">inputs</span></span> |<span data-ttu-id="47331-132">Uma ou mais entradas consumidas pela atividade Pig</span><span class="sxs-lookup"><span data-stu-id="47331-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="47331-133">Não</span><span class="sxs-lookup"><span data-stu-id="47331-133">No</span></span> |
| <span data-ttu-id="47331-134">outputs</span><span class="sxs-lookup"><span data-stu-id="47331-134">outputs</span></span> |<span data-ttu-id="47331-135">Uma ou mais saídas produzidas pela atividade Pig</span><span class="sxs-lookup"><span data-stu-id="47331-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="47331-136">Sim</span><span class="sxs-lookup"><span data-stu-id="47331-136">Yes</span></span> |
| <span data-ttu-id="47331-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="47331-137">linkedServiceName</span></span> |<span data-ttu-id="47331-138">Referência ao cluster HDInsight registrado como um serviço vinculado na Data Factory</span><span class="sxs-lookup"><span data-stu-id="47331-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="47331-139">Sim</span><span class="sxs-lookup"><span data-stu-id="47331-139">Yes</span></span> |
| <span data-ttu-id="47331-140">script</span><span class="sxs-lookup"><span data-stu-id="47331-140">script</span></span> |<span data-ttu-id="47331-141">Especificar o script de Pig embutido</span><span class="sxs-lookup"><span data-stu-id="47331-141">Specify the Pig script inline</span></span> |<span data-ttu-id="47331-142">Não</span><span class="sxs-lookup"><span data-stu-id="47331-142">No</span></span> |
| <span data-ttu-id="47331-143">caminho do script</span><span class="sxs-lookup"><span data-stu-id="47331-143">script path</span></span> |<span data-ttu-id="47331-144">Armazenar o script de Pig em um armazenamento de blob do Azure e fornecer o caminho para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="47331-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="47331-145">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="47331-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="47331-146">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="47331-146">Both cannot be used together.</span></span> <span data-ttu-id="47331-147">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="47331-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="47331-148">Não</span><span class="sxs-lookup"><span data-stu-id="47331-148">No</span></span> |
| <span data-ttu-id="47331-149">define</span><span class="sxs-lookup"><span data-stu-id="47331-149">defines</span></span> |<span data-ttu-id="47331-150">Especificar parâmetros como pares chave/valor para referenciar dentro do script de Pig</span><span class="sxs-lookup"><span data-stu-id="47331-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="47331-151">Não</span><span class="sxs-lookup"><span data-stu-id="47331-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="47331-152">Exemplo</span><span class="sxs-lookup"><span data-stu-id="47331-152">Example</span></span>
<span data-ttu-id="47331-153">Vamos considerar um exemplo de análises de logs de jogos nos quais você deseja identificar o tempo gasto pelos jogadores em jogos lançados por sua empresa.</span><span class="sxs-lookup"><span data-stu-id="47331-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="47331-154">O log de jogo de exemplo a seguir é um arquivo separado por vírgulas (,).</span><span class="sxs-lookup"><span data-stu-id="47331-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="47331-155">Ele contém os seguintes campos: ProfileID, SessionStart, Duration, SrcIPAddress e GameType.</span><span class="sxs-lookup"><span data-stu-id="47331-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="47331-156">O **script Pig** para processar esses dados:</span><span class="sxs-lookup"><span data-stu-id="47331-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="47331-157">Para executar esse script Pig em um pipeline do Data Factory, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="47331-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="47331-158">Criar um serviço vinculado para registrar [seu próprio cluster de cálculo HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurar o [cluster de cálculo HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="47331-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="47331-159">Vamos chamar esse serviço vinculado de **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="47331-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="47331-160">Criar um [serviço vinculado](data-factory-azure-blob-connector.md) para configurar a conexão com o armazenamento de blob do Azure que está hospedando os dados.</span><span class="sxs-lookup"><span data-stu-id="47331-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="47331-161">Vamos chamar esse serviço vinculado de **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="47331-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="47331-162">Criar [conjuntos de dados](data-factory-create-datasets.md) apontando para os dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="47331-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="47331-163">Vamos chamar o conjunto de dados de entrada de **PigSampleIn** e o conjunto de dados de saída de **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="47331-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="47331-164">Copie a consulta Pig em um arquivo do Armazenamento de Blobs do Azure configurado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="47331-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="47331-165">Se o armazenamento do Azure que hospeda os dados for diferente daquele que hospeda o arquivo de consulta, crie um serviço vinculado do Armazenamento do Azure separado.</span><span class="sxs-lookup"><span data-stu-id="47331-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="47331-166">Confira o serviço vinculado na configuração de atividade.</span><span class="sxs-lookup"><span data-stu-id="47331-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="47331-167">Use **scriptPath** para especificar o caminho para o arquivo de script Pig e **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="47331-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="47331-168">Você também pode fornecer o script Pig embutido na definição da atividade usando a propriedade **script** .</span><span class="sxs-lookup"><span data-stu-id="47331-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="47331-169">No entanto, não incentivamos o uso dessa abordagem, pois os caracteres especiais no script precisam de escape e podem causar problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="47331-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="47331-170">A prática recomendada é seguir a etapa 4.</span><span class="sxs-lookup"><span data-stu-id="47331-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="47331-171">Crie o pipeline com a atividade HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="47331-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="47331-172">Essa atividade processa os dados de entrada executando o script Pig no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47331-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="47331-173">Implante o pipeline.</span><span class="sxs-lookup"><span data-stu-id="47331-173">Deploy the pipeline.</span></span> <span data-ttu-id="47331-174">Consulte o artigo [Criando pipelines](data-factory-create-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="47331-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="47331-175">Monitore o pipeline usando as exibições de gerenciamento e monitoramento de data factory.</span><span class="sxs-lookup"><span data-stu-id="47331-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="47331-176">Consulte o artigo [Monitoramento e gerenciando pipelines do Data Factory](data-factory-monitor-manage-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="47331-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="47331-177">Especificando parâmetros para um script Pig</span><span class="sxs-lookup"><span data-stu-id="47331-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="47331-178">Considere o seguinte exemplo: os logs de jogos são ingeridos diariamente no Armazenamento de Blobs do Azure e armazenados em uma pasta particionada com base na data e na hora.</span><span class="sxs-lookup"><span data-stu-id="47331-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="47331-179">Convém parametrizar o script Pig e passar o local da pasta entrada dinamicamente durante a execução, além de produzir a saída particionada com data e hora.</span><span class="sxs-lookup"><span data-stu-id="47331-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="47331-180">Para usar os scripts Pig parametrizado, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="47331-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="47331-181">Defina os parâmetros em **defines**.</span><span class="sxs-lookup"><span data-stu-id="47331-181">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="47331-182">No Script Pig, consulte os parâmetros usando '**$parameterName**', como mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="47331-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="47331-183">Consulte também</span><span class="sxs-lookup"><span data-stu-id="47331-183">See Also</span></span>
* [<span data-ttu-id="47331-184">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="47331-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="47331-185">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="47331-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="47331-186">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="47331-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="47331-187">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="47331-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="47331-188">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="47331-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

