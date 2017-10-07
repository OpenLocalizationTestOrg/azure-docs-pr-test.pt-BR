---
title: "aaaGet iniciado com Hubs de notificação do Azure usando Baidu | Microsoft Docs"
description: "Neste tutorial, você aprenderá como dispositivos toouse Hubs de notificação do Azure toopush notificações tooAndroid usando Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Introdução aos Hubs de Notificação usando o Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Push de nuvem do Baidu é um serviço de nuvem chinês que você pode usar dispositivos de toomobile de notificações de push toosend. Esse serviço é útil na China, onde entregar notificações de push tooAndroid é complexo devido à presença de saudação de lojas de aplicativos diferentes e enviar por push de serviços, além disso toohello disponibilidade de dispositivos Android que não são normalmente conectado tooGCM (Google Nuvem de mensagens).

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial exige:

* SDK do Android (vamos supor que você use Eclipse), que você pode baixar da saudação <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>
* [SDK para Android de Serviços Móveis]
* [Baidu Push Android SDK]

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Criar uma conta de Baidu
toouse Baidu, você deve ter uma conta do Baidu. Se você já tiver um, faça logon toohello [Baidu portal] e ignorar toohello próxima etapa. Caso contrário, consulte Olá seguindo as instruções sobre como toocreate uma conta do Baidu.  

1. Vá toohello [Baidu portal] e clique em Olá**登录**(**Login**) link. Clique em**立即注册**toostart processo de registro de conta de saudação.
   
   ![][1]
2. Insira os detalhes de saudação necessária — phone/código de verificação, senha e endereço de email — e clique em **inscrição**.
   
   ![][2]
3. Você receberá um endereço de email de toohello de email inserido com um link tooactivate sua conta do Baidu.
   
   ![][3]
4. Faça logon na conta de email tooyour, abra o email de ativação do Baidu hello e clique tooactivate de link de ativação de saudação sua conta do Baidu.
   
   ![][4]

Depois que você tiver uma conta de Baidu ativada, faça logon em toohello [Baidu portal].

## <a name="register-as-a-baidu-developer"></a>Registrar-se como desenvolvedor Baidu
1. Depois de fazer logon em toohello [Baidu portal], clique em**更多 >>** (**mais**).
   
      ![][5]
2. Role para baixo na Olá**站长与开发者服务 (serviços de desenvolvedor e Webmaster)** seção e clique em**百度开放云平台**(**Baidu abrir plataforma de nuvem**).
   
      ![][6]
3. Na próxima página do hello, clique em**开发者服务**(**serviços de desenvolvedor**) no canto superior direito de saudação.
   
      ![][7]
4. Na próxima página do hello, clique em**注册开发者**(**desenvolvedores registrados**) no menu de saudação no canto superior direito de saudação.
   
      ![][8]
5. Insira seu nome, uma descrição e um número de telefone celular para receber uma mensagem de texto de verificação e, em seguida, clique em **送验证码** (**Enviar Código de Verificação**). Para números de telefone internacional, é necessário código de país Olá tooenclose entre parênteses. Por exemplo, para um número dos Estados Unidos, ele será **(1) 1234567890**.
   
      ![][9]
6. Em seguida, você deve receber uma mensagem de texto com um número de verificação, conforme mostrado no exemplo a seguir de saudação:
   
      ![][10]
7. Insira o número de verificação de saudação da mensagem de saudação em**验证码**(**código de confirmação**).
8. Por fim, concluir o registro de desenvolvedor de saudação aceitar Olá Baidu contrato e clicando em**提交**(**enviar**). Você verá Olá página após a conclusão bem-sucedida do registro a seguir:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Criar um projeto de envio na nuvem Baidu
Quando você cria um projeto de envio na nuvem Baidu, você recebe sua ID de aplicativo, chave API e a chave secreta.

1. Depois de fazer logon em toohello [Baidu portal], clique em**更多 >>** (**mais**).
   
      ![][5]
2. Role para baixo na Olá**站长与开发者服务**(**Webmaster e serviços de desenvolvedor**) seção e clique em**百度开放云平台**(**Baidu abrir plataforma de nuvem**).
   
      ![][6]
3. Na próxima página do hello, clique em**开发者服务**(**serviços de desenvolvedor**) no canto superior direito de saudação.
   
      ![][7]
4. Na próxima página do hello, clique em**云推送**(**Push de nuvem**) do hello**云服务**(**serviços de nuvem**) seção.
   
      ![][12]
