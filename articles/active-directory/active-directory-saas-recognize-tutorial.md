---
title: "Tutorial: Integração do Azure Active Directory com o Recognize | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e reconhecer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a>Tutorial: integração do Azure Active Directory com o Recognize

Neste tutorial, você aprenderá como toointegrate reconhece com o Azure Active Directory (AD do Azure).

Integrando reconhecer o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooRecognize
- Você pode habilitar seu usuários tooautomatically get conectado tooRecognize (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração tooconfigure AD do Azure com reconhecer, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Recognize

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando reconhecer da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-recognize-from-hello-gallery"></a>Adicionando reconhecer da Galeria de saudação
integração de saudação tooconfigure de reconhecer no AD do Azure, você precisa tooadd reconhecer da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd reconhecer da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **reconhecer**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. No painel de resultados de saudação, selecione **reconhecer**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Recognize, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em reconhecer é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em reconhecer precisa toobe estabelecida.

Reconhecer, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

teste do AD do Azure e tooconfigure o logon único com reconhecer, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de reconhecer](#creating-a-recognize-test-user)**  -toohave um equivalente do Britta Simon em reconhecer que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de reconhecer.

**tooconfigure AD do Azure-logon único com reconhecer, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **reconhecer** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. Em Olá **domínio reconhecer e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://recognizeapp.com/<your-domain>/saml/sso`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://recognizeapp.com/<your-domain>`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente reconhece](mailto:support@recognizeapp.com) obter a URL de logon e você pode obter o valor de identificador abrindo Olá URL de metadados do provedor de serviço de saudação seção de configurações de SSO é explicada posteriormente no tutorial de saudação. . 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. Em Olá **configuração reconhecer** seção, clique em **configurar reconhecer** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. Em uma janela de navegador web diferente, logon tooyour reconhecer locatário como um administrador.

8. Olá canto superior direito, clique em **Menu**. Vá muito**administrador da empresa**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. No painel de navegação esquerdo hello, clique em **configurações**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. Executar Olá seguindo as etapas na **configurações de SSO** seção.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    a. Em **Habilitar SSO**, selecione **ATIVADO**.

    b. Em hello **ID da entidade IDP** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.
    
    c. Em hello **url de destino Sso** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
    
    d. Em Olá **url de destino Slo** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure. 
    
    e. Abra seu baixado **certificado (Base64)** no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado** caixa de texto.
    
    f. Clique em Olá **salvar configurações** botão. 

11. Ao lado de saudação **configurações de SSO** seção, copie a URL de saudação em **url de metadados de provedor de serviço**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. Olá abrir **link de URL de metadados** em um documento de metadados do navegador em branco toodownload hello. Copie Olá EntityDescriptor value(entityID) do arquivo hello e cole-o na **identificador** textbox em **seção domínio reconhecer e URLs** no portal do Azure.
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-recognize-test-user"></a>Criando um usuário de teste do Recognize

Em ordem tooenable AD do Azure usuários toolog em reconhecer, eles devem ser provisionados no reconhecer. No caso de saudação de reconhecer, o provisionamento é uma tarefa manual.

Este aplicativo não dá suporte ao provisionamento de SCIM, mas tem uma sincronização de usuário alternativa que provisiona usuários. 

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon em seu site de empresa Recognize como um administrador.

2. Olá canto superior direito, clique em **Menu**. Vá muito**administrador da empresa**.

3. No painel de navegação esquerdo hello, clique em **configurações**.

4. Executar Olá seguindo as etapas na **usuário sincronização** seção.
   
   ![Novo Usuário](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Novo Usuário")
   
   a. Em **Sincronização habilitada**, selecione **ATIVADO**.
   
   b. Em **Escolher o provedor de sincronização**, selecione **Microsoft / Office 365**.
   
   c. Clique em **Executar Sincronização de Usuário**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRecognize.

![Atribuir usuário][200] 

**tooassign Britta Simon tooRecognize, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **reconhecer**.

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em um bloco de reconhecer Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour reconhecer aplicativos. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

