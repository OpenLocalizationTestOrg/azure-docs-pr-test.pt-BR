---
title: "aaaAzure bibliotecas de autenticação do Active Directory | Microsoft Docs"
description: "saudação do Azure AD Authentication Library (ADAL) os desenvolvedores de aplicativos de cliente permite tooeasily autenticar usuários toocloud ou Active Directory (AD) local e, em seguida, obter tokens de acesso para proteger chamadas de API."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Bibliotecas de Autenticação do Active Directory do Azure
Hello Azure autenticação biblioteca ADAL (Active Directory) permite que cliente aplicativo desenvolvedores tooeasily autenticar usuários toocloud ou Active Directory (AD) local e obter tokens de acesso para proteger chamadas de API. A ADAL facilita a autenticação para os desenvolvedores por meio de recursos, como:
 - suporte para chamadas de método assíncronas
 - um cache de token configurável que armazena tokens de acesso e tokens de atualização
 - atualização de token automática quando um token de acesso expira e um token de atualização está disponível
 - e mais
 
Controlando a maioria da complexidade hello, ADAL ajuda os desenvolvedores a se concentrarem na lógica de negócios e proteja facilmente os recursos, sem ser um especialista em segurança.

A ADAL está disponível em uma variedade de plataformas.

### <a name="client-libraries"></a>Bibliotecas de cliente

| Plataforma | Biblioteca | Baixar | Código-fonte | Amostra | Referência
| --- | --- | --- | --- | --- | --- |
| Cliente .NET, Windows Store, UWP, Xamarin iOS e Android |MSAL para .NET (versão prévia) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Aplicativo da área de trabalho](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Referência](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL para JavaScript (versão prévia) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Aplicativo de Página Única](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Referência](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL para iOS (versão prévia) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Aplicativo iOS](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Referência](https://azuread.github.io/docs/objc/) |
| Android |MSAL para Android (versão prévia) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Aplicativo Android](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Referência](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| Cliente .NET, Windows Store, UWP, Xamarin iOS e Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Aplicativo da área de trabalho](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Referência](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| Cliente .NET, Windows Store, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Aplicativo da área de trabalho](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[Aplicativo de Página Única](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[Aplicativo iOS](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Referência](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Olá repositório Central](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Aplicativo Android](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Aplicativo Web Java](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Bibliotecas do servidor 

| Plataforma | Biblioteca | Baixar | Código-fonte | Amostra | Referência
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN para AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicativo MVC](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN para OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicativo Web](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [API da Web](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN para WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicativo Web MVC](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Extensões do protocolo de identidade para .NET 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |Manipulador JWT para .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Cenários

Aqui estão os três cenários comuns nos quais a ADAL pode ser usada para autenticar um cliente que acesse um recurso remoto:  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Autenticação de usuários de um aplicativo cliente nativo em execução em um dispositivo 

Nesse cenário, um desenvolvedor tem um aplicativo cliente WPF, que precisa tooaccess um recurso remoto protegido pelo AD do Azure, como uma API da web. Ele tem uma assinatura do Azure, sabe como tooinvoke Olá API da web downstream e conhece hello Azure locatário do AD que Olá API da web usa. Como resultado, ele pode usar a autenticação de ADAL toofacilitate com AD do Azure, delegando completamente Olá tooADAL de experiência de autenticação ou tratando explicitamente as credenciais do usuário. ADAL torna fácil tooauthenticate usuário de saudação, obter um token de acesso e token de atualização do AD do Azure e, em seguida, usar Olá acesso toomake token solicitações toohello web API.

Para obter um exemplo de código que demonstra esse cenário usando a autenticação tooAzure AD, consulte [tooWeb de aplicativo cliente WPF nativo API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Autenticar um aplicativo cliente confidencial em execução em um servidor Web

Nesse cenário, um desenvolvedor tem um aplicativo em execução em um servidor que precisa tooaccess um recurso remoto protegido pelo AD do Azure, como uma API da web. Ele tem uma assinatura do Azure, sabe como tooinvoke Olá serviço downstream e conhece Olá AD do Azure locatário Olá API da web usa. Como resultado, ele pode usar autenticação de ADAL toofacilitate com o AD do Azure tratando explicitamente as credenciais do aplicativo hello. ADAL torna fácil tooretrieve um token do AD do Azure usando a credencial do cliente do aplicativo hello e, em seguida, usar esse token toomake solicitações toohello API da web. O ADAL também identificadores de gerenciar o tempo de vida de saudação do hello token de acesso por ele em cache e renovando ele conforme necessário. Para obter um exemplo de código que demonstre este cenário, consulte [tooWeb de aplicativo de console Daemon API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Autenticar um aplicativo cliente confidencial em execução em um servidor, em nome de um usuário 

Nesse cenário, um desenvolvedor tem um aplicativo em execução em um servidor que precisa tooaccess um recurso remoto protegido pelo AD do Azure, como uma API da web. solicitação de saudação também precisa toobe feita em nome de um usuário do AD do Azure. Ele tem uma assinatura do Azure, sabe como tooinvoke Olá API da web downstream e conhece Olá serviço de saudação de locatário do AD do Azure usa. Depois que o usuário Olá é autenticado toohello aplicativo de web, aplicativo hello pode obter um código de autorização para o usuário de saudação do AD do Azure. aplicativo da web Hello, em seguida, pode usar o ADAL tooobtain um token de acesso e token de atualização em nome do usuário usando produtos de credenciais de cliente e código de autorização Olá associados ao aplicativo de saudação do AD do Azure. Depois que o aplicativo da web hello estiver em posse do token de acesso de Olá, pode chamar Olá web API até Olá token expirar. Quando Olá token expirar, aplicativo da web hello pode usar o ADAL tooget um novo token de acesso usando o token de atualização de saudação anteriormente foi recebida. Para obter um exemplo de código que demonstre este cenário, consulte [Native client tooWeb API tooWeb API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Consulte também

- [Olá guia do desenvolvedor do Active Directory do Azure](active-directory-developers-guide.md)
- [Cenários de autenticação do Active Directory do Azure](active-directory-authentication-scenarios.md)
- [Exemplos de código do Active Directory do Azure](active-directory-code-samples.md)
