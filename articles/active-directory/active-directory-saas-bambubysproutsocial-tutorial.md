---
title: "Tutorial: Integração do Azure Active Directory ao Bambu by Sprout Social | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bambu por Sprout sociais."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a>Tutorial: Integração do Azure Active Directory com Bambu by Sprout Social

Neste tutorial, você aprenderá como toointegrate Bambu por Sprout Social com o Azure Active Directory (AD do Azure).

Integrando Bambu por Sprout sociais do AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBambu por Sprout Social
- Você pode habilitar seu usuários tooautomatically get conectado tooBambu por Sprout Social (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Bambu por Sprout sociais, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada de logon único do Bambu by Sprout Social

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Bambu por Sprout Social da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a>Adicionando Bambu por Sprout Social da Galeria de saudação
integração de saudação tooconfigure de Bambu por Sprout Social no AD do Azure, você precisa tooadd Bambu por Sprout Social da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Bambu por Sprout Social da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do hello diálogo tooadd.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Bambu por Sprout Social**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. No painel de resultados de saudação, selecione **Bambu por Sprout Social**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Bambu by Sprout Social, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte de saudação em Bambu por Sprout Social é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Bambu por Sprout Social precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Bambu por Sprout sociais.

tooconfigure e teste de logon único do AD do Azure com Bambu por Sprout sociais, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um Bambu pelo usuário de teste Sprout Social](#creating-a-bambu-by-sprout-social-test-user)**  -toohave um equivalente do Britta Simon em Bambu por Sprout sociais que é a representação toohello vinculado do Azure AD de seus.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Bambu pelo aplicativo Sprout sociais.

**tooconfigure logon único do AD do Azure com Bambu por Sprout sociais, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Bambu por Sprout Social** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. Em Olá **Bambu Sprout domínio sociais e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure. 

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. Em Olá **Bambu pela configuração Social Sprout** seção, clique em **configurar Bambu por Sprout Social** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. tooconfigure logon único no **Bambu por Sprout Social** lado, você precisa toosend Olá baixado **Metadata XML** e **Single Sign-On URL do serviço SAML** muito[Bambu pelo suporte Sprout Social](mailto:support@getbambu.com). Eles serão configurados isso no hello toohave de ordem conexão SSO do SAML definido corretamente em ambos os lados.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar no hello **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **Britta Simon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a>Criando um usuário de teste Bambu by Sprout Social

Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooBambu seu acesso por Sprout sociais.

![Atribuir usuário][200] 

**tooassign Britta Simon tooBambu por Sprout sociais, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Bambu por Sprout Social**.

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá Bambu pelo bloco Sprout Social Olá painel de acesso, você deve obter automaticamente assinado em tooyour Bambu pelo aplicativo Sprout sociais. Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

