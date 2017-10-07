---
title: "Tutorial: Integração do Azure Active Directory ao Autotask Workplace | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Autotask no local de trabalho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a>Tutorial: Integração do Azure Active Directory ao Autotask Workplace

Neste tutorial, você aprenderá como toointegrate Autotask no local de trabalho com o Azure Active Directory (AD do Azure).

Integrando Autotask no local de trabalho com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAutotask no local de trabalho
- Você pode habilitar seu usuários tooautomatically get conectado tooAutotask no local de trabalho (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Autotask no local de trabalho, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Autotask Workplace
- Você deve ser um administrador ou superadministrador no local de trabalho.
- Você deve ter uma conta de administrador no hello AD do Azure.
- usuários de saudação que utilizam este recurso devem ter contas no local de trabalho e hello AD do Azure e seus endereços de email para ambos devem corresponder.

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Autotask no local de trabalho na Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-autotask-workplace-from-hello-gallery"></a>Adicionando Autotask no local de trabalho na Galeria de saudação
integração de saudação tooconfigure do local de trabalho Autotask no AD do Azure, você precisa tooadd Autotask no local de trabalho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Autotask no local de trabalho na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Autotask no local de trabalho**, selecione **Autotask trabalho** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Lista de resultados de local de trabalho Autotask em Olá](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Autotask Workplace, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na área de trabalho Autotask é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho Autotask precisa toobe estabelecida.

Na área de trabalho Autotask, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Autotask de espaço de trabalho, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do local de trabalho Autotask](#create-an-autotask-workplace-test-user)**  -toohave um equivalente do Britta Simon na área de trabalho Autotask que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de área de trabalho Autotask.

**tooconfigure AD do Azure-logon único com o local de trabalho Autotask execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Autotask trabalho** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. Se desejar que o aplicativo hello tooconfigure **IDP** iniciada modo, executar Olá seguindo as etapas na Olá **URLs e domínio do local de trabalho Autotask** seção:

    ![Informações de logon único de Domínio e URLs do Autotask Workplace para IdP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`

4. Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado, verifique **Mostrar configurações de URL avançadas** e executar Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Autotask Workplace para SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awp.autotask.net/loginsso`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Entre em contato com [equipe de suporte do cliente de área de trabalho Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget esses valores. 

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. Em uma janela de navegador web diferente, o logon tooWorkplace Online usando Olá credenciais de administrador.

    >[!Note]
    >Ao configurar Olá IdP, um subdomínio precisará toobe especificado. subdomínio de correta de saudação do tooconfirm, logon tooWorkplace on-line. Depois de conectado, manter Observação toohello subdomínio Olá URL.
    >subdomínio Olá faz parte de saudação entre hello "https://" e ".awp.autotask.net/" e deve ser EUA, UE, autoridade de certificação ou Austrália.

8. Vá muito**configuração** > **Single Sign-On** e executar Olá etapas a seguir:

    ![Configuração de Logon Único do Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    a. Selecione Olá **arquivo de metadados XML** opção e, em seguida, carregar Olá **Metadata XML** baixado do portal do Azure.

    b. Clique em **Habilitar SSO**.
    
    ![Configuração de aprovação de Logon Único do Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    c. Selecione Olá **confirmar essas informações estão corretas e eu confio neste IdP** caixa de seleção.

    d. Clique em **Aprovar**.
     
>[!Note]
>Se você precisar de assistência com a configuração Autotask no local de trabalho, consulte [essa página](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistência com sua conta da empresa.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.

### <a name="create-an-autotask-workplace-test-user"></a>Criar um usuário de teste do Autotask Workplace

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Autotask. Trabalhe com [a equipe de suporte local de trabalho Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd usuários Olá Olá plataforma Autotask no local de trabalho.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAutotask no local de trabalho.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooAutotask no local de trabalho, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Autotask trabalho**.

    ![Olá link Autotask no local de trabalho na lista de aplicativos Olá](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá Autotask no local de trabalho lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de área de trabalho Autotask.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

