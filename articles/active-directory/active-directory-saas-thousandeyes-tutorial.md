---
title: "Tutorial: Integração do Azure Active Directory ao ThousandEyes | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Tutorial: Integração do Active Directory do Azure ao ThousandEyes

Neste tutorial, você aprenderá como toointegrate ThousandEyes com o Azure Active Directory (AD do Azure).

Integrando ThousandEyes com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooThousandEyes
- Você pode habilitar seus usuários tooautomatically get conectado tooThousandEyes (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com ThousandEyes, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do ThousandEyes habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ThousandEyes da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-thousandeyes-from-hello-gallery"></a>Adicionando ThousandEyes da Galeria de saudação
integração de saudação tooconfigure do ThousandEyes no AD do Azure, você precisa tooadd ThousandEyes da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ThousandEyes da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **ThousandEyes**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. No painel de resultados de saudação, selecione **ThousandEyes**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o ThousandEyes, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ThousandEyes é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ThousandEyes precisa toobe estabelecida.

No ThousandEyes, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com ThousandEyes, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave um equivalente do Britta Simon no ThousandEyes é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ThousandEyes.

**tooconfigure AD do Azure-logon único com ThousandEyes, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **ThousandEyes** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. Em Olá **ThousandEyes domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL como:`https://app.thousandeyes.com/login/sso`

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. Em Olá **ThousandEyes configuração** seção, clique em **configurar ThousandEyes** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. Em uma janela de navegador web diferente, logon tooyour **ThousandEyes** site da empresa como um administrador.

8. No menu de saudação na parte superior de saudação, clique em **configurações**.
   
    ![Configurações](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Configurações")

9. Clique em **Conta**
   
    ![Conta](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Conta")

10. Clique em Olá **segurança & autenticação** guia.
   
    ![Segurança e autenticação](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Segurança e autenticação")

11. Em Olá **instalação Single Sign-On** , execute Olá etapas a seguir:
   
    ![Configurar o logon único](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurar o logon único")
  
    a. Selecione **Habilitar Logon Único**.
  
    b. Na caixa de texto **URL de Página de Logon**, cole a **URL do Serviço de Logon Único SAML** copiada do Portal do Azure.
  
    c. Na caixa de texto **URL de Página de Logoff**, cole a **URL de Saída** copiada do Portal do Azure.
  
    d. Na caixa de texto **Emissor do Provedor de Identidade**, cole a **ID de Entidade SAML** copiada do Portal do Azure.
  
    e. Em **certificado de verificação**, clique em **Escolher arquivo**e, em seguida, carregue o certificado de saudação que baixou do portal do Azure.
  
    f. Clique em **Salvar**.
 
> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-thousandeyes-test-user"></a>Criação de um usuário de teste do ThousandEyes

Ordem tooenable AD do Azure usuários toolog no ThousandEyes, eles devem ser provisionados no ThousandEyes.  
No caso de saudação de ThousandEyes, o provisionamento é uma tarefa manual.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros ThousandEyes usuário conta ou APIs fornecidas pelo ThousandEyes tooprovision Azure Active Directory as contas de usuário.

**tooprovision um tooThousandEyes de conta de usuário, execute Olá etapas a seguir:**

1. Faça logon em seu site de empresa ThousandEyes como um administrador.

2. Clique em **Configurações**.
   
    ![Configurações](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Configurações")

3. Clique em **Conta**.
   
    ![Conta](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Conta")

4. Clique em Olá **contas & usuários** guia.
   
    ![Contas e usuários](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Contas e usuários")

5. Em Olá **adicionar usuários e contas** , execute Olá etapas a seguir:
   
    ![Adicionar contas de usuário](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Adicionar contas de usuário")   
  
    a. Em **nome** caixa de texto Nome do tipo saudação do usuário como **Britta Simon**.

    b. Em **Email** caixa de texto, como o email de saudação do tipo de usuário  **brittasimon@contoso.com** .
   
    b. Clique em **tooAccount adicionar novo usuário**.
      
     >[!NOTE]
     >proprietário de conta do Active Directory do Azure Hello serão recebe um email incluindo um link tooconfirm e ativar conta hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooThousandEyes.

![Atribuir usuário][200] 

**tooassign Britta Simon tooThousandEyes, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ThousandEyes**.

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá ThousandEyes bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo ThousandEyes.

Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

