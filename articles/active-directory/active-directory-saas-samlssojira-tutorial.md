---
title: "Tutorial: Integração do Azure Active Directory com o SSO do SAML para Jira da Resolution GmbH | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SSO do SAML para Jira resolução GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Tutorial: Integração do Azure Active Directory com o SSO do SAML para Jira da Resolution GmbH

Neste tutorial, você aprenderá como toointegrate SSO do SAML para Jira resolução GmbH com o Azure Active Directory (AD do Azure).

Integração de SSO do SAML para Jira resolução GmbH com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha tooSAML acesso SSO para Jira resolução GmbH
- Você pode habilitar seu usuários tooautomatically get conectado tooSAML SSO para Jira resolução GmbH (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o SSO do SAML para Jira resolução GmbH, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SSO do SAML para Jira da Resolution GmbH

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o SSO do SAML para Jira resolução GmbH da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a>Adicionando o SSO do SAML para Jira resolução GmbH da Galeria de saudação
tooconfigure Olá integração do SSO do SAML para Jira resolução GmbH no AD do Azure, você precisa tooadd SSO do SAML para Jira resolução GmbH na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SSO do SAML para Jira resolução GmbH da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **SSO do SAML para Jira resolução GmbH**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. No painel de resultados de saudação, selecione **SSO do SAML para Jira resolução GmbH**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o SSO de SAML para Jira da Resolution GmbH com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO do SAML para Jira resolução GmbH é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá no SSO do SAML para Jira resolução GmbH precisa toobe estabelecida.

SSO do SAML para Jira resolução GmbH, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e testar logon único do AD do Azure com o SSO do SAML Jira resolução GmbH, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um SSO do SAML para Jira pelo usuário de teste GmbH resolução](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave um equivalente do Britta Simon no SSO do SAML para Jira resolução GmbH é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu SSO do SAML para Jira resolução GmbH aplicativo.

**tooconfigure logon único do AD do Azure com o SSO do SAML para Jira resolução GmbH, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **SSO do SAML para Jira resolução GmbH** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. Em Olá **SSO do SAML para URLs e Jira resolução GmbH domínio** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`

4. Marque **Mostrar configurações de URL avançadas**. Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Entre em contato com [equipe de suporte do SSO do SAML para Jira resolução GmbH cliente](https://www.resolution.de/go/support) tooget esses valores. 

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. Em uma janela do navegador web diferente, faça logon no tooyour **SSO do SAML para Jira pelo portal de administração de GmbH resolução** como um administrador.

8. Passe o mouse sobre engrenagem e clique em Olá **complementos**.
    
    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. Você é redirecionado tooAdministrator página de acesso. Digite hello **senha** e clique em **confirmar** botão.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. Na seção da guia Complementos, clique em **Localizar novos complementos**. Pesquisa **SAML logon único (SSO) para JIRA** e clique em **instalar** tooinstall botão Olá novo plug-in SAML.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. instalação do plug-in de saudação será iniciado. Clique em **fechar**

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. Clique em **Gerenciar**.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Clique em **configurar** tooconfigure Olá novo plug-in.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. Em **configuração de plug-in de logon único do SAML** , clique em **Adicionar provedor de identidade adicional** botão tooconfigure configurações de saudação do provedor de identidade.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. Execute as seguintes etapas nesta página:

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. Adicionar **nome** da saudação (por exemplo, o AD do Azure) do provedor de identidade.
    
    b. Adicionar **descrição** da saudação (por exemplo, o AD do Azure) do provedor de identidade.

    c. Clique em **XML** e selecione hello **metadados** arquivo que você baixou do portal do Azure.

    d. Clique no botão **Carregar**.

    e. Ele lê Olá IdP metadados e preenche os campos de saudação conforme realçado na captura de tela de saudação.   

16. Clique em **salvar configurações** botão Configurações de saudação toosave.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>Criando um usuário de teste do SSO do SAML para Jira da Resolution GmbH

tooenable AD do Azure usuários toolog em tooSAML SSO para Jira resolução GmbH, eles devem ser provisionados no SSO do SAML para Jira resolução GmbH.  
No SSO do SAML para Jira da Resolution GmbH, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour SSO do SAML para Jira pelo site da empresa GmbH resolução como um administrador.

2. Passe o mouse sobre engrenagem e clique em Olá **gerenciamento de usuário**.

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. São redirecionadas tooAdministrator acesso página tooenter **senha** e clique em **confirmar** botão.

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. Na seção da guia **Gerenciamento de usuário**, clique em **criar usuário**.

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. Em Olá **"Criar novo usuário"** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. Em Olá **endereço de Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.

    b. Em Olá **nome completo** caixa de texto, nome completo do tipo de usuário hello como Britta Simon.

    c. Em Olá **Username** caixa de texto, como o email de saudação do tipo de usuário Brittasimon@contoso.com.

    d. Em Olá **senha** caixa de texto, digite a senha de saudação do usuário.

    e. Clique em **Criar usuário**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAML SSO para Jira resolução GmbH.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSAML SSO para Jira resolução GmbH, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SSO do SAML para Jira resolução GmbH**.

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá SSO do SAML para Jira pelo bloco GmbH resolução Olá painel de acesso, você deve obter automaticamente assinado em tooyour SSO do SAML Jira resolução GmbH aplicativo.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

