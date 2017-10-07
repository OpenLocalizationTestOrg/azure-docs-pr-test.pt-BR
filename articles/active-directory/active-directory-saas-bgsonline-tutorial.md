---
title: "Tutorial: integração do Azure Active Directory com o BGS Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e unidades Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a>Tutorial: Integração do Azure Active Directory ao BGS Online

Neste tutorial, você aprenderá como toointegrate unidades Online com o Azure Active Directory (AD do Azure).

Integrando unidades Online com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBGS Online
- Você pode habilitar seus usuários tooautomatically get conectado tooBGS on-line (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com unidades Online, você precisará Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do BGS Online

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando unidades Online da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-bgs-online-from-hello-gallery"></a>Adicionando unidades Online da Galeria de saudação
integração de Olá tooconfigure de unidades Online no AD do Azure, você precisa tooadd unidades Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd unidades Online da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **unidades Online**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. No painel de resultados de saudação, selecione **unidades Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o BGS Online, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em unidades Online é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em unidades Online precisa toobe estabelecida.

Em unidades Online, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com unidades Online, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste unidades Online](#creating-a-bgs-online-test-user)**  -toohave um equivalente do Britta Simon em unidades Online que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo unidades Online.

**tooconfigure AD do Azure-logon único com unidades Online, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **unidades Online** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. Em Olá **domínio Online unidades e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:

    Para o ambiente de produção, use este padrão `https://<company name>.millwardbrown.report` 

    Para o ambiente de teste, use este padrão `https://millwardbrown.marketingtracker.nl/mt5/`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:
    
    Para o ambiente de produção, use este padrão `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx` 
      
    Para o ambiente de teste, use este padrão `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [unidades Online equipe de suporte](mailTo:bgsdashboardteam@millwardbrown.com) tooget esses valores.
 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. Em Olá **configuração Online de unidades** seção, clique em **configurar unidades Online** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. tooconfigure logon único no **unidades Online** lado, você precisa toosend Olá baixado **Metadata XML** e **Single Sign-On URL do serviço SAML** muito[unidades A equipe de suporte online](mailto:bgsdashboardteam@millwardbrown.com). 


> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-bgs-online-test-user"></a>Criando um usuário de teste do BGS Online

Nesta seção, você criará um usuário chamado Brenda Fernandes no BGS Online. Trabalhar com [unidades Online equipe de suporte](mailto:bgsdashboardteam@millwardbrown.com) tooadd usuários de saudação na plataforma unidades Online hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBGS on-line.

![Atribuir usuário][200] 

**tooassign Britta Simon tooBGS Online, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **unidades Online**.

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.

Quando você clica em bloco unidades Online Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de unidades on-line.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

