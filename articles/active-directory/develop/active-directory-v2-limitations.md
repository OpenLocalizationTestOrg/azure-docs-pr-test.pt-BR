---
title: "aaaAzure do Active Directory restrições e limitações do ponto de extremidade v 2.0 | Microsoft Docs"
description: "Uma lista de limitações e restrições para o ponto de extremidade do AD do Azure de saudação v 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>O ponto de extremidade do hello v 2.0 devo usar?
Ao criar aplicativos que se integram com o Active Directory do Azure, é necessário toodecide se os protocolos de autenticação e o ponto de extremidade de v 2.0 Olá atender às suas necessidades. O ponto de extremidade original do Azure Active Directory ainda tem suporte completo e, em alguns aspectos, tem mais recursos do que o v2.0. No entanto, Olá ponto de extremidade v 2.0 [apresenta benefícios significativos](active-directory-v2-compare.md) para desenvolvedores.

No momento, esta é nossa recomendação simplificada para desenvolvedores:

* Se você deve oferecer suporte a contas pessoais da Microsoft em seu aplicativo, use o ponto de extremidade do hello v 2.0. Mas, antes disso, certifique-se de entender as limitações de saudação que discutimos neste artigo.
* Se seu aplicativo precisa apenas toosupport trabalho da Microsoft e contas de estudante, não use o ponto de extremidade do hello v 2.0. Em vez disso, consulte tooour [guia do desenvolvedor do AD do Azure](active-directory-developers-guide.md).

Ao longo do tempo, o ponto de extremidade do hello v 2.0 crescerá restrições de saudação tooeliminate listadas aqui, para que você só precisará de ponto de extremidade do toouse Olá v 2.0. Em Olá enquanto isso, este artigo é pretendido toohelp é determinar se o ponto de extremidade do hello v 2.0 é ideal para você. Continuaremos tooupdate nesse estado artigo tooreflect Olá atual do ponto de extremidade do hello v 2.0. Deixe de conferir tooreevaluate seus requisitos com recursos de versão 2.0.

Se você tiver um aplicativo existente do AD do Azure que não usa o ponto de extremidade do hello v 2.0, não há nenhum toostart necessidade do zero. Em Olá futuro, forneceremos uma maneira para você toouse seus aplicativos existentes do AD do Azure com o ponto de extremidade do hello v 2.0.

