---
title: "Tutorial: integração do Azure Active Directory com o SCC LifeCycle | Microsoft Docs"
description: "Saiba como toouse SCC LifeCycle com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Tutorial: Integração do Active Directory do Azure com o SCC LifeCycle
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e SCC LifeCycle.  

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma assinatura do SCC LifeCycle com SSO (logon único) habilitado

Após concluir este tutorial, Olá AD do Azure usuários atribuídos tooSCC ciclo de vida será toosingle capaz de entrada para o aplicativo hello no site da empresa do SCC LifeCycle (serviço iniciado pelo provedor logon) ou usando Olá [Introdução Painel de acesso de toohello](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando Olá integração de aplicativos para SCC LifeCycle
2. Configuração do SSO (logon único)
3. Configurando o provisionamento de usuários
4. Atribuindo usuários

![Cenário](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Cenário")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Habilitar Olá integração de aplicativos para SCC LifeCycle
Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para SCC LifeCycle.

**integração do aplicativo hello tooenable para SCC LifeCycle, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
    ![Adicionar aplicativo](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Adicionar um aplicativo da galeria](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **SCC LifeCycle**.
   
    ![Galeria de Aplicativos](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galeria de Aplicativos")
7. No painel de resultados de saudação, selecione **SCC LifeCycle**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooSCC ciclo de vida com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **SCC LifeCycle** página de integração de aplicativos, clique em **configurar logon único** tooopen hello * * configurar logon único * * caixa de diálogo.
   
    ![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurar Logon Único")
2. Em Olá **como você gostaria usuários toosign no ciclo de vida de tooSCC** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurar Logon Único")
3. Em Olá **configurar URL do aplicativo** página Olá **URL de logon** caixa de texto, digite a URL de saudação usado pelo seu toosign usuários em tooyour aplicativo SCC LifeCycle usando saudação padrão a seguir "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*"e, em seguida, clique em **próximo**.
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurar URL do Aplicativo")
4. Em Olá **configurar logon único no SCC LifeCycle** , clique em **baixar metadados**e, em seguida, salve o arquivo de metadados localmente no seu computador.
   
   ![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurar Logon Único")
5. Encaminhe esse arquivo de metadados tooSCC a equipe de suporte do ciclo de vida.
   
   >[!NOTE]
   >O logon único tem toobe habilitado por Olá, equipe de suporte do SCC LifeCycle.
   > 
   > 

6. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
   
    ![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurar Logon Único")
   
## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário

Ordem tooenable AD do Azure usuários toolog no SCC LifeCycle, eles devem ser provisionados no SCC LifeCycle. Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooSCC ciclo de vida.

Quando um toolog de tentativas de usuário atribuído no SCC LifeCycle, uma conta do SCC LifeCycle é criada automaticamente, se necessário.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros SCC LifeCycle usuário conta ou APIs fornecidas pelo SCC LifeCycle tooprovision contas de usuário do AAD.
> 
> 

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooSCC ciclo de vida, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em hello * * SCC LifeCycle * * página de integração de aplicativos, clique em **atribuir usuários**.
   
    ![Atribuir Usuários](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Atribuir Usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
    ![Sim](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

