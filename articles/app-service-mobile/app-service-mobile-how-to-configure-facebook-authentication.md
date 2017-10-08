---
title: "autenticação do Facebook tooconfigure aaaHow para seu aplicativo de serviços de aplicativos"
description: "Saiba como a autenticação do Facebook tooconfigure para seu aplicativo de serviços de aplicativos."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Como tooconfigure o logon do Facebook do serviço de aplicativo aplicativo toouse
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Facebook como um provedor de autenticação.

toocomplete Olá procedimento neste tópico, você deve ter uma conta do Facebook que tem um endereço de email verificado e o número de telefone celular. toocreate uma nova conta do Facebook, ir muito[facebook.com].

## <a name="register"> </a>Registrar seu aplicativo com o Facebook
1. Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo. Copie a **URL**. Você usará esse tooconfigure seu aplicativo do Facebook.
2. Em outra janela do navegador, navegue toohello [os desenvolvedores do Facebook] as credenciais de conta de site da Web e entrar com o Facebook.
3. (Opcional) Se você já não tiver registrado, clique em **aplicativos** > **registrar como um desenvolvedor**, aceite a política de saudação e siga as etapas de registro de saudação.
4. Clique em **Meus Aplicativos** > **Adicionar um Novo Aplicativo** > **Site** > **Ignore e Criar ID do Aplicativo**. 
5. Em **nome de exibição**, digite um nome exclusivo para seu aplicativo, o tipo de sua **Contact Email**, escolha um **categoria** para seu aplicativo, em seguida, clique em **criar ID do aplicativo**e concluir a verificação de segurança de saudação. Isso leva toohello painel do desenvolvedor para o novo aplicativo do Facebook.
6. Em "Logon no Facebook", clique em **Introdução**. Adicionar o aplicativo **URI de redirecionamento** muito**URIs de redirecionamento OAuth válido**, em seguida, clique em **salvar alterações**. 
   
   > [!NOTE]
   > O redirecionamento de URI é a URL de saudação do seu aplicativo anexado ao caminho hello, */.auth/login/facebook/callback*. Por exemplo: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Certifique-se de que você está usando o esquema do hello HTTPS.
   > 
   > 
7. Na navegação saudação do lado esquerdo, clique em **configurações**. Em Olá **segredo do aplicativo** , clique em **Mostrar**, forneça a senha, se solicitado, em seguida, anote os valores de saudação do **ID do aplicativo** e **segredo do aplicativo**. Use esses tooconfigure posterior seu aplicativo no Azure.
   
   > [!IMPORTANT]
   > segredo do aplicativo Hello é uma credencial de segurança importantes. Não compartilhe essa senha com ninguém nem distribua-a em um aplicativo cliente.
   > 
   > 
8. Olá conta do Facebook que foi usado tooregister Olá aplicativo é um administrador do aplicativo hello. Neste ponto, apenas os administradores podem entrar neste aplicativo. tooauthenticate outras contas do Facebook, clique em **revisão de aplicativo** e habilitar **Verifique < seu nome do aplicativo-> público** acesso público geral tooenable usando a autenticação do Facebook.

## <a name="secrets"></a>Aplicativo do Facebook adicionar informações tooyour
1. Em Olá [portal do Azure], navegar tooyour aplicativo. Clique em **Configurações** > **Autenticação/Autorização** e verifique se a **Autenticação do Serviço de Aplicativo** está **Ativada**.
2. Clique em **Facebook**, cole em valores de ID do aplicativo e o segredo do aplicativo hello que você obteve anteriormente, se desejar habilitar escopos necessitados para seu aplicativo e clique em **Okey**.
   
    ![][0]
   
    Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs. Você deve autorizar os usuários no código do aplicativo.
3. (Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Facebook, definir **tootake de ação quando a solicitação não está autenticada** muito**Facebook**. Isso requer que todas as solicitações autenticadas e todas as solicitações não autenticadas são redirecionada tooFacebook para autenticação.
4. Ao concluir a configuração de autenticação, clique em **Salvar**.

Agora você está pronto toouse Facebook para autenticação em seu aplicativo.

## <a name="related-content"> </a>Conteúdo relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[os desenvolvedores do Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portal do Azure]: https://portal.azure.com/
