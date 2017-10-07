---
title: "Tutorial: integração do Azure Active Directory ao Trello | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a>Tutorial: integração do Azure Active Directory ao Trello

Neste tutorial, você aprenderá como toointegrate Trello com o Azure Active Directory (AD do Azure).

Integrando Trello com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTrello
- Você pode habilitar seu usuários tooautomatically get conectado tooTrello (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Trello, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Trello habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Trello da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-trello-from-hello-gallery"></a>Adicionando Trello da Galeria de saudação
integração de saudação tooconfigure de Trello no AD do Azure, você precisa tooadd Trello da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Trello da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Trello**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. No painel de resultados de saudação, selecione **Trello**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Trello, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Trello é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Trello precisa toobe estabelecida.

Trello, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Trello, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Trello](#creating-a-trello-test-user)**  -toohave um equivalente do Britta Simon em Trello é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Trello.

**tooconfigure AD do Azure-logon único com Trello, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Trello** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. Em Olá **Trello domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, executar Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://trello.com/auth/saml/consume/<enterprise>`

4. Em Olá **Trello domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    a. Clique em Olá **Mostrar configurações de URL avançadas**.

    b. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://trello.com/auth/saml/consume/<enterprise>`

    >[!NOTE]
    >Você deve obter Olá  **\<enterprise\>**  espaçador de Trello. Se você não tiver o valor do campo de dados dinâmico Olá, entre em contato com [Trello a equipe de suporte](mailto:support@trello.com) tooget o campo de dados dinâmico Olá para você enterprise.
    > 

5. Aplicativo de Trello espera atributos específicos de toocontain Olá de asserções SAML. Configure Olá seguintes atributos para este aplicativo. Você pode gerenciar os valores hello desses atributos de saudação **"Atributos do usuário"** do aplicativo hello. Olá captura de tela a seguir mostra um exemplo.

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. Em Olá **atributos de tokens SAML** caixa de diálogo, para cada linha mostrada na tabela abaixo, a saudação execute Olá etapas a seguir:
 
    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | User.Email | user.mail |
    | User.FirstName | user.givenname |
    | User.LastName | user.surname |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha. 

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **OK**. 
 
7. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. Em Olá **Trello configuração** seção, clique em **configurar Trello** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. tooget SSO configurado para o seu aplicativo, vá muito[configuração de SSO enterprise Trello](https://trello.com/sso-configuration) página toosend [Trello a equipe de suporte](mailto:support@trello.com) Olá **Single Sign-On URL do serviço SAML** e Anexar Olá **certificado (Base64)**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-trello-test-user"></a>Criando um usuário de teste do Trello

Nesta seção, você cria um usuário chamado Brenda Fernandes no Trello. Nesta seção, você cria um usuário chamado Brenda Fernandes no Trello. Trello dá suporte ao provisionamento just-in-time e uma nova conta é criada primeira vez que entrar de saudação do AD do Azure.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTrello.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTrello, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Trello**.

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco Trello Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Trello aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

