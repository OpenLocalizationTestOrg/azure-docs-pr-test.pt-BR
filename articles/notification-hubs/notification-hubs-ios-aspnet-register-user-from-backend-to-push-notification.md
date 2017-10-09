---
title: "usuário atual do aaaRegister Olá para notificações de push, usando a API da Web | Microsoft Docs"
description: "Saiba como toorequest envio registro de notificação em um aplicativo do iOS com Hubs de notificação do Azure quando o registro é executado pela API da Web do ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>Registrar usuário atual de saudação para notificações por push, usando ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Visão geral
Este tópico mostra como toorequest envio de registro de notificação com Hubs de notificação do Azure quando o registro é realizado pela API da Web do ASP.NET. Este tópico estende tutorial Olá [notificar os usuários com Hubs de notificação]. Você já deve ter concluído etapas Olá necessários no tutorial toocreate Olá autenticado serviço móvel. Para obter mais informações sobre Olá notificar o cenário de usuários, consulte [notificar os usuários com Hubs de notificação].

## <a name="update-your-app"></a>Atualizar seu aplicativo
1. No seu MainStoryboard_iPhone.storyboard, adicione Olá componentes a seguir na biblioteca de objetos de saudação:
   
   * **Rótulo**: "TooUser com Hubs de notificação de Push"
   * **Label**: "InstallationId"
   * **Label**: "User"
   * **Text Field**: "User"
   * **Label**: "Password"
   * **Text Field**: "Password"
   * **Button**: "Login"
     
     Neste ponto, o storyboard Olá seguinte aparência:
     
      ![][0]
2. No editor de assistente hello, criar tomadas para todos os controles de saudação alternada e chamá-los, conecte-se campos de texto de saudação com hello View Controller (delegado) e criar um **ação** para Olá **login** botão.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Crie uma classe denominada **DeviceInfo**, e Olá cópia código a seguir na seção de interface de saudação do arquivo hello DeviceInfo.h:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Copie Olá código na seção de implementação de saudação do arquivo de DeviceInfo.m Olá a seguir:
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. No PushToUserAppDelegate.h, adicione Olá singleton de propriedade a seguir:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. Em Olá **didFinishLaunchingWithOptions** método PushToUserAppDelegate.m, adicionar Olá código a seguir:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    primeira linha de saudação inicializa Olá **DeviceInfo** singleton. Olá segunda linha inicia Olá registro para notificações por push, que já está presente é você já tiver concluído a saudação [começar com Hubs de notificação] tutorial.
7. Em PushToUserAppDelegate.m, implemente o método hello **didRegisterForRemoteNotificationsWithDeviceToken** no seu AppDelegate e adicione Olá código a seguir:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Isso define o token do dispositivo Olá para solicitação de saudação.
   
   > [!NOTE]
   > Neste ponto, não deve haver nenhum outro código nesse método. Se você já tiver uma chamada toohello **registerNativeWithDeviceToken** método foi adicionado quando você concluir a saudação [começar com Hubs de notificação](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, você deve comentários ou remover chamada.
   > 
   > 
8. No arquivo de PushToUserAppDelegate.m de saudação, adicione Olá método do manipulador a seguir:
   
   * aplicativo (void):(UIApplication *) aplicativo didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", userInfo);   UIAlertView * alerta = [[UIAlertView alocação] initWithTitle:@"Notification" mensagem: [userInfo objectForKey:@"inAppMessage]" delegado: nil cancelButtonTitle: @ otherButtonTitles:nil "Okey", nil];   [alerta Mostrar]; }
   
   Este método exibirá um alerta em Olá da interface do usuário quando seu aplicativo recebe notificações enquanto ele está em execução.
9. Abrir Olá PushToUserViewController.m arquivo e teclado Olá retorno em Olá implementação a seguir:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. Em Olá **viewDidLoad** método no arquivo de PushToUserViewController.m hello, inicializar o rótulo de installationId de saudação da seguinte maneira:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Adicione Olá propriedades na interface em PushToUserViewController.m a seguir:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Em seguida, adicione Olá implementação a seguir:
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. Código a seguir de saudação de cópia em Olá **login** criado pelo XCode de método do manipulador:
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    Esse método obtém uma ID de instalação e o canal para notificações por push e enviá-la, junto com o tipo de dispositivo hello, toohello autenticada método de API da Web que cria um registro em Hubs de notificação. Essa API Web foi definida em [notificar os usuários com Hubs de notificação].

Agora que hello aplicativo cliente foi atualizado, retornar toohello [notificar os usuários com Hubs de notificação] e atualizar as notificações de toosend de serviço móvel hello usando Hubs de notificação.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificar os usuários com Hubs de notificação]: /manage/services/notification-hubs/notify-users-aspnet

[começar com Hubs de notificação]: /manage/services/notification-hubs/get-started-notification-hubs-ios
