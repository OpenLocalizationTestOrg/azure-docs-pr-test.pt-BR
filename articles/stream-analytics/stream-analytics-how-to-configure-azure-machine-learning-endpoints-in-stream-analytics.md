---
title: Use pontos de extremidade do Azure Machine Learning no Stream Analytics | Microsoft Docs
description: "Funções definidas pelo usuário da Linguagem de Máquina no Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="24012-103">Integração do Machine Learning ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24012-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="24012-104">O Stream Analytics dá suporte a funções definidas pelo usuário que chamam pontos de extremidade do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24012-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="24012-105">O suporte da API REST para esse recurso é detalhado na [biblioteca de API REST do Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="24012-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="24012-106">Este artigo fornece informações complementares necessárias para a implementação bem-sucedida desse recurso no Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="24012-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="24012-107">Um tutorial também foi publicado e está disponível [aqui](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="24012-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="24012-108">Visão geral: terminologia do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="24012-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="24012-109">O Microsoft Azure Machine Learning fornece uma ferramenta colaborativa do tipo "arrastar e soltar", que você pode usar para criar, testar e implantar soluções de análise preditiva em seus dados.</span><span class="sxs-lookup"><span data-stu-id="24012-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="24012-110">Essa ferramenta é chamada de *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="24012-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="24012-111">O estúdio é usado para interagir com os recursos do Machine Learning e para compilar, testar e iterar facilmente em seu design.</span><span class="sxs-lookup"><span data-stu-id="24012-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="24012-112">Veja abaixo esses recursos e suas definições.</span><span class="sxs-lookup"><span data-stu-id="24012-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="24012-113">
            **Espaço de trabalho**: o *espaço de trabalho* é um contêiner que mantém todos os outros recursos de Machine Learning em um contêiner para gerenciamento e controle.</span><span class="sxs-lookup"><span data-stu-id="24012-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="24012-114">**Experimento**: os *Experimentos* são criados por cientistas de dados a fim de usar conjuntos de dados e treinar um modelo de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="24012-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="24012-115">
            **Ponto de extremidade**: os *Pontos de extremidade* são objetos de Azure Machine Learning usados para aproveitar recursos como entrada, aplicar um modelo de aprendizado de máquina especificado e retornar a saída pontuada.</span><span class="sxs-lookup"><span data-stu-id="24012-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="24012-116">**Serviço da Web de Pontuação**: um *serviço da Web de pontuação* é uma coleção de pontos de extremidade, conforme mencionado acima.</span><span class="sxs-lookup"><span data-stu-id="24012-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="24012-117">Cada ponto de extremidade tem APIs para execução em lote e execução síncrona.</span><span class="sxs-lookup"><span data-stu-id="24012-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="24012-118">O Stream Analytics usa a execução síncrona.</span><span class="sxs-lookup"><span data-stu-id="24012-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="24012-119">O serviço específico é chamado de [Serviço de Solicitação/Resposta](../machine-learning/machine-learning-consume-web-services.md) no Estúdio AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="24012-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="24012-120">Recursos de Machine Learning necessários para trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24012-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="24012-121">Para que o processamento de trabalhos do Stream Analytics seja bem-sucedido, é necessário ter um ponto de extremidade de Solicitação/Resposta, uma [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md)e uma definição do Swagger.</span><span class="sxs-lookup"><span data-stu-id="24012-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="24012-122">O Stream Analytics tem um ponto de extremidade adicional que constrói a URL do ponto de extremidade de swagger, procura a interface e retorna uma definição de UDF padrão para o usuário.</span><span class="sxs-lookup"><span data-stu-id="24012-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="24012-123">Configurar uma UDF de Stream Analytics e Machine Learning por meio da API REST</span><span class="sxs-lookup"><span data-stu-id="24012-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="24012-124">Com as APIs REST, você pode configurar seu trabalho para chamar funções de Linguagem de Máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="24012-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="24012-125">As etapas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="24012-125">The steps are as follows:</span></span>

