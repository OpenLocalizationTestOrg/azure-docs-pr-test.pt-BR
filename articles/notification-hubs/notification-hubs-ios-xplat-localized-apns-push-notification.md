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
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Usar Hubs de notificação toosend localizado recentes notícias tooiOS dispositivos
> [!div class="op_single_selector"]
> * [C# da Windows Store](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Visão geral
Este tópico mostra como Olá toouse [modelos](notification-hubs-templates-cross-platform-push-messages.md) recurso de Hubs de notificação do Azure toobroadcast últimas notificações de notícias que foram localizadas por idioma e dispositivo. Neste tutorial você iniciar com o aplicativo do iOS Olá criado no [toosend de Hubs de notificação de uso últimas notícias]. Ao concluir, que você será capaz de tooregister para categorias que você está interessado, especificar um idioma no qual notificações de saudação tooreceive e receber apenas as notificações por push para categorias de saudação selecionada nesse idioma.

Há um cenário de toothis duas partes:

* aplicativo iOS permite que cliente dispositivos toospecify um idioma e toodifferent toosubscribe recentes categorias de notícias;
* back-end Hello transmite notificações hello, usando Olá **marca** e **modelo** recursos de Hubs de notificação do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Você já deve ter concluído Olá [toosend de Hubs de notificação de uso últimas notícias] tutorial e ter o código de saudação disponível, porque este tutorial baseia-se diretamente ao código.

O uso do Visual Studio 2012 ou posterior é opcional.

## <a name="template-concepts"></a>Conceitos de modelo
Em [toosend de Hubs de notificação de uso últimas notícias] você criou um aplicativo usado **marcas** toonotifications toosubscribe para categorias diferentes de notícias.
No entanto, muitos aplicativos são destinados a vários mercados e requerem localização. Isso significa que o conteúdo de saudação do hello as próprias notificações têm toobe localizado e entregue toohello conjunto correto de dispositivos.
Este tópico mostraremos como Olá toouse **modelo** localizadas de recurso de Hubs de notificação tooeasily entregar notificações das últimas notícias.

Observação: uma maneira toosend localizado notificações é toocreate várias versões de cada marca. Por exemplo, toosupport em inglês, francês e inglês Mandarim, temos três marcas diferentes de notícias do mundo: "world_en", "world_fr" e "world_ch". Podemos teria toosend uma versão localizada do hello world notícias tooeach dessas marcas. Neste tópico usamos a proliferação de saudação tooavoid modelos de marcas e o requisito de saudação de enviar várias mensagens.

Em um nível alto, os modelos são uma maneira toospecify como um dispositivo específico deve receber uma notificação. modelo Olá Especifica o formato de carga exata de saudação referindo tooproperties que fazem parte da mensagem de saudação enviada pelo seu back-end do aplicativo. Em nosso caso, enviaremos uma mensagem independente de localidade contendo todos os idiomas com suporte:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Em seguida, podemos irá garantir que dispositivos registrar com um modelo que refere-se a propriedade de toohello correta. Por exemplo, um aplicativo iOS que quer tooregister para francês notícias registrará a seguir hello:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Os modelos são um recurso muito avançado sobre o qual você pode aprender em nosso artigo [Modelos](notification-hubs-templates-cross-platform-push-messages.md) .

## <a name="hello-app-user-interface"></a>interface de usuário do aplicativo Hello
Agora vamos modificar Olá últimas notícias aplicativo que você criou no tópico Olá [toosend de Hubs de notificação de uso últimas notícias] toosend localizado notícias mais recentes usando modelos.

No seu MainStoryboard_iPhone.storyboard, adicione um controle segmentado com linguagens Olá três que forneceremos suporte: Mandarim, francês e inglês.

![][13]

Faça tooadd-se de que um IBOutlet na sua ViewController.h conforme mostrado abaixo:

![][14]

## <a name="building-hello-ios-app"></a>Criando aplicativo do iOS de saudação
1. No seu Notification.h adicionar Olá *retrieveLocale* método e modificar o repositório de saudação e inscrever-se métodos conforme mostrado abaixo:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    No seu Notification.m modificar Olá *storeCategoriesAndSubscribe* método, adicionando o parâmetro de localidade hello e armazenando-o em padrões de saudação do usuário:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Modifique Olá *assinar* localidade de saudação do método tooinclude:
   
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
   
    Observe como estamos agora usando método hello *registerTemplateWithDeviceToken*, em vez de *registerNativeWithDeviceToken*. Quando registramos para um modelo temos modelo do tooprovide Olá json e também um nome para o modelo de saudação (como o nosso aplicativo poderá tooregister diferentes modelos). Verifique se tooregister suas categorias como marcas, como queremos toomake se tooreceive Olá notifciations para obter as notícias.
   
    Adicione uma localidade de saudação do método tooretrieve saudação padrão das configurações do usuário:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Agora que modificamos nossa classe notificações, temos toomake-se de que o nosso ViewController faz uso de saudação UISegmentControl novo. Adicionar Olá a seguinte linha no hello *viewDidLoad* método toomake se tooshow Olá localidade que está selecionada no momento:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Em seguida, no seu *assinar* método, alterar sua chamada toohello *storeCategoriesAndSubscribe* toohello a seguir:
   
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
3. Por fim, você tem Olá tooupdate *didRegisterForRemoteNotificationsWithDeviceToken* método no seu appdelegate. M, para que você possa atualizar corretamente o seu registro quando seu aplicativo é iniciado. Alterar sua chamada toohello *assinar* método das notificações com os seguintes hello:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(opcional) Envie notificações de modelo localizado do aplicativo de console do .NET.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(opcional) Enviar notificações de modelo traduzido do dispositivo Olá
Se você não tiver acesso tooVisual Studio, ou teste toojust enviar notificações de modelo de saudação localizada diretamente do aplicativo hello no dispositivo de saudação.  Você pode simples adicionar toohello de parâmetros de modelo Olá localizado `SendNotificationRESTAPI` método definido no tutorial anterior hello.

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




## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o uso de modelos, consulte:

* [Notificar usuários com Hubs de Notificação: ASP.NET]
* [Notificar usuários com Hubs de Notificação: Serviços Móveis]

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
