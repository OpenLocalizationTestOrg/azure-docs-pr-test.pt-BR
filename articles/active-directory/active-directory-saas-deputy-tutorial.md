---
title: "Tutorial: integração do Azure Active Directory ao Deputy | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e representante."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a>Tutorial: integração do Azure Active Directory ao Deputy

Neste tutorial, você aprenderá como toointegrate representante com o Azure Active Directory (AD do Azure).

Integrando o representante com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooDeputy
- Você pode habilitar seu usuários tooautomatically get conectado tooDeputy (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o representante, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Deputy habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar representante da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-deputy-from-hello-gallery"></a>Adicionar representante da Galeria de saudação
integração de saudação tooconfigure do representante no AD do Azure, você precisa tooadd representante na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd representante da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **representante**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. No painel de resultados de saudação, selecione **representante**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Deputy com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no representante é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no representante precisa toobe estabelecida.

Substituto, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o representante, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de representante](#creating-a-deputy-test-user)**  -toohave um equivalente do Britta Simon no representante que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de representante.

**tooconfigure AD do Azure-logon único com substituto, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **representante** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. Em Olá **domínio representante e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. Marque **Mostrar configurações de URL avançadas**. Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<your-subdomain>.<region>.deputy.com`
    
    >[!NOTE]
    > O sufixo de região do Deputy é opcional ou ele deve usar uma destas opções: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Entre em contato com [equipe de suporte de representante](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget esses valores. 

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. Em Olá **representante configuração** seção, clique em **representante configurar** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. Navegue toohello URL a seguir:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config). Vá muito**as configurações de segurança** e clique em **editar**.
   
    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. Na página **Configurações de Segurança** , execute etapas abaixo.

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    a. Habilite o **Logon Social**.
   
    b. Abra seu certificado codificado na Base64 que baixou do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado OpenSSL** caixa de texto.
   
    c. Na caixa de texto de URL SSO SAML Olá, digite`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`
    
    d. Na caixa de texto de URL SSO SAML Olá, substitua `<your subdomain>` com seu subdomínio.
   
    e. Na caixa de texto de URL SSO SAML Olá, substitua `<saml sso url>` com hello **Single Sign-On URL do serviço SAML** você copiou da saudação portal do Azure.
   
    f. Clique em **Salvar Configurações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-deputy-test-user"></a>Criando um usuário de teste do Deputy

tooenable AD do Azure usuários toolog em tooDeputy, eles devem ser provisionados no representante. No caso do Deputy, o provisionamento é uma tarefa manual.

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de usuário, execute Olá etapas a seguir:
1. Faça logon no site da empresa tooyour representante como um administrador.

2. No painel de navegação superior hello, clique em **pessoas**.
   
   ![Pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Pessoas")

3. Clique em Olá **adicionar pessoas** botão e clique em **adicionar uma única pessoa**.
   
   ![Adicionar Pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Adicionar Pessoas")

4. Execute Olá etapas a seguir e clique em **salvar e convidar**.
   
   ![Novo Usuário](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Novo Usuário")

   a. Em Olá **nome** caixa de texto Nome do tipo de usuário hello como **BrittaSimon**.
   
   b. Em Olá **Email** caixa de texto, endereço de email de saudação do tipo de uma conta do AD do Azure você deseja tooprovision.
   
   c. Em Olá **trabalhar em** caixa de texto Nome do tipo hello comercial.
   
   d. Clique no botão **Salvar e Convidar**.

5. proprietário de conta do AAD Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa. Você pode usar qualquer ferramenta de criação outros representante usuário conta ou APIs fornecidas pelo representante tooprovision AAD contas de usuário.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDeputy.

![Atribuir usuário][200] 

**tooassign Britta Simon tooDeputy, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **representante**.

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em Olá representante bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de representante.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

