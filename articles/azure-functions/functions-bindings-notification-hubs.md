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
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="9dae9-104">Associação de saída do Hub de Notificação do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9dae9-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="9dae9-105">Este artigo explica como tooconfigure e o código de associações de Hub de notificação do Azure em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dae9-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="9dae9-106">Suas funções podem enviar notificações por push usando um Hub de Notificação do Azure configurado com poucas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="9dae9-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="9dae9-107">No entanto, Olá Hub de notificação do Azure deve ser configurado para Olá plataforma notificações de serviços (PNS) você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="9dae9-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="9dae9-108">Para obter mais informações sobre como configurar um Hub de notificação do Azure e desenvolver um aplicativo cliente que registrar tooreceive notificações, consulte [Introdução aos Hubs de notificação](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e clique em sua plataforma de cliente de destino no Olá Início.</span><span class="sxs-lookup"><span data-stu-id="9dae9-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="9dae9-109">notificações de saudação que enviar podem ser notificações nativas ou notificações de modelo.</span><span class="sxs-lookup"><span data-stu-id="9dae9-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="9dae9-110">Notificações nativas direcionar uma plataforma de notificação específico, conforme configurado no hello `platform` propriedade Olá associação de saída.</span><span class="sxs-lookup"><span data-stu-id="9dae9-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="9dae9-111">Uma notificação de modelo pode ser usado tootarget em várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="9dae9-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="9dae9-112">Propriedades de associação de saída do hub de notificação</span><span class="sxs-lookup"><span data-stu-id="9dae9-112">Notification hub output binding properties</span></span>
<span data-ttu-id="9dae9-113">arquivo de function.json Olá fornece Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="9dae9-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="9dae9-114">`name`: Nome variável usada no código de função para mensagem de saudação do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="9dae9-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="9dae9-115">`type`: deve ser definido muito*"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="9dae9-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="9dae9-116">`tagExpression`: Expressões de marca permitem toospecify que notificações entregues tooa conjunto de dispositivos que se inscreveram notificações tooreceive que correspondem à expressão Olá marca.</span><span class="sxs-lookup"><span data-stu-id="9dae9-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="9dae9-117">Para saber mais, veja [Expressões de marca e de roteamento](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="9dae9-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="9dae9-118">`hubName`: Nome do recurso do hub de notificação Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dae9-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="9dae9-119">`connection`: Essa cadeia de caracteres de conexão deve ser um **configuração de aplicativo** cadeia de caracteres de conexão definida toohello *DefaultFullSharedAccessSignature* valor para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="9dae9-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="9dae9-120">`direction`: deve ser definido muito*"out"*.</span><span class="sxs-lookup"><span data-stu-id="9dae9-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="9dae9-121">`platform`: propriedade de plataforma Olá indica a plataforma de notificação de saudação destinos de sua notificação.</span><span class="sxs-lookup"><span data-stu-id="9dae9-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="9dae9-122">Deve ser um Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="9dae9-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="9dae9-123">Por padrão, se propriedade de plataforma Olá for omitida da saída de hello associação, notificações de modelo podem ser usado tootarget qualquer plataforma configurada no hello Hub de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dae9-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="9dae9-124">Para obter mais informações sobre como usar modelos em geral toosend entre as notificações de plataforma com um Hub de notificação do Azure, consulte [modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="9dae9-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="9dae9-125">`apns` : Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="9dae9-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="9dae9-126">Para obter mais informações sobre como configurar o hub de notificação Olá para o APNS e recebimento da notificação de saudação em um aplicativo cliente, consulte [tooiOS de notificações do envio por push com Hubs de notificação do Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="9dae9-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="9dae9-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="9dae9-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="9dae9-128">Para obter mais informações sobre como configurar o hub de notificação Olá para ADM e recebimento da notificação de saudação em um aplicativo de Kindle, consulte [Introdução aos Hubs de notificação para Kindle aplicativos](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="9dae9-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="9dae9-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="9dae9-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="9dae9-130">Firebase Cloud Messaging, que é a nova versão de saudação do GCM, também é suportado.</span><span class="sxs-lookup"><span data-stu-id="9dae9-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="9dae9-131">Para obter mais informações sobre como configurar o hub de notificação Olá para GCM/FCM e recebimento da notificação de saudação em um aplicativo cliente do Android, consulte [tooAndroid de notificações do envio por push com Hubs de notificação do Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="9dae9-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="9dae9-132">`wns` : [Serviços de Notificação por Push do Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) visando plataformas Windows.</span><span class="sxs-lookup"><span data-stu-id="9dae9-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="9dae9-133">Também há suporte para Windows Phone 8.1 e posterior pelo WNS.</span><span class="sxs-lookup"><span data-stu-id="9dae9-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="9dae9-134">Para obter mais informações sobre como configurar o hub de notificação Olá para o WNS e recebimento da notificação de saudação em um aplicativo do Windows UWP (plataforma Universal), consulte [Introdução à notificação de Hubs para aplicativos universais do Windows plataforma](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="9dae9-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="9dae9-135">`mpns` : [Serviço de Notificação por Push da Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dae9-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="9dae9-136">Essa plataforma dá suporte a plataformas mais antigas do Windows Phone e Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="9dae9-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="9dae9-137">Para obter mais informações sobre como configurar o hub de notificação de saudação do MPNS e recebimento da notificação de saudação em um aplicativo do Windows Phone, consulte [notificações do envio por push com Hubs de notificação do Azure no Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="9dae9-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="9dae9-138">function.json de exemplo:</span><span class="sxs-lookup"><span data-stu-id="9dae9-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="9dae9-139">Configuração da cadeia de conexão do hub de notificação</span><span class="sxs-lookup"><span data-stu-id="9dae9-139">Notification hub connection string setup</span></span>
<span data-ttu-id="9dae9-140">associação de saída toouse um hub de notificação, você deve configurar a cadeia de caracteres de conexão de saudação de hub Olá.</span><span class="sxs-lookup"><span data-stu-id="9dae9-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="9dae9-141">Isso pode ser feito em Olá *integrar* guia selecionando seu hub de notificação ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="9dae9-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="9dae9-142">Você também pode adicionar manualmente uma cadeia de caracteres de conexão para um hub existente adicionando uma cadeia de caracteres de conexão para Olá *DefaultFullSharedAccessSignature* tooyour hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="9dae9-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="9dae9-143">Essa cadeia de caracteres de conexão fornece o acesso de função mensagens de notificação toosend permissão.</span><span class="sxs-lookup"><span data-stu-id="9dae9-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="9dae9-144">Olá *DefaultFullSharedAccessSignature* valor de cadeia de caracteres de conexão pode ser acessado de saudação **chaves** botão na folha principal de saudação do recurso de hub de notificação no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dae9-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="9dae9-145">toomanually adicionar uma cadeia de caracteres de conexão para o hub, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9dae9-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="9dae9-146">Em Olá **função aplicativo** folha de saudação portal do Azure, clique em **configurações de função do aplicativo > Ir configurações do serviço tooApp**.</span><span class="sxs-lookup"><span data-stu-id="9dae9-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="9dae9-147">Em Olá **configurações** folha, clique em **configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="9dae9-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="9dae9-148">Role para baixo toohello **configurações do aplicativo** seção e adicione uma entrada nomeada de *DefaultFullSharedAccessSignature* valor para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="9dae9-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="9dae9-149">Fazer referência a seu aplicativo definindo o nome de cadeia de caracteres em Olá associações de saída.</span><span class="sxs-lookup"><span data-stu-id="9dae9-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="9dae9-150">Semelhante muito**MyHubConnectionString** usado no exemplo hello acima.</span><span class="sxs-lookup"><span data-stu-id="9dae9-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="9dae9-151">Notificações nativas do APNS com gatilhos de fila do C#</span><span class="sxs-lookup"><span data-stu-id="9dae9-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="9dae9-152">Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação de APNS nativo.</span><span class="sxs-lookup"><span data-stu-id="9dae9-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="9dae9-153">Notificações nativas do GCM com gatilhos de fila do C#</span><span class="sxs-lookup"><span data-stu-id="9dae9-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="9dae9-154">Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação GCM nativo.</span><span class="sxs-lookup"><span data-stu-id="9dae9-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="9dae9-155">Notificações nativas do WNS com gatilhos de fila do C#</span><span class="sxs-lookup"><span data-stu-id="9dae9-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="9dae9-156">Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend um WNS nativo notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="9dae9-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

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

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="9dae9-157">Exemplo de modelo para gatilhos de temporizador do Node.js</span><span class="sxs-lookup"><span data-stu-id="9dae9-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="9dae9-158">Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="9dae9-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="9dae9-159">Exemplo de modelo para gatilhos de temporizador do F#</span><span class="sxs-lookup"><span data-stu-id="9dae9-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="9dae9-160">Este exemplo envia uma notificação para um [registro de modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="9dae9-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="9dae9-161">Exemplo de modelo usando um parâmetro de saída</span><span class="sxs-lookup"><span data-stu-id="9dae9-161">Template example using an out parameter</span></span>
<span data-ttu-id="9dae9-162">Este exemplo envia uma notificação um [registro do modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém um `message` espaço reservado no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dae9-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="9dae9-163">Exemplo de modelo com a função assíncrona</span><span class="sxs-lookup"><span data-stu-id="9dae9-163">Template example with asynchronous function</span></span>
<span data-ttu-id="9dae9-164">Se você estiver usando o código assíncrono, os parâmetros de saída não serão permitidos.</span><span class="sxs-lookup"><span data-stu-id="9dae9-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="9dae9-165">Nesse caso use `IAsyncCollector` tooreturn a notificação de modelo.</span><span class="sxs-lookup"><span data-stu-id="9dae9-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="9dae9-166">Olá código a seguir é um exemplo de assíncrono de código de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="9dae9-166">hello following code is an asynchronous example of hello code above.</span></span> 

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

## <a name="template-example-using-json"></a><span data-ttu-id="9dae9-167">Exemplo de modelo usando JSON</span><span class="sxs-lookup"><span data-stu-id="9dae9-167">Template example using JSON</span></span>
<span data-ttu-id="9dae9-168">Este exemplo envia uma notificação um [registro do modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contém um `message` espaço reservado no modelo de saudação usando uma cadeia de caracteres JSON válida.</span><span class="sxs-lookup"><span data-stu-id="9dae9-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="9dae9-169">Exemplo de modelo usando tipos de biblioteca de Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="9dae9-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="9dae9-170">Este exemplo mostra como toouse tipos definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="9dae9-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="9dae9-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dae9-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

