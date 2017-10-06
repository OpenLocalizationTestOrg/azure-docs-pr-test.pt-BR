---
title: "Tutorial: integração do Azure Active Directory ao UserEcho | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a>Tutorial: Integração do Active Directory do Azure com o UserEcho

Neste tutorial, você aprenderá como toointegrate UserEcho com o Azure Active Directory (AD do Azure).

Integrando UserEcho com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooUserEcho
- Você pode habilitar seu usuários tooautomatically get conectado tooUserEcho (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com UserEcho, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do UserEcho habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando UserEcho da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-userecho-from-hello-gallery"></a>Adicionando UserEcho da Galeria de saudação
integração de saudação tooconfigure de UserEcho no AD do Azure, você precisa tooadd UserEcho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd UserEcho da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **UserEcho**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. No painel de resultados de saudação, selecione **UserEcho**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o UserEcho com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em UserEcho é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em UserEcho precisa toobe estabelecida.

UserEcho, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com UserEcho, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste UserEcho](#creating-a-userecho-test-user)**  -toohave um equivalente do Britta Simon em UserEcho é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo UserEcho.

**tooconfigure AD do Azure-logon único com UserEcho, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **UserEcho** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. Em Olá **UserEcho domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.userecho.com/`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.userecho.com/saml/metadata/`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente UserEcho](https://feedback.userecho.com/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. Em Olá **UserEcho configuração** seção, clique em **configurar UserEcho** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. Em outra janela do navegador, entre no site da empresa UserEcho tooyour como um administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em seu menu de saudação de tooexpand de nome de usuário e, em seguida, clique em **instalação**.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. Clique em **Integrações**.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. Clique em **site** e em **Logon único (SAML2)**.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. Em Olá **(SAML) de logon único** página, execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    a. Para **Habilitado para SAML**, selecione **Sim**.
    
    b. Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL SSO SAML** caixa de texto.
    
    c. Colar **URL de logout**, que você copiou de saudação portal do Azure em hello **logoout remoto URL** caixa de texto.
    
    d. Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **certificado x. 509** caixa de texto.
    
    e. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-userecho-test-user"></a>Criando um usuário de teste do UserEcho

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no UserEcho.

**toocreate um usuário chamado Britta Simon no UserEcho, execute Olá etapas a seguir:**

1. Site de empresa de UserEcho tooyour logon como administrador.

2. Na barra de ferramentas de saudação na parte superior do hello, clique em seu menu de saudação de tooexpand de nome de usuário e, em seguida, clique em **instalação**.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. Clique em **usuários**, Olá tooexpand **usuários** seção.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. Clique em **Usuários**.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. Clique em **Convidar um novo usuário**.
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. Em Olá **convidar um novo usuário** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    a. Em Olá **nome** caixa de texto, nome de usuário, Olá como Britta Simon tipo.
    
    b.  Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.
    
    c. Clique em **Convidar**.

Um convite é enviado tooBritta, que permite que seu toostart usando UserEcho. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooUserEcho.

![Atribuir usuário][200] 

**tooassign Britta Simon tooUserEcho, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **UserEcho**.

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.  

Quando você clica em bloco UserEcho Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour UserEcho aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

