---
title: "Tutorial: integração do Azure Active Directory com o DocuSign | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Tutorial: integração do Active Directory do Azure com o DocuSign

Neste tutorial, você aprenderá como toointegrate DocuSign com o Azure Active Directory (AD do Azure).

Integrando o DocuSign com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooDocuSign
- Você pode habilitar seu usuários tooautomatically get conectado tooDocuSign (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o DocuSign, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do DocuSign

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando DocuSign da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-docusign-from-hello-gallery"></a>Adicionando DocuSign da Galeria de saudação
integração de saudação tooconfigure do DocuSign no AD do Azure, você precisa tooadd DocuSign na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd DocuSign da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **DocuSign**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. No painel de resultados de saudação, selecione **DocuSign**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o DocuSign, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no DocuSign é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no DocuSign precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no DocuSign.

tooconfigure e teste de logon único do AD do Azure com o DocuSign, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do DocuSign](#creating-a-docusign-test-user)**  -toohave um equivalente do Britta Simon no DocuSign que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do DocuSign.

**tooconfigure AD do Azure-logon único com o DocuSign, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **DocuSign** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base 64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. Em Olá **DocuSign configuração** seção do portal do Azure, clique em **DocuSign configurar** tooopen configurar o logon na janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**
    
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. Em uma janela de navegador web diferente, o logon tooyour **portal de administração do DocuSign** como um administrador.

6. No menu de navegação Olá Olá esquerda, clique em **domínios**.
   
    ![Configurando o logon único][51]

7. No painel direito da saudação, clique em **declaração domínio**.
   
    ![Configurando o logon único][52]

8. Em Olá **de declaração de um domínio** caixa de diálogo, na Olá **nome de domínio** caixa de texto, digite o domínio da sua empresa e, em seguida, clique em **declaração**. Certificar-se de que você verificar domínio hello e Olá status está ativo.
   
    ![Configurando o logon único][53]

9. No menu no lado esquerdo do hello, clique em **provedores de identidade**  
   
    ![Configurando o logon único][54]
10. No painel direito da saudação, clique em **Adicionar provedor de identidade**. 
   
    ![Configurando o logon único][55]

11. Em Olá **as configurações do provedor de identidade** página, execute Olá etapas a seguir:
   
    ![Configurando o logon único][56]

    a. Em Olá **nome** caixa de texto, digite um nome exclusivo para a sua configuração. Não use espaços.

    b. Colar **ID da entidade SAML** em Olá **emissor do provedor de identidade** caixa de texto.

    c. Colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon do provedor de identidade** caixa de texto.

    d. Colar **URL de logout** em Olá **URL de Logout do provedor de identidade** caixa de texto.

    e. Selecione **Assinar Solicitação AuthN**.

    f. Para **Enviar solicitação AuthN por**, selecione **POST**.

    g. Em **Enviar solicitação de logoff por**, selecione **GET**.

12. Em Olá **mapeamento de atributo personalizado** , escolha o campo Olá deseja toomap com declaração do AD do Azure. Neste exemplo, Olá **emailaddress** declaração é mapeada com valor de saudação do **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. É o nome da declaração saudação padrão do AD do Azure para declaração de email. 
   
    > [!NOTE]
    > Saudação de uso apropriada **identificador de usuário** toomap usuário de saudação do mapeamento de usuário do AD do Azure tooDocuSign. Selecione Olá campo apropriado e insira o valor apropriado de saudação com base nas configurações de sua organização.
          
    ![Configurando o logon único][57]

13. Em Olá **certificado do provedor de identidade** seção, clique em **Adicionar certificado**e, em seguida, carregue o certificado de saudação que baixou do portal do AD do Azure.   
   
    ![Configurando o logon único][58]

14. Clique em **Salvar**.

15. Em Olá **provedores de identidade** seção, clique em **ações**e, em seguida, clique em **pontos de extremidade**.   
   
    ![Configurando o logon único][59]
 
16. Em Olá **exibir pontos de extremidade do SAML 2.0** seção **portal de administração do DocuSign**, executar Olá etapas a seguir:
   
    ![Configurando o logon único][60]
   
    a. Saudação de cópia **URL do emissor de provedor de serviço**e, em seguida, cole a saudação **identificador** textbox em **DocuSign domínio e URLs** seção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Saudação de cópia **URL de logon do provedor de serviço**e, em seguida, cole a saudação **URL de logon** textbox em **DocuSign domínio e URLs** seção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Clique em **Fechar**
    
17. No portal do Azure de Olá, clique em **salvar**.
    
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-docusign-test-user"></a>Criando um usuário de teste do DocuSign

Aplicativo dá suporte a **apenas durante o provisionamento do usuário** e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooDocuSign seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooDocuSign, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **DocuSign**.

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco DocuSign Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour DocuSign aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

