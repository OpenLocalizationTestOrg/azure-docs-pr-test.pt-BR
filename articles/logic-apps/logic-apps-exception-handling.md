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
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Tratar erros e exceções em Aplicativos Lógicos do Azure

Aplicativos lógicos do Azure fornece ferramentas avançadas e padrões toohelp você verificar se que seu integrações são robusto e flexível contra falhas. Qualquer arquitetura de integração representa Olá desafio de tornar o tempo de inatividade de identificador se tooappropriately ou problemas de sistemas dependentes. Lógica de aplicativos torna a manipulação de erros uma experiência de primeira classe, dando a você Olá ferramentas necessárias tooact em exceções e erros em seus fluxos de trabalho.

## <a name="retry-policies"></a>Políticas de repetição

Uma política de repetição é o tipo mais básico de saudação de exceção e tratamento de erros. Se uma solicitação inicial atingiu o tempo limite ou falhou (qualquer solicitação que resulta em um 429 ou resposta 5xx), essa política define se a ação de saudação deve tentar novamente. Por padrão, todas as ações tentam novamente por mais quatro vezes em intervalos de 20 segundos. Portanto, se a primeira solicitação de saudação recebe um `500 Internal Server Error` resposta, o mecanismo de fluxo de trabalho Olá pausa por 20 segundos e tentativas Olá solicitação novamente. Se depois de todas as novas tentativas, resposta Olá ainda é uma exceção ou uma falha, o fluxo de trabalho de saudação continua e marcas Olá status de ação como `Failed`.

