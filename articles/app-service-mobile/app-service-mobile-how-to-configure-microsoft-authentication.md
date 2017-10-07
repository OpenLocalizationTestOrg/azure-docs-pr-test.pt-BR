---
title: "autenticação aaaHow tooconfigure Account da Microsoft para o seu aplicativo de serviços de aplicativos"
description: "Saiba como a autenticação tooconfigure Account da Microsoft para o seu aplicativo de serviços de aplicativos."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Como tooconfigure seu logon do serviço de aplicativo aplicativo toouse Account da Microsoft
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Account da Microsoft como um provedor de autenticação. 

## <a name="register-microsoft-account"> </a>Registrar seu aplicativo na conta da Microsoft
1. Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo. Copiar seu **URL**, que posteriormente você usar tooconfigure seu aplicativo com Account da Microsoft.
2. Navegue toohello [meus aplicativos] página Olá Microsoft Account Developer Center e faça logon com sua conta da Microsoft, se necessário.
3. Clique em **Adicionar um aplicativo** e digite um nome de aplicativo e clique em **Criar aplicativo**.
4. Anote Olá **ID do aplicativo**, pois você precisará dele mais tarde. 
5. Em "Plataformas", clique em **Adicionar plataforma** e selecione "Web".
6. Em "URIs de redirecionamento" fonte Olá ponto de extremidade para seu aplicativo, em seguida, clique em **salvar**. 
   
   > [!NOTE]
   > O redirecionamento de URI é a URL de saudação do seu aplicativo anexado ao caminho hello, */.auth/login/microsoftaccount/callback*. Por exemplo: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Certifique-se de que você está usando o esquema do hello HTTPS.
   
7. Em "Segredos do Aplicativo", clique em **Gerar nova senha**. Anote o valor de saudação que aparece. Depois que você sair página hello, ele não aparecerá novamente.

    > [!IMPORTANT]
    > senha Olá é uma credencial de segurança importantes. Não compartilhe Olá senha com ninguém ou distribuí-lo em um aplicativo cliente.

## <a name="secrets"></a>Adicionar conta da Microsoft informações tooyour aplicativo de serviço de aplicativo
1. Em Olá [portal do Azure], navegar tooyour aplicativo, clique em **configurações** > **autenticação / autorização**.
2. Se Olá autenticação / autorização de recurso não está habilitada, alternar **em**.
3. Clique em **Conta da Microsoft**. Cole em valores hello ID do aplicativo e a senha que você obteve anteriormente e, opcionalmente, habilitar os escopos que seu aplicativo requer. Em seguida, clique em **OK**.
   
    ![][1]
   
    Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs. Você deve autorizar os usuários no código do aplicativo.
4. (Opcional) toorestrict acesso tooyour site tooonly usuários autenticados por conta da Microsoft, definir **tootake de ação quando a solicitação não está autenticada** muito**Microsoft Account**. Isso requer que todas as solicitações autenticadas, e todas as solicitações não autenticadas são redirecionadas tooMicrosoft conta para autenticação.
5. Clique em **Salvar**.

Agora você está pronto toouse Account da Microsoft para autenticação em seu aplicativo.

## <a name="related-content"> </a>Conteúdo relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[meus aplicativos]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portal do Azure]: https://portal.azure.com/
