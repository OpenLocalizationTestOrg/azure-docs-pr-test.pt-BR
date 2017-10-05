---
title: "Enviar notificações por Push seguro com Hubs de Notificação do Azure"
description: "Saiba como enviar notificações por push seguro para um aplicativo Android do Azure. Exemplos de códigos escritos em Java e c#."
documentationcenter: android
keywords: "Enviar notificação, notificações por push, mensagens por push, notificações por push do android"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="1afac-105">Enviar notificações por Push seguro com Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="1afac-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1afac-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="1afac-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="1afac-107">iOS</span><span class="sxs-lookup"><span data-stu-id="1afac-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="1afac-108">Android</span><span class="sxs-lookup"><span data-stu-id="1afac-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1afac-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1afac-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1afac-110">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="1afac-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1afac-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1afac-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1afac-112">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="1afac-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="1afac-113">O suporte à notificação por push no Microsoft Azure permite que você acesse uma infraestrutura de envio de mensagem por push fácil de usar, multiplataforma e expansível que simplifica muito a implementação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="1afac-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="1afac-114">Devido a restrições regulatórias ou de segurança, às vezes, um aplicativo pode querer incluir algo na notificação que não pode ser transmitido por meio da infraestrutura de notificação por push padrão.</span><span class="sxs-lookup"><span data-stu-id="1afac-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="1afac-115">Este tutorial descreve como obter a mesma experiência ao enviar informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo Android cliente e o back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1afac-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="1afac-116">Em um nível superior, o fluxo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1afac-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="1afac-117">O back-end do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1afac-117">The app back-end:</span></span>
   * <span data-ttu-id="1afac-118">Armazena uma carga segura no banco de dados de back-end.</span><span class="sxs-lookup"><span data-stu-id="1afac-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="1afac-119">Envia a ID dessa notificação ao dispositivo Android (nenhuma informação segura é enviada).</span><span class="sxs-lookup"><span data-stu-id="1afac-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="1afac-120">O dispositivo no aplicativo, ao receber a notificação:</span><span class="sxs-lookup"><span data-stu-id="1afac-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="1afac-121">O dispositivo Android entra em contato com o back-end solicitando a carga segura.</span><span class="sxs-lookup"><span data-stu-id="1afac-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="1afac-122">O aplicativo pode mostrar a carga como uma notificação no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1afac-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="1afac-123">É importante observar que no fluxo anterior (e neste tutorial), pressupomos que o dispositivo armazena um token de autenticação no armazenamento local depois que o usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="1afac-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="1afac-124">Isso garante uma experiência perfeita  já que o dispositivo pode recuperar a carga de segurança da notificação usando este token.</span><span class="sxs-lookup"><span data-stu-id="1afac-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="1afac-125">Se o seu aplicativo não armazenar tokens de autenticação no dispositivo, ou se esses tokens puderem expirar, o aplicativo do dispositivo, após receber a notificação por push, deve exibir uma notificação genérica solicitando que o usuário inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1afac-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="1afac-126">Dessa forma, o aplicativo autentica o usuário e mostra a carga de notificação.</span><span class="sxs-lookup"><span data-stu-id="1afac-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="1afac-127">Este tutorial mostra como enviar notificações por push seguro.</span><span class="sxs-lookup"><span data-stu-id="1afac-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="1afac-128">Baseia-se no tutorial [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) (Notificar usuários), de modo que você deve concluir as etapas nesse tutorial, caso ainda não o tenha feito.</span><span class="sxs-lookup"><span data-stu-id="1afac-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="1afac-129">Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1afac-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="1afac-130">Modificar o projeto Android</span><span class="sxs-lookup"><span data-stu-id="1afac-130">Modify the Android project</span></span>
<span data-ttu-id="1afac-131">Agora que você modificou o back-end do aplicativo para enviar apenas a *id* de uma notificação por push, é preciso alterar o aplicativo Android para manipular essa notificação e retornar a chamada do back-end para recuperar a mensagem segura a ser exibida.</span><span class="sxs-lookup"><span data-stu-id="1afac-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="1afac-132">Para atingir essa meta, você precisa certificar-se de que seu aplicativo Android saiba como se autenticar com o back-end ao receber as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="1afac-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="1afac-133">Agora, modificaremos o fluxo de *logon* para salvar o valor do cabeçalho de autenticação nas preferências compartilhadas de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1afac-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="1afac-134">Mecanismos análogos podem ser usados para armazenar qualquer token de autenticação (por ex., tokens OAuth) que o aplicativo precisará usar sem solicitar as credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="1afac-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="1afac-135">No projeto do aplicativo Android, adicione as seguintes constantes na parte superior da classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="1afac-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="1afac-136">Ainda na classe **MainActivity**, atualize o método `getAuthorizationHeader()` para conter o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="1afac-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="1afac-137">Adicione as seguintes instruções `import` na parte superior do arquivo **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="1afac-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="1afac-138">Agora, alteraremos o manipulador que é chamado quando a notificação é recebida.</span><span class="sxs-lookup"><span data-stu-id="1afac-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="1afac-139">Na classe **MyHandler**, altere o método `OnReceive()` para conter:</span><span class="sxs-lookup"><span data-stu-id="1afac-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="1afac-140">Em seguida, adicione o método `retrieveNotification()`, substituindo o espaço reservado `{back-end endpoint}` pelo ponto de extremidade do back-end obtido ao implantar seu back-end:</span><span class="sxs-lookup"><span data-stu-id="1afac-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="1afac-141">Esse método chama o back-end do seu aplicativo para recuperar o conteúdo da notificação usando as credenciais armazenadas nas preferências compartilhadas e o exibe como uma notificação normal.</span><span class="sxs-lookup"><span data-stu-id="1afac-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="1afac-142">Para o usuário do aplicativo, a notificação tem exatamente a mesma aparência que qualquer outra notificação por push.</span><span class="sxs-lookup"><span data-stu-id="1afac-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="1afac-143">Observe que é preferível manipular os casos de propriedade de cabeçalho de autenticação ausente ou de rejeição por meio do back-end.</span><span class="sxs-lookup"><span data-stu-id="1afac-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="1afac-144">A manipulação específica desses casos depende em grande parte da sua meta de experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="1afac-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="1afac-145">Uma opção é exibir uma notificação com um aviso genérico para que o usuário realize a autenticação para recuperar a notificação real.</span><span class="sxs-lookup"><span data-stu-id="1afac-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="1afac-146">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1afac-146">Run the Application</span></span>
<span data-ttu-id="1afac-147">Para executar o aplicativo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1afac-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="1afac-148">Certifique-se de que o **AppBackend** esteja implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="1afac-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="1afac-149">Se estiver usando o Visual Studio, execute o aplicativo da API Web **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="1afac-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="1afac-150">Uma página da Web do ASP.NET é exibida.</span><span class="sxs-lookup"><span data-stu-id="1afac-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="1afac-151">No Eclipse, execute o aplicativo em um dispositivo Android físico ou no emulador.</span><span class="sxs-lookup"><span data-stu-id="1afac-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="1afac-152">Na interface do usuário do aplicativo Android, insira um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="1afac-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="1afac-153">Pode ser qualquer cadeia de caracteres, mas devem ter o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="1afac-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="1afac-154">Na interface do usuário do aplicativo Android, clique em **Logon**.</span><span class="sxs-lookup"><span data-stu-id="1afac-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="1afac-155">Em seguida, clique em **Enviar push**.</span><span class="sxs-lookup"><span data-stu-id="1afac-155">Then click **Send push**.</span></span>

