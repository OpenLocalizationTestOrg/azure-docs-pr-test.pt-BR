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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Use Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API

Esta seção mostra como toouse MSAL tooget um token Olá Microsoft Graph API.

1.  Em `MainWindow.xaml.cs`, adicionar referência de saudação para classe de toohello MSAL biblioteca:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Substitua o código da classe <code>MainWindow</code> por:
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
### <a name="more-information"></a>Mais informações
#### <a name="getting-a-user-token-interactive"></a>Obtendo um token de usuário interativo
Olá chamada `AcquireTokenAsync` método resulta em uma janela solicitando Olá toosign de usuário no. Aplicativos geralmente exigem toosign um usuário no interativamente Olá primeira vez que precisam tooaccess um recurso protegido, ou quando uma operação silenciosa tooacquire um token de falha (por exemplo, senha do usuário Olá expirado).

#### <a name="getting-a-user-token-silently"></a>Obtendo um token de usuário no modo silencioso
`AcquireTokenSilentAsync` manipula as aquisições e a renovação de tokens sem nenhuma interação do usuário. Depois de `AcquireTokenAsync` é executado para Olá primeira vez, `AcquireTokenSilentAsync` é Olá método normal usado tooobtain tokens usados tooaccess recursos para as chamadas subsequentes - protegidos como chamadas toorequest ou renovar os tokens são feitas silenciosamente.
Por fim, `AcquireTokenSilentAsync` falhará – por exemplo, o usuário Olá foi desconectado ou alterou sua senha em outro dispositivo. Quando MSAL detecta que Olá problema pode ser resolvido, exigindo uma ação interativa, ele dispara um `MsalUiRequiredException`. O aplicativo pode tratar essa exceção de duas maneiras:

1.  Fazer uma chamada contra `AcquireTokenAsync` imediatamente, o que resulta em Avisar usuário Olá toosign-in. Esse padrão é geralmente usado em aplicativos online onde não há nenhum conteúdo offline no aplicativo hello disponíveis para usuário hello. gerado por esta instalação interativa do exemplo Hello usa esse padrão: você pode vê-lo na saudação de ação primeira vez que você executar o exemplo hello: porque nenhum usuário já utilizada aplicativo hello, `PublicClientApp.Users.FirstOrDefault()` conterá um valor nulo e um `MsalUiRequiredException` exceção será lançada. Olá código no exemplo hello e identificadores Olá exceção chamando `AcquireTokenAsync` resultando em Avisar usuário Olá toosign-in.

2.  Os aplicativos também podem fazer um usuário toohello indicação visual que uma entrada interativa é necessária para que o usuário Olá pode selecionar Olá hora certa toosign em ou aplicativo hello pode repetir `AcquireTokenSilentAsync` mais tarde. Isso geralmente é usado quando o usuário Olá pode usar outras funcionalidades de aplicativo hello sem interrupção — por exemplo, há conteúdo off-line disponível no aplicativo hello. Nesse caso, o usuário Olá pode decidir quando quiserem toosign no recurso de saudação protegido tooaccess, Olá toorefresh desatualizado informações ou seu aplicativo pode decidir tooretry `AcquireTokenSilentAsync` quando a rede é restaurada depois de ficar indisponível temporariamente.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar API do Microsoft Graph hello usando Olá token obtido apenas

1. Adicionar novo método hello abaixo tooyour `MainWindow.xaml.cs`. método Hello é usado toomake um `GET` solicitação em relação a API do Graph usando um cabeçalho de autorização:

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Mais informações sobre como fazer uma chamada REST em uma API protegida

Este aplicativo de exemplo hello `GetHttpContentWithToken` método é usado toomake um HTTP `GET` solicitação em um recurso protegido que requer um chamador de conteúdo toohello Olá token e retornar. Este método adiciona token Olá adquirido em Olá *cabeçalho de autorização HTTP*. Para este exemplo, o recurso de saudação é Olá Microsoft Graph API *me* ponto de extremidade – que exibe informações de perfil do usuário hello.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Adicionar um toosign método usuário Olá

1. Adicionar Olá após o método tooyour `MainWindow.xaml.cs` toosign usuário hello:

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
### <a name="more-info-on-sign-out"></a>Mais informações sobre a Saída

`SignOutButton_Click`Remove Olá usuário do cache de usuário MSAL – isso efetivamente informará o usuário atual do MSAL tooforget Olá para que uma solicitação futuras tooacquire um token terá êxito apenas se ele for feito toobe interativo.
Embora o aplicativo hello neste exemplo dá suporte a um único usuário, MSAL oferece suporte a cenários onde várias contas podem ser assinados-em Olá simultaneamente – um exemplo é um aplicativo de email onde um usuário tenha várias contas.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Exibir informações básicas de token

1. Adicionar Olá após o método tootooyour `MainWindow.xaml.cs` toodisplay as informações básicas sobre o token hello:

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
### <a name="more-information"></a>Mais informações

Tokens adquirido por meio de *OpenID Connect* também contêm um pequeno subconjunto de usuário de toohello pertinentes de informações. `DisplayBasicTokenInfo`Exibe informações básicas sobre contida no token Olá: por exemplo, usuário Olá exibir nome e ID, bem como Olá expiração do token data e hello cadeia de caracteres que representa o token de acesso de saudação em si. Essa informação é exibida para você toosee. Você pode pressionar Olá *chamar a API do Microsoft Graph* botão várias vezes e veja que Olá mesmo token foi usado para solicitações subsequentes. Você também pode ver a data de validade hello está sendo estendida quando MSAL decide é tempo toorenew Olá token.
<!--end-collapse-->

