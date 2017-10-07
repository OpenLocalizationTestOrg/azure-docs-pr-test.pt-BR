---
title: "aaaSending proteger notificações por Push com Hubs de notificação do Azure"
description: "Saiba como toosend segura envio notificações tooan Android aplicativo do Azure. Exemplos de códigos escritos em Java e c#."
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
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="dc547-105">Enviar notificações por Push seguro com Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="dc547-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc547-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="dc547-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="dc547-107">iOS</span><span class="sxs-lookup"><span data-stu-id="dc547-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="dc547-108">Android</span><span class="sxs-lookup"><span data-stu-id="dc547-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="dc547-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dc547-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dc547-110">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc547-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="dc547-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dc547-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dc547-112">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="dc547-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="dc547-113">Suporte de notificação por push no Microsoft Azure permite que você tooaccess uma infraestrutura de mensagem por push de fácil de usar, multiplataforma, dimensionável, que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="dc547-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="dc547-114">Devido a restrições de segurança ou tooregulatory, às vezes, um aplicativo pode ser conveniente tooinclude algo na notificação de saudação que não pode ser transmitida por meio da infraestrutura de notificação por push padrão hello.</span><span class="sxs-lookup"><span data-stu-id="dc547-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="dc547-115">Este tutorial descreve como tooachieve Olá a mesma experiência, enviando informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo Android do cliente hello e back-end de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dc547-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="dc547-116">Em um nível alto, o fluxo de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="dc547-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="dc547-117">Olá aplicativo back-end:</span><span class="sxs-lookup"><span data-stu-id="dc547-117">hello app back-end:</span></span>
   * <span data-ttu-id="dc547-118">Armazena uma carga segura no banco de dados de back-end.</span><span class="sxs-lookup"><span data-stu-id="dc547-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="dc547-119">Envia Olá ID deste dispositivo Android da toohello de notificação (nenhuma informação de segurança é enviada).</span><span class="sxs-lookup"><span data-stu-id="dc547-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="dc547-120">Olá o aplicativo no dispositivo hello, ao receber a notificação de saudação:</span><span class="sxs-lookup"><span data-stu-id="dc547-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="dc547-121">dispositivo Android Olá contata Olá back-end solicitante Olá carga de segurança.</span><span class="sxs-lookup"><span data-stu-id="dc547-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="dc547-122">aplicativo Hello pode mostrar carga hello como uma notificação no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc547-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="dc547-123">É importante toonote em Olá anterior fluxo (e, neste tutorial), vamos supor que o dispositivo Olá armazena um token de autenticação no armazenamento local, depois Olá usuário fizer logon.</span><span class="sxs-lookup"><span data-stu-id="dc547-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="dc547-124">Isso garante uma experiência completamente, como dispositivo Olá pode recuperar a carga de segurança da notificação hello usando este token.</span><span class="sxs-lookup"><span data-stu-id="dc547-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="dc547-125">Se seu aplicativo não armazenar os tokens de autenticação no dispositivo hello, ou se esses tokens podem ser expirados, aplicativo de dispositivo hello, ao receber a notificação de envio de saudação deve exibir uma notificação genérica solicitando Olá usuário toolaunch Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dc547-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="dc547-126">aplicativo Hello, em seguida, autentica o usuário hello e mostra a carga de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc547-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="dc547-127">Este tutorial mostra como notificações por push de toosend segura.</span><span class="sxs-lookup"><span data-stu-id="dc547-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="dc547-128">Ele se baseia no hello [notificar usuários](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, portanto você deve concluir as etapas de saudação neste tutorial primeiro se ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="dc547-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="dc547-129">Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc547-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="dc547-130">Modificar o projeto Android Olá</span><span class="sxs-lookup"><span data-stu-id="dc547-130">Modify hello Android project</span></span>
