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
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="a3e22-103">Transformar dados usando a Atividade Pig no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a3e22-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="a3e22-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="a3e22-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="a3e22-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="a3e22-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="a3e22-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="a3e22-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="a3e22-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="a3e22-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="a3e22-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="a3e22-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="a3e22-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a3e22-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="a3e22-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a3e22-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="a3e22-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="a3e22-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="a3e22-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a3e22-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="a3e22-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="a3e22-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="a3e22-114">Hello atividade de Pig de HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa consultas de Pig em [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight baseados no Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="a3e22-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a3e22-115">Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="a3e22-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="a3e22-116">Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="a3e22-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="a3e22-117">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="a3e22-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="a3e22-118">Detalhes da sintaxe</span><span class="sxs-lookup"><span data-stu-id="a3e22-118">Syntax details</span></span>
| <span data-ttu-id="a3e22-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a3e22-119">Property</span></span> | <span data-ttu-id="a3e22-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="a3e22-120">Description</span></span> | <span data-ttu-id="a3e22-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a3e22-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e22-122">name</span><span class="sxs-lookup"><span data-stu-id="a3e22-122">name</span></span> |<span data-ttu-id="a3e22-123">Nome da atividade de saudação</span><span class="sxs-lookup"><span data-stu-id="a3e22-123">Name of hello activity</span></span> |<span data-ttu-id="a3e22-124">Sim</span><span class="sxs-lookup"><span data-stu-id="a3e22-124">Yes</span></span> |
| <span data-ttu-id="a3e22-125">description</span><span class="sxs-lookup"><span data-stu-id="a3e22-125">description</span></span> |<span data-ttu-id="a3e22-126">Texto que descreve quais atividade Olá é usada para</span><span class="sxs-lookup"><span data-stu-id="a3e22-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="a3e22-127">Não</span><span class="sxs-lookup"><span data-stu-id="a3e22-127">No</span></span> |
| <span data-ttu-id="a3e22-128">type</span><span class="sxs-lookup"><span data-stu-id="a3e22-128">type</span></span> |<span data-ttu-id="a3e22-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="a3e22-129">HDinsightPig</span></span> |<span data-ttu-id="a3e22-130">Sim</span><span class="sxs-lookup"><span data-stu-id="a3e22-130">Yes</span></span> |
| <span data-ttu-id="a3e22-131">inputs</span><span class="sxs-lookup"><span data-stu-id="a3e22-131">inputs</span></span> |<span data-ttu-id="a3e22-132">Uma ou mais entradas consumida por hello atividade de Pig</span><span class="sxs-lookup"><span data-stu-id="a3e22-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="a3e22-133">Não</span><span class="sxs-lookup"><span data-stu-id="a3e22-133">No</span></span> |
| <span data-ttu-id="a3e22-134">outputs</span><span class="sxs-lookup"><span data-stu-id="a3e22-134">outputs</span></span> |<span data-ttu-id="a3e22-135">Uma ou mais saídas produzido por hello atividade de Pig</span><span class="sxs-lookup"><span data-stu-id="a3e22-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="a3e22-136">Sim</span><span class="sxs-lookup"><span data-stu-id="a3e22-136">Yes</span></span> |
| <span data-ttu-id="a3e22-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="a3e22-137">linkedServiceName</span></span> |<span data-ttu-id="a3e22-138">Cluster do HDInsight toohello registrado como um serviço vinculado na fábrica de dados de referência</span><span class="sxs-lookup"><span data-stu-id="a3e22-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="a3e22-139">Sim</span><span class="sxs-lookup"><span data-stu-id="a3e22-139">Yes</span></span> |
| <span data-ttu-id="a3e22-140">script</span><span class="sxs-lookup"><span data-stu-id="a3e22-140">script</span></span> |<span data-ttu-id="a3e22-141">Especificar Olá Pig script embutido</span><span class="sxs-lookup"><span data-stu-id="a3e22-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="a3e22-142">Não</span><span class="sxs-lookup"><span data-stu-id="a3e22-142">No</span></span> |
| <span data-ttu-id="a3e22-143">caminho do script</span><span class="sxs-lookup"><span data-stu-id="a3e22-143">script path</span></span> |<span data-ttu-id="a3e22-144">Armazenar o script de Pig de saudação em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3e22-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="a3e22-145">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="a3e22-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="a3e22-146">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="a3e22-146">Both cannot be used together.</span></span> <span data-ttu-id="a3e22-147">nome do arquivo Hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a3e22-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="a3e22-148">Não</span><span class="sxs-lookup"><span data-stu-id="a3e22-148">No</span></span> |
| <span data-ttu-id="a3e22-149">define</span><span class="sxs-lookup"><span data-stu-id="a3e22-149">defines</span></span> |<span data-ttu-id="a3e22-150">Especifique parâmetros como pares chave/valor para fazer referência a no script de Pig de saudação</span><span class="sxs-lookup"><span data-stu-id="a3e22-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="a3e22-151">Não</span><span class="sxs-lookup"><span data-stu-id="a3e22-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="a3e22-152">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a3e22-152">Example</span></span>
<span data-ttu-id="a3e22-153">Vamos considerar um exemplo do jogo logs de análise de onde você deseja que o tempo de saudação tooidentify gasto por players jogos iniciado por sua empresa.</span><span class="sxs-lookup"><span data-stu-id="a3e22-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="a3e22-154">Olá log jogo de exemplo a seguir é um arquivo de separados por vírgula (,).</span><span class="sxs-lookup"><span data-stu-id="a3e22-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="a3e22-155">Ele contém Olá campos – ProfileID, SessionStart, duração, SrcIPAddress e GameType a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3e22-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="a3e22-156">Olá **Pig script** tooprocess esses dados:</span><span class="sxs-lookup"><span data-stu-id="a3e22-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="a3e22-157">tooexecute este Pig script em um pipeline da fábrica de dados, Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3e22-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="a3e22-158">Criar um serviço vinculado tooregister [cluster de computação de sua própria HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou configurar [cluster de computação sob demanda HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="a3e22-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="a3e22-159">Vamos chamar esse serviço vinculado de **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a3e22-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="a3e22-160">Criar um [serviço vinculado](data-factory-azure-blob-connector.md) tooconfigure Olá conexão tooAzure o armazenamento de Blob dados saudação de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="a3e22-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="a3e22-161">Vamos chamar esse serviço vinculado de **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a3e22-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="a3e22-162">Criar [conjuntos de dados](data-factory-create-datasets.md) apontar entrada toohello e hello dados de saída.</span><span class="sxs-lookup"><span data-stu-id="a3e22-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="a3e22-163">Vamos chamar o conjunto de dados de entrada hello **PigSampleIn** e o conjunto de dados de saída de hello **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="a3e22-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="a3e22-164">Copie a consulta de Pig de saudação em uma armazenamento de BLOBs do Azure configurado na etapa &#2; de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3e22-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="a3e22-165">Se Olá armazenamento do Azure que hospeda os dados de saudação for diferente da saudação um que hospeda o arquivo de consulta hello, crie um serviço vinculado do armazenamento do Azure separado.</span><span class="sxs-lookup"><span data-stu-id="a3e22-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="a3e22-166">Consulte toohello vinculado de serviço na configuração de atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3e22-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="a3e22-167">Use * * scriptPath * * o arquivo de script do toospecify Olá caminho toopig e **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a3e22-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="a3e22-168">Você também pode fornecer Olá Pig script embutido na definição de atividade hello usando Olá **script** propriedade.</span><span class="sxs-lookup"><span data-stu-id="a3e22-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="a3e22-169">No entanto, não recomendamos essa abordagem, como todos os caracteres especiais no script hello precisa toobe escape e pode causar problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="a3e22-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="a3e22-170">Olá melhor prática é toofollow etapa &#4;.</span><span class="sxs-lookup"><span data-stu-id="a3e22-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="a3e22-171">Crie o pipeline de saudação com hello atividade HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="a3e22-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="a3e22-172">Essa atividade processa dados de entrada hello executando script de Pig no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3e22-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="a3e22-173">Implante o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3e22-173">Deploy hello pipeline.</span></span> <span data-ttu-id="a3e22-174">Consulte o artigo [Criando pipelines](data-factory-create-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a3e22-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="a3e22-175">Monitorar pipeline hello usando o monitoramento de fábrica de dados hello e exibições de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="a3e22-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="a3e22-176">Consulte o artigo [Monitoramento e gerenciando pipelines do Data Factory](data-factory-monitor-manage-pipelines.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a3e22-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="a3e22-177">Especificando parâmetros para um script Pig</span><span class="sxs-lookup"><span data-stu-id="a3e22-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="a3e22-178">Considere Olá exemplo a seguir: logs de jogos são incluídos diariamente no armazenamento de Blob do Azure e armazenados em uma pasta particionada com base na data e hora.</span><span class="sxs-lookup"><span data-stu-id="a3e22-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="a3e22-179">Você deseja script de Pig tooparameterize hello e passa o local de pasta de entrada hello dinamicamente em tempo de execução e também produzir saída Olá particionada com data e hora.</span><span class="sxs-lookup"><span data-stu-id="a3e22-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="a3e22-180">toouse de script Pig com parâmetros, faça Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3e22-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="a3e22-181">Definir parâmetros de saudação na **define**.</span><span class="sxs-lookup"><span data-stu-id="a3e22-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="a3e22-182">Olá Script Pig, consulte toohello parâmetros usando '**$parameterName**' conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a3e22-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="a3e22-183">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a3e22-183">See Also</span></span>
* [<span data-ttu-id="a3e22-184">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="a3e22-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="a3e22-185">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="a3e22-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="a3e22-186">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="a3e22-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="a3e22-187">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="a3e22-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="a3e22-188">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="a3e22-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

