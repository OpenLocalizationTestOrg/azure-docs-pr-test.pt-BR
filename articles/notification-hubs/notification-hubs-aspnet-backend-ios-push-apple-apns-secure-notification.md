---
title: "aaaAzure notificação Hubs seguro Push"
description: "Saiba como toosend segura envio notificações tooan iOS aplicativo do Azure. Exemplos de códigos escritos em Objective-C e c#."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="34f36-104">Push Seguro dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="34f36-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34f36-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="34f36-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="34f36-106">iOS</span><span class="sxs-lookup"><span data-stu-id="34f36-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="34f36-107">Android</span><span class="sxs-lookup"><span data-stu-id="34f36-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="34f36-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="34f36-108">Overview</span></span>
<span data-ttu-id="34f36-109">Suporte de notificação por push no Microsoft Azure permite que você tooaccess uma infraestrutura de push de fácil de usar, multiplataforma, dimensionável, que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas.</span><span class="sxs-lookup"><span data-stu-id="34f36-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="34f36-110">Devido a restrições de segurança ou tooregulatory, às vezes, um aplicativo pode ser conveniente tooinclude algo na notificação de saudação que não pode ser transmitida por meio da infraestrutura de notificação por push padrão hello.</span><span class="sxs-lookup"><span data-stu-id="34f36-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="34f36-111">Este tutorial descreve como tooachieve Olá a mesma experiência, enviando informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo de cliente hello e back-end de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="34f36-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="34f36-112">Em um nível alto, o fluxo de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="34f36-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="34f36-113">Olá aplicativo back-end:</span><span class="sxs-lookup"><span data-stu-id="34f36-113">hello app back-end:</span></span>
   * <span data-ttu-id="34f36-114">Armazena uma carga segura no banco de dados de back-end.</span><span class="sxs-lookup"><span data-stu-id="34f36-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="34f36-115">Envia a ID de saudação do dispositivo toohello notificação (nenhuma informação de segurança é enviada).</span><span class="sxs-lookup"><span data-stu-id="34f36-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="34f36-116">Olá o aplicativo no dispositivo hello, ao receber a notificação de saudação:</span><span class="sxs-lookup"><span data-stu-id="34f36-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="34f36-117">dispositivo Olá contata Olá back-end solicitante Olá carga de segurança.</span><span class="sxs-lookup"><span data-stu-id="34f36-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="34f36-118">aplicativo Hello pode mostrar carga hello como uma notificação no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="34f36-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="34f36-119">É importante toonote em Olá anterior fluxo (e, neste tutorial), vamos supor que o dispositivo Olá armazena um token de autenticação no armazenamento local, depois Olá usuário fizer logon.</span><span class="sxs-lookup"><span data-stu-id="34f36-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="34f36-120">Isso garante uma experiência completamente, como dispositivo Olá pode recuperar a carga de segurança da notificação hello usando este token.</span><span class="sxs-lookup"><span data-stu-id="34f36-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="34f36-121">Se seu aplicativo não armazenar os tokens de autenticação no dispositivo hello, ou se esses tokens podem ser expirados, hello aplicativo de dispositivo, ao receber a notificação de saudação deve exibir uma notificação genérica solicitando Olá usuário toolaunch Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34f36-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="34f36-122">aplicativo Hello, em seguida, autentica o usuário hello e mostra a carga de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="34f36-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="34f36-123">Este tutorial seguro Push mostra como toosend uma notificação por push com segurança.</span><span class="sxs-lookup"><span data-stu-id="34f36-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="34f36-124">Olá tutorial baseia-se em Olá [notificar usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, portanto você deve concluir as etapas de saudação neste tutorial primeiro.</span><span class="sxs-lookup"><span data-stu-id="34f36-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="34f36-125">Este tutorial presume que você criou e configurou o seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="34f36-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="34f36-126">Modificar o projeto do iOS Olá</span><span class="sxs-lookup"><span data-stu-id="34f36-126">Modify hello iOS project</span></span>
<span data-ttu-id="34f36-127">Agora que você modificou o Olá apenas de toosend de back-end do aplicativo *id* de uma notificação, você tem toochange seu toohandle de aplicativo do iOS que notificação e o retorno de chamada hello seu back-end tooretrieve Proteja toobe mensagem exibida.</span><span class="sxs-lookup"><span data-stu-id="34f36-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="34f36-128">tooachieve essa meta, temos toowrite Olá lógica tooretrieve Olá conteúdo seguro do que Olá back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34f36-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="34f36-129">Em **appdelegate. M**, verifique se registros de aplicativo hello silenciosa notificações para que ele processa a id de notificação de saudação enviada de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="34f36-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="34f36-130">Adicionar Olá **UIRemoteNotificationTypeNewsstandContentAvailability** opção didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="34f36-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="34f36-131">No seu **appdelegate. M** adicionar uma seção de implementação na parte superior da saudação com hello declaração a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f36-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="34f36-132">Adicione ao Olá Olá de seção de implementação código a seguir, substituindo o espaço reservado de saudação `{back-end endpoint}` com ponto de extremidade Olá para o back-end obtido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="34f36-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. <span data-ttu-id="34f36-133">Agora temos toohandle notificação de entrada hello e usar o método hello acima tooretrieve Olá conteúdo toodisplay.</span><span class="sxs-lookup"><span data-stu-id="34f36-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="34f36-134">Primeiro, temos tooenable seu toorun de aplicativo do iOS no plano de fundo de saudação ao receber uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="34f36-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="34f36-135">Em **XCode**, selecione o projeto de aplicativo no painel esquerdo do hello, clique em seu destino de aplicativo principal no hello **destinos** seção no painel central hello.</span><span class="sxs-lookup"><span data-stu-id="34f36-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="34f36-136">Em seguida, clique em seu **recursos** guia na parte superior de saudação do seu painel central e verifique Olá **remoto notificações** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="34f36-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="34f36-137">Em **appdelegate. M** adicionar Olá notificações de push toohandle método a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f36-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="34f36-138">Observe que é preferível toohandle casos de saudação de propriedade de cabeçalho de autenticação ausente ou rejeição por Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="34f36-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="34f36-139">tratamento específico de Olá desses casos dependem principalmente em sua experiência de usuário de destino.</span><span class="sxs-lookup"><span data-stu-id="34f36-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="34f36-140">Uma opção é toodisplay uma notificação com um aviso genérico para Olá tooauthenticate tooretrieve Olá real notificação ao usuário.</span><span class="sxs-lookup"><span data-stu-id="34f36-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="34f36-141">Executar Olá aplicativo</span><span class="sxs-lookup"><span data-stu-id="34f36-141">Run hello Application</span></span>
<span data-ttu-id="34f36-142">toorun Olá aplicativo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f36-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="34f36-143">No XCode, execute o aplicativo hello em um dispositivo iOS físicos (push de notificações não funcionará no simulador Olá).</span><span class="sxs-lookup"><span data-stu-id="34f36-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="34f36-144">No aplicativo do iOS Olá da interface do usuário, digite um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="34f36-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="34f36-145">Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="34f36-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="34f36-146">No aplicativo do iOS Olá da interface do usuário, clique em **login**.</span><span class="sxs-lookup"><span data-stu-id="34f36-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="34f36-147">Em seguida, clique em **Enviar push**.</span><span class="sxs-lookup"><span data-stu-id="34f36-147">Then click **Send push**.</span></span> <span data-ttu-id="34f36-148">Você deve ver a notificação de seguro hello está sendo exibida no seu centro de notificação.</span><span class="sxs-lookup"><span data-stu-id="34f36-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
