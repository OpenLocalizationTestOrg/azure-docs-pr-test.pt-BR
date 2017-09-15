## <a name="create-the-webapi-project"></a><span data-ttu-id="44755-101">Criar o projeto WebAPI</span><span class="sxs-lookup"><span data-stu-id="44755-101">Create the WebAPI Project</span></span>
<span data-ttu-id="44755-102">Um novo back-end da API Web ASP.NET será criado nas seções a seguir e terá três objetivos principais:</span><span class="sxs-lookup"><span data-stu-id="44755-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="44755-103">**Autenticar Clientes**: um manipulador de mensagens será adicionado posteriormente para autenticar solicitações de cliente e associar o usuário à solicitação.</span><span class="sxs-lookup"><span data-stu-id="44755-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="44755-104">**Registros de Notificação do Cliente**: mais tarde, você adicionará um controlador para manipular novos registros para um dispositivo cliente receber notificações.</span><span class="sxs-lookup"><span data-stu-id="44755-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="44755-105">O nome de usuário autenticado será automaticamente adicionado ao registro como uma [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="44755-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="44755-106">**Enviar notificações aos clientes**: posteriormente, você também adicionará um controlador para fornecer uma maneira para um usuário disparar um envio por push seguro para dispositivos e clientes associados à marca.</span><span class="sxs-lookup"><span data-stu-id="44755-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="44755-107">As etapas a seguir mostram como criar o novo back-end da API Web ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="44755-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="44755-108">Se você estiver usando o Visual Studio 2015 ou anterior, antes de iniciar este tutorial, instale a versão mais recente do Gerenciador de Pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="44755-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="44755-109">Para verificar, inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44755-109">To check, start Visual Studio.</span></span> <span data-ttu-id="44755-110">No menu **Ferramentas**, clique em **Extensões e Atualizações**.</span><span class="sxs-lookup"><span data-stu-id="44755-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="44755-111">Pesquise por **Gerenciador de Pacotes NuGet** para sua versão do Visual Studio, e verifique se versão mais recente está instalada.</span><span class="sxs-lookup"><span data-stu-id="44755-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="44755-112">Se não tiver, desinstale o Gerenciador de Pacotes NuGet e instale-o novamente.</span><span class="sxs-lookup"><span data-stu-id="44755-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="44755-113">Verifique se você instalou o [SDK do Azure](https://azure.microsoft.com/downloads/) do Visual Studio para implantação de site.</span><span class="sxs-lookup"><span data-stu-id="44755-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="44755-114">Inicie o Visual Studio ou o Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="44755-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="44755-115">Clique em **Gerenciador de Servidores** e entre na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="44755-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="44755-116">Será preciso que você se conecte para que o Visual Studio crie os recursos do site na sua conta.</span><span class="sxs-lookup"><span data-stu-id="44755-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="44755-117">No Visual Studio, clique em **Arquivo**, clique em **Novo**, **Projeto**, expanda **Modelos**, **Visual C#** e clique em **Web** e em **Aplicativo Web ASP.NET**, digite o nome **AppBackend** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="44755-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="44755-118">Na caixa de diálogo **Novo Projeto ASP.NET**, clique em **API Web** e, por último, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="44755-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="44755-119">Na caixa de diálogo **Configurar o Aplicativo Web do Microsoft Azure**, escolha uma assinatura e um **Plano do Serviço de Aplicativo** que você já criou.</span><span class="sxs-lookup"><span data-stu-id="44755-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="44755-120">Você também pode escolher **Criar um novo plano de serviço de aplicativo** e criá-lo na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44755-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="44755-121">Não é necessário um banco de dados para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="44755-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="44755-122">Depois que você tiver selecionado o seu plano de serviço de aplicativo, clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="44755-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="44755-123">Autenticando clientes para o back-end de API da Web</span><span class="sxs-lookup"><span data-stu-id="44755-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="44755-124">Nesta seção, você criará uma nova classe de manipulador de mensagens denominada **AuthenticationTestHandler** para o novo back-end.</span><span class="sxs-lookup"><span data-stu-id="44755-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="44755-125">Essa classe é derivada de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e adicionada como um manipulador de mensagens para poder processar todas as solicitações que chegam ao back-end.</span><span class="sxs-lookup"><span data-stu-id="44755-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="44755-126">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **AppBackend**, clique em **Adicionar**. Em seguida, clique em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="44755-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="44755-127">Nomeie a nova classe **AuthenticationTestHandler.cs** e clique em **Adicionar** para gerar a classe.</span><span class="sxs-lookup"><span data-stu-id="44755-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="44755-128">Essa classe será utilizada para autenticar usuários com a *Autenticação Básica* para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="44755-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="44755-129">Observe que seu aplicativo pode utilizar qualquer esquema de autenticação.</span><span class="sxs-lookup"><span data-stu-id="44755-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="44755-130">Em AuthenticationTestHandler.cs, adicione as seguintes instruções `using`:</span><span class="sxs-lookup"><span data-stu-id="44755-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="44755-131">Em AuthenticationTestHandler.cs, substitua a definição da classe `AuthenticationTestHandler` pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="44755-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="44755-132">Esse manipulador autorizará a solicitação quando as três seguintes condições forem verdadeiras:</span><span class="sxs-lookup"><span data-stu-id="44755-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="44755-133">A solicitação incluía um cabeçalho de *Autorização* .</span><span class="sxs-lookup"><span data-stu-id="44755-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="44755-134">A solicitação usa a autenticação *básica* .</span><span class="sxs-lookup"><span data-stu-id="44755-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="44755-135">A cadeia de caracteres de nome de usuário e a cadeia de caracteres de senha são iguais.</span><span class="sxs-lookup"><span data-stu-id="44755-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="44755-136">Caso contrário, a solicitação será rejeitada.</span><span class="sxs-lookup"><span data-stu-id="44755-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="44755-137">Essa não é uma autenticação verdadeira e uma abordagem de autorização.</span><span class="sxs-lookup"><span data-stu-id="44755-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="44755-138">É apenas um exemplo muito simples para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="44755-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="44755-139">Se a mensagem de solicitação for autenticada e autorizada pelo `AuthenticationTestHandler`, em seguida, o usuário de autenticação básica será anexado à solicitação atual no [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="44755-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="44755-140">As informações do usuário no HttpContext serão usadas por outro controlador (RegisterController) posteriormente para adicionar uma [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx) à solicitação de registro de notificação.</span><span class="sxs-lookup"><span data-stu-id="44755-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="44755-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="44755-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="44755-142">}</span><span class="sxs-lookup"><span data-stu-id="44755-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="44755-143">**Nota de Segurança**: a classe `AuthenticationTestHandler` não oferece autenticação verdadeira.</span><span class="sxs-lookup"><span data-stu-id="44755-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="44755-144">Ela é usada somente para imitar a autenticação básica e não é segura.</span><span class="sxs-lookup"><span data-stu-id="44755-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="44755-145">Você deve implementar um mecanismo de autenticação seguro em seus aplicativos e serviços de produção.</span><span class="sxs-lookup"><span data-stu-id="44755-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="44755-146">Adicione o seguinte código ao final do método `Register` na classe **App_Start/WebApiConfig.cs** para registrar o manipulador de mensagens:</span><span class="sxs-lookup"><span data-stu-id="44755-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="44755-147">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="44755-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="44755-148">Registrar-se nas Notificações usando o backup-end da API Web</span><span class="sxs-lookup"><span data-stu-id="44755-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="44755-149">Nesta seção, adicionaremos um novo controlador ao back-end da API Web para manipular solicitações para registrar um usuário e um dispositivo para notificações usando a biblioteca de cliente dos hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="44755-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="44755-150">O controlador adicionará uma marca de usuário ao usuário que foi autenticado e anexado a HttpContext pelo `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="44755-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="44755-151">A marca terá o formato de cadeia de caracteres, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="44755-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="44755-152">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **AppBackend** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="44755-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="44755-153">No lado esquerdo, clique em **Online** e procure **Microsoft.Azure.NotificationHubs** na caixa **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="44755-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="44755-154">Na lista de resultados, clique em **Hubs de Notificação do Microsoft Azure** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="44755-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="44755-155">Conclua a instalação e, por fim, feche a janela do gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="44755-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="44755-156">Isso adiciona uma referência ao SDK dos Hubs de Notificação do Azure usando o <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="44755-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="44755-157">Agora criaremos um novo arquivo de classe que representa a conexão com o hub de notificação usado para enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="44755-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="44755-158">No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Modelos**, clique em **Adicionar** e, em seguida, em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="44755-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="44755-159">Nomeie a nova classe como **Notifications.cs**, clique em **Adicionar** para gerar a classe.</span><span class="sxs-lookup"><span data-stu-id="44755-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="44755-160">Em Notifications.cs, adicione a seguinte instrução `using` à parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="44755-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="44755-161">Substitua a definição da classe `Notifications` pelo seguinte e certifique-se de substituir os dois espaços reservados pela cadeia de conexão (com acesso completo) para o hub de notificação e o nome do hub (disponível no [Portal Clássico do Azure](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="44755-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="44755-162">Em seguida, criaremos um novo controlador, chamado **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="44755-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="44755-163">No Gerenciador de Soluções, clique com o botão direito na pasta **Controladores**, depois em **Adicionar**, por fim clique em **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="44755-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="44755-164">Clique no item **Controlador de API Web 2 -- Vazio**, depois clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="44755-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="44755-165">Nomeie a nova classe **RegisterController**, em seguida clique em **Adicionar** novamente para gerar o controlador.</span><span class="sxs-lookup"><span data-stu-id="44755-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="44755-166">Em RegisterController.cs, adicione as seguintes instruções `using` :</span><span class="sxs-lookup"><span data-stu-id="44755-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="44755-167">Adicione o código a seguir à definição de classe `RegisterController` .</span><span class="sxs-lookup"><span data-stu-id="44755-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="44755-168">Observe que, nesse código, adicionamos uma marca de usuário para o usuário anexado ao HttpContext.</span><span class="sxs-lookup"><span data-stu-id="44755-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="44755-169">O usuário foi autenticado e anexado ao HttpContext pelo filtro de mensagens que adicionamos, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="44755-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="44755-170">Você também pode adicionar verificações opcionais para conferir se o usuário tem direitos para registro das tags requeridas.</span><span class="sxs-lookup"><span data-stu-id="44755-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
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
10. <span data-ttu-id="44755-171">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="44755-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="44755-172">Enviando notificações do back-end da API Web</span><span class="sxs-lookup"><span data-stu-id="44755-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="44755-173">Nesta seção, você adiciona um novo controlador que expõe uma maneira para dispositivos clientes enviarem uma notificação com base na marca de nome de usuário usando a Biblioteca de Gerenciamento de Serviços dos Hubs de Notificação do Azure no back-end da API Web no ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="44755-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="44755-174">Crie outro novo controlador chamado **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="44755-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="44755-175">Crie-o da mesma maneira como você criou o **RegisterController** na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="44755-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="44755-176">Em NotificationsController.cs, adicione as seguintes instruções `using` :</span><span class="sxs-lookup"><span data-stu-id="44755-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="44755-177">Adicione o método a seguir à classe **NotificationsController** .</span><span class="sxs-lookup"><span data-stu-id="44755-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="44755-178">Esse código envia um tipo de notificação com base no parâmetro `pns` do PNS (Platform Notification Service).</span><span class="sxs-lookup"><span data-stu-id="44755-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="44755-179">O valor de `to_tag` é usado para definir a marca *username* na mensagem.</span><span class="sxs-lookup"><span data-stu-id="44755-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="44755-180">Essa marca deve corresponder a uma marca de nome de usuário de um registro de hub de notificação ativo.</span><span class="sxs-lookup"><span data-stu-id="44755-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="44755-181">A mensagem de notificação é recuperada do corpo da solicitação POST e formatada para o PNS de destino.</span><span class="sxs-lookup"><span data-stu-id="44755-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="44755-182">Dependendo do PNS (Serviço de Notificação de Plataforma) que seus dispositivos com suporte usam para receber notificações, diferentes notificações têm suporte usando diferentes formatos.</span><span class="sxs-lookup"><span data-stu-id="44755-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="44755-183">Por exemplo, em dispositivos do Windows, você pode usar uma [notificação do sistema com WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) à qual um outro PNS não dá suporte diretamente.</span><span class="sxs-lookup"><span data-stu-id="44755-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="44755-184">Então, o back-end precisaria formatar a notificação em uma notificação com suporte para o PNS de dispositivos para os quais que você planeja dar suporte.</span><span class="sxs-lookup"><span data-stu-id="44755-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="44755-185">Em seguida, use a API de envio apropriada na [classe NotificationHubClient](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="44755-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="44755-186">Pressione **F5** para executar o aplicativo e garantir a precisão de seu trabalho até aqui.</span><span class="sxs-lookup"><span data-stu-id="44755-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="44755-187">O aplicativo deve inicializar um navegador da Web e exibir a página inicial ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="44755-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="44755-188">Publicar o novo back-end da API Web</span><span class="sxs-lookup"><span data-stu-id="44755-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="44755-189">Agora, implantaremos esse aplicativo em um Site do Azure para torná-lo acessível de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="44755-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="44755-190">Clique com o botão direito do mouse no projeto **AppBackend** e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="44755-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="44755-191">Escolha **Serviço de Aplicativo do Microsoft Azure** como destino de publicação e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="44755-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="44755-192">Isso abre a caixa de diálogo Criar Serviço de Aplicativo, o que ajuda a criar todos os recursos do Azure necessários para executar seu aplicativo Web ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="44755-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="44755-193">Na caixa de diálogo **Criar Serviço de Aplicativo**, selecione sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="44755-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="44755-194">Clique em **Alterar Tipo** e selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="44755-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="44755-195">Mantenha o **Nome do Aplicativo Web** fornecido e selecione a **Assinatura**, **Grupo de Recursos** e **Plano do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="44755-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="44755-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="44755-196">Click **Create**.</span></span>

4. <span data-ttu-id="44755-197">Anote a propriedade **URL do Site** na seção **Resumo**.</span><span class="sxs-lookup"><span data-stu-id="44755-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="44755-198">Iremos nos referir a essa URL, posteriormente neste tutorial, como seu *ponto de extremidade de back-end* .</span><span class="sxs-lookup"><span data-stu-id="44755-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="44755-199">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="44755-199">Click **Publish**.</span></span>

5. <span data-ttu-id="44755-200">Depois que o assistente é concluído, ele publica o aplicativo Web ASP.NET no Azure e, em seguida, inicia o aplicativo no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="44755-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="44755-201">Seu aplicativo poderá ser exibido nos Serviços de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="44755-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="44755-202">A URL usa o nome do aplicativo Web especificado anteriormente, com o formato http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="44755-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

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
