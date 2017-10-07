---
title: "Tutorial: Integração do Azure Active Directory com o Procore SSO | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Tutorial: integração do Azure Active Directory com o Procore SSO

Neste tutorial, você aprenderá como toointegrate Procore SSO com o Azure Active Directory (AD do Azure).

Integrando Procore SSO com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooProcore SSO
- Você pode habilitar seu usuários tooautomatically get conectado tooProcore SSO (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Procore SSO, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Procore SSO habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Procore SSO da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-procore-sso-from-hello-gallery"></a>Adicionando Procore SSO da Galeria de saudação
integração de saudação tooconfigure do SSO Procore no AD do Azure, você precisa tooadd Procore SSO na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Procore SSO da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **SSO Procore**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. No painel de resultados de saudação, selecione **SSO Procore**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Procore SSO, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO Procore é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em SSO Procore precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Procore SSO.

tooconfigure e teste de logon único do AD do Azure com Procore SSO, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de SSO Procore](#creating-a-procore-sso-test-user)**  -toohave um equivalente do Britta Simon no SSO Procore que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Procore SSO.

**tooconfigure AD do Azure-logon único com o SSO Procore, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **SSO Procore** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. Em Olá **Procore domínio de SSO e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. Em Olá **Procore configuração de SSO** seção, clique em **configurar SSO Procore** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure logon único no **Procore SSO** lado, o site de empresa procore tooyour logon como um administrador.

8. Lista de ferramentas Olá para baixo, clique em **Admin** tooopen página de configurações de SSO de saudação.

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Colar Olá valores nas caixas de saudação conforme descrito abaixo-

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. Em Olá **emissor URL de logon único** caixa, cole Olá ID da entidade SAML copiado da saudação portal do Azure.

    b. Em Olá **SAML destino URL de logon** caixa, cole Olá Single Sign-On URL do serviço SAML copiado da saudação portal do Azure.

    c. Agora, abra Olá **Metadata XML** baixado acima do hello portal do Azure e cópia Olá certificado na marca de saudação chamada **X509Certificate**. Olá colar copiado o valor para Olá **certificado de logon único x509** caixa.

10. Clique em **Salvar alterações**.

11. Depois que essas configurações, você precisa Olá toosend **nome de domínio** (por exemplo **contoso.com**) por meio do qual você está fazendo login toohello Procore [a equipe de suporte Procore](https://support.procore.com/) e elas serão Ative o SSO federado para esse domínio.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-procore-sso-test-user"></a>Criando um usuário de teste do Procore SSO

Siga Olá abaixo etapas toocreate um usuário de teste Procore em seu lado.

1. Site de empresa procore de tooyour de logon como administrador.  

2. Lista de ferramentas Olá para baixo, clique em **diretório** página de diretório tooopen Olá da empresa.

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Clique em **adicionar uma pessoa** opção formulário de saudação tooopen e digite executar as seguintes opções -

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. Em Olá **nome** caixa de texto, nome do usuário do tipo como **Britta**.

    b. Em Olá **Sobrenome** caixa de texto Sobrenome do usuário do tipo como **Simon**.

    c. Em Olá **endereço de Email** caixa de texto, como o endereço de email do usuário do tipo  **BrittaSimon@contoso.com** .

    d. Selecione **Modelo de permissão** como **Aplicar o modelo de permissão mais tarde**.

    e. Clique em **Criar**.

4. Verificar e atualizar detalhes Olá Olá recentemente adicionado entre em contato com.

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Clique em **salvar e enviar convite** (se um convite por email é necessário) ou **salvar** (Salvar diretamente) registro de usuário do toocomplete hello.
    
    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooProcore seu acesso SSO.

![Atribuir usuário][200] 

**tooassign Britta Simon tooProcore SSO, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SSO Procore**.

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Se você quiser testar suas configurações de logon único, abra o Painel de Acesso. Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586). Quando você clica em um bloco de SSO Procore Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado em aplicativos de SSO Procore.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