Você pode configurar políticas de repetição Olá **entradas** para uma determinada ação. Por exemplo, você pode configurar um tootry de política de repetição até 4 vezes em intervalos de 1 hora. Para obter detalhes completos sobre as propriedades de entrada, confira [Ações de fluxo de trabalho e gatilhos][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Se você quisesse seu tooretry de ação HTTP 4 vezes e aguarde 10 minutos entre cada tentativa, você usaria Olá definição a seguir:

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

Para obter mais informações sobre a sintaxe com suporte, consulte Olá [seção da política de repetição em gatilhos e ações de fluxo de trabalho][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Detectar falhas com hello RunAfter propriedade

Cada ação de aplicativo lógica declara quais ações devem terminar antes do início de ação hello, como a ordenação de etapas de saudação do fluxo de trabalho. Na definição de ação hello, essa ordem é conhecido como Olá `runAfter` propriedade. Essa propriedade é um objeto que descreve quais ações e o status de ação executar a ação de saudação. Por padrão, todas as ações adicionadas por meio de saudação lógica de aplicativo Designer estão definidas muito`runAfter` etapa anterior de saudação se hello etapa anterior `Succeeded`. No entanto, você pode personalizar as ações de toofire este valor quando as ações anteriores têm `Failed`, `Skipped`, ou um conjunto de possíveis desses valores. Se você quisesse tooadd tooa um item designado tópico do barramento de serviço depois de uma ação específica `Insert_Row` falhar, você pode usar o hello após `runAfter` configuração:

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

Saudação de aviso `runAfter` propriedade é definida toofire se hello `Insert_Row` ação é `Failed`. ação de saudação toorun se o status da ação Olá é `Succeeded`, `Failed`, ou `Skipped`, use a seguinte sintaxe:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Ações que são executadas e concluídas com êxito depois que uma ação anterior falha são marcadas como `Succeeded`. Esse comportamento significa que se você captura todas as falhas de com êxito em um fluxo de trabalho, Olá execute em si está marcada como `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Escopos e resultados de ações de tooevaluate

Toohow semelhante que você pode executar depois de ações individuais, você pode também agrupar ações dentro de um [escopo](../logic-apps/logic-apps-loops-and-scopes.md), que atuam como um agrupamento lógico de ações. Os escopos são úteis para organizar suas ações de lógica de aplicativo e para executar avaliações de agregação em status de saudação de um escopo. escopo de saudação se recebe um status depois de concluir todas as ações em um escopo. status de saudação do escopo é determinado por hello mesmos critérios de uma execução. Se a ação final Olá em uma ramificação de execução é `Failed` ou `Aborted`, status de saudação é `Failed`.

toofire ações específicas para erros que ocorreram no escopo de saudação, você pode usar `runAfter` com um escopo que está marcado como `Failed`. Se *qualquer* ações no escopo de saudação falharem, a execução após a falha de um escopo permite que você criar uma única ação toocatch falhas.

### <a name="getting-hello-context-of-failures-with-results"></a>Obtendo o contexto de saudação de falhas com resultados

Embora seja útil capturar falhas de um escopo, você também poderá toohelp contexto que entender exatamente quais ações de falha, e nenhum erro ou códigos de status que foram retornados. Olá `@result()` função de fluxo de trabalho fornece contexto sobre o resultado de saudação de todas as ações em um escopo.

`@result()`usa um único parâmetro, o nome do escopo e retorna uma matriz de todos os resultados da ação saudação do dentro desse escopo. Esses objetos de ação incluem hello mesmo atributos como Olá `@actions()` objeto, incluindo a hora de início da ação, hora de término da ação, status da ação, entradas de ação, IDs de correlação de ação e ação gera. toosend o contexto de quaisquer ações que falharam em um escopo, você pode emparelhar facilmente um `@result()` funcionar com um `runAfter`.

tooexecute uma ação *para cada* ação em um escopo que `Failed`, matriz de saudação do filtro de resultados tooactions que falharam, você pode emparelhar `@result()` com um  **[matriz de filtro](../connectors/connectors-native-query.md)**  ação e um  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  loop. Você pode levar a matriz de resultados filtrados hello e executar uma ação para cada falha usando Olá **ForEach** loop. Aqui está um exemplo, seguido por uma explicação detalhada, que envia uma solicitação HTTP POST com corpo de resposta de saudação de quaisquer ações que falharam no escopo de saudação `My_Scope`.

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

Aqui está um toodescribe de passo a passo detalhado, o que acontece:

1. resultado de saudação tooget de todas as ações no `My_Scope`, Olá **matriz de filtro** filtros de ação `@result('My_Scope')`.

2. Olá condição para **matriz de filtro** é qualquer `@result()` item com status igual muito`Failed`. Essa condição filtra a matriz Olá com todos os resultados de ação de `My_Scope` tooan matriz somente com resultados de ação de falha.

3. Executar um **para cada** ação Olá **matriz filtrados** saídas. Esta etapa executa uma ação *para cada* resultado de ação com falha que foi filtrado anteriormente.

    Se uma única ação no escopo de saudação falhou, Olá ações no hello `foreach` executar apenas uma vez. 
    Muitas ações com falha causam uma ação por falha.

4. Enviar um HTTP POST em Olá `foreach` corpo da resposta, do item ou `@item()['outputs']['body']`. Olá `@result()` forma item é Olá mesmo como Olá `@actions()` forma e pode ser analisado Olá mesmo modo.

5. Incluem dois cabeçalhos personalizados com o nome de ação que falhou Olá `@item()['name']` e Olá falha cliente ID de rastreamento `@item()['clientTrackingId']`.

Para referência, aqui está um exemplo de um único `@result()` item, mostrando Olá `name`, `body`, e `clientTrackingId` propriedades que são analisadas no exemplo anterior de saudação. Fora de um `foreach`, `@result()` retorna uma matriz desses objetos.

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

padrões de tratamento de exceção diferente de tooperform, você pode usar expressões Olá mostradas anteriormente. Você pode escolher uma única ação fora de escopo de saudação que aceita Olá toda filtrado matriz de falhas de tratamento de exceção de tooexecute e remover Olá `foreach`. Você também pode incluir outras propriedades úteis do hello `@result()` resposta mostrada anteriormente.

## <a name="azure-diagnostics-and-telemetry"></a>Diagnósticos do Azure e telemetria

Hello padrões anteriores são erros de toohandle excelente maneira e exceções dentro de uma execução, mas você também pode identificar e responder tooerrors independente da saudação execute em si. 
[Diagnóstico do Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fornece uma maneira simples de toosend todas as conta de armazenamento do Azure tooan de fluxo de trabalho de eventos (incluindo todos os status de execução e ação) ou um Hub de eventos do Azure. tooevaluate executar status, você pode monitorar logs hello e métricas ou publicá-los em qualquer ferramenta de monitoramento que você preferir. Uma opção de potencial é toostream todos os eventos de saudação por meio do Hub de eventos do Azure em [do Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). No Stream Analytics, você pode escrever consultas ao vivo fora de qualquer anomalias, médias ou falhas de saudação logs de diagnóstico. Análise de fluxo pode facilmente produzir tooother fontes de dados como filas, tópicos, SQL, o banco de dados do Azure Cosmos e Power BI.

## <a name="next-steps"></a>Próximas etapas

* [Veja como um cliente compila o tratamento de erros com Aplicativos Lógicos do Azure](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Encontrar mais exemplos e cenários dos Aplicativos Lógicos](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Saiba como toocreate automatizado implantações de aplicativos lógicos](../logic-apps/logic-apps-create-deploy-template.md)
* [Compilar e implantar aplicativos lógicos no Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
