---
title: "aaaNotification Hubs últimas notícias Tutorial - iOS"
description: "Saiba como toouse Hubs de notificação de barramento de serviço do Azure toosend recentes dispositivos de tooiOS de notificações de notícias."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="83c3e-103">Usar Hubs de notificação toosend últimas notícias</span><span class="sxs-lookup"><span data-stu-id="83c3e-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="83c3e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="83c3e-104">Overview</span></span>
<span data-ttu-id="83c3e-105">Este tópico mostra como toouse Hubs de notificação do Azure toobroadcast últimas notícias notificações tooan aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="83c3e-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="83c3e-106">Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="83c3e-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="83c3e-107">Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse neles, por exemplo, o leitor de RSS, aplicativos para ventiladores de música, etc.</span><span class="sxs-lookup"><span data-stu-id="83c3e-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="83c3e-108">Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="83c3e-109">Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="83c3e-110">Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência.</span><span class="sxs-lookup"><span data-stu-id="83c3e-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="83c3e-111">Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="83c3e-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83c3e-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83c3e-112">Prerequisites</span></span>
<span data-ttu-id="83c3e-113">Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="83c3e-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="83c3e-114">Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="83c3e-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="83c3e-115">Adicionar aplicativo de toohello de seleção de categoria</span><span class="sxs-lookup"><span data-stu-id="83c3e-115">Add category selection toohello app</span></span>
<span data-ttu-id="83c3e-116">Olá primeira etapa é tooadd Olá da interface do usuário elementos tooyour storyboard existente que permitem Olá usuário tooselect categorias tooregister.</span><span class="sxs-lookup"><span data-stu-id="83c3e-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="83c3e-117">categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="83c3e-118">Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.</span><span class="sxs-lookup"><span data-stu-id="83c3e-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="83c3e-119">No seu MainStoryboard_iPhone.storyboard adicione Olá componentes a seguir na biblioteca de objetos de saudação:</span><span class="sxs-lookup"><span data-stu-id="83c3e-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="83c3e-120">Um rótulo com o texto "Breaking News",</span><span class="sxs-lookup"><span data-stu-id="83c3e-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="83c3e-121">Rótulos com os textos das categorias "World", "Politics", "Business", "Technology", "Science", "Sports",</span><span class="sxs-lookup"><span data-stu-id="83c3e-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="83c3e-122">Seis opções, um por categoria, defina cada comutador **estado** toobe **Off** por padrão.</span><span class="sxs-lookup"><span data-stu-id="83c3e-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="83c3e-123">Um botão rotulado "Assinar"</span><span class="sxs-lookup"><span data-stu-id="83c3e-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="83c3e-124">O storyboard deve ter a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="83c3e-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="83c3e-125">No editor de assistente Olá, criar saídas para todos os comutadores hello e chamá-los "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="83c3e-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="83c3e-126">Crie uma Ação para o botão chamado "subscribe".</span><span class="sxs-lookup"><span data-stu-id="83c3e-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="83c3e-127">O ViewController.h deve conter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="83c3e-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="83c3e-128">Criar um novo **Cocoa Touch Class** chamado `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="83c3e-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="83c3e-129">Copie Olá código na seção de interface de saudação do arquivo hello Notifications.h a seguir:</span><span class="sxs-lookup"><span data-stu-id="83c3e-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="83c3e-130">Adicione Olá tooNotifications.m de diretiva de importação a seguir:</span><span class="sxs-lookup"><span data-stu-id="83c3e-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="83c3e-131">Copie Olá código na seção de implementação de saudação do arquivo hello Notifications.m a seguir.</span><span class="sxs-lookup"><span data-stu-id="83c3e-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="83c3e-132">Essa classe usa toostore do armazenamento local e recuperar as categorias de saudação de notícias receberá este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83c3e-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="83c3e-133">Além disso, ele contém tooregister um método para estas categorias usando uma [modelo](notification-hubs-templates-cross-platform-push-messages.md) registro.</span><span class="sxs-lookup"><span data-stu-id="83c3e-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="83c3e-134">No arquivo de appdelegate. H Olá, adicione uma instrução de importação para Notifications.h e adicionar uma propriedade de uma instância da classe de notificações de saudação:</span><span class="sxs-lookup"><span data-stu-id="83c3e-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="83c3e-135">Em Olá **didFinishLaunchingWithOptions** método appdelegate. M, Adicionar instância de notificações de saudação do hello código tooinitialize no início de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="83c3e-136">`HUBNAME`e `HUBLISTENACCESS` (definido em hubinfo.h) já deve ter Olá `<hub name>` e `<connection string with listen access>` espaços reservados são substituídos pela notificação hub nome e hello conexão cadeia de caracteres para *DefaultListenSharedAccessSignature*que você obteve anteriormente</span><span class="sxs-lookup"><span data-stu-id="83c3e-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="83c3e-137">Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="83c3e-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="83c3e-138">Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="83c3e-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="83c3e-139">chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.</span><span class="sxs-lookup"><span data-stu-id="83c3e-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="83c3e-140">Em Olá **didRegisterForRemoteNotificationsWithDeviceToken** método appdelegate. M, substitua o código de saudação no método hello com hello classe notificações toohello token de dispositivo do código toopass Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="83c3e-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="83c3e-141">classe de notificações de saudação executará Olá se registrar para notificações com categorias de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="83c3e-142">Se o usuário Olá altera as seleções de categoria, podemos chamar hello `subscribeWithCategories` método na resposta toohello **assinar** botão tooupdate-los.</span><span class="sxs-lookup"><span data-stu-id="83c3e-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83c3e-143">Porque o token do dispositivo Olá atribuída pelo serviço de notificação por Push da Apple (APNS) da saudação pode alterada a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="83c3e-144">Este exemplo registra para notificação sempre que o aplicativo hello for iniciado.</span><span class="sxs-lookup"><span data-stu-id="83c3e-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="83c3e-145">Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="83c3e-146">Observe que agora não deve haver nenhum outro código no hello **didRegisterForRemoteNotificationsWithDeviceToken** método.</span><span class="sxs-lookup"><span data-stu-id="83c3e-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="83c3e-147">Olá métodos a seguir já devem estar presentes no appdelegate. M conclusão Olá [começar com Hubs de notificação] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="83c3e-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="83c3e-148">Caso contrário, adicione-os.</span><span class="sxs-lookup"><span data-stu-id="83c3e-148">If not, add them.</span></span>
   
    <span data-ttu-id="83c3e-149">-(void) MessageBox:(NSString *) título mensagem:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="83c3e-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="83c3e-150">}</span><span class="sxs-lookup"><span data-stu-id="83c3e-150">}</span></span>
   
   * <span data-ttu-id="83c3e-151">aplicativo (void):(UIApplication *) aplicativo didReceiveRemoteNotification: (NSDictionary *) userInfo {NSLog (@"% @", userInfo);   [self MessageBox:@"Notification" mensagem: [[userInfo objectForKey:@"aps]" valueForKey:@"alert"]]; }</span><span class="sxs-lookup"><span data-stu-id="83c3e-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="83c3e-152">Esse método manipula notificações recebidas quando está executando o aplicativo hello, exibindo um simples **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="83c3e-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="83c3e-153">Em ViewController.m, adicione uma instrução de importação para Olá appdelegate. H e cópia de código a seguir em Olá XCode gerado **assinar** método.</span><span class="sxs-lookup"><span data-stu-id="83c3e-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="83c3e-154">Esse código atualizará Olá notificação registro toouse Olá novos rótulos de categoria Olá usuário escolheu na interface de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="83c3e-155">Esse método cria um **NSMutableArray** de categorias e usa hello **notificações** lista de saudação toostore classe Olá local armazenamento registra Olá correspondente marcas e com o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="83c3e-156">Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="83c3e-157">Em ViewController.m, adicione Olá Olá código a seguir **viewDidLoad** interface de usuário do método tooset Olá com base nas categorias de saudação salva anteriormente.</span><span class="sxs-lookup"><span data-stu-id="83c3e-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="83c3e-158">aplicativo Hello agora pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que inicia o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="83c3e-159">usuário Olá pode alterar a seleção Olá das categorias no tempo de execução e clique em Olá **assinar** registro de saudação do método tooupdate para dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="83c3e-160">Em seguida, você atualizará Olá Olá de toosend aplicativo últimas notificações de notícias diretamente no próprio aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="83c3e-161">(opcional) Enviando notificações marcadas</span><span class="sxs-lookup"><span data-stu-id="83c3e-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="83c3e-162">Se você não tiver acesso tooVisual Studio, você pode ignorar toohello próxima seção e enviar notificações de aplicativo hello em si.</span><span class="sxs-lookup"><span data-stu-id="83c3e-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="83c3e-163">Você também pode enviar notificação de modelo apropriado de saudação do Olá [Portal clássico do Azure] usando o guia de depuração Olá para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="83c3e-164">(opcional) Enviar notificações de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="83c3e-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="83c3e-165">Normalmente as notificações podem ser enviadas por um serviço de back-end, mas você pode enviar notificações das últimas notícias diretamente do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="83c3e-166">toodo isso atualizaremos Olá `SendNotificationRESTAPI` método que definimos no hello [começar com Hubs de notificação] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="83c3e-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="83c3e-167">Em ViewController.m atualização Olá `SendNotificationRESTAPI` método como segue para que ele aceita um parâmetro de marca de categoria hello e envia Olá adequada [modelo](notification-hubs-templates-cross-platform-push-messages.md) notificação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. <span data-ttu-id="83c3e-168">Em ViewController.m atualização Olá **enviar notificação** ação conforme mostrado no código de saudação que segue.</span><span class="sxs-lookup"><span data-stu-id="83c3e-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="83c3e-169">Para que ele envie notificações hello usando cada marca individualmente e enviar toomultiple plataformas.</span><span class="sxs-lookup"><span data-stu-id="83c3e-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="83c3e-170">Recrie seu projeto e verifique se não há nenhum erro de compilação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="83c3e-171">Execute o aplicativo hello e geram notificações</span><span class="sxs-lookup"><span data-stu-id="83c3e-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="83c3e-172">Olá pressione executar botão toobuild Olá projeto e inicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="83c3e-173">Selecione alguns tooand de toosubscribe opções últimas notícias e pressione Olá **assinar** botão.</span><span class="sxs-lookup"><span data-stu-id="83c3e-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="83c3e-174">Você deve ver uma caixa de diálogo indicando Olá assinou notificações.</span><span class="sxs-lookup"><span data-stu-id="83c3e-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="83c3e-175">Quando você escolhe **assinar**, Olá categorias do aplicativo converte Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="83c3e-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="83c3e-176">Insira um toobe mensagem enviada como notícias mais recentes, em seguida, pressione Olá **enviar notificação** botão.</span><span class="sxs-lookup"><span data-stu-id="83c3e-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="83c3e-177">Como alternativa, execute as notificações de toogenerate aplicativo de console .NET hello.</span><span class="sxs-lookup"><span data-stu-id="83c3e-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="83c3e-178">Notícias de toobreaking cada dispositivo assinado receberá notificações das Olá últimas notícias que você acabou de ser enviado.</span><span class="sxs-lookup"><span data-stu-id="83c3e-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83c3e-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83c3e-179">Next steps</span></span>
<span data-ttu-id="83c3e-180">Neste tutorial, nós aprendemos como toobroadcast últimas notícias por categoria.</span><span class="sxs-lookup"><span data-stu-id="83c3e-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="83c3e-181">Considere a concluir uma saudação tutoriais que realçam outros cenários avançados de Hubs de notificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="83c3e-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="83c3e-182">**[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]**</span><span class="sxs-lookup"><span data-stu-id="83c3e-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="83c3e-183">Saiba como Olá tooexpand últimas notícias aplicativo tooenable enviar localizado notificações.</span><span class="sxs-lookup"><span data-stu-id="83c3e-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[Portal clássico do Azure]: https://manage.windowsazure.com
