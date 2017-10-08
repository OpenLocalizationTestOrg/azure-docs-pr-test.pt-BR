---
title: "Tutorial: Integração do Azure Active Directory ao Clarizen | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Clarizen."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Tutorial: integração do Active Directory do Azure ao Clarizen

Neste tutorial, você aprenderá como toointegrate do Azure Active Directory (AD do Azure) com o Clarizen. Isso proporciona integração Olá seguintes benefícios:

- Você pode controlar, no AD do Azure, que tem acesso tooClarizen.
- Você pode habilitar o toobe de usuários conectado automaticamente tooClarizen (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central, Olá portal do Azure.

cenário de saudação neste tutorial consiste em duas tarefas principais:

1. Adicione Clarizen da Galeria de saudação.
2. Configurar e testar logon único do Azure AD.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com o Clarizen, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura de Clarizen está habilitada para logon único

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Teste o logon único do Azure AD em um ambiente de teste. Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de teste do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Adicionar Clarizen da Galeria de saudação
integração de saudação do tooconfigure do Clarizen no AD do Azure, adicione Clarizen da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

1. Em Olá [portal do Azure](https://portal.azure.com), no painel esquerdo de hello, clique Olá **Active Directory do Azure** ícone.

    ![Ícone do Azure Active Directory][1]

2. Clique em **Aplicativos empresariais**. Em seguida, clique em **Todos os aplicativos**.

    ![Clicar em "Aplicativos corporativos" e em "Todos os aplicativos"][2]

3. Clique em Olá **adicionar** botão na parte superior de Olá Olá da caixa de diálogo.

    ![botão de "Adicionar" Hello][3]

4. Na caixa de pesquisa hello, digite **Clarizen**.

    ![Digitar "Clarizen" na caixa de pesquisa de saudação](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. No painel de resultados de saudação, selecione **Clarizen**e, em seguida, clique em **adicionar** aplicativo hello de tooadd.

    ![Selecionando Clarizen no painel de resultados de saudação](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Em Olá seções a seguir, configurar e testar o logon único do AD do Azure com o Clarizen com base no usuário de teste Olá Britta Simon.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Clarizen é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Clarizen precisa toobe estabelecida. Estabelecer essa relação de link atribuindo o valor de saudação do **nome de usuário** no AD do Azure como valor de saudação do **Username** no Clarizen.

tooconfigure e teste de logon único do AD do Azure com o Clarizen, Olá completa blocos de construção a seguir:

1. **[Configurar o logon único do AD do Azure](#configure-azure-ad-single-sign-on)**  tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  tootest logon único do AD do Azure com Britta Simon.
3. **[Criar um usuário de teste do Clarizen](#create-a-clarizen-test-user)**  toohave um equivalente do Britta Simon no Clarizen é a representação toohello vinculado do Azure AD dela.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD
Habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Clarizen.

1. Em Olá portal do Azure, Olá **Clarizen** página de integração de aplicativos, clique em **o logon único**.

    ![Clicar em "Logon único"][4]

2. Em Olá **o logon único** caixa de diálogo para **modo**, selecione **baseado no SAML logon** tooenable-logon único.

    ![Selecionar "Logon único baseado em SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. Em Olá **Clarizen domínio e URLs** , execute Olá etapas a seguir:

    ![Caixas de URL de resposta e o identificador](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. Em Olá **identificador** caixa, o valor do tipo hello como: **Clarizen**

    b. Em Olá **URL de resposta** , digite uma URL usando o saudação padrão a seguir: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Eles não são valores reais de saudação. Você tem toouse Olá real identificador e URL de resposta. Aqui, sugerimos que você use o valor exclusivo de saudação de uma cadeia de caracteres como Olá identificador. tooget Olá valores reais, Olá contato [equipe de suporte do Clarizen](https://success.clarizen.com/hc/en-us/requests/new).

4. Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.

    ![Clicar em "Criar novo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione uma data de expiração. Em seguida, clique em **Salvar**.

    ![Selecionar e salvar uma data de expiração](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado**e, em seguida, clique em **salvar**.

    ![Marcar Olá a caixa de seleção para tornar o novo certificado de saudação ativo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. Em Olá **certificado de substituição** caixa de diálogo, clique em **Okey**.

    ![Clicar em "Okey" tooconfirm que você deseja toomake Olá certificado active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Clique em download de saudação toostart "Certificate (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. Em Olá **Clarizen configuração** seção, clique em **configurar Clarizen** tooopen Olá **configurar o logon** janela.

    ![Clicar em "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Janela "Configurar o logon", incluindo URLs e arquivos](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. Em uma janela de navegador web diferente, entre no site da empresa Clarizen tooyour como um administrador.

11. Clique no nome de usuário e em **Configurações**.

    ![Clicar em "Configurações" em seu nome de usuário](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Configurações")

12. Clique em Olá **configurações globais** guia. Em seguida, Avançar muito**autenticação federada**, clique em **editar**.

    ![Guia "Configurações Globais"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Configurações Globais")

13. Em Olá **autenticação federada** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![Caixa de diálogo "Autenticação Federada"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Autenticação Federada")

    a. Selecione **Habilitar Autenticação Federada**.

    b. Clique em **carregar** tooupload seu certificado baixado.

    c. Em Olá **URL de entrada** , digite o valor de saudação do **Single Sign-On URL do serviço SAML** da janela de configuração de aplicativo de saudação do AD do Azure.

    d. Em Olá **URL de logout** , digite o valor de saudação do **URL de logout** da janela de configuração de aplicativo de saudação do AD do Azure.

    e. Selecione **Usar POST**.

    f. Clique em **Salvar**.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
No portal do Azure de Olá, crie um usuário de teste chamado Britta Simon.

![Nome e endereço de email do usuário de teste de saudação do AD do Azure][100]

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** ícone.

    ![Ícone do Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Clique em **usuários e grupos**e, em seguida, clique em **todos os usuários** toodisplay lista de saudação de usuários.

    ![Clicar em "Usuários e grupos" e "Todos os usuários"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Na parte superior de Olá Olá da caixa de diálogo, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.

    ![botão de "Adicionar" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![Caixa de diálogo "Usuário" com o nome, p endereço de email e a senha preenchidos](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de endereço de email do tipo hello de saudação conta Britta Simon.

    c. Selecione **Mostrar senha** e anote o valor de saudação do **senha**.

    d. Clique em **Criar**.

### <a name="create-a-clarizen-test-user"></a>Criar um usuário de teste do Clarizen
tooenable a toosign de usuários do AD do Azure no tooClarizen, você deverá provisionar contas de usuário. No caso de saudação do Clarizen, o provisionamento é uma tarefa manual.

1. Entre no tooyour Clarizen site da empresa como um administrador.

2. Clique em **Pessoas**.

    ![Clicar em "Pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "Pessoas")

3. Clique em **Convidar Usuário**.

    ![Botão "Convidar Usuário"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Convidar Usuários")

4. Em Olá **convidar pessoas** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![Caixa de diálogo "Convidar Pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Convidar Pessoas")

    a. Em Olá **Email** caixa de endereço de email do tipo hello de saudação conta Britta Simon.

    b. Clique em **Convidar**.

    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Habilite Britta Simon toouse logon único do Azure, concedendo tooClarizen seu acesso.

![Usuário de teste atribuído][200]

1. No portal do Azure de Olá, abrir modo de exibição de aplicativos de saudação, toohello directory modo de navegação, clique em **aplicativos empresariais**e, em seguida, clique em **todos os aplicativos**.

    ![Clicar em "Aplicativos corporativos" e em "Todos os aplicativos"][201]

2. Na lista de aplicativos hello, selecione **Clarizen**.

    ![Selecionando Clarizen na lista de saudação](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. No painel esquerdo do hello, clique em **usuários e grupos**.

    ![Clicar em “Usuário e grupos”][202]

4. Clique em Olá **adicionar** botão. Em seguida, no hello **Adicionar atribuição** caixa de diálogo, selecione **usuários e grupos**.

    ![botão de "Adicionar" Hello e caixa de diálogo "Adicionar atribuição" hello][203]

5. Em Olá **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de saudação de usuários.

6. Em Olá **usuários e grupos** caixa de diálogo, clique em Olá **selecione** botão.

7. Em Olá **Adicionar atribuição** caixa de diálogo, clique em Olá **atribuir** botão.

### <a name="test-single-sign-on"></a>Testar logon único
Teste sua configuração do Azure AD único logon usando Olá painel de acesso.

Quando você clica em bloco Clarizen Olá Olá painel de acesso, você deve ser conectado automaticamente tooyour aplicativo Clarizen.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
