---
title: "Notificar usuários nos Hubs de Notificação do Azure para iOS com o back-end do .NET"
description: "Saiba como enviar notificações por push para usuários no Azure. Amostras de código escritas em Objective-C e a API do .NET para o back-end."
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="83f73-104">Notificar usuários nos Hubs de Notificação do Azure para iOS com o back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="83f73-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="83f73-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="83f73-105">Overview</span></span>
<span data-ttu-id="83f73-106">O suporte à notificação por push no Azure permite que você acesse uma infraestrutura de envio por push fácil de usar, multiplataforma e expansível que simplifica em muito a implementação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="83f73-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="83f73-107">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push a um usuário específico do aplicativo em um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="83f73-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="83f73-108">Um back-end da API Web ASP.NET é usado para autenticar clientes e gerar notificações, conforme mostrado no tópico de diretrizes [Registrando-se por meio do back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="83f73-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="83f73-109">Este tutorial presume que você criou e configurou o seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83f73-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="83f73-110">Este tutorial também é um pré-requisito para o tutorial [Push Seguro (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="83f73-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="83f73-111">Se desejar usar os Aplicativos Móveis como seu serviço de back-end, veja [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="83f73-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="83f73-112">Modificar seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="83f73-112">Modify your iOS app</span></span>
1. <span data-ttu-id="83f73-113">Abra o aplicativo de exibição de Página única criado no tutorial [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="83f73-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83f73-114">Nesta seção, presumimos que você configurou seu projeto com um nome de organização vazio.</span><span class="sxs-lookup"><span data-stu-id="83f73-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="83f73-115">Caso contrário, será necessário preceder o nome da sua organização a todos os nomes de classe.</span><span class="sxs-lookup"><span data-stu-id="83f73-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="83f73-116">Em seu Main.storyboard, adicione os componentes mostrados na captura de tela abaixo da biblioteca de objetos.</span><span class="sxs-lookup"><span data-stu-id="83f73-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="83f73-117">**Nome de usuário**: um UITextField com texto de espaço reservado, *Inserir nome de usuário*, imediatamente abaixo de enviar rótulo de resultados e restrito às margens esquerda e direita e abaixo do rótulo de resultados de envio.</span><span class="sxs-lookup"><span data-stu-id="83f73-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="83f73-118">**Senha**: um UITextField com texto de espaço reservado, *Digite a senha*, imediatamente abaixo do campo de texto Nome de usuário e restrito às margens esquerda e direita e abaixo do campo de texto Nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="83f73-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="83f73-119">Verifique a opção **Entrada de texto seguro** no Inspetor de atributo, em *Retornar chave*.</span><span class="sxs-lookup"><span data-stu-id="83f73-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="83f73-120">**Fazer logon**: um UIButton chamado imediatamente abaixo do campo de texto de senha e desmarque a opção **Habilitado** no Inspetor de atributos, em *Conteúdo de controle*</span><span class="sxs-lookup"><span data-stu-id="83f73-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="83f73-121">**WNS**: o rótulo e o comutador para habilitar o envio da notificação do Serviço de Notificação do Windows, se ele tiver sido configurado no hub.</span><span class="sxs-lookup"><span data-stu-id="83f73-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="83f73-122">Confira o tutorial [Introdução ao Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="83f73-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="83f73-123">**GCM**: o rótulo e a opção para habilitar o envio da notificação para o Google Cloud Messaging, se ele tiver sido configurado no hub.</span><span class="sxs-lookup"><span data-stu-id="83f73-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="83f73-124">Consulte o tutorial [Introdução ao Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="83f73-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="83f73-125">**APNS**: o rótulo e a opção para habilitar o envio da notificação ao Apple Platform Notification Service.</span><span class="sxs-lookup"><span data-stu-id="83f73-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="83f73-126">**Nome do Usuário do Destinatário**: um UITextField com texto de espaço reservado *marca de nome de usuário do destinatário*, imediatamente abaixo do rótulo GCM e restrita às margens esquerda e direita e abaixo do rótulo do GCM.</span><span class="sxs-lookup"><span data-stu-id="83f73-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="83f73-127">Alguns componentes foram adicionados ao tutorial [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="83f73-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="83f73-128">**Ctrl** e arraste dos componentes, no modo de exibição, para ViewController.h e adicione essas novas saídas.</span><span class="sxs-lookup"><span data-stu-id="83f73-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="83f73-129">No ViewController.h, adicione o seguinte `#define` logo abaixo das instruções de importação.</span><span class="sxs-lookup"><span data-stu-id="83f73-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="83f73-130">Substitua o espaço reservado *<Inserir o seu ponto de extremidade do back-end\>* pela URL de destino que você usou para implantar o back-end do aplicativo na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="83f73-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="83f73-131">Por exemplo, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="83f73-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="83f73-132">Em seu projeto, crie uma nova **classe Cocoa Touch** chamada **RegisterClient** para fazer a interface com o back-end ASP.NET criado por você.</span><span class="sxs-lookup"><span data-stu-id="83f73-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="83f73-133">Criar a classe herdeira de `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="83f73-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="83f73-134">Em seguida, adicione o seguinte código no RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="83f73-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="83f73-135">No RegisterClient.m, atualize a seção `@interface` :</span><span class="sxs-lookup"><span data-stu-id="83f73-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="83f73-136">Substitua a seção `@implementation` no RegisterClient.m pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="83f73-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="83f73-137">O código acima implementa a lógica explicada no artigo de orientação [Registrando-se a partir do back-end do seu aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) , utilizando NSURLSession para realizar chamadas de REST para o back-end do seu aplicativo e NSUserDefaults para armazenar localmente o registrationId retornado pelo hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="83f73-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="83f73-138">Observe que essa classe requer que a propriedade **authorizationHeader** seja configurada para funcionar adequadamente.</span><span class="sxs-lookup"><span data-stu-id="83f73-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="83f73-139">Essa propriedade é definida pela classe **ViewController** após o logon.</span><span class="sxs-lookup"><span data-stu-id="83f73-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="83f73-140">Em ViewController.h, adicione uma instrução `#import` RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="83f73-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="83f73-141">Em seguida, adicione uma declaração para o token do dispositivo e faça referência a uma instância `RegisterClient` na seção `@interface`:</span><span class="sxs-lookup"><span data-stu-id="83f73-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="83f73-142">No ViewController.m, adicione uma declaração de método privado à seção `@interface` :</span><span class="sxs-lookup"><span data-stu-id="83f73-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="83f73-143">O trecho a seguir não é um esquema de autenticação seguro, você deve substituir a implementação de **createAndSetAuthenticationHeaderWithUsername:AndPassword:** pelo seu mecanismo de autenticação específico que gera um token de autenticação a ser consumido pela classe de cliente do registro, por exemplo, OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83f73-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="83f73-144">Em seguida, na seção `@implementation` do ViewController.m, adicione o seguinte código que adiciona a implementação para definir o cabeçalho de autenticação e o token do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83f73-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="83f73-145">Observe como a configuração do token do dispositivo ativa o botão de logon.</span><span class="sxs-lookup"><span data-stu-id="83f73-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="83f73-146">Isso ocorre porque, como parte da ação de logon, o controlador de exibição se registra para notificações por push no back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83f73-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="83f73-147">Portanto, não queremos que ação de Login seja acessível até que o token do dispositivo seja configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="83f73-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="83f73-148">É possível desacoplar o login do registro push desde que a primeira opção ocorra antes da última citada.</span><span class="sxs-lookup"><span data-stu-id="83f73-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="83f73-149">Em ViewController.m, use os trechos de código a seguir para implementar o método de ação em seu botão de **Fazer Logon** e um método para enviar a mensagem de notificação usando o back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="83f73-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="83f73-150">(IBAction) LogInAction: remetente (id) {/ / criar cabeçalho de autenticação e defini-la no cliente de registro NSString * nome de usuário = auto. UsernameField.text;   Senha NSString * = auto. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="83f73-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="83f73-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="83f73-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="83f73-152">__weak ViewController * selfie = auto;   [self.registerClient registerWithDeviceToken:self.deviceToken marcas: nil andCompletion:^(NSError* error) {Se (! erro) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = Sim;               [self MessageBox:@"Success" message:@"Registered com êxito!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="83f73-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="83f73-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="83f73-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="83f73-154">Passar a marca pns e nome de usuário como parâmetros com a URL do REST para o back-end do ASP.NET NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="83f73-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="83f73-155">Solicitação de NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [solicitação setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="83f73-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="83f73-156">Obter a simulação authenticationheader do registro de cliente NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [solicitação setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="83f73-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="83f73-157">Adicionar o corpo da mensagem de notificação [solicitação setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [solicitação setHTTPBody: [mensagem dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="83f73-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="83f73-158">Execute a API REST de notificação de envio no dataTask NSURLSessionDataTask de back-end ASP.NET * = [sessão dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) resposta;        Se (erro | | httpResponse.statusCode! = 200) {NSString* status = [NSString stringWithFormat:@"Error Status para % @: % d\nError: %@\n", pns, httpResponse.statusCode, erro];            dispatch_async(dispatch_get_main_queue(), ^ {/ / anexar texto porque todas as chamadas PNS 3 também podem ter informações para exibição [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="83f73-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="83f73-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="83f73-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="83f73-160">Atualizar a ação para o botão **Enviar notificação** para usar o back-end do ASP.NET e enviar a qualquer PNS habilitado por um comutador.</span><span class="sxs-lookup"><span data-stu-id="83f73-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="83f73-161">Na função **ViewDidLoad**, adicione o código a seguir para instanciar a instância RegisterClient e definir o delegado para os seus campos de texto.</span><span class="sxs-lookup"><span data-stu-id="83f73-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="83f73-162">Agora, em **AppDelegate.m**, remova todo o conteúdo do método **application:didRegisterForPushNotificationWithDeviceToken:** e substitua-o pelo seguinte para se certificar de que o controlador de exibição contenha o token de dispositivo mais recente, recuperado de APNs:</span><span class="sxs-lookup"><span data-stu-id="83f73-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="83f73-163">Por fim, em **AppDelegate.m**, verifique se você tem o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="83f73-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="83f73-164">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="83f73-164">Test the Application</span></span>
1. <span data-ttu-id="83f73-165">No XCode, execute o aplicativo em um dispositivo iOS físico (as notificações por push não funcionarão no simulador).</span><span class="sxs-lookup"><span data-stu-id="83f73-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="83f73-166">Na interface do usuário do aplicativo iOS, insira um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="83f73-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="83f73-167">Eles podem ser qualquer cadeia de caracteres, mas devem ter o mesmo valor da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="83f73-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="83f73-168">Em seguida, clique em **Fazer logon**.</span><span class="sxs-lookup"><span data-stu-id="83f73-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="83f73-169">Você deverá ver um pop-up informando sobre o sucesso da inscrição.</span><span class="sxs-lookup"><span data-stu-id="83f73-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="83f73-170">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="83f73-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="83f73-171">No campo de texto **Marca de nome de usuário do destinatário* , insira a marca de nome de usuário usada com o registro de outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83f73-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="83f73-172">Digite uma mensagem de notificação e clique em **Enviar notificação**.</span><span class="sxs-lookup"><span data-stu-id="83f73-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="83f73-173">Somente os dispositivos que têm um registro com a marca de nome de usuário do destinatário recebem a mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="83f73-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="83f73-174">Isso é enviado somente aos usuários.</span><span class="sxs-lookup"><span data-stu-id="83f73-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
