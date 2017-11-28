---
title: "modelos de aprendizado de máquina aaaUpdate usando o Azure Data Factory | Microsoft Docs"
description: "Descreve como toocreate criar pipelines de previsão usando o Azure Data Factory e aprendizado de máquina do Azure"
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
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="ce1ed-103">Atualizando os modelos do Machine Learning do Azure usando a Atividade de Recurso de Atualização</span><span class="sxs-lookup"><span data-stu-id="ce1ed-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ce1ed-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="ce1ed-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ce1ed-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="ce1ed-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ce1ed-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="ce1ed-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ce1ed-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="ce1ed-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ce1ed-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="ce1ed-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ce1ed-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ce1ed-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ce1ed-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ce1ed-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ce1ed-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="ce1ed-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ce1ed-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ce1ed-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ce1ed-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="ce1ed-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="ce1ed-114">Este artigo complementa Olá principal do Azure Data Factory - artigo de integração de aprendizado de máquina do Azure: [criar pipelines de previsão usando o aprendizado de máquina do Azure e o Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="ce1ed-115">Se você ainda não fez isso, consulte o artigo principal de saudação antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="ce1ed-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ce1ed-116">Overview</span></span>
<span data-ttu-id="ce1ed-117">Ao longo do tempo, os modelos de previsão de saudação em experiências de pontuação do hello Azure ML necessário toobe treinados novamente usando novos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="ce1ed-118">Depois que você treinamento, você deseja tooupdate Olá pontuação serviço web com hello retreinados modelo ML.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="ce1ed-119">Olá etapas típicas tooenable treinar novamente e atualizações modelos de ML do Azure por meio de serviços web são:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="ce1ed-120">Crie um teste no [Estúdio AM do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="ce1ed-121">Quando estiver satisfeito com o modelo de hello, usar o Azure ML Studio toopublish web services para ambos os Olá **experiência de treinamento** e pontuação /**experimento previsão**.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="ce1ed-122">Olá tabela a seguir descreve Olá web services usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="ce1ed-123">Confira [Readaptar os modelos do Machine Learning de forma programática](../machine-learning/machine-learning-retrain-models-programmatically.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="ce1ed-124">**Treinamento do serviço Web** - recebe dados de treinamento e produz modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="ce1ed-125">saída Olá Olá treinamento é um arquivo .ilearner em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="ce1ed-126">Olá **padrão de ponto de extremidade** é criado automaticamente para você quando você publica o treinamento Olá testar como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="ce1ed-127">Você pode criar mais pontos de extremidade, mas exemplo hello usa apenas Olá ponto de extremidade padrão.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="ce1ed-128">**Pontuação do serviço Web** - recebe exemplos de dados sem rótulo de e faz previsões.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="ce1ed-129">saída de Hello de previsão pode ter várias formas, como um arquivo. csv ou linhas em um banco de dados SQL do Azure, dependendo da configuração de saudação do experimento hello.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="ce1ed-130">ponto de extremidade saudação padrão é criado automaticamente para você quando você publica a experiência de previsão de saudação como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="ce1ed-131">Olá, imagem a seguir descreve Olá relação entre o treinamento e pontuação de pontos de extremidade no Azure ML.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVIÇOS WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="ce1ed-133">Você pode chamar hello **treinamento de serviço web** usando Olá **atividades de execução em lote do Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="ce1ed-134">A invocação de um serviço Web de treinamento é igual à invocação de um serviço Web do AM do Azure ML (serviço Web de pontuação) para pontuação de dados.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="ce1ed-135">Olá cobertura de seções anteriores como tooinvoke um serviço de web do ML do Azure de uma fábrica de dados do Azure pipeline em detalhes.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="ce1ed-136">Você pode chamar hello **serviço web de pontuação** usando Olá **atividades de recurso de atualização do Azure ML** tooupdate Olá web service com hello recentemente treinado.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="ce1ed-137">Olá exemplos a seguir fornece as definições de serviço vinculado:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="ce1ed-138">Serviço web de pontuação é um serviço web clássico</span><span class="sxs-lookup"><span data-stu-id="ce1ed-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="ce1ed-139">Se Olá pontuação serviço web é um **serviço web clássico**, criar hello segundo **ponto de extremidade não padrão e atualizável** usando Olá [portal do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ce1ed-140">Confira o artigo [Criar pontos de extremidade](../machine-learning/machine-learning-create-endpoint.md) para conhecer as etapas.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="ce1ed-141">Depois de criar o ponto de extremidade atualizável Olá não padrão, Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="ce1ed-142">Clique em **BATCH EXECUTION** tooget Olá URI valor para Olá **mlEndpoint** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="ce1ed-143">Clique em **recurso de atualização** vincular o valor de URI de saudação tooget para Olá **updateResourceEndpoint** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="ce1ed-144">chave de API de saudação é na própria página de ponto de extremidade hello (no canto do hello inferior direito).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![ponto de extremidade atualizável](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="ce1ed-146">saudação de exemplo a seguir fornece um exemplo de definição de JSON para Olá serviço vinculado do AzureML.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="ce1ed-147">Olá apiKey de saudação do serviço vinculado usa para autenticação.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-147">hello linked service uses hello apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="ce1ed-148">Serviço Web de pontuação é um serviço Web do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce1ed-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="ce1ed-149">Se o serviço web de saudação é Olá novo tipo de serviço da web que expõe um ponto de extremidade do Gerenciador de recursos do Azure, não é necessário tooadd Olá segundo **não-padrão** ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="ce1ed-150">Olá **updateResourceEndpoint** em Olá serviço vinculado é do formato de saudação:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="ce1ed-151">Você pode obter valores de espaços reservados na URL de saudação ao consultar o serviço web Olá Olá [o Portal de serviços do Azure Machine Learning Web](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="ce1ed-152">novo tipo de saudação do ponto de extremidade do recurso de atualização requer um token do AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="ce1ed-153">Especifique **servicePrincipalId** e **servicePrincipalKey**no serviço vinculado do AzureML.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="ce1ed-154">Consulte [como toocreate principal de serviço e atribuir permissões toomanage recursos do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ce1ed-155">Aqui está um exemplo de definição de serviço AzureML vinculado:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
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

<span data-ttu-id="ce1ed-156">Olá cenário a seguir fornece mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-156">hello following scenario provides more details.</span></span> <span data-ttu-id="ce1ed-157">Ele tem um exemplo de readaptação e atualização de modelos de AM do Azure de um pipeline do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="ce1ed-158">Cenário: novo treinamento e atualização de um modelo do AM do Azure</span><span class="sxs-lookup"><span data-stu-id="ce1ed-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="ce1ed-159">Esta seção fornece um pipeline de exemplo que usa Olá **atividade de execução de lote do Azure ML** tooretrain um modelo.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="ce1ed-160">pipeline de saudação também usa Olá **atividade de atualização do recurso do Azure ML** tooupdate modelo Olá Olá pontuação serviço da web.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="ce1ed-161">Olá fornece também Olá de trechos de código JSON para todos os serviços vinculados, conjuntos de dados e pipeline no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="ce1ed-162">Aqui está o modo de exibição de diagrama de saudação do pipeline de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="ce1ed-163">Como você pode ver, hello atividade de execução de lote do Azure ML aceita entrada de treinamento hello e produz uma saída de treinamento (arquivo iLearner).</span><span class="sxs-lookup"><span data-stu-id="ce1ed-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="ce1ed-164">Hello atividade de recursos do Azure ML atualização usa esta saída de treinamento e atualizações Olá modelo no hello pontuação de ponto de extremidade de serviço web.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="ce1ed-165">Hello atividade de atualização de recurso não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="ce1ed-166">Olá placeholderBlob é apenas um saída fictício conjunto de dados que é exigido pelo pipeline de saudação do hello Azure Data Factory serviço toorun.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![diagrama de pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="ce1ed-168">Serviço vinculado do armazenamento de Blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="ce1ed-169">saudação de armazenamento do Azure mantém Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="ce1ed-170">dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-170">training data.</span></span> <span data-ttu-id="ce1ed-171">dados de entrada Hello para serviço de web de treinamento Olá ML do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="ce1ed-172">Arquivo iLearner.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-172">iLearner file.</span></span> <span data-ttu-id="ce1ed-173">saudação de saída do serviço web do hello Azure ML treinamento.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="ce1ed-174">Esse arquivo também é toohello de entrada hello atividade do recurso de atualização.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="ce1ed-175">Aqui está a definição de JSON de exemplo hello do serviço vinculado de saudação:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-175">Here is hello sample JSON definition of hello linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="ce1ed-176">Conjunto de dados de entrada do treinamento:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-176">Training input dataset:</span></span>
<span data-ttu-id="ce1ed-177">Olá seguinte conjunto de dados representa dados de treinamento de entrada hello para serviço de web de treinamento Olá ML do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="ce1ed-178">Hello atividade de execução de lote do ML do Azure usa esse conjunto de dados como entrada.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="ce1ed-179">Conjunto de dados de saída de treinamento:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-179">Training output dataset:</span></span>
<span data-ttu-id="ce1ed-180">Olá seguinte conjunto de dados representa Olá saída iLearner arquivo do serviço web do hello Azure ML treinamento.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="ce1ed-181">Hello atividade de execução de lote do Azure ML produz este conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="ce1ed-182">Este conjunto de dados também é toohello de entrada hello atividade de atualização do recurso do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="ce1ed-183">Serviço vinculado para o ponto de extremidade de treinamento do AM do Azure ML</span><span class="sxs-lookup"><span data-stu-id="ce1ed-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="ce1ed-184">Olá trecho JSON a seguir define um serviço vinculado do aprendizado de máquina do Azure que aponta toohello o ponto de extremidade padrão do serviço de web hello treinamento.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

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

<span data-ttu-id="ce1ed-185">Em **Azure ML Studio**, Olá seguintes valores de tooget para **mlEndpoint** e **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="ce1ed-186">Clique em **serviços WEB** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="ce1ed-187">Clique em Olá **treinamento de serviço web** na lista de saudação de serviços web.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="ce1ed-188">Em Copiar Avançar muito**chave API** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="ce1ed-189">Cole editor de JSON da fábrica de dados Olá chave Olá na área de transferência hello.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="ce1ed-190">Em Olá **studio ML do Azure**, clique em **BATCH EXECUTION** link.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="ce1ed-191">Saudação de cópia **URI da solicitação** de saudação **solicitação** seção e colá-lo no editor de JSON da fábrica de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="ce1ed-192">Serviço Vinculado para o ponto de extremidade de pontuação atualizável do AM do Azure:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="ce1ed-193">Olá trecho JSON a seguir define um serviço vinculado do aprendizado de máquina do Azure que aponta toohello padrão não atualizável ponto de extremidade de Olá pontuação serviço da web.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="ce1ed-194">Conjunto de dados de saída de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="ce1ed-194">Placeholder output dataset:</span></span>
<span data-ttu-id="ce1ed-195">Hello atividade de atualização do recurso do Azure ML não gera nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="ce1ed-196">No entanto, o Azure Data Factory requer uma conjunto de dados toodrive Olá agenda de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="ce1ed-197">Portanto, usamos um conjunto de dados fictício/espaço reservado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="ce1ed-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="ce1ed-198">Pipeline</span></span>
<span data-ttu-id="ce1ed-199">pipeline de saudação tem duas atividades: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="ce1ed-200">Hello atividade de execução de lote do ML do Azure usa dados de treinamento hello como entrada e produz um arquivo iLearner como saída.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="ce1ed-201">atividade de Olá chama o serviço web de treinamento hello (experiência de treinamento exposto como um serviço da web) com dados de treinamento de entrada hello e recebe o arquivo ilearner de saudação do hello webservice.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="ce1ed-202">Olá placeholderBlob é apenas um saída fictício conjunto de dados que é exigido pelo pipeline de saudação do hello Azure Data Factory serviço toorun.</span><span class="sxs-lookup"><span data-stu-id="ce1ed-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

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
