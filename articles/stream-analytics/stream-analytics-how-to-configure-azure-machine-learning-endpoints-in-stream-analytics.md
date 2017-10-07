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
# <a name="machine-learning-integration-in-stream-analytics"></a>Integração do Machine Learning ao Stream Analytics
Análise de fluxo dá suporte a funções definidas pelo usuário que chamar tooAzure pontos de extremidade do aprendizado de máquina. Suporte de API REST para esse recurso é detalhado no hello [biblioteca de API de REST de análise de fluxo](https://msdn.microsoft.com/library/azure/dn835031.aspx). Este artigo fornece informações complementares necessárias para a implementação bem-sucedida desse recurso no Stream Analytics. Um tutorial também foi publicado e está disponível [aqui](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Visão geral: terminologia do Azure Machine Learning
Aprendizado de máquina do Microsoft Azure fornece uma ferramenta de colaboração, arrastar e soltar, você pode usar toobuild, testar e implantar soluções de análise preditiva em seus dados. Essa ferramenta é chamada hello *estúdio de aprendizado de máquina do Azure*. studio Olá é toointeract usado com hello recursos de aprendizagem de máquina e facilmente criar, testar e itere o design. Veja abaixo esses recursos e suas definições.

* **Espaço de trabalho**: Olá *espaço de trabalho* é um contêiner que contém todos os outros recursos de aprendizado de máquina em um contêiner para gerenciamento e controle.
* **Experiência**: *experiências* são criados por dados cientistas tooutilize conjuntos de dados e treinar um modelo de aprendizado de máquina.
* **Ponto de extremidade**: *pontos de extremidade* são Olá aprendizado de máquina do Azure recursos de tootake de objeto usado como entrada, aplicar um modelo de aprendizado de máquina especificado e retorna a saída classificada.
* **Serviço da Web de Pontuação**: um *serviço da Web de pontuação* é uma coleção de pontos de extremidade, conforme mencionado acima.

Cada ponto de extremidade tem APIs para execução em lote e execução síncrona. O Stream Analytics usa a execução síncrona. serviço específico de saudação é chamado um [serviço de solicitação/resposta](../machine-learning/machine-learning-consume-web-services.md) no studio AzureML.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Recursos de Machine Learning necessários para trabalhos do Stream Analytics
Para fins de saudação da análise de fluxo de trabalho de processamento, um ponto de extremidade de solicitação/resposta, uma [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), e uma definição de swagger são todos necessários para a execução bem-sucedida. Análise de fluxo tem um ponto de extremidade adicional que constrói Olá url de ponto de extremidade de swagger, procura interface hello e retorna um usuário de toohello definição padrão UDF.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Configurar uma UDF de Stream Analytics e Machine Learning por meio da API REST
Usando APIs REST, você pode configurar funções trabalho toocall linguagem de máquina do Azure. etapas de saudação são da seguinte maneira:

1. Criar um trabalho de Stream Analytics
2. Definir uma entrada
3. Definir uma saída
4. Criar uma UDF (função definida pelo usuário)
5. Gravar uma transformação de análise de fluxo chamadas Olá UDF
6. Iniciar trabalho Olá

## <a name="creating-a-udf-with-basic-properties"></a>Criação de uma UDF com propriedades básicas
Por exemplo, Olá código de exemplo a seguir cria uma UDF escalar denominada *newudf* que associa o ponto de extremidade de aprendizado de máquina do Azure tooan. Observe que Olá *ponto de extremidade* (URI do serviço) pode ser encontrado na página de ajuda de saudação API para Olá escolhido serviço e hello *apiKey* podem ser encontradas na página principal de serviços de saudação.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Exemplo de corpo de solicitação:  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Chamar o ponto de extremidade RetrieveDefaultDefinition para UDF padrão
Uma vez Olá esqueleto que UDF é criado a definição completa de saudação do hello que UDF é necessária. o ponto de extremidade do Hello RetreiveDefaultDefinition ajuda a obter saudação padrão definição para uma função escalar que é o ponto de extremidade de aprendizado de máquina do Azure tooan associado. carga de saudação abaixo requer tooget Olá UDF definição para uma função escalar que é o ponto de extremidade de aprendizado de máquina do Azure tooan associado. Ela não especifica o ponto de extremidade real Olá pois ele já foi fornecido durante a solicitação PUT. Análise de fluxo chama o ponto de extremidade de saudação fornecido na solicitação de saudação se ele é fornecido explicitamente. Caso contrário, ele usa Olá um originalmente referenciada. Olá aqui usa UDF uma única cadeia de caracteres (uma frase) de parâmetro e retorna uma única saída de tipo de cadeia de caracteres que indica o rótulo "sentimento" hello essa frase.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Exemplo de corpo de solicitação:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Um exemplo disso teria uma aparência como esta.  

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

## <a name="patch-udf-with-hello-response"></a>Patch do UDF com resposta Olá
Agora hello UDF deve ser corrigido com resposta anterior de saudação, conforme mostrado abaixo.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Corpo da solicitação (saída de RetrieveDefaultDefinition):

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Implementar o Stream Analytics transformação toocall Olá UDF
Agora consultar Olá UDF (aqui chamado scoreTweet) para cada evento de entrada e gravar uma resposta para a saída de tooan esse evento.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
