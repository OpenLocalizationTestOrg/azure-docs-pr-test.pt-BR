---
title: "Tutorial: Integração do Azure Active Directory com o Lucidchart | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a>Tutorial: Integração do Active Directory do Azure com o Lucidchart

Neste tutorial, você aprenderá como toointegrate Lucidchart com o Azure Active Directory (AD do Azure).

Integrando o Lucidchart com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLucidchart
- Você pode habilitar seu usuários tooautomatically get conectado tooLucidchart (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Lucidchart, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Lucidchart com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Lucidchart da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-lucidchart-from-hello-gallery"></a>Adicionando Lucidchart da Galeria de saudação
integração de saudação tooconfigure do Lucidchart no AD do Azure, você precisa tooadd Lucidchart da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Lucidchart da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Lucidchart**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. No painel de resultados de saudação, selecione **Lucidchart**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Lucidchart, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Lucidchart é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Lucidchart precisa toobe estabelecida.

No Lucidchart, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Lucidchart, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Lucidchart](#creating-a-lucidchart-test-user)**  -toohave um equivalente do Britta Simon no Lucidchart é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Lucidchart.

**tooconfigure AD do Azure-logon único com o Lucidchart, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Lucidchart** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. Em Olá **Lucidchart domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL como:`https://chart2.office.lucidchart.com/saml/sso/azure`

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Lucidchart como administrador.

7. No menu de saudação na parte superior de saudação, clique em **equipe**.
   
    ![Equipe](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Equipe")

8. Clique em **Aplicativos \> Gerenciar SAML**.
   
    ![Gerenciar SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Gerenciar SAML")

9. Em Olá **configurações de autenticação SAML** caixa de diálogo de página, execute Olá etapas a seguir:
   
    a. Selecione **Habilitar Autenticação SAML** e clique em **Opcional**.

    ![Configurações de Autenticação SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Configurações de Autenticação SAML")
 
    b. Em Olá **domínio** caixa de texto, digite o seu domínio e, em seguida, clique em **alterar certificado**.

    ![Alterar Certificado](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Alterar Certificado")
 
    c. Abra o arquivo de metadados baixado, a saudação de copiar conteúda e, em seguida, cole-Olá **carregar metadados** caixa de texto.

    ![Carregar Metadados](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Carregar Metadados")
 
    d. Selecione **adicionar automaticamente novo agrupamento de usuários toohello**e, em seguida, clique em **salvar alterações**.

    ![Salvar Alterações](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Salvar Alterações")

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-lucidchart-test-user"></a>Criar um usuário de teste do Lucidchart

Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooLucidchart.  Quando um usuário atribuído tenta toolog no Lucidchart usando o painel de acesso hello, Lucidchart verifica se o usuário Olá existe.  

Se não houver conta de usuário ainda, ela é criada automaticamente pelo Lucidchart.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLucidchart.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLucidchart, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Lucidchart**.

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Lucidchart Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Lucidchart aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

