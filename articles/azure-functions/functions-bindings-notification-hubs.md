---
title: "associação de Hub de notificação de funções aaaAzure | Microsoft Docs"
description: "Entender como toouse associação de Hub de notificação do Azure em funções do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Associação de saída do Hub de Notificação do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e o código de associações de Hub de notificação do Azure em funções do Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Suas funções podem enviar notificações por push usando um Hub de Notificação do Azure configurado com poucas linhas de código. No entanto, Olá Hub de notificação do Azure deve ser configurado para Olá plataforma notificações de serviços (PNS) você deseja toouse. Para obter mais informações sobre como configurar um Hub de notificação do Azure e desenvolver um aplicativo cliente que registrar tooreceive notificações, consulte [Introdução aos Hubs de notificação](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e clique em sua plataforma de cliente de destino no Olá Início.

notificações de saudação que enviar podem ser notificações nativas ou notificações de modelo. Notificações nativas direcionar uma plataforma de notificação específico, conforme configurado no hello `platform` propriedade Olá associação de saída. Uma notificação de modelo pode ser usado tootarget em várias plataformas.   

## <a name="notification-hub-output-binding-properties"></a>Propriedades de associação de saída do hub de notificação
arquivo de function.json Olá fornece Olá propriedades a seguir:

* `name`: Nome variável usada no código de função para mensagem de saudação do hub de notificação.
* `type`: deve ser definido muito*"notificationHub"*.
* `tagExpression`: Expressões de marca permitem toospecify que notificações entregues tooa conjunto de dispositivos que se inscreveram notificações tooreceive que correspondem à expressão Olá marca.  Para saber mais, veja [Expressões de marca e de roteamento](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nome do recurso do hub de notificação Olá no hello portal do Azure.
* `connection`: Essa cadeia de caracteres de conexão deve ser um **configuração de aplicativo** cadeia de caracteres de conexão definida toohello *DefaultFullSharedAccessSignature* valor para o hub de notificação.
* `direction`: deve ser definido muito*"out"*. 
* `platform`: propriedade de plataforma Olá indica a plataforma de notificação de saudação destinos de sua notificação. Deve ser um Olá valores a seguir:
  * Por padrão, se propriedade de plataforma Olá for omitida da saída de hello associação, notificações de modelo podem ser usado tootarget qualquer plataforma configurada no hello Hub de notificação do Azure. Para obter mais informações sobre como usar modelos em geral toosend entre as notificações de plataforma com um Hub de notificação do Azure, consulte [modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns` : Apple Push Notification Service. Para obter mais informações sobre como configurar o hub de notificação Olá para o APNS e recebimento da notificação de saudação em um aplicativo cliente, consulte [tooiOS de notificações do envio por push com Hubs de notificação do Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Para obter mais informações sobre como configurar o hub de notificação Olá para ADM e recebimento da notificação de saudação em um aplicativo de Kindle, consulte [Introdução aos Hubs de notificação para Kindle aplicativos](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Firebase Cloud Messaging, que é a nova versão de saudação do GCM, também é suportado. Para obter mais informações sobre como configurar o hub de notificação Olá para GCM/FCM e recebimento da notificação de saudação em um aplicativo cliente do Android, consulte [tooAndroid de notificações do envio por push com Hubs de notificação do Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns` : [Serviços de Notificação por Push do Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) visando plataformas Windows. Também há suporte para Windows Phone 8.1 e posterior pelo WNS. Para obter mais informações sobre como configurar o hub de notificação Olá para o WNS e recebimento da notificação de saudação em um aplicativo do Windows UWP (plataforma Universal), consulte [Introdução à notificação de Hubs para aplicativos universais do Windows plataforma](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns` : [Serviço de Notificação por Push da Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Essa plataforma dá suporte a plataformas mais antigas do Windows Phone e Windows Phone 8. Para obter mais informações sobre como configurar o hub de notificação de saudação do MPNS e recebimento da notificação de saudação em um aplicativo do Windows Phone, consulte [notificações do envio por push com Hubs de notificação do Azure no Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

function.json de exemplo:

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>Configuração da cadeia de conexão do hub de notificação
associação de saída toouse um hub de notificação, você deve configurar a cadeia de caracteres de conexão de saudação de hub Olá. Isso pode ser feito em Olá *integrar* guia selecionando seu hub de notificação ou criar um novo. 

Você também pode adicionar manualmente uma cadeia de caracteres de conexão para um hub existente adicionando uma cadeia de caracteres de conexão para Olá *DefaultFullSharedAccessSignature* tooyour hub de notificação. Essa cadeia de caracteres de conexão fornece o acesso de função mensagens de notificação toosend permissão. Olá *DefaultFullSharedAccessSignature* valor de cadeia de caracteres de conexão pode ser acessado de saudação **chaves** botão na folha principal de saudação do recurso de hub de notificação no hello portal do Azure. toomanually adicionar uma cadeia de caracteres de conexão para o hub, Olá use as etapas a seguir: 

1. Em Olá **função aplicativo** folha de saudação portal do Azure, clique em **configurações de função do aplicativo > Ir configurações do serviço tooApp**.
2. Em Olá **configurações** folha, clique em **configurações de aplicativo**.
3. Role para baixo toohello **configurações do aplicativo** seção e adicione uma entrada nomeada de *DefaultFullSharedAccessSignature* valor para o hub de notificação.
4. Fazer referência a seu aplicativo definindo o nome de cadeia de caracteres em Olá associações de saída. Semelhante muito**MyHubConnectionString** usado no exemplo hello acima.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Notificações nativas do APNS com gatilhos de fila do C#
Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação de APNS nativo. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Notificações nativas do GCM com gatilhos de fila do C#
Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação GCM nativo. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Notificações nativas do WNS com gatilhos de fila do C#
Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend um WNS nativo notificação do sistema. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Exemplo de modelo para gatilhos de temporizador do Node.js
Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém `location` e `message`.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>Exemplo de modelo para gatilhos de temporizador do F#
Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém `location` e `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Exemplo de modelo usando um parâmetro de saída
Este exemplo envia uma notificação um [registro do modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém um `message` espaço reservado no modelo de saudação.

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>Exemplo de modelo com a função assíncrona
Se você estiver usando o código assíncrono, os parâmetros de saída não serão permitidos. Nesse caso use `IAsyncCollector` tooreturn a notificação de modelo. Olá código a seguir é um exemplo de assíncrono de código de saudação acima. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>Exemplo de modelo usando JSON
Este exemplo envia uma notificação um [registro do modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém um `message` espaço reservado no modelo de saudação usando uma cadeia de caracteres JSON válida.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Exemplo de modelo usando tipos de biblioteca de Hubs de Notificação
Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

