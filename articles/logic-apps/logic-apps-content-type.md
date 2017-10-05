---
title: "Manipulação de tipos de conteúdo - Aplicativos lógicos do Azure | Microsoft Docs"
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
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="94cbd-103">Gerenciamento de tipos de conteúdo em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="94cbd-103">Handle content types in logic apps</span></span>

<span data-ttu-id="94cbd-104">JSON, XML, arquivos simples e dados binários são alguns dos diversos tipos de conteúdo que podem fluir em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="94cbd-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="94cbd-105">O mecanismo de aplicativos lógicos oferece suporte a todos os tipos de conteúdo e também é capaz de compreender nativamente o mecanismo de aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="94cbd-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="94cbd-106">Outros podem exigir transmissões ou conversões conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="94cbd-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="94cbd-107">Este artigo descreve como o mecanismo gerencia diferentes tipos de conteúdo e como lidar corretamente com esses tipos quando necessário.</span><span class="sxs-lookup"><span data-stu-id="94cbd-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="94cbd-108">Cabeçalho Content-Type</span><span class="sxs-lookup"><span data-stu-id="94cbd-108">Content-Type Header</span></span>

<span data-ttu-id="94cbd-109">Para iniciar, vamos examinar os dois `Content-Types` que não requerem transmissão nem conversão que podem ser usados em um aplicativo lógico: `application/json` e `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="94cbd-110">Aplicativo/JSON</span><span class="sxs-lookup"><span data-stu-id="94cbd-110">Application/JSON</span></span>

<span data-ttu-id="94cbd-111">O mecanismo de fluxo de trabalho depende do cabeçalho `Content-Type` de chamadas HTTP para determinar o tratamento apropriado.</span><span class="sxs-lookup"><span data-stu-id="94cbd-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="94cbd-112">Qualquer solicitação com o tipo de conteúdo `application/json` será armazenada e tratada como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="94cbd-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="94cbd-113">Além disso, o conteúdo JSON pode ser analisado por padrão sem a necessidade de conversão.</span><span class="sxs-lookup"><span data-stu-id="94cbd-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="94cbd-114">Por exemplo, para analisar uma solicitação com o cabeçalho de tipo de conteúdo `application/json ` em um fluxo de trabalho, use uma expressão como `@body('myAction')['foo'][0]` para obter o valor `bar`, nesse caso:</span><span class="sxs-lookup"><span data-stu-id="94cbd-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="94cbd-115">Nenhuma conversão adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="94cbd-115">No additional casting is needed.</span></span> <span data-ttu-id="94cbd-116">Se estiver trabalhando com dados JSON, mas não tiver um cabeçalho especificado, você poderá convertê-lo manualmente para JSON usando a função `@json()`, por exemplo: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="94cbd-117">Esquema e gerador de esquema</span><span class="sxs-lookup"><span data-stu-id="94cbd-117">Schema and schema generator</span></span>

<span data-ttu-id="94cbd-118">O gatilho da solicitação permite que você insira um esquema JSON para o conteúdo que espera receber.</span><span class="sxs-lookup"><span data-stu-id="94cbd-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="94cbd-119">Esse esquema permite que o designer gere tokens para que você possa consumir o conteúdo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="94cbd-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="94cbd-120">Se não tiver um esquema pronto, escolha **Usar o conteúdo de exemplo para gerar esquema** para poder gerar um esquema JSON de um conteúdo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="94cbd-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Esquema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="94cbd-122">Ação "Parse JSON"</span><span class="sxs-lookup"><span data-stu-id="94cbd-122">'Parse JSON' action</span></span>

<span data-ttu-id="94cbd-123">A ação `Parse JSON` permite que você analise o conteúdo JSON em tokens amigáveis para o consumo do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="94cbd-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="94cbd-124">Assim como com o gatilho da solicitação, essa ação permite que você insira ou gere um esquema JSON para o conteúdo que você deseja analisar.</span><span class="sxs-lookup"><span data-stu-id="94cbd-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="94cbd-125">Essa ferramenta facilita grande parte do consumo de dados do Barramento de Serviço, do Azure Cosmos DB e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="94cbd-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Analisar o JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="94cbd-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="94cbd-127">Text/plain</span></span>

<span data-ttu-id="94cbd-128">Assim como `application/json`, as mensagens HTTP recebidas com o cabeçalho `Content-Type` de `text/plain` são armazenadas em sua forma bruta.</span><span class="sxs-lookup"><span data-stu-id="94cbd-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="94cbd-129">Além disso, se essas mensagens são incluídas em ações subsequentes sem conversão, essas solicitações saem com o cabeçalho `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="94cbd-130">Por exemplo, ao trabalhar com um arquivo simples, você pode obter esse conteúdo HTTP como `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="94cbd-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="94cbd-131">Se na próxima ação, você a enviar como o corpo de outra solicitação (`@body('flatfile')`), a solicitação terá um cabeçalho Content-Type `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="94cbd-132">Se estiver trabalhando com dados de texto sem formatação, mas não tiver um cabeçalho especificado, você poderá converter os dados manualmente para texto usando a função `@string()`, por exemplo: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="94cbd-133">Application/xml e Application/octet-stream e funções de conversor</span><span class="sxs-lookup"><span data-stu-id="94cbd-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="94cbd-134">O mecanismo de aplicativos lógicos sempre mantém o `Content-Type` recebido na resposta ou solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="94cbd-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="94cbd-135">Portanto, se o mecanismo recebe o conteúdo com o `Content-Type` de `application/octet-stream`, e você inclui o conteúdo em uma ação subsequente sem conversão, a solicitação de saída tem `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="94cbd-136">Dessa forma, o mecanismo garante que dados não sejam perdidos ao movê-los pelo fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="94cbd-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="94cbd-137">No entanto, o estado de ação (entradas e saídas) é armazenado em um objeto JSON conforme o estado se move no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="94cbd-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="94cbd-138">Ou seja, para preservar alguns tipos de dados, o mecanismo converte o conteúdo em uma cadeia de caracteres codificada em base64 binária com os metadados apropriados que preservam `$content` e `$content-type`, que são convertidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="94cbd-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="94cbd-139">`@json()` - converte dados em `application/json`</span><span class="sxs-lookup"><span data-stu-id="94cbd-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="94cbd-140">`@xml()` - converte dados em `application/xml`</span><span class="sxs-lookup"><span data-stu-id="94cbd-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="94cbd-141">`@binary()` - converte dados em `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="94cbd-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="94cbd-142">`@string()` - converte dados em `text/plain`</span><span class="sxs-lookup"><span data-stu-id="94cbd-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="94cbd-143">`@base64()` - converte conteúdo em uma cadeia de caracteres de base64</span><span class="sxs-lookup"><span data-stu-id="94cbd-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="94cbd-144">`@base64toString()` - converte uma cadeia de caracteres codificada em base64 em `text/plain`</span><span class="sxs-lookup"><span data-stu-id="94cbd-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="94cbd-145">`@base64toBinary()` - converte uma cadeia de caracteres codificada em base64 em `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="94cbd-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="94cbd-146">`@encodeDataUri()` - codifica uma cadeia de caracteres como uma matriz de bytes dataUri</span><span class="sxs-lookup"><span data-stu-id="94cbd-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="94cbd-147">`@decodeDataUri()` - decodifica uma dataUri em uma matriz de bytes</span><span class="sxs-lookup"><span data-stu-id="94cbd-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="94cbd-148">Por exemplo, caso tenha recebido uma solicitação HTTP com `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="94cbd-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="94cbd-149">Você pode converter e usar mais tarde com algo como `@xml(triggerBody())`, ou em uma função como `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="94cbd-150">Outros tipos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="94cbd-150">Other content types</span></span>

