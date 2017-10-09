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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="1fbda-104">Notificar usuários nos Hubs de Notificação do Azure para iOS com o back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="1fbda-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="1fbda-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1fbda-105">Overview</span></span>
<span data-ttu-id="1fbda-106">Suporte de notificação por push no Azure permite que você tooaccess uma fácil de usar, multiplatform e infraestrutura de envio expandido, o que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas.</span><span class="sxs-lookup"><span data-stu-id="1fbda-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="1fbda-107">Este tutorial mostra como toouse Hubs de notificação do Azure toosend envio usuário de aplicativo específico de tooa notificações em um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="1fbda-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="1fbda-108">Um back-end ASP.NET WebAPI é usado tooauthenticate clientes e notificações de toogenerate, conforme mostrado no tópico de orientação Olá [registro do seu back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="1fbda-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="1fbda-109">Este tutorial presume que você criou e configurou o seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1fbda-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="1fbda-110">Este tutorial também é toohello pré-requisito Olá [proteger Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fbda-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="1fbda-111">Se desejar que os aplicativos móveis toouse como seu serviço de back-end, consulte Olá [Mobile aplicativos começar com envio por Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="1fbda-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="1fbda-112">Modificar seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="1fbda-112">Modify your iOS app</span></span>
1. <span data-ttu-id="1fbda-113">Olá abrir página única visualizar o aplicativo criado no hello [Introdução aos Hubs de notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fbda-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1fbda-114">Nesta seção, presumimos que você configurou seu projeto com um nome de organização vazio.</span><span class="sxs-lookup"><span data-stu-id="1fbda-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="1fbda-115">Caso contrário, será necessário tooprepend seus nomes de classe de tooall de nome de organização.</span><span class="sxs-lookup"><span data-stu-id="1fbda-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="1fbda-116">No seu Main.storyboard Adicione componentes de saudação mostrados na captura de tela hello abaixo na biblioteca de objetos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="1fbda-117">**Nome de usuário**: UITextField um com o texto do espaço reservado, *digitar nome de usuário*, imediatamente abaixo Olá enviar rótulo de resultados e toohello restrita à esquerda e direita margens e abaixo Olá enviar rótulo de resultados.</span><span class="sxs-lookup"><span data-stu-id="1fbda-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="1fbda-118">**Senha**: UITextField um com o texto do espaço reservado, *digite a senha*, imediatamente abaixo Olá campo de texto de nome de usuário e toohello restrita à esquerda e direita margens e abaixo do campo de texto de nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="1fbda-119">Verificar Olá **segura de entrada de texto** opção Olá Inspetor de atributo, em *chave retornar*.</span><span class="sxs-lookup"><span data-stu-id="1fbda-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="1fbda-120">**Faça logon no**: UIButton um rotulada imediatamente abaixo do campo de texto de senha hello e desmarque Olá **habilitado** opção Olá Inspetor de atributos em *conteúdo de controle*</span><span class="sxs-lookup"><span data-stu-id="1fbda-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="1fbda-121">**WNS**: rótulo e o envio de tooenable do comutador hello notificação de serviço de notificação do Windows se ele foi configurado no hub de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="1fbda-122">Consulte Olá [guia de Introdução do Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fbda-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="1fbda-123">**GCM**: rótulo e o envio de tooenable do comutador hello notificação tooGoogle mensagens de nuvem se ele foi configurado no hub de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="1fbda-124">Consulte o tutorial [Introdução ao Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="1fbda-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="1fbda-125">**APNS**: rótulo e o envio de tooenable do comutador hello notificação toohello serviço de notificação de plataforma Apple.</span><span class="sxs-lookup"><span data-stu-id="1fbda-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="1fbda-126">**Recipent Username**: UITextField um com o texto do espaço reservado, *marca de nome de usuário do destinatário*, imediatamente abaixo Olá GCM rótulo e toohello restrita à direita e esquerda margens e abaixo Olá GCM do rótulo.</span><span class="sxs-lookup"><span data-stu-id="1fbda-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="1fbda-127">Alguns componentes foram adicionados em Olá [Introdução aos Hubs de notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fbda-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="1fbda-128">**CTRL** arraste de componentes de saudação do hello exibição tooViewController.h e adicione essas novas saídas.</span><span class="sxs-lookup"><span data-stu-id="1fbda-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
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
2. <span data-ttu-id="1fbda-129">Em ViewController.h, adicione o seguinte Olá `#define` logo abaixo as instruções de importação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="1fbda-130">Olá substituto *< Inserir ponto de extremidade de back-end que seu\>*  espaço reservado com hello usado toodeploy seu back-end do aplicativo na seção anterior de saudação do URL de destino.</span><span class="sxs-lookup"><span data-stu-id="1fbda-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="1fbda-131">Por exemplo, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="1fbda-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="1fbda-132">No seu projeto, criar um novo **Cocoa Touch classe** chamado **RegisterClient** toointerface com hello back-end do ASP.NET é criado.</span><span class="sxs-lookup"><span data-stu-id="1fbda-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="1fbda-133">Criar classe Olá herdando `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="1fbda-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="1fbda-134">Em seguida, adicione Olá Olá RegisterClient.h código a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fbda-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="1fbda-135">Olá RegisterClient.m atualizar Olá `@interface` seção:</span><span class="sxs-lookup"><span data-stu-id="1fbda-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="1fbda-136">Substituir saudação `@implementation` seção Olá RegisterClient.m com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fbda-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="1fbda-137">código de saudação acima implementa a lógica de saudação explicada no artigo de diretrizes Olá [registro do seu back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) usando NSURLSession tooperform REST chama back-end de aplicativo tooyour e NSUserDefaults toolocally repositório Olá registrationId retornado pelo hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="1fbda-138">Observe que essa classe requer sua propriedade **authorizationHeader** toobe definido em ordem toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="1fbda-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="1fbda-139">Essa propriedade é definida pelo Olá **ViewController** classe depois Olá login.</span><span class="sxs-lookup"><span data-stu-id="1fbda-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="1fbda-140">Em ViewController.h, adicione uma instrução `#import` RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="1fbda-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="1fbda-141">Em seguida, adicione uma declaração de token de dispositivo hello e referência tooa `RegisterClient` instância no hello `@interface` seção:</span><span class="sxs-lookup"><span data-stu-id="1fbda-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="1fbda-142">No ViewController.m, adicione uma declaração de método particular em Olá `@interface` seção:</span><span class="sxs-lookup"><span data-stu-id="1fbda-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="1fbda-143">Olá trecho a seguir não é um esquema de autenticação segura, você deve substituir a implementação de saudação do hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** com o mecanismo de autenticação específico Isso gera um toobe de token de autenticação consumida por Olá registro de classe de cliente, por exemplo, OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1fbda-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="1fbda-144">Em seguida, em Olá `@implementation` seção ViewController.m adicionar Olá código que adiciona a implementação de saudação do cabeçalho de token e autenticação de dispositivo de saudação do configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fbda-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="1fbda-145">Observe como o token de configuração do dispositivo Olá permite Olá no botão de logon.</span><span class="sxs-lookup"><span data-stu-id="1fbda-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="1fbda-146">Isso ocorre porque como parte da ação de logon hello, controlador de exibição Olá registra para notificações de push com o back-end de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1fbda-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="1fbda-147">Portanto, não queremos Log na ação toobe acessível até que o token do dispositivo Olá tiver sido configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="1fbda-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="1fbda-148">É possível desacoplar Olá login de registro de push hello como antiga Olá ocorre antes de saudação último.</span><span class="sxs-lookup"><span data-stu-id="1fbda-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="1fbda-149">Em ViewController.m, use Olá após o método de ação de saudação trechos de código tooimplement para o **logon** botão e um método toosend Olá mensagem de notificação usando Olá back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1fbda-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="1fbda-150">(IBAction) LogInAction: remetente (id) {/ / criar cabeçalho de autenticação e defini-la no cliente de registro NSString * nome de usuário = auto. UsernameField.text;   Senha NSString * = auto. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="1fbda-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="1fbda-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="1fbda-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="1fbda-152">__weak ViewController * selfie = auto;   [self.registerClient registerWithDeviceToken:self.deviceToken marcas: nil andCompletion:^(NSError* error) {Se (! erro) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = Sim;               [self MessageBox:@"Success" message:@"Registered com êxito!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="1fbda-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="1fbda-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="1fbda-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="1fbda-154">Passar marca Olá de pns e o nome de usuário como parâmetros com hello URL do REST toohello ASP.NET back-end NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="1fbda-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="1fbda-155">Solicitação de NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [solicitação setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="1fbda-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="1fbda-156">Obter authenticationheader simulações de saudação do cliente de registro Olá NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [solicitação setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="1fbda-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="1fbda-157">Adicionar o corpo da mensagem de notificação Olá [solicitação setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [solicitação setHTTPBody: [mensagem dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="1fbda-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="1fbda-158">Executar notificação de envio de saudação API REST em Olá NSURLSessionDataTask de back-end ASP.NET * dataTask = [sessão dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Erro) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) resposta;        Se (erro | | httpResponse.statusCode! = 200) {NSString* status = [NSString stringWithFormat:@"Error Status para % @: % d\nError: %@\n", pns, httpResponse.statusCode, erro];            dispatch_async(dispatch_get_main_queue(), ^ {/ / anexar texto porque todas as chamadas PNS 3 também podem ter informações tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="1fbda-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="1fbda-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="1fbda-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="1fbda-160">Atualizar ação Olá Olá **enviar notificação** botão back-end ASP.NET de saudação toouse e enviar tooany PNS habilitado por um comutador.</span><span class="sxs-lookup"><span data-stu-id="1fbda-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="1fbda-161">Na função **ViewDidLoad**, adicione Olá instância de RegisterClient Olá tooinstantiate a seguir e defina o delegado Olá para os campos de texto.</span><span class="sxs-lookup"><span data-stu-id="1fbda-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="1fbda-162">Agora em **appdelegate. M**, remova todo o conteúdo de saudação do método hello **aplicativo: didRegisterForPushNotificationWithDeviceToken:** e substitua-o com hello toomake a seguir se Olá exibição controlador contém o token de dispositivo mais recente Olá recuperado do APNs:</span><span class="sxs-lookup"><span data-stu-id="1fbda-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="1fbda-163">Por fim na **appdelegate. M**, certifique-se de ter Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fbda-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="1fbda-164">Saudação de teste aplicativo</span><span class="sxs-lookup"><span data-stu-id="1fbda-164">Test hello Application</span></span>
1. <span data-ttu-id="1fbda-165">No XCode, execute o aplicativo hello em um dispositivo iOS físicos (push de notificações não funcionará no simulador Olá).</span><span class="sxs-lookup"><span data-stu-id="1fbda-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="1fbda-166">No aplicativo do iOS Olá da interface do usuário, digite um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="1fbda-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="1fbda-167">Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá mesmo valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1fbda-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="1fbda-168">Em seguida, clique em **Fazer logon**.</span><span class="sxs-lookup"><span data-stu-id="1fbda-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="1fbda-169">Você deverá ver um pop-up informando sobre o sucesso da inscrição.</span><span class="sxs-lookup"><span data-stu-id="1fbda-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="1fbda-170">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fbda-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="1fbda-171">Em hello **marca de nome de usuário do destinatário* texto campo, digite Olá etiqueta de nome de usuário usada com o registro de saudação de outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fbda-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="1fbda-172">Digite uma mensagem de notificação e clique em **Enviar notificação**.</span><span class="sxs-lookup"><span data-stu-id="1fbda-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="1fbda-173">Somente os dispositivos de saudação que tem um registro com marca de nome de usuário destinatário Olá recebem a mensagem de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fbda-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="1fbda-174">Ela só é enviada toothose usuários.</span><span class="sxs-lookup"><span data-stu-id="1fbda-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
