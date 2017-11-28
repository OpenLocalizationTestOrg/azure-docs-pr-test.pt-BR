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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="1482a-103">Transformar dados usando a Atividade de Streaming do Hadoop no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1482a-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1482a-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="1482a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1482a-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="1482a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1482a-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="1482a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1482a-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="1482a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1482a-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="1482a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1482a-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1482a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1482a-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1482a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1482a-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="1482a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1482a-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1482a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1482a-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="1482a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="1482a-114">Você pode usar o hello atividade HDInsightStreamingActivity invocar um trabalho de transmissão do Hadoop de um pipeline da fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="1482a-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="1482a-115">Olá trecho JSON a seguir mostra Olá sintaxe usando Olá HDInsightStreamingActivity em um arquivo JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="1482a-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="1482a-116">Hello atividade de transmissão do HDInsight em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) executa programas de transmissão do Hadoop no [sua](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight baseados no Windows/Linux cluster.</span><span class="sxs-lookup"><span data-stu-id="1482a-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1482a-117">Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral das atividades de transformação de saudação com suporte e transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="1482a-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="1482a-118">Se você estiver tooAzure nova fábrica de dados, leia [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e Olá tutorial: [compilar seu pipeline de dados primeiro](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="1482a-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="1482a-119">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="1482a-119">JSON sample</span></span>
<span data-ttu-id="1482a-120">cluster do HDInsight Olá é preenchida automaticamente com programas de exemplo (wc.exe e cat.exe) e os dados (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="1482a-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="1482a-121">Por padrão, o nome do contêiner de saudação que é usado pelo cluster do HDInsight Olá é nome de saudação do próprio cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1482a-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="1482a-122">Por exemplo, se o nome do cluster for myhdicluster, o nome do contêiner de blob Olá associado seria myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="1482a-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="1482a-123">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1482a-123">Note hello following points:</span></span>

1. <span data-ttu-id="1482a-124">Saudação de conjunto **linkedServiceName** toohello o nome da saudação vinculado serviço que aponta o cluster do HDInsight tooyour no qual Olá streaming mapreduce trabalho é executado.</span><span class="sxs-lookup"><span data-stu-id="1482a-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="1482a-125">Definir o tipo de saudação da atividade Olá muito**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="1482a-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="1482a-126">Para Olá **mapeador** propriedade, especifique o nome de saudação do executável do mapeador.</span><span class="sxs-lookup"><span data-stu-id="1482a-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="1482a-127">Exemplo hello, cat.exe é executável do mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="1482a-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="1482a-128">Para Olá **Redutor** propriedade, especifique o nome de saudação do executável do Redutor.</span><span class="sxs-lookup"><span data-stu-id="1482a-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="1482a-129">Exemplo hello, wc.exe é Redutor de saudação executável.</span><span class="sxs-lookup"><span data-stu-id="1482a-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="1482a-130">Para Olá **entrada** a propriedade type, especifique o arquivo de entrada hello (incluindo a localização de saudação) para o mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="1482a-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="1482a-131">No exemplo hello: "wasb<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample é o contêiner de blob hello, example/data/Gutenberg é a pasta de saudação e davinci.txt é Olá blob.</span><span class="sxs-lookup"><span data-stu-id="1482a-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="1482a-132">Para Olá **saída** a propriedade type, especifique Olá arquivo de saída (incluindo a localização de saudação) para Redutor hello.</span><span class="sxs-lookup"><span data-stu-id="1482a-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="1482a-133">saída de saudação do trabalho de transmissão do Hadoop Olá é gravada toohello local especificado para esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="1482a-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="1482a-134">Em Olá **filePaths** seção, especifique os caminhos de saudação para executáveis do mapeador e Redutor hello.</span><span class="sxs-lookup"><span data-stu-id="1482a-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="1482a-135">No exemplo hello: "adfsample/example/apps/wc.exe", adfsample é o contêiner de blob hello, example/apps é a pasta hello e wc.exe é hello executável.</span><span class="sxs-lookup"><span data-stu-id="1482a-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="1482a-136">Para Olá **fileLinkedService** propriedade, especifique Olá Olá de serviço vinculado que representa o armazenamento do Azure que contém arquivos de saudação especificados na seção de filePaths Olá o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1482a-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="1482a-137">Para Olá **argumentos** propriedade, especifique os argumentos Olá Olá fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1482a-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="1482a-138">Olá **getDebugInfo** propriedade é um elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="1482a-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="1482a-139">Quando estiver definido como tooFailure, Olá logs são baixadas apenas em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="1482a-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="1482a-140">Quando estiver definido como tooAlways, logs são sempre baixados independentemente do status de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1482a-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="1482a-141">Conforme mostrado no exemplo hello, você especificar um conjunto de dados de saída para hello Hadoop Streaming Activity para Olá **gera** propriedade.</span><span class="sxs-lookup"><span data-stu-id="1482a-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="1482a-142">Este conjunto de dados é um dataset fictício que é necessário toodrive Olá pipeline agendamento.</span><span class="sxs-lookup"><span data-stu-id="1482a-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="1482a-143">Não é necessário toospecify qualquer conjunto de dados de entrada para a atividade de saudação para Olá **entradas** propriedade.</span><span class="sxs-lookup"><span data-stu-id="1482a-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="1482a-144">Exemplo</span><span class="sxs-lookup"><span data-stu-id="1482a-144">Example</span></span>
<span data-ttu-id="1482a-145">pipeline de Olá neste passo a passo executa o programa de streaming mapear/reduzir Olá contagem de palavras em seu cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="1482a-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="1482a-146">Serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="1482a-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="1482a-147">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1482a-147">Azure Storage linked service</span></span>
<span data-ttu-id="1482a-148">Primeiro, crie uma saudação do serviço vinculado toolink armazenamento do Azure que é usado pelo hello Azure HDInsight cluster toohello data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1482a-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="1482a-149">Se você copiar/colar Olá código a seguir, não se esqueça de chave de nome e uma conta de conta de tooreplace com o nome de saudação e a chave do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1482a-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="1482a-150">Serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1482a-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="1482a-151">Em seguida, você criar um serviço vinculado toolink sua fábrica de dados do Azure de toohello de cluster do HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="1482a-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="1482a-152">Se você copiar/colar Olá código a seguir, substitua o nome do cluster HDInsight com nome de saudação do seu cluster HDInsight e alterar os valores de nome e a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="1482a-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="1482a-153">CONJUNTOS DE DADOS</span><span class="sxs-lookup"><span data-stu-id="1482a-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="1482a-154">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="1482a-154">Output dataset</span></span>
<span data-ttu-id="1482a-155">pipeline de saudação neste exemplo não tem entradas.</span><span class="sxs-lookup"><span data-stu-id="1482a-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="1482a-156">Você especifica um conjunto de dados de saída para hello atividade de transmissão do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1482a-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="1482a-157">Este conjunto de dados é um dataset fictício que é necessário toodrive Olá pipeline agendamento.</span><span class="sxs-lookup"><span data-stu-id="1482a-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="1482a-158">Pipeline</span><span class="sxs-lookup"><span data-stu-id="1482a-158">Pipeline</span></span>
<span data-ttu-id="1482a-159">pipeline de saudação neste exemplo tem apenas uma atividade que é do tipo: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="1482a-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="1482a-160">cluster do HDInsight Olá é preenchida automaticamente com programas de exemplo (wc.exe e cat.exe) e os dados (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="1482a-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="1482a-161">Por padrão, o nome do contêiner de saudação que é usado pelo cluster do HDInsight Olá é nome de saudação do próprio cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1482a-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="1482a-162">Por exemplo, se o nome do cluster for myhdicluster, o nome do contêiner de blob Olá associado seria myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="1482a-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="1482a-163">Consulte também</span><span class="sxs-lookup"><span data-stu-id="1482a-163">See Also</span></span>
* [<span data-ttu-id="1482a-164">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="1482a-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="1482a-165">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="1482a-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="1482a-166">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="1482a-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="1482a-167">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="1482a-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="1482a-168">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="1482a-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

