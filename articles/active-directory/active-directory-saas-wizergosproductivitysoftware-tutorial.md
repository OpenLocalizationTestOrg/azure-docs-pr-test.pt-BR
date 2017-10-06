---
title: "Tutorial: integração do Azure Active Directory com o Wizergos Productivity Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Software de produtividade de Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Tutorial: Integração do Azure Active Directory com o Wizergos Productivity Software
Olá objetivo deste tutorial é tooshow você como toointegrate Wizergos Software de produtividade com o Azure Active Directory (AD do Azure).

Integração de Software de produtividade de Wizergos com o Azure AD oferece Olá benefícios a seguir:

* Você pode controlar no AD do Azure que tenha acesso tooWizergos Software de produtividade
* Você pode habilitar seus usuários tooautomatically get conectado tooWizergos Software de produtividade-logon único (SSO) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com o Software de produtividade de Wizergos, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Uma assinatura do Wizergos Productivity Software habilitada para SSO

>[!NOTE]
>Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção. 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable você tootest SSO do AD do Azure em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Software de produtividade de Wizergos da Galeria de saudação
2. Configurar e testar o SSO do Azure AD

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Adicionar Software de produtividade de Wizergos da Galeria de saudação
integração de saudação tooconfigure Wizergos de softwares de produtividade no AD do Azure, você precisa tooadd Wizergos Software de produtividade da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Wizergos Software de produtividade da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1]
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2]
4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4]
6. Na caixa de pesquisa hello, digite **Software de produtividade Wizergos**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. No painel de resultados de saudação, selecione **Software de produtividade Wizergos**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Selecionar aplicativo hello na Galeria de saudação](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configurar e testar SSO do Azure AD
Olá o objetivo desta seção é tooshow como tooconfigure e teste do Azure AD SSO com Software de produtividade Wizergos com base em um usuário de teste chamado "Britta Simon".

Para SSO toowork, o AD do Azure precisa tooknow é qual usuário de contraparte saudação do usuário do Software de produtividade Wizergos tooan no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Software de produtividade Wizergos precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Wizergos Software de produtividade.

tooconfigure e teste de logon único do AD do Azure com BynWizergos Softwareder de produtividade, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de Software de produtividade Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave um equivalente do Britta Simon em Software de produtividade de Wizergos é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-sso"></a>Configurar o SSO do Azure AD
Nesta seção, habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único no aplicativo Wizergos produtividade.

**tooconfigure logon único do AD do Azure com o Software de produtividade Wizergos, execute Olá etapas a seguir:**

1. No portal clássico hello, em Olá **Software de produtividade Wizergos** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**caixa de diálogo.
   
    ![Configurar Logon Único][6] 
2. Em Olá **como você gostaria usuários toosign no Software de produtividade de tooWizergos** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**:
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. Em Olá **definir configurações de aplicativo** página da caixa de diálogo, clique em **próximo**:
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. Em Olá **configurar logon único no Software de produtividade Wizergos** , clique em **Download certificado**e, em seguida, salve o arquivo de saudação em seu computador:
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. Em uma janela de navegador web diferente, locatário do Software de produtividade Wizergos tooyour logon como administrador.
6. No menu de hambúrguer hello, selecione **Admin**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. Na página de administração no menu à esquerda, selecione **AUTENTICAÇÃO** e clique em **Azure AD**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Executar Olá seguindo as etapas na **autenticação** seção.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Clique em **carregar** saudação do botão tooupload baixado o certificado do AD do Azure. 
  2. Em Olá **URL do emissor** caixa de texto colocar o valor de saudação de **URL do emissor** do Assistente de configuração de aplicativo do AD do Azure.
  3. Em Olá **URL de logon único** caixa de texto colocar o valor de saudação de **o URL de serviço de logon único** do Assistente de configuração de aplicativo do AD do Azure.
  4. Em Olá **URL de logout único** caixa de texto colocar o valor de saudação de **URL do serviço de logon único** do Assistente de configuração de aplicativo do AD do Azure.
  5. Clique no botão **Salvar** .
9. No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.
   
    ![Logon Único do AD do Azure][10]
10. Em Olá **único logon confirmação** , clique em **concluir**.  
    
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no portal clássico do hello chamado Britta Simon.

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. Em Tipo de Usuário, selecione Novo usuário na organização.
  2. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
  3. Clique em **Avançar**.
6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. Em Olá **nome** caixa de texto, tipo **Britta**.  
  2. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.
  3. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
  4. Em Olá **função** lista, selecione **usuário**.
  5. Clique em **Avançar**.
7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Anote o valor Olá Olá **nova senha**.
  2. Clique em **Concluído**.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Criar um usuário de teste do Wizergos Productivity Software
Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Wizergos Productivity Software. Trabalhe com a equipe de suporte de Software de produtividade Wizergos via [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd usuários de saudação na plataforma de Software de produtividade Wizergos hello.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenabling Britta Simon toouse Azure SSO concedendo seu Software de produtividade de tooWizergos de acesso.

  ![Atribuir usuário][200]

**tooassign Britta Simon tooWizergos Software de produtividade, execute Olá etapas a seguir:**

1. No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.
   
    ![Atribuir usuário][201]
2. Na lista de aplicativos hello, selecione **Software de produtividade Wizergos**.
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![Atribuir usuário][203]
4. Na lista de usuários hello, selecione **Britta Simon**.
5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a>Testar logon único
Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em um bloco de Software de produtividade Wizergos Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Software de produtividade de Wizergos.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
