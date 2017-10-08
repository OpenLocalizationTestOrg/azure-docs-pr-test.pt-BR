---
title: "autenticação do Twitter tooconfigure aaaHow para seu aplicativo de serviços de aplicativos"
description: "Saiba como autenticação do Twitter tooconfigure para seu aplicativo de serviços de aplicativos."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Como tooconfigure seu logon do serviço de aplicativo aplicativo toouse Twitter
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Twitter como um provedor de autenticação.

toocomplete Olá procedimento neste tópico, você deve ter uma conta do Twitter que tem um número de telefone e endereço de email verificado. toocreate uma nova conta do Twitter, ir muito<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"> </a>Registre seu aplicativo com o Twitter
1. Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo. Copie a **URL**. Você usará esse tooconfigure seu aplicativo do Twitter.
2. Navegue toohello [Twitter desenvolvedores] site da Web, entre com suas credenciais de conta do Twitter e clique em **criar novo aplicativo**.
3. Tipo de saudação **nome** e um **descrição** para seu novo aplicativo. Colar em seu aplicativo **URL** para Olá **site** valor. Em seguida, para Olá **URL de retorno de chamada**, cole Olá **URL de retorno de chamada** copiados anteriormente. Este é o seu gateway de aplicativo móvel anexado ao caminho hello, */.auth/login/twitter/callback*. Por exemplo: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Certifique-se de que você está usando o esquema do hello HTTPS.
4. Na página de saudação do hello inferior, leia e aceite os termos de saudação. Em seguida, clique em **Criar seu Aplicativo do Twitter**. Este aplicativo de saudação registra exibe detalhes do aplicativo hello.
5. Clique Olá **configurações** guia seleção **permitir toosign de toobe usado neste aplicativo com o Twitter**, em seguida, clique em **configurações de atualização**.
6. Selecione Olá **chaves e Tokens de acesso** guia. Anote os valores de saudação do **chave do consumidor (chave de API)** e **segredo do consumidor (segredo de API)**.
   
   > [!NOTE]
   > segredo do consumidor Olá é uma credencial de segurança importantes. Não compartilhe esse segredo com ninguém nem o distribua com seu aplicativo.
   > 
   > 

## <a name="secrets"></a>Twitter Adicionar aplicativo do information tooyour
1. Em Olá [portal do Azure], navegar tooyour aplicativo. Clique em **Configurações** e em **Autenticação/Autorização**.
2. Se Olá autenticação / autorização de recurso não está ativada, ative o comutador hello muito**em**.
3. Clique em **Twitter**. Cole em hello ID do aplicativo e o segredo do aplicativo valores que você obteve anteriormente. Em seguida, clique em **OK**.
   
   ![][1]
   
   Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs. Você deve autorizar os usuários no código do aplicativo.
4. (Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Twitter, definir **tootake de ação quando a solicitação não está autenticada** muito**Twitter**. Isso requer que todas as solicitações autenticadas e todas as solicitações não autenticadas são redirecionada tooTwitter para autenticação.
5. Clique em **Salvar**.

Agora você está pronto toouse Twitter para autenticação em seu aplicativo.

## <a name="related-content"> </a>Conteúdo relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter desenvolvedores]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portal do Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
