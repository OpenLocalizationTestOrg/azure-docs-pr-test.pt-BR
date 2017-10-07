---
title: "Tutorial: integração do Azure Active Directory ao PlanMyLeave | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Tutorial: integração do Azure Active Directory com o PlanMyLeave

Neste tutorial, você aprenderá como toointegrate PlanMyLeave com o Azure Active Directory (AD do Azure).

Integrando PlanMyLeave com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooPlanMyLeave
- Você pode habilitar seu usuários tooautomatically get conectado tooPlanMyLeave (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com PlanMyLeave, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do PlanMyLeave com logon único habilitado


> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando PlanMyLeave da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-planmyleave-from-hello-gallery"></a>Adicionando PlanMyLeave da Galeria de saudação
integração de saudação tooconfigure de PlanMyLeave no AD do Azure, você precisa tooadd PlanMyLeave da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd PlanMyLeave da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **PlanMyLeave**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. No painel de resultados de saudação, selecione **PlanMyLeave**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o PlanMyLeave, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em PlanMyLeave é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em PlanMyLeave precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em PlanMyLeave.

tooconfigure e teste de logon único do AD do Azure com PlanMyLeave, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave um equivalente do Britta Simon em PlanMyLeave é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo PlanMyLeave.

**tooconfigure AD do Azure-logon único com PlanMyLeave, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **PlanMyLeave** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** página da caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. Em Olá **PlanMyLeave domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate entrassem esses valores com hello real na URL e o identificador. Entre em contato com [PlanMyLeave a equipe de suporte](mailto:support@planmyleave.com) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**. Em seguida, clique no botão **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. Em Olá **PlanMyLeave configuração** seção, clique em **configurar PlanMyLeave** tooopen **configurar o logon** janela.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. Em outra janela do navegador da Web, faça logon no locatário do PlanMyLeave como administrador.

11. Vá muito**configuração do sistema**. Em seguida, na Olá **gerenciamento de segurança** seção clique **configurações da empresa SAML** .

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. Em Olá **configurações SAML** seção, clique em editor de ícone.

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. Em Olá **configurações de atualização de SAML** , execute Olá etapas a seguir:

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  Em Olá **URL de logon** caixa de texto, coloque o valor de saudação do **Single Sign-On URL do serviço SAML** da janela de configuração de aplicativo do AD do Azure.

    b.  Abra o arquivo de certificado baixado no bloco de notas, copie somente conteúdo de saudação entre hello---Begin Certificate--- e ---End certificate----lo em sua área de transferência e, em seguida, cole-o toohello **certificado** caixa de texto.

    c. Defina"**é habilitar**"muito"**Sim**".

    d. Clique em **Salvar**.



### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 



### <a name="creating-a-planmyleave-test-user"></a>Criação de um usuário de teste PlanMyLeave

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no PlanMyLeave. O PlanMyLeave dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Será criado um novo usuário durante uma tentativa tooaccess PlanMyLeave se ele ainda não existir.

> [!NOTE]
> Se você precisar toocreate um usuário manualmente, será necessário toocontact [a equipe de suporte PlanMyLeave](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooPlanMyLeave seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooPlanMyLeave, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **PlanMyLeave**.

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco PlanMyLeave Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour PlanMyLeave aplicativo.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png