<span data-ttu-id="dc547-131">Agora que você modificou o Olá apenas de toosend de back-end do aplicativo *id* de uma notificação por push, você tem toochange seu toohandle de aplicativo do Android notificação e o retorno de chamada a saudação tooretrieve de back-end seguro toobe mensagem exibida.</span><span class="sxs-lookup"><span data-stu-id="dc547-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="dc547-132">tooachieve essa meta, você tem toomake-se de que seu aplicativo do Android, sabe como tooauthenticate em si com o back-end quando ele recebe notificações por push de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc547-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="dc547-133">Agora vamos modificar Olá *login* fluxo no valor de cabeçalho de autenticação ordem toosave Olá no hello compartilhado preferências do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dc547-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="dc547-134">Mecanismos semelhantes podem ser usado toostore qualquer token de autenticação (por exemplo, tokens de OAuth) que Olá aplicativo terá toouse sem a necessidade de credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="dc547-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="dc547-135">No seu projeto de aplicativo do Android, adicionar Olá seguintes constantes na parte superior de saudação do hello **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="dc547-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="dc547-136">Ainda no hello **MainActivity** classe, Olá atualização `getAuthorizationHeader()` saudação do método toocontain código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc547-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="dc547-137">Adicione o seguinte Olá `import` instruções na parte superior de saudação do hello **MainActivity** arquivo:</span><span class="sxs-lookup"><span data-stu-id="dc547-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="dc547-138">Agora, alteraremos manipulador de saudação que é chamado quando Olá notificação é recebida.</span><span class="sxs-lookup"><span data-stu-id="dc547-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="dc547-139">Em Olá **MyHandler** classe Alterar Olá `OnReceive()` toocontain método:</span><span class="sxs-lookup"><span data-stu-id="dc547-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="dc547-140">Em seguida, adicione Olá `retrieveNotification()` método, substituindo o espaço reservado de saudação `{back-end endpoint}` com ponto de extremidade do back-end Olá obtido ao implantar seu back-end:</span><span class="sxs-lookup"><span data-stu-id="dc547-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="dc547-141">Este método chama sua notificação de saudação do aplicativo tooretrieve de back-end de conteúdo usando as credenciais de saudação armazenadas em Olá compartilhado preferências e exibe como uma notificação normal.</span><span class="sxs-lookup"><span data-stu-id="dc547-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="dc547-142">notificação de saudação é usuário do aplicativo toohello exatamente como qualquer outra notificação por push.</span><span class="sxs-lookup"><span data-stu-id="dc547-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="dc547-143">Observe que é preferível toohandle casos de saudação de propriedade de cabeçalho de autenticação ausente ou rejeição por Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="dc547-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="dc547-144">tratamento específico de Olá desses casos dependem principalmente em sua experiência de usuário de destino.</span><span class="sxs-lookup"><span data-stu-id="dc547-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="dc547-145">Uma opção é toodisplay uma notificação com um aviso genérico para Olá tooauthenticate tooretrieve Olá real notificação ao usuário.</span><span class="sxs-lookup"><span data-stu-id="dc547-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="dc547-146">Executar Olá aplicativo</span><span class="sxs-lookup"><span data-stu-id="dc547-146">Run hello Application</span></span>
<span data-ttu-id="dc547-147">toorun Olá aplicativo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc547-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="dc547-148">Certifique-se de que o **AppBackend** esteja implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc547-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="dc547-149">Se usar o Visual Studio, execute Olá **AppBackend** aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="dc547-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="dc547-150">Uma página da Web do ASP.NET é exibida.</span><span class="sxs-lookup"><span data-stu-id="dc547-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="dc547-151">No Eclipse, execute o aplicativo hello em um emulador de dispositivo ou hello Android físico.</span><span class="sxs-lookup"><span data-stu-id="dc547-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="dc547-152">No aplicativo do Android Olá da interface do usuário, digite um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="dc547-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="dc547-153">Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="dc547-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="dc547-154">No aplicativo do Android Olá da interface do usuário, clique em **login**.</span><span class="sxs-lookup"><span data-stu-id="dc547-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="dc547-155">Em seguida, clique em **Enviar push**.</span><span class="sxs-lookup"><span data-stu-id="dc547-155">Then click **Send push**.</span></span>

