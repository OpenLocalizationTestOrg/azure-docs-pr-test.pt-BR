### <span data-ttu-id="53267-101"><a name="server-auth"></a>Como autenticar com um provedor (fluxo de servidor)</span><span class="sxs-lookup"><span data-stu-id="53267-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="53267-102">Para que os Aplicativos Móveis gerenciem o processo de autenticação em seu aplicativo, é necessário registrá-los no provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="53267-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="53267-103">Em seguida, no Serviço de Aplicativo do Azure, você precisa configurar a ID e o segredo do aplicativo fornecidos por seu provedor.</span><span class="sxs-lookup"><span data-stu-id="53267-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="53267-104">Para obter mais informações, consulte o tutorial [Adicionar autenticação ao seu aplicativo](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="53267-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="53267-105">Depois de registrar seu provedor de identidade, chame o método `.login()` com o nome do seu provedor.</span><span class="sxs-lookup"><span data-stu-id="53267-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="53267-106">Por exemplo, para fazer logon com o Facebook, use o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="53267-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="53267-107">Os valores válidos para o provedor são 'add', 'facebook', 'google', 'microsoftaccount' e 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="53267-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="53267-108">Atualmente, a Autenticação do Google não funciona por meio de Fluxo de Servidor.</span><span class="sxs-lookup"><span data-stu-id="53267-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="53267-109">Para autenticar com o Google, você deve usar um [método de fluxo de cliente](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="53267-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="53267-110">Nesse caso, o Serviço de Aplicativo do Azure gerencia o fluxo de autenticação OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="53267-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="53267-111">Ele exibe a página de logon do provedor selecionado e gera um token de autenticação do Serviço de Aplicativo após o logon bem-sucedido com o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="53267-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="53267-112">A função de logon, quando concluída, retorna um objeto JSON que expõe a ID do usuário e o token de autenticação do Serviço de Aplicativo nos campos userId e authenticationToken, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="53267-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="53267-113">Esse token pode ser armazenado em cache e reutilizado até que expire.</span><span class="sxs-lookup"><span data-stu-id="53267-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="53267-114"><a name="client-auth"></a>Como autenticar com um provedor (fluxo de cliente)</span><span class="sxs-lookup"><span data-stu-id="53267-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="53267-115">Seu aplicativo também pode entrar em contato de forma independente com o provedor de identidade e fornecer o token retornado ao Serviço de Aplicativo para autenticação.</span><span class="sxs-lookup"><span data-stu-id="53267-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="53267-116">Esse fluxo de cliente permite que você forneça uma experiência de logon único aos usuários ou recupere dados adicionais do usuário do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="53267-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="53267-117">Exemplo básico de autenticação social</span><span class="sxs-lookup"><span data-stu-id="53267-117">Social Authentication basic example</span></span>

<span data-ttu-id="53267-118">Este exemplo usa o SDK de cliente do Facebook para a autenticação:</span><span class="sxs-lookup"><span data-stu-id="53267-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="53267-119">Esse exemplo pressupõe que o token fornecido pelo respectivo SDK do provedor é armazenado na variável 'token'.</span><span class="sxs-lookup"><span data-stu-id="53267-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="53267-120">Exemplo de conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="53267-120">Microsoft Account example</span></span>

<span data-ttu-id="53267-121">O exemplo a seguir usa o Live SDK, que oferece suporte a logon único para aplicativos da Windows Store, usando a Conta da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="53267-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="53267-122">Esse exemplo obtém um token do Live Connect, que é fornecido ao seu Serviço de Aplicativo chamando a função de logon.</span><span class="sxs-lookup"><span data-stu-id="53267-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="53267-123"><a name="auth-getinfo"></a>Como obter informações sobre o usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="53267-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="53267-124">As informações de autenticação podem ser obtidas no ponto de extremidade `/.auth/me` usando uma chamada HTTP com qualquer biblioteca do AJAX.</span><span class="sxs-lookup"><span data-stu-id="53267-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="53267-125">Certifique-se de definir o cabeçalho `X-ZUMO-AUTH` ao token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="53267-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="53267-126">O token de autenticação está armazenado em `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="53267-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="53267-127">Por exemplo, para usar a API de busca:</span><span class="sxs-lookup"><span data-stu-id="53267-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="53267-128">O Fetch está disponível como um [pacote npm](https://www.npmjs.com/package/whatwg-fetch) ou para download do navegador do [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="53267-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="53267-129">Você também pode usar jQuery ou outra API AJAX para buscar as informações.</span><span class="sxs-lookup"><span data-stu-id="53267-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="53267-130">Os dados são recebidos como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="53267-130">Data is received as a JSON object.</span></span>
