---
title: "Tutorial: Integração do Azure Active Directory com o Oneteam | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 7964aaaf9b9570d460f28d86de34b5e87693ba93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="bfcde-103">Tutorial: integração do Azure Active Directory com o Oneteam</span><span class="sxs-lookup"><span data-stu-id="bfcde-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="bfcde-104">Neste tutorial, você aprenderá como toointegrate Oneteam com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="bfcde-104">In this tutorial, you learn how toointegrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfcde-105">Integrando Oneteam com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfcde-105">Integrating Oneteam with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bfcde-106">Você pode controlar no AD do Azure que tenha acesso tooOneteam</span><span class="sxs-lookup"><span data-stu-id="bfcde-106">You can control in Azure AD who has access tooOneteam</span></span>
- <span data-ttu-id="bfcde-107">Você pode habilitar seu usuários tooautomatically get conectado tooOneteam (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-107">You can enable your users tooautomatically get signed-on tooOneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfcde-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bfcde-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfcde-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfcde-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bfcde-110">Prerequisites</span></span>

<span data-ttu-id="bfcde-111">tooconfigure integração do AD do Azure com Oneteam, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfcde-111">tooconfigure Azure AD integration with Oneteam, you need hello following items:</span></span>

- <span data-ttu-id="bfcde-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfcde-113">Uma assinatura habilitada para logon único do Oneteam</span><span class="sxs-lookup"><span data-stu-id="bfcde-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfcde-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bfcde-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfcde-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bfcde-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfcde-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bfcde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfcde-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfcde-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfcde-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bfcde-118">Scenario description</span></span>
<span data-ttu-id="bfcde-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bfcde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfcde-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="bfcde-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfcde-121">Adicionando Oneteam da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bfcde-121">Adding Oneteam from hello gallery</span></span>
2. <span data-ttu-id="bfcde-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-hello-gallery"></a><span data-ttu-id="bfcde-123">Adicionando Oneteam da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bfcde-123">Adding Oneteam from hello gallery</span></span>
<span data-ttu-id="bfcde-124">integração de saudação tooconfigure de Oneteam no AD do Azure, você precisa tooadd Oneteam da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bfcde-124">tooconfigure hello integration of Oneteam into Azure AD, you need tooadd Oneteam from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bfcde-125">**tooadd Oneteam da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bfcde-125">**tooadd Oneteam from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfcde-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bfcde-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfcde-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bfcde-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="bfcde-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bfcde-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="bfcde-133">Na caixa de pesquisa hello, digite **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-133">In hello search box, type **Oneteam**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="bfcde-135">No painel de resultados de saudação, selecione **Oneteam**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bfcde-135">In hello results panel, select **Oneteam**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfcde-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfcde-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Oneteam, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bfcde-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bfcde-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Oneteam é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcde-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Oneteam is tooa user in Azure AD.</span></span> <span data-ttu-id="bfcde-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Oneteam precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bfcde-140">In other words, a link relationship between an Azure AD user and hello related user in Oneteam needs toobe established.</span></span>

<span data-ttu-id="bfcde-141">Oneteam, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfcde-141">In Oneteam, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bfcde-142">tooconfigure e teste de logon único do AD do Azure com Oneteam, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfcde-142">tooconfigure and test Azure AD single sign-on with Oneteam, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bfcde-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bfcde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bfcde-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfcde-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfcde-145">**[Criar um usuário de teste Oneteam](#creating-a-oneteam-test-user)**  -toohave um equivalente do Britta Simon em Oneteam é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="bfcde-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - toohave a counterpart of Britta Simon in Oneteam that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfcde-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="bfcde-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfcde-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="bfcde-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfcde-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfcde-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfcde-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Oneteam.</span><span class="sxs-lookup"><span data-stu-id="bfcde-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="bfcde-150">**tooconfigure AD do Azure-logon único com Oneteam, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bfcde-150">**tooconfigure Azure AD single sign-on with Oneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfcde-151">Em Olá portal do Azure, Olá **Oneteam** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-151">In hello Azure portal, on hello **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="bfcde-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="bfcde-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="bfcde-155">Em Olá **Oneteam domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="bfcde-155">On hello **Oneteam Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="bfcde-157">a.</span><span class="sxs-lookup"><span data-stu-id="bfcde-157">a.</span></span> <span data-ttu-id="bfcde-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="bfcde-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="bfcde-159">b.</span><span class="sxs-lookup"><span data-stu-id="bfcde-159">b.</span></span> <span data-ttu-id="bfcde-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="bfcde-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="bfcde-161">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="bfcde-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="bfcde-163">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="bfcde-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bfcde-164">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="bfcde-164">These values are not real.</span></span> <span data-ttu-id="bfcde-165">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="bfcde-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bfcde-166">Entre em contato com [equipe de suporte do cliente Oneteam](https://support.one-team.com/hc/requests/new) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="bfcde-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) tooget these values.</span></span> 



5. <span data-ttu-id="bfcde-167">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bfcde-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="bfcde-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bfcde-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bfcde-171">tooget SSO configurado para o seu aplicativo, você pode gerar o tíquete de suporte de saudação com [a equipe de suporte Oneteam](https://support.one-team.com/hc/requests/new) e fornecê-los Olá baixado **metadados**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-171">tooget SSO configured for your application, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them hello downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="bfcde-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="bfcde-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bfcde-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="bfcde-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bfcde-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfcde-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfcde-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfcde-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcde-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="bfcde-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bfcde-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfcde-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bfcde-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfcde-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfcde-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfcde-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfcde-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfcde-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfcde-187">a.</span><span class="sxs-lookup"><span data-stu-id="bfcde-187">a.</span></span> <span data-ttu-id="bfcde-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfcde-189">b.</span><span class="sxs-lookup"><span data-stu-id="bfcde-189">b.</span></span> <span data-ttu-id="bfcde-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bfcde-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfcde-191">c.</span><span class="sxs-lookup"><span data-stu-id="bfcde-191">c.</span></span> <span data-ttu-id="bfcde-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bfcde-193">d.</span><span class="sxs-lookup"><span data-stu-id="bfcde-193">d.</span></span> <span data-ttu-id="bfcde-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="bfcde-195">Criação de um usuário de teste do Oneteam</span><span class="sxs-lookup"><span data-stu-id="bfcde-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="bfcde-196">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Oneteam.</span><span class="sxs-lookup"><span data-stu-id="bfcde-196">hello objective of this section is toocreate a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="bfcde-197">O Oneteam dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="bfcde-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bfcde-198">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="bfcde-198">There is no action item for you in this section.</span></span> <span data-ttu-id="bfcde-199">Será criado um novo usuário durante uma tentativa tooaccess Oneteam, se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="bfcde-199">A new user will be created during an attempt tooaccess Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="bfcde-200">Se você precisar toocreate um usuário manualmente, você pode gerar o tíquete de suporte de saudação com [a equipe de suporte Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="bfcde-200">If you need toocreate an user manually, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bfcde-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bfcde-202">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOneteam.</span><span class="sxs-lookup"><span data-stu-id="bfcde-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOneteam.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="bfcde-204">**tooassign Britta Simon tooOneteam, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bfcde-204">**tooassign Britta Simon tooOneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfcde-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bfcde-207">Na lista de aplicativos hello, selecione **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-207">In hello applications list, select **Oneteam**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="bfcde-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="bfcde-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bfcde-211">Click **Add** button.</span></span> <span data-ttu-id="bfcde-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bfcde-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="bfcde-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfcde-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bfcde-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bfcde-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfcde-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bfcde-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfcde-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="bfcde-217">Testing single sign-on</span></span>

<span data-ttu-id="bfcde-218">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfcde-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bfcde-219">Quando você clica em bloco Oneteam Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Oneteam aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bfcde-219">When you click hello Oneteam tile in hello Access Panel, you should get automatically signed-on tooyour Oneteam application.</span></span>
<span data-ttu-id="bfcde-220">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bfcde-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bfcde-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bfcde-221">Additional resources</span></span>

* [<span data-ttu-id="bfcde-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bfcde-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfcde-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfcde-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

