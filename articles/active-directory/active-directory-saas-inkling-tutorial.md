---
title: "Tutorial: Integração do Azure Active Directory ao Inkling | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a>Tutorial: Integração do Azure Active Directory ao Inkling

Neste tutorial, você aprenderá como toointegrate Inkling com o Azure Active Directory (AD do Azure).

Integrando Inkling com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooInkling
- Você pode habilitar seu usuários tooautomatically get conectado tooInkling (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Inkling, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único no Inkling


> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Inkling da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-inkling-from-hello-gallery"></a>Adicionando Inkling da Galeria de saudação
integração de saudação tooconfigure de Inkling no AD do Azure, você precisa tooadd Inkling da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Inkling da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Inkling**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. No painel de resultados de saudação, selecione **Inkling**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Inkling, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Inkling é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Inkling precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Inkling.

teste logon único do AD do Azure com Inkling e tooconfigure, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Inkling](#creating-an-inkling-test-user)**  -toohave um equivalente do Britta Simon em Inkling é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Inkling.

**tooconfigure AD do Azure-logon único com Inkling, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **Inkling** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. Em Olá **Inkling domínio e URLs** , execute Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.inkling.com/saml/v2/metadata/<user-id>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.inkling.com/saml/v2/acs/<user-id>`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [a equipe de suporte Inkling](mailto:press@inkling.com) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**. Em seguida, clique no botão **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. tooget SSO configurado para o seu aplicativo, entre em contato com [a equipe de suporte Inkling](mailto:press@inkling.com) e fornecê-los com baixado **metadados**. 


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 



### <a name="creating-an-inkling-test-user"></a>Criando um usuário de teste do Inkling

Nesta seção, você cria um usuário chamado Brenda Fernandes no Inkling. Trabalhe com [a equipe de suporte Inkling](mailto:press@inkling.com) tooadd usuários de saudação na plataforma de Inkling hello.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooInkling seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooInkling, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Inkling**.

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Inkling Olá Olá painel de acesso, você deve obter o aplicativo de Inkling tooyour automaticamente conectado em.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png