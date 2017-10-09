## <a name="create-hello-webapi-project"></a><span data-ttu-id="6e4c5-101">Criar hello WebAPI projeto</span><span class="sxs-lookup"><span data-stu-id="6e4c5-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="6e4c5-102">Um novo back-end ASP.NET WebAPI será criado em seções Olá a seguir e terá três objetivos principais:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="6e4c5-103">**Autenticação de clientes**: um manipulador de mensagens será adicionado posteriormente solicitações de cliente tooauthenticate e usuário Olá associado com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="6e4c5-104">**Registros de notificação do cliente**: mais tarde, você adicionará um controlador toohandle novos registros para notificações tooreceive um cliente.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="6e4c5-105">Olá nome de usuário autenticado será adicionado automaticamente toohello registro como um [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e4c5-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="6e4c5-106">**Enviar notificações tooClients**: posteriormente, você também adicionará uma tooprovide uma maneira de tootrigger um usuário um toodevices push segura do controlador e clientes associados Olá marca.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="6e4c5-107">Olá, as etapas a seguir mostra como toocreate Olá novo ASP.NET WebAPI back-end:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6e4c5-108">Se você estiver usando o Visual Studio 2015 ou anterior, antes de iniciar este tutorial, verifique se você instalou a versão mais recente de saudação do hello NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="6e4c5-109">toocheck, iniciar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="6e4c5-110">De saudação **ferramentas** menu, clique em **extensões e atualizações**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="6e4c5-111">Procurar **NuGet Package Manager** para sua versão do Visual Studio e verifique se você tem a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="6e4c5-112">Se não, desinstale e reinstale o hello NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="6e4c5-113">Verifique se você instalou Olá Visual Studio [SDK do Azure](https://azure.microsoft.com/downloads/) para implantação de site.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="6e4c5-114">Inicie o Visual Studio ou o Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="6e4c5-115">Clique em **Server Explorer** e entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="6e4c5-116">O Visual Studio será necessário que entrou em recursos do site Olá toocreate em sua conta.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="6e4c5-117">No Visual Studio, clique em **arquivo**, em seguida, clique em **novo**, em seguida, **projeto**, expanda **modelos**, **Visual C#**, em seguida, clique em **Web** e **aplicativo Web ASP.NET**, o nome do tipo hello **AppBackend**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="6e4c5-118">Em Olá **novo projeto ASP.NET** caixa de diálogo, clique em **API da Web**, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="6e4c5-119">Em Olá **configurar o aplicativo de Web do Microsoft Azure** caixa de diálogo, escolha uma assinatura e um **plano de serviço de aplicativo** você já tiver criado.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="6e4c5-120">Você também pode escolher **criar um novo plano de serviço de aplicativo** e criar uma caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="6e4c5-121">Não é necessário um banco de dados para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="6e4c5-122">Depois que você selecionou seu plano de serviço de aplicativo, clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="6e4c5-123">Autenticar clientes toohello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6e4c5-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="6e4c5-124">Nesta seção, você criará uma nova classe de manipulador de mensagem denominada **AuthenticationTestHandler** para Olá novo back-end.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="6e4c5-125">Essa classe é derivada de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e adicionado como um manipulador de mensagens para poder processar todas as solicitações que entram Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="6e4c5-126">No Gerenciador de soluções, clique com botão direito Olá **AppBackend** de projeto, clique em **adicionar**, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="6e4c5-127">Nomeie a nova classe de saudação **AuthenticationTestHandler.cs**e clique em **adicionar** toogenerate classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="6e4c5-128">Essa classe será usado tooauthenticate usuários usando *autenticação básica* para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="6e4c5-129">Observe que seu aplicativo pode utilizar qualquer esquema de autenticação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="6e4c5-130">Em AuthenticationTestHandler.cs, adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="6e4c5-131">Em AuthenticationTestHandler.cs, substituindo Olá `AuthenticationTestHandler` definição da classe com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="6e4c5-132">Este manipulador autorizará solicitação hello quando Olá três condições a seguir forem verdadeira:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="6e4c5-133">solicitação de saudação incluída um *autorização* cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="6e4c5-134">Olá solicitação usa *básica* autenticação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="6e4c5-135">cadeia de caracteres de nome de usuário Hello e cadeia de caracteres de senha Olá são Olá mesma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="6e4c5-136">Caso contrário, Olá solicitação será rejeitada.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="6e4c5-137">Essa não é uma autenticação verdadeira e uma abordagem de autorização.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="6e4c5-138">É apenas um exemplo muito simples para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="6e4c5-139">Se a mensagem de solicitação de saudação é autenticada e autorizada pelo Olá `AuthenticationTestHandler`, usuário de autenticação básica hello serão toohello anexado a solicitação atual no hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e4c5-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="6e4c5-140">Informações do usuário em Olá HttpContext serão usadas por outro controlador (RegisterController) tooadd posteriormente um [marca](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello solicitação de registro de notificação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="6e4c5-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="6e4c5-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="6e4c5-142">}</span><span class="sxs-lookup"><span data-stu-id="6e4c5-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="6e4c5-143">**Observação de segurança**: Olá `AuthenticationTestHandler` classe não fornecerá autenticação true.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="6e4c5-144">Ele é usado toomimic somente a autenticação básica e não é seguro.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="6e4c5-145">Você deve implementar um mecanismo de autenticação seguro em seus aplicativos e serviços de produção.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="6e4c5-146">Adicionar Olá após código final Olá Olá `Register` método hello **App_Start/WebApiConfig.cs** manipulador de mensagem de saudação de tooregister de classe:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="6e4c5-147">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="6e4c5-148">Se registrar para notificações usando Olá WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6e4c5-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="6e4c5-149">Nesta seção, vamos adicionar que um novo toohandle de back-end de WebAPI de toohello controlador solicitações tooregister um usuário e dispositivo para notificações usando a biblioteca de saudação do cliente para hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="6e4c5-150">controlador Olá adicionará uma marca de usuário para usuário Olá que foi autenticada e anexados toohello HttpContext por Olá `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="6e4c5-151">marca de saudação terá o formato de cadeia de caracteres hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="6e4c5-152">No Gerenciador de soluções, clique com botão direito Olá **AppBackend** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6e4c5-153">No lado esquerdo do hello, clique em **Online**e procure **Microsoft.Azure.NotificationHubs** em Olá **pesquisa** caixa.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="6e4c5-154">Na lista de resultados de saudação, clique em **Hubs de notificação do Microsoft Azure**e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="6e4c5-155">Concluir a instalação de saudação e fechar a janela do Gerenciador de pacote de NuGet de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="6e4c5-156">Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="6e4c5-157">Agora, vamos criar um novo arquivo de classe que representa a conexão de saudação com notificação hub usado toosend notificações.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="6e4c5-158">Em Olá Gerenciador de soluções, clique com botão direito Olá **modelos** pasta, clique em **adicionar**, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="6e4c5-159">Nomeie a nova classe de saudação **Notifications.cs**, em seguida, clique em **adicionar** toogenerate classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="6e4c5-160">Em Notifications.cs, adicione o seguinte Olá `using` instrução na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="6e4c5-161">Substituir saudação `Notifications` definição com os seguintes Olá da classe e os espaços reservados de saudação dois tooreplace-se com a cadeia de conexão hello (com acesso completo) para o hub de notificação e Olá nome do hub (disponível em [Portal clássico do Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="6e4c5-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="6e4c5-162">Em seguida, criaremos um novo controlador, chamado **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="6e4c5-163">No Gerenciador de soluções, clique com botão direito Olá **controladores** pasta, em seguida, clique em **adicionar**, em seguida, clique em **controlador**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="6e4c5-164">Clique em Olá **controlador de 2 de API da Web – vazio** item e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="6e4c5-165">Nomeie a nova classe de saudação **RegisterController**e, em seguida, clique em **adicionar** controlador de saudação toogenerate novamente.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="6e4c5-166">Em RegisterController.cs, adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="6e4c5-167">Adicionar Olá seguindo o código dentro de saudação `RegisterController` definição da classe.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="6e4c5-168">Observe que esse código, vamos adicionar uma marca de usuário para usuário Olá que isso é anexado toohello HttpContext.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="6e4c5-169">usuário Olá foi autenticado e conectado toohello HttpContext pelo filtro de mensagem de saudação adicionamos, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="6e4c5-170">Você também pode adicionar tooverify verificações opcional que Olá usuário tem direitos tooregister para Olá solicitado marcas.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="6e4c5-171">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="6e4c5-172">Enviar notificações de saudação WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6e4c5-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="6e4c5-173">Nesta seção, você adicionar um novo controlador que expõe uma maneira de dispositivos de cliente toosend uma notificação com base na marca de nome de usuário hello usando a biblioteca de gerenciamento de serviço do Azure notificação Hubs em Olá ASP.NET WebAPI back-end.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="6e4c5-174">Crie outro novo controlador chamado **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="6e4c5-175">Criá-lo Olá mesma maneira que você criou Olá **RegisterController** na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="6e4c5-176">Em NotificationsController.cs, adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="6e4c5-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="6e4c5-177">Adicionar Olá após o método toohello **NotificationsController** classe.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="6e4c5-178">Esse código enviar um tipo de notificação com base em Olá serviço de notificação de plataforma (PNS) `pns` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="6e4c5-179">Olá valor `to_tag` é usado tooset hello *username* marca na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="6e4c5-180">Essa marca deve corresponder a uma marca de nome de usuário de um registro de hub de notificação ativo.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="6e4c5-181">mensagem de notificação de saudação é extraída de corpo de saudação de solicitação POST hello e formatada para o destino de saudação PNS.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="6e4c5-182">Dependendo Olá plataforma notificação PNS (serviço) que seus dispositivos com suporte usam notificações tooreceive, notificações diferentes têm suporte usando formatos diferentes.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="6e4c5-183">Por exemplo, em dispositivos do Windows, você pode usar uma [notificação do sistema com WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) à qual um outro PNS não dá suporte diretamente.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="6e4c5-184">Para que seu back-end precisem tooformat notificação de saudação em uma notificação com suporte para Olá PNS de dispositivos, você planejar toosupport.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="6e4c5-185">Use Olá envio apropriado API no hello [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="6e4c5-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="6e4c5-186">Pressione **F5** toorun Olá aplicativo e tooensure Olá precisão de seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="6e4c5-187">aplicativo Hello deve iniciar um navegador da web e exibir hello ASP.NET home page.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="6e4c5-188">Publicar Olá novo WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6e4c5-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="6e4c5-189">Agora podemos implantará essa tooan aplicativo site do Azure em ordem toomake-lo acessível de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="6e4c5-190">Clique duas vezes em Olá **AppBackend** do projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="6e4c5-191">Escolha **Serviço de Aplicativo do Microsoft Azure** como destino de publicação e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="6e4c5-192">Isso abre a saudação do serviço de aplicativo criar caixa de diálogo, que ajuda você a criar todos os Olá recursos do Azure necessários toorun Olá ASP.NET web aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="6e4c5-193">Em Olá **criar serviço de aplicativo** caixa de diálogo, selecione sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="6e4c5-194">Clique em **Alterar Tipo** e selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="6e4c5-195">Lembre-Olá **nome do aplicativo Web** Olá fornecida e selecione **assinatura**, **grupo de recursos**, e **plano do serviço de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="6e4c5-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-196">Click **Create**.</span></span>

4. <span data-ttu-id="6e4c5-197">Anote Olá **URL do Site** propriedade Olá **resumo** seção.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="6e4c5-198">Chamaremos toothis URL como o *ponto de extremidade de back-end* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="6e4c5-199">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-199">Click **Publish**.</span></span>

5. <span data-ttu-id="6e4c5-200">Após a conclusão do assistente Olá, ela publica Olá ASP.NET web aplicativo tooAzure e, em seguida, inicia Olá aplicativo no navegador padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="6e4c5-201">Seu aplicativo poderá ser exibido nos Serviços de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="6e4c5-202">Olá URL usa o nome do aplicativo web hello que você especificou anteriormente, com hello formato http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="6e4c5-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
