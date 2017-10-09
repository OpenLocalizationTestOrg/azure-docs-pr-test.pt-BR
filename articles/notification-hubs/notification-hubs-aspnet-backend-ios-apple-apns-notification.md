---
title: "aaaAzure notificar usuários de Hubs de notificação para iOS com o back-end .NET"
description: "Saiba como toosend envio toousers notificações no Azure. Exemplos de código escritos em Objective-C e hello API .NET para Olá back-end."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Notificar usuários nos Hubs de Notificação do Azure para iOS com o back-end do .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Visão geral
Suporte de notificação por push no Azure permite que você tooaccess uma fácil de usar, multiplatform e infraestrutura de envio expandido, o que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas. Este tutorial mostra como toouse Hubs de notificação do Azure toosend envio usuário de aplicativo específico de tooa notificações em um dispositivo específico. Um back-end ASP.NET WebAPI é usado tooauthenticate clientes e notificações de toogenerate, conforme mostrado no tópico de orientação Olá [registro do seu back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> Este tutorial presume que você criou e configurou o seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). Este tutorial também é toohello pré-requisito Olá [proteger Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.
> Se desejar que os aplicativos móveis toouse como seu serviço de back-end, consulte Olá [Mobile aplicativos começar com envio por Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Modificar seu aplicativo iOS
1. Olá abrir página única visualizar o aplicativo criado no hello [Introdução aos Hubs de notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.
   
   > [!NOTE]
   > Nesta seção, presumimos que você configurou seu projeto com um nome de organização vazio. Caso contrário, será necessário tooprepend seus nomes de classe de tooall de nome de organização.
   > 
   > 
2. No seu Main.storyboard Adicione componentes de saudação mostrados na captura de tela hello abaixo na biblioteca de objetos de saudação.
   
    ![][1]
   
   * **Nome de usuário**: UITextField um com o texto do espaço reservado, *digitar nome de usuário*, imediatamente abaixo Olá enviar rótulo de resultados e toohello restrita à esquerda e direita margens e abaixo Olá enviar rótulo de resultados.
   * **Senha**: UITextField um com o texto do espaço reservado, *digite a senha*, imediatamente abaixo Olá campo de texto de nome de usuário e toohello restrita à esquerda e direita margens e abaixo do campo de texto de nome de usuário de saudação. Verificar Olá **segura de entrada de texto** opção Olá Inspetor de atributo, em *chave retornar*.
   * **Faça logon no**: UIButton um rotulada imediatamente abaixo do campo de texto de senha hello e desmarque Olá **habilitado** opção Olá Inspetor de atributos em *conteúdo de controle*
   * **WNS**: rótulo e o envio de tooenable do comutador hello notificação de serviço de notificação do Windows se ele foi configurado no hub de saudação. Consulte Olá [guia de Introdução do Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.
   * **GCM**: rótulo e o envio de tooenable do comutador hello notificação tooGoogle mensagens de nuvem se ele foi configurado no hub de saudação. Consulte o tutorial [Introdução ao Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .
   * **APNS**: rótulo e o envio de tooenable do comutador hello notificação toohello serviço de notificação de plataforma Apple.
   * **Recipent Username**: UITextField um com o texto do espaço reservado, *marca de nome de usuário do destinatário*, imediatamente abaixo Olá GCM rótulo e toohello restrita à direita e esquerda margens e abaixo Olá GCM do rótulo.

    Alguns componentes foram adicionados em Olá [Introdução aos Hubs de notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.

1. **CTRL** arraste de componentes de saudação do hello exibição tooViewController.h e adicione essas novas saídas.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. Em ViewController.h, adicione o seguinte Olá `#define` logo abaixo as instruções de importação. Olá substituto *< Inserir ponto de extremidade de back-end que seu\>*  espaço reservado com hello usado toodeploy seu back-end do aplicativo na seção anterior de saudação do URL de destino. Por exemplo, *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. No seu projeto, criar um novo **Cocoa Touch classe** chamado **RegisterClient** toointerface com hello back-end do ASP.NET é criado. Criar classe Olá herdando `NSObject`. Em seguida, adicione Olá Olá RegisterClient.h código a seguir.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Olá RegisterClient.m atualizar Olá `@interface` seção:
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Substituir saudação `@implementation` seção Olá RegisterClient.m com hello código a seguir.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    código de saudação acima implementa a lógica de saudação explicada no artigo de diretrizes Olá [registro do seu back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) usando NSURLSession tooperform REST chama back-end de aplicativo tooyour e NSUserDefaults toolocally repositório Olá registrationId retornado pelo hub de notificação de saudação.

    Observe que essa classe requer sua propriedade **authorizationHeader** toobe definido em ordem toowork corretamente. Essa propriedade é definida pelo Olá **ViewController** classe depois Olá login.

1. Em ViewController.h, adicione uma instrução `#import` RegisterClient.h. Em seguida, adicione uma declaração de token de dispositivo hello e referência tooa `RegisterClient` instância no hello `@interface` seção:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. No ViewController.m, adicione uma declaração de método particular em Olá `@interface` seção:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Olá trecho a seguir não é um esquema de autenticação segura, você deve substituir a implementação de saudação do hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** com o mecanismo de autenticação específico Isso gera um toobe de token de autenticação consumida por Olá registro de classe de cliente, por exemplo, OAuth, Active Directory.
> 
> 

1. Em seguida, em Olá `@implementation` seção ViewController.m adicionar Olá código que adiciona a implementação de saudação do cabeçalho de token e autenticação de dispositivo de saudação do configuração a seguir.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    Observe como o token de configuração do dispositivo Olá permite Olá no botão de logon. Isso ocorre porque como parte da ação de logon hello, controlador de exibição Olá registra para notificações de push com o back-end de aplicativo hello. Portanto, não queremos Log na ação toobe acessível até que o token do dispositivo Olá tiver sido configurado corretamente. É possível desacoplar Olá login de registro de push hello como antiga Olá ocorre antes de saudação último.
2. Em ViewController.m, use Olá após o método de ação de saudação trechos de código tooimplement para o **logon** botão e um método toosend Olá mensagem de notificação usando Olá back-end do ASP.NET.
   
       - (IBAction) LogInAction: remetente (id) {/ / criar cabeçalho de autenticação e defini-la no cliente de registro NSString * nome de usuário = auto. UsernameField.text;   Senha NSString * = auto. PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = auto;   [self.registerClient registerWithDeviceToken:self.deviceToken marcas: nil andCompletion:^(NSError* error) {Se (! erro) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = Sim;               [self MessageBox:@"Success" message:@"Registered com êxito!"];});}}];}

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            Passar marca Olá de pns e o nome de usuário como parâmetros com hello URL do REST toohello ASP.NET back-end NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            Solicitação de NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [solicitação setHTTPMethod:@"POST"];

            Obter authenticationheader simulações de saudação do cliente de registro Olá NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [solicitação setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            Adicionar o corpo da mensagem de notificação Olá [solicitação setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [solicitação setHTTPBody: [mensagem dataUsingEncoding:NSUTF8StringEncoding]];

            Executar notificação de envio de saudação API REST em Olá NSURLSessionDataTask de back-end ASP.NET * dataTask = [sessão dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Erro) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) resposta;        Se (erro | | httpResponse.statusCode! = 200) {NSString* status = [NSString stringWithFormat:@"Error Status para % @: % d\nError: %@\n", pns, httpResponse.statusCode, erro];            dispatch_async(dispatch_get_main_queue(), ^ {/ / anexar texto porque todas as chamadas PNS 3 também podem ter informações tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. Atualizar ação Olá Olá **enviar notificação** botão back-end ASP.NET de saudação toouse e enviar tooany PNS habilitado por um comutador.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. Na função **ViewDidLoad**, adicione Olá instância de RegisterClient Olá tooinstantiate a seguir e defina o delegado Olá para os campos de texto.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Agora em **appdelegate. M**, remova todo o conteúdo de saudação do método hello **aplicativo: didRegisterForPushNotificationWithDeviceToken:** e substitua-o com hello toomake a seguir se Olá exibição controlador contém o token de dispositivo mais recente Olá recuperado do APNs:
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Por fim na **appdelegate. M**, certifique-se de ter Olá método a seguir:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Saudação de teste aplicativo
1. No XCode, execute o aplicativo hello em um dispositivo iOS físicos (push de notificações não funcionará no simulador Olá).
2. No aplicativo do iOS Olá da interface do usuário, digite um nome de usuário e senha. Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá mesmo valor de cadeia de caracteres. Em seguida, clique em **Fazer logon**.
   
    ![][2]
3. Você deverá ver um pop-up informando sobre o sucesso da inscrição. Clique em **OK**.
   
    ![][3]
4. Em hello **marca de nome de usuário do destinatário* texto campo, digite Olá etiqueta de nome de usuário usada com o registro de saudação de outro dispositivo.
5. Digite uma mensagem de notificação e clique em **Enviar notificação**.  Somente os dispositivos de saudação que tem um registro com marca de nome de usuário destinatário Olá recebem a mensagem de notificação de saudação.  Ela só é enviada toothose usuários.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
