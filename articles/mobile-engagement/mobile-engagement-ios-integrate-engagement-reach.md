---
title: "aaaAzure Mobile Engagement iOS SDK alcançar integração | Microsoft Docs"
description: "Atualizações e procedimentos mais recentes para o SDK do iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>Como tooIntegrate contrato alcançam no iOS
Você deve seguir Olá integração procedimento descrito em Olá [como tooIntegrate contrato no documento de iOS](mobile-engagement-ios-integrate-engagement.md) antes de seguir este guia.

Esta documentação requer o XCode 8. Se você realmente depende XCode 7, você pode usar o hello [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh). Há um bug conhecido nesta versão anterior durante a execução em dispositivos com iOS 10: as notificações de sistema não são acionadas. toofix isso você terá tooimplement Olá preterido API `application:didReceiveRemoteNotification:` em seu aplicativo delegar da seguinte maneira:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Não recomendamos essa solução alternativa** pois esse comportamento pode alterar qualquer atualização da versão futura iOS (até mesmo pequenas) porque esta API do iOS foi preterida. Você deve alternar tooXCode 8 assim que possível.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Habilitar seu aplicativo tooreceive silenciosa notificações por Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Etapas de integração
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Inserir saudação SDK do Reach contrato em seu projeto do iOS
* Adicione o sdk de alcance Olá no seu projeto Xcode. No Xcode, vá muito**projeto \> adicionar tooproject** e escolha Olá `EngagementReach` pasta.

### <a name="modify-your-application-delegate"></a>Modifique seu Representante do Aplicativo
* Na parte superior de saudação do seu arquivo de implementação, importe o módulo de alcance do contrato de hello:

      [...]
      #import "AEReachModule.h"
* No método `applicationDidFinishLaunching:` ou `application:didFinishLaunchingWithOptions:`, crie um módulo de alcance e passá-lo tooyour linha de inicialização contrato existente:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Modificar **'icon.png'** cadeia de caracteres com o nome da imagem Olá desejado como o ícone de notificação.
* Se você quiser toouse Olá opção *valor de notificação de atualização* em campanhas de alcance ou se você quiser que o push nativo toouse \<API/campanha de SaaS/alcance formato/nativo Push\> campanhas, você deve permitir que o módulo de alcance Olá gerenciar Olá ícone de notificação em si (ele será limpa automaticamente a notificação de aplicativo hello e também redefinir o valor de saudação armazenado pelo contrato sempre que o aplicativo hello é iniciado ou foregrounded). Isso é feito adicionando Olá seguinte linha após a inicialização do módulo de alcance:

      [reach setAutoBadgeEnabled:YES];
* Se você quiser toohandle alcance dados por push, você deverá permitir que seu representante do aplicativo está de acordo com toohello `AEReachDataPushDelegate` protocolo. Adicione Olá seguinte linha após a inicialização do módulo de alcance:

      [reach setDataPushDelegate:self];
* Em seguida, você pode implementar métodos Olá `onDataPushStringReceived:` e `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` em seu representante do aplicativo:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Categoria
o parâmetro de categoria Olá é opcional quando você criar uma campanha de envio de dados e permite que você toofilter dados envia. Isso é útil se você quiser toopush diferentes tipos de `Base64` tooidentify de dados e desejar que seu tipo antes da análise-los.

**Seu aplicativo está agora pronto tooreceive e exibição acessar conteúdo!**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Como tooreceive anúncios e controla a qualquer momento
Contrato pode enviar notificações de alcançar os usuários finais de tooyour a qualquer momento usando Olá Apple Push Notification Service.

