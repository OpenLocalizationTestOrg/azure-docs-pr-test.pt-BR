---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a área restrita do Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Tutorial: Integração do Active Directory do Azure com a Área Restrita Salesforce

Neste tutorial, você aprenderá como toointegrate área restrita do Salesforce com o Azure Active Directory (AD do Azure).

Integração de área restrita do Salesforce com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSalesforce área restrita
- Você pode habilitar seu usuários tooautomatically get conectado tooSalesforce seguro (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com área restrita do Salesforce, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Salesforce Sandbox

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando a área restrita do Salesforce da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Adicionando a área restrita do Salesforce da Galeria de saudação
integração de Olá tooconfigure da área restrita do Salesforce no AD do Azure, você precisa tooadd área restrita do Salesforce, na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd área restrita do Salesforce da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **área restrita do Salesforce**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. No painel de resultados de saudação, selecione **área restrita do Salesforce**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Salesforce Sandbox, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em área restrita do Salesforce é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em área restrita do Salesforce deve toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em área restrita do Salesforce.

tooconfigure e teste de logon único do AD do Azure com área restrita do Salesforce, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de área restrita do Salesforce](#creating-a-salesforce-sandbox-test-user)**  -toohave um equivalente do Britta Simon em área restrita do Salesforce que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de área restrita do Salesforce.

**tooconfigure AD do Azure-logon único com área restrita do Salesforce, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **área restrita do Salesforce** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. Em Olá **URLs e domínio de área restrita do Salesforce** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Esse valor não é hello real. Atualize esse valor com a URL de logon real hello. Entre em contato com [equipe de suporte do cliente de área restrita do Salesforce](https://help.salesforce.com/support) tooget esse valor.


4. Se você já tiver configurado logon único para outra instância de área restrita do Salesforce em seu diretório, você também deve configurar Olá **identificador** toohave Olá mesmo valor Olá **URL de entrada**. 
    
    >[!Note]
    >Olá **identificador** campo pode ser encontrado verificando Olá **Mostrar configurações avançadas** caixa de seleção na Olá **configurar URL do aplicativo** página da caixa de diálogo Olá 


5. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. Em Olá **configuração da área restrita Salesforce** seção, clique em **configurar área restrita do Salesforce** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Abra uma nova guia no seu navegador e faça logon tooyour conta de administrador da área restrita do Salesforce.

9. No menu de saudação na parte superior de saudação, clique em **instalação**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. No painel de navegação Olá Olá esquerda, clique em **controles de segurança**e, em seguida, clique em **configurações de logon único**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Na seção configurações de logon único do hello, executar Olá etapas a seguir: ![configurar logon único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Selecione **SAML Habilitado**. 

     b.  Clique em **Novo**.

12. Na seção configurações de logon único SAML do hello, execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    a.In Olá de texto Nome, digite o nome de saudação da configuração de saudação (por exemplo: *SPSSOWAAD\_teste*). 

    b. Colar **ID da entidade Small** valor em Olá **emissor** caixa de texto.

    c. Em Olá **Id da entidade** caixa de texto, tipo **https://test.salesforce.com** se for Olá a primeira instância de área restrita do Salesforce que você está adicionando tooyour directory. Se você já tiver adicionado uma instância de área restrita do Salesforce, em seguida, para Olá **ID da entidade** tipo no hello **URL de logon**, que deveriam estar neste formato:`http://company.my.salesforce.com`  
 
    d. Clique em **procurar** Olá tooupload baixado o certificado.  

    e. Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.
 
    f. Como **local da identidade do SAML**, selecione **identidade está no elemento NameIdentifier Olá Olá declaração assunto**.

    g. Colar **o URL de serviço de logon único** em Olá **URL de logon do provedor de identidade** caixa de texto. 

    h. O SFDC não dá suporte a logout SAML.  Como alternativa, cole 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'-o na Olá **URL de Logout do provedor de identidade** caixa de texto.

    i. Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**. 

    j. Clique em **Salvar**.

### <a name="enable-your-domain"></a>Habilitar seu domínio
Esta seção pressupõe que você já tenha criado um domínio.  Para obter mais informações, consulte [Definindo o nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable seu domínio, executar Olá etapas a seguir:**

1. No painel de navegação esquerdo hello, clique em **gerenciamento de domínio**e, em seguida, clique em **meu domínio.**
   
     ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Verifique se o domínio foi configurado corretamente. 

2. Em Olá **configurações de página de logon** seção, clique em **editar**, em seguida, como **serviço de autenticação**, selecione nome de saudação do hello configuração de logon único SAML de saudação anterior seção e, finalmente, clique em **salvar**.
   
   ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Assim que você tiver um domínio configurado, seus usuários devem usar a área restrita do Salesforce Olá domínio URL toologin toohello.  

valor tooget Olá Olá URL, clique em perfil Olá SSO que você criou na seção anterior hello.    

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários ir muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Criando um usuário de teste do Salesforce Sandbox

Nesta seção, um usuário chamado Brenda Fernandes é criado no Salesforce Sandbox. O Salesforce Sandbox dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.
Não há itens de ação para você nesta seção. Se um usuário ainda não existir na área restrita do Salesforce, um novo será criado quando você tenta tooaccess área restrita do Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSalesforce área restrita.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSalesforce área restrita, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **área restrita do Salesforce**.

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

