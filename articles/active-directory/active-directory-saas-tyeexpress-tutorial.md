---
title: "Tutorial: integração do Azure Active Directory ao T&E Express | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>Tutorial: integração do Azure Active Directory com o T&E Express

Neste tutorial, você aprenderá como toointegrate T & E Express com o Azure Active Directory (AD do Azure).

Integrando T & E Express com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha tooT acesso & E Express
- Você pode habilitar seus usuários tooautomatically get conectado tooT & E Express (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com T & E Express, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do T&E Express

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando T & E Express da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-te-express-from-hello-gallery"></a>Adicionando T & E Express da Galeria de saudação
integração de saudação tooconfigure de T & E Express no AD do Azure, você precisa tooadd T & E Express na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd T & E Express da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **T & E Express**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. No painel de resultados de saudação, selecione **T & E Express**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o T&E Express, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá T & E Express é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em T & E Express toobe necessidades estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em T & E Express.

tooconfigure e teste de logon único do AD do Azure com T & E Express, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste T & E Express](#creating-a-te-express-test-user)**  -toohave um equivalente do Britta Simon T & E Express que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo T & E Express.

**tooconfigure logon único do AD do Azure com T & E Express, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **T & E Express** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. Em Olá **T & E Express domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    a. Em Olá **identificador** texto, o valor do tipo hello como:`https://<domain>.tyeexpress.com`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação. Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação. Entre em contato com [equipe de suporte de T & E Express](http://www.tyeexpress.com/contacto.aspx) tooget esses valores.

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure logon único no **T & E Express** lado, logon toohello T & aplicativo express E sem SAML único logon usando credenciais de administrador.

9. Em Olá **Admin** guia, clique em **domínio SAML** página de configurações do tooOpen Olá SAML.

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. Selecione Olá **Activar(Activate)** opção **não** muito**SI(Yes)**. Em Olá **metadados do provedor de identidade** caixa de texto, colar Olá metadados XML que você tiver donwloaded do portal do Azure.

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Clique em Olá **Guardar(Save)** botão Configurações de saudação toosave. 


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-te-express-test-user"></a>Criar um usuário de teste do T&E Express

Em ordem tooenable AD do Azure usuários toolog em T & E Express, eles devem ser provisionados no T & E Express.  
No caso do T&E Express, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon tooyour T & E Express site da empresa como um administrador.

2. Na marca de administração, clique em página mestra a usuários tooopen Olá para os usuários.

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. Na home page do hello, clique em  **+**  tooadd usuários de saudação.

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Insira todos os detalhes de obrigatório Olá conforme solicitado no formulário hello e clique em Olá Salvar botão toosave Olá detalhes.

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure concedendo sua tooT acesso & E Express.

![Atribuir usuário][200] 

**tooassign tooT Britta Simon & E Express, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **T & E Express**.

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá T & E Express lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour T & Express E aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

