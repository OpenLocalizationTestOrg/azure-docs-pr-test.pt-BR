---
title: "Tutorial de últimas notícias de Hubs de Notificação - Android"
description: "Aprenda a usar Hubs de notificação do barramento de serviço do Azure para enviar notificações de últimas notícias a dispositivos com Android."
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="da961-103">Usar hubs de notificação para enviar notícias recentes</span><span class="sxs-lookup"><span data-stu-id="da961-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="da961-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="da961-104">Overview</span></span>
<span data-ttu-id="da961-105">Este tópico mostra como usar os Hubs de Notificação do Azure para transmitir notificações de últimas notícias para um aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="da961-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="da961-106">Ao concluir, você poderá se registrar nas categorias de últimas notícias que desejar e receber notificações por push apenas para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="da961-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="da961-107">Esse cenário é um padrão comum para muitos aplicativos nos quais as notificações precisam ser enviadas para grupos de usuários que tenham anteriormente expressado seu interesse por elas; por ex., leitor de RSS, aplicativos para fãs de música, etc.</span><span class="sxs-lookup"><span data-stu-id="da961-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="da961-108">Os cenários de transmissão são habilitados por meio da inclusão de uma ou mais *marcas* durante a criação de um registro no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="da961-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="da961-109">Quando as notificações são enviadas para um rótulo, todos os dispositivos que foram registrados para o rótulo receberão a notificação.</span><span class="sxs-lookup"><span data-stu-id="da961-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="da961-110">Como os rótulos são simplesmente cadeias de caracteres, eles não precisam ser provisionados com antecedência.</span><span class="sxs-lookup"><span data-stu-id="da961-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="da961-111">Para obter mais informações sobre marcas, consulte [Expressões de Marca e Roteamento dos Hubs de Notificação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="da961-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da961-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da961-112">Prerequisites</span></span>
<span data-ttu-id="da961-113">Este tópico se baseia no aplicativo criado em [Introdução aos Hubs de Notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="da961-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="da961-114">Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="da961-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="da961-115">Adicionar a seleção de categorias ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="da961-115">Add category selection to the app</span></span>
<span data-ttu-id="da961-116">A primeira etapa é adicionar os elementos da interface do usuário na atividade principal existente, o que permite ao usuário selecionar categorias para o registro.</span><span class="sxs-lookup"><span data-stu-id="da961-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="da961-117">As categorias selecionadas por um usuário são armazenadas no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="da961-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="da961-118">Quando o aplicativo é iniciado, o registro do dispositivo é criado no seu hub de notificação com as categorias selecionadas como rótulos.</span><span class="sxs-lookup"><span data-stu-id="da961-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="da961-119">Abra o arquivo res/layout/activity_main.xml e substitua o conteúdo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="da961-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="da961-120">Abra o arquivo res/values/strings.xml e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="da961-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="da961-121">O layout gráfico do main_activity.xml deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="da961-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="da961-122">Agora, crie uma classe **Notificações** no mesmo pacote que a classe **MainActivity**.</span><span class="sxs-lookup"><span data-stu-id="da961-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="da961-123">Essa classe usa o armazenamento local para armazenar as categorias de notícias que este dispositivo deverá receber.</span><span class="sxs-lookup"><span data-stu-id="da961-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="da961-124">Ela também contém métodos para se registrar nessas categorias.</span><span class="sxs-lookup"><span data-stu-id="da961-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="da961-125">Na classe **MainActivity**, remova os campos particulares para **NotificationHub** e **GoogleCloudMessaging** e adicione um campo para **Notificações**:</span><span class="sxs-lookup"><span data-stu-id="da961-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="da961-126">Em seguida, no método **onCreate**, remova a inicialização do campo **hub** e o método **registerWithNotificationHubs**.</span><span class="sxs-lookup"><span data-stu-id="da961-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="da961-127">Depois, adicione as linhas a seguir, que inicializam uma instância da classe **Notificações** .</span><span class="sxs-lookup"><span data-stu-id="da961-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="da961-128">`HubName` e `HubListenConnectionString` já devem estar definidos com os espaços reservados `<hub name>` e `<connection string with listen access>` com o nome de seu hub de notificação e a cadeia de conexão para *DefaultListenSharedAccessSignature* obtidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="da961-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="da961-129">Como as credenciais que são distribuídas com um aplicativo cliente não são geralmente seguras, você só deve distribuir a chave para acesso de escuta com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="da961-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="da961-130">O acesso de escuta permite que seu aplicativo se registre para receber notificações, mas os registros existentes não podem ser modificados e as notificações não podem ser enviadas.</span><span class="sxs-lookup"><span data-stu-id="da961-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="da961-131">A chave de acesso completa é usada em um serviço back-end protegido para enviar notificações e alterar os registros existentes.</span><span class="sxs-lookup"><span data-stu-id="da961-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="da961-132">Em seguida, adicione as seguintes importações e o método `subscribe` para manipular o evento de clique do botão assinar:</span><span class="sxs-lookup"><span data-stu-id="da961-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="da961-133">Esse método cria uma lista de categorias e usa a classe **Notificações** para armazenar a lista no armazenamento local e registrar os rótulos correspondentes com o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="da961-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="da961-134">Quando as categorias são alteradas, o registro é recriado com as novas categorias.</span><span class="sxs-lookup"><span data-stu-id="da961-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="da961-135">Seu aplicativo agora é capaz de armazenar um conjunto de categorias no armazenamento local do dispositivo e registrar com o hub de notificação, sempre que o usuário alterar a seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="da961-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="da961-136">Registrar-se para receber notificações</span><span class="sxs-lookup"><span data-stu-id="da961-136">Register for notifications</span></span>
<span data-ttu-id="da961-137">Estas etapas registram com o hub de notificação na inicialização, usando as categorias que foram armazenadas no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="da961-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="da961-138">Como o registrationId atribuído pelo Google Cloud Messaging (GCM) pode ser alterado a qualquer momento, você deve se registrar para receber notificações com frequência para evitar falhas de notificação.</span><span class="sxs-lookup"><span data-stu-id="da961-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="da961-139">Este exemplo registra a notificação a cada vez que o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="da961-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="da961-140">Para os aplicativos que são executados com frequência, mais de uma vez por dia, é possível ignorar o registro para preservar a largura de banda se tiver passado menos de um dia desde o registro anterior.</span><span class="sxs-lookup"><span data-stu-id="da961-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="da961-141">Adicione o código a seguir ao final do método **onCreate** na classe **MainActivity**:</span><span class="sxs-lookup"><span data-stu-id="da961-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="da961-142">Isso garante que o aplicativo recupere as categorias do armazenamento local e solicite um registro para essas categorias toda vez que ele for iniciado.</span><span class="sxs-lookup"><span data-stu-id="da961-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="da961-143">Em seguida, atualize o método `onStart()` na classe `MainActivity` como a seguir:</span><span class="sxs-lookup"><span data-stu-id="da961-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="da961-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="da961-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="da961-145">}</span><span class="sxs-lookup"><span data-stu-id="da961-145">}</span></span>
   
    <span data-ttu-id="da961-146">Isso atualiza a atividade principal com base no status de categorias salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="da961-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="da961-147">O aplicativo agora está completo e pode armazenar um conjunto de categorias no armazenamento local do dispositivo utilizado para registrá-las com o hub de notificação, sempre que o usuário alterar a seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="da961-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="da961-148">Em seguida, definiremos um back-end que possa enviar notificações de categoria para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da961-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="da961-149">Enviando notificações marcadas</span><span class="sxs-lookup"><span data-stu-id="da961-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="da961-150">Executar o aplicativo e gerar notificações</span><span class="sxs-lookup"><span data-stu-id="da961-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="da961-151">No Android Studio, compile o aplicativo e inicie-o em um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="da961-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="da961-152">Observe que a interface do usuário do aplicativo fornece um conjunto de alternâncias que permite escolher as categorias nas quais você poderá assinar.</span><span class="sxs-lookup"><span data-stu-id="da961-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="da961-153">Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.</span><span class="sxs-lookup"><span data-stu-id="da961-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="da961-154">O aplicativo converte as categorias selecionadas em rótulos e solicita um novo registro do dispositivo para os rótulos selecionados do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="da961-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="da961-155">As categorias registradas são retornadas e exibidas em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da961-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="da961-156">Envie uma nova notificação, executando o aplicativo de Console .NET.</span><span class="sxs-lookup"><span data-stu-id="da961-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="da961-157">Como alternativa, você pode enviar notificações de modelo marcado usando a guia depuração de seu hub de notificação no [Portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="da961-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="da961-158">As notificações para as categorias selecionadas são exibidas como notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="da961-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da961-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da961-159">Next steps</span></span>
<span data-ttu-id="da961-160">Neste tutorial, aprendemos a enviar as últimas notícias por categoria.</span><span class="sxs-lookup"><span data-stu-id="da961-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="da961-161">Considere a conclusão de um dos seguintes tutoriais que destacam outros cenários avançados de Hubs de Notificação:</span><span class="sxs-lookup"><span data-stu-id="da961-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="da961-162">[Usar os Hubs de Notificação para transmitir as últimas notícias localizadas]</span><span class="sxs-lookup"><span data-stu-id="da961-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="da961-163">Saiba como expandir o aplicativo das últimas notícias para habilitar o envio de notificações localizadas.</span><span class="sxs-lookup"><span data-stu-id="da961-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="da961-164">[Usar os Hubs de Notificação para transmitir as últimas notícias localizadas]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="da961-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="da961-165">[Portal clássico do Azure]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="da961-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