tooenable essa funcionalidade, será tooprepare seu aplicativo para notificações de push da Apple e modificar seu representante do aplicativo.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Preparar seu aplicativo para notificações de push da Apple
Siga o guia de saudação: [como tooPrepare seu aplicativo para notificações de Push da Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Adicione código de cliente necessário Olá
*Agora seu aplicativo deve ter um certificado do Apple push registrado no front-end Olá contrato.*

Se ele não ainda tiver feito isso, você precisa tooregister suas notificações de push de tooreceive do aplicativo.

* Saudação de importação `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Adicionar Olá linha a seguir na inicialização do aplicativo (normalmente em `application:didFinishLaunchingWithOptions:`):

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

Em seguida, você precisa de token do dispositivo tooprovide tooEngagement hello retornada pelos servidores da Apple. Isso é feito no método hello chamado `application:didRegisterForRemoteNotificationsWithDeviceToken:` em seu representante do aplicativo:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Por fim, você tem tooinform Olá SDK Engagement quando seu aplicativo recebe uma notificação remota. toodo que chamam Olá método `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` em seu representante do aplicativo:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> Por padrão, o contrato alcançar controles completionHandler hello. Se você quiser toomanually responder toohello `handler` bloco no seu código, você pode passar nulo para Olá `handler` argumento e controle de conclusão de saudação bloquear por conta própria. Consulte Olá `UIBackgroundFetchResult` tipo para obter uma lista de valores possíveis.
>
>

### <a name="full-example"></a>Exemplo completo
Aqui está um exemplo completo de integração:

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolver conflitos de delegado UNUserNotificationCenter

*Se o aplicativo nem uma das bibliotecas de terceiros implementar um `UNUserNotificationCenterDelegate`, ignore esta parte.*

Um `UNUserNotificationCenter` delegado é usado pelo ciclo de vida de Olá Olá SDK toomonitor de notificações de compromisso em dispositivos que executam o iOS 10 ou superior. Olá SDK tem sua própria implementação de saudação `UNUserNotificationCenterDelegate` de protocolo, mas pode haver apenas um `UNUserNotificationCenter` delegar por aplicativo. Qualquer outro representante adicionado toohello `UNUserNotificationCenter` objeto está em conflito com hello contrato um. Se Olá SDK detectar delegado do seu ou qualquer outra parte, em seguida, ele não usará sua própria implementação toogive você tooresolve uma chance Olá conflitos. Você terá tooadd Olá contrato lógica tooyour possui delegado em ordem tooresolve conflitos de saudação.

Há dois tooachieve de maneiras isso.

Proposta 1, encaminhando o delegado chama toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Ou proposta 2, herdando de saudação `AEUserNotificationHandler` classe

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Você pode determinar se uma notificação de contrato ou não passando seus `userInfo` toohello dicionário agente `isEngagementPushPayload:` método de classe.

Certifique-se de que Olá `UNUserNotificationCenter` representante do objeto é definido tooyour delegado em qualquer Olá `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` método do seu representante de aplicativo.
Por exemplo, se você tiver implementado Olá acima proposta 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a>Como campanhas toocustomize
### <a name="notifications"></a>Notificações
Há dois tipos de notificações: notificações de sistema e no aplicativo.

As notificações do sistema são tratadas pelo iOS e não podem ser personalizadas.

Notificações no aplicativo são feitas de um modo de exibição que é adicionado dinamicamente toohello janela atual do aplicativo. Isso é chamado uma sobreposição de notificação. Sobreposições de notificação são ótimas para uma integração rápida porque eles não requerem que você toomodify qualquer exibição em seu aplicativo.

#### <a name="layout"></a>Layout
aparência de saudação toomodify das suas notificações no aplicativo, você pode modificar simplesmente arquivo hello `AENotificationView.xib` tooyour precisa, como manter valores de marca hello e tipos de sub-visualizações existente hello.

Por padrão, as notificações no aplicativo são apresentadas na parte inferior da saudação da tela hello. Se você preferir toodisplay-los na parte superior de saudação da tela, editar Olá fornecido `AENotificationView.xib` e alterar Olá `AutoSizing` propriedade do modo de exibição de saudação principal para que ele pode ser mantido na parte superior de saudação da sua visão ampla do.

#### <a name="categories"></a>Categorias
Quando você modifica Olá fornecido layout, você modificar a aparência de saudação de todas as notificações. As categorias permitem que toodefine que vários direcionados parece (possivelmente comportamentos) para notificações. Uma categoria pode ser especificada quando você cria uma campanha de Reach. Tenha em mente que categorias também permitem personalizar anúncios e pesquisas, como está descrito mais adiante neste documento.

tooregister um manipulador de categoria para as notificações, você precisa tooadd uma chamada quando Olá alcançar o módulo é inicializada.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`deve ser uma instância de um objeto que está em conformidade com o protocolo toohello `AENotifier`.

Você pode implementar métodos de protocolo hello sozinho ou você pode escolher uma classe existente de saudação tooreimplement `AEDefaultNotifier` que já executa a maioria do trabalho de saudação.

Por exemplo, se você quiser tooredefine exibição de notificação de saudação para uma categoria específica, você pode seguir este exemplo:

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

Esse exemplo simples de categoria pressupõem que você tenha um arquivo chamado `MyNotificationView.xib` no pacote de aplicativo principal. Se o método hello não é capaz de toofind correspondente `.xib`, notificação de saudação não será exibida e contrato produzirá uma mensagem no console de saudação.

Olá fornecido nib arquivo deve respeitar Olá regras a seguir:

* Ele deve conter apenas um modo de exibição.
* Sub-visualizações devem ser de saudação mesmo tipos como Olá aquelas dentro Olá fornecido nib arquivo chamado`AENotificationView.xib`
* Sub-visualizações devem ter Olá mesmo marcas como Olá aquelas dentro Olá fornecido nib arquivo chamado`AENotificationView.xib`

> [!TIP]
> Apenas copie o arquivo de ponta de Olá fornecido, denominado `AENotificationView.xib`e começar a trabalhar a partir daí. Mas tenha cuidado, Olá exibição dentro desse arquivo nib é associada a classe toohello `AENotificationView`. Essa classe redefinido método hello `layoutSubViews` toomove e redimensione seus sub-visualizações toocontext de acordo com. Talvez você queira tooreplace-lo com um `UIView` ou classe do modo de exibição personalizado.
>
>

Se você precisar de personalização mais profunda das suas notificações (se você desejar para a instância tooload sua exibição diretamente no código de saudação), é recomendável tootake examinar Olá fornecida documentação de código e a classe de origem de `Protocol ReferencesDefaultNotifier` e `AENotifier`.

Observe que você pode usar Olá Notificador mesmo para várias categorias.

Você pode Notificador de padrão de saudação também redefinido como este:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Tratamento de notificação
Ao usar a categoria de padrão de saudação, alguns métodos de ciclo de vida são chamados em Olá `AEReachContent` tooreport estatísticas e atualização Olá campanha o estado do objeto:

* Quando a notificação de saudação é exibida no aplicativo, Olá `displayNotification` método é chamado (que relata estatísticas) por `AEReachModule` se `handleNotification:` retorna `YES`.
* Se a notificação de saudação é ignorada, Olá `exitNotification` método é chamado, a estatística é relatada e campanhas Avançar agora podem ser processadas.
* Se a notificação de saudação é clicada, `actionNotification` é chamado, a estatística é relatada e Olá associado ação é executada.

Se sua implementação de `AENotifier` bypasses Olá comportamento padrão, você terá que toocall esses métodos de ciclo de vida por si mesmo. Olá exemplos a seguir ilustra alguns casos em que o comportamento padrão de saudação é ignorado:

* Você não precisa estender `AEDefaultNotifier`, por exemplo, você implementou o tratamento de categoria a partir do zero.
* Você substitui `prepareNotificationView:forContent:`, ser toomap-se de que pelo menos `onNotificationActioned` ou `onNotificationExited` tooone dos controles U.I.

> [!WARNING]
> Se `handleNotification:` lançará uma exceção, Olá conteúdo será excluído e `drop` é chamado, isso é relatado nas estatísticas e campanhas Avançar agora podem ser processadas.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Incluir notificação como parte de uma exibição existente
Sobreposições são ótimas para uma integração rápida, mas podem não ser convenientes algumas vezes ou podem ter efeitos colaterais indesejados.

Se você não estiver satisfeito com o sistema de sobreposição de saudação em alguns dos seus modos de exibição, você pode personalizá-lo para esses modos de exibição.

Você pode decidir tooinclude nosso layout de notificação em exibições existentes. toodo assim, há dois estilos de implementação:

1. Adicionar exibição de notificação hello usando o construtor de interface

   * Abra o *Interface Builder*
   * Insere um 320 x 60 (ou 60 x 768 se você estiver no iPad) `UIView` onde você deseja Olá notificação tooappear
   * Defina o valor de marca de saudação para esta exibição muito: **36822491**
2. Adicione exibição de notificação Olá programaticamente. Basta adicione Olá código a seguir quando o modo de exibição foi inicializado:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

A macro `NOTIFICATION_AREA_VIEW_TAG` pode ser encontrada em `AEDefaultNotifier.h`.

> [!NOTE]
> Notificador de padrão de saudação detecta automaticamente o layout de notificação que Olá incluído nessa exibição e não adicionará uma sobreposição para ele.
>
>

### <a name="announcements-and-polls"></a>Anúncios e pesquisas
#### <a name="layouts"></a>Layouts
Você pode modificar arquivos Olá `AEDefaultAnnouncementView.xib` e `AEDefaultPollView.xib` como manter valores de marca hello e tipos de sub-visualizações existente hello.

#### <a name="categories"></a>Categorias
##### <a name="alternate-layouts"></a>Layouts alternativos
Como as notificações, categoria da campanha Olá pode ser usado toohave de layouts alternativos para suas notificações e pesquisas.

toocreate uma categoria para um aviso, você deve estender **AEAnnouncementViewController** e registrá-lo depois que o módulo de alcance Olá foi inicializado:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Cada vez que um usuário clique em uma notificação para um aviso com a categoria de hello "meu\_categoria", o controlador de exibição registrados (nesse caso `MyCustomAnnouncementViewController`) será inicializado chamando o método hello `initWithAnnouncement:` e modo de exibição de saudação adicionado toohello a janela atual do aplicativo.
>
>

Na implementação de saudação `AEAnnouncementViewController` classe, você terá a propriedade de saudação tooread `announcement` tooinitialize seu sub-visualizações. Considere o exemplo hello abaixo, onde dois rótulos são inicializados usando `title` e `body` propriedades de saudação `AEReachAnnouncement` classe:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Se você não deseja tooload suas exibições sozinho, mas você quiser apenas o layout de exibição do tooreuse saudação padrão comunicado, você pode simplesmente fazer seu controlador de modo de exibição personalizado estende classe Olá fornecido `AEDefaultAnnouncementViewController`. Duplicar nesse caso, o arquivo de ponta de saudação `AEDefaultAnnouncementView.xib` e renomeá-lo para que possam ser carregados pelo controlador de modo de exibição personalizado (para um controlador chamado `CustomAnnouncementViewController`, você deve chamar o arquivo nib `CustomAnnouncementView.xib`).

categoria de padrão de saudação tooreplace de anúncios, simplesmente registrar controlador de modo de exibição personalizado para categoria Olá definido em `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Pesquisas podem ser personalizado Olá mesma maneira:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Esse tempo, Olá fornecido `MyCustomPollViewController` deve estender `AEPollViewController`. Ou você pode escolher tooextend do controlador de padrão de saudação: `AEDefaultPollViewController`.

> [!IMPORTANT]
> Não se esqueça de toocall ou `action` (`submitAnswers:` para controladores de exibição de pesquisa personalizada) ou `exit` método antes de controlador de exibição de saudação é descartada. Caso contrário, as estatísticas não serão enviadas (ou seja, nenhuma análise campanha Olá) e mais importante Avançar campanhas não serão notificadas até que o processo de aplicativo hello seja reiniciado.
>
>

##### <a name="implementation-example"></a>Exemplo de implementação
Essa implementação de exibição de notificação personalizada Olá é carregada de um arquivo externo xib.

Como personalização avançada de notificação, é recomendável toolook no código-fonte da implementação padrão Olá Olá.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
