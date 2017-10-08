---
title: "Tutorial: Integração do Azure Active Directory com o Zendesk | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Tutorial: Integração do Active Directory do Azure com o Zendesk

Neste tutorial, você aprenderá como toointegrate Zendesk com o Azure Active Directory (AD do Azure).

Integração do Zendesk com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooZendesk
- Você pode habilitar seu usuários tooautomatically get conectado tooZendesk (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Zendesk, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Zendesk


> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Zendesk da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-zendesk-from-hello-gallery"></a>Adicionando Zendesk da Galeria de saudação
integração de saudação tooconfigure do Zendesk no AD do Azure, você precisa tooadd Zendesk da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Zendesk da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Zendesk**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. No painel de resultados de saudação, selecione **Zendesk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Zendesk, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zendesk é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zendesk precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Zendesk.

tooconfigure e teste de logon único do AD do Azure com o Zendesk, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Zendesk](#creating-a-zendesk-test-user)**  -toohave um equivalente do Britta Simon no Zendesk é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Zendesk.

**tooconfigure AD do Azure-logon único com o Zendesk, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Zendesk** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. Em Olá **Zendesk domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<subdomain>.zendesk.com`

    b. Em Olá **identificador** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de logon real hello e a URL de identificador. Entre em contato com [equipe de suporte do Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget esses valores. 

4. Zendesk espera as asserções SAML de saudação em um formato específico. Não há nenhum atributo SAML obrigatório, mas, opcionalmente, você pode adicionar um atributo de **atributos de usuário** seção Olá seguir etapas a seguir: 

     ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Clique em Olá **exibir e editar Olá outros atributos** caixa de seleção.
     
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Clique em Olá **Adicionar atributo** tooopen **Adicionar atributo** caixa de diálogo.
    
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. Em Olá **nome** caixa de texto Nome do atributo do tipo hello (por exemplo **emailaddress**).
    
    d. De saudação **valor** lista, o valor do atributo select hello (como **user.mail**).
    
    e. Clique em **Ok**
 
    > [!NOTE] 
    > Você usar atributos de tooadd de atributos de extensão que não estão no AD do Azure por padrão. Clique em [atributos de usuário que podem ser definidos em SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) lista completa de saudação de tooget de SAML atributos que **Zendesk** aceita. 

5. Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. Em Olá **Zendesk configuração** seção, clique em **configurar Zendesk** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zendesk como administrador.

8. Clique em **Administrador**.

9. No painel de navegação esquerdo hello, clique em **configurações**e, em seguida, clique em **segurança**.

10. Em Olá **segurança** página, execute Olá etapas a seguir: 
   
     ![Segurança](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Segurança")

    ![Logon Único](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Logon Único")

     a. Clique em Olá **agentes & Admin** guia.

     b. Selecione **SSO (logon único) e SAML** e, em seguida, selecione **SAML**.

     c. Em **URL SSO SAML** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure. 

     d. Em **URL de Logout remoto** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.
        
     e. Em **impressão digital do certificado** caixa de texto, colar Olá **impressão digital** o valor de certificado que você copiou do portal do Azure.
     
     f. Clique em **Salvar**.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários ir muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 

### <a name="creating-a-zendesk-test-user"></a>Criação de um usuário de teste do Zendesk

toolog de usuários tooenable AD do Azure em **Zendesk**, eles devem ser provisionados no **Zendesk**.  
Dependendo da função hello atribuída em aplicativos hello, Olá seu comportamento esperado:

 1. As contas de **Usuário final** são provisionadas automaticamente ao entrar.
 2. **Agente** e **Admin** contas precisam toobe provisionada manualmente no **Zendesk** antes de entrar.
 
**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Zendesk** locatário.

2. Selecione Olá **lista de clientes** guia.

3. Selecione Olá **usuário** guia e, em seguida, clique em **adicionar**.
   
    ![Adicionar Usuário](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Adicionar Usuário")
4. Digite o endereço de email de saudação de uma conta existente do AD do Azure você deseja tooprovision e, em seguida, clique em **salvar**.
   
    ![Novo Usuário](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Novo Usuário")

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros Zendesk usuário conta ou APIs fornecidas pelo Zendesk tooprovision contas de usuário do AAD.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZendesk.

![Atribuir usuário][200] 

**tooassign Britta Simon tooZendesk, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Zendesk**.

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Zendesk Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Zendesk aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
