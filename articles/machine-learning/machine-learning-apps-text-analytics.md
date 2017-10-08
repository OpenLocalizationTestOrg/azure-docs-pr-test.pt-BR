---
title: "APIs de Machine Learning: análise de texto| Microsoft Docs"
description: "APIs de análise da Microsoft máquina aprendizado texto pode ser usado tooanalyze texto não estruturado para análise de sentimento, extração de frase-chave, a detecção de idioma e detecção de tópico."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>APIs de Machine Learning: análise de texto para sentimento, extração de frases-chave, detecção de idioma e detecção de tópico
> [!NOTE]
> Este guia destina-se a versão 1 do hello API. Versão 2, [ **consulte o documento toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Versão 2 agora é a versão preferencial Olá desta API.
> 
> 

## <a name="overview"></a>Visão geral
Olá API de análise de texto é um conjunto de análises de texto [serviços web](https://datamarket.azure.com/dataset/amla/text-analytics) criados com o aprendizado de máquina do Azure. Olá API pode ser usado tooanalyze texto não estruturado para tarefas, como análise de sentimento, extração de frase-chave, a detecção de idioma e detecção de tópico. Não são de dados de treinamento necessário toouse essa API: basta colocar seus dados de texto. Essa API usa processamento técnicas toodeliver melhor em previsões de classe avançadas do idioma natural.

Você pode ver análises de texto em ação no nosso [site de demonstração](https://text-analytics-demo.azurewebsites.net/), você também encontrará [exemplos](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sobre como análises de texto tooimplement em c# e Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Análise de sentimento
Olá API retorna uma pontuação numérica entre 0 e 1. Too1 fechar pontuações indicar sentimento positivo, enquanto too0 fechar pontuações indicar sentimento negativo. A pontuação de sentimento é gerada usando técnicas de classificação. classificação de toohello de recursos de entrada Hello incluem n-grams, gerados a partir de marcas de parte de fala e word incorporações de recursos. Atualmente, o inglês é Olá só tem suporte a idioma.

## <a name="key-phrase-extraction"></a>Extração de frases-chave
Olá API retorna uma lista de cadeias de caracteres indicando Olá chave estratégias no texto de entrada hello. Empregamos técnicas do kit de ferramentas de Processamento de Linguagem Natural sofisticado do Microsoft Office. Atualmente, o inglês é Olá só tem suporte a idioma.

## <a name="language-detection"></a>Detecção de idioma
Olá API retorna Olá detectou o idioma e uma pontuação numérica entre 0 e 1. Too1 fechar pontuações indicar 100% certeza que idioma Olá identificado é true. Há 120 idiomas com suporte no total.

## <a name="topic-detection"></a>Detecção de tópico
Esta é uma API recém-lançado que retorna Olá principais detectado tópicos para obter uma lista de registros de texto enviada. Um tópico é identificado com uma senha, que pode ser uma ou mais palavras relacionadas. Esta API exige um mínimo de 100 texto registra toobe enviada, mas é projetado toodetect tópicos centenas toothousands de registros. Observe que essa API cobra uma transação por registro de texto enviado. Olá API é projetado toowork bem para humanos curto, gravado texto como revisões e comentários do usuário.

- - -
## <a name="api-definition"></a>Definição da API
### <a name="headers"></a>Cabeçalhos
Certifique-se de incluir cabeçalhos de saudação correto na solicitação, que deve ser da seguinte maneira:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Você pode encontrar sua chave de conta da sua conta no hello [Azure Data Market](https://datamarket.azure.com/account/keys). Observe que, atualmente, apenas JSON é aceita para formatos de entrada e saída. Não há suporte para XML.

- - -
## <a name="single-response-apis"></a>APIs de resposta única
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Solicitação de exemplo**

Na chamada de saudação abaixo, solicitamos análise de sentimento frase hello "Hello World":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Isso retornará uma resposta da seguinte maneira:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Solicitação de exemplo**

Na chamada de saudação abaixo, solicitamos frases-chave Olá encontrado no texto de saudação "Era um toostay hotel significativos em, casa exclusiva e equipe amigável":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Isso retornará uma resposta da seguinte maneira:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Solicitação de exemplo**

Na chamada GET de saudação abaixo, solicitamos para sentimento Olá frases-chave Olá no texto de saudação *Hello World*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Isso retornará uma resposta da seguinte maneira:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Parâmetros opcionais**

`NumberOfLanguagesToDetect` é um parâmetro opcional. saudação padrão é 1.

- - -
## <a name="batch-apis"></a>APIs de lote
saudação de serviço de análise de texto permite extrações de frase-chave e você sentimento toodo em modo de lote. Observe que cada um dos registros de saudação totalizados contagens como uma transação. Por exemplo, se você solicitar o sentimento de 1000 registros em uma única chamada, ocorrerá a dedução de 1000 transações.

Observe que as IDs de saudação inseridos no sistema de saudação são Olá IDs retornados pelo sistema hello. serviço web de saudação não verifica se essas IDs são exclusivas. É responsabilidade de saudação de exclusividade de tooverify chamador hello. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Solicitação de exemplo**

Em Olá POST chame abaixo, solicitamos para opiniões de saudação de frases hello "Hello World", "Olá, mundo Foo" e "Hello meu World" no corpo de saudação de solicitação de saudação:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Corpo da solicitação:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Em resposta Olá abaixo, você obter lista de saudação de pontuações associado com o texto de Ids:

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Solicitação de exemplo**

Neste exemplo, podemos está solicitando a lista de saudação de opiniões de frases-chave Olá em Olá textos a seguir: 

* "Era um toostay hotel significativos em, casa exclusiva e amigável equipe"
* "Foi uma conferência incrível, com palestras muito interessantes"
* "tráfego Olá foi terrível, como também três horas vai aeroporto toohello"

Essa solicitação é feita como um ponto de extremidade do POST chamada toohello:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Corpo da solicitação:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

Em resposta Olá abaixo, você obter lista de saudação de frases-chave associadas com o texto de Ids:

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

Em chamada POST de saudação abaixo, solicitamos a detecção de idioma para duas entradas de texto:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Corpo da solicitação:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Isso retorna Olá resposta, a seguir onde inglês for detectado em hello primeiro de entrada e francês na segunda entrada de saudação:

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>APIs de detecção de tópico
Esta é uma API recém-lançado que retorna Olá principais detectado tópicos para obter uma lista de registros de texto enviada. Um tópico é identificado com uma senha, que pode ser uma ou mais palavras relacionadas. Observe que essa API cobra uma transação por registro de texto enviado.

Esta API exige um mínimo de 100 texto registra toobe enviada, mas é projetado toodetect tópicos centenas toothousands de registros.

### <a name="topics--submit-job"></a>Tópicos – enviar trabalho
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Solicitação de exemplo**

Em chamada POST de saudação abaixo, solicitamos tópicos para um conjunto de 100 artigos, onde Olá primeiro e último entrada artigos são mostrados, e dois StopPhrases são incluídos.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Corpo da solicitação:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Resposta de saudação abaixo, você receberá Olá JobId para trabalho enviado hello:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Uma lista de frases com uma ou mais palavras que não devem ser retornadas como tópicos. Pode ser usado toofilter out tópicos muito genéricos. Por exemplo, em um conjunto de dados sobre análises de hotéis, "hotel" e "hostel" podem ser frases de interrupção adequadas.  

### <a name="topics--poll-for-job-results"></a>Tópicos – pesquisa de resultados do trabalho
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Solicitação de exemplo**

Passe Olá que jobId retornado nos resultados de Olá Olá 'Enviar trabalho' etapa toofetch. É recomendável que você chamar esse ponto de extremidade a cada minuto até que o Status = 'Concluído' na resposta de saudação. Levará cerca de 10 minutos por toocomplete um trabalho, ou mais para trabalhos com milhares de registros.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Durante o processamento, resposta Olá será da seguinte maneira:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Olá API retorna a saída no formato JSON em Olá formato a seguir:

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


Propriedades de saudação para cada parte da resposta de saudação são da seguinte maneira:

**Propriedades de TopicInfo**

| Chave | Descrição |
|:--- |:--- |
| TopicId |Um identificador exclusivo para cada tópico. |
| Pontuação |Contagem de registros atribuído tootopic. |
| KeyPhrase |Uma palavra ou frase para tópico Olá resumindo. Pode ser uma ou várias palavras. |

**Propriedades de TopicAssignment**

| Chave | Descrição |
|:--- |:--- |
| ID |Identificador de registro de saudação. É igual a ID toohello incluída na entrada hello. |
| TopicId |Olá qual registro Olá foi atribuído a ID do tópico. |
| Distância |Confiança registro Olá pertence toohello tópico. Toozero mais próximo de distância indica maior confiança. |

