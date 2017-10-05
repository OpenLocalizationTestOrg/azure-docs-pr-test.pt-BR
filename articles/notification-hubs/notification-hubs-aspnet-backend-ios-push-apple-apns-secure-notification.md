---
title: "Push Seguro dos Hubs de Notificação do Azure"
description: "Saiba como enviar notificações por push seguro para um aplicativo iOS do Azure. Exemplos de códigos escritos em Objective-C e c#."
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
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="f7316-104">Push Seguro dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="f7316-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7316-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f7316-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="f7316-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f7316-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="f7316-107">Android</span><span class="sxs-lookup"><span data-stu-id="f7316-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f7316-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f7316-108">Overview</span></span>
<span data-ttu-id="f7316-109">O suporte à notificação por push no Microsoft Azure permite que você acesse uma infraestrutura de envio por push fácil de usar, multiplataforma e expansível que simplifica em muito a implementação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="f7316-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="f7316-110">Devido a restrições regulatórias ou de segurança, às vezes, um aplicativo pode querer incluir algo na notificação que não pode ser transmitido por meio da infraestrutura de notificação por push padrão.</span><span class="sxs-lookup"><span data-stu-id="f7316-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="f7316-111">Este tutorial descreve como obter a mesma experiência ao enviar informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo cliente e o back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7316-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="f7316-112">Em um nível superior, o fluxo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7316-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="f7316-113">O back-end do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="f7316-113">The app back-end:</span></span>
   * <span data-ttu-id="f7316-114">Armazena uma carga segura no banco de dados de back-end.</span><span class="sxs-lookup"><span data-stu-id="f7316-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="f7316-115">Envia a ID dessa notificação ao dispositivo (nenhuma informação segura é enviada).</span><span class="sxs-lookup"><span data-stu-id="f7316-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="f7316-116">O dispositivo no aplicativo, ao receber a notificação:</span><span class="sxs-lookup"><span data-stu-id="f7316-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="f7316-117">O dispositivo entra em contato com o back-end solicitando a carga segura.</span><span class="sxs-lookup"><span data-stu-id="f7316-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="f7316-118">O aplicativo pode mostrar a carga como uma notificação no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7316-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="f7316-119">É importante observar que no fluxo anterior (e neste tutorial), pressupomos que o dispositivo armazena um token de autenticação no armazenamento local depois que o usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="f7316-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="f7316-120">Isso garante uma experiência perfeita  já que o dispositivo pode recuperar a carga de segurança da notificação usando este token.</span><span class="sxs-lookup"><span data-stu-id="f7316-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="f7316-121">Se o seu aplicativo não armazenar tokens de autenticação no dispositivo, ou se esses tokens puderem expirar, o aplicativo do dispositivo, após receber a notificação, deve exibir uma notificação genérica solicitando que o usuário inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7316-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="f7316-122">Dessa forma, o aplicativo autentica o usuário e mostra a carga de notificação.</span><span class="sxs-lookup"><span data-stu-id="f7316-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="f7316-123">Este tutorial de Push Seguro mostra como enviar uma notificação por push de maneira segura.</span><span class="sxs-lookup"><span data-stu-id="f7316-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="f7316-124">O tutorial baseia-se no tutorial [Notificação de usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) , por isso, você deve concluir as etapas nesse tutorial primeiro.</span><span class="sxs-lookup"><span data-stu-id="f7316-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="f7316-125">Este tutorial presume que você criou e configurou o seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f7316-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="f7316-126">Modificar o projeto iOS</span><span class="sxs-lookup"><span data-stu-id="f7316-126">Modify the iOS project</span></span>
<span data-ttu-id="f7316-127">Agora que você modificou o back-end do aplicativo para enviar apenas a *ID* de uma notificação, é preciso alterar o aplicativo iOS para manipular essa notificação e retornar a chamada do back-end para recuperar a mensagem segura a ser exibida.</span><span class="sxs-lookup"><span data-stu-id="f7316-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="f7316-128">Para isso, precisamos gravar a lógica para recuperar o conteúdo seguro do back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7316-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="f7316-129">Em **AppDelegate.m**, verifique se o aplicativo registra para notificações silenciosas para processar a id de notificação enviada do back-end.</span><span class="sxs-lookup"><span data-stu-id="f7316-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="f7316-130">Adicione a opção **UIRemoteNotificationTypeNewsstandContentAvailability** em didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="f7316-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="f7316-131">No **AppDelegate.m** , adicione uma seção de implementação no topo, com a seguinte declaração:</span><span class="sxs-lookup"><span data-stu-id="f7316-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="f7316-132">Em seguida, adicione o código a seguir à seção de implementação, substituindo o espaço reservado `{back-end endpoint}` pelo ponto de extremidade para seu back-end obtido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f7316-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="f7316-133">Agora, precisamos manipular a notificação de entrada e utilizar o método acima para recuperar o conteúdo a ser exibido.</span><span class="sxs-lookup"><span data-stu-id="f7316-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="f7316-134">Primeiro, precisamos habilitar o aplicativo iOS para ser executado em segundo plano ao receber uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="f7316-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="f7316-135">Em **XCode**, selecione seu projeto de aplicativo no painel à esquerda e depois clique no seu destino de aplicativo principal na seção **Destinos** do painel central.</span><span class="sxs-lookup"><span data-stu-id="f7316-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="f7316-136">Então, clique na guia **Recursos** na parte superior do painel central e marque a caixa de seleção **Notificações Remotas**.</span><span class="sxs-lookup"><span data-stu-id="f7316-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="f7316-137">Em **AppDelegate.m** , adicione o método a seguir para manipular notificações por push:</span><span class="sxs-lookup"><span data-stu-id="f7316-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
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
   
    <span data-ttu-id="f7316-138">Observe que é preferível manipular os casos de propriedade de cabeçalho de autenticação ausente ou de rejeição por meio do back-end.</span><span class="sxs-lookup"><span data-stu-id="f7316-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="f7316-139">A manipulação específica desses casos depende em grande parte da sua meta de experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7316-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="f7316-140">Uma opção é exibir uma notificação com um aviso genérico para que o usuário realize a autenticação para recuperar a notificação real.</span><span class="sxs-lookup"><span data-stu-id="f7316-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f7316-141">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7316-141">Run the Application</span></span>
<span data-ttu-id="f7316-142">Para executar o aplicativo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7316-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="f7316-143">No XCode, execute o aplicativo em um dispositivo iOS físico (as notificações por push não funcionarão no simulador).</span><span class="sxs-lookup"><span data-stu-id="f7316-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="f7316-144">Na interface do usuário do aplicativo iOS, insira um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="f7316-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="f7316-145">Pode ser qualquer cadeia de caracteres, mas elas devem ter o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="f7316-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="f7316-146">Na interface do usuário do aplicativo iOS, clique em **Logon**.</span><span class="sxs-lookup"><span data-stu-id="f7316-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="f7316-147">Em seguida, clique em **Enviar push**.</span><span class="sxs-lookup"><span data-stu-id="f7316-147">Then click **Send push**.</span></span> <span data-ttu-id="f7316-148">Você deve ver a notificação segura sendo exibida no centro de notificações.</span><span class="sxs-lookup"><span data-stu-id="f7316-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
