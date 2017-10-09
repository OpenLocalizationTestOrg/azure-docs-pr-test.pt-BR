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
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="d6ef7-103">Chamar Programas MapReduce da Data Factory</span><span class="sxs-lookup"><span data-stu-id="d6ef7-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="d6ef7-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="d6ef7-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="d6ef7-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="d6ef7-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="d6ef7-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="d6ef7-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="d6ef7-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="d6ef7-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="d6ef7-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="d6ef7-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="d6ef7-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6ef7-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="d6ef7-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6ef7-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="d6ef7-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="d6ef7-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="d6ef7-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d6ef7-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="d6ef7-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="d6ef7-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="d6ef7-114">Hello atividade MapReduce do HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa programas MapReduce em [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster HDInsight baseados no Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d6ef7-115">Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="d6ef7-116">Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="d6ef7-117">Introdução</span><span class="sxs-lookup"><span data-stu-id="d6ef7-117">Introduction</span></span>
<span data-ttu-id="d6ef7-118">Um pipeline em uma fábrica de dados do Azure processa dados nos serviços de armazenamento vinculados utilizando serviços de computação vinculados.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="d6ef7-119">Ela contém uma sequência de atividades em que cada atividade executa uma operação de processamento específica.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="d6ef7-120">Este artigo descreve como usar o hello atividade MapReduce do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="d6ef7-121">Consulte [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) para obter detalhes sobre como executar scripts do Pig/Hive em um cluster HDInsight baseado no Windows/Linux a partir de um pipeline usando atividades do HDInsight Pig e Hive.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="d6ef7-122">JSON para atividade do HDInsight MapReduce</span><span class="sxs-lookup"><span data-stu-id="d6ef7-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="d6ef7-123">Em Olá definição JSON para hello atividade de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d6ef7-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="d6ef7-124">Saudação de conjunto **tipo** de saudação **atividade** muito**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="d6ef7-125">Especificar nome de saudação da classe de saudação para **className** propriedade.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="d6ef7-126">Especificar Olá caminho toohello arquivo JAR, incluindo nome de arquivo hello para **jarFilePath** propriedade.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="d6ef7-127">Especificar serviço Olá vinculado que refere-se toohello armazenamento de BLOBs do Azure que contém o arquivo JAR Olá **jarLinkedService** propriedade.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="d6ef7-128">Especifique quaisquer argumentos para o programa de MapReduce Olá no hello **argumentos** seção.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="d6ef7-129">Em tempo de execução, você ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da estrutura de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="d6ef7-130">toodifferentiate seus argumentos com argumentos de MapReduce hello, considere o uso de opção e valor como argumentos conforme mostrado no exemplo a seguir de saudação (- s, - entrada, --saída etc., são opções imediatamente seguidas por seus valores).</span><span class="sxs-lookup"><span data-stu-id="d6ef7-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

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
<span data-ttu-id="d6ef7-131">Você pode usar o hello atividade MapReduce do HDInsight toorun qualquer arquivo jar de MapReduce em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="d6ef7-132">Olá seguinte definição de JSON de exemplo de um pipeline, hello atividade de HDInsight é configurado toorun um arquivo JAR Mahout.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="d6ef7-133">Exemplo no GitHub</span><span class="sxs-lookup"><span data-stu-id="d6ef7-133">Sample on GitHub</span></span>
<span data-ttu-id="d6ef7-134">Você pode baixar um exemplo para usar o hello atividade MapReduce do HDInsight de: [exemplos de fábrica de dados no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="d6ef7-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="d6ef7-135">Executar programa de contagem de palavras Olá</span><span class="sxs-lookup"><span data-stu-id="d6ef7-135">Running hello Word Count program</span></span>
<span data-ttu-id="d6ef7-136">pipeline de saudação neste exemplo executa Olá contar mapear/reduzir programa em seu cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="d6ef7-137">Serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="d6ef7-137">Linked Services</span></span>
<span data-ttu-id="d6ef7-138">Primeiro, crie uma saudação do serviço vinculado toolink armazenamento do Azure que é usado pelo hello Azure HDInsight cluster toohello data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="d6ef7-139">Se você copiar/colar Olá código a seguir, não se esqueça de tooreplace **nome da conta** e **chave de conta** com nome hello e a chave do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d6ef7-140">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d6ef7-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="d6ef7-141">Serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6ef7-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="d6ef7-142">Em seguida, você criar um serviço vinculado toolink sua fábrica de dados do Azure de toohello de cluster do HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="d6ef7-143">Se você copiar/colar Olá código a seguir, substitua **nome do cluster HDInsight** com o nome de saudação do seu cluster HDInsight e alterar valores de nome e a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="d6ef7-144">CONJUNTOS DE DADOS</span><span class="sxs-lookup"><span data-stu-id="d6ef7-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="d6ef7-145">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="d6ef7-145">Output dataset</span></span>
<span data-ttu-id="d6ef7-146">pipeline de saudação neste exemplo não tem entradas.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="d6ef7-147">Você especifica um conjunto de dados de saída para hello atividade MapReduce do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="d6ef7-148">Este conjunto de dados é um dataset fictício que é necessário toodrive Olá pipeline agendamento.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="d6ef7-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="d6ef7-149">Pipeline</span></span>
<span data-ttu-id="d6ef7-150">pipeline de saudação neste exemplo tem apenas uma atividade que é do tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="d6ef7-151">Algumas das propriedades importantes de saudação em Olá JSON são:</span><span class="sxs-lookup"><span data-stu-id="d6ef7-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="d6ef7-152">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d6ef7-152">Property</span></span> | <span data-ttu-id="d6ef7-153">Observações</span><span class="sxs-lookup"><span data-stu-id="d6ef7-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="d6ef7-154">type</span><span class="sxs-lookup"><span data-stu-id="d6ef7-154">type</span></span> |<span data-ttu-id="d6ef7-155">tipo de saudação deve ser definido muito**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="d6ef7-156">className</span><span class="sxs-lookup"><span data-stu-id="d6ef7-156">className</span></span> |<span data-ttu-id="d6ef7-157">É o nome da classe Olá: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="d6ef7-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="d6ef7-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="d6ef7-158">jarFilePath</span></span> |<span data-ttu-id="d6ef7-159">Arquivo do caminho toohello jar que contém a classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="d6ef7-160">Se você copiar/colar Olá código a seguir, não se esqueça de nome de saudação do toochange do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="d6ef7-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="d6ef7-161">jarLinkedService</span></span> |<span data-ttu-id="d6ef7-162">Serviço vinculado do armazenamento do Azure que contém o arquivo jar de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="d6ef7-163">Esse serviço vinculado refere-se toohello armazenamento associado ao cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="d6ef7-164">argumentos</span><span class="sxs-lookup"><span data-stu-id="d6ef7-164">arguments</span></span> |<span data-ttu-id="d6ef7-165">programa de wordcount Olá leva dois argumentos, uma entrada e uma saída.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="d6ef7-166">Olá entrada é Olá davinci.txt arquivo.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="d6ef7-167">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="d6ef7-167">frequency/interval</span></span> |<span data-ttu-id="d6ef7-168">valores de saudação para essas propriedades correspondem Olá conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="d6ef7-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d6ef7-169">linkedServiceName</span></span> |<span data-ttu-id="d6ef7-170">refere-se o serviço vinculado do HDInsight de toohello criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

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

## <a name="run-spark-programs"></a><span data-ttu-id="d6ef7-171">Executar programas Spark</span><span class="sxs-lookup"><span data-stu-id="d6ef7-171">Run Spark programs</span></span>
<span data-ttu-id="d6ef7-172">Você pode usar programas de Spark MapReduce atividade toorun no seu cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="d6ef7-173">Consulte [Invoke Spark programs from Azure Data Factory (Invocar programas Spark da Azure Data Factory)](data-factory-spark.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6ef7-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="d6ef7-174">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d6ef7-174">See Also</span></span>
* [<span data-ttu-id="d6ef7-175">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="d6ef7-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="d6ef7-176">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="d6ef7-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="d6ef7-177">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="d6ef7-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="d6ef7-178">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="d6ef7-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="d6ef7-179">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="d6ef7-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

