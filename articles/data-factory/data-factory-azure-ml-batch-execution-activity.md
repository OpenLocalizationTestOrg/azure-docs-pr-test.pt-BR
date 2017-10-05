---
title: "Criar pipelines de dados de previsão usando o Azure Data Factory | Microsoft Docs"
description: "Descreve como criar pipelines de previsão usando o Azure Data Factory e o Azure Machine Learning"
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
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="36ee3-103">Criar pipelines de previsão usando Azure Machine Learning e o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="36ee3-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="36ee3-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="36ee3-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="36ee3-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="36ee3-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="36ee3-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="36ee3-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="36ee3-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="36ee3-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="36ee3-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="36ee3-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="36ee3-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="36ee3-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="36ee3-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="36ee3-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="36ee3-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="36ee3-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="36ee3-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="36ee3-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="36ee3-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="36ee3-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="36ee3-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="36ee3-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="36ee3-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="36ee3-115">Azure Machine Learning</span></span>
<span data-ttu-id="36ee3-116">O [Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) permite compilar, testar e implantar soluções de análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="36ee3-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="36ee3-117">De um ponto de vista de alto nível, isso é feito em três etapas:</span><span class="sxs-lookup"><span data-stu-id="36ee3-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="36ee3-118">**Crie um teste de treinamento**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-118">**Create a training experiment**.</span></span> <span data-ttu-id="36ee3-119">Conclua esta etapa usando o Estúdio AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="36ee3-120">O Estúdio AM do Azure é um ambiente de desenvolvimento visual colaborativo usado para treinar e testar um modelo de análise preditiva usando dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="36ee3-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="36ee3-121">**Convertê-lo em um teste preditivo**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="36ee3-122">Quando o modelo foi treinado com dados existentes e você estiver pronto para usá-lo para pontuar novos dados, você preparará e simplificará seu teste para a pontuação.</span><span class="sxs-lookup"><span data-stu-id="36ee3-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="36ee3-123">**Implantá-lo como um serviço da Web**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="36ee3-124">Você pode publicar seu experimento de pontuação como um serviço Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="36ee3-125">Você pode enviar dados ao seu modelo por desse ponto de extremidade de serviço Web e receber previsões de resultado do modelo.</span><span class="sxs-lookup"><span data-stu-id="36ee3-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="36ee3-126">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="36ee3-126">Azure Data Factory</span></span>
<span data-ttu-id="36ee3-127">O Data Factory é um serviço de integração de dados baseado em nuvem que automatiza a **movimentação** e a **transformação** dos dados.</span><span class="sxs-lookup"><span data-stu-id="36ee3-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="36ee3-128">Você pode criar soluções de integração de dados usando o Azure Data Factory que podem ingerir dados de vários repositórios de dados, transformar/processar os dados e publicar os dados resultantes nos repositórios de dados.</span><span class="sxs-lookup"><span data-stu-id="36ee3-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="36ee3-129">O serviço Data Factory permite criar pipelines de dados que movem e transformam dados e depois executar os pipelines em um agendamento especificado (por hora, diariamente, semanalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="36ee3-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="36ee3-130">Ele também fornece visualizações avançadas para exibir a linhagem e as dependências entre os pipelines de dados e monitorar todos os seus pipelines de dados em uma única exibição unificada, a fim de identificar os problemas e configurar alertas de monitoramento facilmente.</span><span class="sxs-lookup"><span data-stu-id="36ee3-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="36ee3-131">Consulte os artigos [Introdução ao Azure Data Factory](data-factory-introduction.md) e [Criar seu primeiro pipeline](data-factory-build-your-first-pipeline.md) para começar a introdução ao serviço do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="36ee3-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="36ee3-132">Data Factory e Machine Learning juntos</span><span class="sxs-lookup"><span data-stu-id="36ee3-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="36ee3-133">O Azure Data Factory permite que você crie facilmente pipelines que usam o serviço Web do [Azure Machine Learning][azure-machine-learning] publicado para a análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="36ee3-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="36ee3-134">Usando a **Atividade de Execução em Lote** em um pipeline do Azure Data Factory, você pode invocar um serviço Web de AM do Azure para fazer previsões sobre dados em lote.</span><span class="sxs-lookup"><span data-stu-id="36ee3-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="36ee3-135">Consulte a seção [Invocando um serviço web de AM do Azure usando a Atividade de Execução em Lote](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="36ee3-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="36ee3-136">Ao longo do tempo, os modelos de previsão nos experimentos de pontuação do AM do Azure precisam ser treinados novamente usando novos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="36ee3-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="36ee3-137">Você pode treinar novamente um modelo do AM do Azure de um pipeline do Data Factory executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36ee3-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="36ee3-138">Publique o experimento de treinamento (e não um experimento preditivo) como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="36ee3-139">Essa etapa é feita no Estúdio AM do Azure como você fez para expor o experimento preditivo como um serviço Web no cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="36ee3-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="36ee3-140">Use a Atividade de Execução de Lote do AM do Azure para chamar o serviço Web para o experimento de treinamento.</span><span class="sxs-lookup"><span data-stu-id="36ee3-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="36ee3-141">Basicamente, você pode usar a atividade de Execução de Lote do AM do Azure para invocar o serviço Web de treinamento e o serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="36ee3-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="36ee3-142">Depois de concluir o treinamento, atualize o serviço Web de pontuação (experimento preditivo exposto como um serviço Web) com o modelo recém-treinado usando a **Atividade de recurso de Atualização de AM do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="36ee3-143">Veja o artigo [Atualização de modelos usando a Atividade do Recurso de Atualização](data-factory-azure-ml-update-resource-activity.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="36ee3-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="36ee3-144">Invocar um serviço Web usando a Atividade de Execução em Lote</span><span class="sxs-lookup"><span data-stu-id="36ee3-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="36ee3-145">Você usa o Azure Data Factory para orquestrar o processamento e movimentação de dados e realizar a execução de lote usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="36ee3-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="36ee3-146">Estas são as etapas de nível superior:</span><span class="sxs-lookup"><span data-stu-id="36ee3-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="36ee3-147">Criar um serviço vinculado de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="36ee3-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="36ee3-148">Você precisará dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="36ee3-148">You need the following values:</span></span>

   1. <span data-ttu-id="36ee3-149">**URI de Solicitação** para a API de Execução do Lote.</span><span class="sxs-lookup"><span data-stu-id="36ee3-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="36ee3-150">Encontre o URI da Solicitação clicando no link **EXECUÇÃO EM LOTE** na página de serviços Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="36ee3-151">
            **Chave de API** para o serviço Web publicado do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="36ee3-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="36ee3-152">Encontre a chave de API clicando no serviço Web que você publicou.</span><span class="sxs-lookup"><span data-stu-id="36ee3-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="36ee3-153">Use a atividade **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="36ee3-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Painel de Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI do lote](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="36ee3-156">Cenário: Experimentos usando entradas/saídas de serviço Web que se referem aos dados no armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="36ee3-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="36ee3-157">Nesse cenário, o serviço Web de Azure Machine Learning faz previsões usando dados de um arquivo em um armazenamento de blob do Azure e armazena os resultados de previsão no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="36ee3-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="36ee3-158">O JSON a seguir define um pipeline do Data Factory com uma atividade AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="36ee3-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="36ee3-159">A atividade contém o conjunto de dados **DecisionTreeInputBlob** como entrada e **DecisionTreeResultBlob** como a saída.</span><span class="sxs-lookup"><span data-stu-id="36ee3-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="36ee3-160">O **DecisionTreeInputBlob** é passado como uma entrada para o serviço Web usando a propriedade JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="36ee3-161">O **DecisionTreeResultBlob** é passado como uma saída para o serviço Web usando a propriedade JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="36ee3-162">Se o serviço Web receber várias entradas, use a propriedade **webServiceInputs** em vez de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="36ee3-163">Veja a seção [Serviço Web exige várias entradas](#web-service-requires-multiple-inputs) para obter um exemplo de como usar a propriedade webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="36ee3-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="36ee3-164">Conjuntos de dados que são referenciados pelas propriedades **webServiceInput**/**webServiceInputs** e **webServiceOutputs** (em **typeProperties**) também devem ser incluídas nas **entradas** e **saídas** da atividade.</span><span class="sxs-lookup"><span data-stu-id="36ee3-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="36ee3-165">Em seu experimento de Azure ML, as portas de entrada e saída do serviço Web e os parâmetros globais têm nomes padrão ("input1", "input2") os quais você pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="36ee3-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="36ee3-166">Os nomes que você usa para as configurações webServiceInputs, webserviceoutputs e globalParameters devem corresponder exatamente aos nomes nos testes.</span><span class="sxs-lookup"><span data-stu-id="36ee3-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="36ee3-167">Você pode exibir a carga de solicitação de exemplo na página de Ajuda de Execução do Lote no ponto de extremidade de Azure ML para verificar o mapeamento esperado.</span><span class="sxs-lookup"><span data-stu-id="36ee3-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
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
> <span data-ttu-id="36ee3-168">Apenas as entradas e saídas da atividade AzureMLBatchExecution podem ser passadas como parâmetros para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="36ee3-169">Por exemplo, no trecho JSON acima, DecisionTreeInputBlob é uma entrada para a atividade de AzureMLBatchExecution, que é passada como entrada para o serviço Web a través do parâmetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="36ee3-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="36ee3-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="36ee3-170">Example</span></span>
<span data-ttu-id="36ee3-171">Este exemplo usa o armazenamento do Azure para conter tanto os dados de entrada quanto os de saída.</span><span class="sxs-lookup"><span data-stu-id="36ee3-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="36ee3-172">Recomendamos que você percorra o tutorial [Compilar seu primeiro pipeline com o Data Factory][adf-build-1st-pipeline] antes de usar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="36ee3-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="36ee3-173">Use o Editor do Data Factory para criar artefatos do Data Factory (serviços vinculados, conjuntos de dados, pipeline) neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="36ee3-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="36ee3-174">Criar um **serviço vinculado** para o **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="36ee3-175">Se os arquivos de entrada e saída estiverem em contas de armazenamento diferentes, você precisará de dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="36ee3-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="36ee3-176">Aqui está um exemplo JSON:</span><span class="sxs-lookup"><span data-stu-id="36ee3-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="36ee3-177">Criar a **entrada** do **conjunto de dados** do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="36ee3-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="36ee3-178">Ao contrário de alguns outros conjuntos de dados do Data Factory, esses conjuntos de dados devem conter os valores **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="36ee3-179">Você pode usar o particionamento para fazer com que cada execução em lote (cada fatia de dados) processe ou produza arquivos de entrada e saída exclusiva.</span><span class="sxs-lookup"><span data-stu-id="36ee3-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="36ee3-180">Você precisará incluir algumas atividades upstream para transformar a entrada no formato de arquivo CSV e colocá-lo na conta de armazenamento para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="36ee3-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="36ee3-181">Nesse caso, não inclua as configurações **external** e **externalData** mostradas no exemplo a seguir e seu DecisionTreeInputBlob seria o conjunto de dados de saída de uma Atividade diferente.</span><span class="sxs-lookup"><span data-stu-id="36ee3-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="36ee3-182">O arquivo csv de entrada deve ter a linha de cabeçalho de coluna.</span><span class="sxs-lookup"><span data-stu-id="36ee3-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="36ee3-183">Se você estiver usando a **Atividade de cópia** para criar/mover o csv para dentro do armazenamento de blobs, você deve definir a propriedade de coleta **blobWriterAddHeade**r como **true**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="36ee3-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="36ee3-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="36ee3-185">Se o arquivo csv não tem a linha de cabeçalho, você poderá ver o seguinte erro: **Erro na atividade: erro ao ler a cadeia de caracteres. Token inesperado: StartObject. Caminho '', linha 1, posição 1**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="36ee3-186">Criar a **saída** do **conjunto de dados** da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="36ee3-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="36ee3-187">Este exemplo usa o particionamento para criar um caminho de saída exclusivo para cada execução de divisão.</span><span class="sxs-lookup"><span data-stu-id="36ee3-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="36ee3-188">Sem o particionamento, a atividade substituiria o arquivo.</span><span class="sxs-lookup"><span data-stu-id="36ee3-188">Without the partitioning, the activity would overwrite the file.</span></span>

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
4. <span data-ttu-id="36ee3-189">Crie um **serviço vinculado** do tipo **AzureMLLinkedService**, fornecendo a chave de API e a URL de execução de lote do modelo.</span><span class="sxs-lookup"><span data-stu-id="36ee3-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="36ee3-190">Por fim, crie um pipeline que contenha uma atividade **AzureMLBatchScoring** .</span><span class="sxs-lookup"><span data-stu-id="36ee3-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="36ee3-191">Em tempo de execução, o pipeline executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36ee3-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="36ee3-192">Obtém o local do arquivo de entrada de seus conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="36ee3-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="36ee3-193">Invocar a API de execução em lote do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="36ee3-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="36ee3-194">Copia a saída da execução em lote no blob especificado no conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="36ee3-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="36ee3-195">A atividade AzureMLBatchExecution pode ter zero ou mais entradas e uma ou mais saídas.</span><span class="sxs-lookup"><span data-stu-id="36ee3-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="36ee3-196">Ambos os valores de data/hora de **início** e de **término** devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="36ee3-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="36ee3-197">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="36ee3-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="36ee3-198">O tempo **final** é opcional.</span><span class="sxs-lookup"><span data-stu-id="36ee3-198">The **end** time is optional.</span></span> <span data-ttu-id="36ee3-199">Se você não especificar o valor para a propriedade **end**, ele será calculado como "**início + 48 horas**"</span><span class="sxs-lookup"><span data-stu-id="36ee3-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="36ee3-200">Para executar o pipeline indefinidamente, especifique **9999-09-09** como o valor para a propriedade **end**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="36ee3-201">Consulte a [Referência de script JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="36ee3-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="36ee3-202">A especificação de entrada para a atividade AzureMLBatchExecution é opcional.</span><span class="sxs-lookup"><span data-stu-id="36ee3-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="36ee3-203">Cenário: Experimentos usando módulos Leitor/Gravador para fazer referência a dados em vários armazenamentos</span><span class="sxs-lookup"><span data-stu-id="36ee3-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="36ee3-204">Outro cenário comum durante a criação de experimentos AM do Azure é usar módulos Leitor e Gravador.</span><span class="sxs-lookup"><span data-stu-id="36ee3-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="36ee3-205">O módulo leitor é usado para carregar dados em um experimento e o módulo gravador é usado para salvar os dados dos experimentos.</span><span class="sxs-lookup"><span data-stu-id="36ee3-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="36ee3-206">Para obter detalhes sobre os módulos de leitor e gravador, consulte os tópicos [Leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Gravador](https://msdn.microsoft.com/library/azure/dn905984.aspx) na biblioteca MSDN.</span><span class="sxs-lookup"><span data-stu-id="36ee3-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="36ee3-207">Ao usar os módulos leitor e gravador, é recomendável usar um parâmetro de serviço Web para cada propriedade desses módulos leitor/gravador.</span><span class="sxs-lookup"><span data-stu-id="36ee3-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="36ee3-208">Esses parâmetros da Web permitem que você configure os valores durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="36ee3-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="36ee3-209">Por exemplo, você poderia criar um experimento com um módulo leitor que usa um banco de dados SQL do Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="36ee3-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="36ee3-210">Depois que o serviço web tiver sido implantado, você precisa habilitar os consumidores do serviço Web para especificar outro servidor SQL do Azure chamado YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="36ee3-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="36ee3-211">Você pode usar um parâmetro de serviço Web para permitir que esse valor seja configurado.</span><span class="sxs-lookup"><span data-stu-id="36ee3-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="36ee3-212">A saída e entrada de serviço Web são diferentes dos parâmetros de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="36ee3-213">No primeiro cenário, você viu como uma entrada e saída podem ser especificados para um serviço Web do AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="36ee3-214">Nesse cenário, você pode passar parâmetros para um serviço Web que correspondem às propriedades dos módulos de leitor/gravador.</span><span class="sxs-lookup"><span data-stu-id="36ee3-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="36ee3-215">Vejamos um cenário para o uso de parâmetros de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="36ee3-216">Você tem um serviço Web implantado de Azure Machine Learning que usa um módulo de leitor para ler dados de uma das fontes de dados compatíveis com o Azure Machine Learning (por exemplo: Banco de Dados SQL do Azure).</span><span class="sxs-lookup"><span data-stu-id="36ee3-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="36ee3-217">Após a execução do lote, os resultados são gravados usando um módulo Gravador (banco de dados SQL do Azure).</span><span class="sxs-lookup"><span data-stu-id="36ee3-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="36ee3-218">Não há entradas e saídas de serviço Web definidas nos experimentos.</span><span class="sxs-lookup"><span data-stu-id="36ee3-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="36ee3-219">Nesse caso, recomendamos que você configure os parâmetros de serviço Web relevantes para os módulos de leitor e gravador.</span><span class="sxs-lookup"><span data-stu-id="36ee3-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="36ee3-220">Essa configuração permite que os módulos de leitor/gravador sejam configurados ao usar a atividade AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="36ee3-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="36ee3-221">Você especifica parâmetros de serviço Web na seção **globalParameters** no JSON da atividade da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="36ee3-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="36ee3-222">Você também pode usar [Funções do Data Factory](data-factory-functions-variables.md) para passar valores para os parâmetros do serviço Web conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36ee3-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="36ee3-223">Os parâmetros de serviço Web diferenciam maiúsculas de minúsculas, portanto, garanta que os nomes que você especificar na atividade de JSON correspondam aos expostos pelo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="36ee3-224">Uso de um módulo Leitor para ler dados de vários arquivos no Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="36ee3-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="36ee3-225">Pipelines de Big Data com atividades como Pig e Hive podem produzir um ou mais arquivos de saída sem extensão.</span><span class="sxs-lookup"><span data-stu-id="36ee3-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="36ee3-226">Por exemplo, quando você especifica uma tabela externa do Hive, os dados para a tabela externa do Hive podem ser armazenados no armazenamento de blob do Azure com o seguinte nome 000000_0.</span><span class="sxs-lookup"><span data-stu-id="36ee3-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="36ee3-227">É possível usar o módulo leitor em um experimento para ler vários arquivos e usá-los para previsões.</span><span class="sxs-lookup"><span data-stu-id="36ee3-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="36ee3-228">Ao usar o módulo de leitor em uma experiência de Azure Machine Learning, é possível especificar o Blob do Azure como uma entrada.</span><span class="sxs-lookup"><span data-stu-id="36ee3-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="36ee3-229">Os arquivos no Armazenamento de Blobs do Azure podem ser os arquivos de saída (Exemplo: 000000_0) que são produzidos por um script de Pig e Hive em execução no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36ee3-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="36ee3-230">O módulo de leitor permite que você leia arquivos (sem extensões), configurando o **Caminho para o contêiner, blob/diretório**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="36ee3-231">O **Caminho para o contêiner** aponta para o contêiner e o **diretório/blob** aponta para a pasta que contém os arquivos, conforme mostra a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="36ee3-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="36ee3-232">O asterisco, \*), **especifica que todos os arquivos no contêiner/pasta (ou seja, data/aggregateddata/year=2014/month-6/\*)** são lidos como parte do teste.</span><span class="sxs-lookup"><span data-stu-id="36ee3-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Propriedades de Blob do Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="36ee3-234">Exemplo</span><span class="sxs-lookup"><span data-stu-id="36ee3-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="36ee3-235">Pipeline com a atividade AzureMLBatchExecution com parâmetros de serviço Web</span><span class="sxs-lookup"><span data-stu-id="36ee3-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="36ee3-236">No exemplo JSON acima:</span><span class="sxs-lookup"><span data-stu-id="36ee3-236">In the above JSON example:</span></span>

* <span data-ttu-id="36ee3-237">O serviço Web implantado de Azure Machine Learning usa um modulo leitor e gravador para ler/gravar dados de/para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="36ee3-238">Este serviço Web expõe os seguintes quatro parâmetros: Nome do servidor de banco de dados, Nome do banco de dados, Nome de conta de usuário do servidor e Senha de conta de usuário do servidor.</span><span class="sxs-lookup"><span data-stu-id="36ee3-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="36ee3-239">Ambos os valores de data/hora de **início** e de **término** devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="36ee3-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="36ee3-240">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="36ee3-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="36ee3-241">O tempo **final** é opcional.</span><span class="sxs-lookup"><span data-stu-id="36ee3-241">The **end** time is optional.</span></span> <span data-ttu-id="36ee3-242">Se você não especificar o valor para a propriedade **end**, ele será calculado como "**início + 48 horas**"</span><span class="sxs-lookup"><span data-stu-id="36ee3-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="36ee3-243">Para executar o pipeline indefinidamente, especifique **9999-09-09** como o valor para a propriedade **end**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="36ee3-244">Consulte a [Referência de script JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter detalhes sobre as propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="36ee3-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="36ee3-245">Outros cenários</span><span class="sxs-lookup"><span data-stu-id="36ee3-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="36ee3-246">Serviço Web exige várias entradas</span><span class="sxs-lookup"><span data-stu-id="36ee3-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="36ee3-247">Se o serviço Web receber várias entradas, use a propriedade **webServiceInputs** em vez de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="36ee3-248">Os conjuntos de dados referenciados por **webServiceInputs** também devem ser incluídos nas **entradas** da Atividade.</span><span class="sxs-lookup"><span data-stu-id="36ee3-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="36ee3-249">Em seu experimento de Azure ML, as portas de entrada e saída do serviço Web e os parâmetros globais têm nomes padrão ("input1", "input2") os quais você pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="36ee3-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="36ee3-250">Os nomes que você usa para as configurações webServiceInputs, webserviceoutputs e globalParameters devem corresponder exatamente aos nomes nos testes.</span><span class="sxs-lookup"><span data-stu-id="36ee3-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="36ee3-251">Você pode exibir a carga de solicitação de exemplo na página de Ajuda de Execução do Lote no ponto de extremidade de Azure ML para verificar o mapeamento esperado.</span><span class="sxs-lookup"><span data-stu-id="36ee3-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="36ee3-252">O serviço Web não requer uma entrada</span><span class="sxs-lookup"><span data-stu-id="36ee3-252">Web Service does not require an input</span></span>
<span data-ttu-id="36ee3-253">Os serviços Web de execução em lote do ML do Azure podem ser usados para executar qualquer fluxo de trabalho, por exemplo, scripts R ou Python, e esses podem não exigir entradas.</span><span class="sxs-lookup"><span data-stu-id="36ee3-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="36ee3-254">Ou o teste pode ser configurado com um módulo Leitor que não expõe GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="36ee3-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="36ee3-255">Nesse caso, a atividade AzureMLBatchExecution seria configurada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="36ee3-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="36ee3-256">O serviço Web não requer uma entrada/saída</span><span class="sxs-lookup"><span data-stu-id="36ee3-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="36ee3-257">O serviço Web de execução de lote do ML do Azure pode não ter nenhuma saída de serviço Web configurada.</span><span class="sxs-lookup"><span data-stu-id="36ee3-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="36ee3-258">Neste exemplo, não há nenhum serviço Web de entrada ou saída, nem GlobalParameters configurados.</span><span class="sxs-lookup"><span data-stu-id="36ee3-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="36ee3-259">Ainda há uma saída configurada na própria atividade, mas ela não é fornecida como um webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="36ee3-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="36ee3-260">O serviço Web usa leitores e gravadores, e a atividade será executada somente quando outras atividades tiverem êxito.</span><span class="sxs-lookup"><span data-stu-id="36ee3-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="36ee3-261">Os módulos leitor e gravador do serviço Web do ML do Azure podem ser configurados para executar com ou sem GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="36ee3-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="36ee3-262">No entanto, convém inserir chamadas de serviço em um pipeline que usa as dependências do conjunto de dados para chamar o serviço apenas quando algum processamento upstream for concluído.</span><span class="sxs-lookup"><span data-stu-id="36ee3-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="36ee3-263">Você também pode disparar alguma outra ação após a execução em lote usando esta abordagem.</span><span class="sxs-lookup"><span data-stu-id="36ee3-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="36ee3-264">Nesse caso, você pode expressar as dependências usando as entradas e saídas de atividade sem nomeá-las como entradas ou saídas do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="36ee3-265">Os **aprendizados** são:</span><span class="sxs-lookup"><span data-stu-id="36ee3-265">The **takeaways** are:</span></span>

* <span data-ttu-id="36ee3-266">Se o ponto de extremidade do teste usar um webServiceInput:, ele será representado por um conjunto de dados de blob e será incluído nas entradas da atividade e na propriedade webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="36ee3-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="36ee3-267">Caso contrário, a propriedade webServiceInput é omitida.</span><span class="sxs-lookup"><span data-stu-id="36ee3-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="36ee3-268">Se o ponto de extremidade do teste usar um webServiceOutput(s):, ele será representado por um conjunto de dados de blob e será incluído nas saídas da atividade e na propriedade webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="36ee3-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="36ee3-269">A saída da atividade e webServiceOutputs são mapeados de acordo com o nome de cada saída no teste.</span><span class="sxs-lookup"><span data-stu-id="36ee3-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="36ee3-270">Caso contrário, a propriedade webServiceOutputs é omitida.</span><span class="sxs-lookup"><span data-stu-id="36ee3-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="36ee3-271">Se o ponto de extremidade do teste expor globalParameter(s), eles serão fornecidos na propriedade globalParameters da atividade como pares de valor e chave.</span><span class="sxs-lookup"><span data-stu-id="36ee3-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="36ee3-272">Caso contrário, a propriedade globalParameters é omitida.</span><span class="sxs-lookup"><span data-stu-id="36ee3-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="36ee3-273">As chaves diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="36ee3-273">The keys are case-sensitive.</span></span> <span data-ttu-id="36ee3-274">[funções do Azure Data Factory](data-factory-functions-variables.md) podem ser usadas nos valores.</span><span class="sxs-lookup"><span data-stu-id="36ee3-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="36ee3-275">Podem ser incluídos nas propriedades de entrada e saída da atividade conjuntos de dados adicionais, sem serem referenciados no typeProperties da atividade.</span><span class="sxs-lookup"><span data-stu-id="36ee3-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="36ee3-276">Esses conjuntos de dados determinam a execução com dependências de fatia, mas são ignorados pela atividade AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="36ee3-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="36ee3-277">Atualização dos modelos usando a Atividade de Recurso de Atualização</span><span class="sxs-lookup"><span data-stu-id="36ee3-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="36ee3-278">Depois de concluir o treinamento, atualize o serviço Web de pontuação (experimento preditivo exposto como um serviço Web) com o modelo recém-treinado usando a **Atividade de recurso de Atualização de AM do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36ee3-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="36ee3-279">Veja o artigo [Atualização de modelos usando a Atividade do Recurso de Atualização](data-factory-azure-ml-update-resource-activity.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="36ee3-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="36ee3-280">Módulos de leitor e gravador</span><span class="sxs-lookup"><span data-stu-id="36ee3-280">Reader and Writer Modules</span></span>
<span data-ttu-id="36ee3-281">Um cenário comum de uso de parâmetros de serviço Web é o uso de leitores e gravadores do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="36ee3-282">O módulo de leitor é usado para carregar dados em um teste a partir de serviços de gerenciamento de dados fora do Estúdio de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="36ee3-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="36ee3-283">O módulo de gravador é usado para salvar dados de seu teste nos serviços de gerenciamento de dados fora do Estúdio de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="36ee3-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="36ee3-284">Para obter detalhes sobre leitor/gravador do SQL do Azure/Blob do Azure, consulte os tópicos [Leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Gravador](https://msdn.microsoft.com/library/azure/dn905984.aspx) na biblioteca MSDN.</span><span class="sxs-lookup"><span data-stu-id="36ee3-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="36ee3-285">O exemplo na seção anterior usou o leitor de blobs do Azure e o gravador de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="36ee3-286">Esta seção discute usando o leitor do SQL do Azure e o gravador do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ee3-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="36ee3-287">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="36ee3-287">Frequently asked questions</span></span>
<span data-ttu-id="36ee3-288">**P:** Tenho vários arquivos que são gerados pelos meus pipelines de Big Data.</span><span class="sxs-lookup"><span data-stu-id="36ee3-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="36ee3-289">Posso usar a atividade AzureMLBatchExecution para trabalhar em todos os arquivos?</span><span class="sxs-lookup"><span data-stu-id="36ee3-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="36ee3-290">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="36ee3-290">**A:** Yes.</span></span> <span data-ttu-id="36ee3-291">Confira a seção **Usando um módulo Leitor para ler dados de vários arquivos no Blob do Azure** para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="36ee3-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="36ee3-292">Atividade de pontuação do lote do ML do Azure</span><span class="sxs-lookup"><span data-stu-id="36ee3-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="36ee3-293">Se você estiver usando a atividade **AzureMLBatchScoring** para integrar-se ao Azure Machine Learning, recomendamos que você use a atividade **AzureMLBatchExecution** mais recente.</span><span class="sxs-lookup"><span data-stu-id="36ee3-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="36ee3-294">A atividade AzureMLBatchExecution foi introduzida na versão de agosto de 2015 do Azure SDK e Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36ee3-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="36ee3-295">Se você quiser continuar usando a atividade AzureMLBatchScoring, continue lendo esta seção.</span><span class="sxs-lookup"><span data-stu-id="36ee3-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="36ee3-296">Atividade de pontuação em lote do ML do Azure usando o armazenamento do Azure para entrada/saída</span><span class="sxs-lookup"><span data-stu-id="36ee3-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="36ee3-297">Parâmetros de serviço Web</span><span class="sxs-lookup"><span data-stu-id="36ee3-297">Web Service Parameters</span></span>
<span data-ttu-id="36ee3-298">Para especificar valores para parâmetros de serviço Web, adicione uma seção **typeProperties** à seção **AzureMLBatchScoringActivty** no JSON do pipeline, conforme mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36ee3-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="36ee3-299">Você também pode usar [Funções do Data Factory](data-factory-functions-variables.md) para passar valores para os parâmetros do serviço Web conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36ee3-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="36ee3-300">Os parâmetros de serviço Web diferenciam maiúsculas de minúsculas, portanto, garanta que os nomes que você especificar na atividade de JSON correspondam aos expostos pelo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="36ee3-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="36ee3-301">Consulte também</span><span class="sxs-lookup"><span data-stu-id="36ee3-301">See Also</span></span>
* <span data-ttu-id="36ee3-302">
            [Postagem do blog do Azure: Introdução ao Azure Data Factory e Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)</span><span class="sxs-lookup"><span data-stu-id="36ee3-302">[Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)</span></span>

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
