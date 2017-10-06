---
title: "Tutorial: Integração do Azure Active Directory ao PolicyStat | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Tutorial: Integração do Azure Active Directory ao PolicyStat

Neste tutorial, você aprenderá como toointegrate PolicyStat com o Azure Active Directory (AD do Azure).

Integrando PolicyStat com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooPolicyStat
- Você pode habilitar seu usuários tooautomatically get conectado tooPolicyStat (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com PolicyStat, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do PolicyStat

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando PolicyStat da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-policystat-from-hello-gallery"></a>Adicionando PolicyStat da Galeria de saudação
integração de saudação tooconfigure de PolicyStat no AD do Azure, você precisa tooadd PolicyStat da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd PolicyStat da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **PolicyStat**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. No painel de resultados de saudação, selecione **PolicyStat**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o PolicyStat, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em PolicyStat é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em PolicyStat precisa toobe estabelecida.

PolicyStat, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com PolicyStat, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste PolicyStat](#creating-a-policystat-test-user)**  -toohave um equivalente do Britta Simon em PolicyStat é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo PolicyStat.

**tooconfigure AD do Azure-logon único com PolicyStat, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **PolicyStat** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. Em Olá **PolicyStat domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.policystat.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente PolicyStat](http://www.policystat.com/support/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooPolicyStat com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

    Olá PolicyStat aplicativo espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens SAML** configuração.  

     Olá captura de tela a seguir mostra um exemplo disso.

     ![Atributos](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Atributos")

6. mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:

    | Nome do atributo    |   Valor do atributo |
    |------------------- | -------------------- |
    | uid | ExtractMailPrefix([mail]) |
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. Em Olá **nome do atributo** caixa de texto, tipo **uid**.

    c. Em Olá **o valor do atributo** caixa de texto, selecione **ExtractMailPrefix()**.    
   
    d. De saudação **Mail** lista, selecione **User.mail**.
    
    e. Clique em **Ok**

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do PolicyStat como administrador.

9. Clique em Olá **Admin** guia e, em seguida, clique em **configuração de logon único** no painel de navegação esquerdo.
   
    ![Menu Administrador](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu Administrador")

10. Em Olá **instalação** seção, selecione **integração de logon único habilitar**.
   
    ![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuração de Logon Único")

11. Clique em **configurar atributos**e em seguida, no hello **configurar atributos** , execute Olá etapas a seguir:
   
    ![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuração de Logon Único")
   
    a. Em Olá **atributo Username** caixa de texto, tipo **uid**.

    b. Em Olá **atributo de nome** caixa de texto, tipo **firstname** do usuário **Britta**.

    c. Em Olá **último nome de atributo** caixa de texto, tipo **lastname** do usuário **Simon**.

    d. Em Olá **Email atributo** caixa de texto, tipo **emailaddress** do usuário  **BrittaSimon@contoso.com** .

    e. Clique em **Salvar Alterações**.

12. Clique em **seus metadados de IDP**e em seguida, no hello **seus metadados de IDP** , execute Olá etapas a seguir:
   
    ![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuração de Logon Único")
   
    a. Abra o arquivo de metadados baixado, a saudação de copiar conteúda e, em seguida, cole-Olá **o metadados do provedor de identidade** caixa de texto.

    b. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-policystat-test-user"></a>Criando um usuário de teste do PolicyStat

Em ordem tooenable AD do Azure usuários toolog em PolicyStat, eles devem ser provisionados no PolicyStat.  

O PolicyStat dá suporte ao provisionamento de usuário just in time. Isso significa que, você não precisa usuários de saudação tooadd manualmente tooPolicyStat. os usuários de saudação serão serão adicionados automaticamente no seu primeiro logon por meio do SSO.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros PolicyStat usuário conta ou APIs fornecidas pelo PolicyStat tooprovision contas de usuário do AD do Azure.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPolicyStat.

![Atribuir usuário][200] 

**tooassign Britta Simon tooPolicyStat, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **PolicyStat**.

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco PolicyStat Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour PolicyStat aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

