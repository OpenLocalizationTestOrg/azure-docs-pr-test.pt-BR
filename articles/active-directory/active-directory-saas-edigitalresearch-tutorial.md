---
title: "Tutorial: integração do Azure Active Directory ao eDigitalResearch | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a>Tutorial: integração do Azure Active Directory ao eDigitalResearch

Neste tutorial, você aprenderá como eDigitalResearch toointegrate com o Azure Active Directory (AD do Azure).

Integrando eDigitalResearch com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooeDigitalResearch.
- Você pode habilitar seu usuários tooautomatically get conectado tooeDigitalResearch (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com eDigitalResearch, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do eDigitalResearch habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando eDigitalResearch da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-edigitalresearch-from-hello-gallery"></a>Adicionando eDigitalResearch da Galeria de saudação
integração de saudação tooconfigure de eDigitalResearch no AD do Azure, você precisa eDigitalResearch tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**eDigitalResearch tooadd da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **eDigitalResearch**, selecione **eDigitalResearch** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![eDigitalResearch na lista de resultados de saudação](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o eDigitalResearch, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em eDigitalResearch é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em eDigitalResearch precisa toobe estabelecida.

EDigitalResearch, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com eDigitalResearch, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave um equivalente do Britta Simon em eDigitalResearch é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo eDigitalResearch.

**tooconfigure AD do Azure-logon único com eDigitalResearch, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **eDigitalResearch** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. Em Olá **eDigitalResearch domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.edigitalresearch.com`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.edigitalresearch.com/login/consume`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [eDigitalResearch a equipe de suporte](http://www.maruedr.com/contact) tooget esses valores.
 


4. Em Olá **o certificado de autenticação SAML** seção, clique em **Base(64) certificado** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    !![link de download de certificado Olá](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. Em Olá **eDigitalResearch configuração** seção, clique em **configurar eDigitalResearch** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID da entidade SAML** de saudação **seção de referência rápida.**

    ![Configuração do eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. tooconfigure logon único no **eDigitalResearch** lado, você precisa toosend Olá baixado **arquivo de certificado (Base64)**, **ID da entidade SAML**, e  **URL de saída** muito[a equipe de suporte eDigitalResearch](http://www.maruedr.com/contact). Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
  
### <a name="create-a-edigitalresearch-test-user"></a>Criar um usuário de teste eDigitalResearch

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no eDigitalResearch. 

Trabalhar com hello [eDigitalResearch a equipe de suporte](http://www.maruedr.com/contact) tooget usuários criados.       
    
 > [!NOTE]
 > proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooeDigitalResearch.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooeDigitalResearch, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **eDigitalResearch**.

    ![Olá eDigitalResearch link na lista de aplicativos Olá](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco eDigitalResearch Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour eDigitalResearch aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

