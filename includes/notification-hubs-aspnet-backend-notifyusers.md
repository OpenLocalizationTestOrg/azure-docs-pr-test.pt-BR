## <a name="create-hello-webapi-project"></a>Criar hello WebAPI projeto
Um novo back-end ASP.NET WebAPI será criado em seções Olá a seguir e terá três objetivos principais:

1. **Autenticação de clientes**: um manipulador de mensagens será adicionado posteriormente solicitações de cliente tooauthenticate e usuário Olá associado com a solicitação de saudação.
2. **Registros de notificação do cliente**: mais tarde, você adicionará um controlador toohandle novos registros para notificações tooreceive um cliente. Olá nome de usuário autenticado será adicionado automaticamente toohello registro como um [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Enviar notificações tooClients**: posteriormente, você também adicionará uma tooprovide uma maneira de tootrigger um usuário um toodevices push segura do controlador e clientes associados Olá marca. 

Olá, as etapas a seguir mostra como toocreate Olá novo ASP.NET WebAPI back-end: 

> [!IMPORTANT]
> Se você estiver usando o Visual Studio 2015 ou anterior, antes de iniciar este tutorial, verifique se você instalou a versão mais recente de saudação do hello NuGet Package Manager. toocheck, iniciar o Visual Studio. De saudação **ferramentas** menu, clique em **extensões e atualizações**. Procurar **NuGet Package Manager** para sua versão do Visual Studio e verifique se você tem a versão mais recente do hello. Se não, desinstale e reinstale o hello NuGet Package Manager.
> 
> ![][B4]
> 
> [!NOTE]
> Verifique se você instalou Olá Visual Studio [SDK do Azure](https://azure.microsoft.com/downloads/) para implantação de site.
> 
> 

1. Inicie o Visual Studio ou o Visual Studio Express. Clique em **Server Explorer** e entrar tooyour conta do Azure. O Visual Studio será necessário que entrou em recursos do site Olá toocreate em sua conta.
2. No Visual Studio, clique em **arquivo**, em seguida, clique em **novo**, em seguida, **projeto**, expanda **modelos**, **Visual C#**, em seguida, clique em **Web** e **aplicativo Web ASP.NET**, o nome do tipo hello **AppBackend**e, em seguida, clique em **Okey**. 
   
    ![][B1]
3. Em Olá **novo projeto ASP.NET** caixa de diálogo, clique em **API da Web**, em seguida, clique em **Okey**.
   
    ![][B2]
4. Em Olá **configurar o aplicativo de Web do Microsoft Azure** caixa de diálogo, escolha uma assinatura e um **plano de serviço de aplicativo** você já tiver criado. Você também pode escolher **criar um novo plano de serviço de aplicativo** e criar uma caixa de diálogo de saudação. Não é necessário um banco de dados para este tutorial. Depois que você selecionou seu plano de serviço de aplicativo, clique em **Okey** toocreate projeto de saudação.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>Autenticar clientes toohello WebAPI Backend
Nesta seção, você criará uma nova classe de manipulador de mensagem denominada **AuthenticationTestHandler** para Olá novo back-end. Essa classe é derivada de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e adicionado como um manipulador de mensagens para poder processar todas as solicitações que entram Olá back-end. 

1. No Gerenciador de soluções, clique com botão direito Olá **AppBackend** de projeto, clique em **adicionar**, em seguida, clique em **classe**. Nomeie a nova classe de saudação **AuthenticationTestHandler.cs**e clique em **adicionar** toogenerate classe de saudação. Essa classe será usado tooauthenticate usuários usando *autenticação básica* para manter a simplicidade. Observe que seu aplicativo pode utilizar qualquer esquema de autenticação.
2. Em AuthenticationTestHandler.cs, adicione o seguinte Olá `using` instruções:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. Em AuthenticationTestHandler.cs, substituindo Olá `AuthenticationTestHandler` definição da classe com hello código a seguir. 
   
    Este manipulador autorizará solicitação hello quando Olá três condições a seguir forem verdadeira:
   
   * solicitação de saudação incluída um *autorização* cabeçalho. 
   * Olá solicitação usa *básica* autenticação. 
   * cadeia de caracteres de nome de usuário Hello e cadeia de caracteres de senha Olá são Olá mesma cadeia de caracteres.
     
     Caso contrário, Olá solicitação será rejeitada. Essa não é uma autenticação verdadeira e uma abordagem de autorização. É apenas um exemplo muito simples para este tutorial.
     
     Se a mensagem de solicitação de saudação é autenticada e autorizada pelo Olá `AuthenticationTestHandler`, usuário de autenticação básica hello serão toohello anexado a solicitação atual no hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Informações do usuário em Olá HttpContext serão usadas por outro controlador (RegisterController) tooadd posteriormente um [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello solicitação de registro de notificação.
     
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
                       // Attach hello new principal object toohello current HttpContext object
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
     > **Observação de segurança**: Olá `AuthenticationTestHandler` classe não fornecerá autenticação true. Ele é usado toomimic somente a autenticação básica e não é seguro. Você deve implementar um mecanismo de autenticação seguro em seus aplicativos e serviços de produção.                
     > 
     > 
4. Adicionar Olá após código final Olá Olá `Register` método hello **App_Start/WebApiConfig.cs** manipulador de mensagem de saudação de tooregister de classe:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Salve suas alterações.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Se registrar para notificações usando Olá WebAPI Backend
Nesta seção, vamos adicionar que um novo toohandle de back-end de WebAPI de toohello controlador solicitações tooregister um usuário e dispositivo para notificações usando a biblioteca de saudação do cliente para hubs de notificação. controlador Olá adicionará uma marca de usuário para usuário Olá que foi autenticada e anexados toohello HttpContext por Olá `AuthenticationTestHandler`. marca de saudação terá o formato de cadeia de caracteres hello, `"username:<actual username>"`.

1. No Gerenciador de soluções, clique com botão direito Olá **AppBackend** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
2. No lado esquerdo do hello, clique em **Online**e procure **Microsoft.Azure.NotificationHubs** em Olá **pesquisa** caixa.
3. Na lista de resultados de saudação, clique em **Hubs de notificação do Microsoft Azure**e, em seguida, clique em **instalar**. Concluir a instalação de saudação e fechar a janela do Gerenciador de pacote de NuGet de saudação.
   
    Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.
4. Agora, vamos criar um novo arquivo de classe que representa a conexão de saudação com notificação hub usado toosend notificações. Em Olá Gerenciador de soluções, clique com botão direito Olá **modelos** pasta, clique em **adicionar**, em seguida, clique em **classe**. Nomeie a nova classe de saudação **Notifications.cs**, em seguida, clique em **adicionar** toogenerate classe de saudação. 
   
    ![][B6]
5. Em Notifications.cs, adicione o seguinte Olá `using` instrução na parte superior de saudação do arquivo hello:
   
        using Microsoft.Azure.NotificationHubs;
6. Substituir saudação `Notifications` definição com os seguintes Olá da classe e os espaços reservados de saudação dois tooreplace-se com a cadeia de conexão hello (com acesso completo) para o hub de notificação e Olá nome do hub (disponível em [Portal clássico do Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Em seguida, criaremos um novo controlador, chamado **RegisterController**. No Gerenciador de soluções, clique com botão direito Olá **controladores** pasta, em seguida, clique em **adicionar**, em seguida, clique em **controlador**. Clique em Olá **controlador de 2 de API da Web – vazio** item e, em seguida, clique em **adicionar**. Nomeie a nova classe de saudação **RegisterController**e, em seguida, clique em **adicionar** controlador de saudação toogenerate novamente.
   
    ![][B7]
   
    ![][B8]
8. Em RegisterController.cs, adicione o seguinte Olá `using` instruções:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Adicionar Olá seguindo o código dentro de saudação `RegisterController` definição da classe. Observe que esse código, vamos adicionar uma marca de usuário para usuário Olá que isso é anexado toohello HttpContext. usuário Olá foi autenticado e conectado toohello HttpContext pelo filtro de mensagem de saudação adicionamos, `AuthenticationTestHandler`. Você também pode adicionar tooverify verificações opcional que Olá usuário tem direitos tooregister para Olá solicitado marcas.
   
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
        // This creates or updates a registration (with provided channelURI) at hello specified id
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
   
            // add check if user is allowed tooadd these tags
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

## <a name="sending-notifications-from-hello-webapi-backend"></a>Enviar notificações de saudação WebAPI Backend
Nesta seção, você adicionar um novo controlador que expõe uma maneira de dispositivos de cliente toosend uma notificação com base na marca de nome de usuário hello usando a biblioteca de gerenciamento de serviço do Azure notificação Hubs em Olá ASP.NET WebAPI back-end.

1. Crie outro novo controlador chamado **NotificationsController**. Criá-lo Olá mesma maneira que você criou Olá **RegisterController** na seção anterior hello.
2. Em NotificationsController.cs, adicione o seguinte Olá `using` instruções:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Adicionar Olá após o método toohello **NotificationsController** classe.
   
    Esse código enviar um tipo de notificação com base em Olá serviço de notificação de plataforma (PNS) `pns` parâmetro. Olá valor `to_tag` é usado tooset hello *username* marca na mensagem de saudação. Essa marca deve corresponder a uma marca de nome de usuário de um registro de hub de notificação ativo. mensagem de notificação de saudação é extraída de corpo de saudação de solicitação POST hello e formatada para o destino de saudação PNS. 
   
    Dependendo Olá plataforma notificação PNS (serviço) que seus dispositivos com suporte usam notificações tooreceive, notificações diferentes têm suporte usando formatos diferentes. Por exemplo, em dispositivos do Windows, você pode usar uma [notificação do sistema com WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) à qual um outro PNS não dá suporte diretamente. Para que seu back-end precisem tooformat notificação de saudação em uma notificação com suporte para Olá PNS de dispositivos, você planejar toosupport. Use Olá envio apropriado API no hello [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
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
4. Pressione **F5** toorun Olá aplicativo e tooensure Olá precisão de seu trabalho até o momento. aplicativo Hello deve iniciar um navegador da web e exibir hello ASP.NET home page. 

## <a name="publish-hello-new-webapi-backend"></a>Publicar Olá novo WebAPI Backend
1. Agora podemos implantará essa tooan aplicativo site do Azure em ordem toomake-lo acessível de todos os dispositivos. Clique duas vezes em Olá **AppBackend** do projeto e selecione **publicar**.
2. Escolha **Serviço de Aplicativo do Microsoft Azure** como destino de publicação e clique em **Publicar**. Isso abre a saudação do serviço de aplicativo criar caixa de diálogo, que ajuda você a criar todos os Olá recursos do Azure necessários toorun Olá ASP.NET web aplicativo no Azure.

    ![][B15]
3. Em Olá **criar serviço de aplicativo** caixa de diálogo, selecione sua conta do Azure. Clique em **Alterar Tipo** e selecione **Aplicativo Web**. Lembre-Olá **nome do aplicativo Web** Olá fornecida e selecione **assinatura**, **grupo de recursos**, e **plano do serviço de aplicativo**.  Clique em **Criar**.

4. Anote Olá **URL do Site** propriedade Olá **resumo** seção. Chamaremos toothis URL como o *ponto de extremidade de back-end* posteriormente neste tutorial. Clique em **Publicar**.

5. Após a conclusão do assistente Olá, ela publica Olá ASP.NET web aplicativo tooAzure e, em seguida, inicia Olá aplicativo no navegador padrão de saudação.  Seu aplicativo poderá ser exibido nos Serviços de Aplicativo do Azure.

Olá URL usa o nome do aplicativo web hello que você especificou anteriormente, com hello formato http://<app_name>.azurewebsites.net.

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
