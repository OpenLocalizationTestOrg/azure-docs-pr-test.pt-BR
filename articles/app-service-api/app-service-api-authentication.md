---
title: "aaaAuthentication e autorização para aplicativos de API no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba mais sobre os serviços de autenticação e autorização de saudação que fornece o serviço de aplicativo do Azure para aplicativos de API."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Autenticação e autorização para aplicativos de API no Serviço de Aplicativo do Azure
## <a name="overview"></a>Visão geral
> [!NOTE]
> Este tópico será migrado tooa consolidado [autenticação do serviço de aplicativo / autorização](../app-service/app-service-authentication-overview.md) tópico, que abrange a Web, móveis e aplicativos de API.
> 
> 

O Serviço de Aplicativo do Azure oferece serviços de autenticação e autorização internos que implementam o [OAuth 2.0](#oauth) e o [OpenID Connect](#oauth). Este artigo descreve os serviços de saudação e opções que estão disponíveis para aplicativos de API no serviço de aplicativo do Azure.

Olá diagrama a seguir ilustra algumas características principais de autenticação do serviço de aplicativo:

* Ele processa previamente as solicitações de API de entrada, o que significa que ele funciona com qualquer linguagem ou estrutura com suporte do Serviço de Aplicativo.
* Ele fornece várias opções para quanto a autenticação de trabalho você deseja toodo em seu próprio código.
* Ele funciona para a autenticação de usuário final e de conta de serviço. 
* Ele dá suporte a cinco provedores de autenticação: Active Directory do Azure, Facebook, Google, Twitter e Conta da Microsoft.
* Ele funciona hello mesmo para aplicativos de API, aplicativos Web e aplicativos móveis.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Independente de linguagem
Processamento de autenticação do serviço de aplicativo ocorre antes de solicitações acessar seu aplicativo de API, o que significa que os recursos de autenticação Olá funcionam para aplicativos escritos em qualquer idioma ou a estrutura da API.  A API pode ser baseada em ASP.NET, Java, Node.js ou qualquer estrutura à qual o Serviço de Aplicativo dê suporte.

Serviço de aplicativo passa no token web JSON hello (JWT) no cabeçalho de autorização de saudação de uma solicitação HTTP e código escrito em qualquer idioma ou a estrutura pode obter Olá informações necessárias de saudação token. Além disso, serviço de aplicativo fornece acesso mais fácil declarações toohello mais comumente usado definindo alguns cabeçalhos especiais, como a seguir hello:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Em uma API .NET, você pode usar o hello `Authorize` atributo e para autorização refinada que você pode facilmente escrever o código com base em declarações porque as informações de declarações são preenchidas nas classes do .NET.

## <a name="multiple-protection-options"></a>Várias opções de proteção
O Serviço de Aplicativo pode impedir que as solicitações HTTP anônimas atinjam seu aplicativo de API, ele pode passar todas as solicitações e validar os tokens para solicitações que os incluem ou pode deixar passar todas as solicitações sem realizar qualquer ação sobre elas:

1. Permitir que somente solicitações autenticadas tooreach seu aplicativo de API.
   
    Se uma solicitação anônima é recebida de um navegador, do serviço de aplicativo redirecionará tooa a página de logon para o provedor de autenticação hello (Twitter do Azure AD, Google, etc.) que você escolher. 
   
    Com essa opção, você não precisa toowrite qualquer código de autenticação em todos os em seu aplicativo, e o código de autorização é simplificado porque a declarações de hello mais importantes são fornecidas nos cabeçalhos HTTP da saudação.
2. Permitir tooreach de todas as solicitações de seu aplicativo de API, mas validar solicitações autenticadas e passa informações de autenticação nos cabeçalhos de saudação HTTP.
   
    Essa opção oferece mais flexibilidade no tratamento de solicitações anônimas, mas você tiver código toowrite se desejar que os usuários anônimos tooprevent usando sua API. Como declarações mais populares do hello são passadas em cabeçalhos de saudação de solicitações HTTP, o código de autorização é relativamente simple.
3. Permitir tooreach de todas as solicitações sua API, executar nenhuma ação nas informações de autenticação em solicitações de saudação.
   
    Essa opção deixa as tarefas de saudação de autenticação e autorização totalmente o código do aplicativo de tooyour.

Em Olá [portal do Azure](https://portal.azure.com/), selecionar opção de saudação desejada no hello **autenticação / autorização** folha.

![](./media/app-service-api-authentication/authblade.png)

Para opções 1 e 2, ativar **autenticação do serviço de aplicativo**e em hello **tootake ação quando a solicitação não está autenticada** lista suspensa escolha **login** ou **Permitir solicitação (nenhuma ação)**.  Se você escolher **login**, você toochoose um provedor de autenticação e configurar esse provedor.

![](./media/app-service-api-authentication/actiontotake.png)

Para obter informações detalhadas sobre como autenticação tooconfigure, consulte [como tooconfigure seu logon de Active Directory do Azure do serviço de aplicativo aplicativo toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). artigo de saudação se aplica a aplicativos tooAPI, bem como os aplicativos móveis e vincula tooother artigos para Olá outros provedores de autenticação.

## <a id="internal"></a> Autenticação da conta de serviço
Autenticação do serviço de aplicativo funciona para cenários internos, como para a chamada de um aplicativo de tooanother API de aplicativo de API. Neste cenário, você pode obter um token usando credenciais para uma conta de serviço em vez de credenciais de usuário final. Uma conta de serviço também pode ser chamada de *entidade de serviço* no Active Directory do Azure e a autenticação que usa essa conta também é conhecida como um cenário de serviço a serviço. 

Para cenários de serviço para proteger a saudação chamada aplicativo de API usando o Active Directory do Azure e fornecer um token de autorização de entidade de serviço do AAD ao chamar hello API do aplicativo. Você pode obter um token, fornecendo a ID de saudação do cliente e o segredo do aplicativo AAD de saudação do cliente. Nenhum código somente no Azure especial é necessário, como true toobe usado para lidar com o token do hello Zumo de serviços móveis. Um exemplo desse cenário usando aplicativos de API do ASP.NET é coberto por tutorial Olá [autenticação principal do serviço para aplicativos de API](app-service-api-dotnet-service-principal-auth.md).

Se você quiser toohandle um cenário de serviços sem usar autenticação do serviço de aplicativo, você pode usar certificados de cliente ou a autenticação básica. Para obter informações sobre certificados de cliente no Azure, consulte [como tooConfigure autenticação mútua do TLS para aplicativos Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Para saber mais sobre a autenticação básica no ASP.NET, confira [Filtros de autenticação na API Web 2 ASP.NET](http://www.asp.net/web-api/overview/security/authentication-filters).

Autenticação de conta de serviço de um aplicativo do serviço de aplicativo lógica aplicativo tooan API é um caso especial que é explicado em [usando sua API personalizada hospedado no serviço de aplicativo com aplicativos lógicos](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Autenticação de cliente móvel
Para obter informações sobre como toohandle autenticação de clientes móveis, consulte Olá [documentação sobre autenticação para aplicativos móveis](../app-service-mobile/app-service-mobile-ios-get-started-users.md). A autenticação do serviço de aplicativo funciona Olá mesma forma para aplicativos móveis e aplicativos de API.

## <a name="more-information"></a>Mais informações
Para obter mais informações sobre autenticação e autorização no serviço de aplicativo do Azure, consulte Olá recursos a seguir:

* [Como expandir a autenticação/autorização do Serviço de Aplicativo](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Como tooconfigure seu logon de Active Directory do Azure do serviço de aplicativo aplicativo toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (inclui links para outros provedores de autenticação na parte superior de saudação da página de saudação). 

Para obter mais informações sobre o OAuth 2.0, OpenID Connect e JSON Web Tokens (JWT), consulte Olá recursos a seguir.

* [Introdução ao OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [Introdução tooOAuth2, OpenID Connect e JSON Web Tokens (JWT) - curso Applied](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Curso Criação e proteção de uma API RESTful para vários clientes no ASP.NET - Pluralsight](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Para obter mais informações sobre o Active Directory do Azure, consulte Olá recursos a seguir.

* [Cenários do AD do Azure](http://aka.ms/aadscenarios)
* [Guia dos desenvolvedores do AD do Azure](http://aka.ms/aaddev)
* [Exemplos do AD do Azure](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Próximas etapas
Este artigo explicou os recursos de autenticação e de autorização do Serviço de Aplicativo que você pode usar para aplicativos de API. tutorial de Avançar Olá Olá fique iniciado série mostra como tooimplement [autenticação de usuário em aplicativos de API do serviço de aplicativo](app-service-api-dotnet-user-principal-auth.md).

