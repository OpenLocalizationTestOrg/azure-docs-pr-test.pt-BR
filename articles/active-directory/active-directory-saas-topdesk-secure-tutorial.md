---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Secure | Microsoft Docs"
description: "Saiba como toouse TOPdesk - seguro com o Active Directory do Azure tooenable-logon único, o provisionamento automatizado e muito mais!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Tutorial: Integração do Active Directory do Azure ao TOPdesk - Secure
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e TOPdesk - seguro.  
cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma assinatura habilitada para logon único do TOPdesk - Secure

Depois de concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooTOPdesk - será seguro seja capaz de toosingle o logon no aplicativo hello no TOPdesk - seguro site da empresa (serviço iniciado pelo provedor logon) ou usando Olá [Introdução Painel de acesso de toohello](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando Olá integração de aplicativos para TOPdesk - seguro
2. Configurando o logon único
3. Configurando o provisionamento de usuários
4. Atribuindo usuários

![Cenário](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Cenário")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Habilitando Olá integração de aplicativos para TOPdesk - seguro
Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para TOPdesk - seguro.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>integração do aplicativo hello tooenable para TOPdesk - seguro, execute Olá etapas a seguir:
1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Aplicativos")

4. Clique em **adicionar** final Olá Olá página.
   
    ![Adicionar aplicativo](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Adicionar aplicativo")

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Adicionar um aplicativo da galeria](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Adicionar um aplicativo da galeria")

6. Em Olá **caixa de pesquisa**, tipo **TOPdesk - seguro**.
   
    ![Galeria de Aplicativos](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galeria de Aplicativos")

7. No painel de resultados de saudação, selecione **TOPdesk - seguro**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>Configurando o logon único
Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooTOPdesk - seguro com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.  
Configurar logon único para TOPdesk - seguro requer que você tooupload um arquivo de ícone do logotipo. arquivo de ícone tooget Olá, equipe de suporte do TOPdesk Olá contato.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure o logon único, execute Olá etapas a seguir:
1. Logon tooyour **TOPdesk - seguro** site da empresa como um administrador.
2. Em Olá **TOPdesk** menu, clique em **configurações**.
   
    ![Configurações](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configurações")

3. Clique em **Configurações de Logon**.
   
    ![Configurações de logon](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configurações de logon")

4. Expanda Olá **configurações de logon** menu e clique **geral**.
   
    ![Geral](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Geral")

5. Em Olá **seguro** seção Olá **logon SAML** configuração, execute Olá etapas a seguir:
   
    ![Configurações técnicas](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Configurações técnicas")
   
    a. Clique em **baixar** toodownload Olá arquivo de metadados público e, em seguida, salve-o localmente no seu computador.
   
    b. Abra o arquivo de metadados hello e localize Olá **AssertionConsumerService** nó.
    
    ![Serviço de Declaração do Consumidor](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Serviço de Declaração do Consumidor")
   
    c. Saudação de cópia **AssertionConsumerService** valor.  
      
    > [!NOTE]
    > Será necessário Olá o valor em Olá **configurar URL do aplicativo** seção mais adiante neste tutorial.
    > 
    > 

6. Em outra janela do navegador da Web, faça logon no **portal clássico do Azure** como administrador.

7. Em Olá **TOPdesk - seguro** página de integração de aplicativos, clique em **configurar logon único** tooopen hello * * configurar logon único * * caixa de diálogo.
   
    ![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurar Logon Único")

8. Em Olá **como seria como usuários toosign em tooTOPdesk - Secure** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurar Logon Único")

9. Em Olá **configurar URL do aplicativo** página, execute Olá etapas a seguir:
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurar URL do Aplicativo")
   
    a. Em Olá **TOPdesk - seguro URL de logon** caixa de texto, digite a URL Olá usada por seu usuários toosign em TOPdesk - seguro aplicativo (por exemplo: "*https://qssolutions.topdesk.net*").
   
    b. Em hello **TOPdesk – URL de resposta pública** textbox, colar Olá **TOPdesk - seguro URL de AssertionConsumerService** (por exemplo: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Clique em **Avançar**.

10. Em Olá **configurar logon único no TOPdesk - seguro** página, toodownload o arquivo de metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de saudação localmente no seu computador.
    
    ![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurar Logon Único")

11. toocreate um arquivo de certificado, execute Olá etapas a seguir:
    
    ![Certificado](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificado")
    
    a. Arquivo de metadados baixado Olá aberto.
    b. Expanda Olá **RoleDescriptor** nó que possui um **xsi: Type** de **fed: ApplicationServiceType**.
    c. Copie o valor Olá Olá **X509Certificate** nó.
    d. Salvar Olá copiado **X509Certificate** valor localmente no seu computador em um arquivo.

12. No TOPdesk - proteger o site da empresa, em Olá **TOPdesk** menu, clique em **configurações**.
    
    ![Configurações](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configurações")

13. Clique em **Configurações de Logon**.
    
    ![Configurações de logon](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configurações de logon")

14. Expanda Olá **configurações de logon** menu e clique **geral**.
    
    ![Geral](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Geral")

15. Em Olá **pública** seção, clique em **adicionar**.
    
    ![Adicionar](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Adicionar")

16. Em Olá **Assistente de configuração SAML** caixa de diálogo de página, execute Olá etapas a seguir:
    
    ![Assistente de configuração SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Assistente de configuração SAML")
    
    a. tooupload arquivo seus metadados baixado, em **metadados de Federação**, clique em **procurar**.

    b. tooupload arquivo seu certificado, em **certificado (RSA)**, clique em **procurar**.

    c. arquivo de logotipo Olá tooupload você obteve da equipe de suporte do TOPdesk hello, em **ícone do logotipo**, clique em **procurar**.

    d. Em Olá **atributo de nome de usuário** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. Em Olá **nome de exibição** caixa de texto, digite um nome para a sua configuração.

    f. Clique em **Salvar**.

17. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
    
    ![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurar Logon Único")

## <a name="configuring-user-provisioning"></a>Configurando o provisionamento de usuários
Em ordem toolog de usuários tooenable AD do Azure no TOPdesk - seguro, eles devem ser provisionados no TOPdesk - seguro.  
No caso de saudação do TOPdesk - seguro, o provisionamento é uma tarefa manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisionamento de usuário, execute Olá etapas a seguir:
1. Logon tooyour **TOPdesk - seguro** site da empresa como administrador.
2. No menu de saudação na parte superior de saudação, clique em **TOPdesk \> novo \> arquivos de suporte \> operador**.
   
    ![Operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operador")

3. Em Olá **novo operador** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Novo operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Novo operador")
   
    a. Clique em guia Geral hello.
   
    b. Em Olá **Sobrenome** caixa de texto de saudação **geral** seção, digite Olá sobrenome de uma conta válida do Active Directory do Azure você deseja tooprovision.
   
    c. Selecione um **Site** para conta Olá Olá **local** seção.
   
    d. Em Olá **nome de logon** caixa de texto de saudação **logon do TOPdesk** seção, digite um nome de logon para o usuário.
   
    e. Clique em **Salvar**.

> [!NOTE]
> Você pode usar qualquer outra TOPdesk - conta de usuário segura ferramentas de criação ou APIs fornecidas pelo TOPdesk - seguro tooprovision contas de usuário do AAD.
> 
> 

## <a name="assigning-users"></a>Atribuindo usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign usuários tooTOPdesk - seguro, execute Olá etapas a seguir:
1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em hello * * TOPdesk - seguro * * página de integração de aplicativos, clique em **atribuir usuários**.
   
    ![Atribuir Usuários](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Atribuir Usuários")

3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
    ![Sim](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

