### <span data-ttu-id="bcfd7-101"><a name="server-auth"></a>Como autenticar com um provedor (fluxo de servidor)</span><span class="sxs-lookup"><span data-stu-id="bcfd7-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="bcfd7-102">os aplicativos móveis toohave gerenciar o processo de autenticação de saudação em seu aplicativo, você deve registrar seu aplicativo com seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="bcfd7-103">Em seguida, em seu serviço de aplicativo do Azure, você precisa tooconfigure Olá ID e segredo fornecida pelo seu provedor.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="bcfd7-104">Para obter mais informações, consulte o tutorial Olá [adicionar autenticação tooyour aplicativo](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="bcfd7-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="bcfd7-105">Depois que você registrou o seu provedor de identidade, chamar hello `.login()` método com nome de saudação do seu provedor.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="bcfd7-106">Por exemplo, toologin com o Facebook usar Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bcfd7-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="bcfd7-107">os valores válidos para o provedor de Olá Olá são 'aad', 'facebook', 'google', 'conta da Microsoft' e 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="bcfd7-108">Atualmente, a Autenticação do Google não funciona por meio de Fluxo de Servidor.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="bcfd7-109">tooauthenticate com o Google, você deve usar um [método cliente fluxo](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="bcfd7-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="bcfd7-110">Nesse caso, o serviço de aplicativo do Azure gerencia o fluxo de autenticação Olá OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="bcfd7-111">Exibe a página de logon de saudação do provedor selecionado hello e gera um token de autenticação do serviço de aplicativo após o logon com êxito com o provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="bcfd7-112">função de logon Hello, quando concluído, retorna um objeto JSON que expõe Olá ID de usuário e o serviço de aplicativo token de autenticação nos campos de identificação do usuário e authenticationToken hello, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="bcfd7-113">Esse token pode ser armazenado em cache e reutilizado até que expire.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="bcfd7-114"><a name="client-auth"></a>Como autenticar com um provedor (fluxo de cliente)</span><span class="sxs-lookup"><span data-stu-id="bcfd7-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="bcfd7-115">Seu aplicativo pode também independentemente entre em contato com o provedor de identidade hello e forneça Olá retornado tooyour token do serviço de aplicativo para autenticação.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="bcfd7-116">Esse fluxo de cliente permite que você tooprovide uma experiência de logon único para usuários ou dados de usuário adicionais tooretrieve saudação do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="bcfd7-117">Exemplo básico de autenticação social</span><span class="sxs-lookup"><span data-stu-id="bcfd7-117">Social Authentication basic example</span></span>

<span data-ttu-id="bcfd7-118">Este exemplo usa o SDK de cliente do Facebook para a autenticação:</span><span class="sxs-lookup"><span data-stu-id="bcfd7-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="bcfd7-119">Este exemplo assume esse token Olá fornecido pelo provedor respectivos Olá SDK é armazenado na variável de token de saudação.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="bcfd7-120">Exemplo de conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="bcfd7-120">Microsoft Account example</span></span>

<span data-ttu-id="bcfd7-121">Olá seguindo o exemplo usa Olá Live SDK, que oferece suporte a single-sign-on para aplicativos da Windows Store usando Account da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="bcfd7-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="bcfd7-122">Este exemplo obtém um token do Live Connect, que é fornecido tooyour do serviço de aplicativo chamando a função de logon hello.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="bcfd7-123"><a name="auth-getinfo"></a>Como: obter informações sobre o usuário autenticado de saudação</span><span class="sxs-lookup"><span data-stu-id="bcfd7-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="bcfd7-124">informações de autenticação Olá podem ser recuperadas da saudação `/.auth/me` chamada de ponto de extremidade usando um HTTP com qualquer biblioteca AJAX.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="bcfd7-125">Certifique-se de que você definir Olá `X-ZUMO-AUTH` token de autenticação do cabeçalho tooyour.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="bcfd7-126">Olá token de autenticação é armazenado no `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="bcfd7-127">Por exemplo, toouse Olá busca API:</span><span class="sxs-lookup"><span data-stu-id="bcfd7-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="bcfd7-128">O Fetch está disponível como um [pacote npm](https://www.npmjs.com/package/whatwg-fetch) ou para download do navegador do [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="bcfd7-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="bcfd7-129">Você também pode usar outras informações de saudação de toofetch de API do AJAX ou jQuery.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="bcfd7-130">Os dados são recebidos como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="bcfd7-130">Data is received as a JSON object.</span></span>
