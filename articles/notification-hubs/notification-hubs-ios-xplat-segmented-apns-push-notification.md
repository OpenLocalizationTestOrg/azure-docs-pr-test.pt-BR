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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar Hubs de notificação toosend últimas notícias
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Visão geral
Este tópico mostra como toouse Hubs de notificação do Azure toobroadcast últimas notícias notificações tooan aplicativo iOS. Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias. Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse neles, por exemplo, o leitor de RSS, aplicativos para ventiladores de música, etc.

Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação. Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação. Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência. Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Pré-requisitos
Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação][get-started]. Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].

## <a name="add-category-selection-toohello-app"></a>Adicionar aplicativo de toohello de seleção de categoria
Olá primeira etapa é tooadd Olá da interface do usuário elementos tooyour storyboard existente que permitem Olá usuário tooselect categorias tooregister. categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação. Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.

1. No seu MainStoryboard_iPhone.storyboard adicione Olá componentes a seguir na biblioteca de objetos de saudação:
   
   * Um rótulo com o texto "Breaking News",
   * Rótulos com os textos das categorias "World", "Politics", "Business", "Technology", "Science", "Sports",
   * Seis opções, um por categoria, defina cada comutador **estado** toobe **Off** por padrão.
   * Um botão rotulado "Assinar"
     
     O storyboard deve ter a seguinte aparência:
     
     ![][3]
2. No editor de assistente Olá, criar saídas para todos os comutadores hello e chamá-los "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"
3. Crie uma Ação para o botão chamado "subscribe". O ViewController.h deve conter o seguinte hello:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Criar um novo **Cocoa Touch Class** chamado `Notifications`. Copie Olá código na seção de interface de saudação do arquivo hello Notifications.h a seguir:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Adicione Olá tooNotifications.m de diretiva de importação a seguir:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Copie Olá código na seção de implementação de saudação do arquivo hello Notifications.m a seguir.
   
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



    Essa classe usa toostore do armazenamento local e recuperar as categorias de saudação de notícias receberá este dispositivo. Além disso, ele contém tooregister um método para estas categorias usando uma [modelo](notification-hubs-templates-cross-platform-push-messages.md) registro.

1. No arquivo de appdelegate. H Olá, adicione uma instrução de importação para Notifications.h e adicionar uma propriedade de uma instância da classe de notificações de saudação:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. Em Olá **didFinishLaunchingWithOptions** método appdelegate. M, Adicionar instância de notificações de saudação do hello código tooinitialize no início de saudação do método hello.  
   
    `HUBNAME`e `HUBLISTENACCESS` (definido em hubinfo.h) já deve ter Olá `<hub name>` e `<connection string with listen access>` espaços reservados são substituídos pela notificação hub nome e hello conexão cadeia de caracteres para *DefaultListenSharedAccessSignature*que você obteve anteriormente
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente. Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações. chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.
   > 
   > 
3. Em Olá **didRegisterForRemoteNotificationsWithDeviceToken** método appdelegate. M, substitua o código de saudação no método hello com hello classe notificações toohello token de dispositivo do código toopass Olá a seguir. classe de notificações de saudação executará Olá se registrar para notificações com categorias de saudação. Se o usuário Olá altera as seleções de categoria, podemos chamar hello `subscribeWithCategories` método na resposta toohello **assinar** botão tooupdate-los.
   
   > [!NOTE]
   > Porque o token do dispositivo Olá atribuída pelo serviço de notificação por Push da Apple (APNS) da saudação pode alterada a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação. Este exemplo registra para notificação sempre que o aplicativo hello for iniciado. Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.
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

    Observe que agora não deve haver nenhum outro código no hello **didRegisterForRemoteNotificationsWithDeviceToken** método.

