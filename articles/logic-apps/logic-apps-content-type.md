---
title: "tipos de conteúdo aaaHandle - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como os aplicativos lógicos do Azure lidam com tipos de conteúdo em tempo de execução e de design"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="7c7ac-103">Gerenciamento de tipos de conteúdo em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="7c7ac-103">Handle content types in logic apps</span></span>

<span data-ttu-id="7c7ac-104">JSON, XML, arquivos simples e dados binários são alguns dos diversos tipos de conteúdo que podem fluir em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="7c7ac-105">Enquanto o hello lógica aplicativos mecanismo dá suporte a todos os tipos de conteúdo, algumas nativamente são entendidas pelo Olá lógica de mecanismo de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="7c7ac-106">Outros podem exigir transmissões ou conversões conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="7c7ac-107">Este artigo descreve como o mecanismo de saudação lida com diferentes tipos de conteúdo e como toocorrectly tratar desses tipos, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="7c7ac-108">Cabeçalho Content-Type</span><span class="sxs-lookup"><span data-stu-id="7c7ac-108">Content-Type Header</span></span>

<span data-ttu-id="7c7ac-109">toostart basicamente, vejamos Olá dois `Content-Types` que não exigem conversão ou conversão que você pode usar em um aplicativo lógico: `application/json` e `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="7c7ac-110">Aplicativo/JSON</span><span class="sxs-lookup"><span data-stu-id="7c7ac-110">Application/JSON</span></span>

<span data-ttu-id="7c7ac-111">mecanismo de fluxo de trabalho Olá depende Olá `Content-Type` cabeçalho de HTTP chama o tratamento do toodetermine Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="7c7ac-112">Qualquer solicitação com o tipo de conteúdo Olá `application/json` são armazenados e manipulados como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="7c7ac-113">Além disso, o conteúdo JSON pode ser analisado por padrão sem a necessidade de conversão.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="7c7ac-114">Por exemplo, você poderia analisar uma solicitação que tem o cabeçalho de tipo de conteúdo de saudação `application/json ` em um fluxo de trabalho usando uma expressão como `@body('myAction')['foo'][0]` valor de saudação tooget `bar` nesse caso:</span><span class="sxs-lookup"><span data-stu-id="7c7ac-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="7c7ac-115">Nenhuma conversão adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-115">No additional casting is needed.</span></span> <span data-ttu-id="7c7ac-116">Se você estiver trabalhando com dados JSON mas não tinham um cabeçalho especificado, você pode manualmente convertê-lo tooJSON usando Olá `@json()` funcionar, por exemplo: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="7c7ac-117">Esquema e gerador de esquema</span><span class="sxs-lookup"><span data-stu-id="7c7ac-117">Schema and schema generator</span></span>

<span data-ttu-id="7c7ac-118">Olá gatilho de solicitação permite que você tooenter um esquema JSON para carga Olá esperado tooreceive.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="7c7ac-119">Esse esquema permite que o designer Olá gerar tokens para que você poder consumir conteúdo de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="7c7ac-120">Se você não tiver um esquema pronto, selecione **esquema de toogenerate de carga de exemplo de uso**, portanto, você pode gerar um esquema JSON de uma carga de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Esquema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="7c7ac-122">Ação "Parse JSON"</span><span class="sxs-lookup"><span data-stu-id="7c7ac-122">'Parse JSON' action</span></span>

<span data-ttu-id="7c7ac-123">Olá `Parse JSON` ação lhe permite analisar o conteúdo JSON em tokens amigáveis para o consumo lógica de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="7c7ac-124">Gatilho de solicitação toohello semelhante, esta ação permite que você insira ou gere um esquema JSON para Olá conteúdo que você deseja tooparse.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="7c7ac-125">Essa ferramenta facilita grande parte do consumo de dados do Barramento de Serviço, do Azure Cosmos DB e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Analisar o JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="7c7ac-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="7c7ac-127">Text/plain</span></span>

<span data-ttu-id="7c7ac-128">Semelhante muito`application/json`, mensagens HTTP recebidas com hello `Content-Type` cabeçalho de `text/plain` são armazenados em formato bruto.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="7c7ac-129">Além disso, se essas mensagens são incluídas em ações subsequentes sem conversão, essas solicitações saem com o cabeçalho `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="7c7ac-130">Por exemplo, ao trabalhar com um arquivo simples, você pode obter esse conteúdo HTTP como `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="7c7ac-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="7c7ac-131">Se na ação de Avançar hello, enviar solicitação hello como corpo de saudação da outra solicitação (`@body('flatfile')`), solicitação Olá teria um `text/plain` cabeçalho Content-Type.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="7c7ac-132">Se você estiver trabalhando com dados que é um texto sem formatação, mas não tinham um cabeçalho especificado, você pode converter manualmente Olá dados tootext usando Olá `@string()` funcionar, por exemplo: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="7c7ac-133">Application/xml e Application/octet-stream e funções de conversor</span><span class="sxs-lookup"><span data-stu-id="7c7ac-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="7c7ac-134">Olá lógica aplicativos mecanismo sempre preserva Olá `Content-Type` que foi recebido no hello HTTP solicitação ou resposta.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="7c7ac-135">Portanto, se o mecanismo de saudação recebe o conteúdo com hello `Content-Type` de `application/octet-stream`, e você incluir que conteúdo em uma ação subsequente sem conversão, solicitação de saída de hello tem `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="7c7ac-136">Dessa forma, mecanismo de saudação pode garantir a dados não sejam perdidos durante a movimentação por meio do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="7c7ac-137">No entanto, o estado de ação de saudação (entradas e saídas) é armazenado em um objeto JSON como Olá move estado por meio do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="7c7ac-138">Portanto toopreserve converte alguns tipos de dados, o mecanismo de Olá Olá tooa conteúdo binário codificado na base64 cadeia de caracteres com os metadados apropriados que preserva as `$content` e `$content-type`, que são automaticamente ser convertido.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="7c7ac-139">`@json()`-Converte dados muito`application/json`</span><span class="sxs-lookup"><span data-stu-id="7c7ac-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="7c7ac-140">`@xml()`-Converte dados muito`application/xml`</span><span class="sxs-lookup"><span data-stu-id="7c7ac-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="7c7ac-141">`@binary()`-Converte dados muito`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="7c7ac-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="7c7ac-142">`@string()`-Converte dados muito`text/plain`</span><span class="sxs-lookup"><span data-stu-id="7c7ac-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="7c7ac-143">`@base64()`-Converte a cadeia de caracteres de base64 tooa conteúdo</span><span class="sxs-lookup"><span data-stu-id="7c7ac-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="7c7ac-144">`@base64toString()`-Converte uma cadeia de caracteres codificada em base64 muito`text/plain`</span><span class="sxs-lookup"><span data-stu-id="7c7ac-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="7c7ac-145">`@base64toBinary()`-Converte uma cadeia de caracteres codificada em base64 muito`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="7c7ac-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="7c7ac-146">`@encodeDataUri()` - codifica uma cadeia de caracteres como uma matriz de bytes dataUri</span><span class="sxs-lookup"><span data-stu-id="7c7ac-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="7c7ac-147">`@decodeDataUri()` - decodifica uma dataUri em uma matriz de bytes</span><span class="sxs-lookup"><span data-stu-id="7c7ac-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="7c7ac-148">Por exemplo, caso tenha recebido uma solicitação HTTP com `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="7c7ac-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="7c7ac-149">Você pode converter e usar mais tarde com algo como `@xml(triggerBody())`, ou em uma função como `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="7c7ac-150">Outros tipos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="7c7ac-150">Other content types</span></span>

<span data-ttu-id="7c7ac-151">Outros tipos de conteúdo são suportados e trabalhar com aplicativos lógicos, mas pode exigir o corpo da mensagem de saudação recuperar manualmente decodificando Olá `$content`.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="7c7ac-152">Por exemplo, suponha que você acionar uma `application/x-www-url-formencoded` solicitação onde `$content` é carga Olá codificado como uma toopreserve de cadeia de caracteres base64 todos os dados:</span><span class="sxs-lookup"><span data-stu-id="7c7ac-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="7c7ac-153">Porque a solicitação de saudação não for texto sem formatação ou JSON, Olá armazenado na ação de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7c7ac-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Atualmente, não existe uma função nativa para dados do formulário, para que você ainda pode usar esses dados em um fluxo de trabalho manualmente acessando dados Olá com uma função, como `@string(body('formdataAction'))`. Se você quisesse Olá solicitação de saída tooalso ter Olá `application/x-www-url-formencoded` cabeçalho de tipo de conteúdo, você pode adicionar o corpo de ação de toohello Olá solicitação sem qualquer conversão como `@body('formdataAction')`. No entanto, esse método funciona somente se o corpo Olá é parâmetro somente Olá Olá `body` entrada. <span data-ttu-id="7c7ac-157">Se você tentar toouse `@body('formdataAction')` em um `application/json` solicitar, você obtém um erro de tempo de execução porque o corpo da saudação codificado é enviado.</span><span class="sxs-lookup"><span data-stu-id="7c7ac-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

