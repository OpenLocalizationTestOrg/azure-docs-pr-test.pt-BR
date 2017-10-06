---
title: aaaPublish aplicativos com Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Publica a nuvem de toohello de aplicativos local com o Proxy de aplicativo do Azure AD em Olá portal do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-proxy-publish-azure-portal.md)
> * [Portal clássico do Azure](active-directory-application-proxy-publish.md)

Proxy de aplicativo do Azure AD (Active Directory) ajuda você a dar suporte a funcionários remotos publicando local aplicativos toobe acessado por meio de saudação à internet. Você pode publicar esses aplicativos por meio de saudação tooprovide portal do Azure acesso remoto seguro de fora da sua rede.

Este artigo orienta Olá etapas toopublish um aplicativo local com o Proxy de aplicativo. Depois de concluir este artigo, os usuários serão ser capaz de tooaccess seu aplicativo remotamente. E você estará pronto tooconfigure recursos adicionais para o aplicativo hello como um único logon informações personalizadas e os requisitos de segurança.

Se você estiver tooApplication novo Proxy, saiba mais sobre esse recurso com o artigo Olá [como tooprovide proteger o acesso remoto aplicativos locais tooon](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Publicar um aplicativo local para acesso remoto

Siga estas etapas toopublish seus aplicativos com Proxy de aplicativo. Se você já não tiver baixado e configurado um conector para sua organização, vá muito[Introdução ao Proxy de aplicativo e instalar o conector Olá](active-directory-application-proxy-enable.md) primeiro e, em seguida, publicar seu aplicativo.

> [!TIP]
> Se você estiver testando o Proxy de aplicativo para Olá primeira vez, escolha um aplicativo que está configurado para autenticação baseada em senha. Proxy de aplicativo oferece suporte a outros tipos de autenticação, mas aplicativos baseados em senha são tooget mais fácil de saudação para cima e em execução rapidamente. 

1. Entrar como um administrador no hello [portal do Azure](https://portal.azure.com/).
2. Selecione **Azure Active Directory** > **Aplicativos empresariais** > **Novo aplicativo**.

  ![Adicionar um aplicativo empresarial](./media/application-proxy-publish-azure-portal/add-app.png)

3. Selecione **Todos** e, em seguida, selecione **Aplicativo local**.  

  ![Adicionar seu próprio aplicativo](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Fornece Olá informações sobre o aplicativo a seguir:

   - **Nome**: nome de saudação do aplicativo de saudação que aparecerá no painel de acesso hello e em Olá portal do Azure. 

   - **URL interna**: Olá URL que você usar o aplicativo hello tooaccess na sua rede privada. Você pode fornecer um caminho específico em Olá toopublish de servidor de back-end, enquanto o restante de saudação do servidor de saudação foi publicada. Dessa forma, você pode publicar sites diferentes na Olá mesmo servidor que diferentes aplicativos e dê a cada um deles suas próprias regras de acesso e do nome.

     > [!TIP]
     > Se você publicar um caminho, certifique-se de que ele inclui todas as imagens necessárias hello, scripts e folhas de estilo para o seu aplicativo. Por exemplo, se seu aplicativo estiver em https://yourapp/app e usa imagens localizadas em https://yourapp/media, você deve publicar https://yourapp/ como caminho de saudação. Essa URL interna não tem página de aterrissagem Olá toobe que os usuários vejam. Para obter mais informações, consulte [Definir uma página inicial personalizada para aplicativos publicados](application-proxy-office365-app-launcher.md).

   - **URL externa**: Olá endereço que os usuários irão tooin ordem tooaccess Olá aplicativo de fora da sua rede. Se você não quiser o domínio de Proxy de aplicativo toouse saudação padrão, leia sobre [domínios personalizados no Proxy de aplicativo do Azure AD](active-directory-application-proxy-custom-domains.md).
   - **Pré-autenticação**: como Proxy de aplicativo verifica os usuários antes de fornecê-los acesso tooyour aplicativo. 

     - Active Directory do Azure: O Proxy de aplicativo redireciona toosign de usuários com o AD do Azure, que autentica suas permissões para o diretório de saudação e o aplicativo. É recomendável manter essa opção como padrão hello, você pode tirar proveito dos recursos de segurança do AD do Azure como acesso condicional e autenticação multifator.
     - Passagem: Os usuários não têm tooauthenticate no aplicativo do Active Directory do Azure tooaccess hello. Você ainda pode configurar os requisitos de autenticação em Olá back-end.
   - **Grupo**: conectores processo Olá acesso remoto tooyour aplicativo e ajudam a organizar aplicativos por região, rede ou finalidade e conectores de grupos de conector. Se você não tiver grupos de conector ainda criados, seu aplicativo recebe muito**padrão**.

   ![Configurar seu aplicativo](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Se necessário, defina configurações adicionais. Para a maioria dos aplicativos, você deve manter essas configurações em seus estados padrão. 
   - **Tempo limite do aplicativo de back-end**: Defina esse valor muito**longo** somente se seu aplicativo estiver lenta tooauthenticate e conecte-se. 
   - **Traduzir URLs nos cabeçalhos**: manter esse valor como **Sim** a menos que seu aplicativo exija o cabeçalho de host original Olá na solicitação de autenticação de saudação.
   - **Traduzir URLs no corpo do aplicativo**: manter esse valor como **não** , a menos que você tiver inserido no código HTML links tooother local aplicativos e não usar domínios personalizados. Para saber mais, consulte [Conversão de link com o Proxy de Aplicativo](application-proxy-link-translation.md).
   
   ![Configurar seu aplicativo](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Selecione **Adicionar**.


## <a name="add-a-test-user"></a>Adicionar um usuário de teste 

tootest que seu aplicativo foi publicado corretamente, adicione uma conta de usuário de teste. Verifique se essa conta já tem permissões tooaccess Olá aplicativo de dentro da rede corporativa hello.

1. Volta na folha de início rápido do hello, selecione **atribuir um usuário para teste**.

  ![Atribuir um usuário para teste](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Usuários de saudação e folha de grupos, selecione **adicionar**.

  ![Adicionar um usuário ou grupo](./media/application-proxy-publish-azure-portal/add-user.png)

3. Na folha de atribuição de adicionar hello, selecione **usuários e grupos** , em seguida, escolher conta Olá deseja tooadd. 
4. Selecione **Atribuir**.

## <a name="test-your-published-app"></a>Testar seu aplicativo publicado

No seu navegador, navegue toohello URL externa que você configurou durante a saudação publicar etapa. Você deve ver a tela de início do hello e ser capaz de toosign com conta de teste Olá você configurar.

![Testar seu aplicativo publicado](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Próximas etapas
- [Baixar conectores](active-directory-application-proxy-enable.md) e [criar grupos de conector](active-directory-application-proxy-connectors-azure-portal.md) toopublish aplicativos em redes separadas e locais.

- [Configurar o logon único](application-proxy-sso-azure-portal.md) para seu aplicativo recém-publicado
