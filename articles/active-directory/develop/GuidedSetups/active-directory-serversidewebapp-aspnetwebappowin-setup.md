---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - instalação | Microsoft Docs"
description: "Implementando a opção Entrar com uma Conta da Microsoft em uma solução ASP.NET com um aplicativo tradicional baseado em navegador da Web usando o padrão OpenID Connect"
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
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="2c3f3-103">Configurar o seu projeto</span><span class="sxs-lookup"><span data-stu-id="2c3f3-103">Set up your project</span></span>

<span data-ttu-id="2c3f3-104">Esta seção mostra Olá etapas tooinstall e configurar o pipeline de autenticação Olá por meio do middleware OWIN em um projeto ASP.NET que usa o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="2c3f3-105">Preferir toodownload este projeto do Visual Studio em vez disso?</span><span class="sxs-lookup"><span data-stu-id="2c3f3-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="2c3f3-106">[Baixar um projeto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="2c3f3-107">Criar seu projeto do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2c3f3-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="2c3f3-108">No Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="2c3f3-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="2c3f3-109">Em *Visual C#\Web*, selecione `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="2c3f3-110">Nomeie o aplicativo e clique em *OK*</span><span class="sxs-lookup"><span data-stu-id="2c3f3-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="2c3f3-111">Selecione `Empty` e Olá selecione caixa de seleção tooadd `MVC` referências</span><span class="sxs-lookup"><span data-stu-id="2c3f3-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="2c3f3-112">Adicionar componentes de autenticação</span><span class="sxs-lookup"><span data-stu-id="2c3f3-112">Add authentication components</span></span>

1. <span data-ttu-id="2c3f3-113">No Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="2c3f3-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="2c3f3-114">Adicionar *pacotes do NuGet middleware OWIN* digitando o seguinte de saudação na janela do Console do Gerenciador de pacotes de saudação:</span><span class="sxs-lookup"><span data-stu-id="2c3f3-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="2c3f3-115">Sobre estas bibliotecas</span><span class="sxs-lookup"><span data-stu-id="2c3f3-115">About these libraries</span></span>

><span data-ttu-id="2c3f3-116">bibliotecas de saudação acima permitem logon único (SSO) usando o OpenID Connect através da autenticação baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="2c3f3-117">Após a autenticação é concluída e token Olá representando Olá usuário é enviado tooyour aplicativo, o middleware OWIN cria um cookie de sessão.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="2c3f3-118">Olá navegador, em seguida, usa esse cookie em solicitações subsequentes para que usuário Olá não seja necessário tooretype sua senha, e nenhuma verificação adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="2c3f3-119">Configurar o pipeline de autenticação Olá</span><span class="sxs-lookup"><span data-stu-id="2c3f3-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="2c3f3-120">Olá etapas a seguir são usada toocreate uma autenticação OpenID Connect OWIN middleware classe inicialização tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="2c3f3-121">Essa classe será executada automaticamente quando o processo do IIS for iniciado.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="2c3f3-122">Se seu projeto não tem um `Startup.cs` arquivo na pasta raiz de saudação:</span><span class="sxs-lookup"><span data-stu-id="2c3f3-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="2c3f3-123">Clique com o botão direito na pasta raiz do projeto Olá: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="2c3f3-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="2c3f3-124">Nomeie-o `Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="2c3f3-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="2c3f3-125">Certifique-se de classe Olá selecionada é uma classe de inicialização OWIN e não uma padrão classe c#.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="2c3f3-126">Confirmar isso verificando se você vir `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` acima Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="2c3f3-127">Adicionar *OWIN* e *Microsoft. IdentityModel* referencia muito`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="2c3f3-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2c3f3-128">Substitua a classe de inicialização com o código de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2c3f3-128">Replace Startup class with hello code below:</span></span>
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a><span data-ttu-id="2c3f3-129">Mais informações</span><span class="sxs-lookup"><span data-stu-id="2c3f3-129">More Information</span></span>

> <span data-ttu-id="2c3f3-130">Olá parâmetros que você fornece em *OpenIDConnectAuthenticationOptions* servem como coordenadas de saudação toocommunicate de aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="2c3f3-131">Como Olá OpenID Connect middleware usa cookies no plano de fundo hello, você também precisa tooset a autenticação de cookie como código Olá acima mostra.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="2c3f3-132">Olá *ValidateIssuer* valor informa OpenIdConnect toonot restringir acesso tooone determinada organização.</span><span class="sxs-lookup"><span data-stu-id="2c3f3-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

