---
title: "Tutorial: integração do Azure Active Directory ao Coupa | Microsoft Docs"
description: "Saiba como toouse Coupa com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Tutorial: integração do Active Directory do Azure ao Coupa
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e do Coupa.  
cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma assinatura habilitada para SSO (logon único) do Coupa

Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooCoupa será toosingle capaz de usar o logon no aplicativo hello usando Olá [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

* Habilitando a integração de aplicativos Olá para o Coupa
* Configurando o logon único
* Configurando o provisionamento de usuários
* Atribuindo usuários

![Cenário](./media/active-directory-saas-coupa-tutorial/IC791897.png "Cenário")

## <a name="enable-hello-application-integration-for-coupa"></a>Habilitar a integração de aplicativos Olá para o Coupa
Olá objetivo desta seção é toooutline como integração de aplicativos tooenable Olá para o Coupa.

**integração do aplicativo hello tooenable para o Coupa, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
   ![Aplicativos](./media/active-directory-saas-coupa-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
   ![Adicionar aplicativo](./media/active-directory-saas-coupa-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
   ![Adicionar um aplicativo da galeria](./media/active-directory-saas-coupa-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **Coupa**.
   
   ![Galeria de Aplicativos](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galeria de Aplicativos")
7. No painel de resultados de saudação, selecione **Coupa**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooCoupa com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.  

Configurar logon único para o Coupa exige que você tooretrieve um valor de impressão digital de um certificado. Se você não estiver familiarizado com esse procedimento, consulte [como tooretrieve o valor de impressão digital do certificado](http://youtu.be/YKQF266SAxI).

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Faça logon no tooyour site da empresa Coupa como administrador.
2. Vá muito**instalação \> controle de segurança**.
   
   ![Controles de Segurança](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de Segurança")
3. Clique em computador toodownload Olá Coupa metadados arquivo tooyour, **baixar e importar metadados de SP**.
   
   ![Metadados SP do Coupa](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadados SP do Coupa")
4. Em uma janela de navegador diferente, faça logon no toohello portal clássico do Azure.
5. Em Olá **Coupa** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurar Logon Único")
6. Em Olá **como você gostaria usuários toosign em tooCoupa** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
   ![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurar Logon Único")
7. Em Olá **configurar URL do aplicativo** página, execute Olá etapas a seguir:
   
   ![Configurar URL do Aplicativo](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurar URL do Aplicativo")   
   1. Em Olá **URL de logon** caixa de texto, digite a URL usada pelo seu toosign usuários em tooyour aplicativo Coupa (por exemplo: "*http://company.Coupa.com*").
   2. Abra o arquivo de metadados do Coupa baixado e copie Olá **índice/URL AssertionConsumerService**.
   3. Em Olá **URL de resposta do Coupa** caixa de texto, colar Olá **índice/URL AssertionConsumerService** valor.
   4. Clique em **Avançar**.
8. Em Olá **configurar logon único no Coupa** página, toodownload o arquivo de metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de saudação localmente no seu computador.
   
   ![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurar Logon Único")
9. No site da empresa Olá Coupa, vá muito**instalação \> controle de segurança**.
   
   ![Controles de Segurança](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de Segurança")
10. Em Olá **efetuar login usando credenciais de Coupa** , execute Olá etapas a seguir:  

   ![Logon usando as credenciais do Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Logon usando as credenciais do Coupa") 
   1. Selecione **Fazer logon usando o SAML**.
   2. Clique em **procurar** tooupload seu arquivo de metadados baixado ativa do Azure.
   3. Clique em **Salvar**.
11. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
    
   ![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurar Logon Único")
    
## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário

Ordem tooenable AD do Azure usuários toolog no Coupa, eles devem ser provisionados no Coupa.  

* No caso de saudação do Coupa, o provisionamento é uma tarefa manual.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Coupa** site da empresa como administrador.
2. No menu de saudação na parte superior de saudação, clique em **instalação**e, em seguida, clique em **usuários**.
   
   ![Usuários](./media/active-directory-saas-coupa-tutorial/IC791908.png "Usuários")
3. Clique em **Criar**.
   
   ![Criar Usuários](./media/active-directory-saas-coupa-tutorial/IC791909.png "Criar Usuários")
4. Em Olá **usuário criar** , execute Olá etapas a seguir:
   
   ![Detalhes do Usuário](./media/active-directory-saas-coupa-tutorial/IC791910.png "Detalhes do Usuário")
   
   1. Saudação de tipo **Login**, **nome**, **Sobrenome**, **ID de logon único**, **Email** atributos de um conta válida do Active Directory do Azure que você deseja tooprovision em Olá relacionados caixas de texto.
   2. Clique em **Criar**.   
   >[!NOTE]
   >proprietário de conta do Active Directory do Azure Olá receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa. 
   > 

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Coupa usuário conta ou APIs fornecidas pelo Coupa tooprovision contas de usuário do AAD. 
> 

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooCoupa, executar Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em hello * * Coupa * * página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir Usuários](./media/active-directory-saas-coupa-tutorial/IC791911.png "Atribuir Usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

