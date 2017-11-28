---
title: "Tutorial: Integração do Azure Active Directory ao EverBridge | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="bd407-103">Tutorial: integração do Azure Active Directory ao Everbridge</span><span class="sxs-lookup"><span data-stu-id="bd407-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="bd407-104">Neste tutorial, você aprenderá como toointegrate EverBridge com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="bd407-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd407-105">Integrando EverBridge com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd407-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd407-106">Você pode controlar no AD do Azure que tenha acesso tooEverBridge</span><span class="sxs-lookup"><span data-stu-id="bd407-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="bd407-107">Você pode habilitar seu usuários tooautomatically get conectado tooEverBridge (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd407-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd407-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd407-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd407-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bd407-110">Prerequisites</span></span>

<span data-ttu-id="bd407-111">tooconfigure integração do AD do Azure com EverBridge, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd407-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="bd407-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd407-113">Uma assinatura do EverBridge com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="bd407-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd407-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bd407-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd407-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bd407-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd407-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bd407-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd407-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd407-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd407-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bd407-118">Scenario description</span></span>
<span data-ttu-id="bd407-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bd407-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd407-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="bd407-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd407-121">Adicionando EverBridge da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bd407-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="bd407-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="bd407-123">Adicionando EverBridge da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bd407-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="bd407-124">integração de saudação tooconfigure de EverBridge no AD do Azure, você precisa tooadd EverBridge da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bd407-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd407-125">**tooadd EverBridge da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd407-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd407-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bd407-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd407-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bd407-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd407-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bd407-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="bd407-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd407-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="bd407-133">Na caixa de pesquisa hello, digite **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="bd407-133">In hello search box, type **EverBridge**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="bd407-135">No painel de resultados de saudação, selecione **EverBridge**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bd407-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd407-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd407-138">Nesta seção, você configurará e testará o logon único do Azure AD com o EverBridge com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bd407-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd407-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em EverBridge é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd407-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="bd407-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em EverBridge precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bd407-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="bd407-141">EverBridge, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd407-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd407-142">tooconfigure e teste de logon único do AD do Azure com EverBridge, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd407-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd407-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bd407-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd407-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd407-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd407-145">**[Criar um usuário de teste EverBridge](#creating-an-everbridge-test-user)**  -toohave um equivalente do Britta Simon em EverBridge é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="bd407-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd407-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="bd407-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd407-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="bd407-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd407-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd407-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd407-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo EverBridge.</span><span class="sxs-lookup"><span data-stu-id="bd407-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="bd407-150">**tooconfigure AD do Azure-logon único com EverBridge, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd407-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd407-151">Em Olá portal do Azure, Olá **EverBridge** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="bd407-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="bd407-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="bd407-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="bd407-155">Em Olá **EverBridge domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd407-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="bd407-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd407-157">a.</span></span> <span data-ttu-id="bd407-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bd407-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="bd407-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd407-159">b.</span></span> <span data-ttu-id="bd407-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="bd407-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd407-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="bd407-161">These values are not real.</span></span> <span data-ttu-id="bd407-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd407-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="bd407-163">Entre em contato com [EverBridge a equipe de suporte](mailto:support@everbridge.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="bd407-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="bd407-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bd407-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="bd407-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bd407-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd407-168">Em Olá **EverBridge configuração** seção, clique em **configurar EverBridge** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="bd407-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bd407-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="bd407-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="bd407-171">tooget SSO configurado para o seu aplicativo, você precisa em toosign tooyour Everbridge locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="bd407-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="bd407-172">No menu de saudação na parte superior do hello, clique Olá **configurações** guia e selecione **Single Sign-On** em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="bd407-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="bd407-174">a.</span><span class="sxs-lookup"><span data-stu-id="bd407-174">a.</span></span> <span data-ttu-id="bd407-175">Em Olá **nome** caixa de texto, nome de saudação do tipo do provedor de identificador (por exemplo: o nome da empresa).</span><span class="sxs-lookup"><span data-stu-id="bd407-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="bd407-176">b.</span><span class="sxs-lookup"><span data-stu-id="bd407-176">b.</span></span> <span data-ttu-id="bd407-177">Em Olá **nome da API** caixa de texto Nome do tipo hello da API.</span><span class="sxs-lookup"><span data-stu-id="bd407-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="bd407-178">c.</span><span class="sxs-lookup"><span data-stu-id="bd407-178">c.</span></span> <span data-ttu-id="bd407-179">Clique em **Escolher arquivo** botão tooupload Olá arquivo de metadados que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd407-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="bd407-180">d.</span><span class="sxs-lookup"><span data-stu-id="bd407-180">d.</span></span> <span data-ttu-id="bd407-181">No hello local da identidade do SAML, selecione **identidade está no elemento NameIdentifier Olá Olá declaração assunto**.</span><span class="sxs-lookup"><span data-stu-id="bd407-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="bd407-182">e.</span><span class="sxs-lookup"><span data-stu-id="bd407-182">e.</span></span> <span data-ttu-id="bd407-183">Em Olá **URL de logon do provedor de identidade** caixa de texto, colar Olá valor da URL do SSO do SAML do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd407-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="bd407-185">f.</span><span class="sxs-lookup"><span data-stu-id="bd407-185">f.</span></span> <span data-ttu-id="bd407-186">No serviço de provedor de associação de solicitação iniciada de hello, selecione **redirecionamento HTTP**.</span><span class="sxs-lookup"><span data-stu-id="bd407-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="bd407-187">g.</span><span class="sxs-lookup"><span data-stu-id="bd407-187">g.</span></span> <span data-ttu-id="bd407-188">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="bd407-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="bd407-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="bd407-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd407-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="bd407-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd407-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd407-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd407-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd407-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd407-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="bd407-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd407-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd407-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bd407-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd407-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bd407-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd407-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd407-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd407-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd407-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd407-204">a.</span><span class="sxs-lookup"><span data-stu-id="bd407-204">a.</span></span> <span data-ttu-id="bd407-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd407-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd407-206">b.</span><span class="sxs-lookup"><span data-stu-id="bd407-206">b.</span></span> <span data-ttu-id="bd407-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd407-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd407-208">c.</span><span class="sxs-lookup"><span data-stu-id="bd407-208">c.</span></span> <span data-ttu-id="bd407-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="bd407-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd407-210">d.</span><span class="sxs-lookup"><span data-stu-id="bd407-210">d.</span></span> <span data-ttu-id="bd407-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bd407-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="bd407-212">Criar um usuário de teste do EverBridge</span><span class="sxs-lookup"><span data-stu-id="bd407-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="bd407-213">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Everbridge.</span><span class="sxs-lookup"><span data-stu-id="bd407-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="bd407-214">Trabalhar com [EverBridge a equipe de suporte](mailto:support@everbridge.com) tooadd usuários de saudação na plataforma de Everbridge hello.</span><span class="sxs-lookup"><span data-stu-id="bd407-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd407-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd407-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEverBridge.</span><span class="sxs-lookup"><span data-stu-id="bd407-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="bd407-218">**tooassign Britta Simon tooEverBridge, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bd407-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd407-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bd407-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bd407-221">Na lista de aplicativos hello, selecione **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="bd407-221">In hello applications list, select **EverBridge**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="bd407-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bd407-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="bd407-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bd407-225">Click **Add** button.</span></span> <span data-ttu-id="bd407-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd407-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="bd407-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd407-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd407-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd407-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd407-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bd407-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd407-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="bd407-231">Testing single sign-on</span></span>

<span data-ttu-id="bd407-232">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="bd407-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd407-233">Quando você clica em bloco Everbridge Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Everbridge aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd407-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd407-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bd407-234">Additional resources</span></span>

* [<span data-ttu-id="bd407-235">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bd407-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd407-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd407-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

