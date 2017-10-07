---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Tutorial: Integração do Azure Active Directory com o Salesforce

Neste tutorial, você aprenderá como toointegrate Salesforce com o Azure Active Directory (AD do Azure).

Integrando o Salesforce com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSalesforce
- Você pode habilitar seu usuários tooautomatically get conectado tooSalesforce (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com a equipe de vendas, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Salesforce com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando a equipe de vendas da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-salesforce-from-hello-gallery"></a>Adicionando a equipe de vendas da Galeria de saudação
integração de saudação tooconfigure da equipe de vendas no AD do Azure, você precisa tooadd Salesforce da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Salesforce da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Salesforce**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. No painel de resultados de saudação, selecione **Salesforce**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Salesforce, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Salesforce é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na equipe de vendas precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Salesforce.

tooconfigure e teste de logon único do AD do Azure com a equipe de vendas, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Salesforce](#creating-a-salesforce-test-user)**  -toohave um equivalente do Britta Simon no Salesforce é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo com a equipe de vendas.

**tooconfigure AD do Azure-logon único com o Salesforce, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Salesforce** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Em Olá **URLs e domínio do Salesforce** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir: 
   * Conta empresarial: `https://<subdomain>.my.salesforce.com`
   * Conta de desenvolvedor: `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Esses valores não são Olá real. Atualize esses valores com URL de logon real hello. Entre em contato com [equipe de suporte da equipe de vendas de cliente](https://help.salesforce.com/support) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Em Olá **Salesforce configuração** seção, clique em **configurar Salesforce** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.** 

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Abra uma nova guia no seu navegador e faça logon tooyour conta de administrador do Salesforce.

8.  Em Olá **administrador** painel de navegação, clique em **controles de segurança** tooexpand Olá relacionadas a seção. Em seguida, clique em **Configurações de Logon Único**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  Em Olá **configurações de logon único** , clique em Olá **editar** botão.
    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Se você não é possível tooenable Single Sign-On configurações para sua conta do Salesforce, talvez seja necessário toocontact [equipe de suporte da equipe de vendas de cliente](https://help.salesforce.com/support). 

10. Selecione **SAML Habilitado** e, em seguida, clique em **Salvar**.

      ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. tooconfigure seu SAML único logon configurações, clique em **novo**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. Em Olá **Single Sign-On Editar configuração de SAML** página, faça Olá configurações a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Para Olá **nome** , digite um nome amigável para essa configuração. Fornecer um valor para **nome** preencher automaticamente Olá **nome da API** caixa de texto.

    b. Colar **ID da entidade Small** valor em Olá **emissor** campo na equipe de vendas.

    c. Em Olá **caixa de texto de Id de entidade**, digite seu nome de domínio do Salesforce usando saudação padrão a seguir:
      
      * Conta empresarial: `https://<subdomain>.my.salesforce.com`
      * Conta de desenvolvedor: `https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Clique em **procurar** ou **Escolher arquivo** tooopen Olá **tooUpload Escolher arquivo** caixa de diálogo, selecione seu certificado Salesforce e, em seguida, clique em **abrir**certificado de saudação tooupload.

    e. Para **Tipo de Identidade do SAML**, selecione **A declaração contém o nome de usuário salesforce.com do Usuário**.

    f. Para **local da identidade do SAML**, selecione **identidade está no elemento NameIdentifier Olá Olá declaração do assunto**

    g. Colar **o URL de serviço de logon único** em Olá **URL de logon do provedor de identidade** campo na equipe de vendas.
    
    h. Para **Associação de Solicitação Iniciada do Provedor de Serviço**, selecione **Redirecionamento HTTP**.
    
    i. Por fim, clique em **salvar** tooapply seu SAML único-configurações de logon.

13. No painel de navegação esquerdo Olá no Salesforce, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Role para baixo toohello **configuração de autenticação** seção e, em seguida, clique em Olá **editar** botão.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. Em Olá **serviço de autenticação** seção, selecione o nome amigável de saudação da sua configuração de SSO do SAML e, em seguida, clique em **salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Se mais de um serviço de autenticação for selecionado, os usuários são solicitado tooselect qual serviço de autenticação como toosign ao iniciar o ambiente de equipe de vendas tooyour de logon único. Se você não quiser toohappen, você deve **Deixe todos os outros serviços de autenticação desmarcada**.
<CE>    
> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No painel de navegação esquerdo Olá Olá **portal do Azure**, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-salesforce-test-user"></a>Criar um usuário de teste do Salesforce

Nesta seção, é criado um usuário denominado Brenda Fernandes no Salesforce. O Salesforce dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.
Não há itens de ação para você nesta seção. Se um usuário ainda não existir na equipe de vendas, um novo será criado quando você tenta tooaccess Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSalesforce.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSalesforce, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Salesforce**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

tootest seu único-configurações de logon, abra Olá painel de acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), faça logon na conta de teste hello e clique em **Salesforce**.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

