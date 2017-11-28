---
title: "Notificação de Usuários nos Hubs de Notificação do Azure para Android com o back-end do .NET"
description: "Saiba como enviar notificações por push para usuários no Azure. Exemplos de código escritos em Java para Android"
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 418a4b638dfaa3fee33a7a7242433699205c79f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="25b72-104">Notificação de Usuários nos Hubs de Notificação do Azure para Android com o back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="25b72-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="25b72-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="25b72-105">Overview</span></span>
<span data-ttu-id="25b72-106">O suporte à notificação por push no Azure permite que você acesse uma infraestrutura de envio por push fácil de usar, multiplataforma e expansível que simplifica em muito a implementação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="25b72-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="25b72-107">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push a um usuário específico do aplicativo em um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="25b72-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="25b72-108">Um back-end da API Web ASP.NET é usado para autenticar clientes e gerar notificações, conforme mostrado no tópico de diretrizes [Registrando-se por meio do back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="25b72-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="25b72-109">Este tutorial baseia-se no hub de notificação que você criou no tutorial [Introdução aos Hubs de Notificação](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="25b72-109">This tutorial builds on the notification hub that you created in the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="25b72-110">Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="25b72-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-the-android-project"></a><span data-ttu-id="25b72-111">Criar o projeto Android</span><span class="sxs-lookup"><span data-stu-id="25b72-111">Create the Android Project</span></span>
<span data-ttu-id="25b72-112">A próxima etapa é criar o aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="25b72-112">The next step is to create the Android application.</span></span>

1. <span data-ttu-id="25b72-113">Siga o tutorial [Introdução aos Hubs de Notificação (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) para criar e configurar o aplicativo para receber notificações por push do GCM.</span><span class="sxs-lookup"><span data-stu-id="25b72-113">Follow the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial to create and configure your app to receive push notifications from GCM.</span></span>
2. <span data-ttu-id="25b72-114">Abra o arquivo **res/layout/activity_main.xml** e substitua pelas definições de conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="25b72-114">Open your **res/layout/activity_main.xml** file, replace the with the following content definitions.</span></span>
   
    <span data-ttu-id="25b72-115">Isso adiciona novos controles EditText para fazer logon como um usuário.</span><span class="sxs-lookup"><span data-stu-id="25b72-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="25b72-116">Além disso, um campo é adicionado para uma marca username, que fará parte das notificações enviadas:</span><span class="sxs-lookup"><span data-stu-id="25b72-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. <span data-ttu-id="25b72-117">Abra o arquivo **res/values/strings.xml** e substitua a definição `send_button` pelas linhas a seguir, que redefinem a cadeia de caracteres para o `send_button` e adicione cadeias de caracteres aos outros controles:</span><span class="sxs-lookup"><span data-stu-id="25b72-117">Open your **res/values/strings.xml** file and replace the `send_button` definition with the following lines that redefine the string for the `send_button` and add strings for the other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="25b72-118">O layout gráfico do main_activity.xml deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="25b72-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="25b72-119">Crie uma nova classe chamada **RegisterClient** no mesmo pacote que a classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="25b72-119">Create a new class named **RegisterClient** in the same package as your `MainActivity` class.</span></span> <span data-ttu-id="25b72-120">Use o código a seguir para o novo arquivo de classe.</span><span class="sxs-lookup"><span data-stu-id="25b72-120">Use the code below for the new class file.</span></span>
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    <span data-ttu-id="25b72-121">Esse componente implementa as chamadas do REST necessárias para entrar em contato com o back-end do aplicativo para se registrar para as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="25b72-121">This component implements the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="25b72-122">Ele também armazena localmente os *registrationIds* criados pelo Hub de Notificação, conforme detalhado em [Registrando-se por meio do back-end do aplicativo](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="25b72-122">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="25b72-123">Observe que ele usa um token de autorização armazenado localmente quando você clica no botão **Fazer logon** .</span><span class="sxs-lookup"><span data-stu-id="25b72-123">Note that it uses an authorization token stored in local storage when you click the **Log in** button.</span></span>
5. <span data-ttu-id="25b72-124">Na sua classe `MainActivity`, remova ou comente o campo particular para o `NotificationHub` e adicione um campo para a classe `RegisterClient` e uma cadeia de caracteres para seu ponto de extremidade do back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="25b72-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for the `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="25b72-125">Substitua `<Enter Your Backend Endpoint>` pelo ponto de extremidade de back-end real obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="25b72-125">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="25b72-126">Por exemplo: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="25b72-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="25b72-127">Na sua classe `MainActivity`, no método `onCreate`, remova ou comente a inicialização do campo `hub` e a chamada ao método `registerWithNotificationHubs`.</span><span class="sxs-lookup"><span data-stu-id="25b72-127">In your `MainActivity` class, in the `onCreate` method, remove or comment out the initialization of the `hub` field and the call to the `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="25b72-128">Em seguida, adicione código para inicializar uma instância da classe `RegisterClient` .</span><span class="sxs-lookup"><span data-stu-id="25b72-128">Then add code to initialize an instance of the `RegisterClient` class.</span></span> <span data-ttu-id="25b72-129">O método deve conter as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="25b72-129">The method should contain the following lines:</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. <span data-ttu-id="25b72-130">Em sua classe `MainActivity`, exclua ou comente o método `registerWithNotificationHubs` inteiro.</span><span class="sxs-lookup"><span data-stu-id="25b72-130">In your `MainActivity` class, delete or comment out the entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="25b72-131">Ele não será usado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="25b72-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="25b72-132">Adicione as seguintes instruções `import` ao seu arquivo **MainActivity.java** .</span><span class="sxs-lookup"><span data-stu-id="25b72-132">Add the following `import` statements to your **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="25b72-133">Em seguida, adicione os seguintes métodos para manipular o evento de clique do botão **Fazer logon** e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="25b72-133">Then, add the following methods to handle the **Log in** button click event and sending push notifications.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed to register", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls the ASP.NET WebAPI backend to send the notification message
         * to the platform notification service based on the pns parameter.
         *
         * @param pns     The platform notification service to send the notification message to. Must
         *                be one of the following ("wns", "gcm", "apns").
         * @param userTag The tag for the user who will receive the notification message. This string
         *                must not contain spaces or special characters.
         * @param message The notification message string. This string must include the double quotes
         *                to be used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed to send " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="25b72-134">O manipulador `login` para o botão **Fazer logon** gera um token de autenticação básico usando o nome de usuário e senha de entrada (observe que isso representa qualquer token utilizado pelo esquema de autenticação) e depois usa `RegisterClient` para chamar o back-end para registro.</span><span class="sxs-lookup"><span data-stu-id="25b72-134">The `login` handler for the **Log in** button generates a basic authentication token using on the input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` to call the backend for registration.</span></span>

    <span data-ttu-id="25b72-135">O método `sendPush` chama o back-end para disparar uma notificação segura para o usuário com base na marca user.</span><span class="sxs-lookup"><span data-stu-id="25b72-135">The `sendPush` method calls the backend to trigger a secure notification to the user based on the user tag.</span></span> <span data-ttu-id="25b72-136">O serviço de notificação de plataforma que `sendPush` tem como destino depende da cadeia de caracteres `pns` passada.</span><span class="sxs-lookup"><span data-stu-id="25b72-136">The platform notification service that `sendPush` targets depends on the `pns` string passed in.</span></span>

1. <span data-ttu-id="25b72-137">Em sua classe `MainActivity`, atualize o método `sendNotificationButtonOnClick` para chamar o método `sendPush` com aos serviços de notificação de plataforma selecionados do usuário a seguir.</span><span class="sxs-lookup"><span data-stu-id="25b72-137">In your `MainActivity` class, update the `sendNotificationButtonOnClick` method to call the `sendPush` method with the user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends the push notification
        * message to each platform selected.
        *
        * @param v The view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-the-application"></a><span data-ttu-id="25b72-138">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="25b72-138">Run the Application</span></span>
1. <span data-ttu-id="25b72-139">Execute o aplicativo em um dispositivo ou em um emulador usando o Studio Android.</span><span class="sxs-lookup"><span data-stu-id="25b72-139">Run the application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="25b72-140">No aplicativo Android, insira um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="25b72-140">In the Android app, enter a username and password.</span></span> <span data-ttu-id="25b72-141">Eles devem ter o mesmo valor de cadeia de caracteres e não devem conter espaços ou caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="25b72-141">They must both be the same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="25b72-142">No aplicativo Android, clique em **Fazer logon**.</span><span class="sxs-lookup"><span data-stu-id="25b72-142">In the Android app, click **Log in**.</span></span> <span data-ttu-id="25b72-143">Aguarde uma mensagem de notificação do sistema que afirma **Conectado e registrado**.</span><span class="sxs-lookup"><span data-stu-id="25b72-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="25b72-144">Isso habilitará o botão **Enviar Notificação** .</span><span class="sxs-lookup"><span data-stu-id="25b72-144">This will enable the **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="25b72-145">Clique nos botões de alternância para habilitar todas as plataformas onde você executou o aplicativo e registrou um usuário.</span><span class="sxs-lookup"><span data-stu-id="25b72-145">Click the toggle buttons to enable all platforms where you have ran the app and registered a user.</span></span>
5. <span data-ttu-id="25b72-146">Insira o nome do usuário que receberá a mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="25b72-146">Enter the user's name that will receive the notification message.</span></span> <span data-ttu-id="25b72-147">Esse usuário deverá estar registrados para notificações nos dispositivos de destino.</span><span class="sxs-lookup"><span data-stu-id="25b72-147">That user must be registered for notifications on the target devices.</span></span>
6. <span data-ttu-id="25b72-148">Insira uma mensagem para o usuário a ser recebida como uma mensagem de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="25b72-148">Enter a message for the user to receive as a push notification message.</span></span>
7. <span data-ttu-id="25b72-149">Clique em **Enviar Notificação**.</span><span class="sxs-lookup"><span data-stu-id="25b72-149">Click **Send Notification**.</span></span>  <span data-ttu-id="25b72-150">Cada dispositivo com um registro com a marca username correspondente receberá a notificação de push.</span><span class="sxs-lookup"><span data-stu-id="25b72-150">Each device that has a registration with the matching username tag will receive the push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