1. <span data-ttu-id="24012-126">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24012-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="24012-127">Definir uma entrada</span><span class="sxs-lookup"><span data-stu-id="24012-127">Define an input</span></span>
3. <span data-ttu-id="24012-128">Definir uma saída</span><span class="sxs-lookup"><span data-stu-id="24012-128">Define an output</span></span>
4. <span data-ttu-id="24012-129">Criar uma UDF (função definida pelo usuário)</span><span class="sxs-lookup"><span data-stu-id="24012-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="24012-130">Criar uma transformação do Stream Analytics que chama a UDF</span><span class="sxs-lookup"><span data-stu-id="24012-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="24012-131">Iniciar o trabalho</span><span class="sxs-lookup"><span data-stu-id="24012-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="24012-132">Criação de uma UDF com propriedades básicas</span><span class="sxs-lookup"><span data-stu-id="24012-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="24012-133">Por exemplo, o exemplo de código a seguir cria uma UDF escalar chamada *newudf* que realiza um vínculo a um ponto de extremidade de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24012-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="24012-134">Observe que o *ponto de extremidade* (URI de serviço) pode ser encontrado na página de ajuda da API do serviço escolhido e a *apiKey* pode ser encontrada na página principal de Serviços.</span><span class="sxs-lookup"><span data-stu-id="24012-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="24012-135">Exemplo de corpo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="24012-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="24012-136">Chamar o ponto de extremidade RetrieveDefaultDefinition para UDF padrão</span><span class="sxs-lookup"><span data-stu-id="24012-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="24012-137">Após a criação do esqueleto da UDF, é necessário obter a definição completa da UDF.</span><span class="sxs-lookup"><span data-stu-id="24012-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="24012-138">O ponto de extremidade RetreiveDefaultDefinition ajuda a obter a definição padrão para uma função escalar associada a um ponto de extremidade de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24012-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="24012-139">A carga abaixo exige que você obtenha definição padrão da UDF para uma função escalar associada a um ponto de extremidade de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24012-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="24012-140">Ela não especifica o ponto de extremidade real, pois ele já foi fornecido durante a solicitação PUT.</span><span class="sxs-lookup"><span data-stu-id="24012-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="24012-141">O Stream Analytics chamará o ponto de extremidade fornecido na solicitação se ele for fornecido explicitamente.</span><span class="sxs-lookup"><span data-stu-id="24012-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="24012-142">Caso contrário, ele usa o ponto referenciado originalmente.</span><span class="sxs-lookup"><span data-stu-id="24012-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="24012-143">Neste exemplo, a UDF usa um parâmetro de cadeia única (uma sentença) e retorna uma única saída do tipo de cadeia de caracteres que indica o rótulo "sentimento" daquela sentença.</span><span class="sxs-lookup"><span data-stu-id="24012-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="24012-144">Exemplo de corpo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="24012-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="24012-145">Um exemplo disso teria uma aparência como esta.</span><span class="sxs-lookup"><span data-stu-id="24012-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="24012-146">Aplicar patch à UDF com a resposta</span><span class="sxs-lookup"><span data-stu-id="24012-146">Patch UDF with the response</span></span>
<span data-ttu-id="24012-147">Agora a UDF deve ser corrigida com a resposta anterior, conforme exibido abaixo.</span><span class="sxs-lookup"><span data-stu-id="24012-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="24012-148">Corpo da solicitação (saída de RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="24012-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="24012-149">Implementar uma transformação do Stream Analytics que chama a UDF</span><span class="sxs-lookup"><span data-stu-id="24012-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="24012-150">Agora, consulte a UDF (chamada aqui de scoreTweet) para cada evento de entrada e grave uma resposta para esse evento em uma saída.</span><span class="sxs-lookup"><span data-stu-id="24012-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="24012-151">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="24012-151">Get help</span></span>
<span data-ttu-id="24012-152">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="24012-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="24012-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24012-153">Next steps</span></span>
* [<span data-ttu-id="24012-154">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="24012-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="24012-155">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="24012-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="24012-156">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="24012-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="24012-157">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="24012-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="24012-158">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24012-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
