---
title: "Tutorial: integração do Azure Active Directory com o Jobscience | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Tutorial: Integração do Active Directory do Azure com o Jobscience

Neste tutorial, você aprenderá como toointegrate Jobscience com o Azure Active Directory (AD do Azure).

Integrando o Jobscience com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooJobscience
- Você pode habilitar seu usuários tooautomatically get conectado tooJobscience (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Jobscience, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Jobscience

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Jobscience da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-jobscience-from-hello-gallery"></a>Adicionando Jobscience da Galeria de saudação
integração de saudação tooconfigure do Jobscience no AD do Azure, você precisa tooadd Jobscience da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Jobscience da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Jobscience**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. No painel de resultados de saudação, selecione **Jobscience**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Jobscience, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Jobscience é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Jobscience precisa toobe estabelecida.

No Jobscience, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Jobscience, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Jobscience](#creating-a-jobscience-test-user)**  -toohave um equivalente do Britta Simon no Jobscience é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Jobscience.

**tooconfigure AD do Azure-logon único com o Jobscience, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Jobscience** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. Em Olá **Jobscience domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Obter esse valor [equipe de suporte do cliente Jobscience](https://www.jobscience.com/support) ou do perfil SSO Olá criará que é explicado posteriormente no tutorial de saudação. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. Em Olá **Jobscience configuração** seção, clique em **configurar Jobscience** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Faça logon em tooyour site da empresa Jobscience como um administrador.

8. Vá muito**instalação**.
   
   ![Configuração](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Configuração")

9. No painel de navegação à esquerda do hello, no hello **administrar** seção, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá  **Meu domínio** página. 
   
   ![Meu Domínio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Meu Domínio")

10. tooverify seu domínio foi configurado corretamente, certifique-se de que ela está em "**etapa 4 implantado tooUsers**" e examine seu "**minhas configurações de domínio**".

    ![Domínio implantado tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser domínio implantado")

11. No site da empresa Olá Jobscience, clique em **controles de segurança**e, em seguida, clique em **configurações de logon único**.
    
    ![Controles de Segurança](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Controles de Segurança")

12. Em Olá **configurações de logon único** , execute Olá etapas a seguir:
    
    ![Configurações de Logon Único](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Configurações de Logon Único")
    
    a. Selecione **SAML Habilitado**.

    b. Clique em **Novo**.

13. Em Olá **Single Sign-On Editar configuração de SAML** caixa de diálogo, executar Olá etapas a seguir:
    
    ![Configurações de Logon Único do SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Configurações de Logon Único do SAML")
    
    a. Em Olá **nome** caixa de texto, digite um nome para a sua configuração.

    b. Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.

    c. Em Olá **Id da entidade** caixa de texto, tipo`https://salesforce-jobscience.com`

    d. Clique em **procurar** tooupload seu certificado do AD do Azure.

    e. Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.

    f. Como **local da identidade do SAML**, selecione **identidade está no elemento Nameidentifier Olá Olá declaração assunto**.

    g. Em **URL de logon do provedor de identidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.

    h. Em **URL de Logout do provedor de identidade** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.

    i. Clique em **Salvar**.

14. No painel de navegação à esquerda do hello, no hello **administrar** seção, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá  **Meu domínio** página. 
    
    ![Meu Domínio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Meu Domínio")

15. Em Olá **meu domínio** página Olá **identidade visual da página de logon** seção, clique em **editar**.
    
    ![Identidade Visual da Página de Logon](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Identidade Visual da Página de Logon")

16. Em Olá **identidade visual da página de logon** página Olá **serviço de autenticação** seção, o nome de saudação do seu **configurações de SSO do SAML** é exibido. Selecione-o e, em seguida, clique em **Salvar**.
    
    ![Identidade Visual da Página de Logon](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Identidade Visual da Página de Logon")

17. Logon único iniciado pelo tooget Olá SP, clique em URL de logon em Olá **as configurações de logon único** em Olá **controles de segurança** seção do menu.

    ![Controles de Segurança](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Controles de Segurança")
    
    Clique em perfil Olá SSO que você criou na etapa de saudação acima. Esta página mostra Olá logon único na URL para a sua empresa (por exemplo, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-jobscience-test-user"></a>Criando um usuário de teste do Jobscience

Ordem tooenable AD do Azure usuários toolog em tooJobscience, eles devem ser provisionados no Jobscience. No caso de saudação do Jobscience, o provisionamento é uma tarefa manual.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Jobscience usuário conta ou APIs fornecidas pela Jobscience tooprovision Azure Active Directory as contas de usuário.
>  
        
**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Jobscience** site da empresa como administrador.

2. Vá tooSetup.
   
   ![Configuração](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Configuração")
3. Vá muito**gerenciar usuários \> usuários**.
   
   ![Usuários](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Usuários")
4. Clique em **Novo Usuário**.
   
   ![Todos os Usuários](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Todos os Usuários")
5. Em Olá **Editar usuário** caixa de diálogo, executar Olá etapas a seguir:
   
   ![Editar Usuário](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Editar Usuário")
   
   a. Em Olá **nome** caixa de texto, digite um nome de usuário, Olá como Britta.
   
   b. Em Olá **Sobrenome** caixa de texto, digite um sobrenome do usuário hello como Simon.
   
   c. Em Olá **Alias** caixa de texto, digite um nome de alias do usuário hello como brittas.

   d. Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.

   e. Em Olá **nome de usuário** caixa de texto, digite um nome de usuário do usuário, como Brittasimon@contoso.com.

   f. Em Olá **apelido** caixa de texto, digite um nome de usuário como Simon de nick.

   g. Clique em **Salvar**.

    
> [!NOTE]
> proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooJobscience.

![Atribuir usuário][200] 

**tooassign Britta Simon tooJobscience, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Jobscience**.

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Jobscience Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Jobscience aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

