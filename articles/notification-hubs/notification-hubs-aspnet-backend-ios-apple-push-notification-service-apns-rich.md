---
title: "Push Avançado dos Hubs de Notificação do Azure"
description: "Saiba como enviar notificações por push avançado para um aplicativo iOS do Azure. Exemplos de códigos escritos em Objective-C e c#."
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
ms.openlocfilehash: 394efdc2dfaff0666bc23d8a448b0a00d414da99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="809d8-104">Push Avançado dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="809d8-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="809d8-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="809d8-105">Overview</span></span>
<span data-ttu-id="809d8-106">Para atrair os usuários com conteúdo elaborado instantâneo, um aplicativo talvez queira enviar por push além do texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="809d8-106">In order to engage users with instant rich contents, an application might want to push beyond plain text.</span></span> <span data-ttu-id="809d8-107">Essas notificações promovem interações do usuário e apresentam conteúdo, como urls, sons, imagens/cupons e muito mais.</span><span class="sxs-lookup"><span data-stu-id="809d8-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="809d8-108">Esse tutorial se baseia no tópico [Notificar Usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) e mostra como enviar notificações por push que incorporam cargas (por exemplo, imagem).</span><span class="sxs-lookup"><span data-stu-id="809d8-108">This tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how to send push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="809d8-109">Este tutorial é compatível com iOS 7 e 8.</span><span class="sxs-lookup"><span data-stu-id="809d8-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="809d8-110">Em um alto nível:</span><span class="sxs-lookup"><span data-stu-id="809d8-110">At a high level:</span></span>

1. <span data-ttu-id="809d8-111">O back-end do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="809d8-111">The app backend:</span></span>
   * <span data-ttu-id="809d8-112">Armazena a carga avançada (nesse caso, imagem) no armazenamento de banco de dados/local do back-end</span><span class="sxs-lookup"><span data-stu-id="809d8-112">Stores the rich payload (in this case, image) in the backend database/local storage</span></span>
   * <span data-ttu-id="809d8-113">Envia a ID dessa notificação avançadas para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="809d8-113">Sends ID of this rich notification to the device</span></span>
2. <span data-ttu-id="809d8-114">Aplicativo no dispositivo:</span><span class="sxs-lookup"><span data-stu-id="809d8-114">App on the device:</span></span>
   * <span data-ttu-id="809d8-115">Entra em contato com o back-end solicitando a carga avançada com a ID recebe</span><span class="sxs-lookup"><span data-stu-id="809d8-115">Contacts the backend requesting the rich payload with the ID it receives</span></span>
   * <span data-ttu-id="809d8-116">Envia notificações de usuários no dispositivo quando a recuperação de dados estiver concluída e mostra a carga imediatamente quando os usuários toque para saber mais</span><span class="sxs-lookup"><span data-stu-id="809d8-116">Sends users notifications on the device when data retrieval is complete, and shows the payload immediately when users tap to learn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="809d8-117">Projeto WebAPI</span><span class="sxs-lookup"><span data-stu-id="809d8-117">WebAPI Project</span></span>
