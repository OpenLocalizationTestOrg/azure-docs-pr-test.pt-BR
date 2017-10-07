---
title: "Tutorial: integração do Azure Active Directory ao Origami | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a>Tutorial: Integração do Azure Active Directory ao Origami

Neste tutorial, você aprenderá como toointegrate Origami com o Azure Active Directory (AD do Azure).

Integrando Origami AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooOrigami
- Você pode habilitar seu usuários tooautomatically get conectado tooOrigami (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Origami, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Origami

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Origami da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-origami-from-hello-gallery"></a>Adicionando Origami da Galeria de saudação
integração de saudação tooconfigure de Origami no AD do Azure, você precisa tooadd Origami na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Origami da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Origami**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. No painel de resultados de saudação, selecione **Origami**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Origami, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Origami é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Origami precisa toobe estabelecida.

Origami, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Origami, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Origami](#creating-an-origami-test-user)**  -toohave um equivalente do Britta Simon em Origami é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Origami.

**tooconfigure AD do Azure-logon único com Origami, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Origami** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. Em Olá **Origami domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://live.origamirisk.com/origami/account/login?account=<companyname>`

    > [!NOTE] 
    > Olá valor não é real. Valor de saudação de atualização com hello URL de logon real. Entre em contato com [equipe de suporte de cliente Origami](https://wordpress.org/support/theme/origami) tooget valor de saudação. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. Em Olá **Origami configuração** seção, clique em **configurar Origami** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. Faça logon no toohello conta Origami com direitos de administrador.

8. No menu de saudação na parte superior de saudação, clique em **Admin**.
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. Na página de diálogo de logon único na instalação hello, execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    a. Selecione **Habilitar Logon Único**.

    b. Em Olá **entrar URL do provedor de identidade da página** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.

    c. Em Olá **URL da página de logout do provedor de identidade** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.

    d. Clique em **procurar** certificado de saudação tooupload que baixou do portal do Azure de saudação.

    e. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-origami-test-user"></a>Criando um usuário de teste do Origami

Nesta seção, você criará um usuário chamado Brenda Fernandes no Origami. 

1. Faça logon no toohello conta Origami com direitos de administrador.

2. No menu de saudação na parte superior de saudação, clique em **Admin**.
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. Em Olá **usuários e segurança** caixa de diálogo, clique em **usuários**.
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. Clique em **Adicionar Novo Usuário**.
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. Na caixa de diálogo de adicionar novo usuário hello, execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    a. Em Olá **nome de usuário** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .

    b. Em Olá **senha** caixa de texto, digite uma senha.

    c. Em Olá **Confirmar senha** caixa de texto, digite a senha de saudação novamente.

    d. Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.

    e. Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.

    f. Clique em **Salvar**.
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. Atribuir **funções de usuário** e **acesso para cliente** toohello usuário. 
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOrigami.

![Atribuir usuário][200] 

**tooassign Britta Simon tooOrigami, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Origami**.

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Origami Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Origami.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

