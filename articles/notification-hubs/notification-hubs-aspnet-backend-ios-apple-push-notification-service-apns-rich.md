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
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="d77a0-104">Push Avançado dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="d77a0-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="d77a0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d77a0-105">Overview</span></span>
<span data-ttu-id="d77a0-106">Em ordem tooengage os usuários com conteúdo rich instantâneo, um aplicativo pode querer toopush além do texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="d77a0-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="d77a0-107">Essas notificações promovem interações do usuário e apresentam conteúdo, como urls, sons, imagens/cupons e muito mais.</span><span class="sxs-lookup"><span data-stu-id="d77a0-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="d77a0-108">Este tutorial baseia-se em Olá [notificar usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tópico e mostra como toosend enviar notificações por push que incorporam cargas (por exemplo, a imagem).</span><span class="sxs-lookup"><span data-stu-id="d77a0-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="d77a0-109">Este tutorial é compatível com iOS 7 e 8.</span><span class="sxs-lookup"><span data-stu-id="d77a0-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="d77a0-110">Em um alto nível:</span><span class="sxs-lookup"><span data-stu-id="d77a0-110">At a high level:</span></span>

1. <span data-ttu-id="d77a0-111">saudação de aplicativos back-end:</span><span class="sxs-lookup"><span data-stu-id="d77a0-111">hello app backend:</span></span>
   * <span data-ttu-id="d77a0-112">Repositórios Olá carga avançada (nesse caso, a imagem) no armazenamento de banco de dados/local de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="d77a0-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="d77a0-113">Envia a ID do dispositivo toohello notificação avançada</span><span class="sxs-lookup"><span data-stu-id="d77a0-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="d77a0-114">Aplicativo no dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="d77a0-114">App on hello device:</span></span>
   * <span data-ttu-id="d77a0-115">Contatos Olá solicitando a carga avançados Olá com a ID de saudação recebe de back-end</span><span class="sxs-lookup"><span data-stu-id="d77a0-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="d77a0-116">Envia notificações de usuários no dispositivo hello quando a recuperação de dados estiver concluída e mostra a carga de saudação imediatamente quando os usuários tocam em toolearn mais</span><span class="sxs-lookup"><span data-stu-id="d77a0-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="d77a0-117">Projeto WebAPI</span><span class="sxs-lookup"><span data-stu-id="d77a0-117">WebAPI Project</span></span>
1. <span data-ttu-id="d77a0-118">No Visual Studio, abra Olá **AppBackend** projeto que você criou no hello [notificar usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d77a0-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="d77a0-119">Obtenha uma imagem que você deseja toonotify aos usuários e colocá-la em um **img** pasta no diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="d77a0-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="d77a0-120">Clique em **Mostrar todos os arquivos** em Olá Gerenciador de soluções e clique pasta Olá muito**incluir no projeto**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="d77a0-121">Com imagem Olá selecionada, altere sua ação de compilação na janela Propriedades muito**recurso inserido**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="d77a0-122">Em **Notifications.cs**, adicione o seguinte Olá usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="d77a0-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="d77a0-123">Saudação de atualização inteira **notificações** classe com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d77a0-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="d77a0-124">Ser tooreplace se espaços reservados de saudação com suas credenciais de hub de notificação e o nome do arquivo de imagem.</span><span class="sxs-lookup"><span data-stu-id="d77a0-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
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
   > <span data-ttu-id="d77a0-125">(opcional) Consulte também[como tooembed e acessar recursos usando o Visual C#](http://support.microsoft.com/kb/319292) para obter mais informações sobre como tooadd e obter os recursos de projeto.</span><span class="sxs-lookup"><span data-stu-id="d77a0-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="d77a0-126">Em **NotificationsController.cs**, redefinir **NotificationsController** com hello trechos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d77a0-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="d77a0-127">Isso envia um toodevice de id de notificação avançada silenciosa inicial e permite a recuperação do lado do cliente da imagem:</span><span class="sxs-lookup"><span data-stu-id="d77a0-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
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
8. <span data-ttu-id="d77a0-128">Agora podemos reimplantar esta tooan aplicativo site do Azure em ordem toomake-lo acessível de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d77a0-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="d77a0-129">Clique duas vezes em Olá **AppBackend** do projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="d77a0-130">Selecione o Site do Azure como seu destino de publicação.</span><span class="sxs-lookup"><span data-stu-id="d77a0-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="d77a0-131">Faça logon com sua conta do Azure e selecione um site novo ou existente e anote Olá **URL de destino** propriedade Olá **Conexão** guia. Chamaremos toothis URL como o *ponto de extremidade de back-end* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d77a0-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="d77a0-132">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="d77a0-133">Modificar o projeto do iOS Olá</span><span class="sxs-lookup"><span data-stu-id="d77a0-133">Modify hello iOS project</span></span>
<span data-ttu-id="d77a0-134">Agora que você tenha modificado o hello apenas do aplicativo back-end toosend *id* de uma notificação, você alterará o toohandle de aplicativo do iOS essa id e recuperar mensagem avançados de saudação do seu back-end.</span><span class="sxs-lookup"><span data-stu-id="d77a0-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="d77a0-135">Abra seu projeto de iOS e habilitar notificações remotas pelo destino de aplicativo principal de tooyour indo em Olá **destinos** seção.</span><span class="sxs-lookup"><span data-stu-id="d77a0-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="d77a0-136">Clique em **recursos**, ativar **modos de segundo plano**e verifique Olá **remoto notificações** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="d77a0-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="d77a0-137">Vá muito**Main.storyboard**e certifique-se de ter um controlador de exibição (mencionado tooas início View Controller neste tutorial) de [notificar o usuário](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d77a0-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="d77a0-138">Adicionar um **navegação controlador** tooyour de storyboard e arraste controle tooHome View Controller toomake-Olá **exibição de raiz** de navegação.</span><span class="sxs-lookup"><span data-stu-id="d77a0-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="d77a0-139">Verifique se Olá **é inicial View Controller** em atributos Inspetor é selecionado para Olá somente no controlador de navegação.</span><span class="sxs-lookup"><span data-stu-id="d77a0-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="d77a0-140">Adicionar um **View Controller** toostoryboard e adicione um **imagem**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="d77a0-141">Isso é página Olá os usuários verão quando desejarem toolearn mais clicando no notifiication Olá.</span><span class="sxs-lookup"><span data-stu-id="d77a0-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="d77a0-142">O storyboard deve ter a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="d77a0-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="d77a0-143">Clique em Olá **início View Controller** no storyboard e verifique se ele possui **homeViewController** como seu **classe personalizada** e **Storyboard ID**em Inspetor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="d77a0-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="d77a0-144">Olá mesmo para o controlador de exibição de imagem como **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="d77a0-145">Em seguida, crie uma nova classe de controlador de exibição denominada **imageViewController** toohandle Olá interface de usuário que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="d77a0-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="d77a0-146">Em **imageViewController.h**, adicionar Olá declarações de interface do controlador toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="d77a0-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="d77a0-147">Verifique se toocontrol e arraste da saudação storyboard imagem exibição toothese propriedades toolink Olá dois:</span><span class="sxs-lookup"><span data-stu-id="d77a0-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="d77a0-148">Em **imageViewController.m**, adicione o seguinte de saudação final Olá **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="d77a0-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="d77a0-149">Em **appdelegate. M**, controlador de imagem Olá importação criada:</span><span class="sxs-lookup"><span data-stu-id="d77a0-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="d77a0-150">Adicione uma seção de interface com hello declaração a seguir:</span><span class="sxs-lookup"><span data-stu-id="d77a0-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="d77a0-151">Em **AppDelegate**, verifique se o aplicativo se registra para notificações silenciosas em **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="d77a0-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="d77a0-152">SUBSTITUTE em Olá após a implementação para **aplicativo: didRegisterForRemoteNotificationsWithDeviceToken** tootake storyboard de saudação alterações de interface do usuário em conta:</span><span class="sxs-lookup"><span data-stu-id="d77a0-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="d77a0-153">Em seguida, adicione Olá métodos a seguir muito**appdelegate. M** tooretrieve Olá imagem do ponto de extremidade e enviar uma notificação local quando a recuperação for concluída.</span><span class="sxs-lookup"><span data-stu-id="d77a0-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="d77a0-154">Certifique-se de espaço reservado de saudação de toosubstitute `{backend endpoint}` com seu ponto de extremidade de back-end:</span><span class="sxs-lookup"><span data-stu-id="d77a0-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
3. <span data-ttu-id="d77a0-155">Lidar com a notificação local Olá acima através da abertura de controlador de exibição de imagem Olá no **appdelegate. M** com hello métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d77a0-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="d77a0-156">Executar Olá aplicativo</span><span class="sxs-lookup"><span data-stu-id="d77a0-156">Run hello Application</span></span>
1. <span data-ttu-id="d77a0-157">No XCode, execute o aplicativo hello em um dispositivo iOS físicos (push de notificações não funcionará no simulador Olá).</span><span class="sxs-lookup"><span data-stu-id="d77a0-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="d77a0-158">No aplicativo do iOS Olá da interface do usuário, insira um nome de usuário e a senha da saudação mesmo valor para a autenticação e clique em **logon**.</span><span class="sxs-lookup"><span data-stu-id="d77a0-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="d77a0-159">Clique em **Enviar por push** e você verá um alerta no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d77a0-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="d77a0-160">Se você clicar em **mais**, será colocado toohello imagem escolhida tooinclude no seu back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d77a0-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="d77a0-161">Você também pode clicar em **enviar por push** e pressione o botão página inicial de saudação do seu dispositivo imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d77a0-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="d77a0-162">Em alguns momentos, você receberá uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="d77a0-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="d77a0-163">Se você tocar nela ou clique em mais, você será levado tooyour conteúdo da imagem avançados do aplicativo e hello.</span><span class="sxs-lookup"><span data-stu-id="d77a0-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
