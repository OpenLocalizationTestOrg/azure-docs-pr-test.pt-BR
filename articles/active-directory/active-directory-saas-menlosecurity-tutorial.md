---
title: "Tutorial: Integração do Azure Active Directory com o Menlo Security | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Menlo segurança."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a>Tutorial: Integração do Azure Active Directory com o Menlo Security

Neste tutorial, você aprenderá como toointegrate Menlo segurança com o Azure Active Directory (AD do Azure).

Integração de segurança Menlo com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooMenlo segurança
- Você pode habilitar seu usuários tooautomatically get conectado tooMenlo segurança (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte. [O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com segurança Menlo, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Menlo Security habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando segurança Menlo da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-menlo-security-from-hello-gallery"></a>Adicionando segurança Menlo da Galeria de saudação
integração de Olá tooconfigure de Menlo segurança no AD do Azure, você precisa tooadd Menlo segurança da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd segurança Menlo da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Menlo segurança**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. No painel de resultados de saudação, selecione **Menlo segurança**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Menlo Security com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em segurança Menlo é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em segurança Menlo precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em segurança Menlo.

tooconfigure e teste de logon único do AD do Azure com segurança Menlo, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de segurança Menlo](#creating-a-menlo-security-test-user)**  -toohave um equivalente do Britta Simon em segurança Menlo toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de segurança de Menlo.

**tooconfigure AD do Azure-logon único com segurança Menlo, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Menlo segurança** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. Em Olá **Menlo domínio de segurança e as URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.menlosecurity.com/account/login`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`

    > [!NOTE] 
    > Esses valores não são Olá real. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte de cliente de segurança Menlo](https://www.menlosecurity.com/menlo-contact) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. Em hello **a configuração de segurança Menlo** seção, clique em **configurar segurança de Menlo** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML**, e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. tooconfigure logon único no **Menlo segurança** lado, o logon toohello **Menlo segurança** site como um administrador.

8. Em **configurações** ir muito**autenticação** e executar as seguintes ações:
    
    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    a. Caixa de seleção de saudação de escala **habilitar a autenticação do usuário usando SAML**.

    b. Selecione **permitir acesso externo** muito**Sim**.

    c. Em **Provedor SAML**, selecione **Azure Active Directory**.

    d. **O ponto de extremidade do SAML 2.0** : Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.

    e. **Identificador de serviço (emissor)** : Olá colar **ID da entidade SAML** que você copiou do portal do Azure.

    f. **Certificado x. 509** : Olá abrir **certificado (Base64)** baixado da saudação Portal do Azure no bloco de notas e cole-o nesta caixa.

    g. Clique em **salvar** toosave configurações de saudação.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-menlo-security-test-user"></a>Criar um usuário de teste do Menlo Security
 
Nesta seção, você criará uma usuária chamada Brenda Fernandes no Menlo Security. Trabalhar com [equipe de suporte de cliente de segurança Menlo](https://www.menlosecurity.com/menlo-contact) tooadd usuários de saudação na plataforma de segurança Menlo hello. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMenlo segurança.

![Atribuir usuário][200] 

**tooassign Britta Simon tooMenlo segurança, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Menlo segurança**.

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD.

Abra uma janela de navegador em um tootrigger de modo "InPrivate" ou "Incognito" uma nova autenticação.  No Internet Explorer, use Ctrl + Shift + P.  No Chrome, use Ctrl + Shift + N.  Na janela de navegação particular hello, procurar tooa recurso protegido e executar um logon do AD do Azure.  Após o logon bem-sucedido, será o site solicitado toohello feito em uma sessão de isolamento.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

