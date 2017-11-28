---
title: "Tutorial: Integração do Azure Active Directory ao Tango Analytics | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e análise de Tango."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 2076397e746235692f07241650d5556afb3c3d28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="bd308-103">Tutorial: Integração do Azure Active Directory ao Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="bd308-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="bd308-104">Neste tutorial, você aprenderá como toointegrate Tango análise com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="bd308-104">In this tutorial, you learn how toointegrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd308-105">Integrando Tango análise AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd308-105">Integrating Tango Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd308-106">Você pode controlar no AD do Azure que tenha acesso tooTango análise</span><span class="sxs-lookup"><span data-stu-id="bd308-106">You can control in Azure AD who has access tooTango Analytics</span></span>
- <span data-ttu-id="bd308-107">Você pode habilitar seu usuários tooautomatically get conectado tooTango Analytics (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-107">You can enable your users tooautomatically get signed-on tooTango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd308-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd308-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd308-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd308-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bd308-110">Prerequisites</span></span>

<span data-ttu-id="bd308-111">tooconfigure integração do AD do Azure com a análise de Tango, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd308-111">tooconfigure Azure AD integration with Tango Analytics, you need hello following items:</span></span>

- <span data-ttu-id="bd308-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd308-113">Uma assinatura habilitada para logon único do Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="bd308-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd308-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bd308-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd308-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bd308-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd308-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bd308-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd308-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd308-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd308-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bd308-118">Scenario description</span></span>
<span data-ttu-id="bd308-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bd308-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd308-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="bd308-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd308-121">Adicionando Tango análise da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bd308-121">Adding Tango Analytics from hello gallery</span></span>
2. <span data-ttu-id="bd308-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-hello-gallery"></a><span data-ttu-id="bd308-123">Adicionando Tango análise da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bd308-123">Adding Tango Analytics from hello gallery</span></span>
<span data-ttu-id="bd308-124">integração de Olá tooconfigure de análise de Tango no AD do Azure, você precisa tooadd Tango análise da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bd308-124">tooconfigure hello integration of Tango Analytics into Azure AD, you need tooadd Tango Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd308-125">**tooadd Tango análise da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd308-125">**tooadd Tango Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd308-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bd308-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd308-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bd308-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd308-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bd308-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="bd308-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd308-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="bd308-133">Na caixa de pesquisa hello, digite **Tango análise**.</span><span class="sxs-lookup"><span data-stu-id="bd308-133">In hello search box, type **Tango Analytics**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="bd308-135">No painel de resultados de saudação, selecione **Tango análise**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bd308-135">In hello results panel, select **Tango Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd308-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd308-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tango Analytics, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bd308-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd308-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na análise do Tango é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd308-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tango Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="bd308-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na análise do Tango precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bd308-140">In other words, a link relationship between an Azure AD user and hello related user in Tango Analytics needs toobe established.</span></span>

<span data-ttu-id="bd308-141">Na análise do Tango, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd308-141">In Tango Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd308-142">tooconfigure e teste de logon único do AD do Azure com a análise de Tango, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd308-142">tooconfigure and test Azure AD single sign-on with Tango Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd308-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bd308-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd308-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd308-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd308-145">**[Criar um usuário de teste de análise de Tango](#creating-a-tango-analytics-test-user)**  -toohave um equivalente do Britta Simon na análise do Tango que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="bd308-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - toohave a counterpart of Britta Simon in Tango Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd308-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="bd308-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd308-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="bd308-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd308-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd308-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd308-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de análise de Tango.</span><span class="sxs-lookup"><span data-stu-id="bd308-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="bd308-150">**tooconfigure AD do Azure-logon único com análises de Tango, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd308-150">**tooconfigure Azure AD single sign-on with Tango Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd308-151">Em Olá portal do Azure, Olá **Tango análise** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="bd308-151">In hello Azure portal, on hello **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="bd308-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="bd308-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="bd308-155">Em Olá **Tango análise de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd308-155">On hello **Tango Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="bd308-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd308-157">a.</span></span> <span data-ttu-id="bd308-158">Em Olá **identificador** caixa de texto, o valor do tipo hello`TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="bd308-158">In hello **Identifier** textbox, type hello value `TACORE_SSO`</span></span>

    <span data-ttu-id="bd308-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd308-159">b.</span></span> <span data-ttu-id="bd308-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="bd308-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd308-161">Olá valor de URL de resposta não é real.</span><span class="sxs-lookup"><span data-stu-id="bd308-161">hello Reply URL value is not real.</span></span> <span data-ttu-id="bd308-162">Atualize esse com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="bd308-162">Update this with hello actual Reply URL.</span></span> <span data-ttu-id="bd308-163">Entre em contato com [equipe de suporte de análise de Tango](mailto:support@tangoanalytics.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="bd308-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) tooget this value.</span></span>

4. <span data-ttu-id="bd308-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bd308-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="bd308-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bd308-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd308-168">tooconfigure logon único no **Tango análise** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte de análise de Tango](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="bd308-168">tooconfigure single sign-on on **Tango Analytics** side, you need toosend hello downloaded **Metadata XML** too[Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="bd308-169">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="bd308-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bd308-170">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="bd308-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd308-171">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="bd308-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd308-172">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd308-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd308-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd308-174">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd308-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="bd308-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd308-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd308-177">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bd308-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd308-179">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bd308-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd308-181">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd308-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd308-183">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd308-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd308-185">a.</span><span class="sxs-lookup"><span data-stu-id="bd308-185">a.</span></span> <span data-ttu-id="bd308-186">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd308-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd308-187">b.</span><span class="sxs-lookup"><span data-stu-id="bd308-187">b.</span></span> <span data-ttu-id="bd308-188">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd308-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd308-189">c.</span><span class="sxs-lookup"><span data-stu-id="bd308-189">c.</span></span> <span data-ttu-id="bd308-190">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="bd308-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd308-191">d.</span><span class="sxs-lookup"><span data-stu-id="bd308-191">d.</span></span> <span data-ttu-id="bd308-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bd308-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="bd308-193">Criação um usuário de teste do Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="bd308-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="bd308-194">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="bd308-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="bd308-195">Trabalhar com [equipe de suporte de análise de Tango](mailto:support@tangoanalytics.com) para adicionar usuários de saudação na plataforma de análise de Tango hello.</span><span class="sxs-lookup"><span data-stu-id="bd308-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add hello users in hello Tango Analytics platform.</span></span> <span data-ttu-id="bd308-196">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="bd308-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd308-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd308-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTango análise.</span><span class="sxs-lookup"><span data-stu-id="bd308-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTango Analytics.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="bd308-200">**tooassign Britta Simon tooTango Analytics, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd308-200">**tooassign Britta Simon tooTango Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd308-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bd308-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bd308-203">Na lista de aplicativos hello, selecione **Tango análise**.</span><span class="sxs-lookup"><span data-stu-id="bd308-203">In hello applications list, select **Tango Analytics**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="bd308-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bd308-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="bd308-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bd308-207">Click **Add** button.</span></span> <span data-ttu-id="bd308-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd308-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="bd308-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd308-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd308-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd308-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd308-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd308-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd308-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="bd308-213">Testing single sign-on</span></span>

<span data-ttu-id="bd308-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd308-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd308-215">Quando você clica em Olá Tango análise lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de análise de Tango.</span><span class="sxs-lookup"><span data-stu-id="bd308-215">When you click hello Tango Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Tango Analytics application.</span></span>
<span data-ttu-id="bd308-216">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bd308-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd308-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bd308-217">Additional resources</span></span>

* [<span data-ttu-id="bd308-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bd308-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd308-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd308-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png

