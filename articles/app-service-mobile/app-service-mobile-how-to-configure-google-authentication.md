---
title: "autenticação do Google tooconfigure aaaHow para seu aplicativo de serviços de aplicativos"
description: "Saiba como autenticação do Google tooconfigure para seu aplicativo de serviços de aplicativos."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Como tooconfigure o logon do serviço de aplicativo aplicativo toouse Google
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Google como um provedor de autenticação.

toocomplete Olá procedimento neste tópico, você deve ter uma conta do Google que tem um endereço de email verificado. toocreate uma nova conta do Google, vá muito[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"> </a>Registre seu aplicativo com o Google
1. Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo. Copiar seu **URL**, que você usar tooconfigure posterior seu aplicativo do Google.
2. Navegue toohello [apis do Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) site, entrar com suas credenciais de conta do Google, clique em **criar projeto**, forneça um **nome do projeto**, em seguida, clique em  **Criar**.
3. Em **APIs Sociais**, clique em **API do Google+** e em **Habilitar**.
4. Na saudação à esquerda de navegação, **credenciais** > **tela de consentimento de OAuth**, em seguida, selecione seu **endereço de Email**, insira um **nome do produto**e clique em **salvar**.
5. Em Olá **credenciais** , clique em **criar credenciais** > **ID do cliente OAuth**, em seguida, selecione **aplicativo Web**.
6. Colar Olá do serviço de aplicativo **URL** você copiou anteriormente em **origens autorizadas de JavaScript**, em seguida, cole o redirecionamento de URI em **URI de redirecionamento autorizado**. Olá redirecionar URI é a URL de saudação do seu aplicativo anexado ao caminho hello, */.auth/login/google/callback*. Por exemplo: `https://contoso.azurewebsites.net/.auth/login/google/callback`. Certifique-se de que você está usando o esquema do hello HTTPS. Em seguida, clique em **Criar**.
7. Na próxima tela de Olá, anote os valores de saudação do cliente de saudação segredo do cliente e a ID.

    > [!IMPORTANT]
    > segredo do cliente Olá é uma credencial de segurança importantes. Não compartilhe essa senha com ninguém nem distribua-a em um aplicativo cliente.


## <a name="secrets"></a>Aplicativo do Google adicionar informações tooyour
1. Em Olá [portal do Azure], navegar tooyour aplicativo. Clique em **Configurações** e em **Autenticação/Autorização**.
2. Se Olá autenticação / autorização de recurso não está ativada, ative o comutador hello muito**em**.
3. Clique em **Google**. Cole em valores de ID do aplicativo e o segredo do aplicativo hello que você obteve anteriormente e, opcionalmente, habilitar os escopos que seu aplicativo requer. Em seguida, clique em **OK**.
   
   ![][1]
   
   Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs. Você deve autorizar os usuários no código do aplicativo.
4. (Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Google, definir **tootake de ação quando a solicitação não está autenticada** muito**Google**. Isso requer que todas as solicitações autenticadas e todas as solicitações não autenticadas são redirecionada tooGoogle para autenticação.
5. Clique em **Salvar**.

Agora você está pronto toouse Google para autenticação em seu aplicativo.

## <a name="related-content"> </a>Conteúdo relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal do Azure]: https://portal.azure.com/