1. Olá métodos a seguir já devem estar presentes no appdelegate. M conclusão Olá [começar com Hubs de notificação] [ get-started] tutorial.  Caso contrário, adicione-os.
   
    -(void) MessageBox:(NSString *) título mensagem:(NSString *) messageText {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * aplicativo (void):(UIApplication *) aplicativo didReceiveRemoteNotification: (NSDictionary *) userInfo {NSLog (@"% @", userInfo);   [self MessageBox:@"Notification" mensagem: [[userInfo objectForKey:@"aps]" valueForKey:@"alert"]]; }
   
   Esse método manipula notificações recebidas quando está executando o aplicativo hello, exibindo um simples **UIAlert**.
2. Em ViewController.m, adicione uma instrução de importação para Olá appdelegate. H e cópia de código a seguir em Olá XCode gerado **assinar** método. Esse código atualizará Olá notificação registro toouse Olá novos rótulos de categoria Olá usuário escolheu na interface de usuário de saudação.
   
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
   
   Esse método cria um **NSMutableArray** de categorias e usa hello **notificações** lista de saudação toostore classe Olá local armazenamento registra Olá correspondente marcas e com o hub de notificação. Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.
3. Em ViewController.m, adicione Olá Olá código a seguir **viewDidLoad** interface de usuário do método tooset Olá com base nas categorias de saudação salva anteriormente.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



aplicativo Hello agora pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que inicia o aplicativo hello.  usuário Olá pode alterar a seleção Olá das categorias no tempo de execução e clique em Olá **assinar** registro de saudação do método tooupdate para dispositivo hello. Em seguida, você atualizará Olá Olá de toosend aplicativo últimas notificações de notícias diretamente no próprio aplicativo hello.

## <a name="optional-sending-tagged-notifications"></a>(opcional) Enviando notificações marcadas
Se você não tiver acesso tooVisual Studio, você pode ignorar toohello próxima seção e enviar notificações de aplicativo hello em si. Você também pode enviar notificação de modelo apropriado de saudação do Olá [Portal clássico do Azure] usando o guia de depuração Olá para o hub de notificação. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(opcional) Enviar notificações de dispositivo Olá
Normalmente as notificações podem ser enviadas por um serviço de back-end, mas você pode enviar notificações das últimas notícias diretamente do aplicativo hello. toodo isso atualizaremos Olá `SendNotificationRESTAPI` método que definimos no hello [começar com Hubs de notificação] [ get-started] tutorial.

1. Em ViewController.m atualização Olá `SendNotificationRESTAPI` método como segue para que ele aceita um parâmetro de marca de categoria hello e envia Olá adequada [modelo](notification-hubs-templates-cross-platform-push-messages.md) notificação.
   
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
2. Em ViewController.m atualização Olá **enviar notificação** ação conforme mostrado no código de saudação que segue. Para que ele envie notificações hello usando cada marca individualmente e enviar toomultiple plataformas.

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



1. Recrie seu projeto e verifique se não há nenhum erro de compilação.

## <a name="run-hello-app-and-generate-notifications"></a>Execute o aplicativo hello e geram notificações
1. Olá pressione executar botão toobuild Olá projeto e inicie o aplicativo hello. Selecione alguns tooand de toosubscribe opções últimas notícias e pressione Olá **assinar** botão. Você deve ver uma caixa de diálogo indicando Olá assinou notificações.
   
    ![][1]
   
    Quando você escolhe **assinar**, Olá categorias do aplicativo converte Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação.
2. Insira um toobe mensagem enviada como notícias mais recentes, em seguida, pressione Olá **enviar notificação** botão. Como alternativa, execute as notificações de toogenerate aplicativo de console .NET hello.
   
    ![][2]
3. Notícias de toobreaking cada dispositivo assinado receberá notificações das Olá últimas notícias que você acabou de ser enviado.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, nós aprendemos como toobroadcast últimas notícias por categoria. Considere a concluir uma saudação tutoriais que realçam outros cenários avançados de Hubs de notificação a seguir:

* **[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]**
  
    Saiba como Olá tooexpand últimas notícias aplicativo tooenable enviar localizado notificações.

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
