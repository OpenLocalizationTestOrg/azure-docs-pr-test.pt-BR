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
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="b8bb4-103">Registrar usuário atual de saudação para notificações por push, usando ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b8bb4-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8bb4-104">iOS</span><span class="sxs-lookup"><span data-stu-id="b8bb4-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b8bb4-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b8bb4-105">Overview</span></span>
<span data-ttu-id="b8bb4-106">Este tópico mostra como toorequest envio de registro de notificação com Hubs de notificação do Azure quando o registro é realizado pela API da Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="b8bb4-107">Este tópico estende tutorial Olá [notificar os usuários com Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="b8bb4-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="b8bb4-108">Você já deve ter concluído etapas Olá necessários no tutorial toocreate Olá autenticado serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="b8bb4-109">Para obter mais informações sobre Olá notificar o cenário de usuários, consulte [notificar os usuários com Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="b8bb4-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="b8bb4-110">Atualizar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8bb4-110">Update your app</span></span>
1. <span data-ttu-id="b8bb4-111">No seu MainStoryboard_iPhone.storyboard, adicione Olá componentes a seguir na biblioteca de objetos de saudação:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="b8bb4-112">**Rótulo**: "TooUser com Hubs de notificação de Push"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="b8bb4-113">**Label**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="b8bb4-114">**Label**: "User"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-114">**Label**: "User"</span></span>
   * <span data-ttu-id="b8bb4-115">**Text Field**: "User"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="b8bb4-116">**Label**: "Password"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="b8bb4-117">**Text Field**: "Password"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="b8bb4-118">**Button**: "Login"</span><span class="sxs-lookup"><span data-stu-id="b8bb4-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="b8bb4-119">Neste ponto, o storyboard Olá seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="b8bb4-120">No editor de assistente hello, criar tomadas para todos os controles de saudação alternada e chamá-los, conecte-se campos de texto de saudação com hello View Controller (delegado) e criar um **ação** para Olá **login** botão.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="b8bb4-121">Crie uma classe denominada **DeviceInfo**, e Olá cópia código a seguir na seção de interface de saudação do arquivo hello DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="b8bb4-122">Copie Olá código na seção de implementação de saudação do arquivo de DeviceInfo.m Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
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
5. <span data-ttu-id="b8bb4-123">No PushToUserAppDelegate.h, adicione Olá singleton de propriedade a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="b8bb4-124">Em Olá **didFinishLaunchingWithOptions** método PushToUserAppDelegate.m, adicionar Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="b8bb4-125">primeira linha de saudação inicializa Olá **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="b8bb4-126">Olá segunda linha inicia Olá registro para notificações por push, que já está presente é você já tiver concluído a saudação [começar com Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="b8bb4-127">Em PushToUserAppDelegate.m, implemente o método hello **didRegisterForRemoteNotificationsWithDeviceToken** no seu AppDelegate e adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="b8bb4-128">Isso define o token do dispositivo Olá para solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b8bb4-129">Neste ponto, não deve haver nenhum outro código nesse método.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="b8bb4-130">Se você já tiver uma chamada toohello **registerNativeWithDeviceToken** método foi adicionado quando você concluir a saudação [começar com Hubs de notificação](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, você deve comentários ou remover chamada.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="b8bb4-131">No arquivo de PushToUserAppDelegate.m de saudação, adicione Olá método do manipulador a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="b8bb4-132">aplicativo (void):(UIApplication *) aplicativo didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", userInfo);   UIAlertView * alerta = [[UIAlertView alocação] initWithTitle:@"Notification" mensagem: [userInfo objectForKey:@"inAppMessage]" delegado: nil cancelButtonTitle: @ otherButtonTitles:nil "Okey", nil];   [alerta Mostrar]; }</span><span class="sxs-lookup"><span data-stu-id="b8bb4-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="b8bb4-133">Este método exibirá um alerta em Olá da interface do usuário quando seu aplicativo recebe notificações enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="b8bb4-134">Abrir Olá PushToUserViewController.m arquivo e teclado Olá retorno em Olá implementação a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="b8bb4-135">Em Olá **viewDidLoad** método no arquivo de PushToUserViewController.m hello, inicializar o rótulo de installationId de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="b8bb4-136">Adicione Olá propriedades na interface em PushToUserViewController.m a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="b8bb4-137">Em seguida, adicione Olá implementação a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-137">Then, add hello following implementation:</span></span>
    
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
13. <span data-ttu-id="b8bb4-138">Código a seguir de saudação de cópia em Olá **login** criado pelo XCode de método do manipulador:</span><span class="sxs-lookup"><span data-stu-id="b8bb4-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
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
    
    <span data-ttu-id="b8bb4-139">Esse método obtém uma ID de instalação e o canal para notificações por push e enviá-la, junto com o tipo de dispositivo hello, toohello autenticada método de API da Web que cria um registro em Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="b8bb4-140">Essa API Web foi definida em [notificar os usuários com Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="b8bb4-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="b8bb4-141">Agora que hello aplicativo cliente foi atualizado, retornar toohello [notificar os usuários com Hubs de notificação] e atualizar as notificações de toosend de serviço móvel hello usando Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="b8bb4-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificar os usuários com Hubs de notificação]: /manage/services/notification-hubs/notify-users-aspnet

[começar com Hubs de notificação]: /manage/services/notification-hubs/get-started-notification-hubs-ios
