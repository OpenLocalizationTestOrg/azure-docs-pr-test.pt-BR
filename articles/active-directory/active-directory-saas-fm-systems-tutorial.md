---
title: "Tutorial: integração do Azure Active Directory com o FM:Systems | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FM: Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="c7ee5-103">Tutorial: Integração do Azure Active Directory com o FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7ee5-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="c7ee5-104">Neste tutorial, você aprenderá como toointegrate FM: Systems com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c7ee5-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7ee5-105">Integrando o FM: Systems com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7ee5-106">Você pode controlar no AD do Azure que tenha acesso tooFM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7ee5-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="c7ee5-107">Você pode habilitar seus usuários tooautomatically get conectado tooFM:Systems (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7ee5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7ee5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7ee5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7ee5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7ee5-110">Prerequisites</span></span>

<span data-ttu-id="c7ee5-111">tooconfigure integração do AD do Azure com o FM: Systems, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="c7ee5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7ee5-113">Uma assinatura habilitada para logon único do FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7ee5-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7ee5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7ee5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7ee5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7ee5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7ee5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7ee5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7ee5-118">Scenario description</span></span>
<span data-ttu-id="c7ee5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7ee5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7ee5-121">Adicionando FM: Systems da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c7ee5-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="c7ee5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="c7ee5-123">Adicionando FM: Systems da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c7ee5-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="c7ee5-124">integração de saudação tooconfigure do FM: Systems no AD do Azure, você precisa tooadd FM: Systems na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7ee5-125">**tooadd FM: Systems da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7ee5-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7ee5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7ee5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7ee5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7ee5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7ee5-133">Na caixa de pesquisa hello, digite **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-133">In hello search box, type **FM:Systems**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="c7ee5-135">No painel de resultados de saudação, selecione **FM: Systems**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7ee5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7ee5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o FM:Systems com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7ee5-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no FM: Systems é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="c7ee5-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no FM: Systems precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="c7ee5-141">No FM: Systems, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7ee5-142">tooconfigure e teste de logon único do AD do Azure com o FM: Systems, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7ee5-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7ee5-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7ee5-145">**[Criar um usuário de teste do FM: Systems](#creating-an-fmsystems-test-user)**  -toohave um equivalente de Britta Simon no FM: Systems que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7ee5-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7ee5-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7ee5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7ee5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7ee5-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo FM: Systems.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="c7ee5-150">**tooconfigure AD do Azure-logon único com o FM: Systems, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7ee5-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7ee5-151">Em Olá portal do Azure, Olá **FM: Systems** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7ee5-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="c7ee5-155">Em Olá **URLs e domínio do FM: Systems** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="c7ee5-157">Em Olá **URL de resposta** caixa de texto, digite o FM: Systems **URL de resposta**, digite a URL do hello usando saudação padrão a seguir:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="c7ee5-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7ee5-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-158">This value is not real.</span></span> <span data-ttu-id="c7ee5-159">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="c7ee5-160">Entre em contato com [equipe de suporte do FM: Systems](https://fmsystems.com/ask-us/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="c7ee5-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="c7ee5-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7ee5-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7ee5-165">tooconfigure logon único no **FM: Systems** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do FM: Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="c7ee5-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="c7ee5-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="c7ee5-167">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="c7ee5-168">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c7ee5-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7ee5-169">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7ee5-170">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7ee5-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7ee5-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7ee5-172">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7ee5-174">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7ee5-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7ee5-175">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7ee5-177">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7ee5-179">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7ee5-181">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7ee5-183">a.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-183">a.</span></span> <span data-ttu-id="c7ee5-184">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7ee5-185">b.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-185">b.</span></span> <span data-ttu-id="c7ee5-186">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7ee5-187">c.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-187">c.</span></span> <span data-ttu-id="c7ee5-188">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7ee5-189">d.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-189">d.</span></span> <span data-ttu-id="c7ee5-190">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="c7ee5-191">Criar um usuário de teste do FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7ee5-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="c7ee5-192">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do FM:Systems como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="c7ee5-193">Vá muito**administração do sistema \> gerenciar segurança \> usuários \> lista de usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="c7ee5-194">![Administração do Sistema](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Administração do Sistema")</span><span class="sxs-lookup"><span data-stu-id="c7ee5-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="c7ee5-195">Clique em **Criar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="c7ee5-196">![Criar Novo Usuário](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Criar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="c7ee5-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="c7ee5-197">Em Olá **Create User** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ee5-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c7ee5-198">![Criar usuário](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="c7ee5-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="c7ee5-199">a.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-199">a.</span></span> <span data-ttu-id="c7ee5-200">Saudação de tipo **UserName**, Olá **senha**, **Confirmar senha**, **email** e hello **ID de funcionário**de uma válida do Azure relacionadas à conta do Active Directory você deseja tooprovision em Olá caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="c7ee5-201">b.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-201">b.</span></span> <span data-ttu-id="c7ee5-202">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7ee5-203">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7ee5-204">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFM:Systems.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7ee5-206">**tooassign Britta Simon tooFM:Systems, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7ee5-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7ee5-207">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7ee5-209">Na lista de aplicativos hello, selecione **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="c7ee5-211">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7ee5-213">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-213">Click **Add** button.</span></span> <span data-ttu-id="c7ee5-214">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7ee5-216">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7ee5-217">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7ee5-218">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7ee5-219">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7ee5-219">Testing single sign-on</span></span>

<span data-ttu-id="c7ee5-220">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7ee5-221">Quando você clica em bloco FM: Systems Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour FM: Systems aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7ee5-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="c7ee5-222">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7ee5-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7ee5-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7ee5-223">Additional resources</span></span>

* [<span data-ttu-id="c7ee5-224">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ee5-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7ee5-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7ee5-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

