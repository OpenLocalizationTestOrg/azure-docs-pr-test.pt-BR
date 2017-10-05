---
title: "Associação Twilio e Azure Functions | Microsoft Docs"
description: "Entenda como usar associações Twilio com Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 870e47ec7f8ce41ee4acadc7b8ed59298958acbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="send-sms-messages-from-azure-functions-using-the-twilio-output-binding"></a><span data-ttu-id="09bb3-104">Enviar mensagens SMS do Azure Functions usando associações de saída do Twilio</span><span class="sxs-lookup"><span data-stu-id="09bb3-104">Send SMS messages from Azure Functions using the Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="09bb3-105">Este artigo explica como configurar e usar associações Twilio com o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="09bb3-105">This article explains how to configure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="09bb3-106">O Azure Functions dá suporte às saídas de associações do Twilio para habilitar funções para envio de mensagens de texto SMS com algumas linhas de código e uma conta [Twilio](https://www.twilio.com/).</span><span class="sxs-lookup"><span data-stu-id="09bb3-106">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-the-twilio-output-binding"></a><span data-ttu-id="09bb3-107">function.json para a associação de saída do Twilio</span><span class="sxs-lookup"><span data-stu-id="09bb3-107">function.json for the Twilio output binding</span></span>
<span data-ttu-id="09bb3-108">O arquivo function.json fornece as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="09bb3-108">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="09bb3-109">`name`: nome da variável usada no código de função, para a mensagem de texto SMS do Twilio.</span><span class="sxs-lookup"><span data-stu-id="09bb3-109">`name` : Variable name used in function code for the Twilio SMS text message.</span></span>
* <span data-ttu-id="09bb3-110">`type`: deve ser definido como *"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="09bb3-110">`type` : must be set to *"twilioSms"*.</span></span>
* <span data-ttu-id="09bb3-111">`accountSid`: esse valor deve ser definido como o nome de uma Configuração de aplicativo que contém a SID da sua conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="09bb3-111">`accountSid` : This value must be set to the name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="09bb3-112">`authToken`: esse valor deve ser definido como o nome de uma Configuração de aplicativo que contém seu token de autenticação do Twilio.</span><span class="sxs-lookup"><span data-stu-id="09bb3-112">`authToken` : This value must be set to the name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="09bb3-113">`to`: esse valor é definido como o número de telefone para o qual será enviada a mensagem de texto SMS.</span><span class="sxs-lookup"><span data-stu-id="09bb3-113">`to` : This value is set to the phone number that the SMS text is sent to.</span></span>
* <span data-ttu-id="09bb3-114">`from`: esse valor é definido como o número de telefone com o qual será enviada a mensagem de texto SMS.</span><span class="sxs-lookup"><span data-stu-id="09bb3-114">`from` : This value is set to the phone number that the SMS text is sent from.</span></span>
* <span data-ttu-id="09bb3-115">`direction` : deve ser definido como *out*.</span><span class="sxs-lookup"><span data-stu-id="09bb3-115">`direction` : must be set to *"out"*.</span></span>
* <span data-ttu-id="09bb3-116">`body`: esse valor pode ser usado para fixar a mensagem de texto SMS no código se você não precisa defini-la dinamicamente no código de sua função.</span><span class="sxs-lookup"><span data-stu-id="09bb3-116">`body` : This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> 

<span data-ttu-id="09bb3-117">function.json de exemplo:</span><span class="sxs-lookup"><span data-stu-id="09bb3-117">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="09bb3-118">Exemplo de gatilho de fila C# com saída de associação do Twilio</span><span class="sxs-lookup"><span data-stu-id="09bb3-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="09bb3-119">Síncrono</span><span class="sxs-lookup"><span data-stu-id="09bb3-119">Synchronous</span></span>
<span data-ttu-id="09bb3-120">Esse código de exemplo síncrono, para um gatilho de fila de armazenamento do Azure, usa um parâmetro de saída para enviar uma mensagem de texto para um cliente que fez um pedido.</span><span class="sxs-lookup"><span data-stu-id="09bb3-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter to send a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="09bb3-121">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="09bb3-121">Asynchronous</span></span>
<span data-ttu-id="09bb3-122">Esse código de exemplo assíncrono, para um gatilho de fila de armazenamento do Azure, envia uma mensagem de texto para um cliente que fez um pedido.</span><span class="sxs-lookup"><span data-stu-id="09bb3-122">This asynchronous example code for an Azure Storage queue trigger sends a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="09bb3-123">Exemplo de gatilho de fila Node.js com saída de associação do Twilio</span><span class="sxs-lookup"><span data-stu-id="09bb3-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="09bb3-124">Este exemplo do Node.js envia uma mensagem de texto para um cliente que fez um pedido.</span><span class="sxs-lookup"><span data-stu-id="09bb3-124">This Node.js example sends a text message to a customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="09bb3-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09bb3-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

