---
title: tipos de aaaApp para o ponto de extremidade do hello Active Directory do Azure v 2.0 | Microsoft Docs
description: "tipos de saudação de aplicativos e cenários com suporte pelo ponto de extremidade do hello Active Directory do Azure v 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Tipos de aplicativo de ponto de extremidade do hello Active Directory do Azure v 2.0
Olá ponto de extremidade do Azure Active Directory (AD do Azure) v 2.0 dá suporte à autenticação para uma variedade de arquiteturas de aplicativos modernos, todas elas com base em protocolos padrão do setor [OAuth 2.0 ou o OpenID Connect](active-directory-v2-protocols.md). Este artigo descreve os tipos de saudação de aplicativos que você pode criar usando a versão 2.0 do AD do Azure, independentemente de seu idioma preferencial ou plataforma. Olá, informações neste artigo são projetado toohelp compreender os cenários de alto nível antes de você [começar a trabalhar com o código de saudação](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure. toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>Noções básicas de saudação
Você deve registrar cada aplicativo que usa o ponto de extremidade do hello v 2.0 em Olá [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com). processo de registro de aplicativo Hello coleta e atribui esses valores para seu aplicativo:

* Uma **ID de Aplicativo** que identifica exclusivamente o aplicativo
* Um **URI de redirecionamento** que você pode usar toodirect respostas tooyour back aplicativo
* Alguns outros valores específicos de cenário

Para obter detalhes, saiba como muito[registrar um aplicativo](active-directory-v2-app-registration.md).

Depois que o aplicativo hello é registrado, Olá aplicativo se comunica com o AD do Azure enviando solicitações toohello AD do Azure v 2.0 ponto de extremidade. Podemos fornecer estruturas de código-fonte aberto e bibliotecas que manipular detalhes de saudação dessas solicitações. Você também tem lógica de autenticação Olá opção tooimplement Olá por conta própria, criando pontos de extremidade toothese de solicitações:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>Aplicativos Web
Para aplicativos web (.NET, PHP, Java, Ruby, Python, nós) que Olá acessos de usuário por meio de um navegador, você pode usar [OpenID Connect](active-directory-v2-protocols.md) para entrada do usuário. No OpenID Connect, Olá web aplicativo recebe um token de ID. Um token de ID é um token de segurança que verifica a identidade do usuário hello e fornece informações sobre o usuário Olá na forma de saudação de declarações:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Você pode aprender sobre todos os tipos de saudação de tokens e declarações que estão disponíveis tooan aplicativo hello [v 2.0 tokens referência](active-directory-v2-tokens.md).

Em aplicativos de servidor da web, o fluxo de autenticação de entrada hello usa essas etapas de alto nível:

![Fluxo de autenticação do aplicativo Web](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Você pode garantir Olá a identidade de usuário por meio da validação de token de ID de saudação com uma chave pública de autenticação recebido do ponto de extremidade do hello v 2.0. Um cookie de sessão é definido, o que pode ser um usuário de saudação tooidentify usado em solicitações de página subsequente.

toosee este cenário em ação, tente um Olá web sign-in do código de aplicativo amostras em nosso v 2.0 [Introdução](active-directory-appmodel-v2-overview.md#getting-started) seção.

Além disso toosimple entrar, um aplicativo web do servidor talvez seja necessário tooaccess outro serviço da web, como uma API REST. Nesse caso, aplicativo de servidor web hello participa de um fluxo combinado de OpenID Connect e OAuth 2.0, usando Olá [fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols.md). Para saber mais sobre esse cenário, leia sobre a [Introdução aos aplicativos Web e APIs Web](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>APIs da Web
Você pode usar o hello v 2.0 ponto de extremidade toosecure serviços da web, como a API da Web RESTful de seu aplicativo. Em vez de tokens de ID e os cookies de sessão, uma API da Web usa um toosecure de token de acesso OAuth 2.0 seus dados e tooauthenticate solicitações de entrada. chamador Olá da API Web acrescenta um token de acesso no cabeçalho de autorização de saudação de uma solicitação HTTP, como este:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Olá API da Web usa identidade e tooextract informações sobre chamador Olá de declarações são codificadas no token de acesso de saudação do chamador de API Olá tooverify token Olá acesso. toolearn sobre todos os tipos de saudação de tokens e declarações que estão disponíveis tooan aplicativo, consulte Olá [v 2.0 tokens referência](active-directory-v2-tokens.md).

Uma API da Web pode dar a usuários Olá power tooopt em ou recusar a funcionalidade específica ou dados expondo permissões, também conhecido como [escopos](active-directory-v2-scopes.md). Para um chamada aplicativo tooacquire tooa escopo de permissão, o usuário de saudação deve concordar toohello escopo durante um fluxo. o ponto de extremidade do Hello v 2.0 pede a permissão de usuário hello e registra as permissões em todos os tokens de acesso que Olá que recebe de API da Web. Olá Web API valida os tokens de acesso de saudação recebidas em cada chamada e executa verificações de autorização.

Uma API da Web pode receber tokens de acesso de todos os tipos de aplicativos, incluindo aplicativos de servidor Web, aplicativos móveis e de desktop, aplicativos de página única, daemons do lado do servidor e até outras APIs da Web. fluxo de alto nível Olá para uma API da Web tem esta aparência:

![Fluxo de autenticação da API Web](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn como toosecure uma API da Web usando os tokens de acesso OAuth2, check-out Olá código da API da Web amostras em nosso [Introdução](active-directory-appmodel-v2-overview.md#getting-started) seção.

Em muitos casos, APIs da web também precisa de solicitações de saída toomake tooother downstream web APIs protegido pelo Active Directory do Azure.  toodo assim, APIs da web podem tirar proveito do AD do Azure **em nome de** fluxo, que permite Olá web API tooexchange um token de acesso de entrada para outra toobe de token de acesso usado em solicitações de saída.  Olá v 2.0 ponto de extremidade em nome de fluxo é descrito em [detalhes](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Aplicativos móveis e nativos
Aplicativos de dispositivo instalado, como aplicativos de desktop e móveis, muitas vezes é preciso tooaccess serviços de back-end ou APIs da Web que armazenam dados e executar funções em nome do usuário. Esses aplicativos podem adicionar serviços de tooback-end de entrada e autorização usando Olá [fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

Nesse fluxo, aplicativo hello recebe um código de autorização do ponto de extremidade do hello v 2.0 quando Olá usuário faz logon. Serviços de back-end do aplicativo do hello representa código Olá autorização permissão toocall em nome de usuário de saudação que está conectado. aplicativo Hello pode trocar o código de autorização Olá no plano de fundo de saudação para um token de acesso OAuth 2.0 e um token de atualização. aplicativo Hello pode usar tooWeb tooauthenticate token de acesso Olá APIs em solicitações HTTP e usar Olá atualização tooget token novos tokens de acesso quando os tokens de acesso mais antigos expirarem.

![Fluxo de autenticação do aplicativo nativo](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Aplicativos de página única (JavaScript)
Muitos aplicativos modernos têm um aplicativo de página única front-end que é escrito principalmente em JavaScript. Geralmente, ele é escrito usando uma estrutura como AngularJS, Ember.js ou Durandal.js. o ponto de extremidade do Hello AD do Azure versão 2.0 dá suporte a esses aplicativos usando Olá [fluxo implícito do OAuth 2.0](active-directory-v2-protocols-implicit.md).

Nesse fluxo, o aplicativo hello recebe tokens diretamente do hello v 2.0 autorizar o ponto de extremidade, sem qualquer trocas de servidor para servidor. Todas as lógica de autenticação e leva de tratamento de sessão ocorre inteiramente no cliente de JavaScript hello, sem redirecionamentos de página adicionais.

![Fluxo de autenticação implícita](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee este cenário em ação, tente um dos exemplos de código do aplicativo de página única saudação em nosso [Introdução](active-directory-appmodel-v2-overview.md#getting-started) seção.

## <a name="daemons-and-server-side-apps"></a>Daemons e aplicativos do lado do servidor
Aplicativos que têm processos de execução longa ou que opere sem interação com o usuário também precisam de uma maneira que tooaccess protegidos recursos, como APIs da Web. Esses aplicativos podem autenticar e obter tokens usando a identidade do aplicativo hello, em vez de um usuário delegado identidade, com o fluxo de credenciais de cliente Olá OAuth 2.0.

Nesse fluxo, o aplicativo hello interage diretamente com hello `/token` pontos de extremidade do ponto de extremidade tooobtain:

![Fluxo de autenticação de aplicativo de daemon](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild um aplicativo daemon, consulte a documentação de credenciais de cliente de saudação em nosso [Introdução](active-directory-appmodel-v2-overview.md#getting-started) seção ou tente um [aplicativo de exemplo .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
