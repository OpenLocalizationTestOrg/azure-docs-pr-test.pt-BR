---
title: Atualizar modelos de Machine Learning usando o Azure Data Factory | Microsoft Docs
description: "Descreve como criar pipelines de previsão usando o Azure Data Factory e o Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="fa79d-103">Atualizando os modelos do Machine Learning do Azure usando a Atividade de Recurso de Atualização</span><span class="sxs-lookup"><span data-stu-id="fa79d-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="fa79d-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="fa79d-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="fa79d-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="fa79d-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="fa79d-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="fa79d-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="fa79d-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="fa79d-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="fa79d-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="fa79d-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="fa79d-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fa79d-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="fa79d-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fa79d-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="fa79d-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="fa79d-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="fa79d-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fa79d-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="fa79d-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="fa79d-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="fa79d-114">Este artigo complementa o principal Azure Data Factory - Artigo de integração do Azure Machine Learning: [Criar pipelines de previsão usando o Azure Machine Learning e o Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="fa79d-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="fa79d-115">Se você ainda não fez isso, leia o artigo principal antes de ler este.</span><span class="sxs-lookup"><span data-stu-id="fa79d-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="fa79d-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fa79d-116">Overview</span></span>
<span data-ttu-id="fa79d-117">Ao longo do tempo, os modelos de previsão nos experimentos de pontuação do AM do Azure precisam ser treinados novamente usando novos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="fa79d-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="fa79d-118">Depois de concluir o novo treinamento, você deseja atualizar o serviço Web de pontuação com o modelo do AM treinado novamente.</span><span class="sxs-lookup"><span data-stu-id="fa79d-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="fa79d-119">As etapas típicas para habilitar novos treinamentos e a atualização de modelos do AM do Azure por meio de serviços Web são:</span><span class="sxs-lookup"><span data-stu-id="fa79d-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="fa79d-120">Crie um teste no [Estúdio AM do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="fa79d-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="fa79d-121">Quando estiver satisfeito com o modelo, use o Estúdio AM do Azure para publicar serviços Web para o **teste de treinamento** e o teste de pontuação/**previsão**.</span><span class="sxs-lookup"><span data-stu-id="fa79d-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="fa79d-122">A tabela a seguir descreve os serviços Web usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="fa79d-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="fa79d-123">Confira [Readaptar os modelos do Machine Learning de forma programática](../machine-learning/machine-learning-retrain-models-programmatically.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fa79d-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="fa79d-124">**Treinamento do serviço Web** - recebe dados de treinamento e produz modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="fa79d-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="fa79d-125">A saída do novo treinamento é um arquivo .ilearner em um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="fa79d-126">O **ponto de extremidade padrão** é criado automaticamente para você quando o experimento de treinamento é publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="fa79d-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="fa79d-127">Você pode criar mais pontos de extremidade, mas o exemplo usa apenas o ponto de extremidade padrão.</span><span class="sxs-lookup"><span data-stu-id="fa79d-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="fa79d-128">**Pontuação do serviço Web** - recebe exemplos de dados sem rótulo de e faz previsões.</span><span class="sxs-lookup"><span data-stu-id="fa79d-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="fa79d-129">A saída de previsão pode ter diversas formas, como um arquivo .csv ou linhas em um banco de dados SQL do Azure, dependendo da configuração do experimento.</span><span class="sxs-lookup"><span data-stu-id="fa79d-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="fa79d-130">O ponto de extremidade padrão é criado automaticamente para você quando o teste preditivo é publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="fa79d-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="fa79d-131">A figura a seguir descreve o relacionamento entre os pontos de extremidade de treinamento e de pontuação no AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVIÇOS WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="fa79d-133">Você pode invocar o **training web service** usando o **Atividade de Execução de Lote do AM do Azure**.</span><span class="sxs-lookup"><span data-stu-id="fa79d-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="fa79d-134">A invocação de um serviço Web de treinamento é igual à invocação de um serviço Web do AM do Azure ML (serviço Web de pontuação) para pontuação de dados.</span><span class="sxs-lookup"><span data-stu-id="fa79d-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="fa79d-135">As seções anteriores abordam em detalhes como invocar um serviço Web de AM do Azure de um pipeline do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fa79d-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="fa79d-136">Você pode invocar o **scoring web service** usando o **Atividade de Recurso de Atualização de AM do Azure** para atualizar o serviço Web com o modelo recém-treinado.</span><span class="sxs-lookup"><span data-stu-id="fa79d-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="fa79d-137">Os exemplos a seguir fornecem as definições de serviço vinculado:</span><span class="sxs-lookup"><span data-stu-id="fa79d-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="fa79d-138">Serviço web de pontuação é um serviço web clássico</span><span class="sxs-lookup"><span data-stu-id="fa79d-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="fa79d-139">Se o serviço web de pontuação é um **serviço web clássico**, crie o segundo **ponto de extremidade não padrão e atualizável** usando o [portal do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fa79d-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="fa79d-140">Confira o artigo [Criar pontos de extremidade](../machine-learning/machine-learning-create-endpoint.md) para conhecer as etapas.</span><span class="sxs-lookup"><span data-stu-id="fa79d-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="fa79d-141">Depois de criar o ponto de extremidade atualizável não padrão, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fa79d-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="fa79d-142">Clique em **EXECUÇÃO EM LOTE** para obter o valor do URI para a propriedade JSON **mlEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="fa79d-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="fa79d-143">Clique no link **ATUALIZAR RECURSO** para obter o valor do URI para a propriedade JSON **updateResourceEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="fa79d-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="fa79d-144">A chave de API está na própria página do ponto de extremidade (no canto inferior direito).</span><span class="sxs-lookup"><span data-stu-id="fa79d-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![ponto de extremidade atualizável](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="fa79d-146">O exemplo a seguir fornece um exemplo de definição de JSON para o serviço AzureML vinculado.</span><span class="sxs-lookup"><span data-stu-id="fa79d-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="fa79d-147">O serviço vinculado usa o apiKey para autenticação.</span><span class="sxs-lookup"><span data-stu-id="fa79d-147">The linked service uses the apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="fa79d-148">Serviço Web de pontuação é um serviço Web do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa79d-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="fa79d-149">Se o serviço web é o novo tipo de serviço da web que expõe um ponto de extremidade do Azure Resource Manager, você não precisa adicionar o segundo **não-padrão** ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fa79d-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="fa79d-150">O **updateResourceEndpoint** no serviço vinculado está no formato:</span><span class="sxs-lookup"><span data-stu-id="fa79d-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="fa79d-151">Você pode obter valores para espaços reservados na URL ao consultar o serviço da web sobre o [Portal de serviços da Web do Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="fa79d-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="fa79d-152">O novo tipo de ponto de extremidade de recursos de atualização requer um token do AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fa79d-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="fa79d-153">Especifique **servicePrincipalId** e **servicePrincipalKey**no serviço vinculado do AzureML.</span><span class="sxs-lookup"><span data-stu-id="fa79d-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="fa79d-154">Consulte [como criar entidade de serviço e atribuir permissões para gerenciar recursos do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fa79d-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="fa79d-155">Aqui está um exemplo de definição de serviço AzureML vinculado:</span><span class="sxs-lookup"><span data-stu-id="fa79d-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="fa79d-156">O cenário a seguir fornece mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="fa79d-156">The following scenario provides more details.</span></span> <span data-ttu-id="fa79d-157">Ele tem um exemplo de readaptação e atualização de modelos de AM do Azure de um pipeline do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fa79d-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="fa79d-158">Cenário: novo treinamento e atualização de um modelo do AM do Azure</span><span class="sxs-lookup"><span data-stu-id="fa79d-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="fa79d-159">Esta seção fornece um pipeline de exemplo que usa a **atividade de Execução em lote do AM do Azure** para treinar novamente um modelo.</span><span class="sxs-lookup"><span data-stu-id="fa79d-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="fa79d-160">O pipeline também usa a **atividade do Recurso de atualização do AM do Azure** para atualizar o modelo no serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="fa79d-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="fa79d-161">A seção também fornece trechos de JSON para todos os serviços vinculados, conjuntos de dados e pipeline no exemplo.</span><span class="sxs-lookup"><span data-stu-id="fa79d-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="fa79d-162">Este é o modo de exibição de diagrama do pipeline de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fa79d-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="fa79d-163">Como você pode ver, a atividade de Execução em lote do AM do Azure assume a entrada de treinamento e produz uma saída de treinamento (arquivo iLearner).</span><span class="sxs-lookup"><span data-stu-id="fa79d-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="fa79d-164">A Atividade de Recurso de Atualização do AM do Azure obtém a saída deste treinamento e atualiza o modelo no ponto de extremidade de serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="fa79d-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="fa79d-165">A Atividade do Recurso de Atualização não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="fa79d-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="fa79d-166">O placeholderBlob é apenas um conjunto de dados de saída fictício necessário ao serviço Azure Data Factory para executar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="fa79d-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![diagrama de pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="fa79d-168">Serviço vinculado do armazenamento de Blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="fa79d-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="fa79d-169">O Armazenamento do Azure contém os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="fa79d-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="fa79d-170">dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="fa79d-170">training data.</span></span> <span data-ttu-id="fa79d-171">Os dados de entrada para o serviço Web de treinamento de AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="fa79d-172">Arquivo iLearner.</span><span class="sxs-lookup"><span data-stu-id="fa79d-172">iLearner file.</span></span> <span data-ttu-id="fa79d-173">Os dados de saída do serviço Web de treinamento de AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="fa79d-174">Este arquivo também é a entrada para a atividade do Recurso de atualização.</span><span class="sxs-lookup"><span data-stu-id="fa79d-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="fa79d-175">Veja a definição JSON de exemplo do serviço vinculado:</span><span class="sxs-lookup"><span data-stu-id="fa79d-175">Here is the sample JSON definition of the linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="fa79d-176">Conjunto de dados de entrada do treinamento:</span><span class="sxs-lookup"><span data-stu-id="fa79d-176">Training input dataset:</span></span>
<span data-ttu-id="fa79d-177">O conjunto de dados a seguir representa os dados de treinamento de entrada do serviço Web de treinamento do AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="fa79d-178">A atividade de Execução de Lote do AM do Azure obtém esse conjunto de dados como uma entrada.</span><span class="sxs-lookup"><span data-stu-id="fa79d-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="fa79d-179">Conjunto de dados de saída de treinamento:</span><span class="sxs-lookup"><span data-stu-id="fa79d-179">Training output dataset:</span></span>
<span data-ttu-id="fa79d-180">O conjunto de dados a seguir representa o arquivo do iLearner de saída do serviço Web de treinamento do AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="fa79d-181">A Atividade de Execução de Lote do AM do Azure produz este conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="fa79d-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="fa79d-182">O conjunto de dados também é a entrada para a atividade do Recurso de Atualização do AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa79d-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="fa79d-183">Serviço vinculado para o ponto de extremidade de treinamento do AM do Azure ML</span><span class="sxs-lookup"><span data-stu-id="fa79d-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="fa79d-184">O trecho JSON a seguir define um serviço vinculado de Azure Machine Learning que aponta para o ponto de extremidade padrão do serviço Web de treinamento.</span><span class="sxs-lookup"><span data-stu-id="fa79d-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="fa79d-185">No **Azure ML Studio**, faça o seguinte para obter os valores de **mlEndpoint** e **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="fa79d-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="fa79d-186">Clique em **SERVIÇOS WEB** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="fa79d-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="fa79d-187">Clique no **serviço Web de treinamento** na lista de serviços Web.</span><span class="sxs-lookup"><span data-stu-id="fa79d-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="fa79d-188">Clique em Copiar ao lado da caixa de texto **Chave de API** .</span><span class="sxs-lookup"><span data-stu-id="fa79d-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="fa79d-189">Cole a chave na área de transferência e no editor JSON do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fa79d-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="fa79d-190">No **Azure ML Studio**, clique no link **EXECUÇÃO EM LOTE**.</span><span class="sxs-lookup"><span data-stu-id="fa79d-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="fa79d-191">Copie o **URI da Solicitação** da seção **Solicitação** e cole-o no editor de JSON do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fa79d-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="fa79d-192">Serviço Vinculado para o ponto de extremidade de pontuação atualizável do AM do Azure:</span><span class="sxs-lookup"><span data-stu-id="fa79d-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="fa79d-193">O trecho de código do JSON a seguir define um serviço vinculado do Azure Machine Learning que aponta para o ponto de extremidade não padrão atualizável do serviço Web de pontuação.</span><span class="sxs-lookup"><span data-stu-id="fa79d-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="fa79d-194">Conjunto de dados de saída de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="fa79d-194">Placeholder output dataset:</span></span>
<span data-ttu-id="fa79d-195">A atividade de Atualização do recurso do AM do Azure não gera qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="fa79d-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="fa79d-196">No entanto, o Azure Data Factory exige um conjunto de dados de saída para gerar a agenda de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="fa79d-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="fa79d-197">Portanto, usamos um conjunto de dados fictício/espaço reservado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="fa79d-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="fa79d-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="fa79d-198">Pipeline</span></span>
<span data-ttu-id="fa79d-199">O pipeline tem duas atividades: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="fa79d-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="fa79d-200">A atividade de Execução em lote do AM do Azure usa os dados de treinamento como entrada e produz um arquivo iLearner como saída.</span><span class="sxs-lookup"><span data-stu-id="fa79d-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="fa79d-201">A atividade invoca o serviço Web de treinamento (experimento de treinamento exposto como um serviço Web) com os dados de treinamento de entrada e recebe o arquivo ilearner do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="fa79d-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="fa79d-202">O placeholderBlob é apenas um conjunto de dados de saída fictício necessário ao serviço Azure Data Factory para executar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="fa79d-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![diagrama de pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
