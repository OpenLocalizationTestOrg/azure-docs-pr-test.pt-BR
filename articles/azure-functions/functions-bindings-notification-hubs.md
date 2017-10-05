---
title: "Associação do Hub de Notificação do Azure Functions | Microsoft Docs"
description: "Entenda como usar a associação de Hub de Notificação do Azure no Azure Functions."
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
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="70d4f-104">Associação de saída do Hub de Notificação do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="70d4f-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="70d4f-105">Este artigo explica como configurar e codificar associações do Hub de Notificação no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="70d4f-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="70d4f-106">Suas funções podem enviar notificações por push usando um Hub de Notificação do Azure configurado com poucas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="70d4f-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="70d4f-107">No entanto, o Hub de Notificação do Azure deve estar configurado para os PNS (Serviços de Notificações de Plataforma) que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="70d4f-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="70d4f-108">Para saber mais sobre a configuração de um Hub de Notificação do Azure e sobre o desenvolvimento de aplicativos cliente que se registram para receber notificações, consulte [Introdução aos Hubs de Notificação](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e clique em sua plataforma de cliente de destino na parte superior.</span><span class="sxs-lookup"><span data-stu-id="70d4f-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="70d4f-109">As notificações enviadas podem ser notificações nativas ou notificações de modelo.</span><span class="sxs-lookup"><span data-stu-id="70d4f-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="70d4f-110">Notificações nativas são destinadas a uma plataforma específica de notificação, conforme configurado na propriedade `platform` da associação de saída.</span><span class="sxs-lookup"><span data-stu-id="70d4f-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="70d4f-111">Uma notificação de modelo pode ser usada para ter como destino várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="70d4f-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="70d4f-112">Propriedades de associação de saída do hub de notificação</span><span class="sxs-lookup"><span data-stu-id="70d4f-112">Notification hub output binding properties</span></span>
<span data-ttu-id="70d4f-113">O arquivo function.json fornece as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="70d4f-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="70d4f-114">`name` : nome da variável usada no código de função para a mensagem do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="70d4f-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="70d4f-115">`type` : deve ser definido como *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="70d4f-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="70d4f-116">`tagExpression` : as expressões de marca permitem que você especifique que as notificações sejam entregues a um conjunto de dispositivos que se registraram para receber notificações que correspondem à expressão de marca.</span><span class="sxs-lookup"><span data-stu-id="70d4f-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="70d4f-117">Para saber mais, veja [Expressões de marca e de roteamento](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="70d4f-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="70d4f-118">`hubName` : nome do recurso de hub de notificação no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70d4f-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="70d4f-119">`connection` : essa cadeia de conexão deve ser uma cadeia de conexão de **Configuração de Aplicativo** definida com o valor *DefaultFullSharedAccessSignature* para seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="70d4f-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="70d4f-120">`direction` : deve ser definido como *out*.</span><span class="sxs-lookup"><span data-stu-id="70d4f-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="70d4f-121">`platform` : a propriedade da plataforma indica a plataforma de notificação à qual sua notificação se destina.</span><span class="sxs-lookup"><span data-stu-id="70d4f-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="70d4f-122">Deve ser um dos seguintes valores: </span><span class="sxs-lookup"><span data-stu-id="70d4f-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="70d4f-123">Por padrão, se a propriedade da plataforma é omitida da associação de saída, as notificações de modelo podem ser usadas para atingir qualquer plataforma configurada no Hub de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="70d4f-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="70d4f-124">Para obter mais informações sobre como usar modelos em geral para enviar várias notificações de plataforma com um Hub de Notificação do Azure, consulte [Modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="70d4f-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="70d4f-125">`apns` : Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="70d4f-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="70d4f-126">Para obter mais informações sobre como configurar o hub de notificação do APNS e receber a notificação em um aplicativo cliente, consulte [Enviar notificações por push para iOS com os Hubs de Notificação do Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="70d4f-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="70d4f-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="70d4f-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="70d4f-128">Para obter mais informações sobre como configurar o hub de notificação para ADM e receber a notificação de um aplicativo Kindle, consulte [Introdução aos Hubs de Notificação para aplicativos Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="70d4f-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="70d4f-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="70d4f-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="70d4f-130">Também há suporte para o Firebase Cloud Messaging, que é a nova versão do GCM.</span><span class="sxs-lookup"><span data-stu-id="70d4f-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="70d4f-131">Para obter mais informações sobre como configurar o hub de notificação para GCM/FCM e receber a notificação em um aplicativo de cliente Android, consulte [Enviar notificações por push para o Android com Hubs de Notificação do Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="70d4f-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="70d4f-132">`wns` : [Serviços de Notificação por Push do Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) visando plataformas Windows.</span><span class="sxs-lookup"><span data-stu-id="70d4f-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="70d4f-133">Também há suporte para Windows Phone 8.1 e posterior pelo WNS.</span><span class="sxs-lookup"><span data-stu-id="70d4f-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="70d4f-134">Para obter mais informações sobre como configurar o hub de notificação para WNS e receber a notificação de um aplicativo UWP (Plataforma Universal do Windows), consulte [Introdução aos Hubs de Notificação para aplicativos da Plataforma Universal do Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="70d4f-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="70d4f-135">`mpns` : [Serviço de Notificação por Push da Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="70d4f-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="70d4f-136">Essa plataforma dá suporte a plataformas mais antigas do Windows Phone e Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="70d4f-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="70d4f-137">Para obter mais informações sobre como configurar o hub de notificação para MPNS e receber a notificação em um aplicativo do Windows Phone, consulte [Enviar notificações de push com Hubs de Notificação do Azure no Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="70d4f-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="70d4f-138">function.json de exemplo:</span><span class="sxs-lookup"><span data-stu-id="70d4f-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="70d4f-139">Configuração da cadeia de conexão do hub de notificação</span><span class="sxs-lookup"><span data-stu-id="70d4f-139">Notification hub connection string setup</span></span>
<span data-ttu-id="70d4f-140">Para usar uma associação de saída de um hub de notificação, você deve configurar a cadeia de conexão para o hub.</span><span class="sxs-lookup"><span data-stu-id="70d4f-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="70d4f-141">Faça isso na guia *Integrar* selecionando seu hub de notificação ou criando um novo.</span><span class="sxs-lookup"><span data-stu-id="70d4f-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="70d4f-142">Você também pode adicionar manualmente uma cadeia de conexão a um hub existente adicionando uma cadeia de conexão à *DefaultFullSharedAccessSignature* para seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="70d4f-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="70d4f-143">Essa cadeia de conexão fornece sua permissão de acesso à função para enviar mensagens de notificação.</span><span class="sxs-lookup"><span data-stu-id="70d4f-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="70d4f-144">O valor da cadeia de conexão *DefaultFullSharedAccessSignature* pode ser acessado do botão **chaves** na folha principal do seu recurso de hub de notificação no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70d4f-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="70d4f-145">Para adicionar manualmente uma cadeia de conexão ao hub, use estas etapas:</span><span class="sxs-lookup"><span data-stu-id="70d4f-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="70d4f-146">Na folha **Aplicativo de funções** do portal do Azure, clique em **Configurações do Aplicativo de funções > Vá para as configurações do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="70d4f-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="70d4f-147">Na folha **Configurações**, clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="70d4f-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="70d4f-148">Role para baixo até a seção **Configurações do aplicativo** e adicione uma entrada nomeada para o valor *DefaultFullSharedAccessSignature* para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="70d4f-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="70d4f-149">Faça referência ao nome da sua cadeia de configurações do aplicativo nas associações de saída.</span><span class="sxs-lookup"><span data-stu-id="70d4f-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="70d4f-150">Semelhante à **MyHubConnectionString** usada no exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="70d4f-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="70d4f-151">Notificações nativas do APNS com gatilhos de fila do C#</span><span class="sxs-lookup"><span data-stu-id="70d4f-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="70d4f-152">Este exemplo mostra como usar tipos definidos na [Biblioteca de Hubs de Notificações do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) para enviar uma notificação nativa do APNS.</span><span class="sxs-lookup"><span data-stu-id="70d4f-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="70d4f-153">Notificações nativas do GCM com gatilhos de fila do C#</span><span class="sxs-lookup"><span data-stu-id="70d4f-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="70d4f-154">Este exemplo mostra como usar tipos definidos na [Biblioteca de Hubs de Notificações do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) para enviar uma notificação nativa do GCM.</span><span class="sxs-lookup"><span data-stu-id="70d4f-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="70d4f-155">Notificações nativas do WNS com gatilhos de fila do C#</span><span class="sxs-lookup"><span data-stu-id="70d4f-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="70d4f-156">Este exemplo mostra como usar tipos definidos na [Biblioteca de Hubs de Notificações do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) para enviar uma notificação nativa WNS do sistema.</span><span class="sxs-lookup"><span data-stu-id="70d4f-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="70d4f-157">Exemplo de modelo para gatilhos de temporizador do Node.js</span><span class="sxs-lookup"><span data-stu-id="70d4f-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="70d4f-158">Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="70d4f-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="70d4f-159">Exemplo de modelo para gatilhos de temporizador do F#</span><span class="sxs-lookup"><span data-stu-id="70d4f-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="70d4f-160">Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="70d4f-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="70d4f-161">Exemplo de modelo usando um parâmetro de saída</span><span class="sxs-lookup"><span data-stu-id="70d4f-161">Template example using an out parameter</span></span>
<span data-ttu-id="70d4f-162">Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém um espaço reservado `message` no modelo.</span><span class="sxs-lookup"><span data-stu-id="70d4f-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="70d4f-163">Exemplo de modelo com a função assíncrona</span><span class="sxs-lookup"><span data-stu-id="70d4f-163">Template example with asynchronous function</span></span>
<span data-ttu-id="70d4f-164">Se você estiver usando o código assíncrono, os parâmetros de saída não serão permitidos.</span><span class="sxs-lookup"><span data-stu-id="70d4f-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="70d4f-165">Nesse caso, use `IAsyncCollector` para retornar a notificação de modelo.</span><span class="sxs-lookup"><span data-stu-id="70d4f-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="70d4f-166">O código a seguir é um exemplo de código assíncrono acima.</span><span class="sxs-lookup"><span data-stu-id="70d4f-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="70d4f-167">Exemplo de modelo usando JSON</span><span class="sxs-lookup"><span data-stu-id="70d4f-167">Template example using JSON</span></span>
<span data-ttu-id="70d4f-168">Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém um espaço reservado `message` no modelo usando uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="70d4f-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="70d4f-169">Exemplo de modelo usando tipos de biblioteca de Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="70d4f-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="70d4f-170">Este exemplo mostra como usar tipos definidos na [Biblioteca de Hubs de Notificações do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="70d4f-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="70d4f-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70d4f-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

