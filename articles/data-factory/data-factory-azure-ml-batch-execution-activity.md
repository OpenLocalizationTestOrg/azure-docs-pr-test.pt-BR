---
title: "aaaCreate pipelines de dados de previsão usando o Azure Data Factory | Microsoft Docs"
description: "Descreve como toocreate criar pipelines de previsão usando o Azure Data Factory e aprendizado de máquina do Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="592ac-103">Criar pipelines de previsão usando Azure Machine Learning e o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="592ac-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="592ac-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="592ac-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="592ac-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="592ac-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="592ac-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="592ac-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="592ac-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="592ac-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="592ac-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="592ac-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="592ac-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="592ac-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="592ac-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="592ac-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="592ac-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="592ac-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="592ac-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="592ac-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="592ac-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="592ac-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="592ac-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="592ac-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="592ac-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="592ac-115">Azure Machine Learning</span></span>
<span data-ttu-id="592ac-116">[O aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/services/machine-learning/) permite toobuild, testar e implantar soluções de análise de previsão.</span><span class="sxs-lookup"><span data-stu-id="592ac-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="592ac-117">De um ponto de vista de alto nível, isso é feito em três etapas:</span><span class="sxs-lookup"><span data-stu-id="592ac-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="592ac-118">**Crie um teste de treinamento**.</span><span class="sxs-lookup"><span data-stu-id="592ac-118">**Create a training experiment**.</span></span> <span data-ttu-id="592ac-119">Siga esta etapa usando hello Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="592ac-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="592ac-120">o estúdio de ML Olá é um ambiente de colaboração de desenvolvimento visual que você use tootrain e testa um modelo de análise de previsão usando dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="592ac-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="592ac-121">**Convertê-lo a experiência de previsão tooa**.</span><span class="sxs-lookup"><span data-stu-id="592ac-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="592ac-122">Depois que o modelo foi treinado com dados existentes e você está pronto toouse-tooscore novos dados, preparar e simplificar sua experiência de pontuação.</span><span class="sxs-lookup"><span data-stu-id="592ac-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="592ac-123">**Implantá-lo como um serviço da Web**.</span><span class="sxs-lookup"><span data-stu-id="592ac-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="592ac-124">Você pode publicar seu experimento de pontuação como um serviço Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="592ac-125">Você pode enviar o modelo de dados de tooyour por este ponto de extremidade de serviço web e receber previsões de resultado para o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="592ac-126">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="592ac-126">Azure Data Factory</span></span>
<span data-ttu-id="592ac-127">Fábrica de dados é um serviço de integração de dados com base em nuvem que orquestra e automatiza Olá **movimentação** e **transformação** de dados.</span><span class="sxs-lookup"><span data-stu-id="592ac-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="592ac-128">Você pode criar soluções de integração de dados usando a fábrica de dados do Azure que podem incluir dados de várias fontes de dados, / processo de transformação dados saudação e publicar Olá resultado dados toohello dados repositórios.</span><span class="sxs-lookup"><span data-stu-id="592ac-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="592ac-129">Serviço de fábrica de dados permite que você toocreate pipelines de dados que moverem e transform dados e execute pipelines Olá em um agendamento especificado (por hora, diariamente, semanalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="592ac-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="592ac-130">Ele também fornece a linhagem de saudação toodisplay visualizações avançadas e as dependências entre seus pipelines de dados e monitorar todos os seus pipelines de dados de um problema de identificar tooeasily exibição unificada exclusiva e configurar alertas de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="592ac-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="592ac-131">Consulte [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e [criar seu primeiro pipeline](data-factory-build-your-first-pipeline.md) artigos tooquickly começar com hello serviço do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="592ac-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="592ac-132">Data Factory e Machine Learning juntos</span><span class="sxs-lookup"><span data-stu-id="592ac-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="592ac-133">Ativa a fábrica de dados do Azure tooeasily você criar pipelines que usam uma publicação [aprendizado de máquina do Azure] [ azure-machine-learning] web service para análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="592ac-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="592ac-134">Usando Olá **atividade de execução de lote** em um pipeline da fábrica de dados do Azure, você pode invocar um previsões de toomake Azure ML web service nos dados de saudação em lote.</span><span class="sxs-lookup"><span data-stu-id="592ac-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="592ac-135">Consulte [invocar um ML do Azure usando o serviço web hello atividade de execução de lote](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="592ac-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="592ac-136">Ao longo do tempo, os modelos de previsão de saudação em experiências de pontuação do hello Azure ML necessário toobe treinados novamente usando novos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="592ac-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="592ac-137">Você pode treinar novamente um modelo ML do Azure de um pipeline da fábrica de dados fazendo Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="592ac-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="592ac-138">Publica a experiência de treinamento de saudação (experiência não previsão) como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="592ac-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="592ac-139">Você executar esta etapa no hello Azure ML Studio como você fez experimento previsão tooexpose como um serviço web no cenário anterior hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="592ac-140">Use serviço de web hello atividade de execução de lote do Azure ML tooinvoke Olá para teste de treinamento hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="592ac-141">Basicamente, você pode usar tooinvoke de atividade de execução de lote do ML do Azure Olá treinamento serviço web e o serviço web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="592ac-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="592ac-142">Depois de terminar com treinamento, atualizar Olá pontuação serviço da web (previsão experimento exposto como um serviço da web) com hello recentemente treinado usando Olá **a atividade de recurso de atualização do Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="592ac-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="592ac-143">Veja o artigo [Atualização de modelos usando a Atividade do Recurso de Atualização](data-factory-azure-ml-update-resource-activity.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="592ac-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="592ac-144">Invocar um serviço Web usando a Atividade de Execução em Lote</span><span class="sxs-lookup"><span data-stu-id="592ac-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="592ac-145">Você usa o processamento e a movimentação de dados do Azure Data Factory tooorchestrate e, em seguida, executar execução em lotes usando o aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="592ac-146">Aqui estão as etapas de nível superior de saudação:</span><span class="sxs-lookup"><span data-stu-id="592ac-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="592ac-147">Criar um serviço vinculado de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="592ac-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="592ac-148">Você precisa Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="592ac-148">You need hello following values:</span></span>

   1. <span data-ttu-id="592ac-149">**URI de solicitação** para Olá API de execução do lote.</span><span class="sxs-lookup"><span data-stu-id="592ac-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="592ac-150">Você pode encontrar hello URI da solicitação clicando Olá **BATCH EXECUTION** link na página de serviços web hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="592ac-151">**Chave de API** para Olá publicado o serviço web de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="592ac-152">Você pode encontrar a chave de API Olá clicando Olá web service que você publicou.</span><span class="sxs-lookup"><span data-stu-id="592ac-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="592ac-153">Saudação de uso **AzureMLBatchExecution** atividade.</span><span class="sxs-lookup"><span data-stu-id="592ac-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Painel de Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI do lote](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="592ac-156">Cenário: Experiências usando entradas/saídas de serviço de Web que se referem a toodata no armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="592ac-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="592ac-157">Nesse cenário, hello serviço da Web de aprendizado de máquina do Azure faz previsões usando dados de um arquivo em um armazenamento de BLOBs do Azure e armazena os resultados da previsão Olá no armazenamento de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="592ac-158">Olá JSON a seguir define um pipeline da fábrica de dados com uma atividade AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="592ac-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="592ac-159">atividade de saudação tem Olá dataset **DecisionTreeInputBlob** como entrada e **DecisionTreeResultBlob** como saída de hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="592ac-160">Olá **DecisionTreeInputBlob** é passado como um serviço web de entrada toohello por usando Olá **webServiceInput** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="592ac-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="592ac-161">Olá **DecisionTreeResultBlob** é passado como um serviço de Web saída toohello por usando Olá **webserviceoutputs na** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="592ac-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="592ac-162">Se o serviço web de saudação pega várias entradas, use Olá **webServiceInputs** propriedade em vez de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="592ac-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="592ac-163">Consulte Olá [Web service exige várias entradas](#web-service-requires-multiple-inputs) seção para obter um exemplo de como usar Olá webServiceInputs propriedade.</span><span class="sxs-lookup"><span data-stu-id="592ac-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="592ac-164">Conjuntos de dados que são referenciados por Olá **webServiceInput**/**webServiceInputs** e **webserviceoutputs na** propriedades (em  **typeProperties**) também deve ser incluído no hello atividade **entradas** e **gera**.</span><span class="sxs-lookup"><span data-stu-id="592ac-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="592ac-165">Em seu experimento de Azure ML, as portas de entrada e saída do serviço Web e os parâmetros globais têm nomes padrão ("input1", "input2") os quais você pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="592ac-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="592ac-166">nomes de saudação usados para configurações de globalParameters, webServiceInputs e webserviceoutputs na devem corresponder exatamente aos nomes de saudação em experiências de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="592ac-167">Você pode exibir a carga de solicitação de exemplo hello na página de ajuda de execução de lote de saudação para o mapeamento do ML do Azure ponto de extremidade tooverify Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="592ac-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="592ac-168">Somente entradas e saídas da atividade de AzureMLBatchExecution Olá podem ser passadas como parâmetros toohello serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="592ac-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="592ac-169">Por exemplo, Olá acima trecho JSON, DecisionTreeInputBlob é uma entrada toohello AzureMLBatchExecution atividade, que é passada como um serviço Web de entrada toohello por meio do parâmetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="592ac-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="592ac-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="592ac-170">Example</span></span>
<span data-ttu-id="592ac-171">Este toohold de armazenamento do Azure do exemplo usa ambos Olá dados de entrada e saídos.</span><span class="sxs-lookup"><span data-stu-id="592ac-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="592ac-172">É recomendável que você passe por Olá [criar seu primeiro pipeline com a fábrica de dados] [ adf-build-1st-pipeline] tutorial antes de executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="592ac-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="592ac-173">Use Olá Editor da fábrica de dados toocreate Data Factory artefatos (serviços vinculados, conjuntos de dados, pipeline) neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="592ac-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="592ac-174">Criar um **serviço vinculado** para o **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="592ac-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="592ac-175">Se hello arquivos de entrada e saídos estiverem em diferentes contas de armazenamento, você precisa de dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="592ac-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="592ac-176">Aqui está um exemplo JSON:</span><span class="sxs-lookup"><span data-stu-id="592ac-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="592ac-177">Criar hello **entrada** do Azure Data Factory **conjunto de dados**.</span><span class="sxs-lookup"><span data-stu-id="592ac-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="592ac-178">Ao contrário de alguns outros conjuntos de dados do Data Factory, esses conjuntos de dados devem conter os valores **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="592ac-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="592ac-179">Você pode usar particionamento toocause tooprocess de execução (cada fatia de dados) cada lote ou produzir entrada exclusiva e arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="592ac-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="592ac-180">Talvez seja necessário tooinclude alguns Olá tootransform de atividade de upstream de entrada em formato de arquivo CSV hello e colocá-lo na conta de armazenamento de saudação de cada fatia.</span><span class="sxs-lookup"><span data-stu-id="592ac-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="592ac-181">Nesse caso, não inclua Olá **externo** e **externalData** configurações mostradas no hello seguir exemplo e sua DecisionTreeInputBlob seria Olá o conjunto de dados de saída de uma atividade diferente.</span><span class="sxs-lookup"><span data-stu-id="592ac-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="592ac-182">O arquivo csv de entrada deve ter a linha de cabeçalho de coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="592ac-183">Se você estiver usando Olá **atividade de cópia** toocreate/mover Olá csv, no armazenamento de blob hello, você deve definir a propriedade de coletor de saudação **blobWriterAddHeader** muito**true**.</span><span class="sxs-lookup"><span data-stu-id="592ac-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="592ac-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="592ac-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="592ac-185">Se o arquivo csv de saudação não tem linha de cabeçalho hello, você poderá ver Olá erro a seguir: **erro na atividade: erro ao ler a cadeia de caracteres. Token inesperado: StartObject. Caminho '', linha 1, posição 1**.</span><span class="sxs-lookup"><span data-stu-id="592ac-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="592ac-186">Criar hello **saída** do Azure Data Factory **conjunto de dados**.</span><span class="sxs-lookup"><span data-stu-id="592ac-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="592ac-187">Este exemplo usa o particionamento toocreate um caminho de saída exclusivo para cada execução da fatia.</span><span class="sxs-lookup"><span data-stu-id="592ac-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="592ac-188">Sem particionamento hello, atividade de saudação substituiria o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="592ac-189">Criar um **serviço vinculado** do tipo: **AzureMLLinkedService**, fornecendo a chave de API de saudação e URL de execução de lote de modelo.</span><span class="sxs-lookup"><span data-stu-id="592ac-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="592ac-190">Por fim, crie um pipeline que contenha uma atividade **AzureMLBatchScoring** .</span><span class="sxs-lookup"><span data-stu-id="592ac-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="592ac-191">Em tempo de execução, pipeline executa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="592ac-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="592ac-192">Obtém o local de saudação do arquivo de entrada hello de seus conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="592ac-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="592ac-193">Invoca a execução de lote de aprendizado de máquina do Azure Olá API</span><span class="sxs-lookup"><span data-stu-id="592ac-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="592ac-194">Cópias Olá lote execução saída toohello blob, dado no conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="592ac-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="592ac-195">A atividade AzureMLBatchExecution pode ter zero ou mais entradas e uma ou mais saídas.</span><span class="sxs-lookup"><span data-stu-id="592ac-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="592ac-196">Ambos os valores de data/hora de **início** e de **término** devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="592ac-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="592ac-197">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="592ac-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="592ac-198">Olá **final** tempo é opcional.</span><span class="sxs-lookup"><span data-stu-id="592ac-198">hello **end** time is optional.</span></span> <span data-ttu-id="592ac-199">Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas.**"</span><span class="sxs-lookup"><span data-stu-id="592ac-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="592ac-200">pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="592ac-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="592ac-201">Consulte a [Referência de script JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="592ac-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="592ac-202">A especificação de entrada para a atividade de AzureMLBatchExecution Olá é opcional.</span><span class="sxs-lookup"><span data-stu-id="592ac-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="592ac-203">Cenário: Experiências usando módulos de leitor/gravador toorefer toodata em vários armazenamentos</span><span class="sxs-lookup"><span data-stu-id="592ac-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="592ac-204">Outro cenário comum ao criar experimentos do ML do Azure é toouse módulos de leitor e gravador.</span><span class="sxs-lookup"><span data-stu-id="592ac-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="592ac-205">Olá leitor é usada tooload dados em uma experiência e módulo de gravador Olá toosave dados de suas experiências.</span><span class="sxs-lookup"><span data-stu-id="592ac-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="592ac-206">Para obter detalhes sobre os módulos de leitor e gravador, consulte os tópicos [Leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Gravador](https://msdn.microsoft.com/library/azure/dn905984.aspx) na biblioteca MSDN.</span><span class="sxs-lookup"><span data-stu-id="592ac-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="592ac-207">Ao usar módulos de leitor e gravador Olá, é uma boa prática toouse um parâmetro de serviço da Web para cada propriedade desses módulos de leitor/gravador.</span><span class="sxs-lookup"><span data-stu-id="592ac-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="592ac-208">Esses parâmetros da web permitem que você os valores hello tooconfigure durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="592ac-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="592ac-209">Por exemplo, você poderia criar um experimento com um módulo leitor que usa um banco de dados SQL do Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="592ac-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="592ac-210">Após a implantação do serviço web de saudação, você deseja tooenable consumidores de saudação de Olá web serviço toospecify outro servidor do SQL Azure chamado YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="592ac-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="592ac-211">Você pode usar um tooallow de parâmetro de serviço Web este toobe valor configurado.</span><span class="sxs-lookup"><span data-stu-id="592ac-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="592ac-212">A saída e entrada de serviço Web são diferentes dos parâmetros de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="592ac-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="592ac-213">Primeiro cenário de saudação, você viu como entrada e saída podem ser especificados para um serviço Web do ML do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="592ac-214">Nesse cenário, você deve passar parâmetros para um serviço Web que correspondem a tooproperties dos módulos de leitor/gravador.</span><span class="sxs-lookup"><span data-stu-id="592ac-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="592ac-215">Vejamos um cenário para o uso de parâmetros de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="592ac-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="592ac-216">Você tem um serviço implantado de web de aprendizado de máquina do Azure que usa um leitor módulo tooread de dados de uma das fontes de dados de saudação suportadas pelo aprendizado de máquina do Azure (por exemplo: banco de dados do SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="592ac-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="592ac-217">Após a execução do lote hello, resultados de saudação são gravados usando um módulo de gravador (banco de dados do SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="592ac-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="592ac-218">Sem as entradas e saídas são definidas em experiências de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="592ac-219">Nesse caso, é recomendável que você configure os parâmetros de serviço web relevantes para os módulos de leitor e gravador de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="592ac-220">Essa configuração permite Olá leitor/gravador toobe módulos configurado ao usar Olá AzureMLBatchExecution atividade.</span><span class="sxs-lookup"><span data-stu-id="592ac-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="592ac-221">Especificar parâmetros de serviço da Web em Olá **globalParameters** seção atividade Olá JSON da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="592ac-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="592ac-222">Você também pode usar [funções da fábrica de dados](data-factory-functions-variables.md) passar valores para Olá parâmetros de serviço da Web conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="592ac-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="592ac-223">parâmetros de serviço da Web Hello diferenciam maiusculas de minúsculas, portanto, verifique que Olá você especificar na atividade de saudação JSON correspondam Olá aqueles expostos pelo Olá serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="592ac-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="592ac-224">Usando um leitor módulo tooread de dados de vários arquivos no Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="592ac-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="592ac-225">Pipelines de Big Data com atividades como Pig e Hive podem produzir um ou mais arquivos de saída sem extensão.</span><span class="sxs-lookup"><span data-stu-id="592ac-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="592ac-226">Por exemplo, quando você especificar uma tabela de Hive externa, hello dados para a tabela de Hive externo Olá podem ser armazenados no armazenamento de BLOBs do Azure com hello 000000_0 de nome a seguir.</span><span class="sxs-lookup"><span data-stu-id="592ac-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="592ac-227">Você pode usar o módulo de leitor de saudação em um experimento tooread vários arquivos e usá-los para previsões.</span><span class="sxs-lookup"><span data-stu-id="592ac-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="592ac-228">Ao usar o módulo do leitor de saudação em uma experiência de aprendizado de máquina do Azure, você pode especificar o Blob do Azure como uma entrada.</span><span class="sxs-lookup"><span data-stu-id="592ac-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="592ac-229">arquivos de saudação em Olá armazenamento de BLOBs do Azure podem ser arquivos de saída de hello (exemplo: 000000_0) que são produzidos por um script de Pig e Hive em execução no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="592ac-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="592ac-230">Olá módulo reader permite tooread arquivos (com nenhuma extensão) Configurando Olá **toocontainer de caminho, o diretório/blob**.</span><span class="sxs-lookup"><span data-stu-id="592ac-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="592ac-231">Olá **caminho toocontainer** pontos toohello contêiner e **directory/blob** pontos toofolder que contém arquivos de saudação conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="592ac-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="592ac-232">Olá, ou seja, o asterisco \*) **Especifica que todos os Olá arquivos Olá/pasta do contêiner (ou seja, aggregateddata/dados/ano = mês/2014-6 /\*)** são lidas como parte da experiência de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Propriedades de Blob do Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="592ac-234">Exemplo</span><span class="sxs-lookup"><span data-stu-id="592ac-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="592ac-235">Pipeline com a atividade AzureMLBatchExecution com parâmetros de serviço Web</span><span class="sxs-lookup"><span data-stu-id="592ac-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="592ac-236">Em Olá acima exemplo JSON:</span><span class="sxs-lookup"><span data-stu-id="592ac-236">In hello above JSON example:</span></span>

* <span data-ttu-id="592ac-237">Olá implantado aprendizado de máquina do Azure Web serviço usa um leitor e um gravador módulo tooread/gravação de dados de / tooan banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="592ac-238">Esse serviço da Web expõe Olá quatro parâmetros a seguir: nome do servidor, nome do banco de dados, nome de conta de usuário do servidor e senha de conta de usuário do servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="592ac-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="592ac-239">Ambos os valores de data/hora de **início** e de **término** devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="592ac-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="592ac-240">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="592ac-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="592ac-241">Olá **final** tempo é opcional.</span><span class="sxs-lookup"><span data-stu-id="592ac-241">hello **end** time is optional.</span></span> <span data-ttu-id="592ac-242">Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas.**"</span><span class="sxs-lookup"><span data-stu-id="592ac-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="592ac-243">pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="592ac-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="592ac-244">Consulte a [Referência de script JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="592ac-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="592ac-245">Outros cenários</span><span class="sxs-lookup"><span data-stu-id="592ac-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="592ac-246">Serviço Web exige várias entradas</span><span class="sxs-lookup"><span data-stu-id="592ac-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="592ac-247">Se o serviço web de saudação pega várias entradas, use Olá **webServiceInputs** propriedade em vez de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="592ac-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="592ac-248">Conjuntos de dados que são referenciados por Olá **webServiceInputs** também deve ser incluído no hello atividade **entradas**.</span><span class="sxs-lookup"><span data-stu-id="592ac-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="592ac-249">Em seu experimento de Azure ML, as portas de entrada e saída do serviço Web e os parâmetros globais têm nomes padrão ("input1", "input2") os quais você pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="592ac-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="592ac-250">nomes de saudação usados para configurações de globalParameters, webServiceInputs e webserviceoutputs na devem corresponder exatamente aos nomes de saudação em experiências de saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="592ac-251">Você pode exibir a carga de solicitação de exemplo hello na página de ajuda de execução de lote de saudação para o mapeamento do ML do Azure ponto de extremidade tooverify Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="592ac-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="592ac-252">O serviço Web não requer uma entrada</span><span class="sxs-lookup"><span data-stu-id="592ac-252">Web Service does not require an input</span></span>
<span data-ttu-id="592ac-253">Serviços web do Azure ML lote execução pode ser usado toorun quaisquer fluxos de trabalho, por exemplo, R ou scripts de Python, que podem não exigir qualquer entrada.</span><span class="sxs-lookup"><span data-stu-id="592ac-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="592ac-254">Ou então, experimento Olá pode ser configurado com um módulo do leitor que não expõem quaisquer GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="592ac-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="592ac-255">Nesse caso, hello atividade AzureMLBatchExecution será configurada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="592ac-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="592ac-256">O serviço Web não requer uma entrada/saída</span><span class="sxs-lookup"><span data-stu-id="592ac-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="592ac-257">Olá serviço web do ML do Azure batch execução pode não ter nenhuma saída do serviço Web configurada.</span><span class="sxs-lookup"><span data-stu-id="592ac-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="592ac-258">Neste exemplo, não há nenhum serviço Web de entrada ou saída, nem GlobalParameters configurados.</span><span class="sxs-lookup"><span data-stu-id="592ac-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="592ac-259">Ainda há uma saída configurada na atividade de saudação em si, mas ele não é fornecido como um webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="592ac-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="592ac-260">Web Service usa leitores e gravadores e hello atividade é executada somente quando outras atividades tiveram êxito</span><span class="sxs-lookup"><span data-stu-id="592ac-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="592ac-261">Olá módulos do Azure ML web service leitor e gravador podem ser configurado toorun com ou sem qualquer GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="592ac-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="592ac-262">No entanto, talvez você queira tooembed serviço chamadas em um pipeline que usa o serviço de saudação do conjunto de dados dependências tooinvoke apenas quando algum processamento upstream foi concluída.</span><span class="sxs-lookup"><span data-stu-id="592ac-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="592ac-263">Você também pode disparar qualquer outra ação após a execução do lote hello usando essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="592ac-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="592ac-264">Nesse caso, você pode expressar dependências hello usando atividade entradas e saídas, sem nomear qualquer um deles como o serviço Web de entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="592ac-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="592ac-265">Olá **argumentos** são:</span><span class="sxs-lookup"><span data-stu-id="592ac-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="592ac-266">Se o ponto de extremidade de teste usa um webServiceInput: ele é representado por um conjunto de dados de blob e está incluído em entradas de atividade hello e propriedade de webServiceInput hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="592ac-267">Caso contrário, a propriedade de webServiceInput Olá é omitida.</span><span class="sxs-lookup"><span data-stu-id="592ac-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="592ac-268">Se o ponto de extremidade de teste usa webServiceOutput(s): eles são representados por conjuntos de dados de blob e são incluídos nas saídas da atividade de saudação e na propriedade de webserviceoutputs na saudação.</span><span class="sxs-lookup"><span data-stu-id="592ac-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="592ac-269">atividade Hello gera e webserviceoutputs na são mapeados por nome de saudação de cada saída experimento hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="592ac-270">Caso contrário, a propriedade webserviceoutputs de saudação é omitida.</span><span class="sxs-lookup"><span data-stu-id="592ac-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="592ac-271">Se o ponto de extremidade do experimento expõe globalParameter(s), eles recebem na propriedade do hello atividade globalParameters como pares de chave, valor.</span><span class="sxs-lookup"><span data-stu-id="592ac-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="592ac-272">Caso contrário, a propriedade globalParameters de saudação é omitida.</span><span class="sxs-lookup"><span data-stu-id="592ac-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="592ac-273">chaves de saudação diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="592ac-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="592ac-274">[As funções do Azure Data Factory](data-factory-functions-variables.md) pode ser usada em valores hello.</span><span class="sxs-lookup"><span data-stu-id="592ac-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="592ac-275">Conjuntos de dados adicionais podem ser incluídos em Olá entradas e saídas de propriedades de atividade, sem que está sendo referenciado no hello atividade typeProperties.</span><span class="sxs-lookup"><span data-stu-id="592ac-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="592ac-276">Esses conjuntos de dados determinam a execução com dependências de fatia mas caso contrário, são ignorados pelo hello atividade AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="592ac-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="592ac-277">Atualização dos modelos usando a Atividade de Recurso de Atualização</span><span class="sxs-lookup"><span data-stu-id="592ac-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="592ac-278">Depois de terminar com treinamento, atualizar Olá pontuação serviço da web (previsão experimento exposto como um serviço da web) com hello recentemente treinado usando Olá **a atividade de recurso de atualização do Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="592ac-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="592ac-279">Veja o artigo [Atualização de modelos usando a Atividade do Recurso de Atualização](data-factory-azure-ml-update-resource-activity.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="592ac-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="592ac-280">Módulos de leitor e gravador</span><span class="sxs-lookup"><span data-stu-id="592ac-280">Reader and Writer Modules</span></span>
<span data-ttu-id="592ac-281">Um cenário comum para uso de parâmetros de serviço da Web é o uso de saudação do Azure SQL leitores e gravadores.</span><span class="sxs-lookup"><span data-stu-id="592ac-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="592ac-282">módulo do leitor de saudação é usado tooload dados em uma experiência de gerenciamento de serviços de dados fora do estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="592ac-283">módulo de gravador Olá é toosave dados de suas experiências em serviços de gerenciamento de dados fora do estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="592ac-284">Para obter detalhes sobre leitor/gravador do SQL do Azure/Blob do Azure, consulte os tópicos [Leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Gravador](https://msdn.microsoft.com/library/azure/dn905984.aspx) na biblioteca MSDN.</span><span class="sxs-lookup"><span data-stu-id="592ac-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="592ac-285">exemplo Hello na seção anterior Olá usado leitor de BLOBs do Azure hello e gravador de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="592ac-286">Esta seção discute usando o leitor do SQL do Azure e o gravador do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="592ac-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="592ac-287">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="592ac-287">Frequently asked questions</span></span>
<span data-ttu-id="592ac-288">**P:** Tenho vários arquivos que são gerados pelos meus pipelines de Big Data.</span><span class="sxs-lookup"><span data-stu-id="592ac-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="592ac-289">Pode usar o hello atividade AzureMLBatchExecution toowork em todos os arquivos de Olá?</span><span class="sxs-lookup"><span data-stu-id="592ac-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="592ac-290">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="592ac-290">**A:** Yes.</span></span> <span data-ttu-id="592ac-291">Consulte Olá **usando um leitor módulo tooread de dados de vários arquivos no Blob do Azure** seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="592ac-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="592ac-292">Atividade de pontuação do lote do ML do Azure</span><span class="sxs-lookup"><span data-stu-id="592ac-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="592ac-293">Se você estiver usando Olá **AzureMLBatchScoring** toointegrate de atividade com o aprendizado de máquina do Azure, recomendamos que você use hello mais recente **AzureMLBatchExecution** atividade.</span><span class="sxs-lookup"><span data-stu-id="592ac-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="592ac-294">Hello atividade AzureMLBatchExecution é introduzido no hello versão de agosto de 2015 do SDK do Azure e o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="592ac-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="592ac-295">Se você quiser toocontinue usando Olá AzureMLBatchScoring atividade, continue a ler esta seção.</span><span class="sxs-lookup"><span data-stu-id="592ac-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="592ac-296">Atividade de pontuação em lote do ML do Azure usando o armazenamento do Azure para entrada/saída</span><span class="sxs-lookup"><span data-stu-id="592ac-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="592ac-297">Parâmetros de serviço Web</span><span class="sxs-lookup"><span data-stu-id="592ac-297">Web Service Parameters</span></span>
<span data-ttu-id="592ac-298">toospecify valores para parâmetros de serviço da Web, adicione um **typeProperties** seção toohello **AzureMLBatchScoringActivty** seção no pipeline de saudação JSON, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="592ac-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="592ac-299">Você também pode usar [funções da fábrica de dados](data-factory-functions-variables.md) passar valores para Olá parâmetros de serviço da Web conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="592ac-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="592ac-300">parâmetros de serviço da Web Hello diferenciam maiusculas de minúsculas, portanto, verifique que Olá você especificar na atividade de saudação JSON correspondam Olá aqueles expostos pelo Olá serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="592ac-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="592ac-301">Consulte também</span><span class="sxs-lookup"><span data-stu-id="592ac-301">See Also</span></span>
* <span data-ttu-id="592ac-302">
            [Postagem do blog do Azure: Introdução ao Azure Data Factory e Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)</span><span class="sxs-lookup"><span data-stu-id="592ac-302">[Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)</span></span>

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
