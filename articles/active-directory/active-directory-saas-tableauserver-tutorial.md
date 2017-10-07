---
title: "Tutorial: Integração do Azure Active Directory ao Tableau Server | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tableau Server."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>Tutorial: Integração do Azure Active Directory ao Tableau Server

Neste tutorial, você aprenderá como toointegrate Tableau Server com o Azure Active Directory (AD do Azure).

Integrando Tableau servidor com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTableau Server
- Você pode habilitar seu usuários tooautomatically get conectado tooTableau servidor (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o servidor Tableau, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Tableau Server

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Tableau Server da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-tableau-server-from-hello-gallery"></a>Adicionando Tableau Server da Galeria de saudação
integração de saudação tooconfigure do servidor Tableau no AD do Azure, você precisa tooadd Tableau servidor da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Tableau Server da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Tableau Server**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. No painel de resultados de saudação, selecione **Tableau servidor**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Tableau Server, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no servidor Tableau é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no servidor Tableau precisa toobe estabelecida.

No servidor Tableau, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o servidor Tableau, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do servidor Tableau](#creating-a-tableau-server-test-user)**  -toohave um equivalente do Britta Simon no servidor Tableau toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de servidor Tableau.

**tooconfigure AD do Azure-logon único com o servidor Tableau, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Tableau servidor** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. Em Olá **Tableau o domínio do servidor e as URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://azure.<domain name>.link`
    
    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://azure.<domain name>.link`

    c. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > Olá anteriores valores não são valores reais. Posteriormente, você atualiza valores hello com URL real hello e o identificador de página de configuração do servidor de Tableau de saudação. 

4. Aplicativo de servidor tableau espera as asserções de SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de saudação **"Atributos do usuário"** seção na página de integração de aplicativos. Olá, seguinte captura de tela mostra um exemplo de hello mesmo.
    
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | ---------------| --------------- |    
    | Nome de Usuário | *user.displayname* |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**


6. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget SSO configurado para o seu aplicativo, você precisa de locatário de servidor Tableau toosign em tooyour como um administrador.
   
   a. Configuração de servidor Tableau hello, clique em Olá **SAML** guia.
  
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. Selecione caixa de seleção de saudação do **SAML de uso para o logon único**.
   
   c. URL de retorno de servidor tableau — Olá URL que os usuários Tableau Server acessará, como http://tableau_server. Não é recomendável usar http://localhost. O uso de URL com barra à direita (por exemplo, http://tableau_server/) não é aceito. Cópia **URL de retorno de servidor Tableau** e cole-o tooAzure AD **URL de logon** textbox em **Tableau o domínio do servidor e as URLs** seção.
   
   d. ID de entidade SAML, ID da entidade Olá identifica exclusivamente a instalação de servidor Tableau toohello IdP. Você pode inserir a URL do servidor Tableau novamente aqui, se desejar, mas ele não tem toobe a URL do servidor Tableau. Cópia **ID da entidade SAML** e cole-o tooAzure AD **identificador** textbox em **Tableau o domínio do servidor e as URLs** seção.
     
   e. Clique em Olá **Exportar arquivo de metadados** e abri-lo no aplicativo de editor de texto de saudação. Localize o URL do serviço de consumidor de declaração com Http Post e índice 0 e copiar Olá URL. Agora colar tooAzure AD **URL de resposta** textbox em **Tableau o domínio do servidor e as URLs** seção.
   
   f. Localize o arquivo de metadados de federação que baixou do portal do Azure e, em seguida, carregá-lo no hello **arquivo de metadados Idp SAML**.
   
   g. Clique em Olá **Okey** botão na página de configuração do servidor Tableau hello.
   
    >[!NOTE] 
    >Cliente tem tooupload nenhum certificado na configuração de SSO do SAML Server Tableau hello e ele será obter ignorado em Olá fluxo SSO.
    >Se você precisar ajudar a configurar o SAML no servidor Tableau, consulte o artigo toothis [configurar SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).
    >
<CE>

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-tableau-server-test-user"></a>Criação de um usuário de teste do Tableau Server

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no servidor Tableau. É necessário tooprovision todos os usuários de saudação no servidor de Tableau hello. 

Esse nome de usuário de saudação deve corresponder o valor de saudação que você configurou no atributo personalizado de saudação do AD do Azure de **nome de usuário**. Com hello correto de mapeamento de integração Olá deve funcionar [Configurando o AD do Azure Single Sign-On](#configuring-azure-ad-single-sign-on).

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, é necessário ter toocontact Olá Tableau Server administrador em sua organização.
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTableau Server.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTableau Server, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Tableau Server**.

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Tableau Server Olá Olá painel de acesso, você deve obter um aplicativo de servidor Tableau tooyour automaticamente conectado em.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

