---
title: "Tutorial: integração do Azure Active Directory com a Adobe Creative Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Adobe criativos da nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Tutorial: integração do Azure Active Directory com a Adobe Creative Cloud

Neste tutorial, você aprenderá como toointegrate Adobe Creative nuvem com o Azure Active Directory (AD do Azure).

Integração do Adobe criativos da nuvem com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAdobe criativos da nuvem
- Você pode habilitar seu usuários tooautomatically get conectado tooAdobe criativos da nuvem (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Adobe criativos da nuvem, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura da Creative Cloud habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Adobe criativos da nuvem da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Adicionando Adobe criativos da nuvem da Galeria de saudação
integração de saudação tooconfigure do Adobe criativos da nuvem no Azure AD, é necessário tooadd Adobe criativos da nuvem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Adobe criativos da nuvem da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Adobe criativos da nuvem**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. No painel de resultados de saudação, selecione **Adobe criativos da nuvem**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com a Adobe Creative Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Adobe criativos da nuvem é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Adobe criativos da nuvem precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Adobe criativos da nuvem.

tooconfigure e teste de logon único do AD do Azure com Adobe criativos da nuvem, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Adobe criativos da nuvem](#creating-an-adobe-creative-cloud-test-user)**  -toohave um equivalente do Britta Simon no Adobe criativos da nuvem que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Adobe criativos da nuvem.

**tooconfigure logon único do AD do Azure com Adobe criativos da nuvem, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **Adobe criativos da nuvem** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Em Olá **Adobe Creative nuvem domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. Em Olá **identificador** texto, o valor do tipo hello como:`https://www.okta.com/saml2/service-provider/<token>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação. Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação. Se você precisar toocreate um usuário manualmente, é necessário a equipe de suporte do toocontact Olá Adobe criativos da nuvem.

4. Em Olá **Adobe Creative nuvem domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Clique em Olá **Mostrar configurações de URL avançadas** opção

    b. Em Olá **URL de logon** texto, o valor do tipo hello como:`https://adobe.com`

5. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Em Olá **Adobe Creative configuração de nuvem** seção, clique em **configurar Adobe criativos da nuvem** tooopen **configurar o logon** janela. Copie Olá **Id da entidade SAML** e **URL do serviço SSO do SAML** da seção de referência rápida.

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. Em uma janela de navegador web diferente, locatário de nuvem Creative Adobe tooyour logon como administrador.

8.  Vá muito**identidade** Olá painel de navegação esquerdo e clique em seu domínio. Em seguida, executar Olá seguindo as etapas na **logon único na configuração necessária** seção.

    ![Configurações](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Configurações")

9. Clique em **procurar** Olá tooupload baixado certificado do AD do Azure muito**certificado IDP**.

10. Em Olá **emissor IDP** caixa de texto, coloque o valor de saudação do **Id da entidade SAML** que você copiou de **configurar o logon** seção no portal do Azure.

11. Em Olá **URL de logon IDP** caixa de texto, coloque o valor de saudação do **URL do serviço SSO do SAML** que você copiou de **configurar o logon** seção no portal do Azure.

12. Selecione **Redirecionamento HTTP** como **Associação IdP**.

13. Selecione **Endereço de email** como **Configuração de logon do usuário**.
 
14. Clique no botão **Salvar** .

15. painel Olá agora apresentará Olá XML **"Baixar metadados"** arquivo. Ele contém a URL EntityDescriptor e a URL AssertionConsumerService da Adobe. Abra arquivo hello e configurá-las no hello aplicativo AD do Azure.

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Olá Use EntityDescriptor valor Adobe fornecida por **identificador** em Olá **definir configurações de aplicativo** caixa de diálogo.

    b. Olá Use AssertionConsumerService valor Adobe fornecida por **URL de resposta** em Olá **definir configurações de aplicativo** caixa de diálogo.
 
### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Criando um usuário de teste da Adobe Creative Cloud

Em ordem tooenable AD do Azure usuários toolog em Adobe criativos da nuvem, eles devem ser provisionados no Adobe criativos da nuvem.  
No caso de saudação do Adobe criativos da nuvem, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon tooyour site de empresa do Adobe criativos da nuvem como um administrador.

2. Clique em **Pessoas**.

    ![Pessoas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Pessoas")

3. Clique em **Convidar Usuário**.

    ![Convidar Usuários](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Convidar Usuários")

4. Em Olá **convidar pessoas** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Convidar Pessoas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Convidar Pessoas")

    a. Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.
    
    b. Clique em **Convidar**.

    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooAdobe seu acesso criativos da nuvem.

![Atribuir usuário][200] 

**tooassign Britta Simon tooAdobe criativos da nuvem, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Adobe criativos da nuvem**.

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Adobe criativos da nuvem Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Adobe criativos da nuvem.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png