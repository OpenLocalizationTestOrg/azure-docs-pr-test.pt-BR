---
title: "Tutorial: Integração do Azure Active Directory ao Evernote | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a>Tutorial: Integração do Azure Active Directory ao Evernote

Neste tutorial, você aprenderá como toointegrate Evernote com o Azure Active Directory (AD do Azure).

Integrando Evernote com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooEvernote.
- Você pode habilitar seu usuários tooautomatically get conectado tooEvernote (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Evernote, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Evernote habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Evernote da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-evernote-from-hello-gallery"></a>Adicionando Evernote da Galeria de saudação
integração de saudação tooconfigure de Evernote no AD do Azure, você precisa tooadd Evernote da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Evernote da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Evernote**, selecione **Evernote** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Evernote na lista de resultados de saudação](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Evernote, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Evernote é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Evernote precisa toobe estabelecida.

Evernote, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Evernote, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Evernote](#create-an-evernote-test-user)**  -toohave um equivalente do Britta Simon em Evernote é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Evernote.

**tooconfigure AD do Azure-logon único com Evernote, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Evernote** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. Em Olá **Evernote domínio e URLs** , execute Olá etapas a seguir se desejar que o modo de aplicativo de hello tooconfigure IDP iniciado:

    ![Informações de logon único de URLs e Domínio do Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://www.evernote.com/saml2`

4. Verificar **Mostrar configurações de URL avançadas** e executar Olá etapa a seguir se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Informações de logon único de URLs e Domínio do Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://www.evernote.com/Login.action`   

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. Em Olá **Evernote configuração** seção, clique em **configurar Evernote** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. Em outra janela do navegador da Web, faça logon em seu site de empresa do Evernote como administrador.

9. Vá muito**Console do administrador**

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. De saudação **'Admin Console'**, ir muito**'Security'** e selecione **' Single Sign-On'**

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. Configure Olá valores a seguir:

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    a.  **Habilitar SSO:** SSO é habilitado por padrão (clique **desabilitar Single Sign-on** requisito de SSO Olá tooremove)

    b. Colar **SAML logon único na URL do serviço** valor que você copiou de saudação portal do Azure em hello **URL de solicitação de HTTP de SAML** caixa de texto.

    c. Abra o certificado baixado de saudação do Azure AD em um bloco de notas e copie Olá de conteúdo incluindo "Iniciar certificado" e "END" e colá-la no hello **certificado x. 509** caixa de texto. 

    d.Clique em **Salvar Alterações**

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-an-evernote-test-user"></a>Criar um usuário de teste do Evernote

Em ordem tooenable AD do Azure usuários toolog em Evernote, eles devem ser provisionados no Evernote.  
No caso de saudação de Evernote, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon no tooyour Evernote site da empresa como um administrador.

2. Clique em Olá **Console do administrador**.

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. De saudação **'Admin Console'**, ir muito**'Adicionar usuários'**.

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. **Adicionar membros da equipe** em Olá **Email** caixa de texto, digite o endereço de email de saudação da conta de usuário e clique em **convidar.**

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. Depois que o convite é enviado, proprietário de conta do Active Directory do Azure Olá receberão um convite por email tooaccept hello.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEvernote.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooEvernote, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Evernote**.

    ![link de Evernote Olá na lista de aplicativos Olá](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Evernote Olá Olá painel de acesso, você deve obter conectado tooyour Evernote aplicativo. Você vai ser logon como uma conta de organização mas toolog necessidade com sua conta pessoal. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

