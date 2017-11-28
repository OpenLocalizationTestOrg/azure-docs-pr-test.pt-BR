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
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="f06e5-103">Enviar notificações de plataforma cruzada toousers com Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="f06e5-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="f06e5-104">No tutorial anterior Olá [notificar os usuários com Hubs de notificação], você aprendeu como dispositivos de tooall notificações toopush registrado por um usuário autenticado específico.</span><span class="sxs-lookup"><span data-stu-id="f06e5-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="f06e5-105">Neste tutorial, várias solicitações foram toosend necessária uma plataforma de cliente tooeach suporte para notificação.</span><span class="sxs-lookup"><span data-stu-id="f06e5-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="f06e5-106">Notificação de Hubs dá suporte a modelos que permitem que você especifique como deseja que um dispositivo específico tooreceive notificações.</span><span class="sxs-lookup"><span data-stu-id="f06e5-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="f06e5-107">Isso simplifica o envio de notificações entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="f06e5-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="f06e5-108">Este tópico demonstra como tootake aproveitar toosend de modelos, em uma única solicitação, uma notificação de plataforma que se destina a todas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="f06e5-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="f06e5-109">Para obter informações detalhadas sobre modelos, confira [Visão geral de Hubs de Notificação do Azure][Templates].</span><span class="sxs-lookup"><span data-stu-id="f06e5-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f06e5-110">Projetos do Windows Phone 8.1 e versões anteriores não têm suporte usando o Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="f06e5-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="f06e5-111">Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="f06e5-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="f06e5-112">Hubs de notificação permite que um dispositivo tooregister vários modelos com hello mesma marca.</span><span class="sxs-lookup"><span data-stu-id="f06e5-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="f06e5-113">Nesse caso, uma mensagem de entrada direcionando que marca resulta em várias notificações entregues toohello dispositivo, um para cada modelo.</span><span class="sxs-lookup"><span data-stu-id="f06e5-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="f06e5-114">Isso permite que você toodisplay Olá a mesma mensagem em várias notificações visual, como ambos como uma notificação e como uma notificação do sistema em um aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="f06e5-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="f06e5-115">Concluir Olá notificações de etapas entre plataformas toosend usando modelos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f06e5-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="f06e5-116">No hello Gerenciador de soluções do Visual Studio, expanda Olá **controladores** pasta e arquivo de RegisterController.cs Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="f06e5-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="f06e5-117">Localize o bloco de saudação do código em Olá **colocar** método que cria um novo registro substituir Olá `switch` conteúdo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f06e5-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="f06e5-118">Esse código chama Olá método específico de plataforma toocreate um registro do modelo em vez de um registro nativo.</span><span class="sxs-lookup"><span data-stu-id="f06e5-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="f06e5-119">Os registros existentes não precisam ser modificados porque os registros de modelo derivam de registros nativos.</span><span class="sxs-lookup"><span data-stu-id="f06e5-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="f06e5-120">Em Olá **notificações** controlador, substituir Olá **sendNotification** método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f06e5-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="f06e5-121">Esse código envia uma notificação tooall plataformas em Olá mesmo tempo e sem ter que toospecify uma carga nativo.</span><span class="sxs-lookup"><span data-stu-id="f06e5-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="f06e5-122">Compilações de Hubs de notificação e entrega Olá dispositivo tooevery de carga corretas com hello fornecido *marca* valor, conforme especificado em modelos do hello registrado.</span><span class="sxs-lookup"><span data-stu-id="f06e5-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="f06e5-123">Publicar novamente seu projeto back-end do WebApi.</span><span class="sxs-lookup"><span data-stu-id="f06e5-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="f06e5-124">Execute novamente o aplicativo de cliente hello e verifique se o registro terá êxito.</span><span class="sxs-lookup"><span data-stu-id="f06e5-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="f06e5-125">(Opcional) Implantar Olá cliente aplicativo tooa segundo dispositivo, execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f06e5-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="f06e5-126">Observe que uma notificação é exibida em cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f06e5-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f06e5-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f06e5-127">Next Steps</span></span>
<span data-ttu-id="f06e5-128">Agora que você concluiu este tutorial, saiba mais sobre Hubs de Notificação e modelos nestes tópicos:</span><span class="sxs-lookup"><span data-stu-id="f06e5-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="f06e5-129">**[Usar Hubs de notificação toosend últimas notícias]**</span><span class="sxs-lookup"><span data-stu-id="f06e5-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="f06e5-130">Demonstra outro cenário para a utilização de modelos</span><span class="sxs-lookup"><span data-stu-id="f06e5-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="f06e5-131">**[Visão geral dos Hubs de Notificação][Templates]**</span><span class="sxs-lookup"><span data-stu-id="f06e5-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="f06e5-132">O tópico Visão Geral tem informações mais detalhadas sobre modelos.</span><span class="sxs-lookup"><span data-stu-id="f06e5-132">Overview topic has more detailed information on templates.</span></span>

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