5. Quando você for um desenvolvedor registrado, você ver**管理控制台**(**Console de gerenciamento**) no menu superior hello. Clique em **开发者服务管理** (**Gerenciamento de Serviço de Desenvolvedores**).
   
      ![][13]
6. Na próxima página do hello, clique em**创建工程**(**criar projeto**).
   
      ![][14]
7. Insira um nome de aplicativo e clique em **创建** (**Criar**).
   
      ![][15]
8. Após a criação bem-sucedida de um projeto de push da nuvem Baidu, você verá uma página com a **ID de Aplicativo**, **Chave de API** e **Chave Secreta**. Anote a chave de API hello e chave secreta, que vamos usar mais tarde.
   
      ![][16]
9. Configurar projeto Olá para notificações por push clicando**云推送**(**por Push de nuvem**) no painel esquerdo da saudação.
   
      ![][31]
10. Na página seguinte do hello, clique em Olá**推送设置**(**enviar por Push configurações**) botão.
    
    ![][32]  
11. Na página de configuração hello, adicionar nome do pacote de saudação que você usará em seu projeto Android em Olá**应用包名**(**pacote de aplicativo**) campo e, em seguida, clique em**保存设置**( **Salvar**).  
    
    ![][33]

Consulte Olá**保存成功!** Mensagem (**salva com êxito!**).

## <a name="configure-your-notification-hub"></a>Configurar seu Hub de Notificação
1. Entrar toohello [Portal clássico do Azure]e, em seguida, clique em **+ novo** na parte inferior da saudação da tela hello.
2. Clique em **Serviços de Aplicativos**, em **Barramento de Serviço**, em **Hub de Notificação** e em **Criação Rápida**.
3. Forneça um nome para sua **Hub de notificação**, selecione Olá **região** e hello **Namespace** onde este hub de notificação será criado e, em seguida, clique em  **Criar um novo Hub de notificação**.  
   
      ![][17]
4. Clique em Olá namespace em que você criou seu hub de notificação e, em seguida, clique em **Hubs de notificação** na parte superior da saudação.
   
      ![][18]
5. Hub de notificação Olá selecione que você criou e, em seguida, clique em **configurar** no menu superior hello.
   
      ![][19]
6. Role para baixo toohello **as configurações de notificação baidu** seção e insira a chave de API de saudação e a chave secreta que você obteve do console do Baidu Olá anteriormente para seu projeto de envio por push de nuvem do Baidu. Clique em **Salvar**.
   
      ![][20]
7. Clique em Olá **painel** guia na parte superior de Olá Olá hub de notificação e, em seguida, clique em **Exibir cadeia de Conexão**.
   
      ![][21]
8. Anote Olá **DefaultListenSharedAccessSignature** e **DefaultFullSharedAccessSignature** de saudação **acessar as informações de conexão** janela.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Conecte-se o seu hub de notificação do aplicativo toohello
1. No Eclipse ADT, crie um novo projeto Android (**Arquivo** > **Novo** > **Projeto de Aplicativo Android**).
   
    ![][23]
2. Insira um **nome do aplicativo** e certifique-se de que Olá **mínimo necessário SDK** versão está definida muito**API 16: Android 4.1**.
   
    ![][24]
3. Clique em **próximo** e continuar após o Assistente de saudação até Olá **Criar atividade** janela é exibida. Verifique se **atividade em branco** está selecionado e, por fim, selecione **concluir** toocreate um novo aplicativo Android.
   
    ![][25]
4. Certifique-se de que Olá **destino de compilação de projeto** está definida corretamente.
   
    ![][26]
