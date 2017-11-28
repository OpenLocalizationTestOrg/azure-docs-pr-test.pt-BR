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
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="9ac55-104">Gatilho de temporizador do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ac55-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="9ac55-105">Este artigo explica como tooconfigure e o código de timer dispara em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac55-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="9ac55-106">O Azure Functions tem uma associação de gatilho de timer que permite executar o código de função com base em um agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="9ac55-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="9ac55-107">gatilho de timer Olá dá suporte a várias instâncias em expansão. Uma única instância de uma função específica de timer é executada em todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="9ac55-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="9ac55-108">Gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="9ac55-108">Timer trigger</span></span>
<span data-ttu-id="9ac55-109">função de tooa de gatilho de timer Hello usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="9ac55-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="9ac55-110">Olá valor `schedule` é um [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que inclua esses seis campos:</span><span class="sxs-lookup"><span data-stu-id="9ac55-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="9ac55-111">Muitas das expressões de cron Olá encontrar online omitir Olá `{second}` campo.</span><span class="sxs-lookup"><span data-stu-id="9ac55-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="9ac55-112">Se você copiar de um deles, você precisa tooadjust para Olá extra `{second}` campo.</span><span class="sxs-lookup"><span data-stu-id="9ac55-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="9ac55-113">Para obter exemplos específicos, consulte [Agendar exemplos](#examples) abaixo.</span><span class="sxs-lookup"><span data-stu-id="9ac55-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="9ac55-114">saudação padrão fuso horário usado com expressões de CRON Olá é Tempo Universal Coordenado (UTC).</span><span class="sxs-lookup"><span data-stu-id="9ac55-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="9ac55-115">toohave expressão CRON com base em outro fuso horário, criar uma nova configuração de aplicativo para seu aplicativo de função chamada `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="9ac55-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="9ac55-116">Nome do conjunto Olá valor toohello de saudação desejado fuso horário conforme Olá [índice de fuso horário do Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ac55-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="9ac55-117">Por exemplo, a *Hora padrão da costa leste dos EUA* é UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="9ac55-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="9ac55-118">toohave seu timer gatilho acionado em 10:00 AM EST diariamente, use Olá expressão CRON que contas para o fuso horário UTC a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac55-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="9ac55-119">Como alternativa, você pode adicionar uma nova configuração de aplicativo para seu aplicativo de função chamado `WEBSITE_TIME_ZONE` e defina o valor de saudação muito**horário padrão Oriental**.</span><span class="sxs-lookup"><span data-stu-id="9ac55-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="9ac55-120">Em seguida, Olá CRON expressão a seguir pode ser usado para 10:00 AM EST:</span><span class="sxs-lookup"><span data-stu-id="9ac55-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="9ac55-121">Exemplos de agendamento</span><span class="sxs-lookup"><span data-stu-id="9ac55-121">Schedule examples</span></span>
<span data-ttu-id="9ac55-122">Aqui estão alguns exemplos de expressões de CRON, você pode usar para Olá `schedule` propriedade.</span><span class="sxs-lookup"><span data-stu-id="9ac55-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="9ac55-123">tootrigger uma vez a cada cinco minutos:</span><span class="sxs-lookup"><span data-stu-id="9ac55-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="9ac55-124">tootrigger uma vez na parte superior de saudação de cada hora:</span><span class="sxs-lookup"><span data-stu-id="9ac55-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="9ac55-125">tootrigger uma vez a cada duas horas:</span><span class="sxs-lookup"><span data-stu-id="9ac55-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="9ac55-126">tootrigger uma vez a cada hora de too5 9: 00 PM:</span><span class="sxs-lookup"><span data-stu-id="9ac55-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="9ac55-127">tootrigger às 9:30:00 diariamente:</span><span class="sxs-lookup"><span data-stu-id="9ac55-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="9ac55-128">tootrigger às 9:30:00 todo dia:</span><span class="sxs-lookup"><span data-stu-id="9ac55-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="9ac55-129">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="9ac55-129">Trigger usage</span></span>
<span data-ttu-id="9ac55-130">Quando uma função de gatilho de timer é invocada, Olá [objeto temporizador](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) é passado para a função hello.</span><span class="sxs-lookup"><span data-stu-id="9ac55-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="9ac55-131">Olá JSON a seguir é uma representação de exemplo do objeto de timer de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac55-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="9ac55-132">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="9ac55-132">Trigger sample</span></span>
<span data-ttu-id="9ac55-133">Suponha que você tenha Olá seguindo gatilho de timer no hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="9ac55-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="9ac55-134">Consulte exemplo específico do idioma hello que lê o temporizador de saudação toosee de objeto se ele está atrasado.</span><span class="sxs-lookup"><span data-stu-id="9ac55-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="9ac55-135">C#</span><span class="sxs-lookup"><span data-stu-id="9ac55-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="9ac55-136">F#</span><span class="sxs-lookup"><span data-stu-id="9ac55-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="9ac55-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="9ac55-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="9ac55-138">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="9ac55-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="9ac55-139">Exemplo de gatilho em F#</span><span class="sxs-lookup"><span data-stu-id="9ac55-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="9ac55-140">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="9ac55-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="9ac55-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ac55-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

