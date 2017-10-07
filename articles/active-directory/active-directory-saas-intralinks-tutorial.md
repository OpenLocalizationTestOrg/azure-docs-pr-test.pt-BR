---
title: "Tutorial: integração do Azure Active Directory com o Intralinks | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Tutorial: Integração do Azure Active Directory com o Intralinks

Neste tutorial, você aprenderá como toointegrate Intralinks com o Azure Active Directory (AD do Azure).

Integrando Intralinks com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooIntralinks
- Você pode habilitar seus usuários tooautomatically get conectado tooIntralinks (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Intralinks, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Intralinks

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Intralinks da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-intralinks-from-hello-gallery"></a>Adicionando Intralinks da Galeria de saudação
integração de saudação tooconfigure de Intralinks no AD do Azure, você precisa tooadd Intralinks da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Intralinks da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Intralinks**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. No painel de resultados de saudação, selecione **Intralinks**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Intralinks, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Intralinks é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Intralinks precisa toobe estabelecida.

Intralinks, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Intralinks, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Intralinks](#creating-an-intralinks-test-user)**  -toohave um equivalente do Britta Simon em Intralinks é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Intralinks.

**tooconfigure AD do Azure-logon único com Intralinks, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Intralinks** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. Em Olá **Intralinks domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Entre em contato com [equipe de suporte do cliente Intralinks](https://www.intralinks.com/contact-1) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. tooconfigure logon único no **Intralinks** lado, você precisa toosend Olá baixado **Metadata XML** [equipe de suporte do Intralinks](https://www.intralinks.com/contact-1). Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-intralinks-test-user"></a>Criação de um usuário de teste do Intralinks

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Intralinks. Trabalhe com [Intralinks equipe de suporte](https://www.intralinks.com/contact-1) tooadd usuários de saudação na plataforma de Intralinks hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIntralinks.

![Atribuir usuário][200] 

**tooassign Britta Simon tooIntralinks, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Intralinks**.

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

### <a name="add-intralinks-via-or-elite-application"></a>Adicionar o aplicativo Intralinks VIA ou Elite

Usa Intralinks Olá mesma plataforma de identidade SSO para todos os outros aplicativos Intralinks excluindo aplicativo Nexus de negócio. Para que se planejar toouse qualquer outro aplicativo de Intralinks, em seguida, primeiro é necessário tooconfigure SSO para um aplicativo primário Intralinks usando Olá procedimento descrito acima.

Depois que você pode seguir Olá abaixo procedimento tooadd outro aplicativo Intralinks em seu locatário que pode aproveitar esse aplicativo primário para o SSO. 

>[!NOTE]
>Este recurso está disponível apenas clientes de SKU do tooAzure AD Premium e não está disponível para clientes gratuito ou básico de SKU.

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]


2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Intralinks**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Em **Intralinks Adicionar aplicativo** executar Olá etapas a seguir:

    ![Adicionar o aplicativo Intralinks VIA ou Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    a. Em **nome** caixa de texto, digite o nome apropriado do aplicativo hello, por exemplo, **Intralinks Elite**.

    b. Clique no botão **Adicionar**.

6.  Em Olá portal do Azure, Olá **Intralinks** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

7. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **logon vinculado**.
 
    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. Obter URL do SSO iniciado Olá Olá SP de [Intralinks equipe](https://www.intralinks.com/contact-1) para Olá outro aplicativo Intralinks e insira-a na **configurar URL de logon** conforme mostrado abaixo. 
    
     ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     Na caixa de texto de URL de entrada hello, digite Olá URL usado pelo seu aplicativo de Intralinks tooyour toosign em usuários usando o saudação padrão a seguir:
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. Atribuir Olá aplicativo toouser ou grupos, conforme mostrado na seção de saudação  **[usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá Intralinks bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Intralinks aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

