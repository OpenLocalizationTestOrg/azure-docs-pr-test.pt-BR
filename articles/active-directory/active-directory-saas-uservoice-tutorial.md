---
title: "Tutorial: Integração do Azure Active Directory com o UserVoice | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Tutorial: Integração do Azure Active Directory com o UserVoice

Neste tutorial, você aprenderá como toointegrate UserVoice com o Azure Active Directory (AD do Azure).

Integrando o UserVoice com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooUserVoice.
- Você pode habilitar seu usuários tooautomatically get conectado tooUserVoice (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o UserVoice, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do UserVoice com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando UserVoice da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-uservoice-from-hello-gallery"></a>Adicionando UserVoice da Galeria de saudação
integração de saudação tooconfigure do UserVoice no AD do Azure, você precisa tooadd UserVoice da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd UserVoice da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **UserVoice**, selecione **UserVoice** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![UserVoice na lista de resultados de saudação](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o UserVoice, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no UserVoice é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no UserVoice precisa toobe estabelecida.

No UserVoice, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o UserVoice, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do UserVoice](#create-a-uservoice-test-user)**  -toohave um equivalente do Britta Simon no UserVoice é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do UserVoice.

**tooconfigure AD do Azure-logon único com o UserVoice, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **UserVoice** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. Em Olá **UserVoice domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de URLs e Domínio do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.UserVoice.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.UserVoice.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente do UserVoice](https://www.uservoice.com/) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.

    ![link de download de certificado Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. Em Olá **UserVoice configuração** seção, clique em **configurar UserVoice** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour UserVoice como um administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, selecione **portal da Web** menu hello.
   
    ![Seção Configurações no lado do aplicativo](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Configurações")

9. Em Olá **portal da Web** guia Olá **autenticação de usuário** seção, clique em **editar** tooopen Olá **Editar autenticação de usuário** caixa de diálogo página.
   
    ![Guia Portal da Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portal da Web")

10. Em Olá **Editar autenticação de usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Editar autenticação de usuário](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Editar autenticação de usuário")
   
    a. Clique em **SSO (Logon Único)**.
 
    b. Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **entrar remoto SSO** caixa de texto.

    c. Saudação de colar **URL de logout** valor que você copiou de saudação portal do Azure em hello **caixa de texto de saída remota de SSO**.
 
    d. Saudação de colar **impressão digital** valor, que você copiou do portal do Azure para o **impressão digital de certificado SHA1 atual** caixa de texto.
    
    e. Clique em **Salvar Configurações de Autenticação**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-uservoice-test-user"></a>Criar um usuário de teste do UserVoice

tooenable AD do Azure usuários toolog em tooUserVoice, eles devem ser provisionados no UserVoice. No caso de saudação do UserVoice, o provisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de usuário, execute Olá etapas a seguir:
1. Faça logon no tooyour **UserVoice** locatário.

2. Vá muito**configurações**.
   
    ![Configurações](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Configurações")

3. Clique em **Geral**.

4. Clique em **Agentes e permissões**.
   
    ![Agentes e permissões](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agentes e permissões")

5. Clique em **Adicionar administradores**.
   
    ![Adicionar administradores](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Adicionar administradores")

6. Em Olá **convidar administradores** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Convidar administradores](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Convidar administradores")
   
    a. Na caixa de texto de Emails Olá, digite o endereço de email de saudação da conta de Olá você deseja tooprovision e, em seguida, clique em **adicionar**.
   
    b. Clique em **Convidar**.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros UserVoice usuário conta ou APIs fornecidas pelo UserVoice tooprovision contas de usuário do AAD.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooUserVoice.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooUserVoice, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **UserVoice**.

    ![link do UserVoice Olá na lista de aplicativos Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco UserVoice Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour UserVoice aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

