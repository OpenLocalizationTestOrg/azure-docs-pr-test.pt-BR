---
title: "Tutorial: Integração do Azure Active Directory ao ScreenSteps | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Tutorial: Integração do Active Directory do Azure com o ScreenSteps

Neste tutorial, você aprenderá como toointegrate ScreenSteps com o Azure Active Directory (AD do Azure).

Integrando o ScreenSteps com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooScreenSteps.
- Você pode habilitar seus usuários tooautomatically get conectado tooScreenSteps (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o ScreenSteps, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do ScreenSteps habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ScreenSteps da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-screensteps-from-hello-gallery"></a>Adicionando ScreenSteps da Galeria de saudação
integração de saudação tooconfigure do ScreenSteps no AD do Azure, você precisa tooadd ScreenSteps da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ScreenSteps da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **ScreenSteps**, selecione **ScreenSteps** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![ScreenSteps na lista de resultados de saudação](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o ScreenSteps, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ScreenSteps é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ScreenSteps precisa toobe estabelecida.

ScreenSteps, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o ScreenSteps, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do ScreenSteps](#create-a-screensteps-test-user)**  -toohave um equivalente do Britta Simon em ScreenSteps é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ScreenSteps.

**tooconfigure AD do Azure-logon único com o ScreenSteps, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **ScreenSteps** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. Em Olá **ScreenSteps domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello real URL de entrada, que é explicada mais adiante neste tutorial. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. Em Olá **ScreenSteps configuração** seção, clique em **configurar ScreenSteps** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa ScreenSteps como um administrador.

8. Clique em **Configurações da Conta**.

    ![Gerenciamento de contas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Gerenciamento de contas")

9. Clique em **Logon Único**.

    ![Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticação Remota")

10. Clique em  **Criar Ponto de Extremidade de Logon Único**.

    ![Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticação Remota")

11. Em Olá **criar único logon no ponto de extremidade** , execute Olá etapas a seguir:

    ![Criar um Ponto de Extremidade de Autenticação](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Criar um Ponto de Extremidade de Autenticação")
    
    a. Em Olá **título** caixa de texto, digite um título.
    
    b. De saudação **modo** lista, selecione **SAML**.
    
    c. Clique em **Criar**.

12. **Editar** Olá novo ponto de extremidade.

    ![Editar ponto de extremidade](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Editar ponto de extremidade")

13. Em Olá **Editar único logon no ponto de extremidade** , execute Olá etapas a seguir:

    ![Ponto de Extremidade de Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Ponto de Extremidade de Autenticação Remota")

    a. Clique em **novo arquivo de certificado SAML carregamento**e, em seguida, carregar Olá certificado, que você baixou do portal do Azure.
    
    b. Colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de logon remoto** caixa de texto.
    
    c. Colar **URL de logout** valor que você copiou de saudação portal do Azure em hello **URL de logoff** caixa de texto.
    
    d. Selecione um **grupo** tooassign toowhen de usuários que são provisionados.
    
    e. Clique em **Atualizar**.

    f. Saudação de cópia **SAML consumidor URL** toohello área de transferência e cole no toohello **URL de logon** textbox em **ScreenSteps domínio e URLs** seção.
    
    g. Retornar toohello **Editar único logon no ponto de extremidade**.
    
    h. Clique em Olá **tornar padrão para a conta** botão toouse esse ponto de extremidade para todos os usuários que fizerem logon em ScreenSteps. Como alternativa, você pode clicar Olá **adicionar tooSite** botão toouse esse ponto de extremidade para sites específicos em **ScreenSteps**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-screensteps-test-user"></a>Criar um usuário de teste do ScreenSteps

Nesta seção, você criará um usuário chamado Brenda Fernandes no ScreenSteps. Trabalhar com [equipe de suporte do cliente ScreenSteps](https://www.screensteps.com/contact) para adicionar usuários de saudação na plataforma do ScreenSteps hello. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooScreenSteps.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooScreenSteps, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ScreenSteps**.

    ![link de ScreenSteps Olá na lista de aplicativos Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá ScreenSteps bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo ScreenSteps.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

