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
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Enviar notificações por Push seguro com Hubs de Notificação do Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Visão geral
> [!IMPORTANT]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Suporte de notificação por push no Microsoft Azure permite que você tooaccess uma infraestrutura de mensagem por push de fácil de usar, multiplataforma, dimensionável, que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.

Devido a restrições de segurança ou tooregulatory, às vezes, um aplicativo pode ser conveniente tooinclude algo na notificação de saudação que não pode ser transmitida por meio da infraestrutura de notificação por push padrão hello. Este tutorial descreve como tooachieve Olá a mesma experiência, enviando informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo Android do cliente hello e back-end de aplicativo hello.

Em um nível alto, o fluxo de saudação é o seguinte:

1. Olá aplicativo back-end:
   * Armazena uma carga segura no banco de dados de back-end.
   * Envia Olá ID deste dispositivo Android da toohello de notificação (nenhuma informação de segurança é enviada).
2. Olá o aplicativo no dispositivo hello, ao receber a notificação de saudação:
   * dispositivo Android Olá contata Olá back-end solicitante Olá carga de segurança.
   * aplicativo Hello pode mostrar carga hello como uma notificação no dispositivo de saudação.

É importante toonote em Olá anterior fluxo (e, neste tutorial), vamos supor que o dispositivo Olá armazena um token de autenticação no armazenamento local, depois Olá usuário fizer logon. Isso garante uma experiência completamente, como dispositivo Olá pode recuperar a carga de segurança da notificação hello usando este token. Se seu aplicativo não armazenar os tokens de autenticação no dispositivo hello, ou se esses tokens podem ser expirados, aplicativo de dispositivo hello, ao receber a notificação de envio de saudação deve exibir uma notificação genérica solicitando Olá usuário toolaunch Olá aplicativo. aplicativo Hello, em seguida, autentica o usuário hello e mostra a carga de notificação de saudação.

Este tutorial mostra como notificações por push de toosend segura. Ele se baseia no hello [notificar usuários](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, portanto você deve concluir as etapas de saudação neste tutorial primeiro se ainda não o fez.

> [!NOTE]
> Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Modificar o projeto Android Olá
Agora que você modificou o Olá apenas de toosend de back-end do aplicativo *id* de uma notificação por push, você tem toochange seu toohandle de aplicativo do Android notificação e o retorno de chamada a saudação tooretrieve de back-end seguro toobe mensagem exibida.
tooachieve essa meta, você tem toomake-se de que seu aplicativo do Android, sabe como tooauthenticate em si com o back-end quando ele recebe notificações por push de saudação.

Agora vamos modificar Olá *login* fluxo no valor de cabeçalho de autenticação ordem toosave Olá no hello compartilhado preferências do seu aplicativo. Mecanismos semelhantes podem ser usado toostore qualquer token de autenticação (por exemplo, tokens de OAuth) que Olá aplicativo terá toouse sem a necessidade de credenciais de usuário.

1. No seu projeto de aplicativo do Android, adicionar Olá seguintes constantes na parte superior de saudação do hello **MainActivity** classe:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Ainda no hello **MainActivity** classe, Olá atualização `getAuthorizationHeader()` saudação do método toocontain código a seguir:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Adicione o seguinte Olá `import` instruções na parte superior de saudação do hello **MainActivity** arquivo:
   
        import android.content.SharedPreferences;

Agora, alteraremos manipulador de saudação que é chamado quando Olá notificação é recebida.

1. Em Olá **MyHandler** classe Alterar Olá `OnReceive()` toocontain método:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Em seguida, adicione Olá `retrieveNotification()` método, substituindo o espaço reservado de saudação `{back-end endpoint}` com ponto de extremidade do back-end Olá obtido ao implantar seu back-end:
   
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

Este método chama sua notificação de saudação do aplicativo tooretrieve de back-end de conteúdo usando as credenciais de saudação armazenadas em Olá compartilhado preferências e exibe como uma notificação normal. notificação de saudação é usuário do aplicativo toohello exatamente como qualquer outra notificação por push.

Observe que é preferível toohandle casos de saudação de propriedade de cabeçalho de autenticação ausente ou rejeição por Olá back-end. tratamento específico de Olá desses casos dependem principalmente em sua experiência de usuário de destino. Uma opção é toodisplay uma notificação com um aviso genérico para Olá tooauthenticate tooretrieve Olá real notificação ao usuário.

## <a name="run-hello-application"></a>Executar Olá aplicativo
toorun Olá aplicativo, Olá a seguir:

1. Certifique-se de que o **AppBackend** esteja implantado no Azure. Se usar o Visual Studio, execute Olá **AppBackend** aplicativo de API da Web. Uma página da Web do ASP.NET é exibida.
2. No Eclipse, execute o aplicativo hello em um emulador de dispositivo ou hello Android físico.
3. No aplicativo do Android Olá da interface do usuário, digite um nome de usuário e senha. Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá o mesmo valor.
4. No aplicativo do Android Olá da interface do usuário, clique em **login**. Em seguida, clique em **Enviar push**.

