
Esta seção mostra como toosend últimas notícias como marcados notificações de modelo de um aplicativo de console do .NET.

Se você estiver usando aplicativos móveis, consulte toohello [adicionar notificações de push para aplicativos móveis] tutorial e selecione a plataforma na parte superior da saudação.

Se você quiser toouse Java ou PHP consulte muito[como toouse Hubs de notificação do Java/PHP]. Você pode enviar notificações de qualquer back-end usando a [interface REST de Hubs de notificação].

Ignore as etapas 1 a 3, se você criou o aplicativo de console hello para enviar notificações quando concluído [começar com Hubs de notificação].

1. No Visual Studio, crie um novo aplicativo de console em Visual C#:
   
       ![][13]
2. No menu principal do Visual Studio hello, clique em **ferramentas**, **Gerenciador de biblioteca de pacote**, e **Package Manager Console**, em seguida, na janela de console Olá digite o seguinte e pressione **Insira**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá [pacote NuGet de Hubs Microsoft.Azure.Notification].
3. Abrir arquivo hello Program.cs e adicione o seguinte Olá `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
4. Em Olá `Program` classe, adicione Olá seguinte método ou substitua-o se ele já existe:
   
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
   
    Esse código envia uma notificação de modelo para cada uma das marcas de seis Olá na matriz de cadeia de caracteres de saudação. uso de saudação de marcas garante que dispositivos recebam as notificações somente para categorias de saudação registrada.
5. Olá acima código, substitua Olá `<hub name>` e `<connection string with full access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultFullSharedAccessSignature* do painel de saudação do hub de notificação .
6. Adicionar Olá Olá linhas a seguir **principal** método:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Crie aplicativo de console hello.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[começar com Hubs de notificação]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interface REST de Hubs de notificação]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[adicionar notificações de push para aplicativos móveis]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[como toouse Hubs de notificação do Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pacote NuGet de Hubs Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
