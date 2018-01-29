---
title: "Encadeamento de funções nas Funções Duráveis – Azure"
description: "Saiba como executar um exemplo de Funções Duráveis que executa uma sequência de funções."
services: functions
author: cgillum
manager: cfowler
editor: 
tags: 
keywords: 
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 9ba1cdc5c72e04802d29794fa6cb40a29cc1d353
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="function-chaining-in-durable-functions---hello-sequence-sample"></a>Encadeamento de funções nas Funções Duráveis – Exemplo se sequência Hello

Encadeamento de funções é o padrão de executar uma sequência de funções em uma ordem específica. Frequentemente, a saída de uma função precisa ser aplicada à entrada de outra função. Este artigo descreve um exemplo que usa as [Funções Duráveis](durable-functions-overview.md) para implementar o encadeamento de funções.

## <a name="prerequisites"></a>Pré-requisitos

* Siga as instruções em [Instalar Funções Duráveis](durable-functions-install.md) para configurar o exemplo.

## <a name="the-functions"></a>As funções

Este artigo explica as seguintes funções no aplicativo de exemplo:

* `E1_HelloSequence`: uma função de orquestrador que chama `E1_SayHello` várias vezes em uma sequência. Ela armazena as saídas das chamadas `E1_SayHello` e registra os resultados.
* `E1_SayHello`: uma função de atividade que precede uma cadeia de caracteres com "Hello".

As seções a seguir explicam a configuração e o código que são usados para desenvolvimento no portal do Azure. O código para desenvolvimento no Visual Studio é exibido no final do artigo.
 
## <a name="functionjson-file"></a>Arquivo function.json

Se você usa o Visual Studio Code ou o portal do Azure para desenvolvimento, este é o conteúdo do arquivo *function.json* para a função de orquestrador. A maioria dos arquivos *function.json* do orquestrador são quase exatamente iguais a esse.

[!code-json[Main](~/samples-durable-functions/samples/csx/E1_HelloSequence/function.json)]

O importante é o tipo de associação de `orchestrationTrigger`. Todas as funções de orquestrador devem usar esse tipo de gatilho.

> [!WARNING]
> Para obedecer a regra de "não fazer E/S" das funções de orquestrador, não use nenhuma associação de entrada ou saída ao usar a associação de gatilho `orchestrationTrigger`.  Se outras associações de entrada ou de saída forem necessárias, elas deverão ser usadas no contexto das funções `activityTrigger`, que são chamadas pelo orquestrador.

## <a name="c-script-visual-studio-code-and-azure-portal-sample-code"></a>Script C# (código de exemplo do Visual Studio Code e do portal do Azure) 

Este é o código-fonte:

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E1_HelloSequence/run.csx)]

Todas as funções de orquestração em C# devem ter um parâmetro do tipo `DurableOrchestrationContext`, que existe no assembly `Microsoft.Azure.WebJobs.Extensions.DurableTask`. Se você estiver usando o script C#, o assembly poderá ser referenciado usando a notação `#r`. Esse objeto de contexto permite chamar outras funções de *atividade* e passar parâmetros de entrada usando seu método [CallActivityAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_).

O código chama `E1_SayHello` três vezes seguidas com valores de parâmetros diferentes. O valor retornado de cada chamada é adicionado à lista `outputs`, que é retornada ao final da função.

O arquivo *function.json* da função de atividade `E1_SayHello` é semelhante ao de `E1_HelloSequence`, exceto por usar um tipo de associação `activityTrigger` em vez de um tipo de associação `orchestrationTrigger`.

[!code-json[Main](~/samples-durable-functions/samples/csx/E1_SayHello/function.json)]

> [!NOTE]
> Qualquer função chamada por uma função de orquestração deve usar a associação `activityTrigger`.

A implementação de `E1_SayHello` é uma operação de formatação de cadeia de caracteres relativamente simples.

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E1_SayHello/run.csx)]

Essa função tem um parâmetro do tipo [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html), que ela usa para obter a entrada que lhe foi passada pela chamada da função de orquestrador para [`CallActivityAsync<T>`](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_).

## <a name="run-the-sample"></a>Execute o exemplo

Para executar a orquestração de `E1_HelloSequence`, envie a solicitação HTTP POST o seguir.

```
POST http://{host}/orchestrators/E1_HelloSequence
```

Por exemplo, se você estiver executando a amostra em um aplicativo da função chamado "myfunctionapp", substitua "{host}" por "myfunctionapp.azurewebsites.net".

O resultado é uma resposta HTTP 202, como esta (resumido para fins de brevidade):

```
HTTP/1.1 202 Accepted
Content-Length: 719
Content-Type: application/json; charset=utf-8
Location: http://{host}/admin/extensions/DurableTaskExtension/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}

(...trimmed...)
```

Neste ponto, a orquestração é enfileirada e começa a ser executada imediatamente. A URL no cabeçalho `Location` pode ser usada para verificar o status da execução.

```
GET http://{host}/admin/extensions/DurableTaskExtension/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```

O resultado é o status da orquestração. Ela é executada e concluída rapidamente e você a verá com estado *Concluído*, com uma resposta semelhante esta (resumida para fins de brevidade):

```
HTTP/1.1 200 OK
Content-Length: 179
Content-Type: application/json; charset=utf-8

{"runtimeStatus":"Completed","input":null,"output":["Hello Tokyo!","Hello Seattle!","Hello London!"],"createdTime":"2017-06-29T05:24:57Z","lastUpdatedTime":"2017-06-29T05:24:59Z"}
```

Como você pode ver, o `runtimeStatus` da instância é *Concluído* e o `output` contém o resultado serializado em JSON da execução da função de orquestrador.

> [!NOTE]
> O ponto de extremidade HTTP POST que iniciou a função de orquestrador é implementado no aplicativo de exemplo como uma função de gatilho HTTP chamada "HttpStart". Você pode implementar uma lógica inicial semelhante a outros tipos de gatilho, como `queueTrigger`, `eventHubTrigger` ou `timerTrigger`.

Examine os logs de execução da função. O função `E1_HelloSequence` iniciou e foi concluída várias vezes devido ao comportamento de reprodução descrito na [visão geral](durable-functions-overview.md). Por outro lado, houve apenas três execuções de `E1_SayHello`, uma vez que as execuções dessas funções não são repetidas.

## <a name="visual-studio-sample-code"></a>Código de exemplo do Visual Studio

Esta é a orquestração como um único arquivo em C# em um projeto do Visual Studio:

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HelloSequence.cs)]

## <a name="next-steps"></a>Próximas etapas

Este exemplo demonstrou uma orquestração de encadeamento de função simples. O próximo exemplo mostra como implementar o padrão de fan-out/fan-in. 

> [!div class="nextstepaction"]
> [Executar o exemplo de fan-out/fan-in](durable-functions-cloud-backup.md)
