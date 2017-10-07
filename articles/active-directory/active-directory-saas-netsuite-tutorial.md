---
title: "Tutorial: Integração do Azure Active Directory com o NetSuite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Tutorial: Integração do Azure Active Directory com o Netsuite

Neste tutorial, você aprenderá como toointegrate Netsuite com o Azure Active Directory (AD do Azure).

Integrando o Netsuite com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooNetsuite
- Você pode habilitar seu usuários tooautomatically get conectado tooNetsuite (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Netsuite, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Netsuite

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Netsuite da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-netsuite-from-hello-gallery"></a>Adicionando Netsuite da Galeria de saudação
integração de saudação tooconfigure do Netsuite no AD do Azure, você precisa tooadd Netsuite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Netsuite da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Netsuite**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. No painel de resultados de saudação, selecione **Netsuite**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Netsuite, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Netsuite é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Netsuite precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Netsuite.

tooconfigure e teste de logon único do AD do Azure com o Netsuite, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Netsuite](#creating-a-netsuite-test-user)**  -toohave um equivalente do Britta Simon no Netsuite é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Netsuite.

**tooconfigure AD do Azure-logon único com o Netsuite, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Netsuite** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. Em Olá **Netsuite domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Esse valor não é o valor real. Valor de saudação de atualização com hello URL de resposta real. Entre em contato com [equipe de suporte do Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget esse valor.
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. Em Olá **Netsuite configuração** seção, clique em **configurar Netsuite** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Abra uma nova guia no navegador e entre no site Netsuite de sua empresa como administrador.

8. Na barra de ferramentas de saudação na parte superior de saudação da página de saudação, clique em **instalação**, em seguida, clique em **Gerenciador de instalação**.

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. De saudação **tarefas de configuração** lista, selecione **integração**.

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. Em Olá **gerenciar autenticação** seção, clique em **o logon único do SAML**.

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. Em Olá **instalação do SAML** página, execute Olá etapas a seguir:
   
    a. Saudação de cópia **Single Sign-On URL do serviço SAML** o valor da **referência rápida** seção **configurar o logon** e cole-a saudação **provedor de identidade Página de logon** campo Netsuite.

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. No NetSuite, selecione **Método de Autenticação Primária**.

    c. Para o campo de saudação rotulado **metadados do provedor de identidade SAMLV2**, selecione **carregar arquivo de metadados IDP**. Em seguida, clique em **procurar** arquivo de metadados de saudação tooupload que baixou do portal do Azure.

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Clique em **Enviar**.

12. No Azure AD, clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** e adicione um atributo.

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Para Olá **nome do atributo** , digite em `account`. Para Olá **o valor do atributo** , digite sua ID de conta do Netsuite Esse valor é constante e alteração de conta. Instruções sobre como toofind sua ID da conta estão incluídas abaixo:

      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. No Netsuite, clique em **instalação** no menu de navegação superior hello.

    b. Em seguida, clique em Olá **tarefas de configuração** seção do menu de navegação à esquerda hello, selecione Olá **integração** seção e, em seguida, clique em **preferências de serviços Web**.

    c. Copie a ID da conta Netsuite e cole-a saudação **o valor do atributo** campo no AD do Azure.

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Antes dos usuários podem executar logon único no Netsuite, eles devem primeiro atribua Olá permissões apropriadas no Netsuite. Siga as instruções de saudação abaixo tooassign essas permissões.

    a. No menu de navegação superior hello, clique em **instalação**, em seguida, clique em **Gerenciador de instalação**.
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. No menu de navegação à esquerda do hello, selecione **usuários/funções**, em seguida, clique em **gerenciar funções**.
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Clique em **Nova Função**.

    d. Digite um **nome** de nova função e selecione Olá **Single Sign-On somente** caixa de seleção.
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Clique em **Salvar**.

    f. No menu de saudação na parte superior de saudação, clique em **permissões**. Em seguida, clique em **Instalação**.
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Selecione **Instalar o Logon Único do SAM** e, em seguida, clique em **Adicionar**.

    h. Clique em **Salvar**.

    i. No menu de navegação superior hello, clique em **instalação**, em seguida, clique em **Gerenciador de instalação**.
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. No menu de navegação à esquerda do hello, selecione **usuários/funções**, em seguida, clique em **gerenciar usuários**.
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Selecione um usuário de teste. Em seguida, clique em **Editar**.
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. Na caixa de diálogo de funções hello, selecione função hello que você criou e clique em **adicionar**.
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Clique em **Salvar**.
    
> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 

### <a name="creating-a-netsuite-test-user"></a>Criando um usuário de teste do Netsuite

Nesta seção, um usuário chamado Brenda Fernandes é criado no Netsuite. O Netsuite dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.
Não há itens de ação para você nesta seção. Se um usuário não existir no Netsuite, um novo é criado quando você tenta tooaccess Netsuite.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNetsuite.

![Atribuir usuário][200] 

**tooassign Britta Simon tooNetsuite, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Netsuite**.

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

tootest seu único-configurações de logon, abra Olá painel de acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), entre na conta de teste hello e clique em **Netsuite**.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

