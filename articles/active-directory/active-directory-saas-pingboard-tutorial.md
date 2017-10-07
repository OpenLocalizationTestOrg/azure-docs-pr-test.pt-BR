---
title: "Tutorial: Integração do Azure Active Directory com o Pingboard | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Tutorial: Integração do Azure Active Directory ao Pingboard

Neste tutorial, você aprenderá como toointegrate Pingboard com o Azure Active Directory (AD do Azure).

Integrando Pingboard com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooPingboard
- Você pode habilitar seu usuários tooautomatically get conectado tooPingboard (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Pingboard, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Pingboard habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Pingboard da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-pingboard-from-hello-gallery"></a>Adicionando Pingboard da Galeria de saudação
integração de saudação tooconfigure de Pingboard no AD do Azure, você precisa tooadd Pingboard da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Pingboard da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Pingboard**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. No painel de resultados de saudação, selecione **Pingboard**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Pingboard, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Pingboard é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Pingboard precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Pingboard.

tooconfigure e teste de logon único do AD do Azure com Pingboard, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Pingboard](#creating-a-pingboard-test-user)**  -toohave um equivalente do Britta Simon em Pingboard é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Pingboard.

**tooconfigure AD do Azure-logon único com Pingboard, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **Pingboard** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. Em Olá **Pingboard domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. Em Olá **identificador** texto, o valor do tipo hello como:`http://<entity-id>.pingboard.com/sp`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação. Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação. Entre em contato com [equipe de suporte do cliente Pingboard](https://support.pingboard.com/) tooget esses valores. 

4. Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. Em Olá **URL de logon** texto, o valor do tipo hello como:`http://<sub-domain>.pingboard.com/sign_in`
     
5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure SSO no lado do Pingboard, abra uma nova janela do navegador e faça logon tooyour Pingboard conta. Você deve ser um tooset de admin Pingboard o logon único no.

8. No menu superior Olá selecione **aplicativos > integrações**

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  Em Olá **integrações** página, localize Olá **"Active Directory do Azure"** lado a lado e clique nele.

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. Em Olá modal que segue clique **"Configurar"**

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. Em Olá página a seguir, você observará que "integração do Azure de SSO está habilitada.". Abra Olá baixou o arquivo de Metadata XML em uma saudação de bloco de notas e cole o conteúdo no **metadados IDP**.

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. arquivo Hello será validado e, se tudo estiver correto, o logon único será habilitado

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-pingboard-test-user"></a>Criando um usuário de teste do Pingboard

Em ordem tooenable AD do Azure usuários toolog em Pingboard, eles devem ser provisionados no Pingboard.  
No caso de saudação de Pingboard, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon no tooyour Pingboard site da empresa como um administrador.

2. Clique no botão **"Adicionar Funcionário"** na página **Diretório**.

    ![Adicionar Funcionário](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. Em Olá **"Adicionar funcionários"** caixa de diálogo de página, execute Olá etapas a seguir.

    ![Convidar Pessoas](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. Em Olá **nome completo** caixa de texto, nome completo do tipo saudação do Britta Simon.

    b. Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.

    c. Em Olá **cargo** caixa de texto, tipo hello cargo do Britta Simon.

    d. Em Olá **local** suspenso, local selecione saudação do Britta Simon.
    
    e. Clique em **Adicionar**.   

4. Uma tela de confirmação aparecerá tooconfirm adição de saudação do usuário.
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooPingboard seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooPingboard, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Pingboard**.

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Pingboard Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Pingboard aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