1. <span data-ttu-id="809d8-118">No Visual Studio, abra o projeto **AppBackend** que você criou no tutorial [Notificar Usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="809d8-118">In Visual Studio, open the **AppBackend** project that you created in the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="809d8-119">Obter uma imagem para notificar usuários e colocá-la em uma pasta **img** no diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="809d8-119">Obtain an image you would like to notify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="809d8-120">Clique em **Mostrar Todos os Arquivos** no Gerenciador de Soluções e clique com o botão direito na pasta para **Incluir no Projeto**.</span><span class="sxs-lookup"><span data-stu-id="809d8-120">Click **Show All Files** in the Solution Explorer, and right-click the folder to **Include In Project**.</span></span>
4. <span data-ttu-id="809d8-121">Com a imagem selecionada, altere sua Ação de Compilação na janela Propriedades para **Recurso Inserido**.</span><span class="sxs-lookup"><span data-stu-id="809d8-121">With the image selected, change its Build Action in Properties window to **Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="809d8-122">Em **Notifications.cs**, adicione o seguinte usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="809d8-122">In **Notifications.cs**, add the following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="809d8-123">Atualize a classe inteira de **Notificações** com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="809d8-123">Update the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="809d8-124">Certifique-se de substituir os espaços reservados por suas credenciais de hub de notificação e o nome do arquivo de imagem.</span><span class="sxs-lookup"><span data-stu-id="809d8-124">Be sure to replace the placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message to display to users
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
                // Placeholders: replace with the connection string (with full access) for your notification hub and the hub name from the Azure Classics Portal
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
   > <span data-ttu-id="809d8-125">(opcional) Confira [Como inserir e acessar recursos usando o Visual C#](http://support.microsoft.com/kb/319292) para obter mais informações sobre como adicionar e obter recursos de projeto.</span><span class="sxs-lookup"><span data-stu-id="809d8-125">(optional) Refer to [How to embed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how to add and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="809d8-126">Em **NotificationsController.cs**, redefina **NotificationsController** com os trechos a seguir.</span><span class="sxs-lookup"><span data-stu-id="809d8-126">In **NotificationsController.cs**, redefine **NotificationsController**  with the following snippets.</span></span> <span data-ttu-id="809d8-127">Isso envia uma id de notificação avançada silenciosa inicial ao dispositivo e permite a recuperação do cliente da imagem:</span><span class="sxs-lookup"><span data-stu-id="809d8-127">This sends an initial silent rich notification id to device and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) to client
        public async Task<HttpResponseMessage> Post() {
            // Replace the placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification to apns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="809d8-128">Agora, reimplantaremos esse aplicativo em um Site do Azure para torná-lo acessível a partir de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="809d8-128">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="809d8-129">Clique com o botão direito do mouse no projeto **AppBackend** e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="809d8-129">Right-click on the **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="809d8-130">Selecione o Site do Azure como seu destino de publicação.</span><span class="sxs-lookup"><span data-stu-id="809d8-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="809d8-131">Faça logon em sua conta do Azure e selecione um site novo ou existente, então anote a propriedade **URL de destino** na guia **Conexão**.</span><span class="sxs-lookup"><span data-stu-id="809d8-131">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="809d8-132">Iremos nos referir a essa URL, posteriormente neste tutorial, como seu *ponto de extremidade de back-end* .</span><span class="sxs-lookup"><span data-stu-id="809d8-132">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="809d8-133">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="809d8-133">Click **Publish**.</span></span>

## <a name="modify-the-ios-project"></a><span data-ttu-id="809d8-134">Modificar o projeto iOS</span><span class="sxs-lookup"><span data-stu-id="809d8-134">Modify the iOS project</span></span>
<span data-ttu-id="809d8-135">Agora que você modificou o back-end do aplicativo para enviar apenas a *id* de notificação, deve alterar seu aplicativo iOS para lidar com essa id e recuperar a mensagem avançada do seu back-end.</span><span class="sxs-lookup"><span data-stu-id="809d8-135">Now that you have modified your app backend to send just the *id* of a notification, you will change your iOS app to handle that id and retrieve the rich message from your backend.</span></span>

1. <span data-ttu-id="809d8-136">Abra o projeto do iOS e habilite notificações remotas indo para o destino do aplicativo principal na seção **Destinos** .</span><span class="sxs-lookup"><span data-stu-id="809d8-136">Open your iOS project, and enable remote notifications by going to your main app target in the **Targets** section.</span></span>
2. <span data-ttu-id="809d8-137">Clique em **Recursos**, ative **Modos de Segundo Plano** e marque a caixa de seleção **Notificações Remotas**.</span><span class="sxs-lookup"><span data-stu-id="809d8-137">Click on **Capabilities**, turn on **Background Modes**, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="809d8-138">Acesse **Main.storyboard**e verifique se você possui um Controlador de Exibição (indicado como Controlador de Exibição Doméstico nesse tutorial) do tutorial [Notificar Usuário](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="809d8-138">Go to **Main.storyboard**, and make sure you have a View Controller (refered to as Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="809d8-139">Adicione um **Controlador de Navegação** ao storyboard, mantenha a tecla Control pressionada e arraste para o Controlador de Exibição Doméstica para torná-lo a **visualização raiz** da navegação.</span><span class="sxs-lookup"><span data-stu-id="809d8-139">Add a **Navigation Controller** to your storyboard, and control-drag to Home View Controller to make it the **root view** of navigation.</span></span> <span data-ttu-id="809d8-140">Verifique se **É o Controlador de Exibição Inicial** no inspetor de atributos está selecionado somente para o Controlador de Navegação.</span><span class="sxs-lookup"><span data-stu-id="809d8-140">Make sure the **Is Initial View Controller** in Attributes inspector is selected for the Navigation Controller only.</span></span>
5. <span data-ttu-id="809d8-141">Adicione um **Controlador de Exibição** ao storyboard e adicione uma **Visualização de Imagem**.</span><span class="sxs-lookup"><span data-stu-id="809d8-141">Add a **View Controller** to storyboard and add an **Image View**.</span></span> <span data-ttu-id="809d8-142">Esta é a página que os usuários verão quando desejarem saber mais, clicando na notificação.</span><span class="sxs-lookup"><span data-stu-id="809d8-142">This is the page users will see once they choose to learn more by clicking on the notifiication.</span></span> <span data-ttu-id="809d8-143">O storyboard deve ter a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="809d8-143">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="809d8-144">Clique no **Controlador de Exibição Doméstica** no storyboard, verifique se tem **homeViewController** como sua **Classe Personalizada** e **ID do Storyboard** abaixo do Inspetor de identidade.</span><span class="sxs-lookup"><span data-stu-id="809d8-144">Click on the **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under the Identity inspector.</span></span>
7. <span data-ttu-id="809d8-145">Faça o mesmo para Controlador de Exibição de Imagem como **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="809d8-145">Do the same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="809d8-146">Em seguida, crie uma nova classe de Controlador de Exibição denominada **imageViewController** para lidar com a IU que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="809d8-146">Then, create a new View Controller class titled **imageViewController** to handle the UI you just created.</span></span>
9. <span data-ttu-id="809d8-147">Em **imageViewController.h**, adicione os itens abaixo às declarações de interface do controlador.</span><span class="sxs-lookup"><span data-stu-id="809d8-147">In **imageViewController.h**, add the following to the controller's interface declarations.</span></span> <span data-ttu-id="809d8-148">Certifique-se de manter Control pressionado e arrastar da exibição de imagem do storyboard para essas propriedades para vincular as duas:</span><span class="sxs-lookup"><span data-stu-id="809d8-148">Make sure to control-drag from the storyboard image view to these properties to link the two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="809d8-149">Em **imageViewController.m**, adicione o seguinte no fim de **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="809d8-149">In **imageViewController.m**, add the following at the end of **viewDidload**:</span></span>
    
        // Display the UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="809d8-150">Em **AppDelegate.m**, importe o controlador de imagem criado:</span><span class="sxs-lookup"><span data-stu-id="809d8-150">In **AppDelegate.m**, import the image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="809d8-151">Adicione uma seção de interface com a seguinte declaração:</span><span class="sxs-lookup"><span data-stu-id="809d8-151">Add an interface section with the following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect to Image View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="809d8-152">Em **AppDelegate**, verifique se o aplicativo se registra para notificações silenciosas em **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="809d8-152">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="809d8-153">Substitua na seguinte implementação para **application:didRegisterForRemoteNotificationsWithDeviceToken** para considerar as alterações de IU do storyboard:</span><span class="sxs-lookup"><span data-stu-id="809d8-153">Subsitute in the following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** to take the storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at the root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="809d8-154">Em seguida, adicione os métodos a seguir a **AppDelegate.m** pare recuperar a imagem do ponto de extremidade e enviar uma notificação local quando a recuperação estiver completa.</span><span class="sxs-lookup"><span data-stu-id="809d8-154">Then, add the following methods to **AppDelegate.m** to retrieve the image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="809d8-155">Não deixe de substituir o espaço reservado `{backend endpoint}` pelo seu ponto de extremidade do back-end:</span><span class="sxs-lookup"><span data-stu-id="809d8-155">Make sure to substitute the placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
                   // From NSData to UIImage
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
   
                       // "5" is arbitrary here to give you enough time to quit out of the app and receive push notifications
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
           // Add "else if" here to handle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="809d8-156">Trate a notificação local acima abrindo o controlador de exibição de imagem no **AppDelegate.m** com os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="809d8-156">Handle the local notification above by opening up the image view controller in **AppDelegate.m** with the following methods:</span></span>
   
       // Helper: redirect users to image view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image to image view controller
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
           // Add "else if" here to handle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-the-application"></a><span data-ttu-id="809d8-157">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="809d8-157">Run the Application</span></span>
1. <span data-ttu-id="809d8-158">No XCode, execute o aplicativo em um dispositivo iOS físico (as notificações por push não funcionarão no simulador).</span><span class="sxs-lookup"><span data-stu-id="809d8-158">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="809d8-159">Na IU de aplicativo do iOS, insira um nome de usuário e senha do mesmo valor para a autenticação e clique em **Fazer Logon**.</span><span class="sxs-lookup"><span data-stu-id="809d8-159">In the iOS app UI, enter a username and password of the same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="809d8-160">Clique em **Enviar por push** e você verá um alerta no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="809d8-160">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="809d8-161">Se você clicar em **Mais**, você será levado à imagem que optou por incluir no back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="809d8-161">If you click on **More**, you will be brought to the image you chose to include in your app backend.</span></span>
4. <span data-ttu-id="809d8-162">Você pode também clicar em **Enviar por push** e imediatamente pressionar o botão Início do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="809d8-162">You can also click **Send push** and immediately press the home button of your device.</span></span> <span data-ttu-id="809d8-163">Em alguns momentos, você receberá uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="809d8-163">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="809d8-164">Se você tocar nela ou clicar em Mais, será levado para seu aplicativo e o conteúdo da imagem avançado.</span><span class="sxs-lookup"><span data-stu-id="809d8-164">If you tap on it or click More, you will be brought to your app and the rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
