---
title: "bibliotecas de autenticação aaaAzure do Active Directory v 2.0 | Microsoft Docs"
description: "Bibliotecas de cliente compatível e bibliotecas de middleware do servidor e biblioteca relacionada, fonte e links de exemplos, ponto de extremidade do hello Active Directory do Azure v 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Bibliotecas de autenticação do Azure Active Directory v2.0
ponto de extremidade do Hello Azure Active Directory (AD do Azure) v 2.0 dá suporte a protocolos de OAuth 2.0 e OpenID Connect 1.0 de saudação padrão do setor. Você pode usar várias bibliotecas da Microsoft e de outras organizações com o ponto de extremidade do hello v 2.0.

Quando você cria um aplicativo que usa o ponto de extremidade do hello v 2.0, é recomendável que você use bibliotecas que são gravadas por especialistas de domínio do protocolo que seguem uma metodologia Security Development Lifecycle (SDL), como [Olá um seguido pela Microsoft] [Microsoft-SDL]. Se você decidir suporte a código toohand protocolos hello, recomendamos que você siga a metodologia SDL e preste muita atenção toohello considerações de segurança nas especificações de padrões de saudação para cada protocolo.

## <a name="types-of-libraries"></a>Tipos de bibliotecas
O Azure AD v 2.0 funciona com dois tipos de bibliotecas:

* **Bibliotecas de cliente**. Servidores e clientes nativos usam tokens de acesso de tooget de bibliotecas de cliente para chamar um recurso, como o Microsoft Graph.
* **Bibliotecas de middleware de servidor**. Os aplicativos Web usam bibliotecas de middleware de servidor para a entrada do usuário. APIs da Web usam tokens toovalidate de bibliotecas de middleware de servidor que são enviadas por clientes nativos ou por outros servidores.

## <a name="library-support"></a>Suporte à biblioteca
Como você pode escolher qualquer biblioteca compatível com os padrões ao usar o ponto de extremidade do hello v 2.0, é importante tooknow onde toogo para obter suporte. Para problemas e solicitações de recursos no código de biblioteca, contate o proprietário da biblioteca de saudação. Para problemas e solicitações de recursos na implementação do protocolo do lado do serviço hello, contate a Microsoft.

As bibliotecas vêm em duas categorias de suporte:

* **Com suporte da Microsoft**. A Microsoft fornece correções para essas bibliotecas e fez a devida diligência do SDL nessas bibliotecas.
* **Compatível**. A Microsoft testou essas bibliotecas em cenários básicos e confirmado que funcionam com o ponto de extremidade do hello v 2.0. A Microsoft não fornece correções para essas bibliotecas e não as analisou. Problemas e solicitações de recursos devem ser o projeto de código-fonte aberto da biblioteca toohello direcionado.

Para obter uma lista de bibliotecas que funcionam com o ponto de extremidade do hello v 2.0, consulte Olá próximas seções neste artigo.


## <a name="microsoft-supported-client-libraries"></a>Bibliotecas de cliente com suporte da Microsoft

> [!IMPORTANT]
> bibliotecas de visualização do Hello MSAL são adequadas para uso em um ambiente de produção. Fornecemos Olá mesmo suporte de nível de produção para essas bibliotecas, como fazemos o nosso bibliotecas de produção atual (ADAL). Durante a visualização de saudação podemos fazer alterações toohello MSAL API, o formato do cache interno, e outros mecanismos dessas bibliotecas sem aviso prévio, será necessário tootake junto com correções de bugs ou melhorias de recurso. Isso pode afetar seu aplicativo. Por exemplo, um formato de cache de toohello de alteração pode afetar os usuários, como exigir que eles toosign em novamente. Uma alteração de API pode exigir tooupdate seu código. Quando fornecemos Olá versão disponibilidade geral, exigirá que você versão de disponibilidade geral toohello tooupdate dentro de seis meses, como aplicativos escritos usando uma visualização versão da biblioteca pode não funcionar.

| Plataforma | Biblioteca | Baixar | Código-fonte | Amostra | Referência
| --- | --- | --- | --- | --- | --- |
| Cliente .NET, Windows Store, UWP, Xamarin iOS e Android | .NET da MSAL (versão prévia) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Aplicativo de área de trabalho](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (versão prévia) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Aplicativo de Página Única](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS, macOS | MSAL (versão prévia) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Aplicativo iOS](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (versão prévia) | [Olá repositório Central](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Aplicativo Android](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Bibliotecas de middleware de servidor com suporte da Microsoft

| Plataforma | Biblioteca | Baixar | Código-fonte | Amostra | Referência
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | Middleware OWIN OpenID Connect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicativo MVC](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | Middleware OWIN OAuth Bearer para Azure AD |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | Manipulador JWT para .NET 4.5 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | Middleware OpenID Connect para ASP.NET |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[Segurança do ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[Aplicativo MVC](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | Middleware OAuth Bearer para ASP.NET |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[Segurança do ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | Manipulador JWT para .NET Core  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Aplicativo Web](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Bibliotecas de cliente compatíveis
| Plataforma | Nome da biblioteca | Versão testada | Código-fonte | Amostra |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Exemplo de aplicativo nativo](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Exemplo de aplicativo nativo](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Bibliotecas de middleware de servidor compatíveis
| Plataforma | Nome da biblioteca | Versão testada | Código-fonte | Amostra |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribe Java scribejava](https://github.com/scribejava/scribejava) | [Versão 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [Olá PHP League oauth2-cliente](https://github.com/thephpleague/oauth2-client) | [Versão 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python-Flask |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |[Aplicativo Web](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>Conteúdo relacionado
Para obter mais informações sobre o ponto de extremidade do AD do Azure de saudação v 2.0, consulte Olá [visão geral do AD do Azure aplicativo modelo v 2.0][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