## <a name="restrictions-on-app-types"></a>Restrições de tipos de aplicativo
Atualmente, hello seguintes tipos de aplicativos não são suportados pelo ponto de extremidade do hello v 2.0. Para obter uma descrição dos tipos de aplicativos com suporte, consulte [tipos de aplicativo de ponto de extremidade do hello Active Directory do Azure v 2.0](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>APIs da Web autônomas
Você pode usar o ponto de extremidade do hello v 2.0 muito[criar uma API da Web que é protegida com OAuth 2.0](active-directory-v2-flows.md#web-apis). No entanto, essa API da Web pode receber tokens somente de um aplicativo que tem Olá a ID do mesmo aplicativo. Você não pode acessar uma API Web de um cliente com uma ID de aplicativo diferente. cliente de saudação não ser capaz de toorequest ou obtenha permissões tooyour API da Web.

toosee como toobuild uma API da Web que aceita tokens de um cliente que tenha Olá a mesma ID de aplicativo, consulte Olá exemplos de API da Web de ponto de extremidade v 2.0 em nosso [Introdução](active-directory-appmodel-v2-overview.md#getting-started) seção.

## <a name="restrictions-on-app-registrations"></a>Restrições quanto a registros de aplicativos
No momento, para cada aplicativo que você deseja toointegrate com o ponto de extremidade do hello v 2.0, você deve criar um registro de aplicativo no hello novo [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). O AD do Azure existente ou aplicativos de conta da Microsoft não são compatíveis com o ponto de extremidade do hello v 2.0. Aplicativos que são registrados em qualquer portal diferente Olá Portal de registro de aplicativo não são compatíveis com o ponto de extremidade do hello v 2.0. Olá futuro, planejamos tooprovide toouse uma maneira um aplicativo existente como um aplicativo v 2.0. No entanto, no momento, há um caminho de migração para um toowork de aplicativo existente com o ponto de extremidade do hello v 2.0.

Além disso, os registros do aplicativo que você criar no hello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ter Olá condições a seguir:

* Apenas dois segredos do aplicativo são permitidos por ID do Aplicativo.
* Um registro de aplicativo registrado por um usuário com uma conta pessoal da Microsoft pode ser exibido e gerenciado somente por uma única conta de desenvolvedor. Ele não pode ser compartilhado entre vários desenvolvedores.  Se você quiser tooshare seu registro de aplicativo entre vários desenvolvedores, você pode criar o aplicativo hello entrar no portal de registro de saudação com uma conta do AD do Azure.
* Há várias restrições em formato de saudação do redirecionamento Olá URI que é permitido. Para obter mais informações sobre redirecionamento de URIs, consulte Olá próxima seção.

## <a name="restrictions-on-redirect-uris"></a>Restrições de URIs de redirecionamento
Atualmente, os aplicativos que estão registrados no hello Portal de registro de aplicativo são conjunto restrito tooa limitado de valores URI de redirecionamento. Olá redirecionar URI para serviços e aplicativos web deve começar com o esquema de saudação `https`, e todos os valores URI de redirecionamento devem compartilhar um único domínio DNS. Por exemplo, não é possível registrar um aplicativo Web que tem um destes URIs de redirecionamento:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

sistema de registro de saudação compara Olá todo nome DNS de saudação existente redirecionar URI toohello nome DNS de redirecionamento Olá URI que você está adicionando. nome DNS do Hello solicitação tooadd Olá falhará se uma saudação seguintes condições for verdadeira:  

* nome DNS todo saudação do URI de redirecionamento novo Olá não coincide com nome DNS de saudação do URI de redirecionamento existente Olá.
* Olá todo nome DNS do URI de redirecionamento novo Olá não é um subdomínio do URI de redirecionamento existente hello.

Por exemplo, se o aplicativo hello tem esse URI de redirecionamento:

`https://login.contoso.com`

Você pode adicionar tooit, como este:

`https://login.contoso.com/new`

Nesse caso, o nome DNS de saudação corresponder exatamente. Ou você pode fazer isto:

`https://new.login.contoso.com`

Nesse caso, você está fazendo referência tooa subdomínio DNS de login.contoso.com. Se você quiser toohave um aplicativo que tenha o logon east.contoso.com e west.contoso.com logon como URIs de redirecionamento, você deve adicionar que os URIs de redirecionamento nesta ordem:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Você pode adicionar Olá último dois porque eles são subdomínios de saudação primeiro URI de redirecionamento, contoso.com. Essa limitação será removida em uma versão futura.

toolearn como tooregister um aplicativo hello Portal de registro de aplicativo, consulte [como tooregister um aplicativo com o ponto de extremidade do hello v 2.0](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Restrições de serviços e APIs
No momento, o ponto de extremidade do hello v 2.0 dá suporte a entrar para qualquer aplicativo que está registrado no hello Portal de registro de aplicativo, e que esteja na lista de saudação do [suporte para fluxos de autenticação](active-directory-v2-flows.md). No entanto, esses aplicativos podem adquirir tokens de acesso do OAuth 2.0 para um conjunto muito limitado de recursos. problemas de ponto de extremidade Olá v 2.0 acessar tokens apenas para:

* aplicativo Hello que solicitou o token hello. Um aplicativo pode adquirir um token de acesso para si mesmo, se o aplicativo lógico Olá é composto de vários componentes diferentes ou camadas. toosee esse cenário em ação, Confira nosso [Introdução](active-directory-appmodel-v2-overview.md#getting-started) tutoriais.
* saudação de email do Outlook, o calendário e contatos APIs de REST, que estão localizados em https://outlook.office.com. toolearn como toowrite um aplicativo que acessa essas APIs, consulte Olá [Office Introdução](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) tutoriais.
* APIs do Microsoft Graph. Você pode aprender mais sobre [Microsoft Graph](https://graph.microsoft.io) e dados Olá tooyou disponível.

Nenhum outro serviço tem suporte no momento. Mais serviços Online da Microsoft serão adicionados em Olá futura, além disso toosupport para seus próprios serviços e APIs da Web personalizados.

## <a name="restrictions-on-libraries-and-sdks"></a>Restrição de bibliotecas e SDKs
No momento, o suporte de biblioteca para o ponto de extremidade do hello v 2.0 é limitado. Se desejar que o ponto de extremidade do toouse Olá v 2.0 em um aplicativo de produção, você terá estas opções:

* Se você estiver criando um aplicativo da web, você pode usar com segurança Microsoft disponível middleware do lado do servidor tooperform entrar e token de validação. Esses incluem hello OWIN Open ID conectar middleware para ASP.NET e hello Node. js Passport plug-in. Para obter exemplos de código que usam o middleware da Microsoft, veja a nossa seção [Introdução](active-directory-appmodel-v2-overview.md#getting-started).
* Se você estiver criando um aplicativo móvel ou de área de trabalho, poderá usar uma de nossa MSAL (Biblioteca de Autenticação da Microsoft) de versão prévia.  Essas bibliotecas estão em uma visualização de suporte de produção, portanto, é seguro toouse-los em aplicativos de produção. Você pode ler mais sobre termos Olá Olá visualizar e Olá bibliotecas disponíveis em nosso [referência bibliotecas de autenticação](active-directory-v2-libraries.md).
* Para plataformas não cobertas por bibliotecas Microsoft, você pode integrar com o ponto de extremidade do hello v 2.0 diretamente enviando e recebendo mensagens de protocolo no código do aplicativo. Olá protocolos de OpenID Connect e OAuth v 2.0 [explicitamente documentadas](active-directory-v2-protocols.md) toohelp executar tal uma integração.
* Por fim, você pode usar o código-fonte aberto abrir ID conectar e OAuth bibliotecas toointegrate com o ponto de extremidade do hello v 2.0. protocolo do Hello v 2.0 deve ser compatível com muitas bibliotecas de protocolo do código-fonte aberto sem alterações importantes. disponibilidade Olá desses tipos de bibliotecas varia de acordo com o idioma e plataforma. Olá [abrir conexão de ID](http://openid.net/connect/) e [OAuth 2.0](http://oauth.net/2/) sites mantém uma lista de implementações populares. Para obter mais informações, consulte [bibliotecas v 2.0 e a autenticação do Active Directory do Azure](active-directory-v2-libraries.md)e lista de saudação de bibliotecas de cliente do código-fonte aberto e exemplos que foram testados com o ponto de extremidade do hello v 2.0.

## <a name="restrictions-on-protocols"></a>Restrições quanto a protocolos
o ponto de extremidade do Hello v 2.0 não oferece suporte SAML ou WS-Federation; suporta apenas a conexão aberta de ID e OAuth 2.0.  Nem todos os recursos e funcionalidades dos protocolos OAuth foram incorporadas ao ponto de extremidade do hello v 2.0. Esses recursos de protocolo e os recursos estão atualmente *não disponível* no ponto de extremidade do hello v 2.0:

* Tokens de ID que são emitidos pelo ponto de extremidade do hello v 2.0 não contêm um `email` de declaração de usuário hello, mesmo se você adquirir permissão de saudação usuário tooview seus emails.
* ponto de extremidade de OpenID conectar UserInfo Olá não está implementado no ponto de extremidade do hello v 2.0. No entanto, todos os dados de perfil de usuário que você potencialmente receberia neste ponto de extremidade está disponível de saudação do Microsoft Graph `/me` ponto de extremidade.
* o ponto de extremidade do Hello v 2.0 não oferece suporte a emissão de declarações de função ou grupo em tokens de ID.
* Olá [concessão de credenciais de senha de proprietário do OAuth 2.0 recurso](https://tools.ietf.org/html/rfc6749#section-4.3) não é suportado pelo ponto de extremidade do hello v 2.0.

Além disso, o ponto de extremidade do hello v 2.0 não suporta qualquer forma de saudação SAML ou protocolos WS-Federation.

toobetter compreender o escopo de saudação da funcionalidade de protocolo com suporte no ponto de extremidade v 2.0 de hello, leia nossa [referência de protocolo OpenID Connect e OAuth 2.0](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Restrições de contas corporativas e de estudante
Se você tiver usado a biblioteca de autenticação do Active Directory (ADAL) em aplicativos do Windows, você pode se beneficiam com autenticação integrada do Windows, que usa a concessão de asserção SAML Security Assertion Markup Language () hello. Com essa concessão, os usuários de locatários do Azure AD federados se autenticam com suas instâncias do Active Directory local sem inserir as credenciais. Atualmente, concessão de asserção SAML Olá não tem suporte no ponto de extremidade do hello v 2.0.
