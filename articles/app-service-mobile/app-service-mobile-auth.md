---
title: "aaaAuthentication e autorização em aplicativos móveis do Azure | Microsoft Docs"
description: "Referência conceitual e visão geral da saudação autenticação / autorização de recursos para aplicativos móveis do Azure"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Autenticação e Autorização nos Aplicativos Móveis do Azure
## <a name="what-is-app-service-authentication--authorization"></a>O que é a Autenticação/Autorização do Serviço de Aplicativo?
> [!NOTE]
> Este tópico será migrado tooa consolidado [autenticação do serviço de aplicativo / autorização](../app-service/app-service-authentication-overview.md) tópico, que abrange a Web, móveis e aplicativos de API.
> 
> 

Autenticação do serviço de aplicativo / autorização é um recurso que permite que seu aplicativo toolog usuários sem alterações de código necessárias no back-end de aplicativo hello. Ele fornece uma maneira fácil tooprotect seu aplicativo e o trabalho com dados por usuário.

Serviço de aplicativo usa a identidade federada, em que um participante 3º **provedor de identidade** "IDP ("), armazena as contas e autentica usuários, e aplicativo hello usa essa identidade em vez de seu próprio. Serviço de aplicativo oferece suporte a provedores de identidade cinco imediato saudação: *Active Directory do Azure*, *Facebook*, *Google*, *Microsoft Account*, e *Twitter*. Você também pode expandir esse suporte para seus aplicativos ao integrar outro provedor de identidade ou sua própria solução de identidade personalizada.

Seu aplicativo pode utilizar qualquer quantidade desses provedores de identidade, para que você possa fornecer opções de como fazer logon aos seus usuários finais.

Se você quiser tooget iniciado imediatamente, consulte uma saudação tutoriais a seguir:

* [Adicionar aplicativo do iOS tooyour autenticação]
* [Adicionar autenticação tooyour xamarin aplicativo]
* [Adicionar autenticação tooyour xamarin aplicativo]
* [Adicionar aplicativo do Windows tooyour autenticação]

## <a name="how-authentication-works"></a>Como funciona a autenticação
Em ordem tooauthenticate de usando um dos provedores de identidade Olá, é necessário primeiro tooknow de provedor de identidade tooconfigure Olá sobre seu aplicativo. provedor de identidade Hello, em seguida, fornece IDs e segredos que você forneça back toohello aplicativo. Isso conclui a relação de confiança hello e permite que o serviço de aplicativo toovalidate identidades fornecidas tooit.

Essas etapas são detalhadas no hello seguintes tópicos:

* [Como tooconfigure seu logon do aplicativo toouse Active Directory do Azure]
* [Como tooconfigure o logon do Facebook toouse aplicativo]
* [Como tooconfigure o logon do Google toouse aplicativo]
* [Como tooconfigure seu logon do aplicativo toouse Account da Microsoft]
* [Como tooconfigure o logon do Twitter toouse aplicativo]

Depois que tudo está configurado no back-end do hello, você pode modificar seu toolog de cliente no. Há duas abordagens aqui:

* SDK de cliente usando uma única linha de código, permitem Olá aplicativos móveis entre em usuários.
* Aproveitar um SDK publicado por uma identidade de tooestablish do provedor de identidade fornecida e, em seguida, obtenha acesso tooApp serviço.

> [!TIP]
> A maioria dos aplicativos deve usar um tooget SDK do provedor, uma experiência de logon mais sensação de nativo e suporte de atualização de tooleverage e outros benefícios específicos do provedor.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>Como funciona a autenticação sem um SDK do provedor
Se você não desejar tooset um provedor de SDK, você pode permitir logon de saudação do tooperform de aplicativos móveis para você. SDK de cliente de aplicativos móveis Olá abrirá um provedor de toohello de exibição da web de sua completa e escolhendo Olá entrar. Ocasionalmente em blogs e fóruns, que você verá isso chamado tooas hello "fluxo de servidor" ou "orientado para servidor fluxo", pois o servidor de saudação está gerenciando logon hello e SDK de cliente Olá nunca recebe o token de saudação do provedor.

código de saudação necessário toostart que esse fluxo é coberto no tutorial de autenticação Olá para cada plataforma. No final de saudação do fluxo de Olá, SDK de cliente Olá tem um token de serviço de aplicativo e token Olá é anexado automaticamente tooall solicitações toohello backend.

