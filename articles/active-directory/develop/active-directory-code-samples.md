---
title: "Exemplos de código do Active Directory de aaaAzure | Microsoft Docs"
description: "Um índice de exemplos de código do Active Directory do Azure, organizados por cenário."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Exemplos de código do Active Directory do Azure
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Você pode usar o Microsoft Azure Active Directory (AD do Azure) tooadd autenticação e autorização tooyour aplicativos web e APIs da web. Esta seção contém links você toosamples que mostram como isso é feito e trechos de código que você pode usar em seus aplicativos. Na página de exemplo de código hello, você encontrará leitura detalhados-me tópicos que ajudam com requisitos, a instalação e configuração. E código Olá comentado toohelp entender as seções críticas hello.

cenário básico do toounderstand Olá para cada tipo de exemplo, consulte os cenários de autenticação do AD do Azure.

Contribuir tooour amostras no GitHub: [exemplos do Microsoft Azure Active Directory e a documentação](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>TooWeb de navegador da Web aplicativo
Estes exemplos mostram como toowrite um aplicativo web que direciona Olá toosign do navegador do usuário em tooAzure AD.

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| C# / .NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Use usuários de tooauthenticate OpenID Connect (middleware ASP.Net OpenID Connect OWIN) de um locatário do AD do Azure. |
| C# / .NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Um aplicativo de web .NET MVC multilocatário que usa OpenID Connect (middleware ASP.Net OpenID Connect OWIN) o tooauthenticate usuários de vários locatários do AD do Azure. |
| C# / .NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Use usuários de tooauthenticate do WS-Federation (middleware ASP.Net WS-Federation OWIN) de um locatário do AD do Azure. |

## <a name="single-page-application-spa"></a>SPA (Aplicativo de Página Única)
Este exemplo mostra como toowrite um aplicativo de página única protegido com o Azure AD.  

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| JavaScript, C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Use o ADAL para JavaScript e o Azure AD aplicativo de página única toosecure um AngularJS com base em implementado com um ASP.NET web API back-end. |

## <a name="native-application-tooweb-api"></a>TooWeb do aplicativo nativo API
Estes exemplos de código mostram como os aplicativos cliente nativos toobuild que chamam APIs web que são protegidos pelo AD do Azure. Eles usam a [biblioteca de autenticação do Azure AD (ADAL)](active-directory-authentication-libraries.md) e o [OAuth 2.0 no Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| JavaScript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Use o plug-in ADAL de saudação para Apache Cordova toobuild um aplicativo do Apache Cordova que chama uma API da web e usa o Azure AD para autenticação. |
| C# / .NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Um aplicativo .NET WPF que chama uma API da Web protegida usando o Azure AD. |
| C# / .NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Um aplicativo da Windows Store que chama uma API da Web protegida pelo Azure AD. |
| C# / .NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Um aplicativo da Windows Store que chama uma API da Web de multilocatários protegida pelo Azure AD. |
| C# / .NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Um aplicativo cliente nativo que chama uma API da web, que obtém um token tooact em nome de usuário original hello e, em seguida, usa Olá token toocall outra API da web. |
| C# / .NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Um aplicativo da Windows Store para Windows Phone 8.1 que chama uma API da Web protegida pelo Azure AD. |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |Um aplicativo iOS que chama uma API da Web que requer o Azure AD para autenticação. |
| C# / .NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Um aplicativo cliente nativo que inclui lógica tooprocess um token JWT em uma API da web, em vez de usar o middleware OWIN. |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Um Xamarin associação toohello nativo do Azure AD Authentication Library (ADAL) para Olá biblioteca Android. |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Uma associação de Xamarin toohello nativo do Azure AD Authentication Library (ADAL) para iOS. |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Um projeto Xamarin direcionado a cinco plataformas e que chama uma API da Web protegida pelo Azure AD. |
| C# / .NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Um aplicativo nativo que realiza a autenticação não interativa e chama uma API da Web protegida pelo Azure AD. |

## <a name="web-application-tooweb-api"></a>TooWeb de aplicativo da Web API
Estes exemplos de código mostram como usar [OAuth 2.0 no AD do Azure](https://msdn.microsoft.com/library/azure/dn645545.aspx) aplicativos web toobuild que chamam APIs web que são protegidos pelo AD do Azure.

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| C# / .NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Chame uma API da web com permissões de saudação assinado do usuário. |
| C# / .NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Chame uma API da web com as permissões do aplicativo hello. |
| C# / .NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Adicione autorização com [OAuth 2.0 no AD do Azure](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan aplicação web para que ele pode chamar uma API da web. |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Configure um serviço de API REST que é integrado ao Azure AD para proteção da API. Inclui um servidor Node.js com uma API da Web. |
| C# / .NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Um multi-aplicativo da web MVC que usa OpenID Connect (middleware ASP.Net OpenID Connect OWIN) de usuários de tooauthenticate de um locatário do AD do Azure. Usa uma saudação de tooinvoke de código de autorização API do Graph. |

## <a name="server-or-daemon-application-tooweb-api"></a>Servidor ou aplicativo Daemon tooWeb API
Esses exemplos de código mostram como toobuild um daemon ou aplicativo de servidor que recebe recursos de uma API da web usando [da biblioteca de autenticação do AD do Azure (ADAL)](active-directory-authentication-libraries.md) e [OAuth 2.0 no AD do Azure](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| C# / .NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Um aplicativo de console chama uma API da Web. credencial de saudação do cliente é uma senha. |
| C# / .NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Um aplicativo de console que chama uma API da Web. credencial de saudação do cliente é um certificado. |

## <a name="calling-azure-ad-graph-api"></a>Chamando a Graph API do AD do Azure
Essas amostras de código mostram como toobuild os aplicativos que chamam Olá tooread e gravar dados do diretório do Azure AD Graph API.

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Um aplicativo web que usa Olá Graph API tooaccess dados de diretório do AD do Azure. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Um aplicativo web que usa Olá Graph API tooaccess dados de diretório do AD do Azure. |
| C# / .NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Um aplicativo web que usa Olá Graph API tooaccess dados de diretório do AD do Azure. |
| C# / .NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Este aplicativo de console demonstra comuns de leitura e gravação chamadas toohello API do Graph e mostra como o usuário tooexecute atribuição de licença e atualize a foto em miniatura de um usuário e links. |
| C# / .NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Um aplicativo de console que usa consulta diferencial Olá Olá Graph API tooget periódica altera toouser objetos em um locatário do AD do Azure. |
| C# / .NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Um aplicativo MVC usa consultas de API do Graph toogenerate um organograma organizacional simples. |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Um aplicativo PHP que chama Olá Graph API tooregister uma extensão e, em seguida, ler, atualizar e excluir valores no atributo de extensão de saudação. |

## <a name="authorization"></a>Autorização
Eles mostram exemplos de código como toouse AD do Azure para autorização.

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| C# / .NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Executa o RBAC (controle de acesso baseado em função) usando declarações de grupo do Azure Active Directory em um aplicativo que é integrado ao Azure AD. |
| C# / .NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Executa o RBAC (controle de acesso baseado em função) usando funções de aplicativo do Azure Active Directory em um aplicativo que é integrado ao Azure AD. |

## <a name="legacy-walkthroughs"></a>Passo a passo herdado
Essas orientações usam tecnologia ligeiramente mais antiga, mas ainda podem ser interessantes.

| Linguagem/plataforma | Amostra | Descrição |
| --- | --- | --- |
| C# / .NET |[Autorização baseada em função e baseada em ACL em um aplicativo do Microsoft Azure AD](http://go.microsoft.com/fwlink/?LinkId=331694) |Execute RBAC (autorização baseada em função) e autorização baseada em ACL em um aplicativo que é integrado ao Azure AD. |
| C# / .NET |[AAL - serviço de tooREST de aplicativo da Windows Store - autenticação](http://go.microsoft.com/fwlink/?LinkId=330605) |Use [da biblioteca de autenticação do AD do Azure (ADAL)](active-directory-authentication-libraries.md) (antigo AAL) para o aplicativo da Windows Store Beta tooadd usuário autenticação recursos tooa Windows Store. |
| C# / .NET |[ADAL - tooREST do serviço de aplicativo nativo - autenticação com AAD pela caixa de diálogo do navegador](http://go.microsoft.com/fwlink/?LinkId=259814) |Use [da biblioteca de autenticação do AD do Azure (ADAL)](active-directory-authentication-libraries.md) tooadd autenticação recursos tooa WPF de cliente de usuário. |
| C# / .NET |[ADAL - tooREST do serviço de aplicativo nativo - autenticação com ACS via diálogo de navegador](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Use [da biblioteca de autenticação do AD do Azure (ADAL)](active-directory-authentication-libraries.md) e [Access Control Service 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) tooadd autenticação recursos tooa WPF de cliente de usuário. |
| C# / .NET |[ADAL - servidor tooServer autenticação](http://go.microsoft.com/fwlink/?LinkId=259816) |Use [da biblioteca de autenticação do AD do Azure (ADAL)](active-directory-authentication-libraries.md) toosecure chamadas de serviço de um tooan de processo do lado do servidor serviço REST da API Web MVC4. |
| C# / .NET |[Adicionando tooYour logon usando o aplicativo Web Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Configure um .NET aplicativo tooperform web SSO em seu diretório do AD do Azure enterprise. |
| C# / .NET |[Desenvolvendo aplicativos Web multilocatários com o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Usar o AD do Azure tooadd toohello logon único e recursos de acesso de diretório de um toowork de aplicativos .NET em várias organizações. |
| Java |[Aplicativo de exemplo Java para Graph API Azure AD](http://go.microsoft.com/fwlink/?LinkId=263969) |Use dados do diretório tooaccess Olá API do Graph do AD do Azure. |
| PHP |[Aplicativo de exemplo PHP para Graph API do Azure AD](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Use dados do diretório tooaccess Olá API do Graph do AD do Azure. |
| C# / .NET |[Aplicativo de exemplo para Graph API do Azure AD](http://go.microsoft.com/fwlink/?LinkID=262648) |Use dados do diretório tooaccess Olá API do Graph do AD do Azure. |
| C# / .NET |[Aplicativo de exemplo para consulta diferencial gráfica do Azure AD](http://go.microsoft.com/fwlink/?LinkId=275398) |Use consulta diferencial Olá Olá Graph API tooget mudanças periódicas toouser objetos um locatário do AD do Azure. |
| C# / .NET |[Aplicativo de exemplo para integrar aplicativos multilocatários em nuvem para o Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Integre um aplicativo multilocatário no Azure AD. |
| C# / .NET |[Proteger um aplicativo da Windows Store e o serviço Web REST usando o Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Criar um recurso da API da web simples e um aplicativo de cliente da Windows Store usando o Azure AD e Olá [da biblioteca de autenticação do AD do Azure (ADAL)](active-directory-authentication-libraries.md). |
| C# / .NET |[Usando Olá tooQuery de API do Graph do AD do Azure](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Configure uma saudação de toouse de aplicativo do Microsoft .NET dados do Azure AD Graph API tooaccess de um diretório de locatário do AD do Azure. |

## <a name="see-also"></a>Consulte também
##### <a name="other-resources"></a>Outros recursos
[Guia do desenvolvedor do Active Directory do Azure](active-directory-developers-guide.md)

[Conceitos e referência da Graph API do Azure AD](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Biblioteca auxiliar da Graph API do Azure AD](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
