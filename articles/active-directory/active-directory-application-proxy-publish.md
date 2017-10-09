---
title: aaaPublish aplicativos com Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Publica a nuvem de toohello de aplicativos local com o Proxy de aplicativo do AD do Azure no portal clássico do hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-proxy-publish-azure-portal.md)
> * [Portal clássico do Azure](active-directory-application-proxy-publish.md)

Proxy de aplicativo do AD do Azure ajuda a dar suporte a funcionários remotos publicando local aplicativos toobe acessado por meio de saudação à internet. Neste ponto, você já deve ter [habilitada Proxy de aplicativo no portal clássico do Azure de saudação](active-directory-application-proxy-enable.md). Este artigo orienta Olá etapas toopublish os aplicativos em execução em sua rede local e fornecer acesso remoto seguro de fora da sua rede. Depois de concluir este artigo, você estará pronto tooconfigure aplicativo de hello com informações personalizadas ou requisitos de segurança.

> [!NOTE]
> Proxy de aplicativo é um recurso que está disponível somente se você atualizou toohello Premium ou edição Basic do Active Directory do Azure. Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md). Se você quiser toouse Proxy de aplicativo, você pode [publicar aplicativos no portal do Azure de saudação](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Publicar um aplicativo usando o Assistente de saudação
1. Entrar como um administrador no hello [portal clássico do Azure](https://manage.windowsazure.com/).
2. Vá tooActive diretório e selecione Olá diretório onde você habilitou o Proxy de aplicativo.
   
    ![Active Directory - ícone](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Clique em Olá **aplicativos** guia e, em seguida, clique em Olá **adicionar** botão Olá final da tela hello
   
    ![Adicionar aplicativo](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Selecione **Publicar um aplicativo que estará acessível fora de sua rede**.
   
    ![Publicar um aplicativo que estará acessível fora de sua rede](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Fornece Olá informações sobre o aplicativo a seguir:
   
   * **Nome**: nome de usuário amigável Olá para seu aplicativo. Ele deve ser exclusivo dentro no diretório.
   * **URL interna**: endereço Olá Olá conector de Proxy de aplicativo usa tooaccess Olá aplicativo dentro da sua rede privada. Você pode fornecer um caminho específico em Olá toopublish de servidor de back-end, enquanto o restante de saudação do servidor de saudação foi publicada. Dessa forma, você pode publicar sites diferentes na Olá mesmo servidor e dê a cada um deles suas próprias regras de acesso e do nome.
     
     > [!TIP]
     > Se você publicar um caminho, certifique-se de que ele inclui todas as imagens necessárias hello, scripts e folhas de estilo para o seu aplicativo. Por exemplo, se seu aplicativo estiver em https://yourapp/app e usa imagens localizadas em https://yourapp/media, você deve publicar https://yourapp/ como caminho de saudação.
     > 
     > 
   * **Método de pré-autenticação**: como Proxy de aplicativo verifica os usuários antes de fornecê-los acesso tooyour aplicativo. Escolha uma das opções de saudação do menu suspenso de saudação.
     
     * Active Directory do Azure: O Proxy de aplicativo redireciona toosign de usuários com o AD do Azure, que autentica suas permissões para o diretório de saudação e o aplicativo.
     * Passagem: Os usuários não tenham aplicativo do tooauthenticate tooaccess hello.
     
     ![Propriedades do aplicativo](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. Assistente de saudação toofinish, clique Olá marca de seleção na parte inferior da saudação da tela hello. aplicativo Hello agora está definido no AD do Azure.

## <a name="assign-users-and-groups-toohello-application"></a>Atribuir usuários e grupos toohello aplicativo
Em ordem para seus usuários tooaccess o aplicativo publicado, você precisa tooassign-los individualmente ou em grupos. (Lembre-se de tooassign muito por conta própria acessar.) Cada usuário que você atribui precisa de uma licença para o Azure Básico ou superior. Você pode atribuir licenças individualmente ou toogroups. Para obter mais informações, consulte [atribuindo usuários tooan aplicativo](active-directory-applications-guiding-developers-assigning-users.md). 

Para aplicativos que exigem pré-autenticação, atribuir a um usuário concede o aplicativo de hello toouse permissão. Para aplicativos que não exigem pré-autenticação, atribuir um usuário significa que o usuário Olá pode acessar aplicativo hello por meio do painel de acesso de saudação.

1. Após concluir assistente de Adicionar aplicativo hello, consulte Olá página do seu aplicativo de início rápido. toomanage quem tem acesso toohello aplicativo, selecione **usuários e grupos**.
   
    ![Início rápido do Proxy de Aplicativo para atribuir usuários - captura de tela](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Pesquise grupos específicos no diretório ou mostre todos os usuários. resultados da pesquisa toodisplay hello, clique em marca de seleção de saudação.
   
      ![Pesquisar grupos ou usuários - captura de tela](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Selecione cada usuário ou grupo que deseja tooassign toothis aplicativo e clique **atribuir**. Será solicitado tooconfirm esta ação.

> [!NOTE]
> Para aplicativos de autenticação integrada do Windows, você pode atribuir apenas usuários e grupos que são sincronizados do Active Directory local. Usuários que entram com uma conta da Microsoft e convidados não podem ser atribuídos para aplicativos publicados com o Proxy de Aplicativo do Azure Active Directory. Verifique se os usuários entrar com credenciais que fazem parte da saudação mesmo domínio que o aplicativo hello está sendo publicado.
> 
> 

## <a name="test-your-published-application"></a>Testar seu aplicativo publicado
Depois de publicar seu aplicativo, você pode testar-navegando toohello URL que você publicou. Verifique se você pode acessá-lo, se ele faz a renderização corretamente e se tudo funciona conforme o esperado. Se você tiver problemas ou receber uma mensagem de erro, tente Olá [guia de solução de problemas](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Configurar seu aplicativo
Você pode modificar os aplicativos publicados ou configurar opções avançadas na página Configurar de saudação. Nessa página, você pode personalizar o seu aplicativo, alterando nome hello ou carregar um logotipo. Você também pode gerenciar regras de acesso como Olá método de pré-autenticação ou autenticação multifator.

![Configuração avançada](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Depois de publicar aplicativos usando o Azure Active Directory Application Proxy, eles aparecem na lista de aplicativos Olá no AD do Azure e gerenciá-los lá.

Se você desabilitar os serviços de Proxy de aplicativo depois que você tenha publicado os aplicativos, aplicativos de saudação não são mais acessíveis de fora da sua rede privada. Os usuários ainda podem acessar Olá aplicativos locais como de costume.

tooview um aplicativo e certifique-se que ele está acessível, clique duas vezes no nome de saudação do aplicativo hello. Se Olá serviço Proxy de aplicativo está desabilitado e o aplicativo hello não está disponível, uma mensagem de aviso será exibida na parte superior de saudação da tela hello.

toodelete um aplicativo, selecione um aplicativo na lista de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas
* [Publicar aplicativos usando seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)
* [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
* [Habilitar o acesso condicional](active-directory-application-proxy-conditional-access.md)
* [Trabalho com aplicativos com reconhecimento de declaração](active-directory-application-proxy-claims-aware-apps.md)

Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)

