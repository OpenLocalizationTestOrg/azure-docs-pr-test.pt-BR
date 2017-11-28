---
title: "Introdução à Área de Trabalho do Windows no Azure AD v2 – Uso | Microsoft Docs"
description: "Como os aplicativos .NET da Área de Trabalho do Windows (XAML) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 826ba0a00b26993d4f37f0a8ce587d7bb77e7eb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="1408c-103">Usar a MSAL (Biblioteca de Autenticação da Microsoft) para obter um token para a API do Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1408c-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="1408c-104">Esta seção mostra como usar a MSAL para obter um token da API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1408c-104">This section shows how to use MSAL to get a token the Microsoft Graph API.</span></span>

1.  <span data-ttu-id="1408c-105">Em `MainWindow.xaml.cs`, adicione a referência para a biblioteca MSAL à classe:</span><span class="sxs-lookup"><span data-stu-id="1408c-105">In `MainWindow.xaml.cs`, add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="1408c-106">Substitua o código da classe <code>MainWindow</code> por:</span><span class="sxs-lookup"><span data-stu-id="1408c-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set the API Endpoint to Graph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set the scope for API call to user.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - to acquire a token requiring user to sign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need to call AcquireTokenAsync to acquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="1408c-107">Mais informações</span><span class="sxs-lookup"><span data-stu-id="1408c-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="1408c-108">Obtendo um token de usuário interativo</span><span class="sxs-lookup"><span data-stu-id="1408c-108">Getting a user token interactive</span></span>
<span data-ttu-id="1408c-109">A chamada ao método `AcquireTokenAsync` resulta em uma janela que solicita a conexão do usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-109">Calling the `AcquireTokenAsync` method results in a window prompting the user to sign in.</span></span> <span data-ttu-id="1408c-110">Em geral, os aplicativos exigem que um usuário se conecte de forma interativa na primeira vez que precisam acessar um recurso protegido ou quando uma operação silenciosa para a aquisição de um token falha (por exemplo, a senha do usuário expirou).</span><span class="sxs-lookup"><span data-stu-id="1408c-110">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="1408c-111">Obtendo um token de usuário no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="1408c-111">Getting a user token silently</span></span>
<span data-ttu-id="1408c-112">`AcquireTokenSilentAsync` manipula as aquisições e a renovação de tokens sem nenhuma interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="1408c-113">Depois que `AcquireTokenAsync` é executado pela primeira vez, `AcquireTokenSilentAsync` é o método comum usado para obter tokens para acessar recursos protegidos nas próximas chamadas – já que as chamadas para solicitar ou renovar tokens são feitas no modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="1408c-113">After `AcquireTokenAsync` is executed for the first time, `AcquireTokenSilentAsync` is the usual method used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="1408c-114">Em certas ocasiões, `AcquireTokenSilentAsync` falhará – por exemplo, o usuário saiu do serviço ou alterou sua senha em outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1408c-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="1408c-115">Quando a MSAL detectar que o problema pode ser resolvido com a solicitação de uma ação interativa, ela disparará uma `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="1408c-115">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="1408c-116">O aplicativo pode tratar essa exceção de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="1408c-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="1408c-117">Fazer uma chamada a `AcquireTokenAsync` imediatamente, o que resultará na solicitação de conexão do usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting the user to sign-in.</span></span> <span data-ttu-id="1408c-118">Esse padrão geralmente é usado em aplicativos online em que não há nenhum conteúdo offline no aplicativo disponível para o usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-118">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="1408c-119">A amostra gerada por esta instalação guiada usa esse padrão: você pode vê-lo em ação na primeira vez que executar a amostra: como nenhum usuário nunca usou o aplicativo, `PublicClientApp.Users.FirstOrDefault()` conterá um valor nulo e uma exceção `MsalUiRequiredException` será gerada.</span><span class="sxs-lookup"><span data-stu-id="1408c-119">The sample generated by this guided setup uses this pattern: you can see it in action the first time you execute the sample: because no user ever used the application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="1408c-120">Em seguida, o código na amostra trata a exceção chamando `AcquireTokenAsync`, o que resulta na solicitação de conexão do usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-120">The code in the sample then handles the exception by calling `AcquireTokenAsync` resulting in prompting the user to sign-in.</span></span>

2.  <span data-ttu-id="1408c-121">Os aplicativos também podem fazer uma indicação visual para o usuário de que uma conexão interativa é necessária e, portanto, o usuário pode escolher o momento certo para se conectar ou o aplicativo pode tentar `AcquireTokenSilentAsync` novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1408c-121">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="1408c-122">Normalmente, isso é usado quando o usuário consegue usar outras funcionalidades do aplicativo sem ser interrompido – por exemplo, há conteúdo offline disponível no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1408c-122">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="1408c-123">Nesse caso, o usuário pode decidir quando deseja se conectar para acessar o recurso protegido ou atualizar as informações desatualizadas ou o aplicativo pode decidir tentar `AcquireTokenSilentAsync` novamente quando a rede é restaurada depois de ficar temporariamente indisponível.</span><span class="sxs-lookup"><span data-stu-id="1408c-123">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="1408c-124">Chamar a API do Microsoft Graph usando o token obtido recentemente</span><span class="sxs-lookup"><span data-stu-id="1408c-124">Call the Microsoft Graph API using the token you just obtained</span></span>

1. <span data-ttu-id="1408c-125">Adicione o novo método abaixo ao `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="1408c-125">Add the new method below to your `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="1408c-126">O método é usado para fazer uma solicitação `GET` na API do Graph usando um cabeçalho de autorização:</span><span class="sxs-lookup"><span data-stu-id="1408c-126">The method is used to make a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request to a URL using an HTTP Authorization header
/// </summary>
/// <param name="url">The URL</param>
/// <param name="token">The token</param>
/// <returns>String containing the results of the GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add the token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="1408c-127">Mais informações sobre como fazer uma chamada REST em uma API protegida</span><span class="sxs-lookup"><span data-stu-id="1408c-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="1408c-128">Neste aplicativo de exemplo, o método `GetHttpContentWithToken` é usado para fazer uma solicitação HTTP `GET` em um recurso protegido que exige um token e, em seguida, retornar o conteúdo para o chamador.</span><span class="sxs-lookup"><span data-stu-id="1408c-128">In this sample application, the `GetHttpContentWithToken` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="1408c-129">Esse método adiciona o token adquirido no *cabeçalho de Autorização HTTP*.</span><span class="sxs-lookup"><span data-stu-id="1408c-129">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="1408c-130">Para esta amostra, o recurso é o ponto de extremidade *me* da API do Microsoft Graph – que exibe as informações de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-130">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="1408c-131">Adicionar um método para desconectar o usuário</span><span class="sxs-lookup"><span data-stu-id="1408c-131">Add a method to sign out the user</span></span>

1. <span data-ttu-id="1408c-132">Adicione o seguinte método ao `MainWindow.xaml.cs` para desconectar o usuário:</span><span class="sxs-lookup"><span data-stu-id="1408c-132">Add the following method to your `MainWindow.xaml.cs` to sign out the user:</span></span>

```csharp
/// <summary>
/// Sign out the current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="1408c-133">Mais informações sobre a Saída</span><span class="sxs-lookup"><span data-stu-id="1408c-133">More info on Sign-Out</span></span>

