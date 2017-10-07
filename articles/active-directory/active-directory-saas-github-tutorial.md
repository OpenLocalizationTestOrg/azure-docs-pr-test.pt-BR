---
title: "Tutorial: Integração do Azure Active Directory ao GitHub | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Tutorial: Integração do Azure Active Directory ao GitHub

Neste tutorial, você aprenderá como toointegrate GitHub com o Azure Active Directory (AD do Azure).

Integração do GitHub com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooGitHub
- Você pode habilitar seu usuários tooautomatically get conectado tooGitHub (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com GitHub, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do GitHub habilitada para logon único


> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando GitHub da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-github-from-hello-gallery"></a>Adicionando GitHub da Galeria de saudação
integração de saudação tooconfigure do GitHub no AD do Azure, você precisa tooadd GitHub na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd GitHub da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **GitHub.com**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. No painel de resultados de saudação, selecione **GitHub**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o GitHub, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no GitHub é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no GitHub precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no GitHub.

tooconfigure e teste de logon único do AD do Azure com GitHub, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do GitHub](#creating-a-GitHub-test-user)**  -toohave um equivalente do Britta Simon no GitHub é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo do GitHub.

**tooconfigure AD do Azure-logon único com GitHub, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **GitHub** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. Em Olá **domínio GitHub e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. Em Olá **URL de logon** texto, o valor do tipo hello como:`https://github.com/orgs/<entity-id>/sso`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com URL de logon real hello e identificador. Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação. Vá tooGitHub Admin seção tooretrieve esses valores. 

4. Em Olá **atributos de usuário** seção, selecione **identificador de usuário** como user.mail.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**. Em seguida, clique no botão **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. Em Olá **GitHub configuração** seção, clique em **configurar o GitHub** tooopen **configurar o logon** janela.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. Em outra janela do navegador da Web, faça logon em seu site de organização do GitHub como administrador.

12. Navegue muito**configurações** e clique em **segurança**

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Verificar Olá **habilitar autenticação SAML** caixa, revelar os campos de Olá logon único na configuração. Em seguida, use Olá único logon URL valor tooupdate Olá única URL de logon na configuração do AD do Azure.

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Configure Olá campos a seguir:

    a. **URL de logon**: insira **SAML logon único na URL do serviço** de saudação **configurar o GitHub** seção no AD do Azure

    b. **Emissor**: insira **ID da entidade SAML** de saudação **configurar o GitHub** seção no AD do Azure

    c. **Certificado público**: Olá abrir baixado o certificado do Azure AD em um bloco de notas e copie Olá de conteúdo incluindo "Iniciar certificado" e "END"

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Clique em **configuração SAML do teste** tooconfirm que não há falhas de validação ou erros durante o SSO.

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Clique em **Salvar**

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 


### <a name="creating-a-github-test-user"></a>Criar um usuário de teste do GitHub

Em ordem tooenable AD do Azure usuários toolog no GitHub, eles devem ser provisionados no GitHub.  
No caso de saudação do GitHub, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon tooyour site do GitHub da empresa como um administrador.

2. Clique em **Pessoas**.

    ![Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Pessoas")

3. Clique em **Convidar membro**.

    ![Convidar Usuários](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Convidar Usuários")

4. Em Olá **convite membro** caixa de diálogo de página, execute Olá etapas a seguir:

    a. Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.

    ![Convidar Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Convidar Pessoas")
    
    b. Clique em **Enviar Convite**.

    ![Convidar Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Convidar Pessoas")

    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooGitHub seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooGitHub, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **GitHub.com**.

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco GitHub Olá Olá painel de acesso, você deve obter tooyour assinado no aplicativo do GitHub. Você vai ser logon como uma conta de organização mas toolog necessidade com sua conta pessoal.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
