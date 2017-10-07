---
title: "gatilho de timer de funções aaaAzure | Microsoft Docs"
description: "Entenda como toouse timer dispara em funções do Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a>Gatilho de temporizador do Azure Functions

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e o código de timer dispara em funções do Azure. O Azure Functions tem uma associação de gatilho de timer que permite executar o código de função com base em um agendamento definido. 

gatilho de timer Olá dá suporte a várias instâncias em expansão. Uma única instância de uma função específica de timer é executada em todas as instâncias.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Gatilho de temporizador
função de tooa de gatilho de timer Hello usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

Olá valor `schedule` é um [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que inclua esses seis campos: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Muitas das expressões de cron Olá encontrar online omitir Olá `{second}` campo. Se você copiar de um deles, você precisa tooadjust para Olá extra `{second}` campo. Para obter exemplos específicos, consulte [Agendar exemplos](#examples) abaixo.

saudação padrão fuso horário usado com expressões de CRON Olá é Tempo Universal Coordenado (UTC). toohave expressão CRON com base em outro fuso horário, criar uma nova configuração de aplicativo para seu aplicativo de função chamada `WEBSITE_TIME_ZONE`. Nome do conjunto Olá valor toohello de saudação desejado fuso horário conforme Olá [índice de fuso horário do Microsoft](https://msdn.microsoft.com/library/ms912391.aspx). 

Por exemplo, a *Hora padrão da costa leste dos EUA* é UTC-05:00. toohave seu timer gatilho acionado em 10:00 AM EST diariamente, use Olá expressão CRON que contas para o fuso horário UTC a seguir:

```json
"schedule": "0 0 15 * * *",
``` 

Como alternativa, você pode adicionar uma nova configuração de aplicativo para seu aplicativo de função chamado `WEBSITE_TIME_ZONE` e defina o valor de saudação muito**horário padrão Oriental**.  Em seguida, Olá CRON expressão a seguir pode ser usado para 10:00 AM EST: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Exemplos de agendamento
Aqui estão alguns exemplos de expressões de CRON, você pode usar para Olá `schedule` propriedade. 

tootrigger uma vez a cada cinco minutos:

```json
"schedule": "0 */5 * * * *"
```

tootrigger uma vez na parte superior de saudação de cada hora:

```json
"schedule": "0 0 * * * *",
```

tootrigger uma vez a cada duas horas:

```json
"schedule": "0 0 */2 * * *",
```

tootrigger uma vez a cada hora de too5 9: 00 PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger às 9:30:00 diariamente:

```json
"schedule": "0 30 9 * * *",
```

tootrigger às 9:30:00 todo dia:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Uso de gatilho
Quando uma função de gatilho de timer é invocada, Olá [objeto temporizador](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) é passado para a função hello. Olá JSON a seguir é uma representação de exemplo do objeto de timer de saudação. 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a>Exemplo de gatilho
Suponha que você tenha Olá seguindo gatilho de timer no hello `bindings` matriz de function.json:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Consulte exemplo específico do idioma hello que lê o temporizador de saudação toosee de objeto se ele está atrasado.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemplo de gatilho em C# #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Exemplo de gatilho em F# #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemplo de gatilho em Node.js
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

