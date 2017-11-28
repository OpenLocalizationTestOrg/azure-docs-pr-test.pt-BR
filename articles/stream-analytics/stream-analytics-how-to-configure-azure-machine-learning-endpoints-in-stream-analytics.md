---
title: "aaaUse pontos de extremidade de aprendizado de máquina do Azure no Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="a2413-103">Integração do Machine Learning ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2413-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="a2413-104">Análise de fluxo dá suporte a funções definidas pelo usuário que chamar tooAzure pontos de extremidade do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="a2413-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="a2413-105">Suporte de API REST para esse recurso é detalhado no hello [biblioteca de API de REST de análise de fluxo](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2413-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="a2413-106">Este artigo fornece informações complementares necessárias para a implementação bem-sucedida desse recurso no Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="a2413-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="a2413-107">Um tutorial também foi publicado e está disponível [aqui](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a2413-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="a2413-108">Visão geral: terminologia do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a2413-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="a2413-109">Aprendizado de máquina do Microsoft Azure fornece uma ferramenta de colaboração, arrastar e soltar, você pode usar toobuild, testar e implantar soluções de análise preditiva em seus dados.</span><span class="sxs-lookup"><span data-stu-id="a2413-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="a2413-110">Essa ferramenta é chamada hello *estúdio de aprendizado de máquina do Azure*.</span><span class="sxs-lookup"><span data-stu-id="a2413-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="a2413-111">studio Olá é toointeract usado com hello recursos de aprendizagem de máquina e facilmente criar, testar e itere o design.</span><span class="sxs-lookup"><span data-stu-id="a2413-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="a2413-112">Veja abaixo esses recursos e suas definições.</span><span class="sxs-lookup"><span data-stu-id="a2413-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="a2413-113">**Espaço de trabalho**: Olá *espaço de trabalho* é um contêiner que contém todos os outros recursos de aprendizado de máquina em um contêiner para gerenciamento e controle.</span><span class="sxs-lookup"><span data-stu-id="a2413-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="a2413-114">**Experiência**: *experiências* são criados por dados cientistas tooutilize conjuntos de dados e treinar um modelo de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="a2413-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="a2413-115">**Ponto de extremidade**: *pontos de extremidade* são Olá aprendizado de máquina do Azure recursos de tootake de objeto usado como entrada, aplicar um modelo de aprendizado de máquina especificado e retorna a saída classificada.</span><span class="sxs-lookup"><span data-stu-id="a2413-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="a2413-116">**Serviço da Web de Pontuação**: um *serviço da Web de pontuação* é uma coleção de pontos de extremidade, conforme mencionado acima.</span><span class="sxs-lookup"><span data-stu-id="a2413-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="a2413-117">Cada ponto de extremidade tem APIs para execução em lote e execução síncrona.</span><span class="sxs-lookup"><span data-stu-id="a2413-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="a2413-118">O Stream Analytics usa a execução síncrona.</span><span class="sxs-lookup"><span data-stu-id="a2413-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="a2413-119">serviço específico de saudação é chamado um [serviço de solicitação/resposta](../machine-learning/machine-learning-consume-web-services.md) no studio AzureML.</span><span class="sxs-lookup"><span data-stu-id="a2413-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="a2413-120">Recursos de Machine Learning necessários para trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2413-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="a2413-121">Para fins de saudação da análise de fluxo de trabalho de processamento, um ponto de extremidade de solicitação/resposta, uma [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), e uma definição de swagger são todos necessários para a execução bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="a2413-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="a2413-122">Análise de fluxo tem um ponto de extremidade adicional que constrói Olá url de ponto de extremidade de swagger, procura interface hello e retorna um usuário de toohello definição padrão UDF.</span><span class="sxs-lookup"><span data-stu-id="a2413-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="a2413-123">Configurar uma UDF de Stream Analytics e Machine Learning por meio da API REST</span><span class="sxs-lookup"><span data-stu-id="a2413-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="a2413-124">Usando APIs REST, você pode configurar funções trabalho toocall linguagem de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2413-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="a2413-125">etapas de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a2413-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="a2413-126">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2413-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="a2413-127">Definir uma entrada</span><span class="sxs-lookup"><span data-stu-id="a2413-127">Define an input</span></span>
3. <span data-ttu-id="a2413-128">Definir uma saída</span><span class="sxs-lookup"><span data-stu-id="a2413-128">Define an output</span></span>
4. <span data-ttu-id="a2413-129">Criar uma UDF (função definida pelo usuário)</span><span class="sxs-lookup"><span data-stu-id="a2413-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="a2413-130">Gravar uma transformação de análise de fluxo chamadas Olá UDF</span><span class="sxs-lookup"><span data-stu-id="a2413-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="a2413-131">Iniciar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="a2413-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="a2413-132">Criação de uma UDF com propriedades básicas</span><span class="sxs-lookup"><span data-stu-id="a2413-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="a2413-133">Por exemplo, Olá código de exemplo a seguir cria uma UDF escalar denominada *newudf* que associa o ponto de extremidade de aprendizado de máquina do Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="a2413-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="a2413-134">Observe que Olá *ponto de extremidade* (URI do serviço) pode ser encontrado na página de ajuda de saudação API para Olá escolhido serviço e hello *apiKey* podem ser encontradas na página principal de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2413-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="a2413-135">Exemplo de corpo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="a2413-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="a2413-136">Chamar o ponto de extremidade RetrieveDefaultDefinition para UDF padrão</span><span class="sxs-lookup"><span data-stu-id="a2413-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="a2413-137">Uma vez Olá esqueleto que UDF é criado a definição completa de saudação do hello que UDF é necessária.</span><span class="sxs-lookup"><span data-stu-id="a2413-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="a2413-138">o ponto de extremidade do Hello RetreiveDefaultDefinition ajuda a obter saudação padrão definição para uma função escalar que é o ponto de extremidade de aprendizado de máquina do Azure tooan associado.</span><span class="sxs-lookup"><span data-stu-id="a2413-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="a2413-139">carga de saudação abaixo requer tooget Olá UDF definição para uma função escalar que é o ponto de extremidade de aprendizado de máquina do Azure tooan associado.</span><span class="sxs-lookup"><span data-stu-id="a2413-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="a2413-140">Ela não especifica o ponto de extremidade real Olá pois ele já foi fornecido durante a solicitação PUT.</span><span class="sxs-lookup"><span data-stu-id="a2413-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="a2413-141">Análise de fluxo chama o ponto de extremidade de saudação fornecido na solicitação de saudação se ele é fornecido explicitamente.</span><span class="sxs-lookup"><span data-stu-id="a2413-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="a2413-142">Caso contrário, ele usa Olá um originalmente referenciada.</span><span class="sxs-lookup"><span data-stu-id="a2413-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="a2413-143">Olá aqui usa UDF uma única cadeia de caracteres (uma frase) de parâmetro e retorna uma única saída de tipo de cadeia de caracteres que indica o rótulo "sentimento" hello essa frase.</span><span class="sxs-lookup"><span data-stu-id="a2413-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="a2413-144">Exemplo de corpo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="a2413-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="a2413-145">Um exemplo disso teria uma aparência como esta.</span><span class="sxs-lookup"><span data-stu-id="a2413-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="a2413-146">Patch do UDF com resposta Olá</span><span class="sxs-lookup"><span data-stu-id="a2413-146">Patch UDF with hello response</span></span>
<span data-ttu-id="a2413-147">Agora hello UDF deve ser corrigido com resposta anterior de saudação, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a2413-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="a2413-148">Corpo da solicitação (saída de RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="a2413-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="a2413-149">Implementar o Stream Analytics transformação toocall Olá UDF</span><span class="sxs-lookup"><span data-stu-id="a2413-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="a2413-150">Agora consultar Olá UDF (aqui chamado scoreTweet) para cada evento de entrada e gravar uma resposta para a saída de tooan esse evento.</span><span class="sxs-lookup"><span data-stu-id="a2413-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="a2413-151">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="a2413-151">Get help</span></span>
<span data-ttu-id="a2413-152">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a2413-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2413-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2413-153">Next steps</span></span>
* [<span data-ttu-id="a2413-154">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2413-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a2413-155">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a2413-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a2413-156">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a2413-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a2413-157">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a2413-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a2413-158">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a2413-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
