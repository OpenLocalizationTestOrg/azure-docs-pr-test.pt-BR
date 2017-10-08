---
title: "Tutorial: Integração do Azure Active Directory ao Tangoe Command Premium Mobile| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tangoe comando Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>Tutorial: Integração do Azure Active Directory ao Tangoe Command Premium Mobile

Neste tutorial, você aprenderá como toointegrate Tangoe comando Premium móvel com o Azure Active Directory (AD do Azure).

Integrando Tangoe comando Premium móvel com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTangoe comando Premium Mobile
- Você pode habilitar seu usuários tooautomatically get conectado tooTangoe comando Premium Mobile (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Tangoe comando Premium móvel, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Tangoe Command Premium Mobile habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Tangoe comando Premium móvel da Galeria de saudação
2. Configurar e testar logon único do Azure AD

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>Adicionar Tangoe comando Premium móvel da Galeria de saudação
integração de Olá tooconfigure do Tangoe comando Premium Mobile no AD do Azure, você precisa tooadd Tangoe comando Premium móvel da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Tangoe comando Premium móvel da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Tangoe comando Premium Mobile**, selecione **Tangoe comando Premium Mobile** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Adicionar o Tangoe Command Premium Mobile da galeria ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o Tangoe Command Premium Mobile, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Tangoe comando Premium Mobile é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Tangoe comando Premium Mobile precisa toobe estabelecida.

Tangoe comando Premium Mobile, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Tangoe comando Premium Mobile, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Tangoe comando Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave um equivalente do Britta Simon no Tangoe comando Premium Mobile que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo móvel do Tangoe comando Premium.

**tooconfigure logon único do AD do Azure com Tangoe comando Premium Mobile, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Tangoe comando Premium Mobile** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Logon único baseado em SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. Em Olá **Tangoe comando Premium Mobile domínio e URLs** , execute Olá etapas a seguir:

    ![Domínio e URLs do Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta real hello e a URL de logon. Entre em contato com [a equipe de suporte Tangoe comando Premium móveis cliente](https://www.tangoe.com/contact-2/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. Em Olá **Tangoe comando Premium Mobile configuração** seção, clique em **configurar o Tangoe comando Premium Mobile** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Seção Configuração do Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget SSO configurado para o seu aplicativo, entre em contato com seu [a equipe de suporte Tangoe comando Premium móveis cliente](https://www.tangoe.com/contact-2/) e fornecer Olá seguintes:

   - arquivo de metadados baixado Olá
   - Olá **ID de entidade de SAML**
   - Olá **Single Sign-On URL do serviço SAML**
   - Olá **URL de logout**

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Adicionar usuário](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>Criar um usuário de teste do Tangoe Command Premium Mobile

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tangoe Command Premium Mobile. 

Aplicativo Tangoe comando Premium Mobile precisa de todas as toobe de usuários Olá provisionado no aplicativo hello antes de fazer logon único. Portanto, o trabalho com hello [a equipe de suporte Tangoe comando Premium móveis cliente](https://www.tangoe.com/contact-2/) tooprovision todos esses usuários para o aplicativo hello. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTangoe comando Premium Mobile.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTangoe comando Premium móveis, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Tangoe comando Premium Mobile**.

    ![Tangoe Command Premium Mobile na lista de aplicativos](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.

Quando você clica em bloco Tangoe comando Premium Mobile Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo móvel do Tangoe comando Premium. Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