<span data-ttu-id="1408c-134">`SignOutButton_Click` remove o usuário do cache de usuário da MSAL – efetivamente, isso informará a MSAL para esquecer o usuário atual; portanto, uma solicitação futura de aquisição de um token terá êxito apenas se for feita para ser interativa.</span><span class="sxs-lookup"><span data-stu-id="1408c-134">`SignOutButton_Click` removes the user from MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>
<span data-ttu-id="1408c-135">Embora o aplicativo nesta amostra dê suporte a um único usuário, a MSAL dá suporte a cenários em que várias contas podem estar conectadas ao mesmo tempo – um exemplo é um aplicativo de email no qual um usuário tem várias contas.</span><span class="sxs-lookup"><span data-stu-id="1408c-135">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="1408c-136">Exibir informações básicas de token</span><span class="sxs-lookup"><span data-stu-id="1408c-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="1408c-137">Adicione o seguinte método ao `MainWindow.xaml.cs` para exibir informações básicas sobre o token:</span><span class="sxs-lookup"><span data-stu-id="1408c-137">Add the following method to to your `MainWindow.xaml.cs` to display basic information about the token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in the token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="1408c-138">Mais informações</span><span class="sxs-lookup"><span data-stu-id="1408c-138">More Information</span></span>

<span data-ttu-id="1408c-139">Os tokens adquirido por meio do *OpenID Connect* também contêm um pequeno subconjunto de informações pertinentes ao usuário.</span><span class="sxs-lookup"><span data-stu-id="1408c-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent to the user.</span></span> <span data-ttu-id="1408c-140">`DisplayBasicTokenInfo` exibe informações básicas contidas no token: por exemplo, o nome de exibição do usuário e a ID, bem como a data de expiração do token e a cadeia de caracteres que representa o token de acesso em si.</span><span class="sxs-lookup"><span data-stu-id="1408c-140">`DisplayBasicTokenInfo` displays basic information contained in the token: for example, the user's display name and ID, as well as the token expiration date and the string representing the access token itself.</span></span> <span data-ttu-id="1408c-141">Essas informações são exibidas para sua visualização.</span><span class="sxs-lookup"><span data-stu-id="1408c-141">This information is displayed for you to see.</span></span> <span data-ttu-id="1408c-142">Pressione o botão *Chamar API do Microsoft Graph* várias vezes e veja que o mesmo token foi reutilizado em solicitações posteriores.</span><span class="sxs-lookup"><span data-stu-id="1408c-142">You can hit the *Call Microsoft Graph API* button multiple times and see that the same token was reused for subsequent requests.</span></span> <span data-ttu-id="1408c-143">Veja também a data de expiração que está sendo estendida quando a MSAL decide a hora de renovar o token.</span><span class="sxs-lookup"><span data-stu-id="1408c-143">You can also see the expiration date being extended when MSAL decides it is time to renew the token.</span></span>
<!--end-collapse-->

