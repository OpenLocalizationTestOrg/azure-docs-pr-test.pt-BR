---
title: "aaaSend toousers de notificações de plataforma cruzada com Hubs de notificação (ASP.NET)"
description: "Saiba como toosend toouse de modelos de Hubs de notificação, em uma única solicitação, uma notificação de plataforma que se destina a todas as plataformas."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Enviar notificações de plataforma cruzada toousers com Hubs de notificação
No tutorial anterior Olá [notificar os usuários com Hubs de notificação], você aprendeu como dispositivos de tooall notificações toopush registrado por um usuário autenticado específico. Neste tutorial, várias solicitações foram toosend necessária uma plataforma de cliente tooeach suporte para notificação. Notificação de Hubs dá suporte a modelos que permitem que você especifique como deseja que um dispositivo específico tooreceive notificações. Isso simplifica o envio de notificações entre plataformas. Este tópico demonstra como tootake aproveitar toosend de modelos, em uma única solicitação, uma notificação de plataforma que se destina a todas as plataformas. Para obter informações detalhadas sobre modelos, confira [Visão geral de Hubs de Notificação do Azure][Templates].
> [!IMPORTANT]
> Projetos do Windows Phone 8.1 e versões anteriores não têm suporte usando o Visual Studio de 2017. Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Hubs de notificação permite que um dispositivo tooregister vários modelos com hello mesma marca. Nesse caso, uma mensagem de entrada direcionando que marca resulta em várias notificações entregues toohello dispositivo, um para cada modelo. Isso permite que você toodisplay Olá a mesma mensagem em várias notificações visual, como ambos como uma notificação e como uma notificação do sistema em um aplicativo da Windows Store.
> 
> 

Concluir Olá notificações de etapas entre plataformas toosend usando modelos a seguir:

1. No hello Gerenciador de soluções do Visual Studio, expanda Olá **controladores** pasta e arquivo de RegisterController.cs Olá aberto.
2. Localize o bloco de saudação do código em Olá **colocar** método que cria um novo registro substituir Olá `switch` conteúdo com hello código a seguir:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Esse código chama Olá método específico de plataforma toocreate um registro do modelo em vez de um registro nativo. Os registros existentes não precisam ser modificados porque os registros de modelo derivam de registros nativos.
3. Em Olá **notificações** controlador, substituir Olá **sendNotification** método com hello código a seguir:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Esse código envia uma notificação tooall plataformas em Olá mesmo tempo e sem ter que toospecify uma carga nativo. Compilações de Hubs de notificação e entrega Olá dispositivo tooevery de carga corretas com hello fornecido *marca* valor, conforme especificado em modelos do hello registrado.
4. Publicar novamente seu projeto back-end do WebApi.
5. Execute novamente o aplicativo de cliente hello e verifique se o registro terá êxito.
6. (Opcional) Implantar Olá cliente aplicativo tooa segundo dispositivo, execute o aplicativo hello.
   
    Observe que uma notificação é exibida em cada dispositivo.

## <a name="next-steps"></a>Próximas etapas
Agora que você concluiu este tutorial, saiba mais sobre Hubs de Notificação e modelos nestes tópicos:

* **[Usar Hubs de notificação toosend últimas notícias]** <br/>Demonstra outro cenário para a utilização de modelos
* **[Visão geral dos Hubs de Notificação][Templates]**<br/>O tópico Visão Geral tem informações mais detalhadas sobre modelos.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Usar Hubs de notificação toosend últimas notícias]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[notificar os usuários com Hubs de notificação]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
