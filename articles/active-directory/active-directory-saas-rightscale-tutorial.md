---
title: "Tutorial: Integração do Azure Active Directory ao Rightscale | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="22bf0-103">Tutorial: Integração do Azure Active Directory ao Rightscale</span><span class="sxs-lookup"><span data-stu-id="22bf0-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="22bf0-104">Neste tutorial, você aprenderá como toointegrate Rightscale com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="22bf0-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22bf0-105">Integrando Rightscale com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="22bf0-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="22bf0-106">Você pode controlar no AD do Azure que tenha acesso tooRightscale</span><span class="sxs-lookup"><span data-stu-id="22bf0-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="22bf0-107">Você pode habilitar seu usuários tooautomatically get conectado tooRightscale (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22bf0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="22bf0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22bf0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22bf0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="22bf0-110">Prerequisites</span></span>

<span data-ttu-id="22bf0-111">tooconfigure integração do AD do Azure com Rightscale, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="22bf0-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="22bf0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22bf0-113">Uma assinatura habilitada para logon único do Rightscale</span><span class="sxs-lookup"><span data-stu-id="22bf0-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22bf0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="22bf0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22bf0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="22bf0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22bf0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="22bf0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22bf0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22bf0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22bf0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="22bf0-118">Scenario description</span></span>
<span data-ttu-id="22bf0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="22bf0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22bf0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="22bf0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22bf0-121">Adicionando Rightscale da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="22bf0-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="22bf0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="22bf0-123">Adicionando Rightscale da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="22bf0-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="22bf0-124">integração de saudação tooconfigure de Rightscale no AD do Azure, você precisa tooadd Rightscale da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="22bf0-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="22bf0-125">**tooadd Rightscale da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22bf0-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="22bf0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="22bf0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22bf0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="22bf0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="22bf0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22bf0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="22bf0-133">Na caixa de pesquisa hello, digite **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-133">In hello search box, type **Rightscale**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="22bf0-135">No painel de resultados de saudação, selecione **Rightscale**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="22bf0-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22bf0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22bf0-138">Nesta seção, você configura e testa o logon único do Azure AD com o Rightscale, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="22bf0-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22bf0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Rightscale é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="22bf0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="22bf0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Rightscale precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="22bf0-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="22bf0-141">Rightscale, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="22bf0-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="22bf0-142">tooconfigure e teste de logon único do AD do Azure com Rightscale, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="22bf0-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="22bf0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="22bf0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="22bf0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22bf0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22bf0-145">**[Criar um usuário de teste Rightscale](#creating-a-rightscale-test-user)**  -toohave um equivalente do Britta Simon em Rightscale é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="22bf0-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="22bf0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="22bf0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22bf0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="22bf0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22bf0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="22bf0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22bf0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Rightscale.</span><span class="sxs-lookup"><span data-stu-id="22bf0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="22bf0-150">**tooconfigure AD do Azure-logon único com Rightscale, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22bf0-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="22bf0-151">Em Olá portal do Azure, Olá **Rightscale** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="22bf0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="22bf0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="22bf0-155">Em Olá **Rightscale domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP** você não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="22bf0-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="22bf0-157">Em Olá **Rightscale domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="22bf0-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="22bf0-159">a.</span><span class="sxs-lookup"><span data-stu-id="22bf0-159">a.</span></span> <span data-ttu-id="22bf0-160">Clique em Olá **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="22bf0-161">b.</span><span class="sxs-lookup"><span data-stu-id="22bf0-161">b.</span></span> <span data-ttu-id="22bf0-162">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="22bf0-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="22bf0-163">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="22bf0-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="22bf0-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="22bf0-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="22bf0-167">Em Olá **Rightscale configuração** seção, clique em **configurar Rightscale** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="22bf0-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="22bf0-168">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="22bf0-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="22bf0-169">![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="22bf0-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="22bf0-170">tooget SSO configurado para o seu aplicativo, você precisa em toosign tooyour RightScale locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="22bf0-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="22bf0-171">a.</span><span class="sxs-lookup"><span data-stu-id="22bf0-171">a.</span></span> <span data-ttu-id="22bf0-172">No menu de saudação na parte superior do hello, clique Olá **configurações** guia e selecione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="22bf0-174">b.</span><span class="sxs-lookup"><span data-stu-id="22bf0-174">b.</span></span> <span data-ttu-id="22bf0-175">Clique em hello "**novo**" botão tooadd **seus provedores de identidade SAML**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="22bf0-177">c.</span><span class="sxs-lookup"><span data-stu-id="22bf0-177">c.</span></span> <span data-ttu-id="22bf0-178">Na caixa de texto de saudação do **nome de exibição**, insira o nome da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="22bf0-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="22bf0-180">d.</span><span class="sxs-lookup"><span data-stu-id="22bf0-180">d.</span></span> <span data-ttu-id="22bf0-181">Selecione **usando uma dica de descoberta SSO iniciado permitir RightScale** e entrada seu **nome de domínio** em Olá abaixo da caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="22bf0-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="22bf0-183">e.</span><span class="sxs-lookup"><span data-stu-id="22bf0-183">e.</span></span> <span data-ttu-id="22bf0-184">Cole o valor de saudação do **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure em **o ponto de extremidade do SAML SSO** em RightScale.</span><span class="sxs-lookup"><span data-stu-id="22bf0-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="22bf0-186">f.</span><span class="sxs-lookup"><span data-stu-id="22bf0-186">f.</span></span> <span data-ttu-id="22bf0-187">Cole o valor de saudação do **ID da entidade SAML** que você copiou do portal do Azure em **EntityID SAML** em RightScale.</span><span class="sxs-lookup"><span data-stu-id="22bf0-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="22bf0-189">g.</span><span class="sxs-lookup"><span data-stu-id="22bf0-189">g.</span></span> <span data-ttu-id="22bf0-190">Clique em **navegador** certificado de saudação do botão tooupload que baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="22bf0-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="22bf0-192">h.</span><span class="sxs-lookup"><span data-stu-id="22bf0-192">h.</span></span> <span data-ttu-id="22bf0-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="22bf0-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="22bf0-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="22bf0-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="22bf0-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="22bf0-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="22bf0-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22bf0-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="22bf0-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="22bf0-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="22bf0-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22bf0-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="22bf0-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="22bf0-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22bf0-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22bf0-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="22bf0-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22bf0-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="22bf0-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22bf0-209">a.</span><span class="sxs-lookup"><span data-stu-id="22bf0-209">a.</span></span> <span data-ttu-id="22bf0-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22bf0-211">b.</span><span class="sxs-lookup"><span data-stu-id="22bf0-211">b.</span></span> <span data-ttu-id="22bf0-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="22bf0-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22bf0-213">c.</span><span class="sxs-lookup"><span data-stu-id="22bf0-213">c.</span></span> <span data-ttu-id="22bf0-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="22bf0-215">d.</span><span class="sxs-lookup"><span data-stu-id="22bf0-215">d.</span></span> <span data-ttu-id="22bf0-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="22bf0-217">Criando um usuário de teste do Rightscale</span><span class="sxs-lookup"><span data-stu-id="22bf0-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="22bf0-218">Nesta seção, você criará um usuário chamado Brenda Fernandes no RightScale.</span><span class="sxs-lookup"><span data-stu-id="22bf0-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="22bf0-219">Trabalhar com [equipe de suporte do cliente Rightscale](mailto:support@rightscale.com) tooadd usuários de saudação na plataforma de RightScale hello.</span><span class="sxs-lookup"><span data-stu-id="22bf0-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="22bf0-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="22bf0-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRightscale.</span><span class="sxs-lookup"><span data-stu-id="22bf0-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="22bf0-223">**tooassign Britta Simon tooRightscale, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22bf0-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="22bf0-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="22bf0-226">Na lista de aplicativos hello, selecione **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-226">In hello applications list, select **Rightscale**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="22bf0-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="22bf0-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="22bf0-230">Click **Add** button.</span></span> <span data-ttu-id="22bf0-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22bf0-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="22bf0-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="22bf0-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="22bf0-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22bf0-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22bf0-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22bf0-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22bf0-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="22bf0-236">Testing single sign-on</span></span>

<span data-ttu-id="22bf0-237">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="22bf0-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="22bf0-238">Quando você clica em bloco RightScale Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour RightScale aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22bf0-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22bf0-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="22bf0-239">Additional resources</span></span>

* [<span data-ttu-id="22bf0-240">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="22bf0-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22bf0-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="22bf0-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

