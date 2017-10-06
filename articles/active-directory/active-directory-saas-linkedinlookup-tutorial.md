---
title: "Tutorial: Integração do Azure Active Directory ao LinkedIn Lookup | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e pesquisa LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Tutorial: Integração do Azure Active Directory ao LinkedIn Lookup

Neste tutorial, você aprenderá como toointegrate pesquisa LinkedIn com o Azure Active Directory (AD do Azure).

Integração de pesquisa do LinkedIn com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLinkedIn pesquisa
- Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn pesquisa (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com pesquisa LinkedIn, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do LinkedIn Lookup

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando LinkedIn pesquisa da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>Adicionando LinkedIn pesquisa da Galeria de saudação
integração de saudação tooconfigure da pesquisa do LinkedIn no AD do Azure, você precisa tooadd LinkedIn pesquisa na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd LinkedIn pesquisa da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do hello diálogo tooadd.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **LinkedIn pesquisa**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. No painel de resultados de saudação, selecione **LinkedIn pesquisa**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você vai configurar e testar o logon único do Azure AD com o LinkedIn Lookup, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na pesquisa do LinkedIn é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na pesquisa do LinkedIn precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na pesquisa do LinkedIn.

tooconfigure e teste de logon único do AD do Azure com pesquisa LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de pesquisa LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave um equivalente do Britta Simon na pesquisa LinkedIn que é a representação toohello vinculado do Azure AD.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de pesquisa do LinkedIn.

**tooconfigure AD do Azure-logon único com pesquisa LinkedIn, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **LinkedIn pesquisa** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, na **modo** selecione **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. Em uma janela de navegador web diferente, o logon tooyour **LinkedIn pesquisa** site como um administrador.

4. Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**. Além disso, selecione **pesquisa** na lista suspensa hello.

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. No portal do Azure, em **LinkedIn pesquisa domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn 

    b. Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn

7. Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > Isso não é um valor real. usuário Olá tem tooupdate esses valores com hello URL de logon real. Entre em contato com [equipe de suporte do cliente do LinkedIn pesquisa](https://business.LinkedIn.com/lookup) tooget esse valor.

8. O **LinkedIn pesquisa** aplicativo espera as asserções SAML de saudação em um formato específico. usuário Olá tem uma configuração de atributos de token SAML do toohello de mapeamentos de atributo personalizado tooadd. Olá captura de tela a seguir mostra um exemplo. Olá valor padrão de **identificador de usuário** é **User** mas pesquisa LinkedIn espera este toobe mapeada com o endereço de email do usuário hello. Você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização. 

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação. usuário Olá precisa tooadd quatro declarações denominadas **email**, **departamento**, **firstname**, e **lastname** e valor de saudação é toobe mapeada com **user.mail**, **User. Department**, **user.givenname**, e **user.surname** respectivamente

    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | nome| user.givenname |
    | sobrenome| user.surname |

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**

10. Executar Olá seguindo as etapas na Olá **nome** atributo -

    a. Clique em saudação do hello atributo tooopen **Editar atributo** janela.

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Excluir o valor da URL de saudação da saudação **namespace**.
    
    c. Clique em **Okey** toosave configuração de saudação.

10. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Vá muito**as configurações de administração do LinkedIn** seção. Carregue o arquivo de XML de saudação baixado do hello portal do Azure clicando Olá **arquivo carregar XML** opção.

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Clique em **na** tooenable SSO. Status SSO é alterado de **não conectado** muito**conectado**

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **Britta Simon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Criação de um usuário de teste do LinkedIn Lookup

Aplicativo de pesquisa vinculado oferece suporte a apenas em Time (JIT) de provisionamento de usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello. Ativar **automaticamente atribuir licenças** tooassign um usuário de toohello de licença.
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLinkedIn pesquisa.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLinkedIn pesquisa, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **LinkedIn pesquisa**.

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá LinkedIn pesquisa bloco no painel de acesso de saudação, você deve ser redirecionado tooOrganizational página onde você tem tooprovide os detalhes da conta pessoais LinkedIn. Ele vincula a sua conta pessoal à sua conta de negócios do LinkedIn. 

Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

