---
title: "Tutorial: Integração do Azure Active Directory com o Qualtrics | Microsoft Docs"
description: "Saiba como toouse Qualtrics com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Tutorial: Integração do Active Directory do Azure com o Qualtrics
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e Qualtrics.  

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma assinatura do Qualtrics com SSO (logon único) habilitado

Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooQualtrics será toosingle capaz de usar o logon no aplicativo hello em seu site da empresa do Qualtrics (serviço iniciado pelo provedor logon), ou por meio de saudação [toohello de Introdução Acessar o painel](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando a integração de aplicativos de saudação para Qualtrics
2. Configuração do SSO (logon único)
3. Configurando o provisionamento de usuários
4. Atribuindo usuários

![Cenário](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Cenário")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Habilitando a integração de aplicativos de saudação para Qualtrics
Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para Qualtrics.

**integração de aplicativos de saudação tooenable para Qualtrics, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
   ![Aplicativos](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
   ![Adicionar aplicativo](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
   ![Adicionar um aplicativo da galeria](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **Qualtrics**.
   
   ![Galeria de Aplicativos](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galeria de Aplicativos")
7. No painel de resultados de saudação, selecione **Qualtrics**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooQualtrics com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **Qualtrics** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurar Logon Único")
2. Em Olá **como você gostaria usuários toosign em tooQualtrics** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
   ![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurar Logon Único")
3. Em Olá **configurar URL do aplicativo** página Olá **Qualtrics URL de logon** caixa de texto, digite a URL (por exemplo: "*https://ssotest2ut1.qualtrics.com*") e, em seguida, clique em **Próxima**.
   
   ![Configurar URL do Aplicativo](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurar URL do Aplicativo")
4. Em Olá **configurar logon único no Qualtrics** , clique em **baixar metadados**e, em seguida, salve o arquivo de metadados de saudação em seu computador.
   
   ![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurar Logon Único")
5. Envie toohello de arquivo de metadados de saudação equipe de suporte do Qualtrics.
   
   >[!NOTE]
   >a configuração de SSO Olá tem toobe executada pelo Olá, equipe de suporte do Qualtrics. Você receberá uma notificação assim Olá configuração foi concluída.
   > 
   > 
6. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurar Logon Único")
   
## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário

Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooQualtrics. Quando um usuário atribuído tenta toolog no Qualtrics usando o painel de acesso hello, Qualtrics verifica se o usuário Olá existe.  

Se ainda não houver uma conta de usuário disponível, ela será automaticamente criada pelo Qualtrics.

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign tooQualtrics de usuários, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em Olá **Qualtrics** página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir Usuários](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Atribuir Usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

