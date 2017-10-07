---
title: "Tutorial: integração do Azure Active Directory do ao Dropbox for Business | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Tutorial: integração do Active Directory do Azure ao Dropbox for Business

Neste tutorial, você aprenderá como toointegrate Dropbox para empresas com o Azure Active Directory (AD do Azure).

Integrando o Dropbox for Business com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooDropbox para empresas
- Você pode habilitar seu usuários tooautomatically get conectado tooDropbox para negócios (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com Dropbox for Business, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Dropbox for Business

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Dropbox for Business da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Adicionando Dropbox for Business da Galeria de saudação
integração de saudação do tooconfigure do Dropbox for Business no AD do Azure, você precisa tooadd Dropbox para empresas da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Dropbox for Business da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Dropbox for Business**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. No painel de resultados de saudação, selecione **Dropbox for Business**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Dropbox for Business, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Dropbox for Business é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Dropbox for Business precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Dropbox for Business.

tooconfigure e teste de logon único do Azure AD com Dropbox para empresas, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar uma pasta de transferência para o usuário de teste de negócios](#creating-a-dropbox-for-business-test-user)**  -toohave um equivalente do Britta Simon no Dropbox para empresas que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Dropbox para o aplicativo de negócios.

**tooconfigure AD do Azure-logon único com Dropbox for Business, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Dropbox for Business** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. Em Olá **Dropbox para o domínio de negócios e URLs** , execute Olá etapas a seguir:

    a. Faça logon no tooyour Dropbox para o locatário de negócios. 
   
    ![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurar logon único")
   
    b. No painel de navegação Olá no lado esquerdo do hello, clique em **Console de administração**. 
   
    ![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurar logon único")
   
    c. Em Olá **Console de administração**, clique em **autenticação** no painel de navegação esquerdo hello. 
   
    ![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurar logon único")
   
    d. Em Olá **o logon único** seção, selecione **habilitar logon único**e, em seguida, clique em **mais** tooexpand nesta seção.  
   
    ![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurar logon único")
   
    e. Copiar URL da saudação Avançar muito**os usuários podem entrar digitando seu endereço de email ou podem ir diretamente para**. 
    
    ![Configurar o logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. Em Olá portal do Azure, na Olá **URL de logon** caixa de texto, colar Olá URL.

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Esse valor não é o valor real. Atualize o valor de saudação com hello real URL de logon você obter de sua seção de logon único. Entre em contato com [Dropbox para a equipe de suporte do cliente de negócios](https://www.dropbox.com/business/contact) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. Em Olá **Dropbox for Business configuração** seção, clique em **configurar Dropbox for Business** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure logon único no **Dropbox for Business** lado, vá em seu locatário Dropbox for Business, em Olá **o logon único** seção Olá **autenticação** página, Execute Olá etapas a seguir: 
   
    ![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurar logon único")
   
    a. Clique em **Obrigatório**.
   
    b. Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **URL de entrada** caixa de texto.

    c. Clique em **escolher certificado**e, em seguida, procure tooyour **arquivo de certificado codificado em Base64**.

    d. Clique em **salvar alterações** toocomplete configuração de saudação em seu locatário DropBox for Business.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Criando um usuário de teste do Dropbox for Business

Nesta seção, um usuário chamado Brenda Fernandes é criado no Dropbox for Business. O Dropbox for Business dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Se um usuário não existir no Dropbox for Business, um novo é criado quando você tenta tooaccess Dropbox para empresas.

>[!Note]
>Se você precisar toocreate um usuário manualmente, entre em contato com [Dropbox para a equipe de suporte do cliente de negócios](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDropbox para empresas.

![Atribuir usuário][200] 

**tooassign Britta Simon tooDropbox para empresas, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Dropbox for Business**.

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em hello Dropbox para o bloco de negócios no hello painel de acesso, você deve obter a página de logon do seu Dropbox para aplicativo de negócios.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

