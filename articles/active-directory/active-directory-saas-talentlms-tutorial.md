---
title: "Tutorial: integração do Azure Active Directory com o TalentLMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="72895-103">Tutorial: integração do Azure Active Directory com o TalentLMS</span><span class="sxs-lookup"><span data-stu-id="72895-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="72895-104">Neste tutorial, você aprenderá como toointegrate TalentLMS com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="72895-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72895-105">Integrando o TalentLMS com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72895-106">Você pode controlar no AD do Azure que tenha acesso tooTalentLMS</span><span class="sxs-lookup"><span data-stu-id="72895-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="72895-107">Você pode habilitar seus usuários tooautomatically get conectado tooTalentLMS (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72895-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="72895-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72895-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72895-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72895-110">Prerequisites</span></span>

<span data-ttu-id="72895-111">tooconfigure integração do AD do Azure com o TalentLMS, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="72895-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72895-113">Uma assinatura habilitada para logon único do TalentLMS</span><span class="sxs-lookup"><span data-stu-id="72895-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72895-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="72895-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72895-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="72895-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72895-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="72895-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72895-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72895-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72895-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="72895-118">Scenario description</span></span>
<span data-ttu-id="72895-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="72895-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72895-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="72895-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72895-121">Adicionando TalentLMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="72895-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="72895-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="72895-123">Adicionando TalentLMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="72895-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="72895-124">integração de saudação tooconfigure do TalentLMS no AD do Azure, você precisa tooadd TalentLMS da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="72895-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72895-125">**tooadd TalentLMS da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72895-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72895-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="72895-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="72895-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="72895-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72895-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72895-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="72895-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72895-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="72895-133">Na caixa de pesquisa hello, digite **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="72895-133">In hello search box, type **TalentLMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="72895-135">No painel de resultados de saudação, selecione **TalentLMS**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="72895-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72895-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72895-138">Nesta seção, você configurará e testará o logon único do Azure AD com o TalentLMS, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="72895-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="72895-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no TalentLMS é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="72895-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="72895-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TalentLMS precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="72895-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="72895-141">No TalentLMS, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="72895-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72895-142">tooconfigure e teste de logon único do AD do Azure com o TalentLMS, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72895-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="72895-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72895-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72895-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72895-145">**[Criar um usuário de teste do TalentLMS](#creating-a-talentlms-test-user)**  -toohave um equivalente do Britta Simon no TalentLMS é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="72895-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72895-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="72895-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72895-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="72895-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72895-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="72895-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72895-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="72895-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="72895-150">**tooconfigure AD do Azure-logon único com o TalentLMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72895-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="72895-151">Em Olá portal do Azure, Olá **TalentLMS** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="72895-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="72895-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="72895-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="72895-155">Em Olá **TalentLMS domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="72895-157">a.</span><span class="sxs-lookup"><span data-stu-id="72895-157">a.</span></span> <span data-ttu-id="72895-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="72895-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="72895-159">b.</span><span class="sxs-lookup"><span data-stu-id="72895-159">b.</span></span> <span data-ttu-id="72895-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="72895-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72895-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="72895-161">These values are not real.</span></span> <span data-ttu-id="72895-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="72895-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="72895-163">Entre em contato com [equipe de suporte do cliente TalentLMS](https://www.talentlms.com/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="72895-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="72895-164">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** valor de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="72895-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="72895-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="72895-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72895-168">Em Olá **TalentLMS configuração** seção, clique em **configurar TalentLMS** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="72895-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="72895-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="72895-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="72895-171">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour TalentLMS como um administrador.</span><span class="sxs-lookup"><span data-stu-id="72895-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="72895-172">Em Olá **conta e configurações** seção, clique em Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="72895-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="72895-173">![Conta e Configurações](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Conta e Configurações")</span><span class="sxs-lookup"><span data-stu-id="72895-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="72895-174">Clique em **SSO (Logon Único)**.</span><span class="sxs-lookup"><span data-stu-id="72895-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="72895-175">Olá seção de logon único, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="72895-176">![Logon Único](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="72895-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="72895-177">a.</span><span class="sxs-lookup"><span data-stu-id="72895-177">a.</span></span> <span data-ttu-id="72895-178">De saudação **tipo de integração de SSO** lista, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="72895-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="72895-179">b.</span><span class="sxs-lookup"><span data-stu-id="72895-179">b.</span></span> <span data-ttu-id="72895-180">Em hello **provedor de identidade (IDP)** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72895-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="72895-181">c.</span><span class="sxs-lookup"><span data-stu-id="72895-181">c.</span></span> <span data-ttu-id="72895-182">Saudação de colar **impressão digital** valor no portal do Azure em Olá **impressão digital do certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="72895-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="72895-183">d.</span><span class="sxs-lookup"><span data-stu-id="72895-183">d.</span></span>  <span data-ttu-id="72895-184">Em Olá **URL de logon remoto** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72895-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="72895-185">e.</span><span class="sxs-lookup"><span data-stu-id="72895-185">e.</span></span> <span data-ttu-id="72895-186">Em Olá **URL de logout remoto** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72895-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="72895-187">f.</span><span class="sxs-lookup"><span data-stu-id="72895-187">f.</span></span> <span data-ttu-id="72895-188">Preencha o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="72895-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="72895-189">Em Olá **TargetedID** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="72895-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="72895-190">Em Olá **nome** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="72895-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="72895-191">Em Olá **Sobrenome** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="72895-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="72895-192">Em Olá **Email** caixa de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="72895-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="72895-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="72895-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="72895-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="72895-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72895-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="72895-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72895-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72895-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72895-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="72895-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72895-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="72895-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72895-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72895-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="72895-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72895-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="72895-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72895-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="72895-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72895-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72895-209">a.</span><span class="sxs-lookup"><span data-stu-id="72895-209">a.</span></span> <span data-ttu-id="72895-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72895-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72895-211">b.</span><span class="sxs-lookup"><span data-stu-id="72895-211">b.</span></span> <span data-ttu-id="72895-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72895-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72895-213">c.</span><span class="sxs-lookup"><span data-stu-id="72895-213">c.</span></span> <span data-ttu-id="72895-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="72895-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="72895-215">d.</span><span class="sxs-lookup"><span data-stu-id="72895-215">d.</span></span> <span data-ttu-id="72895-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="72895-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="72895-217">Criação de um usuário de teste do TalentLMS</span><span class="sxs-lookup"><span data-stu-id="72895-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="72895-218">tooenable AD do Azure usuários toolog em tooTalentLMS, eles devem ser provisionados no TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="72895-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="72895-219">No caso de saudação do TalentLMS, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="72895-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="72895-220">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72895-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="72895-221">Faça logon no tooyour **TalentLMS** locatário.</span><span class="sxs-lookup"><span data-stu-id="72895-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="72895-222">Clique em **Usuários** e em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="72895-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="72895-223">Em Olá **adicionar usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72895-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="72895-224">![Adicionar Usuário](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="72895-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="72895-225">a.</span><span class="sxs-lookup"><span data-stu-id="72895-225">a.</span></span> <span data-ttu-id="72895-226">Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="72895-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="72895-227">b.</span><span class="sxs-lookup"><span data-stu-id="72895-227">b.</span></span> <span data-ttu-id="72895-228">Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="72895-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="72895-229">c.</span><span class="sxs-lookup"><span data-stu-id="72895-229">c.</span></span> <span data-ttu-id="72895-230">Em Olá **endereço de Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="72895-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="72895-231">d.</span><span class="sxs-lookup"><span data-stu-id="72895-231">d.</span></span> <span data-ttu-id="72895-232">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="72895-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="72895-233">Você pode usar qualquer ferramenta de criação outros TalentLMS usuário conta ou APIs fornecidas pelo TalentLMS tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="72895-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="72895-234">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="72895-235">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTalentLMS.</span><span class="sxs-lookup"><span data-stu-id="72895-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="72895-237">**tooassign Britta Simon tooTalentLMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72895-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="72895-238">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72895-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="72895-240">Na lista de aplicativos hello, selecione **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="72895-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="72895-242">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="72895-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="72895-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="72895-244">Click **Add** button.</span></span> <span data-ttu-id="72895-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72895-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="72895-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="72895-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72895-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72895-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72895-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72895-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72895-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="72895-250">Testing single sign-on</span></span>

<span data-ttu-id="72895-251">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="72895-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="72895-252">Quando você clica em Olá TalentLMS bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo do TalentLMS</span><span class="sxs-lookup"><span data-stu-id="72895-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72895-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="72895-253">Additional resources</span></span>

* [<span data-ttu-id="72895-254">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="72895-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72895-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72895-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

