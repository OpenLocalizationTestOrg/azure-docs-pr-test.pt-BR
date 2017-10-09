---
title: "Tutorial: Integração do Azure Active Directory ao Rightscale | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Tutorial: Integração do Azure Active Directory ao Rightscale

Neste tutorial, você aprenderá como toointegrate Rightscale com o Azure Active Directory (AD do Azure).

Integrando Rightscale com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooRightscale
- Você pode habilitar seu usuários tooautomatically get conectado tooRightscale (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Rightscale, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Rightscale

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Rightscale da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-rightscale-from-hello-gallery"></a>Adicionando Rightscale da Galeria de saudação
integração de saudação tooconfigure de Rightscale no AD do Azure, você precisa tooadd Rightscale da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Rightscale da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Rightscale**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. No painel de resultados de saudação, selecione **Rightscale**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Rightscale, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Rightscale é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Rightscale precisa toobe estabelecida.

Rightscale, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Rightscale, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Rightscale](#creating-a-rightscale-test-user)**  -toohave um equivalente do Britta Simon em Rightscale é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Rightscale.

**tooconfigure AD do Azure-logon único com Rightscale, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Rightscale** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. Em Olá **Rightscale domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP** você não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. Em Olá **Rightscale domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Clique em Olá **Mostrar configurações de URL avançadas**.

    b. Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://login.rightscale.com/`

5. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. Em Olá **Rightscale configuração** seção, clique em **configurar Rightscale** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. tooget SSO configurado para o seu aplicativo, você precisa em toosign tooyour RightScale locatário como um administrador.

    a. No menu de saudação na parte superior do hello, clique Olá **configurações** guia e selecione **Single Sign-On**.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Clique em hello "**novo**" botão tooadd **seus provedores de identidade SAML**.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. Na caixa de texto de saudação do **nome de exibição**, insira o nome da sua empresa.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Selecione **usando uma dica de descoberta SSO iniciado permitir RightScale** e entrada seu **nome de domínio** em Olá abaixo da caixa de texto.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Cole o valor de saudação do **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure em **o ponto de extremidade do SAML SSO** em RightScale.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Cole o valor de saudação do **ID da entidade SAML** que você copiou do portal do Azure em **EntityID SAML** em RightScale.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Clique em **navegador** certificado de saudação do botão tooupload que baixou do portal do Azure.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Clique em **Salvar**.
<CE>
> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-rightscale-test-user"></a>Criando um usuário de teste do Rightscale

Nesta seção, você criará um usuário chamado Brenda Fernandes no RightScale. Trabalhar com [equipe de suporte do cliente Rightscale](mailto:support@rightscale.com) tooadd usuários de saudação na plataforma de RightScale hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRightscale.

![Atribuir usuário][200] 

**tooassign Britta Simon tooRightscale, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Rightscale**.

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.  

Quando você clica em bloco RightScale Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour RightScale aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

