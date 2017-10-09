---
title: "aaaAzure notificação Hubs Rich Push"
description: "Saiba como rich toosend envio notificações tooan iOS aplicativo do Azure. Exemplos de códigos escritos em Objective-C e c#."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Push Avançado dos Hubs de Notificação do Azure
## <a name="overview"></a>Visão geral
Em ordem tooengage os usuários com conteúdo rich instantâneo, um aplicativo pode querer toopush além do texto sem formatação. Essas notificações promovem interações do usuário e apresentam conteúdo, como urls, sons, imagens/cupons e muito mais. Este tutorial baseia-se em Olá [notificar usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tópico e mostra como toosend enviar notificações por push que incorporam cargas (por exemplo, a imagem).

Este tutorial é compatível com iOS 7 e 8.

  ![][IOS1]

Em um alto nível:

1. saudação de aplicativos back-end:
   * Repositórios Olá carga avançada (nesse caso, a imagem) no armazenamento de banco de dados/local de back-end Olá
   * Envia a ID do dispositivo toohello notificação avançada
2. Aplicativo no dispositivo hello:
   * Contatos Olá solicitando a carga avançados Olá com a ID de saudação recebe de back-end
   * Envia notificações de usuários no dispositivo hello quando a recuperação de dados estiver concluída e mostra a carga de saudação imediatamente quando os usuários tocam em toolearn mais

## <a name="webapi-project"></a>Projeto WebAPI
1. No Visual Studio, abra Olá **AppBackend** projeto que você criou no hello [notificar usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.
2. Obtenha uma imagem que você deseja toonotify aos usuários e colocá-la em um **img** pasta no diretório do projeto.
3. Clique em **Mostrar todos os arquivos** em Olá Gerenciador de soluções e clique pasta Olá muito**incluir no projeto**.
4. Com imagem Olá selecionada, altere sua ação de compilação na janela Propriedades muito**recurso inserido**.
   
    ![][IOS2]
5. Em **Notifications.cs**, adicione o seguinte Olá usando a instrução:
   
        using System.Reflection;
6. Saudação de atualização inteira **notificações** classe com hello código a seguir. Ser tooreplace se espaços reservados de saudação com suas credenciais de hub de notificação e o nome do arquivo de imagem.
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > (opcional) Consulte também[como tooembed e acessar recursos usando o Visual C#](http://support.microsoft.com/kb/319292) para obter mais informações sobre como tooadd e obter os recursos de projeto.
   > 
   > 
7. Em **NotificationsController.cs**, redefinir **NotificationsController** com hello trechos de código a seguir. Isso envia um toodevice de id de notificação avançada silenciosa inicial e permite a recuperação do lado do cliente da imagem:
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. Agora podemos reimplantar esta tooan aplicativo site do Azure em ordem toomake-lo acessível de todos os dispositivos. Clique duas vezes em Olá **AppBackend** do projeto e selecione **publicar**.
9. Selecione o Site do Azure como seu destino de publicação. Faça logon com sua conta do Azure e selecione um site novo ou existente e anote Olá **URL de destino** propriedade Olá **Conexão** guia. Chamaremos toothis URL como o *ponto de extremidade de back-end* posteriormente neste tutorial. Clique em **Publicar**.

## <a name="modify-hello-ios-project"></a>Modificar o projeto do iOS Olá
Agora que você tenha modificado o hello apenas do aplicativo back-end toosend *id* de uma notificação, você alterará o toohandle de aplicativo do iOS essa id e recuperar mensagem avançados de saudação do seu back-end.

1. Abra seu projeto de iOS e habilitar notificações remotas pelo destino de aplicativo principal de tooyour indo em Olá **destinos** seção.
2. Clique em **recursos**, ativar **modos de segundo plano**e verifique Olá **remoto notificações** caixa de seleção.
   
    ![][IOS3]
3. Vá muito**Main.storyboard**e certifique-se de ter um controlador de exibição (mencionado tooas início View Controller neste tutorial) de [notificar o usuário](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.
4. Adicionar um **navegação controlador** tooyour de storyboard e arraste controle tooHome View Controller toomake-Olá **exibição de raiz** de navegação. Verifique se Olá **é inicial View Controller** em atributos Inspetor é selecionado para Olá somente no controlador de navegação.
5. Adicionar um **View Controller** toostoryboard e adicione um **imagem**. Isso é página Olá os usuários verão quando desejarem toolearn mais clicando no notifiication Olá. O storyboard deve ter a seguinte aparência:
   
    ![][IOS4]
6. Clique em Olá **início View Controller** no storyboard e verifique se ele possui **homeViewController** como seu **classe personalizada** e **Storyboard ID**em Inspetor de identidade hello.
7. Olá mesmo para o controlador de exibição de imagem como **imageViewController**.
8. Em seguida, crie uma nova classe de controlador de exibição denominada **imageViewController** toohandle Olá interface de usuário que você acabou de criar.
9. Em **imageViewController.h**, adicionar Olá declarações de interface do controlador toohello a seguir. Verifique se toocontrol e arraste da saudação storyboard imagem exibição toothese propriedades toolink Olá dois:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. Em **imageViewController.m**, adicione o seguinte de saudação final Olá **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. Em **appdelegate. M**, controlador de imagem Olá importação criada:
    
        #import "imageViewController.h"
12. Adicione uma seção de interface com hello declaração a seguir:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. Em **AppDelegate**, verifique se o aplicativo se registra para notificações silenciosas em **application: didFinishLaunchingWithOptions**:
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. SUBSTITUTE em Olá após a implementação para **aplicativo: didRegisterForRemoteNotificationsWithDeviceToken** tootake storyboard de saudação alterações de interface do usuário em conta:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Em seguida, adicione Olá métodos a seguir muito**appdelegate. M** tooretrieve Olá imagem do ponto de extremidade e enviar uma notificação local quando a recuperação for concluída. Certifique-se de espaço reservado de saudação de toosubstitute `{backend endpoint}` com seu ponto de extremidade de back-end:
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. Lidar com a notificação local Olá acima através da abertura de controlador de exibição de imagem Olá no **appdelegate. M** com hello métodos a seguir:
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>Executar Olá aplicativo
1. No XCode, execute o aplicativo hello em um dispositivo iOS físicos (push de notificações não funcionará no simulador Olá).
2. No aplicativo do iOS Olá da interface do usuário, insira um nome de usuário e a senha da saudação mesmo valor para a autenticação e clique em **logon**.
3. Clique em **Enviar por push** e você verá um alerta no aplicativo. Se você clicar em **mais**, será colocado toohello imagem escolhida tooinclude no seu back-end do aplicativo.
4. Você também pode clicar em **enviar por push** e pressione o botão página inicial de saudação do seu dispositivo imediatamente. Em alguns momentos, você receberá uma notificação por push. Se você tocar nela ou clique em mais, você será levado tooyour conteúdo da imagem avançados do aplicativo e hello.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
