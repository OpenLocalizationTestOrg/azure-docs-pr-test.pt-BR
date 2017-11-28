---
title: Chamar o Programa MapReduce da Data Factory do Azure
description: Saiba como processar dados executando programas MapReduce em um cluster HDInsight do Azure em uma Azure Data Factory.
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
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="5e3e9-103">Chamar Programas MapReduce da Data Factory</span><span class="sxs-lookup"><span data-stu-id="5e3e9-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5e3e9-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="5e3e9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5e3e9-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="5e3e9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5e3e9-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="5e3e9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5e3e9-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e3e9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5e3e9-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="5e3e9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5e3e9-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5e3e9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5e3e9-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5e3e9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5e3e9-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="5e3e9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5e3e9-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5e3e9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5e3e9-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="5e3e9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5e3e9-114">A atividade de MapReduce do HDInsight em um [pipeline](data-factory-create-pipelines.md) do Data Factory executa programas MapReduce [no seu próprio cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) HDInsight baseado em Windows/Linux, ou em um [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="5e3e9-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5e3e9-115">Este artigo se baseia no artigo sobre [atividades de transformação de dados](data-factory-data-transformation-activities.md) que apresenta uma visão geral da transformação de dados e as atividades de transformação permitidas.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="5e3e9-116">Se você estiver conhecendo o Azure Data Factory agora, leia a [Introdução ao Azure Data Factory](data-factory-introduction.md) e siga o tutorial [Criar seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="5e3e9-117">Introdução</span><span class="sxs-lookup"><span data-stu-id="5e3e9-117">Introduction</span></span>
<span data-ttu-id="5e3e9-118">Um pipeline em uma fábrica de dados do Azure processa dados nos serviços de armazenamento vinculados utilizando serviços de computação vinculados.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="5e3e9-119">Ela contém uma sequência de atividades em que cada atividade executa uma operação de processamento específica.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="5e3e9-120">Este artigo descreve como usar atividade do HDInsight MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="5e3e9-121">Consulte [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) para obter detalhes sobre como executar scripts do Pig/Hive em um cluster HDInsight baseado no Windows/Linux a partir de um pipeline usando atividades do HDInsight Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="5e3e9-122">JSON para atividade do HDInsight MapReduce</span><span class="sxs-lookup"><span data-stu-id="5e3e9-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="5e3e9-123">Na definição do JSON para a atividade de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5e3e9-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="5e3e9-124">Defina o **tipo** da **atividade** como **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="5e3e9-125">Especifique o nome da classe para a propriedade **className** .</span><span class="sxs-lookup"><span data-stu-id="5e3e9-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="5e3e9-126">Especifique o caminho para o arquivo JAR, incluindo o nome do arquivo para a propriedade **jarFilePath** .</span><span class="sxs-lookup"><span data-stu-id="5e3e9-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="5e3e9-127">Especifique o serviço vinculado que faz referência ao Armazenamento de Blob do Azure que contém o arquivo JAR para a propriedade **jarLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="5e3e9-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="5e3e9-128">Especifique todos os argumentos para o programa MapReduce na seção **arguments**.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="5e3e9-129">Em tempo de execução, você verá alguns argumentos extras (por exemplo: mapreduce.job.tags) da estrutura MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="5e3e9-130">Para diferenciar seus argumentos com os argumentos MapReduce, considere usar opção e valor como argumentos, conforme mostrado no exemplo a seguir (- s, --input - output etc... são opções seguidas imediatamente por seus valores).</span><span class="sxs-lookup"><span data-stu-id="5e3e9-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="5e3e9-131">Você pode usar a atividade do HDInsight MapReduce para executar qualquer arquivo de jar do MapReduce em um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="5e3e9-132">Na seguinte definição de JSON de exemplo de uma pipeline, a Atividade HDInsight é configurada para executar um arquivo JAR do Mahout.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="5e3e9-133">Exemplo no GitHub</span><span class="sxs-lookup"><span data-stu-id="5e3e9-133">Sample on GitHub</span></span>
<span data-ttu-id="5e3e9-134">Você pode baixar um exemplo para usar a atividade do MapReduce HDInsight em: [Exemplos do Data Factory no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="5e3e9-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="5e3e9-135">Executando o programa de contagem de palavras</span><span class="sxs-lookup"><span data-stu-id="5e3e9-135">Running the Word Count program</span></span>
<span data-ttu-id="5e3e9-136">O pipeline neste exemplo executa o programa de contagem de palavras de mapa/redução no cluster do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="5e3e9-137">Serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="5e3e9-137">Linked Services</span></span>
<span data-ttu-id="5e3e9-138">Primeiro, crie um serviço vinculado para vincular o armazenamento do Azure que é usado pelo cluster do Azure HDInsight à fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="5e3e9-139">Se você copiar/colar o código a seguir, não se esqueça de substituir o **nome da conta** e a **chave de conta** pelo nome e chave do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="5e3e9-140">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5e3e9-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="5e3e9-141">Serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e3e9-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="5e3e9-142">Em seguida, você cria um serviço vinculado para vincular seu cluster do HDInsight do Azure para a fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="5e3e9-143">Se você copiar/colar o código a seguir, substitua o **nome do cluster do HDInsight** pelo nome do seu cluster do HDInsight e altere os valores de nome e senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="5e3e9-144">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="5e3e9-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="5e3e9-145">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="5e3e9-145">Output dataset</span></span>
<span data-ttu-id="5e3e9-146">O pipeline neste exemplo não tem entradas.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="5e3e9-147">Especifique um conjunto de dados de saída para a atividade do HDInsight MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="5e3e9-148">Esse conjunto de dados é apenas um conjunto fictício exigido para direcionar a agenda de pipeline.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="5e3e9-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="5e3e9-149">Pipeline</span></span>
<span data-ttu-id="5e3e9-150">O pipeline neste exemplo tem apenas uma atividade que seja do tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="5e3e9-151">Algumas das propriedades importantes no JSON são:</span><span class="sxs-lookup"><span data-stu-id="5e3e9-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="5e3e9-152">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5e3e9-152">Property</span></span> | <span data-ttu-id="5e3e9-153">Observações</span><span class="sxs-lookup"><span data-stu-id="5e3e9-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="5e3e9-154">type</span><span class="sxs-lookup"><span data-stu-id="5e3e9-154">type</span></span> |<span data-ttu-id="5e3e9-155">O tipo deve ser definido como **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="5e3e9-156">className</span><span class="sxs-lookup"><span data-stu-id="5e3e9-156">className</span></span> |<span data-ttu-id="5e3e9-157">Nome da classe é: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="5e3e9-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="5e3e9-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="5e3e9-158">jarFilePath</span></span> |<span data-ttu-id="5e3e9-159">Caminho para o arquivo jar que contém a classe.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="5e3e9-160">Se você copiar/colar o código a seguir, não se esqueça de alterar o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="5e3e9-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="5e3e9-161">jarLinkedService</span></span> |<span data-ttu-id="5e3e9-162">Serviço vinculado do Armazenamento do Azure que contém o arquivo jar.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="5e3e9-163">Esse serviço vinculado faz referência ao armazenamento que está associado ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="5e3e9-164">argumentos</span><span class="sxs-lookup"><span data-stu-id="5e3e9-164">arguments</span></span> |<span data-ttu-id="5e3e9-165">O programa wordcount leva dois argumentos, uma entrada e uma saída.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="5e3e9-166">O arquivo de entrada é o davinci.txt.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="5e3e9-167">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="5e3e9-167">frequency/interval</span></span> |<span data-ttu-id="5e3e9-168">Os valores dessas propriedades correspondem ao conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="5e3e9-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5e3e9-169">linkedServiceName</span></span> |<span data-ttu-id="5e3e9-170">refere-se ao serviço vinculado do HDInsight criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="5e3e9-171">Executar programas Spark</span><span class="sxs-lookup"><span data-stu-id="5e3e9-171">Run Spark programs</span></span>
<span data-ttu-id="5e3e9-172">Você pode usar a atividade MapReduce para executar programas Spark no cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="5e3e9-173">Consulte [Invoke Spark programs from Azure Data Factory (Invocar programas Spark da Azure Data Factory)](data-factory-spark.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5e3e9-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="5e3e9-174">Consulte também</span><span class="sxs-lookup"><span data-stu-id="5e3e9-174">See Also</span></span>
* [<span data-ttu-id="5e3e9-175">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="5e3e9-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="5e3e9-176">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="5e3e9-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="5e3e9-177">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e3e9-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="5e3e9-178">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="5e3e9-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="5e3e9-179">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="5e3e9-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

