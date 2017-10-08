---
title: "Tutorial: Integração do Azure Active Directory ao Halogen Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e alogênio Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a>Tutorial: Integração do Active Directory do Azure com o Halogen Software

Neste tutorial, você aprenderá como toointegrate alogênio Software com o Azure Active Directory (AD do Azure).

Integração do Software alogênio com o Azure AD fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHalogen Software
- Você pode habilitar seu usuários tooautomatically get conectado tooHalogen Software (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com halogênio Software, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Halogen Software com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Software alogênio da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-halogen-software-from-hello-gallery"></a>Adicionar Software alogênio da Galeria de saudação

integração de saudação tooconfigure do Software alogênio no AD do Azure, você precisa tooadd alogênio Software na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Software alogênio da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **alogênio Software**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. No painel de resultados de saudação, selecione **alogênio Software**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Halogen Software com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Software alogênio é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Software alogênio precisa toobe estabelecida.

No Software de alogênio, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com halogênio Software, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de Software alogênio](#creating-a-halogen-software-test-user)**  -toohave um equivalente do Britta Simon no Software alogênio toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo alogênio.

**tooconfigure AD do Azure-logon único com o Software de alogênio, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **alogênio Software** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. Em Olá **alogênio Software domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://global.hgncloud.com/<companyname>`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [a equipe de suporte do cliente de Software alogênio](https://support.halogensoftware.com/) tooget esses valores. 
 


4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. Em uma janela de navegador diferente, logon tooyour **alogênio Software** aplicativo como um administrador.

7. Clique em Olá **opções** guia. 
   
    ![O que é o Azure AD Connect][12]

8. No painel de navegação esquerdo hello, clique em **configuração SAML**. 
   
    ![O que é o Azure AD Connect][13]

9. Em Olá **configuração SAML** página, execute Olá etapas a seguir: 

    ![O que é o Azure AD Connect][14]

     a. Como **Identificador exclusivo**, selecione **NameID**.

     b. Em **Identificador exclusivo mapeia para**, selecione **Nome de usuário**.
  
     c. tooupload seu arquivo de metadados baixado, clique em **procurar** tooselect arquivo de saudação e, em seguida, **carregar arquivo**.
 
     d. configuração de saudação tootest, clique em **executar teste**. 
    
    >[!NOTE]
    >Você precisa toowait para mensagem de saudação "*Olá SAML teste for concluído. Feche esta janela*". Em seguida, feche a janela de navegador aberta de saudação. Olá **habilitar SAML** caixa de seleção só estará habilitada se o teste de saudação foi concluída. 
     
     e. Selecione **Habilitar SAML**.
    
     f. Clique em **Salvar Alterações**. 

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto Nome do tipo como **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-halogen-software-test-user"></a>Criação de um usuário de teste do Halogen Software

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon alogênio software.

**toocreate um usuário chamado Britta Simon no Software de alogênio execute Olá etapas a seguir:**

1. Logon tooyour **alogênio Software** aplicativo como um administrador.

2. Clique em Olá **usuário Center** guia e, em seguida, clique em **Create User**.
   
    ![O que é o Azure AD Connect][300]  

3. Em Olá **novo usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![O que é o Azure AD Connect][301]

    a. Em Olá **nome** caixa de texto, nome do primeiro tipo de usuário hello como **Britta**.
    
    b. Em Olá **Sobrenome** caixa de texto, digite sobrenome do usuário hello como **Simon**. 

    c. Em Olá **Username** caixa de texto, tipo **Britta Simon**, nome de usuário hello como Olá portal do Azure.

    d. Em Olá **senha** caixa de texto, digite uma senha para Britta.
    
    e. Clique em **Salvar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHalogen Software.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHalogen Software, executar Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **alogênio Software**.

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco alogênio Software Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Software alogênio.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
