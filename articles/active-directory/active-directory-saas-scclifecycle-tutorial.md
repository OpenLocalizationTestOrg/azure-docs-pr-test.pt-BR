---
title: "Tutorial: integração do Azure Active Directory com o SCC LifeCycle | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SCC LifeCycle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 63623c5bd2d951612040f0121615a406bf83e890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Tutorial: Integração do Active Directory do Azure com o SCC LifeCycle

Neste tutorial, você aprenderá como toointegrate SCC LifeCycle com o Azure Active Directory (AD do Azure).

Integração do SCC LifeCycle com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSCC ciclo de vida
- Você pode habilitar seu usuários tooautomatically get conectado tooSCC ciclo de vida (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o ciclo de vida de SCC, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SCC LifeCycle

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o ciclo de vida de SCC da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-scc-lifecycle-from-hello-gallery"></a>Adicionando o ciclo de vida de SCC da Galeria de saudação
integração de saudação tooconfigure do ciclo de vida de SCC no AD do Azure, você precisa tooadd SCC LifeCycle na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SCC LifeCycle da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **SCC LifeCycle**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. No painel de resultados de saudação, selecione **SCC LifeCycle**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure

Nesta seção, você configura e testa o logon único do Azure AD com o SCC LifeCycle, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ciclo de vida de SCC é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação do ciclo de vida de SCC precisa toobe estabelecida.

No ciclo de vida de SCC, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o ciclo de vida de SCC, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do ciclo de vida de SCC](#creating-an-scc-lifecycle-test-user)**  -toohave um equivalente do Britta Simon no ciclo de vida de SCC é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do SCC LifeCycle.

**tooconfigure AD do Azure-logon único com SCC LifeCycle, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **SCC LifeCycle** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. Em Olá **domínio de ciclo de vida de SCC e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente do ciclo de vida de SCC](mailto:lifecycle.support@scc.com) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. tooconfigure logon único no **SCC LifeCycle** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do SCC LifeCycle](mailto:lifecycle.support@scc.com). Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.

     >[!NOTE]
   >O logon único tem toobe habilitado por Olá, equipe de suporte do SCC LifeCycle.
   > 
   > 

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-scc-lifecycle-test-user"></a>Criando um usuário de teste do SCC LifeCycle

Ordem tooenable AD do Azure usuários toolog no SCC LifeCycle, eles devem ser provisionados no SCC LifeCycle. Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooSCC ciclo de vida.

Quando um toolog de tentativas de usuário atribuído no SCC LifeCycle, uma conta do SCC LifeCycle é criada automaticamente, se necessário.

> [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSCC ciclo de vida.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSCC ciclo de vida, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos.**

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SCC LifeCycle**.

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá SCC LifeCycle bloco no painel de acesso de saudação, você deve obter tooSCC automaticamente conectado no ciclo de vida de aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

