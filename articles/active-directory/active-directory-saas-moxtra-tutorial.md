---
title: "Tutorial: Integração do Azure Active Directory com o Moxtra | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Tutorial: integração do Active Directory do Azure ao Moxtra

Neste tutorial, você aprenderá como toointegrate o Moxtra com o Azure Active Directory (AD do Azure).

Integrando o Moxtra com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooMoxtra
- Você pode habilitar seu usuários tooautomatically get conectado tooMoxtra (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Moxtra, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Moxtra

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o Moxtra da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-moxtra-from-hello-gallery"></a>Adicionando o Moxtra da Galeria de saudação
integração de saudação tooconfigure do Moxtra no AD do Azure, você precisa tooadd o Moxtra da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd o Moxtra da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **o Moxtra**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. No painel de resultados de saudação, selecione **o Moxtra**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Moxtra, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Moxtra é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Moxtra precisa toobe estabelecida.

O Moxtra, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Moxtra, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste o Moxtra](#creating-a-moxtra-test-user)**  -toohave um equivalente do Britta Simon no Moxtra que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo o Moxtra.

**tooconfigure AD do Azure-logon único com o Moxtra, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **o Moxtra** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. Em Olá **o Moxtra domínio e URLs** , execute Olá etapa a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL como:`https://www.moxtra.com/service/#login`

4. O Moxtra aplicativo espera as asserções de SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo para essa configuração. 

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | ------------------- | -------------------- |    
    | nome | user.givenname |
    | sobrenome | user.surname |
    | idpid    | <ID da Entidade SAML> 

    > [!Note]
    > Olá valor **idpid** atributo não é real. Você pode obter o valor real de saudação do **referência rápida** seção em **o Moxtra configuração**.
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.

    d. Clique em **OK**.
    
5. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. Em Olá **configuração o Moxtra** seção, clique em **o Moxtra configurar** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. Em outra janela do navegador, entre no site da empresa tooyour o Moxtra como um administrador.

9. Na barra de ferramentas Olá Olá esquerda, clique em **Console de Administração > logon único do SAML**e, em seguida, clique em **novo**.
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. Em Olá **SAML** página, execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: *SAML*). 
  
    b. Em hello **ID da entidade IdP** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure. 
 
    c. Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure. 
 
    d. Em Olá **AuthnContextClassRef** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:ac:classes:Password**. 
 
    e. Em Olá **formato NameID** caixa de texto, tipo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: emailAddress**. 
 
    f. Abra certificado que você baixou do portal do Azure no bloco de notas, copie o conteúdo de saudação e, em seguida, cole-o em Olá **certificado** caixa de texto.    
 
    g. No domínio de email SAML de saudação texto, digite seu domínio de email SAML.    
  
    >[!NOTE]
    >domínio de saudação do tooverify toosee Olá etapas, clique em hello "****" abaixo.

    h. Clique em **Atualizar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-moxtra-test-user"></a>Criar um usuário de teste Moxtra

Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no Moxtra.

**toocreate um usuário chamado Britta Simon no Moxtra, execute Olá etapas a seguir:**

1. Faça logon no tooyour o Moxtra site da empresa como um administrador.

2. Na barra de ferramentas Olá Olá esquerda, clique em **Console de Administração > Gerenciamento de usuário**e, em seguida, **adicionar usuário**.
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:
  
    a. Em Olá **nome** caixa de texto, tipo **Britta**.
  
    b. Em Olá **Sobrenome** caixa de texto, tipo **Simon**.
  
    c. Em Olá **Email** caixa de texto, tipo de endereço de email de Britta igual em portal do Azure.
  
    d. Em Olá **divisão** caixa de texto, tipo **desenvolvimento**.
  
    e. Em Olá **departamento** caixa de texto, tipo **IT**.
  
    f. Selecione **Administrator**.
  
    g. Clique em **Adicionar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMoxtra.

![Atribuir usuário][200] 

**tooassign Britta Simon tooMoxtra, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **o Moxtra**.

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco o Moxtra Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour o Moxtra aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