### <a name="how-authentication-with-a-provider-sdk-works"></a>Como funciona a autenticação com um SDK do provedor
Trabalhando com um provedor de SDK permite Olá toointeract de experiência de log mais junto com a plataforma de Olá aplicativo de saudação do sistema operacional está em execução no. Isso também fornece um token do provedor e algumas informações de usuário no cliente hello, o que torna muito mais fácil gráfico de tooconsume APIs e personalizar a experiência do usuário hello. Ocasionalmente em blogs e fóruns você verá esse Olá tooas chamado "fluxo de cliente" ou "direcionada pelo cliente fluxo" desde o código no cliente hello está tratando logon hello e código de saudação do cliente tem token de acesso do provedor de tooa.

Depois de obter um token do provedor, ele precisa toobe enviado tooApp serviço para validação. No final de saudação do fluxo de Olá, SDK de cliente Olá tem um token de serviço de aplicativo e token Olá é anexado automaticamente tooall solicitações toohello backend. desenvolvedor Olá também pode manter um token de referência do provedor toohello se eles assim escolhem.

## <a name="how-authorization-works"></a>Como funciona a autorização
Autenticação do serviço de aplicativo / autorização expõe várias opções para **tootake de ação quando a solicitação não está autenticada**. Antes de seu código recebe uma solicitação em questão, você pode ter toosee de verificação do serviço de aplicativo se Olá solicitação for autenticada e se não, rejeite-o e a tentativa de logon de usuário do hello toohave antes de tentar novamente.

Uma opção é toohave não autenticado solicitações redirecionam tooone Olá de provedores de identidade. Em um navegador da web, na verdade, isso levaria nova página do hello usuário tooa. No entanto, seu cliente móvel não poderá ser redirecionado dessa maneira, e as respostas não autenticadas receberão uma resposta HTTP *401 não autorizado* . Dito isto, primeira solicitação de saudação faz com que o cliente sempre deve ser o ponto de extremidade de logon toohello e, em seguida, você pode fazer chamadas tooany outras APIs. Se você tentar outra API toocall antes de efetuar login, o cliente receberá um erro.

Se você quiser toohave mais granular controle sobre quais pontos de extremidade requer autenticação, você também pode escolher "nenhuma ação (Permitir solicitação)" para as solicitações não autenticadas. Nesse caso, todas as decisões de autenticação são adiadas tooyour o código do aplicativo. Isso também permite que você tooallow acesso toospecific usuários com base nas regras de autorização personalizada.

## <a name="documentation"></a>Documentação
Olá Mostrar tutoriais a seguir como tooadd autenticação tooyour clientes móveis usando o serviço de aplicativo:

* [Adicionar aplicativo do iOS tooyour autenticação]
* [Adicionar autenticação tooyour xamarin aplicativo]
* [Adicionar autenticação tooyour xamarin aplicativo]
* [Adicionar aplicativo do Windows tooyour autenticação]

Olá seguintes tutoriais mostram como provedores de autenticação diferentes de tooleverage tooconfigure do serviço de aplicativo:

* [Como tooconfigure seu logon do aplicativo toouse Active Directory do Azure]
* [Como tooconfigure o logon do Facebook toouse aplicativo]
* [Como tooconfigure o logon do Google toouse aplicativo]
* [Como tooconfigure seu logon do aplicativo toouse Account da Microsoft]
* [Como tooconfigure o logon do Twitter toouse aplicativo]

Se desejar toouse um sistema de identidade que Olá aqueles fornecidos aqui, você também pode aproveitar Olá [visualizar o suporte a autenticação personalizada no SDK do servidor do .NET Olá](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Adicionar aplicativo do iOS tooyour autenticação]: app-service-mobile-ios-get-started-users.md
[Adicionar autenticação tooyour xamarin aplicativo]: app-service-mobile-xamarin-ios-get-started-users.md
[Adicionar autenticação tooyour xamarin aplicativo]: app-service-mobile-xamarin-android-get-started-users.md
[Adicionar aplicativo do Windows tooyour autenticação]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Como tooconfigure seu logon do aplicativo toouse Active Directory do Azure]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Como tooconfigure o logon do Facebook toouse aplicativo]: app-service-mobile-how-to-configure-facebook-authentication.md
[Como tooconfigure o logon do Google toouse aplicativo]: app-service-mobile-how-to-configure-google-authentication.md
[Como tooconfigure seu logon do aplicativo toouse Account da Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Como tooconfigure o logon do Twitter toouse aplicativo]: app-service-mobile-how-to-configure-twitter-authentication.md
