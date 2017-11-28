---
title: "Tutorial: Integração do Azure Active Directory ao LockPath Keylight | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="025a8-103">Tutorial: Integração do Azure Active Directory ao LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="025a8-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="025a8-104">Neste tutorial, você aprenderá como toointegrate LockPath Keylight com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="025a8-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="025a8-105">Integrando LockPath Keylight com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="025a8-106">Você pode controlar no AD do Azure que tenha acesso tooLockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="025a8-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="025a8-107">Você pode habilitar seu usuários tooautomatically get conectado tooLockPath Keylight (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="025a8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="025a8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="025a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="025a8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="025a8-110">Prerequisites</span></span>

<span data-ttu-id="025a8-111">integração do AD do Azure com LockPath Keylight de tooconfigure, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="025a8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="025a8-113">Uma assinatura habilitada para logon único do LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="025a8-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="025a8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="025a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="025a8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="025a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="025a8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="025a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="025a8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="025a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="025a8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="025a8-118">Scenario description</span></span>
<span data-ttu-id="025a8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="025a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="025a8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="025a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="025a8-121">Adicionando LockPath Keylight da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="025a8-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="025a8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="025a8-123">Adicionando LockPath Keylight da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="025a8-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="025a8-124">integração de saudação tooconfigure de LockPath Keylight no AD do Azure, você precisa tooadd LockPath Keylight na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="025a8-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="025a8-125">**tooadd LockPath Keylight da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="025a8-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="025a8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="025a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="025a8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="025a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="025a8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="025a8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="025a8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="025a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="025a8-133">Na caixa de pesquisa hello, digite **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="025a8-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="025a8-135">No painel de resultados de saudação, selecione **LockPath Keylight**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="025a8-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="025a8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="025a8-138">Nesta seção, você configura e testa o logon único do Azure AD com o LockPath Keylight, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="025a8-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="025a8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LockPath Keylight é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="025a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="025a8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em LockPath Keylight precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="025a8-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="025a8-141">LockPath Keylight, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="025a8-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="025a8-142">tooconfigure e teste de logon único do AD do Azure com LockPath Keylight, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="025a8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="025a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="025a8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="025a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="025a8-145">**[Criar um usuário de teste LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave um equivalente do Britta Simon em LockPath Keylight que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="025a8-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="025a8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="025a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="025a8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="025a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="025a8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="025a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="025a8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="025a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="025a8-150">**tooconfigure AD do Azure-logon único com LockPath Keylight, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="025a8-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="025a8-151">Em Olá portal do Azure, Olá **LockPath Keylight** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="025a8-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="025a8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="025a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="025a8-155">Em Olá **LockPath Keylight domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="025a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="025a8-157">a.</span></span> <span data-ttu-id="025a8-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="025a8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="025a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="025a8-159">b.</span></span> <span data-ttu-id="025a8-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="025a8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="025a8-161">c.</span><span class="sxs-lookup"><span data-stu-id="025a8-161">c.</span></span> <span data-ttu-id="025a8-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="025a8-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="025a8-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="025a8-163">These values are not real.</span></span> <span data-ttu-id="025a8-164">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="025a8-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="025a8-165">Entre em contato com [equipe de suporte do cliente de Keylight LockPath](https://www.lockpath.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="025a8-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="025a8-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="025a8-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="025a8-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="025a8-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="025a8-170">Em Olá **LockPath Keylight configuração** seção, clique em **configurar LockPath Keylight** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="025a8-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="025a8-171">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="025a8-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="025a8-173">tooenable SSO no LockPath Keylight, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="025a8-174">a.</span><span class="sxs-lookup"><span data-stu-id="025a8-174">a.</span></span> <span data-ttu-id="025a8-175">Logon tooyour LockPath Keylight conta como administrador.</span><span class="sxs-lookup"><span data-stu-id="025a8-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="025a8-176">b.</span><span class="sxs-lookup"><span data-stu-id="025a8-176">b.</span></span> <span data-ttu-id="025a8-177">No menu de saudação na parte superior de saudação, clique em **pessoa**e selecione **Keylight instalação**.</span><span class="sxs-lookup"><span data-stu-id="025a8-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="025a8-179">c.</span><span class="sxs-lookup"><span data-stu-id="025a8-179">c.</span></span> <span data-ttu-id="025a8-180">Em treeview Olá Olá esquerda, clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="025a8-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="025a8-182">d.</span><span class="sxs-lookup"><span data-stu-id="025a8-182">d.</span></span> <span data-ttu-id="025a8-183">Em Olá **configurações SAML** caixa de diálogo, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="025a8-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="025a8-185">Em Olá **editar configurações de SAML** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="025a8-187">a.</span><span class="sxs-lookup"><span data-stu-id="025a8-187">a.</span></span> <span data-ttu-id="025a8-188">Definir **autenticação SAML** muito**Active**.</span><span class="sxs-lookup"><span data-stu-id="025a8-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="025a8-189">b.</span><span class="sxs-lookup"><span data-stu-id="025a8-189">b.</span></span> <span data-ttu-id="025a8-190">Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="025a8-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="025a8-191">c.</span><span class="sxs-lookup"><span data-stu-id="025a8-191">c.</span></span> <span data-ttu-id="025a8-192">Saudação de colar **URL do serviço de logon único** valor que você copiou de saudação portal do Azure em hello **URL de Logout do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="025a8-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="025a8-193">d.</span><span class="sxs-lookup"><span data-stu-id="025a8-193">d.</span></span> <span data-ttu-id="025a8-194">Clique em **Escolher arquivo** tooselect sua LockPath Keylight baixado do certificado e, em seguida, clique em **abrir** certificado de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="025a8-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="025a8-195">e.</span><span class="sxs-lookup"><span data-stu-id="025a8-195">e.</span></span> <span data-ttu-id="025a8-196">Definir **local de Id de usuário SAML** muito**elemento NameIdentifier da declaração do assunto Olá**.</span><span class="sxs-lookup"><span data-stu-id="025a8-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="025a8-197">f.</span><span class="sxs-lookup"><span data-stu-id="025a8-197">f.</span></span> <span data-ttu-id="025a8-198">Fornecer Olá **Keylight provedor** usando saudação padrão a seguir: **https://&lt;CompanyName&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="025a8-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="025a8-199">g.</span><span class="sxs-lookup"><span data-stu-id="025a8-199">g.</span></span> <span data-ttu-id="025a8-200">Definir **automática provisionar usuários** muito**Active**.</span><span class="sxs-lookup"><span data-stu-id="025a8-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="025a8-201">h.</span><span class="sxs-lookup"><span data-stu-id="025a8-201">h.</span></span> <span data-ttu-id="025a8-202">Definir **tipo de conta de provisionamento automático** muito**usuário completo**.</span><span class="sxs-lookup"><span data-stu-id="025a8-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="025a8-203">i.</span><span class="sxs-lookup"><span data-stu-id="025a8-203">i.</span></span> <span data-ttu-id="025a8-204">Defina **Provisionar função de segurança automaticamente** e selecione **Usuário Padrão com SAML**.</span><span class="sxs-lookup"><span data-stu-id="025a8-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="025a8-205">j.</span><span class="sxs-lookup"><span data-stu-id="025a8-205">j.</span></span> <span data-ttu-id="025a8-206">Defina **Provisionar configuração de segurança automaticamente** e selecione **Configuração de Usuário Padrão**.</span><span class="sxs-lookup"><span data-stu-id="025a8-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="025a8-207">k.</span><span class="sxs-lookup"><span data-stu-id="025a8-207">k.</span></span> <span data-ttu-id="025a8-208">Em Olá **atributo de Email** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="025a8-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="025a8-209">l.</span><span class="sxs-lookup"><span data-stu-id="025a8-209">l.</span></span> <span data-ttu-id="025a8-210">Em Olá **atributo de nome** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="025a8-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="025a8-211">m.</span><span class="sxs-lookup"><span data-stu-id="025a8-211">m.</span></span> <span data-ttu-id="025a8-212">Em Olá **atributo de Sobrenome** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="025a8-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="025a8-213">n.</span><span class="sxs-lookup"><span data-stu-id="025a8-213">n.</span></span> <span data-ttu-id="025a8-214">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="025a8-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="025a8-215">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="025a8-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="025a8-216">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="025a8-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="025a8-217">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="025a8-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="025a8-218">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="025a8-219">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="025a8-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="025a8-221">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="025a8-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="025a8-222">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="025a8-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="025a8-224">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="025a8-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="025a8-226">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="025a8-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="025a8-228">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="025a8-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="025a8-230">a.</span><span class="sxs-lookup"><span data-stu-id="025a8-230">a.</span></span> <span data-ttu-id="025a8-231">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="025a8-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="025a8-232">b.</span><span class="sxs-lookup"><span data-stu-id="025a8-232">b.</span></span> <span data-ttu-id="025a8-233">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="025a8-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="025a8-234">c.</span><span class="sxs-lookup"><span data-stu-id="025a8-234">c.</span></span> <span data-ttu-id="025a8-235">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="025a8-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="025a8-236">d.</span><span class="sxs-lookup"><span data-stu-id="025a8-236">d.</span></span> <span data-ttu-id="025a8-237">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="025a8-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="025a8-238">Criando um usuário de teste do LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="025a8-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="025a8-239">Nesta seção, você cria um usuário chamado Brenda Fernandes no LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="025a8-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="025a8-240">O LockPath Keylight dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="025a8-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="025a8-241">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="025a8-241">There is no action item for you in this section.</span></span> <span data-ttu-id="025a8-242">Um novo usuário é criado ao acessar LockPath Keylight se o usuário Olá ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="025a8-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="025a8-243">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do cliente de Keylight LockPath](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="025a8-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="025a8-244">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="025a8-245">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="025a8-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="025a8-247">**tooassign tooLockPath Britta Simon Keylight, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="025a8-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="025a8-248">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="025a8-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="025a8-250">Na lista de aplicativos hello, selecione **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="025a8-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="025a8-252">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="025a8-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="025a8-254">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="025a8-254">Click **Add** button.</span></span> <span data-ttu-id="025a8-255">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="025a8-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="025a8-257">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="025a8-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="025a8-258">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="025a8-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="025a8-259">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="025a8-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="025a8-260">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="025a8-260">Testing single sign-on</span></span>

<span data-ttu-id="025a8-261">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="025a8-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="025a8-262">Quando você clica em Olá LockPath Keylight lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour LockPath Keylight aplicativo.</span><span class="sxs-lookup"><span data-stu-id="025a8-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="025a8-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="025a8-263">Additional resources</span></span>

* [<span data-ttu-id="025a8-264">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="025a8-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="025a8-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="025a8-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

