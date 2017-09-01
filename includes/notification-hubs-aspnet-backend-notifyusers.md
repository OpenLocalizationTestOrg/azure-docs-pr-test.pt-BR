## <a name="create-the-webapi-project"></a>Criar o projeto WebAPI
Um novo back-end da API Web ASP.NET será criado nas seções a seguir e terá três objetivos principais:

1. **Autenticar Clientes**: um manipulador de mensagens será adicionado posteriormente para autenticar solicitações de cliente e associar o usuário à solicitação.
2. **Registros de Notificação do Cliente**: mais tarde, você adicionará um controlador para manipular novos registros para um dispositivo cliente receber notificações. O nome de usuário autenticado será automaticamente adicionado ao registro como uma [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Enviar notificações aos clientes**: posteriormente, você também adicionará um controlador para fornecer uma maneira para um usuário disparar um envio por push seguro para dispositivos e clientes associados à marca. 

As etapas a seguir mostram como criar o novo back-end da API Web ASP.NET: 

> [!IMPORTANT]
> Se você estiver usando o Visual Studio 2015 ou anterior, antes de iniciar este tutorial, instale a versão mais recente do Gerenciador de Pacotes NuGet. Para verificar, inicie o Visual Studio. No menu **Ferramentas**, clique em **Extensões e Atualizações**. Pesquise por **Gerenciador de Pacotes NuGet** para sua versão do Visual Studio, e verifique se versão mais recente está instalada. Se não tiver, desinstale o Gerenciador de Pacotes NuGet e instale-o novamente.
> 
> ![][B4]
> 
> [!NOTE]
> Verifique se você instalou o [SDK do Azure](https://azure.microsoft.com/downloads/) do Visual Studio para implantação de site.
> 
> 

1. Inicie o Visual Studio ou o Visual Studio Express. Clique em **Gerenciador de Servidores** e entre na sua conta do Azure. Será preciso que você se conecte para que o Visual Studio crie os recursos do site na sua conta.
2. No Visual Studio, clique em **Arquivo**, clique em **Novo**, **Projeto**, expanda **Modelos**, **Visual C#** e clique em **Web** e em **Aplicativo Web ASP.NET**, digite o nome **AppBackend** e clique em **OK**. 
   
    ![][B1]
3. Na caixa de diálogo **Novo Projeto ASP.NET**, clique em **API Web** e, por último, clique em **OK**.
   
    ![][B2]
4. Na caixa de diálogo **Configurar o Aplicativo Web do Microsoft Azure**, escolha uma assinatura e um **Plano do Serviço de Aplicativo** que você já criou. Você também pode escolher **Criar um novo plano de serviço de aplicativo** e criá-lo na caixa de diálogo. Não é necessário um banco de dados para este tutorial. Depois que você tiver selecionado o seu plano de serviço de aplicativo, clique em **OK** para criar o projeto.
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a>Autenticando clientes para o back-end de API da Web
Nesta seção, você criará uma nova classe de manipulador de mensagens denominada **AuthenticationTestHandler** para o novo back-end. Essa classe é derivada de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e adicionada como um manipulador de mensagens para poder processar todas as solicitações que chegam ao back-end. 

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **AppBackend**, clique em **Adicionar**. Em seguida, clique em **Classe**. Nomeie a nova classe **AuthenticationTestHandler.cs** e clique em **Adicionar** para gerar a classe. Essa classe será utilizada para autenticar usuários com a *Autenticação Básica* para manter a simplicidade. Observe que seu aplicativo pode utilizar qualquer esquema de autenticação.
2. Em AuthenticationTestHandler.cs, adicione as seguintes instruções `using`:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. Em AuthenticationTestHandler.cs, substitua a definição da classe `AuthenticationTestHandler` pelo código a seguir. 
   
    Esse manipulador autorizará a solicitação quando as três seguintes condições forem verdadeiras:
   
   * A solicitação incluía um cabeçalho de *Autorização* . 
   * A solicitação usa a autenticação *básica* . 
   * A cadeia de caracteres de nome de usuário e a cadeia de caracteres de senha são iguais.
     
     Caso contrário, a solicitação será rejeitada. Essa não é uma autenticação verdadeira e uma abordagem de autorização. É apenas um exemplo muito simples para este tutorial.
     
     Se a mensagem de solicitação for autenticada e autorizada pelo `AuthenticationTestHandler`, em seguida, o usuário de autenticação básica será anexado à solicitação atual no [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). As informações do usuário no HttpContext serão usadas por outro controlador (RegisterController) posteriormente para adicionar uma [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx) à solicitação de registro de notificação.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach the new principal object to the current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Nota de Segurança**: a classe `AuthenticationTestHandler` não oferece autenticação verdadeira. Ela é usada somente para imitar a autenticação básica e não é segura. Você deve implementar um mecanismo de autenticação seguro em seus aplicativos e serviços de produção.                
     > 
     > 
4. Adicione o seguinte código ao final do método `Register` na classe **App_Start/WebApiConfig.cs** para registrar o manipulador de mensagens:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Salve suas alterações.

## <a name="registering-for-notifications-using-the-webapi-backend"></a>Registrar-se nas Notificações usando o backup-end da API Web
Nesta seção, adicionaremos um novo controlador ao back-end da API Web para manipular solicitações para registrar um usuário e um dispositivo para notificações usando a biblioteca de cliente dos hubs de notificação. O controlador adicionará uma marca de usuário ao usuário que foi autenticado e anexado a HttpContext pelo `AuthenticationTestHandler`. A marca terá o formato de cadeia de caracteres, `"username:<actual username>"`.

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **AppBackend** e clique em **Gerenciar Pacotes NuGet**.
2. No lado esquerdo, clique em **Online** e procure **Microsoft.Azure.NotificationHubs** na caixa **Pesquisar**.
3. Na lista de resultados, clique em **Hubs de Notificação do Microsoft Azure** e, em seguida, clique em **Instalar**. Conclua a instalação e, por fim, feche a janela do gerenciador de pacotes NuGet.
   
    Isso adiciona uma referência ao SDK dos Hubs de Notificação do Azure usando o <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet Microsoft.Azure.Notification Hubs</a>.
4. Agora criaremos um novo arquivo de classe que representa a conexão com o hub de notificação usado para enviar notificações. No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Modelos**, clique em **Adicionar** e, em seguida, em **Classe**. Nomeie a nova classe como **Notifications.cs**, clique em **Adicionar** para gerar a classe. 
   
    ![][B6]
5. Em Notifications.cs, adicione a seguinte instrução `using` à parte superior do arquivo:
   
        using Microsoft.Azure.NotificationHubs;
6. Substitua a definição da classe `Notifications` pelo seguinte e certifique-se de substituir os dois espaços reservados pela cadeia de conexão (com acesso completo) para o hub de notificação e o nome do hub (disponível no [Portal Clássico do Azure](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Em seguida, criaremos um novo controlador, chamado **RegisterController**. No Gerenciador de Soluções, clique com o botão direito na pasta **Controladores**, depois em **Adicionar**, por fim clique em **Controlador**. Clique no item **Controlador de API Web 2 -- Vazio**, depois clique em **Adicionar**. Nomeie a nova classe **RegisterController**, em seguida clique em **Adicionar** novamente para gerar o controlador.
   
    ![][B7]
   
    ![][B8]
8. Em RegisterController.cs, adicione as seguintes instruções `using` :
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Adicione o código a seguir à definição de classe `RegisterController` . Observe que, nesse código, adicionamos uma marca de usuário para o usuário anexado ao HttpContext. O usuário foi autenticado e anexado ao HttpContext pelo filtro de mensagens que adicionamos, `AuthenticationTestHandler`. Você também pode adicionar verificações opcionais para conferir se o usuário tem direitos para registro das tags requeridas.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at the specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed to add these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Salve suas alterações.

## <a name="sending-notifications-from-the-webapi-backend"></a>Enviando notificações do back-end da API Web
Nesta seção, você adiciona um novo controlador que expõe uma maneira para dispositivos clientes enviarem uma notificação com base na marca de nome de usuário usando a Biblioteca de Gerenciamento de Serviços dos Hubs de Notificação do Azure no back-end da API Web no ASP.NET.

1. Crie outro novo controlador chamado **NotificationsController**. Crie-o da mesma maneira como você criou o **RegisterController** na seção anterior.
2. Em NotificationsController.cs, adicione as seguintes instruções `using` :
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Adicione o método a seguir à classe **NotificationsController** .
   
    Esse código envia um tipo de notificação com base no parâmetro `pns` do PNS (Platform Notification Service). O valor de `to_tag` é usado para definir a marca *username* na mensagem. Essa marca deve corresponder a uma marca de nome de usuário de um registro de hub de notificação ativo. A mensagem de notificação é recuperada do corpo da solicitação POST e formatada para o PNS de destino. 
   
    Dependendo do PNS (Serviço de Notificação de Plataforma) que seus dispositivos com suporte usam para receber notificações, diferentes notificações têm suporte usando diferentes formatos. Por exemplo, em dispositivos do Windows, você pode usar uma [notificação do sistema com WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) à qual um outro PNS não dá suporte diretamente. Então, o back-end precisaria formatar a notificação em uma notificação com suporte para o PNS de dispositivos para os quais que você planeja dar suporte. Em seguida, use a API de envio apropriada na [classe NotificationHubClient](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Pressione **F5** para executar o aplicativo e garantir a precisão de seu trabalho até aqui. O aplicativo deve inicializar um navegador da Web e exibir a página inicial ASP.NET. 

## <a name="publish-the-new-webapi-backend"></a>Publicar o novo back-end da API Web
1. Agora, implantaremos esse aplicativo em um Site do Azure para torná-lo acessível de todos os dispositivos. Clique com o botão direito do mouse no projeto **AppBackend** e selecione **Publicar**.
2. Escolha **Serviço de Aplicativo do Microsoft Azure** como destino de publicação e clique em **Publicar**. Isso abre a caixa de diálogo Criar Serviço de Aplicativo, o que ajuda a criar todos os recursos do Azure necessários para executar seu aplicativo Web ASP.NET no Azure.

    ![][B15]
3. Na caixa de diálogo **Criar Serviço de Aplicativo**, selecione sua conta do Azure. Clique em **Alterar Tipo** e selecione **Aplicativo Web**. Mantenha o **Nome do Aplicativo Web** fornecido e selecione a **Assinatura**, **Grupo de Recursos** e **Plano do Serviço de Aplicativo**.  Clique em **Criar**.

4. Anote a propriedade **URL do Site** na seção **Resumo**. Iremos nos referir a essa URL, posteriormente neste tutorial, como seu *ponto de extremidade de back-end* . Clique em **Publicar**.

5. Depois que o assistente é concluído, ele publica o aplicativo Web ASP.NET no Azure e, em seguida, inicia o aplicativo no navegador padrão.  Seu aplicativo poderá ser exibido nos Serviços de Aplicativo do Azure.

A URL usa o nome do aplicativo Web especificado anteriormente, com o formato http://<app_name>.azurewebsites.net.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
