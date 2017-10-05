---
title: Gatilho de temporizador do Azure Functions | Microsoft Docs
description: Entenda como usar gatilhos de temporizador no Azure Functions.
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
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="e3c88-104">Gatilho de temporizador do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e3c88-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e3c88-105">Este artigo explica como configurar e codificar gatilhos de temporizador no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e3c88-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="e3c88-106">O Azure Functions tem uma associação de gatilho de timer que permite executar o código de função com base em um agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="e3c88-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="e3c88-107">O gatilho de timer dá suporte à expansão em várias instâncias. Uma única instância de uma função específica de timer é executada em todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="e3c88-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="e3c88-108">Gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="e3c88-108">Timer trigger</span></span>
<span data-ttu-id="e3c88-109">O gatilho de timer de uma função usa o seguinte objeto JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="e3c88-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="e3c88-110">O valor de `schedule` é uma [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que inclui estes seis campos:</span><span class="sxs-lookup"><span data-stu-id="e3c88-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="e3c88-111">Muitas das expressões cron encontradas online omitem o campo `{second}`.</span><span class="sxs-lookup"><span data-stu-id="e3c88-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="e3c88-112">Se você copiar de um deles, precisará ajustá-lo para o campo `{second}`.</span><span class="sxs-lookup"><span data-stu-id="e3c88-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="e3c88-113">Para obter exemplos específicos, consulte [Agendar exemplos](#examples) abaixo.</span><span class="sxs-lookup"><span data-stu-id="e3c88-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="e3c88-114">O fuso horário padrão usado com as expressões CRON é a Hora Universal Coordenada (UTC).</span><span class="sxs-lookup"><span data-stu-id="e3c88-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="e3c88-115">Para que a expressão CRON se baseie em outro fuso horário, crie uma nova configuração de aplicativo para o aplicativo de funções denominada `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="e3c88-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="e3c88-116">Defina o valor para o nome do fuso horário desejado, conforme mostrado no [Índice de fuso horário da Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3c88-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="e3c88-117">Por exemplo, a *Hora padrão da costa leste dos EUA* é UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="e3c88-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="e3c88-118">Para que o timer dispare às 10:00 AM EST diariamente, use a seguinte expressão CRON que considera o fuso horário UTC:</span><span class="sxs-lookup"><span data-stu-id="e3c88-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="e3c88-119">Como alternativa, você pode adicionar uma nova configuração de aplicativo para seu aplicativo de funções denominada `WEBSITE_TIME_ZONE` e definir o valor como **Horário padrão da costa leste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="e3c88-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="e3c88-120">Em seguida, a seguinte expressão CRON poderia ser usada para 10:00 EST:</span><span class="sxs-lookup"><span data-stu-id="e3c88-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="e3c88-121">Exemplos de agendamento</span><span class="sxs-lookup"><span data-stu-id="e3c88-121">Schedule examples</span></span>
<span data-ttu-id="e3c88-122">Aqui estão alguns exemplos de expressões CRON que você pode usar para a propriedade `schedule`.</span><span class="sxs-lookup"><span data-stu-id="e3c88-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="e3c88-123">Para disparar uma vez a cada cinco minutos:</span><span class="sxs-lookup"><span data-stu-id="e3c88-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="e3c88-124">Para disparar uma vez a cada hora:</span><span class="sxs-lookup"><span data-stu-id="e3c88-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="e3c88-125">Para disparar uma vez a cada duas horas:</span><span class="sxs-lookup"><span data-stu-id="e3c88-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="e3c88-126">Para disparar uma vez a cada hora das 9h às 17h:</span><span class="sxs-lookup"><span data-stu-id="e3c88-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="e3c88-127">Para disparar às 9h30 todos os dias:</span><span class="sxs-lookup"><span data-stu-id="e3c88-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="e3c88-128">Para disparar às 9h30 todos os dias da semana:</span><span class="sxs-lookup"><span data-stu-id="e3c88-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e3c88-129">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="e3c88-129">Trigger usage</span></span>
<span data-ttu-id="e3c88-130">Quando uma função de gatilho de timer é chamada, o [objeto timer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) é passado para a função.</span><span class="sxs-lookup"><span data-stu-id="e3c88-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="e3c88-131">O JSON a seguir é uma representação de exemplo do objeto timer.</span><span class="sxs-lookup"><span data-stu-id="e3c88-131">The following JSON is an example representation of the timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="e3c88-132">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="e3c88-132">Trigger sample</span></span>
<span data-ttu-id="e3c88-133">Suponha que você tenha o seguinte gatilho de timer na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="e3c88-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="e3c88-134">Consulte o exemplo específico da linguagem que lê o objeto de timer para ver se ele está atrasado.</span><span class="sxs-lookup"><span data-stu-id="e3c88-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="e3c88-135">C#</span><span class="sxs-lookup"><span data-stu-id="e3c88-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e3c88-136">F#</span><span class="sxs-lookup"><span data-stu-id="e3c88-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="e3c88-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="e3c88-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="e3c88-138">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="e3c88-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="e3c88-139">Exemplo de gatilho em F#</span><span class="sxs-lookup"><span data-stu-id="e3c88-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="e3c88-140">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="e3c88-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="e3c88-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3c88-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

