
<span data-ttu-id="d93a4-101">Esta seção mostra como toosend últimas notícias como marcados notificações de modelo de um aplicativo de console do .NET.</span><span class="sxs-lookup"><span data-stu-id="d93a4-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="d93a4-102">Se você estiver usando aplicativos móveis, consulte toohello [adicionar notificações de push para aplicativos móveis] tutorial e selecione a plataforma na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d93a4-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="d93a4-103">Se você quiser toouse Java ou PHP consulte muito[como toouse Hubs de notificação do Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="d93a4-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="d93a4-104">Você pode enviar notificações de qualquer back-end usando a [interface REST de Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="d93a4-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="d93a4-105">Ignore as etapas 1 a 3, se você criou o aplicativo de console hello para enviar notificações quando concluído [começar com Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="d93a4-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="d93a4-106">No Visual Studio, crie um novo aplicativo de console em Visual C#:</span><span class="sxs-lookup"><span data-stu-id="d93a4-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="d93a4-107">No menu principal do Visual Studio hello, clique em **ferramentas**, **Gerenciador de biblioteca de pacote**, e **Package Manager Console**, em seguida, na janela de console Olá digite o seguinte e pressione **Insira**:</span><span class="sxs-lookup"><span data-stu-id="d93a4-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="d93a4-108">Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá [pacote NuGet de Hubs Microsoft.Azure.Notification].</span><span class="sxs-lookup"><span data-stu-id="d93a4-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="d93a4-109">Abrir arquivo hello Program.cs e adicione o seguinte Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="d93a4-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="d93a4-110">Em Olá `Program` classe, adicione Olá seguinte método ou substitua-o se ele já existe:</span><span class="sxs-lookup"><span data-stu-id="d93a4-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="d93a4-111">Esse código envia uma notificação de modelo para cada uma das marcas de seis Olá na matriz de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="d93a4-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="d93a4-112">uso de saudação de marcas garante que dispositivos recebam as notificações somente para categorias de saudação registrada.</span><span class="sxs-lookup"><span data-stu-id="d93a4-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="d93a4-113">Olá acima código, substitua Olá `<hub name>` e `<connection string with full access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultFullSharedAccessSignature* do painel de saudação do hub de notificação .</span><span class="sxs-lookup"><span data-stu-id="d93a4-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="d93a4-114">Adicionar Olá Olá linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="d93a4-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="d93a4-115">Crie aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="d93a4-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[começar com Hubs de notificação]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interface REST de Hubs de notificação]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[adicionar notificações de push para aplicativos móveis]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[como toouse Hubs de notificação do Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pacote NuGet de Hubs Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
