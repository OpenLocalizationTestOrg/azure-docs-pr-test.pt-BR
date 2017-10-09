---
title: "aaaNotification Hubs últimas notícias Tutorial - Android"
description: "Saiba como toouse Hubs de notificação de barramento de serviço do Azure toosend recentes dispositivos de tooAndroid de notificações de notícias."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar Hubs de notificação toosend últimas notícias
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Visão geral
Este tópico mostra como toouse Hubs de notificação do Azure toobroadcast últimas notícias notificações tooan aplicativo Android. Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias. Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse neles, por exemplo, o leitor de RSS, aplicativos para ventiladores de música, etc.

Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação. Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação. Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência. Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Pré-requisitos
Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação][get-started]. Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].

## <a name="add-category-selection-toohello-app"></a>Adicionar aplicativo de toohello de seleção de categoria
Olá primeira etapa é tooadd Olá da interface do usuário elementos tooyour principal atividade existente que permitem Olá usuário tooselect categorias tooregister. categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação. Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.

1. Abra o arquivo res/layout/activity_main.xml e substituir o conteúdo de saudação com os seguintes hello:
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. Abra o arquivo res/values/strings.xml e adicione Olá linhas seguintes:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    O layout gráfico do main_activity.xml deve ter esta aparência:
   
    ![][A1]
3. Agora, crie uma classe **notificações** Olá mesmo pacote como seu **MainActivity** classe.
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    Essa classe usa categorias de saudação do hello armazenamento local toostore de notícias este dispositivo tem tooreceive. Ele também contém métodos tooregister para essas categorias.
4. Na classe **MainActivity**, remova os campos particulares para **NotificationHub** e **GoogleCloudMessaging** e adicione um campo para **Notificações**:
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. Em seguida, no hello **onCreate** método, remover Olá inicialização de saudação **hub** campo e hello **registerWithNotificationHubs** método. Adicione Olá linhas que inicializar uma instância de saudação seguintes **notificações** classe. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`e `HubListenConnectionString` já deve ser definido com hello `<hub name>` e `<connection string with listen access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultListenSharedAccessSignature* que você obteve anteriormente.

    > [AZURE.NOTE] Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente. Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações. chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.


1. Em seguida, adicione Olá a seguir importa e `subscribe` saudação do método toohandle inscrever-se o botão de evento de clique:
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    Esse método cria uma lista de categorias e usa Olá **notificações** classe toostore lista de saudação no armazenamento local hello e registre marcas correspondentes Olá com seu hub de notificação. Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.

Seu aplicativo agora é capaz de toostore um conjunto de categorias no armazenamento local no dispositivo hello e registrar com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.

## <a name="register-for-notifications"></a>Registrar-se para receber notificações
Estas etapas se registrar com o hub de notificação de saudação na inicialização usando as categorias de saudação que foram armazenadas no armazenamento local.

> [!NOTE]
> Como Olá registrationId atribuído pelo Google Cloud Messaging (GCM) pode ser alterado a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação. Este exemplo registra para notificação sempre que o aplicativo hello for iniciado. Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.
> 
> 

1. Adicionar Olá após código final Olá Olá **onCreate** método hello **MainActivity** classe:
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Isso torna-se de que sempre que o aplicativo hello é iniciado, ele recupera as categorias de saudação do armazenamento local e solicita um registro para estas categorias. 
2. Em seguida, atualize Olá `onStart()` método hello `MainActivity` classe da seguinte maneira:
   
    @Override  protected void onStart() {
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    }
   
    Isso atualiza a atividade principal hello, com base no status de saudação das categorias salvas anteriormente.

aplicativo Hello agora está concluído e pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias. Em seguida, definiremos um back-end que pode enviar categoria notificações toothis aplicativo.

## <a name="sending-tagged-notifications"></a>Enviando notificações marcadas
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Execute o aplicativo hello e geram notificações
1. No Android Studio, compile o aplicativo hello e iniciá-lo em um dispositivo ou emulador.
   
    Observe que o aplicativo hello de que interface do usuário fornece um conjunto alterna que permite que você escolha Olá categorias toosubscribe para.
2. Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.
   
    aplicativo Hello converte categorias Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação. Olá categorias registradas são retornadas e exibidas em uma notificação do sistema.
3. Envie uma notificação de novo, executando o aplicativo de Console .NET hello.  Como alternativa, você pode enviar notificações de modelo marcadas, usando a guia de depuração de saudação do hub de notificação em hello [Portal clássico do Azure].
   
    As notificações para categorias de saudação selecionada aparecem como notificações do sistema.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, nós aprendemos como toobroadcast últimas notícias por categoria. Considere a concluir uma saudação tutoriais que realçam outros cenários avançados de Hubs de notificação a seguir:

* [Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]
  
    Saiba como Olá tooexpand últimas notícias aplicativo tooenable enviar localizado notificações.

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Portal clássico do Azure]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
