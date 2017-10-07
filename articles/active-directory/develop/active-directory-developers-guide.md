---
title: aaaAzure do Active Directory para desenvolvedores | Microsoft Docs
description: "Este artigo fornece uma visão geral sobre como conectar-se às contas corporativa e de estudante da Microsoft usando o Azure Active Directory."
services: active-directory
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4dbbea6c1e0b8a70c0c36ddd1caec5658130a003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-for-developers"></a>Azure Active Directory para desenvolvedores
Active Directory do Azure é um serviço de identidade de nuvem que permite aos desenvolvedores toosecurely entrar qualquer usuário com uma conta corporativa ou escolar feito pela Microsoft.  documentação de saudação aqui mostra como tooadd AD do Azure dão suporte ao aplicativo de tooyour usando protocolos de autenticação padrão do setor, OAuth & OpenID Connect.

| | |
| --- | --- |
|[Noções básicas de autenticação](active-directory-authentication-scenarios.md) | Tooauthentication uma introdução ao AD do Azure |
|[Tipos de aplicativos](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Uma visão geral de cenários de autenticação de saudação suportados pelo AD do Azure |                                
                                                                              
## <a name="get-started"></a>Introdução
Essas configurações interativa orientará usando nosso toosign de bibliotecas de autenticação de usuários do Active Directory do Azure.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Aplicativos móveis e de desktop](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />Aplicativos móveis e de desktop</center> | [Visão geral](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET](active-directory-devquickstarts-dotnet.md)<br /><br />[Windows](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md)<br /><br />[OAuth 2.0](active-directory-protocols-oauth-code.md) |
| <center>![Aplicativos Web](./media/active-directory-developers-guide/Web_app.png)<br />Aplicativos Web</center> | [Visão geral](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [NodeJS](active-directory-devquickstarts-openidconnect-nodejs.md)<br /><br />[OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) |  |
| <center>![Aplicativos de Página Única](./media/active-directory-developers-guide/SPA.png)<br />Aplicativos de Página Única</center> | [Visão geral](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![APIs da Web](./media/active-directory-developers-guide/Web_API.png)<br />APIs da Web</center> | [Visão geral](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[NodeJS](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![De serviços](./media/active-directory-developers-guide/Service_App.png)<br />De serviços</center> | [Visão geral](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#server-or-daemon-application-to-web-api)<br /><br />[Credenciais do cliente do OAuth 2.0](active-directory-protocols-oauth-service-to-service.md) |  |

## <a name="guides"></a>Guias
Esses artigos informam como as tarefas comuns de tooperform com o Active Directory do Azure.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[Registro do Aplicativo](active-directory-integrating-applications.md)           | Como tooregister um aplicativo no AD do Azure |
|[Aplicativos multilocatário](active-directory-devhowto-multi-tenant-overview.md)    | Como conta de trabalho toosign na Microsoft |
|[OAuth e OpenID Connect](active-directory-protocols-openid-connect-code.md)| Como os usuários toosign e chamar APIs da web usando os protocolos de autenticação moderna |
|[Mais guias...](active-directory-developers-guide-index.md#guides)        |     |

## <a name="reference"></a>Referência
Esses artigos fornecem informações detalhadas sobre as APIs, as mensagens de protocolo e os termos usados no Azure Active Directory.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [Bibliotecas de autenticação (ADAL)](active-directory-authentication-libraries.md)   | Uma visão geral das bibliotecas de saudação & SDKs fornecidos pelo AD do Azure |
| [Exemplos de código](active-directory-code-samples.md)                                  | Uma lista de todos os exemplos de código do Azure AD |
| [Glossário](active-directory-dev-glossary.md)                                      | Terminologia e definições de palavras usadas em toda esta documentação |
| [Mais materiais de referência...](active-directory-developers-guide-index.md#reference)|     |

## <a name="help--support"></a>Ajuda + suporte
Esses são Olá melhores lugares tooget ajuda com o desenvolvimento no Active Directory do Azure.

|  |  
|---|
|[Marcas `azure-active-directory` e `adal` do Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)      |
|[Feedback no Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)|
| [Experimente o Microsoft Dev Chat (gratuito para um período limitado)](http://aka.ms/devchat) |

<br />

> [!NOTE]
> Se você precisar toosign-in particulares contas da Microsoft, talvez você queira tooconsider usando Olá [o ponto de extremidade do AD do Azure v 2.0](active-directory-appmodel-v2-overview.md).  o ponto de extremidade do AD do Azure de saudação v 2.0 é Unificação de saudação de contas pessoais da Microsoft e contas de trabalho da Microsoft (a partir do AD do Azure) em um sistema de autenticação único.
