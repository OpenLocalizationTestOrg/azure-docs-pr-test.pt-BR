---
title: "aaaAzure notificação Hubs seguro Push"
description: "Saiba como toosend segura envio notificações tooan iOS aplicativo do Azure. Exemplos de códigos escritos em Objective-C e c#."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Push Seguro dos Hubs de Notificação do Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Visão geral
Suporte de notificação por push no Microsoft Azure permite que você tooaccess uma infraestrutura de push de fácil de usar, multiplataforma, dimensionável, que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas.

Devido a restrições de segurança ou tooregulatory, às vezes, um aplicativo pode ser conveniente tooinclude algo na notificação de saudação que não pode ser transmitida por meio da infraestrutura de notificação por push padrão hello. Este tutorial descreve como tooachieve Olá a mesma experiência, enviando informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo de cliente hello e back-end de aplicativo hello.

Em um nível alto, o fluxo de saudação é o seguinte:

1. Olá aplicativo back-end:
   * Armazena uma carga segura no banco de dados de back-end.
   * Envia a ID de saudação do dispositivo toohello notificação (nenhuma informação de segurança é enviada).
2. Olá o aplicativo no dispositivo hello, ao receber a notificação de saudação:
   * dispositivo Olá contata Olá back-end solicitante Olá carga de segurança.
   * aplicativo Hello pode mostrar carga hello como uma notificação no dispositivo de saudação.

É importante toonote em Olá anterior fluxo (e, neste tutorial), vamos supor que o dispositivo Olá armazena um token de autenticação no armazenamento local, depois Olá usuário fizer logon. Isso garante uma experiência completamente, como dispositivo Olá pode recuperar a carga de segurança da notificação hello usando este token. Se seu aplicativo não armazenar os tokens de autenticação no dispositivo hello, ou se esses tokens podem ser expirados, hello aplicativo de dispositivo, ao receber a notificação de saudação deve exibir uma notificação genérica solicitando Olá usuário toolaunch Olá aplicativo. aplicativo Hello, em seguida, autentica o usuário hello e mostra a carga de notificação de saudação.

Este tutorial seguro Push mostra como toosend uma notificação por push com segurança. Olá tutorial baseia-se em Olá [notificar usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, portanto você deve concluir as etapas de saudação neste tutorial primeiro.

> [!NOTE]
> Este tutorial presume que você criou e configurou o seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Modificar o projeto do iOS Olá
Agora que você modificou o Olá apenas de toosend de back-end do aplicativo *id* de uma notificação, você tem toochange seu toohandle de aplicativo do iOS que notificação e o retorno de chamada hello seu back-end tooretrieve Proteja toobe mensagem exibida.

tooachieve essa meta, temos toowrite Olá lógica tooretrieve Olá conteúdo seguro do que Olá back-end do aplicativo.

1. Em **appdelegate. M**, verifique se registros de aplicativo hello silenciosa notificações para que ele processa a id de notificação de saudação enviada de back-end de saudação. Adicionar Olá **UIRemoteNotificationTypeNewsstandContentAvailability** opção didFinishLaunchingWithOptions:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. No seu **appdelegate. M** adicionar uma seção de implementação na parte superior da saudação com hello declaração a seguir:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Adicione ao Olá Olá de seção de implementação código a seguir, substituindo o espaço reservado de saudação `{back-end endpoint}` com ponto de extremidade Olá para o back-end obtido anteriormente:

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. Agora temos toohandle notificação de entrada hello e usar o método hello acima tooretrieve Olá conteúdo toodisplay. Primeiro, temos tooenable seu toorun de aplicativo do iOS no plano de fundo de saudação ao receber uma notificação por push. Em **XCode**, selecione o projeto de aplicativo no painel esquerdo do hello, clique em seu destino de aplicativo principal no hello **destinos** seção no painel central hello.
2. Em seguida, clique em seu **recursos** guia na parte superior de saudação do seu painel central e verifique Olá **remoto notificações** caixa de seleção.
   
    ![][IOS1]
3. Em **appdelegate. M** adicionar Olá notificações de push toohandle método a seguir:
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    Observe que é preferível toohandle casos de saudação de propriedade de cabeçalho de autenticação ausente ou rejeição por Olá back-end. tratamento específico de Olá desses casos dependem principalmente em sua experiência de usuário de destino. Uma opção é toodisplay uma notificação com um aviso genérico para Olá tooauthenticate tooretrieve Olá real notificação ao usuário.

## <a name="run-hello-application"></a>Executar Olá aplicativo
toorun Olá aplicativo, Olá a seguir:

1. No XCode, execute o aplicativo hello em um dispositivo iOS físicos (push de notificações não funcionará no simulador Olá).
2. No aplicativo do iOS Olá da interface do usuário, digite um nome de usuário e senha. Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá o mesmo valor.
3. No aplicativo do iOS Olá da interface do usuário, clique em **login**. Em seguida, clique em **Enviar push**. Você deve ver a notificação de seguro hello está sendo exibida no seu centro de notificação.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
