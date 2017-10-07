---
title: "Tutorial: Integração do Azure Active Directory com o Tableau Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Tutorial: Integração do Azure Active Directory com o Tableau Online

Neste tutorial, você aprenderá como toointegrate Tableau Online com o Azure Active Directory (AD do Azure).

Integrando Tableau Online com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTableau Online
- Você pode habilitar seu usuários tooautomatically get conectado tooTableau on-line (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Tableau Online, você precisará Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Tableau Online

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Tableau Online da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-tableau-online-from-hello-gallery"></a>Adicionando Tableau Online da Galeria de saudação
integração de saudação tooconfigure do Tableau Online no AD do Azure, você precisa tooadd Tableau Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Tableau on-line da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Tableau Online**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. No painel de resultados de saudação, selecione **Tableau Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Tableau Online, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Tableau Online é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Tableau Online precisa toobe estabelecida.

Tableau Online, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Tableau Online, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Online Tableau](#creating-a-tableau-online-test-user)**  -toohave um equivalente do Britta Simon em Tableau Online que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Tableau Online.

**tooconfigure AD do Azure-logon único com Tableau Online, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Tableau Online** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. Em Olá **URLs e domínio Online Tableau** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://sso.online.tableau.com`

    b. Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://sso.online.tableau.com/public/sp/<instancename>`

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. Em uma janela de navegador diferente, logon tooyour aplicativo Tableau Online. Vá muito**configurações** e **autenticação**.
   
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML, em **tipos de autenticação** seção. Verificar Olá **logon único com SAML** caixa de seleção.
   
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Role para baixo até a seção **Import metadata file into Tableau Online** .  Clique em Procurar e importe o arquivo de metadados de saudação que baixou do AD do Azure. Em seguida, clique em **Apply**.
   
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. Em Olá **corresponder asserções** seção, insira o nome asserção provedor de identidade de saudação correspondente para **endereço de email**, **nome**, e **sobrenome** . tooget essas informações do AD do Azure: 
  
    a. No hello portal do Azure, vá Olá **Tableau Online** página de integração de aplicativos.
    
    b. Na seção de atributos de saudação, selecione Olá **"Exibir e editar todos os outros atributos de usuário"** caixa de seleção. 
    
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Copie o valor do namespace Olá para esses atributos: givenname, email e sobrenome usando Olá seguintes etapas:

   ![Logon Único do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. Clique no valor **user.givenname** 
    
    e. Copie o valor de saudação da saudação **namespace** caixa de texto.

   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. valores de namesapce toocopy Olá para email hello e sobrenome siga Olá etapas anteriores.

    g. Alternar aplicativo Online Tableau toohello, então, configurar Olá **atributos Online Tableau** seção da seguinte maneira:
     * Email: **mail** ou **userprincipalname**
     * Nome: **givenname**
     * Sobrenome: **surname**
   
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-tableau-online-test-user"></a>Criação de um usuário de teste do Tableau Online

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tableau Online.

1. No **Tableau Online**, clique em **Configurações** e na seção **Autenticação**. Role para baixo demais**selecionar usuários** seção. Clique em **Adicionar Usuários** e em **Inserir Endereços de Email**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Selecione **Adicionar usuários para autenticação de logon único (SSO)**. Em Olá **insira endereços de Email** Adicionar caixa de textobritta.simon@contoso.com
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. Clique em **Criar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTableau on-line.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTableau Online, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Tableau Online**.

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco Tableau Online Olá Olá painel de acesso, você deve obter aplicativo Tableau Online automaticamente assinado em tooyour.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

