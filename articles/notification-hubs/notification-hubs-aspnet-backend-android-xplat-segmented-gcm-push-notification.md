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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="ab7a3-103">Usar Hubs de notificação toosend últimas notícias</span><span class="sxs-lookup"><span data-stu-id="ab7a3-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="ab7a3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ab7a3-104">Overview</span></span>
<span data-ttu-id="ab7a3-105">Este tópico mostra como toouse Hubs de notificação do Azure toobroadcast últimas notícias notificações tooan aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="ab7a3-106">Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="ab7a3-107">Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse neles, por exemplo, o leitor de RSS, aplicativos para ventiladores de música, etc.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="ab7a3-108">Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="ab7a3-109">Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="ab7a3-110">Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="ab7a3-111">Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ab7a3-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab7a3-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab7a3-112">Prerequisites</span></span>
<span data-ttu-id="ab7a3-113">Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="ab7a3-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="ab7a3-114">Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="ab7a3-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="ab7a3-115">Adicionar aplicativo de toohello de seleção de categoria</span><span class="sxs-lookup"><span data-stu-id="ab7a3-115">Add category selection toohello app</span></span>
<span data-ttu-id="ab7a3-116">Olá primeira etapa é tooadd Olá da interface do usuário elementos tooyour principal atividade existente que permitem Olá usuário tooselect categorias tooregister.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="ab7a3-117">categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="ab7a3-118">Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="ab7a3-119">Abra o arquivo res/layout/activity_main.xml e substituir o conteúdo de saudação com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
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
2. <span data-ttu-id="ab7a3-120">Abra o arquivo res/values/strings.xml e adicione Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="ab7a3-121">O layout gráfico do main_activity.xml deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="ab7a3-122">Agora, crie uma classe **notificações** Olá mesmo pacote como seu **MainActivity** classe.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
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
   
    <span data-ttu-id="ab7a3-123">Essa classe usa categorias de saudação do hello armazenamento local toostore de notícias este dispositivo tem tooreceive.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="ab7a3-124">Ele também contém métodos tooregister para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="ab7a3-125">Na classe **MainActivity**, remova os campos particulares para **NotificationHub** e **GoogleCloudMessaging** e adicione um campo para **Notificações**:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="ab7a3-126">Em seguida, no hello **onCreate** método, remover Olá inicialização de saudação **hub** campo e hello **registerWithNotificationHubs** método.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="ab7a3-127">Adicione Olá linhas que inicializar uma instância de saudação seguintes **notificações** classe.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="ab7a3-128">`HubName`e `HubListenConnectionString` já deve ser definido com hello `<hub name>` e `<connection string with listen access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultListenSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="ab7a3-129">Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="ab7a3-130">Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="ab7a3-131">chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="ab7a3-132">Em seguida, adicione Olá a seguir importa e `subscribe` saudação do método toohandle inscrever-se o botão de evento de clique:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="ab7a3-133">Esse método cria uma lista de categorias e usa Olá **notificações** classe toostore lista de saudação no armazenamento local hello e registre marcas correspondentes Olá com seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="ab7a3-134">Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="ab7a3-135">Seu aplicativo agora é capaz de toostore um conjunto de categorias no armazenamento local no dispositivo hello e registrar com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="ab7a3-136">Registrar-se para receber notificações</span><span class="sxs-lookup"><span data-stu-id="ab7a3-136">Register for notifications</span></span>
<span data-ttu-id="ab7a3-137">Estas etapas se registrar com o hub de notificação de saudação na inicialização usando as categorias de saudação que foram armazenadas no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="ab7a3-138">Como Olá registrationId atribuído pelo Google Cloud Messaging (GCM) pode ser alterado a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="ab7a3-139">Este exemplo registra para notificação sempre que o aplicativo hello for iniciado.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="ab7a3-140">Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="ab7a3-141">Adicionar Olá após código final Olá Olá **onCreate** método hello **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="ab7a3-142">Isso torna-se de que sempre que o aplicativo hello é iniciado, ele recupera as categorias de saudação do armazenamento local e solicita um registro para estas categorias.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="ab7a3-143">Em seguida, atualize Olá `onStart()` método hello `MainActivity` classe da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="ab7a3-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="ab7a3-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="ab7a3-145">}</span><span class="sxs-lookup"><span data-stu-id="ab7a3-145">}</span></span>
   
    <span data-ttu-id="ab7a3-146">Isso atualiza a atividade principal hello, com base no status de saudação das categorias salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="ab7a3-147">aplicativo Hello agora está concluído e pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="ab7a3-148">Em seguida, definiremos um back-end que pode enviar categoria notificações toothis aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="ab7a3-149">Enviando notificações marcadas</span><span class="sxs-lookup"><span data-stu-id="ab7a3-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="ab7a3-150">Execute o aplicativo hello e geram notificações</span><span class="sxs-lookup"><span data-stu-id="ab7a3-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="ab7a3-151">No Android Studio, compile o aplicativo hello e iniciá-lo em um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="ab7a3-152">Observe que o aplicativo hello de que interface do usuário fornece um conjunto alterna que permite que você escolha Olá categorias toosubscribe para.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="ab7a3-153">Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="ab7a3-154">aplicativo Hello converte categorias Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="ab7a3-155">Olá categorias registradas são retornadas e exibidas em uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="ab7a3-156">Envie uma notificação de novo, executando o aplicativo de Console .NET hello.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="ab7a3-157">Como alternativa, você pode enviar notificações de modelo marcadas, usando a guia de depuração de saudação do hub de notificação em hello [Portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="ab7a3-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="ab7a3-158">As notificações para categorias de saudação selecionada aparecem como notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab7a3-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab7a3-159">Next steps</span></span>
<span data-ttu-id="ab7a3-160">Neste tutorial, nós aprendemos como toobroadcast últimas notícias por categoria.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="ab7a3-161">Considere a concluir uma saudação tutoriais que realçam outros cenários avançados de Hubs de notificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab7a3-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="ab7a3-162">[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]</span><span class="sxs-lookup"><span data-stu-id="ab7a3-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="ab7a3-163">Saiba como Olá tooexpand últimas notícias aplicativo tooenable enviar localizado notificações.</span><span class="sxs-lookup"><span data-stu-id="ab7a3-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