5. Baixe o arquivo de 0.4.jar de hubs de notificação de saudação do hello **arquivos** guia da saudação [notificação-Hubs-Android-SDK em Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Adicionar Olá arquivo toohello **bibliotecas** pasta de projeto do Eclipse e atualização Olá *bibliotecas* pasta.
6. Baixe e descompacte Olá [Baidu Push Android SDK], abra Olá **bibliotecas** pasta e, em seguida, Olá cópia **pushservice x.y.z** jar do arquivo e hello **armeabi**  &  **mips** pastas no hello **bibliotecas** pasta do seu aplicativo Android.
7. Olá abrir **AndroidManifest.xml** arquivo do seu Android do projeto e adicionar permissões de saudação que são exigidas pelo Olá Baidu SDK.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Adicionar Olá **android: name** propriedade tooyour **aplicativo** elemento **AndroidManifest.xml**, substituindo *yourprojectname* (para exemplo, **com.example.BaiduTest**). Verifique se o nome do projeto corresponde Olá um que você configurou no console do Baidu hello.
   
        <application android:name="yourprojectname.DemoApplication"
9. Adicionar Olá seguinte configuração dentro do elemento de aplicativo hello após Olá **. MainActivity** elemento da atividade, substituindo *yourprojectname* (por exemplo, **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Adicionar uma nova classe chamada **ConfigurationSettings.java** toohello projeto.
    
     ![][28]
    
     ![][29]
11. Adicione Olá tooit de código a seguir:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Definir o valor de saudação do **API_KEY** com o que você recuperou do projeto da nuvem Baidu Olá anteriormente, **NotificationHubName** com seu nome de hub de notificação de saudação Portal clássico do Azure e  **NotificationHubConnectionString** com DefaultListenSharedAccessSignature de saudação Portal clássico do Azure.
12. Adicionar uma nova classe chamada **DemoApplication.java**e adicione Olá tooit de código a seguir:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Adicionar uma nova classe chamada **MyPushMessageReceiver.java**e adicione Olá tooit de código a seguir. É classe Olá identificadores Olá notificações por push que são recebidas do servidor de envio por push do hello Baidu.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Abra **MainActivity.java**e adicione Olá após toohello **onCreate** método:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Abra Olá seguindo as instruções de importação na parte superior da saudação:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Enviar notificações tooyour aplicativo
Você pode testar rapidamente a receber notificações em seu aplicativo pelo envio de notificações em Olá [portal do Azure](https://portal.azure.com/) usando Olá **enviar** botão no hub de notificação hello, conforme mostrado no hello tela a seguir:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Notificações por push normalmente são enviadas em um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível. Se uma biblioteca não está disponível para o back-end, você pode usar o hello API REST diretamente as mensagens de notificação toosend.

Neste tutorial, podemos manter a simplicidade e demonstrar a testar seu aplicativo de cliente por meio do envio de notificações usando Olá SDK .NET para hubs de notificação em um aplicativo de console, em vez de um serviço de back-end. É recomendável Olá [usar Hubs de notificação toopush notificações toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial como a próxima etapa hello para enviar notificações de um back-end do ASP.NET. No entanto, a saudação abordagens a seguir pode ser usada para enviar notificações:

* **Interface REST**: você pode dar suporte à notificação em qualquer plataforma de back-end usando Olá [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK .NET de Hubs de notificação do Microsoft Azure**: em Olá Gerenciador de pacotes do Nuget para Visual Studio, execute [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [como toouse Hubs de notificação do Node. js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Aplicativos móveis**: para obter um exemplo de como toosend notificações de um back-end aplicativos de celular do serviço de aplicativo do Azure que esteja integrado com Hubs de notificação, consulte [aplicativo móvel de tooyour adicionar de notificações por push](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: para obter um exemplo de como as notificações de toosend usando Olá APIs REST, consulte "como toouse Hubs de notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Opcional) Enviar notificações de um aplicativo de console do .NET.
Nesta seção, vamos mostrar o envio de uma notificação usando um aplicativo de console do .NET.

1. Crie um novo aplicativo de console do Visual C#:
   
    ![][30]
2. Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Essa instrução adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Arquivo hello abrir **Program.cs** e adicione o seguinte hello usando a instrução:
   
        using Microsoft.Azure.NotificationHubs;
4. No seu `Program` de classe, adicione Olá método a seguir e substitua *DefaultFullSharedAccessSignatureSASConnectionString* e *NotificationHubName* com valores hello que você tem.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Adicionar Olá seguintes linhas no seu **principal** método:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Testar seu aplicativo
tootest neste aplicativo com um telefone real, basta conectar Olá computador do telefone tooyour usando um cabo USB. Essa ação carrega o aplicativo para telefone Olá anexado.

tootest esse aplicativo com o emulador do Windows hello, Olá Eclipse superior barra de ferramentas, clique **executar**e, em seguida, selecione seu aplicativo: ele inicia o emulador do Windows hello, carga, e é executado Olá aplicativo.

aplicativo Hello recupera Olá 'userId' e 'channelId' de saudação serviço de notificação por Push do Baidu e registra com o hub de notificação de saudação.

toosend uma notificação de teste, você pode usar o guia de depuração de saudação do hello Portal clássico do Azure. Se você criou um aplicativo de console hello .NET para o Visual Studio, basta pressione tecla F5 de saudação no aplicativo do Visual Studio toorun hello. aplicativo Hello envia uma notificação que aparece na área de notificação superior de saudação do seu dispositivo ou emulador.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[SDK para Android de Serviços Móveis]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Portal clássico do Azure]: https://manage.windowsazure.com/
[Baidu portal]: http://www.baidu.com/
