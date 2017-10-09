---
title: "aaaAzure AD v2 Windows Desktop Introdução - uso | Microsoft Docs"
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
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="c130c-103">Use Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="c130c-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="c130c-104">Esta seção mostra como toouse MSAL tooget um token Olá Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="c130c-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="c130c-105">Em `MainWindow.xaml.cs`, adicionar referência de saudação para classe de toohello MSAL biblioteca:</span><span class="sxs-lookup"><span data-stu-id="c130c-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="c130c-106">Substitua o código da classe <code>MainWindow</code> por:</span><span class="sxs-lookup"><span data-stu-id="c130c-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
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
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
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
### <a name="more-information"></a><span data-ttu-id="c130c-107">Mais informações</span><span class="sxs-lookup"><span data-stu-id="c130c-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="c130c-108">Obtendo um token de usuário interativo</span><span class="sxs-lookup"><span data-stu-id="c130c-108">Getting a user token interactive</span></span>
<span data-ttu-id="c130c-109">Olá chamada `AcquireTokenAsync` método resulta em uma janela solicitando Olá toosign de usuário no.</span><span class="sxs-lookup"><span data-stu-id="c130c-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="c130c-110">Aplicativos geralmente exigem toosign um usuário no interativamente Olá primeira vez que precisam tooaccess um recurso protegido, ou quando uma operação silenciosa tooacquire um token de falha (por exemplo, senha do usuário Olá expirado).</span><span class="sxs-lookup"><span data-stu-id="c130c-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="c130c-111">Obtendo um token de usuário no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="c130c-111">Getting a user token silently</span></span>
<span data-ttu-id="c130c-112">`AcquireTokenSilentAsync` manipula as aquisições e a renovação de tokens sem nenhuma interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c130c-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="c130c-113">Depois de `AcquireTokenAsync` é executado para Olá primeira vez, `AcquireTokenSilentAsync` é Olá método normal usado tooobtain tokens usados tooaccess recursos para as chamadas subsequentes - protegidos como chamadas toorequest ou renovar os tokens são feitas silenciosamente.</span><span class="sxs-lookup"><span data-stu-id="c130c-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="c130c-114">Por fim, `AcquireTokenSilentAsync` falhará – por exemplo, o usuário Olá foi desconectado ou alterou sua senha em outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c130c-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="c130c-115">Quando MSAL detecta que Olá problema pode ser resolvido, exigindo uma ação interativa, ele dispara um `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="c130c-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="c130c-116">O aplicativo pode tratar essa exceção de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="c130c-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="c130c-117">Fazer uma chamada contra `AcquireTokenAsync` imediatamente, o que resulta em Avisar usuário Olá toosign-in.</span><span class="sxs-lookup"><span data-stu-id="c130c-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="c130c-118">Esse padrão é geralmente usado em aplicativos online onde não há nenhum conteúdo offline no aplicativo hello disponíveis para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="c130c-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="c130c-119">gerado por esta instalação interativa do exemplo Hello usa esse padrão: você pode vê-lo na saudação de ação primeira vez que você executar o exemplo hello: porque nenhum usuário já utilizada aplicativo hello, `PublicClientApp.Users.FirstOrDefault()` conterá um valor nulo e um `MsalUiRequiredException` exceção será lançada.</span><span class="sxs-lookup"><span data-stu-id="c130c-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="c130c-120">Olá código no exemplo hello e identificadores Olá exceção chamando `AcquireTokenAsync` resultando em Avisar usuário Olá toosign-in.</span><span class="sxs-lookup"><span data-stu-id="c130c-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="c130c-121">Os aplicativos também podem fazer um usuário toohello indicação visual que uma entrada interativa é necessária para que o usuário Olá pode selecionar Olá hora certa toosign em ou aplicativo hello pode repetir `AcquireTokenSilentAsync` mais tarde.</span><span class="sxs-lookup"><span data-stu-id="c130c-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="c130c-122">Isso geralmente é usado quando o usuário Olá pode usar outras funcionalidades de aplicativo hello sem interrupção — por exemplo, há conteúdo off-line disponível no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c130c-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="c130c-123">Nesse caso, o usuário Olá pode decidir quando quiserem toosign no recurso de saudação protegido tooaccess, Olá toorefresh desatualizado informações ou seu aplicativo pode decidir tooretry `AcquireTokenSilentAsync` quando a rede é restaurada depois de ficar indisponível temporariamente.</span><span class="sxs-lookup"><span data-stu-id="c130c-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="c130c-124">Chamar API do Microsoft Graph hello usando Olá token obtido apenas</span><span class="sxs-lookup"><span data-stu-id="c130c-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="c130c-125">Adicionar novo método hello abaixo tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="c130c-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="c130c-126">método Hello é usado toomake um `GET` solicitação em relação a API do Graph usando um cabeçalho de autorização:</span><span class="sxs-lookup"><span data-stu-id="c130c-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="c130c-127">Mais informações sobre como fazer uma chamada REST em uma API protegida</span><span class="sxs-lookup"><span data-stu-id="c130c-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="c130c-128">Este aplicativo de exemplo hello `GetHttpContentWithToken` método é usado toomake um HTTP `GET` solicitação em um recurso protegido que requer um chamador de conteúdo toohello Olá token e retornar.</span><span class="sxs-lookup"><span data-stu-id="c130c-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="c130c-129">Este método adiciona token Olá adquirido em Olá *cabeçalho de autorização HTTP*.</span><span class="sxs-lookup"><span data-stu-id="c130c-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="c130c-130">Para este exemplo, o recurso de saudação é Olá Microsoft Graph API *me* ponto de extremidade – que exibe informações de perfil do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="c130c-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="c130c-131">Adicionar um toosign método usuário Olá</span><span class="sxs-lookup"><span data-stu-id="c130c-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="c130c-132">Adicionar Olá após o método tooyour `MainWindow.xaml.cs` toosign usuário hello:</span><span class="sxs-lookup"><span data-stu-id="c130c-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

