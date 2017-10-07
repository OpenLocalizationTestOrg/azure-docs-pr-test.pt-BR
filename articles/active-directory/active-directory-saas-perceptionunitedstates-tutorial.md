---
title: "Tutorial: Integração do Azure Active Directory ao Perception United States (não UltiPro) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Estados Unidos de percepção (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Tutorial: Integração do Azure Active Directory ao Perception United States (não UltiPro)

Neste tutorial, você aprenderá como toointegrate EUA percepção (Non-UltiPro) com o Azure Active Directory (AD do Azure).

Integração dos Estados Unidos de percepção (Non-UltiPro) com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooPerception Estados Unidos (Non-UltiPro).
- Você pode habilitar seu usuários tooautomatically get conectado tooPerception Estados Unidos (Non-UltiPro) (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com percepção dos Estados Unidos (Non-UltiPro), você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Perception United States (não UltiPro)

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Estados Unidos de percepção (Non-UltiPro) da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Adicionar Estados Unidos de percepção (Non-UltiPro) da Galeria de saudação
integração de saudação do tooconfigure de percepção dos Estados Unidos (Non-UltiPro) no AD do Azure, você precisa tooadd dos Estados Unidos de percepção (Non-UltiPro) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd EUA percepção (Non-UltiPro) da Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **dos Estados Unidos de percepção (Non-UltiPro)**, selecione **dos Estados Unidos de percepção (Non-UltiPro)** no painel de resultados e clique em **adicionar** tooadd de botão aplicativo Hello.

    ![EUA percepção (Non-UltiPro) na lista de resultados de saudação](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Perception United States (não UltiPro) com base em uma usuária de teste chamada “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no percepção dos Estados Unidos (Non-UltiPro) é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em percepção dos Estados Unidos (Non-UltiPro) precisa toobe estabelecida.

No percepção dos Estados Unidos (Non-UltiPro), atribua o valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com percepção dos Estados Unidos (Non-UltiPro), você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste dos Estados Unidos de percepção (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave um equivalente de Britta Simon no percepção dos Estados Unidos (Non-UltiPro) que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de percepção Brasil (Non-UltiPro).

**tooconfigure AD do Azure-logon único com percepção dos Estados Unidos (Non-UltiPro), execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **dos Estados Unidos de percepção (Non-UltiPro)** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. Em Olá **domínio EstadosUnidos percepção (Non-UltiPro) e as URLs** , execute Olá etapas a seguir:

    ![Informações sobre logon único de domínio e URLs do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://perception.kanjoya.com/sp`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > Olá valor não é real. Você atualizará o valor de saudação com hello real URL de resposta, que é explicada posteriormente no tutorial de saudação.
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. Em Olá **dos Estados Unidos de percepção (Non-UltiPro) configuração** seção, clique em **configurar percepção dos Estados Unidos (Non-UltiPro)** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**

    a. Olá **percepção Brasil (Non-UltiPro)** aplicativo requer Olá **ID da entidade SAML** valor, o que você copiou toobe uri codificado. valor de uri codificado do tooget hello, use a seguir Olá vincular:**http://www.url-encode-decode.com/**.

    b. Depois de obter o uri de saudação valor codificado combiná-lo com hello **URL de resposta** conforme mencionado abaixo -

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Olá colar acima do valor em Olá **URL de resposta** textbox em **domínio EstadosUnidos percepção (Non-UltiPro) e as URLs** seção.

    ![Configuração do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. Em outra janela do navegador, entre no site da empresa dos Estados Unidos de percepção (Non-UltiPro) tooyour como um administrador.

8. Na barra de ferramentas principal hello, clique em **configurações de conta**.

    ![Usuário do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. Em Olá **configurações de conta** página, execute Olá etapas a seguir:

    ![Usuário do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. Em Olá **nome da empresa** caixa de texto Nome do tipo hello de saudação **empresa**.
    
    b. Em Olá **nome da conta** caixa de texto Nome do tipo hello de saudação **conta**.

    c. Em **padrão resposta-tooEmail** caixa de texto, a saudação de tipo válida **Email**.

    d. Selecione **Provedor de identidade SSO** como **SAML 2.0**.

10. Em Olá **configuração SSO** página, execute Olá etapas a seguir:

    ![SSOConfig do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Selecione **Tipo de SAML NameID** como **EMAIL**.

    b. Em Olá **nome de configuração de SSO** caixa de texto, nome de saudação do tipo do seu **configuração**.
    
    c. Em **nome do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure. 

    d. Em **caixa de texto de domínio de SAML**, digite Olá domínio como  **@contoso.com** .

    e. Clique em **carregar novamente** Olá tooupload **Metadata XML** arquivo.

    f. Clique em **Atualizar**.


> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Criar um usuário de teste do Perception United States (não UltiPro)

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Perception United States (não UltiPro). Trabalhar com [a equipe de suporte dos Estados Unidos de percepção (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd usuários de saudação na plataforma do hello percepção Brasil (Non-UltiPro).

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPerception EUA (Non-UltiPro).

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooPerception EUA (Non-UltiPro), execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **dos Estados Unidos de percepção (Non-UltiPro)**.

    ![link do Hello percepção Brasil (Non-UltiPro) na lista de aplicativos Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em um bloco de percepção Brasil (Non-UltiPro) Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo percepção Brasil (Non-UltiPro).
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

