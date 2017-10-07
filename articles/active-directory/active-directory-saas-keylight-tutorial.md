---
title: "Tutorial: Integração do Azure Active Directory ao LockPath Keylight | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Tutorial: Integração do Azure Active Directory ao LockPath Keylight

Neste tutorial, você aprenderá como toointegrate LockPath Keylight com o Azure Active Directory (AD do Azure).

Integrando LockPath Keylight com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLockPath Keylight
- Você pode habilitar seu usuários tooautomatically get conectado tooLockPath Keylight (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do AD do Azure com LockPath Keylight de tooconfigure, é necessário Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do LockPath Keylight

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando LockPath Keylight da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Adicionando LockPath Keylight da Galeria de saudação
integração de saudação tooconfigure de LockPath Keylight no AD do Azure, você precisa tooadd LockPath Keylight na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd LockPath Keylight da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **LockPath Keylight**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. No painel de resultados de saudação, selecione **LockPath Keylight**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o LockPath Keylight, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LockPath Keylight é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em LockPath Keylight precisa toobe estabelecida.

LockPath Keylight, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com LockPath Keylight, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave um equivalente do Britta Simon em LockPath Keylight que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo LockPath Keylight.

**tooconfigure AD do Azure-logon único com LockPath Keylight, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **LockPath Keylight** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. Em Olá **LockPath Keylight domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.keylightgrc.com/`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.keylightgrc.com`

    c. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Entre em contato com [equipe de suporte do cliente de Keylight LockPath](https://www.lockpath.com/contact/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. Em Olá **LockPath Keylight configuração** seção, clique em **configurar LockPath Keylight** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable SSO no LockPath Keylight, execute Olá etapas a seguir:
   
    a. Logon tooyour LockPath Keylight conta como administrador.
    
    b. No menu de saudação na parte superior de saudação, clique em **pessoa**e selecione **Keylight instalação**.
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. Em treeview Olá Olá esquerda, clique em **SAML**.
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. Em Olá **configurações SAML** caixa de diálogo, clique em **editar**.
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/404.png) 

8. Em Olá **editar configurações de SAML** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Definir **autenticação SAML** muito**Active**.

    b. Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de logon do provedor de identidade** caixa de texto.

    c. Saudação de colar **URL do serviço de logon único** valor que você copiou de saudação portal do Azure em hello **URL de Logout do provedor de identidade** caixa de texto.

    d. Clique em **Escolher arquivo** tooselect sua LockPath Keylight baixado do certificado e, em seguida, clique em **abrir** certificado de saudação tooupload.

    e. Definir **local de Id de usuário SAML** muito**elemento NameIdentifier da declaração do assunto Olá**.
    
    f. Fornecer Olá **Keylight provedor** usando saudação padrão a seguir: **https://&lt;CompanyName&gt;. keylightgrc.com**.
    
    g. Definir **automática provisionar usuários** muito**Active**.

    h. Definir **tipo de conta de provisionamento automático** muito**usuário completo**.

    i. Defina **Provisionar função de segurança automaticamente** e selecione **Usuário Padrão com SAML**.
    
    j. Defina **Provisionar configuração de segurança automaticamente** e selecione **Configuração de Usuário Padrão**.
     
    k. Em Olá **atributo de Email** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. Em Olá **atributo de nome** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. Em Olá **atributo de Sobrenome** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Criando um usuário de teste do LockPath Keylight

Nesta seção, você cria um usuário chamado Brenda Fernandes no LockPath Keylight. O LockPath Keylight dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Um novo usuário é criado ao acessar LockPath Keylight se o usuário Olá ainda não existe. 

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do cliente de Keylight LockPath](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLockPath Keylight.

![Atribuir usuário][200] 

**tooassign tooLockPath Britta Simon Keylight, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **LockPath Keylight**.

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá LockPath Keylight lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour LockPath Keylight aplicativo. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

