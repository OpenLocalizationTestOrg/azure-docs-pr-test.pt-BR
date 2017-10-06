---
title: aaaAzure AD B2C | Microsoft Docs
description: "tipos de saudação de aplicativos que você pode criar em hello Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: tipos de aplicativos
O Active Directory B2C do Azure (AD do Azure) oferece suporte à autenticação para várias arquiteturas de aplicativos modernos. Todas elas são baseadas em protocolos padrão da indústria Olá [OAuth 2.0](active-directory-b2c-reference-protocols.md) ou [OpenID Connect](active-directory-b2c-reference-protocols.md). Este documento descreve brevemente os tipos de saudação de aplicativos que você pode criar, independente de plataforma ou idioma Olá preferir. Ele também ajuda a compreender os cenários de alto nível de saudação antes de você [começar a criar aplicativos](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>Noções básicas de saudação
Cada aplicativo que usa o Azure AD B2C deve ser registrado no seu [directory B2C](active-directory-b2c-get-started.md) via Olá [Portal do Azure](https://portal.azure.com/). processo de registro de aplicativo Hello coleta e atribui o aplicativo de tooyour alguns valores:

* Uma **ID de aplicativo** que identifica exclusivamente o aplicativo.
* Um **URI de redirecionamento** que pode ser usado toodirect respostas tooyour back aplicativo.
* Quaisquer outros valores específicos ao cenário. Para obter mais detalhes, saiba como muito[registrar um aplicativo](active-directory-b2c-app-registration.md).

Depois que o aplicativo hello é registrado, ele se comunica com o Azure AD enviando solicitações toohello AD do Azure v 2.0 ponto de extremidade:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Cada solicitação que é enviada tooAzure AD B2C Especifica um **política**. Uma política controla o comportamento de saudação do AD do Azure. Você também pode usar esses pontos de extremidade toocreate um conjunto altamente personalizável de experiências do usuário. Algumas políticas comuns incluem inscrição, entrada e edição de perfil. Se você não estiver familiarizado com as políticas, você deve ler sobre hello Azure AD B2C [estrutura da política extensível](active-directory-b2c-reference-policies.md) antes de continuar.

interação de saudação de todos os aplicativos com um ponto de extremidade v 2.0 segue um padrão semelhante de alto nível:

1. aplicativo Hello direciona Olá usuário toohello v 2.0 ponto de extremidade tooexecute um [política](active-directory-b2c-reference-policies.md).
2. usuário Olá conclui política Olá acordo com a definição de política de toohello.
3. aplicativo Hello recebe algum tipo de token de segurança do ponto de extremidade do hello v 2.0.
4. aplicativo Hello usa informações de token tooaccess protegido Olá segurança ou um recurso protegido.
5. servidor de saudação do recurso valida Olá segurança tooverify token que o acesso pode ser concedido.
6. aplicativo Hello atualiza periodicamente o token de segurança de saudação.

<!-- TODO: Need a page for libraries toolink too-->
Essas etapas podem diferir ligeiramente com base no tipo de saudação do aplicativo que você está criando. Bibliotecas de código-fonte aberto podem abordar detalhes Olá para você.

## <a name="web-apps"></a>Aplicativos Web
Para os aplicativos Web (incluindo .NET, PHP, Java, Ruby, Python e Node.js) hospedados em um servidor e acessados por meio de um navegador, o Azure AD B2C dá suporte ao [OpenID Connect](active-directory-b2c-reference-protocols.md) para todas as experiências de usuário. Isso inclui gerenciamento de entrada, de inscrição e de perfil. Na implementação de saudação do Azure AD B2C do OpenID Connect, seu aplicativo web inicia essas experiências de usuário emitindo solicitações de autenticação tooAzure AD. Olá resultado da solicitação de saudação é um `id_token`. Esse token de segurança representa a identidade do usuário hello. Ele também fornece informações sobre usuário Olá na forma de saudação de declarações:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Saiba mais sobre os tipos de saudação do aplicativo de tooan disponíveis de tokens e declarações em hello [referência de token B2C](active-directory-b2c-reference-tokens.md).

Em aplicativos Web, cada execução de uma [política](active-directory-b2c-reference-policies.md) usa estas etapas de alto nível:

![Imagem de raias do aplicativo Web](./media/active-directory-b2c-apps/webapp.png)

Validação de saudação `id_token` usando uma chave pública de autenticação recebido do AD do Azure é suficiente identidade de saudação do tooverify do usuário de saudação. Isso também define um cookie de sessão que pode ser usado tooidentify Olá usuário em solicitações de página subsequente.

toosee este cenário em ação, tente uma das Olá web aplicativo entrar exemplos de código nosso [Introdução seção](active-directory-b2c-overview.md#get-started).

Em adição toofacilitating simples entrar, um aplicativo de servidor web pode ser também necessário tooaccess um serviço web de back-end. Nesse caso, pode executar um pouco diferentes Olá web aplicativo [OpenID Connect fluxo](active-directory-b2c-reference-oidc.md) e adquirir tokens usando códigos de autorização e tokens de atualização. Este cenário é descrito na seguinte Olá [seção APIs da Web](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>APIs da Web
Você pode usar os serviços do Azure AD B2C toosecure web como API de web RESTful do seu aplicativo. APIs da Web pode usar OAuth 2.0 toosecure seus dados, solicitações HTTP de entrada usando tokens de autenticação. chamador de saudação de uma API da web acrescenta um token no cabeçalho de autorização de saudação de uma solicitação HTTP:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Olá web API, em seguida, pode usar a identidade e tooextract informações sobre chamador Olá de declarações são codificadas no token de saudação do chamador do hello tooverify token Olá API. Saiba mais sobre os tipos de saudação do aplicativo de tooan disponíveis de tokens e declarações em hello [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Atualmente, o Azure AD B2C dá suporte apenas a APIs Web acessadas por seus próprios clientes conhecidos. Por exemplo, seu aplicativo completo pode incluir um aplicativo iOS e aplicativo do Android e um API Web de back-end. Essa arquitetura tem total suporte. Permitir que um cliente de parceiro, como outro aplicativo do iOS, tooaccess Olá mesmo web que API não é suportada atualmente. Todos os componentes de saudação do seu aplicativo completo devem compartilhar um ID de aplicativo único.
>
>

Uma API Web pode receber tokens de muitos tipos de clientes, incluindo aplicativos Web, aplicativos móveis e de área de trabalho, aplicativos de página única, daemons do lado do servidor e até outras APIs Web. Aqui está um exemplo de fluxo de saudação completa para um aplicativo web que chama uma API da web:

![Imagem de raias da API da Web do aplicativo Web](./media/active-directory-b2c-apps/webapi.png)

toolearn mais informações sobre códigos de autorização, tokens de atualização e as etapas de saudação para obtenção de tokens, leia sobre Olá [protocolo OAuth 2.0](active-directory-b2c-reference-oauth-code.md).

toolearn como toosecure uma API da web usando o Azure AD B2C, check-out Olá web Tutoriais de API em nosso [Introdução seção](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Aplicativos móveis e nativos
Aplicativos que são instalados em dispositivos, como aplicativos de desktop e móveis, muitas vezes é preciso tooaccess serviços de back-end ou APIs da web em nome dos usuários. Você pode adicionar aplicativos nativos de tooyour personalizado de identidade de experiências de gerenciamento e com segurança chamar serviços back-end usando o Azure AD B2C e hello [fluxo de código de autorização do OAuth 2.0](active-directory-b2c-reference-oauth-code.md).  

Nesse fluxo, o aplicativo hello executa [políticas](active-directory-b2c-reference-policies.md) e recebe um `authorization_code` do AD do Azure após a conclusão de usuário Olá política hello. Olá `authorization_code` representa Olá serviços de back-end do aplicativo permissão toocall em nome de usuário de saudação que está conectado no momento. aplicativo Hello pode trocar Olá `authorization_code` no plano de fundo de saudação de um `id_token` e um `refresh_token`.  saudação de aplicativo pode usar Olá `id_token` tooauthenticate tooa back-end API da web nas solicitações HTTP. Ele também pode usar o hello `refresh_token` tooget um novo `id_token` quando expira mais antiga.

> [!NOTE]
> B2C do AD do Azure atualmente suporta apenas os tokens são usados tooaccess um serviço da web de back-end do aplicativo. Por exemplo, seu aplicativo completo pode incluir um aplicativo iOS e aplicativo do Android e um API Web de back-end. Essa arquitetura tem total suporte. Permitindo uma API da web do parceiro de sua tooaccess de aplicativo do iOS usando tokens de acesso OAuth 2.0 não é suportada atualmente. Todos os componentes de saudação do seu aplicativo completo devem compartilhar um ID de aplicativo único.
>
>

![Imagem de raias do aplicativo Nativo](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Limitações atuais
B2C do Azure AD não oferece suporte a saudação seguintes tipos de aplicativos, mas eles são roteiro de saudação. 

### <a name="daemonsserver-side-apps"></a>Aplicativos daemons/do lado do servidor
Aplicativos que contêm os processos de execução longa ou que opere sem a presença de saudação do usuário também precisam de uma maneira que tooaccess protegidos recursos, como APIs da web. Esses aplicativos podem autenticar e obter tokens usando a identidade do aplicativo hello (em vez de um delegado a identidade de usuário) e usando o fluxo de credenciais de cliente Olá OAuth 2.0.

Atualmente, esse fluxo não tem o suporte do AD B2C do Azure. Esses aplicativos podem obter tokens somente após a ocorrência de um fluxo de usuário interativo.

### <a name="web-api-chains-on-behalf-of-flow"></a>Cadeias de API Web (fluxo Em nome de)
Muitas arquiteturas incluem uma web API que precisa toocall outra API da web downstream, onde ambas são protegidas pelo Azure AD B2C. Esse cenário é comum em clientes nativos que têm um back-end de API Web. Em seguida, chama um serviço online da Microsoft, como hello Azure AD Graph API.

Neste cenário de API da web encadeadas pode ter suporte por meio de concessão de credencial de portador do OAuth 2.0 JWT hello, também conhecido como Olá em nome de fluxo.  No entanto, fluxo de saudação em nome de não está implementado atualmente no hello Azure AD B2C.
