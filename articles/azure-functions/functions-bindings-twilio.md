---
title: "associação de funções Twilio aaaAzure | Microsoft Docs"
description: "Entender como toouse Twilio associações com funções do Azure."
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
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>Enviar mensagens SMS das funções do Azure usando Olá Twilio associação de saída
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como as associações de Twilio tooconfigure e uso com funções do Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

As funções do Azure oferece suporte a tooenable de associações de saída Twilio mensagens de texto SMS funções toosend com algumas linhas de código e um [Twilio](https://www.twilio.com/) conta. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>saída de Twilio Function.JSON para Olá associação
arquivo de function.json Olá fornece Olá propriedades a seguir:

* `name`: Nome da variável usado no código de função para Olá mensagem de texto SMS Twilio.
* `type`: deve ser definido muito*"twilioSms"*.
* `accountSid`: Esse valor deve ser definido toohello nome de uma configuração de aplicativo que contém o Sid de conta do Twilio.
* `authToken`: Esse valor deve ser definido como toohello o nome de uma configuração de aplicativo que contém o token de autenticação do Twilio.
* `to`: Esse valor é definido o número de telefone de toohello Olá SMS texto é enviado para.
* `from`: Esse valor é definir o número de telefone de toohello texto SMS de saudação enviada.
* `direction`: deve ser definido muito*"out"*.
* `body`: Esse valor pode ser mensagem de texto usado toohard código Olá SMS se tooset dinamicamente na saudação de código não é necessário para sua função. 

function.json de exemplo:

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Exemplo de gatilho de fila C# com saída de associação do Twilio
#### <a name="synchronous"></a>Síncrono
Este código de exemplo síncrona para um gatilho de fila de armazenamento do Azure usa um fora parâmetro toosend um cliente de tooa de mensagem de texto que fez uma ordem.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a>Assíncrono
Esse código de exemplo assíncrona para um gatilho de fila de armazenamento do Azure envia um cliente de tooa de mensagem de texto que fez uma ordem.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Exemplo de gatilho de fila Node.js com saída de associação do Twilio
Este exemplo Node. js envia um cliente de tooa de mensagem de texto que fez uma ordem.

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

