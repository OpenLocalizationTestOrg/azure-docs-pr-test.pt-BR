---
title: "Tutorial: integração do Azure Active Directory ao LinkedInSalesNavigator | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a>Tutorial: integração do Azure Active Directory com o LinkedIn Sales Navigator

Neste tutorial, você aprenderá como toointegrate LinkedIn vendas navegador com o Azure Active Directory (AD do Azure).

Integrando LinkedIn vendas navegador com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLinkedIn navegador de vendas
- Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn navegador de vendas (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, procurar [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o navegador de vendas LinkedIn, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do LinkedIn Sales Navigator com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Evite usar o ambiente de produção a menos que necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando LinkedIn vendas navegador da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a>Adicionando LinkedIn vendas navegador da Galeria de saudação
integração de saudação tooconfigure do navegador de vendas LinkedIn no AD do Azure, você precisa tooadd LinkedIn vendas navegador na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd LinkedIn navegador de vendas da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **LinkedIn vendas navegador**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. No painel de resultados de saudação, selecione **LinkedIn vendas navegador**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Sales Navigator, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no navegador de vendas LinkedIn é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no navegador de vendas LinkedIn precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no navegador de vendas do LinkedIn.

tooconfigure e teste de logon único do AD do Azure com o navegador de vendas LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do navegador de vendas LinkedIn](#creating-a-linkedin-sales-navigator-test-user)**  -toohave um equivalente do Britta Simon no navegador de vendas LinkedIn que é vinculado toohello AD do Azure representação do usuário hello.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de navegador de vendas do LinkedIn.

**tooconfigure logon único do AD do Azure com o navegador de vendas LinkedIn, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **LinkedIn vendas navegador** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, na **modo** selecione **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. Em uma janela de navegador web diferente, o logon tooyour **LinkedIn vendas navegador** site como um administrador.

4. Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**. Além disso, selecione **vendas navegador** na lista suspensa hello.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. No portal do Azure, em **LinkedIn vendas navegador de domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    a. Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn 

    b. Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn

7. Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`

8. O **LinkedIn vendas navegador** aplicativo espera asserções SAML de saudação em um formato específico, o que exige que a configuração de atributos de token SAML do tooyour de mapeamentos de atributo personalizado tooadd. Olá captura de tela a seguir mostra um exemplo. Olá valor padrão de **identificador de usuário** é **User** mas LinkedIn vendas navegador espera toobe mapeada com o endereço de email do usuário hello. Você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização. 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação. usuário Olá precisa tooadd quatro declarações denominadas **email**, **departamento**, **firstname**, e **lastname** e valor de saudação é toobe mapeada com **user.mail**, **User. Department**, **user.givenname**, e **user.surname** respectivamente

    | Nome do atributo | Valor do atributo |
    | --- | --- |    
    | email| user.mail |
    | department| user.department |
    | nome| user.givenname |
    | sobrenome| user.surname |
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    a. Clique em **Adicionar atributo** caixa de diálogo do atributo tooopen hello.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**

10. Executar Olá seguindo as etapas na Olá **nome** atributo -

    a. Clique em saudação do hello atributo tooopen **Editar atributo** janela.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    b. Excluir o valor da URL de saudação da saudação **namespace**.
    
    c. Clique em **Okey** toosave configuração de saudação.

11. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. Vá muito**as configurações de administração do LinkedIn** seção. Clique em **arquivo carregar XML** Olá tooupload arquivo Metadata XML que você baixou do portal do Azure de saudação.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. Clique em **na** tooenable SSO. Status SSO é alterado de **não conectado** muito**conectado**

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a>Criar um usuário de teste do LinkedIn Sales Navigator

Aplicativo de navegador de vendas vinculado dá suporte apenas em Time (JIT) de provisionamento de usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello. Ativar **automaticamente atribuir licenças** tooassign um usuário de toohello de licença.
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLinkedIn navegador de vendas.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLinkedIn navegador de vendas, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **LinkedIn vendas navegador**.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco LinkedIn vendas navegador Olá Olá painel de acesso, você deve ser redirecionado tooOrganizational página onde você tem tooprovide os detalhes da conta pessoais LinkedIn. Ele vincula a sua conta pessoal à sua conta de negócios do LinkedIn. Para obter mais informações sobre Olá painel de acesso, consulte [Introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

