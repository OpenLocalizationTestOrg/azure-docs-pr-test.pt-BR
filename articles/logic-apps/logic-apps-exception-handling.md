---
title: "aaaError & tratamento de exceção - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Padrões para tratamento de erros e exceções em Aplicativos Lógicos do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="54233-103">Tratar erros e exceções em Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="54233-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="54233-104">Aplicativos lógicos do Azure fornece ferramentas avançadas e padrões toohelp você verificar se que seu integrações são robusto e flexível contra falhas.</span><span class="sxs-lookup"><span data-stu-id="54233-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="54233-105">Qualquer arquitetura de integração representa Olá desafio de tornar o tempo de inatividade de identificador se tooappropriately ou problemas de sistemas dependentes.</span><span class="sxs-lookup"><span data-stu-id="54233-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="54233-106">Lógica de aplicativos torna a manipulação de erros uma experiência de primeira classe, dando a você Olá ferramentas necessárias tooact em exceções e erros em seus fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="54233-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="54233-107">Políticas de repetição</span><span class="sxs-lookup"><span data-stu-id="54233-107">Retry policies</span></span>

<span data-ttu-id="54233-108">Uma política de repetição é o tipo mais básico de saudação de exceção e tratamento de erros.</span><span class="sxs-lookup"><span data-stu-id="54233-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="54233-109">Se uma solicitação inicial atingiu o tempo limite ou falhou (qualquer solicitação que resulta em um 429 ou resposta 5xx), essa política define se a ação de saudação deve tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="54233-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="54233-110">Por padrão, todas as ações tentam novamente por mais quatro vezes em intervalos de 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="54233-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="54233-111">Portanto, se a primeira solicitação de saudação recebe um `500 Internal Server Error` resposta, o mecanismo de fluxo de trabalho Olá pausa por 20 segundos e tentativas Olá solicitação novamente.</span><span class="sxs-lookup"><span data-stu-id="54233-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="54233-112">Se depois de todas as novas tentativas, resposta Olá ainda é uma exceção ou uma falha, o fluxo de trabalho de saudação continua e marcas Olá status de ação como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="54233-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="54233-113">Você pode configurar políticas de repetição Olá **entradas** para uma determinada ação.</span><span class="sxs-lookup"><span data-stu-id="54233-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="54233-114">Por exemplo, você pode configurar um tootry de política de repetição até 4 vezes em intervalos de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="54233-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="54233-115">Para obter detalhes completos sobre as propriedades de entrada, confira [Ações de fluxo de trabalho e gatilhos][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="54233-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="54233-116">Se você quisesse seu tooretry de ação HTTP 4 vezes e aguarde 10 minutos entre cada tentativa, você usaria Olá definição a seguir:</span><span class="sxs-lookup"><span data-stu-id="54233-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="54233-117">Para obter mais informações sobre a sintaxe com suporte, consulte Olá [seção da política de repetição em gatilhos e ações de fluxo de trabalho][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="54233-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="54233-118">Detectar falhas com hello RunAfter propriedade</span><span class="sxs-lookup"><span data-stu-id="54233-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="54233-119">Cada ação de aplicativo lógica declara quais ações devem terminar antes do início de ação hello, como a ordenação de etapas de saudação do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="54233-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="54233-120">Na definição de ação hello, essa ordem é conhecido como Olá `runAfter` propriedade.</span><span class="sxs-lookup"><span data-stu-id="54233-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="54233-121">Essa propriedade é um objeto que descreve quais ações e o status de ação executar a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="54233-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="54233-122">Por padrão, todas as ações adicionadas por meio de saudação lógica de aplicativo Designer estão definidas muito`runAfter` etapa anterior de saudação se hello etapa anterior `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="54233-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="54233-123">No entanto, você pode personalizar as ações de toofire este valor quando as ações anteriores têm `Failed`, `Skipped`, ou um conjunto de possíveis desses valores.</span><span class="sxs-lookup"><span data-stu-id="54233-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="54233-124">Se você quisesse tooadd tooa um item designado tópico do barramento de serviço depois de uma ação específica `Insert_Row` falhar, você pode usar o hello após `runAfter` configuração:</span><span class="sxs-lookup"><span data-stu-id="54233-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="54233-125">Saudação de aviso `runAfter` propriedade é definida toofire se hello `Insert_Row` ação é `Failed`.</span><span class="sxs-lookup"><span data-stu-id="54233-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="54233-126">ação de saudação toorun se o status da ação Olá é `Succeeded`, `Failed`, ou `Skipped`, use a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="54233-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="54233-127">Ações que são executadas e concluídas com êxito depois que uma ação anterior falha são marcadas como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="54233-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="54233-128">Esse comportamento significa que se você captura todas as falhas de com êxito em um fluxo de trabalho, Olá execute em si está marcada como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="54233-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="54233-129">Escopos e resultados de ações de tooevaluate</span><span class="sxs-lookup"><span data-stu-id="54233-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="54233-130">Toohow semelhante que você pode executar depois de ações individuais, você pode também agrupar ações dentro de um [escopo](../logic-apps/logic-apps-loops-and-scopes.md), que atuam como um agrupamento lógico de ações.</span><span class="sxs-lookup"><span data-stu-id="54233-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="54233-131">Os escopos são úteis para organizar suas ações de lógica de aplicativo e para executar avaliações de agregação em status de saudação de um escopo.</span><span class="sxs-lookup"><span data-stu-id="54233-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="54233-132">escopo de saudação se recebe um status depois de concluir todas as ações em um escopo.</span><span class="sxs-lookup"><span data-stu-id="54233-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="54233-133">status de saudação do escopo é determinado por hello mesmos critérios de uma execução.</span><span class="sxs-lookup"><span data-stu-id="54233-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="54233-134">Se a ação final Olá em uma ramificação de execução é `Failed` ou `Aborted`, status de saudação é `Failed`.</span><span class="sxs-lookup"><span data-stu-id="54233-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="54233-135">toofire ações específicas para erros que ocorreram no escopo de saudação, você pode usar `runAfter` com um escopo que está marcado como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="54233-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="54233-136">Se *qualquer* ações no escopo de saudação falharem, a execução após a falha de um escopo permite que você criar uma única ação toocatch falhas.</span><span class="sxs-lookup"><span data-stu-id="54233-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="54233-137">Obtendo o contexto de saudação de falhas com resultados</span><span class="sxs-lookup"><span data-stu-id="54233-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="54233-138">Embora seja útil capturar falhas de um escopo, você também poderá toohelp contexto que entender exatamente quais ações de falha, e nenhum erro ou códigos de status que foram retornados.</span><span class="sxs-lookup"><span data-stu-id="54233-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="54233-139">Olá `@result()` função de fluxo de trabalho fornece contexto sobre o resultado de saudação de todas as ações em um escopo.</span><span class="sxs-lookup"><span data-stu-id="54233-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="54233-140">`@result()`usa um único parâmetro, o nome do escopo e retorna uma matriz de todos os resultados da ação saudação do dentro desse escopo.</span><span class="sxs-lookup"><span data-stu-id="54233-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="54233-141">Esses objetos de ação incluem hello mesmo atributos como Olá `@actions()` objeto, incluindo a hora de início da ação, hora de término da ação, status da ação, entradas de ação, IDs de correlação de ação e ação gera.</span><span class="sxs-lookup"><span data-stu-id="54233-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="54233-142">toosend o contexto de quaisquer ações que falharam em um escopo, você pode emparelhar facilmente um `@result()` funcionar com um `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="54233-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="54233-143">tooexecute uma ação *para cada* ação em um escopo que `Failed`, matriz de saudação do filtro de resultados tooactions que falharam, você pode emparelhar `@result()` com um  **[matriz de filtro](../connectors/connectors-native-query.md)**  ação e um  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  loop.</span><span class="sxs-lookup"><span data-stu-id="54233-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="54233-144">Você pode levar a matriz de resultados filtrados hello e executar uma ação para cada falha usando Olá **ForEach** loop.</span><span class="sxs-lookup"><span data-stu-id="54233-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="54233-145">Aqui está um exemplo, seguido por uma explicação detalhada, que envia uma solicitação HTTP POST com corpo de resposta de saudação de quaisquer ações que falharam no escopo de saudação `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="54233-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="54233-146">Aqui está um toodescribe de passo a passo detalhado, o que acontece:</span><span class="sxs-lookup"><span data-stu-id="54233-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="54233-147">resultado de saudação tooget de todas as ações no `My_Scope`, Olá **matriz de filtro** filtros de ação `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="54233-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="54233-148">Olá condição para **matriz de filtro** é qualquer `@result()` item com status igual muito`Failed`.</span><span class="sxs-lookup"><span data-stu-id="54233-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="54233-149">Essa condição filtra a matriz Olá com todos os resultados de ação de `My_Scope` tooan matriz somente com resultados de ação de falha.</span><span class="sxs-lookup"><span data-stu-id="54233-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="54233-150">Executar um **para cada** ação Olá **matriz filtrados** saídas.</span><span class="sxs-lookup"><span data-stu-id="54233-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="54233-151">Esta etapa executa uma ação *para cada* resultado de ação com falha que foi filtrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="54233-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="54233-152">Se uma única ação no escopo de saudação falhou, Olá ações no hello `foreach` executar apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="54233-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="54233-153">Muitas ações com falha causam uma ação por falha.</span><span class="sxs-lookup"><span data-stu-id="54233-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="54233-154">Enviar um HTTP POST em Olá `foreach` corpo da resposta, do item ou `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="54233-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="54233-155">Olá `@result()` forma item é Olá mesmo como Olá `@actions()` forma e pode ser analisado Olá mesmo modo.</span><span class="sxs-lookup"><span data-stu-id="54233-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="54233-156">Incluem dois cabeçalhos personalizados com o nome de ação que falhou Olá `@item()['name']` e Olá falha cliente ID de rastreamento `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="54233-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="54233-157">Para referência, aqui está um exemplo de um único `@result()` item, mostrando Olá `name`, `body`, e `clientTrackingId` propriedades que são analisadas no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="54233-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="54233-158">Fora de um `foreach`, `@result()` retorna uma matriz desses objetos.</span><span class="sxs-lookup"><span data-stu-id="54233-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="54233-159">padrões de tratamento de exceção diferente de tooperform, você pode usar expressões Olá mostradas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="54233-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="54233-160">Você pode escolher uma única ação fora de escopo de saudação que aceita Olá toda filtrado matriz de falhas de tratamento de exceção de tooexecute e remover Olá `foreach`.</span><span class="sxs-lookup"><span data-stu-id="54233-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="54233-161">Você também pode incluir outras propriedades úteis do hello `@result()` resposta mostrada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="54233-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="54233-162">Diagnósticos do Azure e telemetria</span><span class="sxs-lookup"><span data-stu-id="54233-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="54233-163">Hello padrões anteriores são erros de toohandle excelente maneira e exceções dentro de uma execução, mas você também pode identificar e responder tooerrors independente da saudação execute em si.</span><span class="sxs-lookup"><span data-stu-id="54233-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="54233-164">[Diagnóstico do Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fornece uma maneira simples de toosend todas as conta de armazenamento do Azure tooan de fluxo de trabalho de eventos (incluindo todos os status de execução e ação) ou um Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="54233-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="54233-165">tooevaluate executar status, você pode monitorar logs hello e métricas ou publicá-los em qualquer ferramenta de monitoramento que você preferir.</span><span class="sxs-lookup"><span data-stu-id="54233-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="54233-166">Uma opção de potencial é toostream todos os eventos de saudação por meio do Hub de eventos do Azure em [do Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="54233-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="54233-167">No Stream Analytics, você pode escrever consultas ao vivo fora de qualquer anomalias, médias ou falhas de saudação logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="54233-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="54233-168">Análise de fluxo pode facilmente produzir tooother fontes de dados como filas, tópicos, SQL, o banco de dados do Azure Cosmos e Power BI.</span><span class="sxs-lookup"><span data-stu-id="54233-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54233-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54233-169">Next Steps</span></span>

* [<span data-ttu-id="54233-170">Veja como um cliente compila o tratamento de erros com Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="54233-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="54233-171">Encontrar mais exemplos e cenários dos Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="54233-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="54233-172">Saiba como toocreate automatizado implantações de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="54233-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="54233-173">Compilar e implantar aplicativos lógicos no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54233-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
