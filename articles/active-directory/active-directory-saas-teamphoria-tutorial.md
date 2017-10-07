---
title: "Tutorial: integração do Azure Active Directory com o Teamphoria | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Tutorial: integração do Azure Active Directory ao Teamphoria

Neste tutorial, você aprenderá como toointegrate Teamphoria com o Azure Active Directory (AD do Azure).

Integrando Teamphoria com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTeamphoria
- Você pode habilitar seu usuários tooautomatically get conectado tooTeamphoria (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Teamphoria, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Teamphoria

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Teamphoria da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-teamphoria-from-hello-gallery"></a>Adicionando Teamphoria da Galeria de saudação
integração de saudação tooconfigure de Teamphoria no AD do Azure, você precisa tooadd Teamphoria da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Teamphoria da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Teamphoria**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. No painel de resultados de saudação, selecione **Teamphoria**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Teamphoria, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Teamphoria é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Teamphoria precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Teamphoria.

tooconfigure e teste de logon único do AD do Azure com Teamphoria, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Teamphoria](#creating-a-teamphoria-test-user)**  -toohave um equivalente do Britta Simon em Teamphoria é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Teamphoria.

**tooconfigure AD do Azure-logon único com Teamphoria, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **Teamphoria** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. Em Olá **Teamphoria domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite a URL do hello usando saudação padrão a seguir:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com hello URL de logon real. Entre em contato com [equipe de suporte do cliente Teamphoria](https://www.teamphoria.com/) tooget Olá logon na URL. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. Em Olá **Teamphoria configuração** seção, clique em **configurar Teamphoria** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure logon único no **Teamphoria** lado, o aplicativo de Teamphoria tooyour logon como administrador.

8. Vá muito**as configurações de administração** opção em ferramentas de saudação à esquerda e sob Olá Olá guia Configurar clique em **logon único** tooopen janela de configuração de SSO de saudação.

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Clique em **adicionar novo provedor de identidade** opção no formulário de saudação de tooopen Olá canto superior direito para adicionar configurações de saudação do SSO.

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Insira detalhes de saudação nos campos Olá conforme descrito abaixo-

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **NOME de exibição** : digite o nome de exibição de saudação do hello plug-in na página de administração de saudação.

    b. **NOME do botão** : nome de saudação de guia de saudação que será exibido na página de logon Olá para registrar em log por meio do SSO.

    c. **CERTIFICADO** : Abra Olá certificado obtido anteriormente Olá portal do Azure no bloco de notas, copia o conteúdo de saudação do hello mesmo e cole-o aqui na caixa de hello.

    d. **PONTO de entrada** : Olá colar **Single Sign-On URL do serviço SAML** copiados Olá anterior de formulário portal do Azure.

    e. Alternar a opção de saudação muito**ON** e clique em **salvar**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-teamphoria-test-user"></a>Criar um usuário de teste do Teamphoria

Em ordem tooenable AD do Azure usuários toolog em Teamphoria, eles devem ser provisionados no Teamphoria. No caso de saudação de Teamphoria, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon no tooyour Teamphoria site da empresa como um administrador.

2. Clique em **ADMIN** configurações na barra de ferramentas à esquerda do hello e em Olá **gerenciar** guia clique **usuários** tooopen página de administrador Olá para usuários.

    ![Adicionar Funcionário](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Clique em Olá **MANUAL CONVIDAR** opção.

    ![Convidar Pessoas](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. Nessa página, realize a ação a seguir. 
    
    ![Convidar Pessoas](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. Em Olá **endereço de EMAIL** caixa de texto, Olá **endereço de email** de BrittaSimon.

    b. Em Olá **nome** caixa de texto, tipo **Britta**.

    c. Em Olá **Sobrenome** caixa de texto, tipo **Simon**.

    d. Clique em **CONVIDAR 1 USUÁRIO**. Os usuários precisam tooaccept Olá convite tooget criado no sistema de saudação.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooTeamphoria seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTeamphoria, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Teamphoria**.

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Se você quiser testar suas configurações de logon único, abra o Painel de Acesso. Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

