---
title: "aaaNotification Hubs localizado últimas notícias Tutorial para iOS"
description: "Saiba como toouse toosend de Hubs de notificação de barramento de serviço do Azure localizado notificações das últimas notícias (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="4aba1-103">Usar Hubs de notificação toosend localizado recentes notícias tooiOS dispositivos</span><span class="sxs-lookup"><span data-stu-id="4aba1-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4aba1-104">C# da Windows Store</span><span class="sxs-lookup"><span data-stu-id="4aba1-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="4aba1-105">iOS</span><span class="sxs-lookup"><span data-stu-id="4aba1-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4aba1-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4aba1-106">Overview</span></span>
<span data-ttu-id="4aba1-107">Este tópico mostra como Olá toouse [modelos](notification-hubs-templates-cross-platform-push-messages.md) recurso de Hubs de notificação do Azure toobroadcast últimas notificações de notícias que foram localizadas por idioma e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4aba1-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="4aba1-108">Neste tutorial você iniciar com o aplicativo do iOS Olá criado no [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="4aba1-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="4aba1-109">Ao concluir, que você será capaz de tooregister para categorias que você está interessado, especificar um idioma no qual notificações de saudação tooreceive e receber apenas as notificações por push para categorias de saudação selecionada nesse idioma.</span><span class="sxs-lookup"><span data-stu-id="4aba1-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="4aba1-110">Há um cenário de toothis duas partes:</span><span class="sxs-lookup"><span data-stu-id="4aba1-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="4aba1-111">aplicativo iOS permite que cliente dispositivos toospecify um idioma e toodifferent toosubscribe recentes categorias de notícias;</span><span class="sxs-lookup"><span data-stu-id="4aba1-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="4aba1-112">back-end Hello transmite notificações hello, usando Olá **marca** e **modelo** recursos de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aba1-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4aba1-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4aba1-113">Prerequisites</span></span>
<span data-ttu-id="4aba1-114">Você já deve ter concluído Olá [toosend de Hubs de notificação de uso últimas notícias] tutorial e ter o código de saudação disponível, porque este tutorial baseia-se diretamente ao código.</span><span class="sxs-lookup"><span data-stu-id="4aba1-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="4aba1-115">O uso do Visual Studio 2012 ou posterior é opcional.</span><span class="sxs-lookup"><span data-stu-id="4aba1-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="4aba1-116">Conceitos de modelo</span><span class="sxs-lookup"><span data-stu-id="4aba1-116">Template concepts</span></span>
<span data-ttu-id="4aba1-117">Em [toosend de Hubs de notificação de uso últimas notícias] você criou um aplicativo usado **marcas** toonotifications toosubscribe para categorias diferentes de notícias.</span><span class="sxs-lookup"><span data-stu-id="4aba1-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="4aba1-118">No entanto, muitos aplicativos são destinados a vários mercados e requerem localização.</span><span class="sxs-lookup"><span data-stu-id="4aba1-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="4aba1-119">Isso significa que o conteúdo de saudação do hello as próprias notificações têm toobe localizado e entregue toohello conjunto correto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4aba1-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="4aba1-120">Este tópico mostraremos como Olá toouse **modelo** localizadas de recurso de Hubs de notificação tooeasily entregar notificações das últimas notícias.</span><span class="sxs-lookup"><span data-stu-id="4aba1-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="4aba1-121">Observação: uma maneira toosend localizado notificações é toocreate várias versões de cada marca.</span><span class="sxs-lookup"><span data-stu-id="4aba1-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="4aba1-122">Por exemplo, toosupport em inglês, francês e inglês Mandarim, temos três marcas diferentes de notícias do mundo: "world_en", "world_fr" e "world_ch".</span><span class="sxs-lookup"><span data-stu-id="4aba1-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="4aba1-123">Podemos teria toosend uma versão localizada do hello world notícias tooeach dessas marcas.</span><span class="sxs-lookup"><span data-stu-id="4aba1-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="4aba1-124">Neste tópico usamos a proliferação de saudação tooavoid modelos de marcas e o requisito de saudação de enviar várias mensagens.</span><span class="sxs-lookup"><span data-stu-id="4aba1-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="4aba1-125">Em um nível alto, os modelos são uma maneira toospecify como um dispositivo específico deve receber uma notificação.</span><span class="sxs-lookup"><span data-stu-id="4aba1-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="4aba1-126">modelo Olá Especifica o formato de carga exata de saudação referindo tooproperties que fazem parte da mensagem de saudação enviada pelo seu back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4aba1-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="4aba1-127">Em nosso caso, enviaremos uma mensagem independente de localidade contendo todos os idiomas com suporte:</span><span class="sxs-lookup"><span data-stu-id="4aba1-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="4aba1-128">Em seguida, podemos irá garantir que dispositivos registrar com um modelo que refere-se a propriedade de toohello correta.</span><span class="sxs-lookup"><span data-stu-id="4aba1-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="4aba1-129">Por exemplo, um aplicativo iOS que quer tooregister para francês notícias registrará a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="4aba1-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="4aba1-130">Os modelos são um recurso muito avançado sobre o qual você pode aprender em nosso artigo [Modelos](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="4aba1-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="4aba1-131">interface de usuário do aplicativo Hello</span><span class="sxs-lookup"><span data-stu-id="4aba1-131">hello app user interface</span></span>
<span data-ttu-id="4aba1-132">Agora vamos modificar Olá últimas notícias aplicativo que você criou no tópico Olá [toosend de Hubs de notificação de uso últimas notícias] toosend localizado notícias mais recentes usando modelos.</span><span class="sxs-lookup"><span data-stu-id="4aba1-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="4aba1-133">No seu MainStoryboard_iPhone.storyboard, adicione um controle segmentado com linguagens Olá três que forneceremos suporte: Mandarim, francês e inglês.</span><span class="sxs-lookup"><span data-stu-id="4aba1-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="4aba1-134">Faça tooadd-se de que um IBOutlet na sua ViewController.h conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="4aba1-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="4aba1-135">Criando aplicativo do iOS de saudação</span><span class="sxs-lookup"><span data-stu-id="4aba1-135">Building hello iOS app</span></span>
1. <span data-ttu-id="4aba1-136">No seu Notification.h adicionar Olá *retrieveLocale* método e modificar o repositório de saudação e inscrever-se métodos conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="4aba1-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="4aba1-137">No seu Notification.m modificar Olá *storeCategoriesAndSubscribe* método, adicionando o parâmetro de localidade hello e armazenando-o em padrões de saudação do usuário:</span><span class="sxs-lookup"><span data-stu-id="4aba1-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="4aba1-138">Modifique Olá *assinar* localidade de saudação do método tooinclude:</span><span class="sxs-lookup"><span data-stu-id="4aba1-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    <span data-ttu-id="4aba1-139">Observe como estamos agora usando método hello *registerTemplateWithDeviceToken*, em vez de *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="4aba1-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="4aba1-140">Quando registramos para um modelo temos modelo do tooprovide Olá json e também um nome para o modelo de saudação (como o nosso aplicativo poderá tooregister diferentes modelos).</span><span class="sxs-lookup"><span data-stu-id="4aba1-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="4aba1-141">Verifique se tooregister suas categorias como marcas, como queremos toomake se tooreceive Olá notifciations para obter as notícias.</span><span class="sxs-lookup"><span data-stu-id="4aba1-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="4aba1-142">Adicione uma localidade de saudação do método tooretrieve saudação padrão das configurações do usuário:</span><span class="sxs-lookup"><span data-stu-id="4aba1-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="4aba1-143">Agora que modificamos nossa classe notificações, temos toomake-se de que o nosso ViewController faz uso de saudação UISegmentControl novo.</span><span class="sxs-lookup"><span data-stu-id="4aba1-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="4aba1-144">Adicionar Olá a seguinte linha no hello *viewDidLoad* método toomake se tooshow Olá localidade que está selecionada no momento:</span><span class="sxs-lookup"><span data-stu-id="4aba1-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="4aba1-145">Em seguida, no seu *assinar* método, alterar sua chamada toohello *storeCategoriesAndSubscribe* toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aba1-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. <span data-ttu-id="4aba1-146">Por fim, você tem Olá tooupdate *didRegisterForRemoteNotificationsWithDeviceToken* método no seu appdelegate. M, para que você possa atualizar corretamente o seu registro quando seu aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="4aba1-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="4aba1-147">Alterar sua chamada toohello *assinar* método das notificações com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="4aba1-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="4aba1-148">(opcional) Envie notificações de modelo localizado do aplicativo de console do .NET.</span><span class="sxs-lookup"><span data-stu-id="4aba1-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="4aba1-149">(opcional) Enviar notificações de modelo traduzido do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="4aba1-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="4aba1-150">Se você não tiver acesso tooVisual Studio, ou teste toojust enviar notificações de modelo de saudação localizada diretamente do aplicativo hello no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aba1-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="4aba1-151">Você pode simples adicionar toohello de parâmetros de modelo Olá localizado `SendNotificationRESTAPI` método definido no tutorial anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4aba1-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];

            [dataTask resume];
        }




## <a name="next-steps"></a><span data-ttu-id="4aba1-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4aba1-152">Next Steps</span></span>
<span data-ttu-id="4aba1-153">Para obter mais informações sobre o uso de modelos, consulte:</span><span class="sxs-lookup"><span data-stu-id="4aba1-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="4aba1-154">[Notificar usuários com Hubs de Notificação: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="4aba1-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="4aba1-155">[Notificar usuários com Hubs de Notificação: Serviços Móveis]</span><span class="sxs-lookup"><span data-stu-id="4aba1-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend de Hubs de notificação de uso últimas notícias]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notificar usuários com Hubs de Notificação: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notificar usuários com Hubs de Notificação: Serviços Móveis]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
