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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="364be-103">APIs de Machine Learning: análise de texto para sentimento, extração de frases-chave, detecção de idioma e detecção de tópico</span><span class="sxs-lookup"><span data-stu-id="364be-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="364be-104">Este guia destina-se a versão 1 do hello API.</span><span class="sxs-lookup"><span data-stu-id="364be-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="364be-105">Versão 2, [ **consulte o documento toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="364be-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="364be-106">Versão 2 agora é a versão preferencial Olá desta API.</span><span class="sxs-lookup"><span data-stu-id="364be-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="364be-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="364be-107">Overview</span></span>
<span data-ttu-id="364be-108">Olá API de análise de texto é um conjunto de análises de texto [serviços web](https://datamarket.azure.com/dataset/amla/text-analytics) criados com o aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="364be-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="364be-109">Olá API pode ser usado tooanalyze texto não estruturado para tarefas, como análise de sentimento, extração de frase-chave, a detecção de idioma e detecção de tópico.</span><span class="sxs-lookup"><span data-stu-id="364be-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="364be-110">Não são de dados de treinamento necessário toouse essa API: basta colocar seus dados de texto.</span><span class="sxs-lookup"><span data-stu-id="364be-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="364be-111">Essa API usa processamento técnicas toodeliver melhor em previsões de classe avançadas do idioma natural.</span><span class="sxs-lookup"><span data-stu-id="364be-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="364be-112">Você pode ver análises de texto em ação no nosso [site de demonstração](https://text-analytics-demo.azurewebsites.net/), você também encontrará [exemplos](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sobre como análises de texto tooimplement em c# e Python.</span><span class="sxs-lookup"><span data-stu-id="364be-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="364be-113">Análise de sentimento</span><span class="sxs-lookup"><span data-stu-id="364be-113">Sentiment analysis</span></span>
<span data-ttu-id="364be-114">Olá API retorna uma pontuação numérica entre 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="364be-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="364be-115">Too1 fechar pontuações indicar sentimento positivo, enquanto too0 fechar pontuações indicar sentimento negativo.</span><span class="sxs-lookup"><span data-stu-id="364be-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="364be-116">A pontuação de sentimento é gerada usando técnicas de classificação.</span><span class="sxs-lookup"><span data-stu-id="364be-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="364be-117">classificação de toohello de recursos de entrada Hello incluem n-grams, gerados a partir de marcas de parte de fala e word incorporações de recursos.</span><span class="sxs-lookup"><span data-stu-id="364be-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="364be-118">Atualmente, o inglês é Olá só tem suporte a idioma.</span><span class="sxs-lookup"><span data-stu-id="364be-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="364be-119">Extração de frases-chave</span><span class="sxs-lookup"><span data-stu-id="364be-119">Key phrase extraction</span></span>
<span data-ttu-id="364be-120">Olá API retorna uma lista de cadeias de caracteres indicando Olá chave estratégias no texto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="364be-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="364be-121">Empregamos técnicas do kit de ferramentas de Processamento de Linguagem Natural sofisticado do Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="364be-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="364be-122">Atualmente, o inglês é Olá só tem suporte a idioma.</span><span class="sxs-lookup"><span data-stu-id="364be-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="364be-123">Detecção de idioma</span><span class="sxs-lookup"><span data-stu-id="364be-123">Language detection</span></span>
<span data-ttu-id="364be-124">Olá API retorna Olá detectou o idioma e uma pontuação numérica entre 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="364be-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="364be-125">Too1 fechar pontuações indicar 100% certeza que idioma Olá identificado é true.</span><span class="sxs-lookup"><span data-stu-id="364be-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="364be-126">Há 120 idiomas com suporte no total.</span><span class="sxs-lookup"><span data-stu-id="364be-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="364be-127">Detecção de tópico</span><span class="sxs-lookup"><span data-stu-id="364be-127">Topic detection</span></span>
<span data-ttu-id="364be-128">Esta é uma API recém-lançado que retorna Olá principais detectado tópicos para obter uma lista de registros de texto enviada.</span><span class="sxs-lookup"><span data-stu-id="364be-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="364be-129">Um tópico é identificado com uma senha, que pode ser uma ou mais palavras relacionadas.</span><span class="sxs-lookup"><span data-stu-id="364be-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="364be-130">Esta API exige um mínimo de 100 texto registra toobe enviada, mas é projetado toodetect tópicos centenas toothousands de registros.</span><span class="sxs-lookup"><span data-stu-id="364be-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="364be-131">Observe que essa API cobra uma transação por registro de texto enviado.</span><span class="sxs-lookup"><span data-stu-id="364be-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="364be-132">Olá API é projetado toowork bem para humanos curto, gravado texto como revisões e comentários do usuário.</span><span class="sxs-lookup"><span data-stu-id="364be-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="364be-133">Definição da API</span><span class="sxs-lookup"><span data-stu-id="364be-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="364be-134">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="364be-134">Headers</span></span>
<span data-ttu-id="364be-135">Certifique-se de incluir cabeçalhos de saudação correto na solicitação, que deve ser da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="364be-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="364be-136">Você pode encontrar sua chave de conta da sua conta no hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="364be-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="364be-137">Observe que, atualmente, apenas JSON é aceita para formatos de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="364be-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="364be-138">Não há suporte para XML.</span><span class="sxs-lookup"><span data-stu-id="364be-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="364be-139">APIs de resposta única</span><span class="sxs-lookup"><span data-stu-id="364be-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="364be-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="364be-140">GetSentiment</span></span>
<span data-ttu-id="364be-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="364be-142">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-142">**Example request**</span></span>

<span data-ttu-id="364be-143">Na chamada de saudação abaixo, solicitamos análise de sentimento frase hello "Hello World":</span><span class="sxs-lookup"><span data-stu-id="364be-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="364be-144">Isso retornará uma resposta da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="364be-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="364be-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="364be-145">GetKeyPhrases</span></span>
<span data-ttu-id="364be-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="364be-147">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-147">**Example request**</span></span>

<span data-ttu-id="364be-148">Na chamada de saudação abaixo, solicitamos frases-chave Olá encontrado no texto de saudação "Era um toostay hotel significativos em, casa exclusiva e equipe amigável":</span><span class="sxs-lookup"><span data-stu-id="364be-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="364be-149">Isso retornará uma resposta da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="364be-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="364be-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="364be-150">GetLanguage</span></span>
<span data-ttu-id="364be-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="364be-152">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-152">**Example request**</span></span>

<span data-ttu-id="364be-153">Na chamada GET de saudação abaixo, solicitamos para sentimento Olá frases-chave Olá no texto de saudação *Hello World*</span><span class="sxs-lookup"><span data-stu-id="364be-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="364be-154">Isso retornará uma resposta da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="364be-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="364be-155">**Parâmetros opcionais**</span><span class="sxs-lookup"><span data-stu-id="364be-155">**Optional parameters**</span></span>

<span data-ttu-id="364be-156">`NumberOfLanguagesToDetect` é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="364be-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="364be-157">saudação padrão é 1.</span><span class="sxs-lookup"><span data-stu-id="364be-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="364be-158">APIs de lote</span><span class="sxs-lookup"><span data-stu-id="364be-158">Batch APIs</span></span>
<span data-ttu-id="364be-159">saudação de serviço de análise de texto permite extrações de frase-chave e você sentimento toodo em modo de lote.</span><span class="sxs-lookup"><span data-stu-id="364be-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="364be-160">Observe que cada um dos registros de saudação totalizados contagens como uma transação.</span><span class="sxs-lookup"><span data-stu-id="364be-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="364be-161">Por exemplo, se você solicitar o sentimento de 1000 registros em uma única chamada, ocorrerá a dedução de 1000 transações.</span><span class="sxs-lookup"><span data-stu-id="364be-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="364be-162">Observe que as IDs de saudação inseridos no sistema de saudação são Olá IDs retornados pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="364be-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="364be-163">serviço web de saudação não verifica se essas IDs são exclusivas.</span><span class="sxs-lookup"><span data-stu-id="364be-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="364be-164">É responsabilidade de saudação de exclusividade de tooverify chamador hello.</span><span class="sxs-lookup"><span data-stu-id="364be-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="364be-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="364be-165">GetSentimentBatch</span></span>
<span data-ttu-id="364be-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="364be-167">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-167">**Example request**</span></span>

<span data-ttu-id="364be-168">Em Olá POST chame abaixo, solicitamos para opiniões de saudação de frases hello "Hello World", "Olá, mundo Foo" e "Hello meu World" no corpo de saudação de solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="364be-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="364be-169">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="364be-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="364be-170">Em resposta Olá abaixo, você obter lista de saudação de pontuações associado com o texto de Ids:</span><span class="sxs-lookup"><span data-stu-id="364be-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="364be-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="364be-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="364be-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="364be-173">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-173">**Example request**</span></span>

<span data-ttu-id="364be-174">Neste exemplo, podemos está solicitando a lista de saudação de opiniões de frases-chave Olá em Olá textos a seguir:</span><span class="sxs-lookup"><span data-stu-id="364be-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="364be-175">"Era um toostay hotel significativos em, casa exclusiva e amigável equipe"</span><span class="sxs-lookup"><span data-stu-id="364be-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="364be-176">"Foi uma conferência incrível, com palestras muito interessantes"</span><span class="sxs-lookup"><span data-stu-id="364be-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="364be-177">"tráfego Olá foi terrível, como também três horas vai aeroporto toohello"</span><span class="sxs-lookup"><span data-stu-id="364be-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="364be-178">Essa solicitação é feita como um ponto de extremidade do POST chamada toohello:</span><span class="sxs-lookup"><span data-stu-id="364be-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="364be-179">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="364be-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="364be-180">Em resposta Olá abaixo, você obter lista de saudação de frases-chave associadas com o texto de Ids:</span><span class="sxs-lookup"><span data-stu-id="364be-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="364be-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="364be-181">GetLanguageBatch</span></span>

<span data-ttu-id="364be-182">Em chamada POST de saudação abaixo, solicitamos a detecção de idioma para duas entradas de texto:</span><span class="sxs-lookup"><span data-stu-id="364be-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="364be-183">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="364be-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="364be-184">Isso retorna Olá resposta, a seguir onde inglês for detectado em hello primeiro de entrada e francês na segunda entrada de saudação:</span><span class="sxs-lookup"><span data-stu-id="364be-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="364be-185">APIs de detecção de tópico</span><span class="sxs-lookup"><span data-stu-id="364be-185">Topic Detection APIs</span></span>
<span data-ttu-id="364be-186">Esta é uma API recém-lançado que retorna Olá principais detectado tópicos para obter uma lista de registros de texto enviada.</span><span class="sxs-lookup"><span data-stu-id="364be-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="364be-187">Um tópico é identificado com uma senha, que pode ser uma ou mais palavras relacionadas.</span><span class="sxs-lookup"><span data-stu-id="364be-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="364be-188">Observe que essa API cobra uma transação por registro de texto enviado.</span><span class="sxs-lookup"><span data-stu-id="364be-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="364be-189">Esta API exige um mínimo de 100 texto registra toobe enviada, mas é projetado toodetect tópicos centenas toothousands de registros.</span><span class="sxs-lookup"><span data-stu-id="364be-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="364be-190">Tópicos – enviar trabalho</span><span class="sxs-lookup"><span data-stu-id="364be-190">Topics – Submit job</span></span>
<span data-ttu-id="364be-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="364be-192">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-192">**Example request**</span></span>

<span data-ttu-id="364be-193">Em chamada POST de saudação abaixo, solicitamos tópicos para um conjunto de 100 artigos, onde Olá primeiro e último entrada artigos são mostrados, e dois StopPhrases são incluídos.</span><span class="sxs-lookup"><span data-stu-id="364be-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="364be-194">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="364be-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="364be-195">Resposta de saudação abaixo, você receberá Olá JobId para trabalho enviado hello:</span><span class="sxs-lookup"><span data-stu-id="364be-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="364be-196">Uma lista de frases com uma ou mais palavras que não devem ser retornadas como tópicos.</span><span class="sxs-lookup"><span data-stu-id="364be-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="364be-197">Pode ser usado toofilter out tópicos muito genéricos.</span><span class="sxs-lookup"><span data-stu-id="364be-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="364be-198">Por exemplo, em um conjunto de dados sobre análises de hotéis, "hotel" e "hostel" podem ser frases de interrupção adequadas.</span><span class="sxs-lookup"><span data-stu-id="364be-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="364be-199">Tópicos – pesquisa de resultados do trabalho</span><span class="sxs-lookup"><span data-stu-id="364be-199">Topics – Poll for job results</span></span>
<span data-ttu-id="364be-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="364be-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="364be-201">**Solicitação de exemplo**</span><span class="sxs-lookup"><span data-stu-id="364be-201">**Example request**</span></span>

<span data-ttu-id="364be-202">Passe Olá que jobId retornado nos resultados de Olá Olá 'Enviar trabalho' etapa toofetch.</span><span class="sxs-lookup"><span data-stu-id="364be-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="364be-203">É recomendável que você chamar esse ponto de extremidade a cada minuto até que o Status = 'Concluído' na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="364be-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="364be-204">Levará cerca de 10 minutos por toocomplete um trabalho, ou mais para trabalhos com milhares de registros.</span><span class="sxs-lookup"><span data-stu-id="364be-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="364be-205">Durante o processamento, resposta Olá será da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="364be-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="364be-206">Olá API retorna a saída no formato JSON em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="364be-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="364be-207">Propriedades de saudação para cada parte da resposta de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="364be-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="364be-208">**Propriedades de TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="364be-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="364be-209">Chave</span><span class="sxs-lookup"><span data-stu-id="364be-209">Key</span></span> | <span data-ttu-id="364be-210">Descrição</span><span class="sxs-lookup"><span data-stu-id="364be-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="364be-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="364be-211">TopicId</span></span> |<span data-ttu-id="364be-212">Um identificador exclusivo para cada tópico.</span><span class="sxs-lookup"><span data-stu-id="364be-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="364be-213">Pontuação</span><span class="sxs-lookup"><span data-stu-id="364be-213">Score</span></span> |<span data-ttu-id="364be-214">Contagem de registros atribuído tootopic.</span><span class="sxs-lookup"><span data-stu-id="364be-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="364be-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="364be-215">KeyPhrase</span></span> |<span data-ttu-id="364be-216">Uma palavra ou frase para tópico Olá resumindo.</span><span class="sxs-lookup"><span data-stu-id="364be-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="364be-217">Pode ser uma ou várias palavras.</span><span class="sxs-lookup"><span data-stu-id="364be-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="364be-218">**Propriedades de TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="364be-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="364be-219">Chave</span><span class="sxs-lookup"><span data-stu-id="364be-219">Key</span></span> | <span data-ttu-id="364be-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="364be-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="364be-221">ID</span><span class="sxs-lookup"><span data-stu-id="364be-221">Id</span></span> |<span data-ttu-id="364be-222">Identificador de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="364be-222">Identifier for hello record.</span></span> <span data-ttu-id="364be-223">É igual a ID toohello incluída na entrada hello.</span><span class="sxs-lookup"><span data-stu-id="364be-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="364be-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="364be-224">TopicId</span></span> |<span data-ttu-id="364be-225">Olá qual registro Olá foi atribuído a ID do tópico.</span><span class="sxs-lookup"><span data-stu-id="364be-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="364be-226">Distância</span><span class="sxs-lookup"><span data-stu-id="364be-226">Distance</span></span> |<span data-ttu-id="364be-227">Confiança registro Olá pertence toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="364be-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="364be-228">Toozero mais próximo de distância indica maior confiança.</span><span class="sxs-lookup"><span data-stu-id="364be-228">Distance closer toozero indicates higher confidence.</span></span> |

