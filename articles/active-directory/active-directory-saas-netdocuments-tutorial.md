---
title: "Tutorial: Integração do Azure Active Directory ao NetDocuments | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a>Tutorial: Integração do Active Directory do Azure com o NetDocuments

Neste tutorial, você aprenderá como toointegrate NetDocuments com o Azure Active Directory (AD do Azure).

Integrando o NetDocuments com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooNetDocuments
- Você pode habilitar seus usuários tooautomatically get conectado tooNetDocuments (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o NetDocuments, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do NetDocuments

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando NetDocuments da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-netdocuments-from-hello-gallery"></a>Adicionando NetDocuments da Galeria de saudação
integração de saudação tooconfigure do NetDocuments no AD do Azure, você precisa tooadd NetDocuments da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd NetDocuments da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **NetDocuments**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. No painel de resultados de saudação, selecione **NetDocuments**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o NetDocuments, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no NetDocuments é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no NetDocuments precisa toobe estabelecida.

No NetDocuments, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o NetDocuments, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do NetDocuments](#creating-a-netdocuments-test-user)**  -toohave um equivalente do Britta Simon no NetDocuments é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo NetDocuments.

**tooconfigure AD do Azure-logon único com o NetDocuments, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **NetDocuments** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. Em Olá **NetDocuments domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de logon real hello e a URL de resposta. Entre em contato com [equipe de suporte do NetDocuments](https://support.netdocuments.com/hc/) tooget esses valores.
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do NetDocuments como administrador.

7. Vá muito**Admin**.

8. Clique em **Adicionar e remover usuários e grupos**.
   
    ![Repositório](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositório")

9. Clique em **Configurar opções de autenticação avançadas**.
    
    ![Configurar opções de autenticação avançadas](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurar opções de autenticação avançadas")

10. Em Olá **identidade federada** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Identidade Federada](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identidade Federada")
   
    a. Para **Tipo de servidor de identidade federada**, selecione **Serviços de Federação do Active Directory**.
   
    b. Clique em **Escolher arquivo**, Olá tooupload baixou o arquivo de metadados que você baixou do portal do Azure.
   
    c. Clique em **OK**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-netdocuments-test-user"></a>Criar um usuário de teste do NetDocuments

tooenable AD do Azure usuários toolog em tooNetDocuments, eles devem ser provisionados no NetDocuments.  
No caso de saudação do NetDocuments, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Tocar em tooyour **NetDocuments** site da empresa como administrador.

2. No menu de saudação na parte superior de saudação, clique em **Admin**.
   
    ![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")

3. Clique em **Adicionar e remover usuários e grupos**.
   
    ![Repositório](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositório")

4. Em Olá **endereço de Email** caixa de texto, digite o endereço de email de Olá de uma conta válida do Active Directory do Azure você deseja tooprovision e, em seguida, clique em **adicionar usuário**.
   
    ![Endereço de Email](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Endereço de Email")
   
   >[!NOTE]
   >proprietário de conta do Active Directory do Azure Olá receberá um email que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa. Você pode usar qualquer ferramenta de criação outros NetDocuments usuário conta ou APIs fornecidas pela NetDocuments tooprovision Azure Active Directory as contas de usuário.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNetDocuments.

![Atribuir usuário][200] 

**tooassign Britta Simon tooNetDocuments, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **NetDocuments**.

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá NetDocuments bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo NetDocuments.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

