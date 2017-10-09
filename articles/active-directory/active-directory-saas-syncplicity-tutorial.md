---
title: "Tutorial: Integração do Azure Active Directory com o Syncplicity | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>Tutorial: Integração do Active Directory do Azure com o Syncplicity

Neste tutorial, você aprenderá como toointegrate Syncplicity com o Azure Active Directory (AD do Azure).

Integrando o Syncplicity com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSyncplicity
- Você pode habilitar seu usuários tooautomatically get conectado tooSyncplicity (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Syncplicity, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Syncplicity

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Syncplicity da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-syncplicity-from-hello-gallery"></a>Adicionando Syncplicity da Galeria de saudação
integração de saudação tooconfigure do Syncplicity no AD do Azure, você precisa tooadd Syncplicity da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Syncplicity da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Syncplicity**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. No painel de resultados de saudação, selecione **Syncplicity**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Syncplicity, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Syncplicity é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Syncplicity precisa toobe estabelecida.

No Syncplicity, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Syncplicity, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Syncplicity](#creating-a-syncplicity-test-user)**  -toohave um equivalente do Britta Simon no Syncplicity que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Syncplicity.

**tooconfigure AD do Azure-logon único com o Syncplicity, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Syncplicity** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. Em Olá **Syncplicity domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.syncplicity.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente do Syncplicity](https://www.syncplicity.com/contact-us) tooget esses valores. 
 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. Em Olá **Syncplicity configuração** seção, clique em **configurar Syncplicity** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. Entrar tooyour **Syncplicity** locatário.

8. No menu de saudação na parte superior de saudação, clique em **admin**, selecione **configurações**e, em seguida, clique em **domínio personalizado e logon único**.
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. Em Olá **Single Sign-On (SSO)** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Logon Único \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    a. Em Olá **domínio personalizado** caixa de texto, nome de saudação do tipo do seu domínio.
  
    b. Selecione **Habilitado** como **Status do Logon Único**.

    c. Em Olá **Id da entidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.

    d. Em Olá **URL da página de entrada** caixa de texto, Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.

    e. Em Olá **URL da página de Logout** caixa de texto, Olá colar **URL de logout** que você copiou do portal do Azure.

    f. Em **certificado do provedor de identidade**, clique em **Escolher arquivo**e, em seguida, carregue o certificado de saudação que você baixou do portal do Azure de saudação. 

    g. Clique em **SALVAR ALTERAÇÕES**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-syncplicity-test-user"></a>Criar um usuário de teste do Syncplicity
Para AAD usuários toobe capaz de toosign no, eles devem ser provisionados tooSyncplicity aplicativo. Esta seção descreve como contas de usuário do AAD toocreate no Syncplicity.

**tooprovision um tooSyncplicity de conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Syncplicity** locatário (por exemplo: `https://company.Syncplicity.com`).

2. Clique em **Administrador** e selecione **Contas de Usuário**.

3. Clique em **ADICIONAR UM USUÁRIO**.
   
    ![Gerenciar Usuários](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gerenciar Usuários")

4. Saudação de tipo **endereços de Email** de uma conta do AAD que você deseja tooprovision, selecione **usuário** como **função**e, em seguida, clique em **próximo**.
   
    ![Dados da Conta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Dados da Conta")
   
    >[!NOTE]
    >proprietário de conta do AAD Olá obtém um email incluindo um link tooconfirm e ativar conta hello. 
    > 

5. Selecione um grupo em sua empresa do qual o novo usuário deverá se tornar membro e clique em **AVANÇAR**.
   
    ![Associação a um Grupo](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Associação a um Grupo")
   
    >[!NOTE]
    >Se não houver nenhum grupo listado, basta clicar em **AVANÇAR**. 
    > 

6. Selecione as pastas Olá seria como tooplace sob controle do Syncplicity no computador do usuário hello e, em seguida, clique em **próximo**.
   
    ![Pastas do Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Pastas do Syncplicity")

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Syncplicity usuário conta ou APIs fornecidas pelo Syncplicity tooprovision contas de usuário do AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSyncplicity.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSyncplicity, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Syncplicity**.

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco Syncplicity Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Syncplicity aplicativo.
## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