```csharp
/// <summary>
/// Sign out hello current user
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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="c130c-133">Mais informações sobre a Saída</span><span class="sxs-lookup"><span data-stu-id="c130c-133">More info on Sign-Out</span></span>

<span data-ttu-id="c130c-134">`SignOutButton_Click`Remove Olá usuário do cache de usuário MSAL – isso efetivamente informará o usuário atual do MSAL tooforget Olá para que uma solicitação futuras tooacquire um token terá êxito apenas se ele for feito toobe interativo.</span><span class="sxs-lookup"><span data-stu-id="c130c-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="c130c-135">Embora o aplicativo hello neste exemplo dá suporte a um único usuário, MSAL oferece suporte a cenários onde várias contas podem ser assinados-em Olá simultaneamente – um exemplo é um aplicativo de email onde um usuário tenha várias contas.</span><span class="sxs-lookup"><span data-stu-id="c130c-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="c130c-136">Exibir informações básicas de token</span><span class="sxs-lookup"><span data-stu-id="c130c-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="c130c-137">Adicionar Olá após o método tootooyour `MainWindow.xaml.cs` toodisplay as informações básicas sobre o token hello:</span><span class="sxs-lookup"><span data-stu-id="c130c-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in hello token
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
### <a name="more-information"></a><span data-ttu-id="c130c-138">Mais informações</span><span class="sxs-lookup"><span data-stu-id="c130c-138">More Information</span></span>

<span data-ttu-id="c130c-139">Tokens adquirido por meio de *OpenID Connect* também contêm um pequeno subconjunto de usuário de toohello pertinentes de informações.</span><span class="sxs-lookup"><span data-stu-id="c130c-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="c130c-140">`DisplayBasicTokenInfo`Exibe informações básicas sobre contida no token Olá: por exemplo, usuário Olá exibir nome e ID, bem como Olá expiração do token data e hello cadeia de caracteres que representa o token de acesso de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="c130c-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="c130c-141">Essa informação é exibida para você toosee.</span><span class="sxs-lookup"><span data-stu-id="c130c-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="c130c-142">Você pode pressionar Olá *chamar a API do Microsoft Graph* botão várias vezes e veja que Olá mesmo token foi usado para solicitações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="c130c-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="c130c-143">Você também pode ver a data de validade hello está sendo estendida quando MSAL decide é tempo toorenew Olá token.</span><span class="sxs-lookup"><span data-stu-id="c130c-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

