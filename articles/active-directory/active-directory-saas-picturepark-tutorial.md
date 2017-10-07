---
title: "Tutorial: Integração do Azure Active Directory ao Picturepark | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Tutorial: Integração do Azure Active Directory ao Picturepark

Neste tutorial, você aprenderá como toointegrate Picturepark com o Azure Active Directory (AD do Azure).

Integrando o Picturepark com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooPicturepark
- Você pode habilitar seu usuários tooautomatically get conectado tooPicturepark (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Picturepark, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Picturepark

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Picturepark da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-picturepark-from-hello-gallery"></a>Adicionando Picturepark da Galeria de saudação
integração de saudação tooconfigure do Picturepark no AD do Azure, você precisa tooadd Picturepark da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Picturepark da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Picturepark**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. No painel de resultados de saudação, selecione **Picturepark**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Picturepark, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Picturepark é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Picturepark precisa toobe estabelecida.

No Picturepark, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Picturepark, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Picturepark](#creating-a-picturepark-test-user)**  -toohave um equivalente do Britta Simon no Picturepark é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Picturepark.

**tooconfigure AD do Azure-logon único com o Picturepark, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Picturepark** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. Em Olá **Picturepark domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.picturepark.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente do Picturepark](https://picturepark.com/about/contact/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. Em Olá **Picturepark configuração** seção, clique em **configurar Picturepark** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Picturepark como administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em **ferramentas administrativas**e, em seguida, clique em **Console de gerenciamento**.
   
    ![Console de Gerenciamento](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console de Gerenciamento")

9. Clique em **Autenticação** e em **Provedores de identidade**.
   
    ![Autenticação](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticação")

10. Em Olá **configuração do provedor de identidade** , execute Olá etapas a seguir:
   
    ![Configuração do Provedor de Identidade](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuração do Provedor de Identidade")
   
    a. Clique em **Adicionar**.
  
    b. Digite um nome para sua configuração.
   
    c. Selecione **Definir como padrão**.
   
    d. Em **URI do emissor** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
    e. Em **impressão digital do emissor confiável** caixa de texto valor Olá colar **impressão digital** que você copiou de **o certificado de autenticação SAML** seção. 

11. Clique em **JoinDefaultUsersGroup**.

12. Olá tooset **Emailaddress** atributo Olá **declaração** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e clique em **salvar**.

      ![Configuração](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuração")

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-picturepark-test-user"></a>Criando um usuário de teste do Picturepark

Ordem tooenable AD do Azure usuários toolog no Picturepark, eles devem ser provisionados no Picturepark. No caso de saudação do Picturepark, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Picturepark** locatário.

2. Na barra de ferramentas de saudação na parte superior do hello, clique em **ferramentas administrativas**e, em seguida, clique em **usuários**.
   
    ![Usuários](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Usuários")

3. Em Olá **visão geral sobre usuários** , clique em **novo**.
   
    ![Gerenciamento de usuário](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gerenciamento de usuário")

4. Em Olá **Create User** caixa de diálogo, executar Olá seguindo as etapas de um válida do Azure Active Directory usuário você deseja tooprovision:
   
    ![Criar usuário](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Criar usuário")
   
    a. Em Olá **endereço de Email** caixa de texto, Olá tipo **endereço de email** do usuário Olá  **BrittaSimon@contoso.com** .  
   
    b. Em Olá **senha** e **Confirmar senha** caixas de texto, Olá tipo **senha** de BrittaSimon. 
   
    c. Em Olá **nome** caixa de texto, Olá tipo **nome** do usuário Olá **Britta**. 
   
    d. Em Olá **Sobrenome** caixa de texto, Olá tipo **Sobrenome** do usuário Olá **Simon**.
   
    e. Em Olá **empresa** caixa de texto, Olá tipo **nome da empresa** do usuário hello. 
   
    f. Em Olá **país** caixa de texto, selecione Olá **país** do usuário hello.
  
    g. Em Olá **ZIP** caixa de texto, Olá tipo **CEP** de cidade hello.
   
    h. Em Olá **Cidade** caixa de texto, Olá tipo **nome da cidade** do usuário hello.

    i. Selecione um **Idioma**.
   
    j. Clique em **Criar**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Picturepark usuário conta ou APIs fornecidas pelo Picturepark tooprovision contas de usuário do AD do Azure.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPicturepark.

![Atribuir usuário][200] 

**tooassign Britta Simon tooPicturepark, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Picturepark**.

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Picturepark Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Picturepark aplicativo. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