<span data-ttu-id="94cbd-151">Outros tipos de conteúdo têm suporte e funcionam com aplicativos lógicos, mas podem exigir a recuperação manual do corpo da mensagem por meio da decodificação do `$content`.</span><span class="sxs-lookup"><span data-stu-id="94cbd-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="94cbd-152">Por exemplo, suponha que você dispare uma solicitação `application/x-www-url-formencoded` onde `$content` é o conteúdo codificado como uma cadeia de caracteres base64 para preservar todos os dados:</span><span class="sxs-lookup"><span data-stu-id="94cbd-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="94cbd-153">Como a solicitação não é texto sem formatação, nem JSON, ela é armazenada na ação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="94cbd-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Quando não houver uma função nativa para dados de formulário, você ainda pode usar esses dados em um fluxo de trabalho ao acessar manualmente os dados com uma função como `@string(body('formdataAction'))`. Se desejar que a solicitação de saída também tenha o cabeçalho de tipo de conteúdo `application/x-www-url-formencoded` , você pode adicionar a solicitação ao corpo de ação sem conversões, como `@body('formdataAction')`. No entanto, esse método só funciona se o corpo é o único parâmetro na entrada `body`. <span data-ttu-id="94cbd-157">Se você tentar usar `@body('formdataAction')` em uma solicitação `application/json`, o corpo codificado será enviado causando erro de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="94cbd-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

