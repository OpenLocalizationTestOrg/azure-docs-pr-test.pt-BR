---
title: "Tutorial: integração do Azure Active Directory com o etouches | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>Tutorial: integração do Azure Active Directory com o etouches

Neste tutorial, você aprenderá como etouches toointegrate com o Azure Active Directory (AD do Azure).

Integrando etouches com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooetouches
- Você pode habilitar seus usuários tooautomatically get conectado tooetouches (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com etouches, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do etouches habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando etouches da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-etouches-from-hello-gallery"></a>Adicionando etouches da Galeria de saudação
integração de saudação tooconfigure de etouches no AD do Azure, você precisa etouches tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**etouches tooadd da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **etouches**, selecione **etouches** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![etouches na lista de resultados de saudação](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o etouches, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em etouches é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em etouches precisa toobe estabelecida.

Etouches, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com etouches, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste etouches](#create-an-etouches-test-user)**  -toohave um equivalente do Britta Simon em etouches é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo etouches.

**tooconfigure AD do Azure-logon único com etouches, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **etouches** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. Em Olá **etouches domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar o valor Olá com hello real entrar na URL e o identificador, que é explicada posteriormente no tutorial de saudação.
    > 

4. aplicativo de etouches espera asserções SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de saudação **usuário atributo** do aplicativo hello. Olá captura de tela a seguir mostra um exemplo. 

    ![Atributo de Usuário](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | ------------------- | -------------------- |
    | Email | user.mail |    
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Adicionar Atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Caixa de diálogo Adicionar Atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **OK**. 

6. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget SSO configurado para o seu aplicativo executar Olá seguindo as etapas no aplicativo de etouches hello: 

    ![configuração do etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    a. Logon muito**etouches** usando os direitos de administrador de saudação do aplicativo.
   
    b. Vá toohello **SAML** configuração.

    c. Em Olá **configurações gerais** seção, abra seu certificado baixado do portal do Azure no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o na caixa de texto Olá IDP metadados. 

    d. Clique em Olá **Salvar & permanecer** botão.
  
    e. Clique em Olá **metadados de atualização** botão Olá seção de metadados de SAML. 

    f. Isso abre Olá página e executar o SSO. Uma vez Olá SSO está funcionando, em seguida, você pode configurar o nome de usuário de saudação.

    g. No campo de nome de usuário de saudação, selecione Olá **emailaddress** conforme mostrado na imagem de saudação abaixo. 

    h. Saudação de cópia **ID da entidade SP** valor e cole-a saudação **identificador** caixa de texto, que está em **etouches domínio e URLs** seção no portal do Azure.

    i. Saudação de cópia **URL SSO / ACS** valor e cole-a saudação **URL de logon** caixa de texto, que está em **etouches domínio e URLs** seção no portal do Azure.
   
> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-an-etouches-test-user"></a>Criar um usuário de teste no etouches

Nesta seção, você criará um usuário chamado Brenda Fernandes no etouches. Trabalhar com [etouches cliente equipe de suporte](https://www.etouches.com/event-software/support/customer-support/) tooadd usuários de saudação na plataforma de etouches hello.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooetouches.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooetouches, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **etouches**.

    ![Olá etouches link na lista de aplicativos Olá](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único


Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em Olá etouches bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour etouches aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

